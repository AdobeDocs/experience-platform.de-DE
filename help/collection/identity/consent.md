---
title: Einverständnis und Identität bei der Datenerfassung
description: Erfahren Sie, wie sich Einverständnisentscheidungen auf das Identitätsverhalten in Web SDK-Implementierungen auswirken, einschließlich ECID-Generierung, Cookie-Persistenz und Besucherkontinuität.
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '1149'
ht-degree: 2%

---

# Einverständnis und Identität bei der Datenerfassung

Einverständnis und Identität sind in Web SDK-Implementierungen eng miteinander verbunden. Wie und wann Sie Ihr Einverständnis einholen, wirkt sich direkt darauf aus, wann und ob die Web-SDK eine ECID generiert, Identitäts-Cookies setzt und Daten an die Edge Network sendet. Wenn das Einverständnis nicht sorgfältig gehandhabt wird, ist das Ergebnis häufig eine unerwartete Besucherinflation, Lücken in der Identitätskontinuität oder beides.

Auf dieser Seite wird erläutert, wie Einverständnisentscheidungen mit dem Identitätsverhalten interagieren, und es wird Anleitung zur Konfiguration Ihrer Implementierung bereitgestellt, um häufige Fehler zu vermeiden. Hintergrundinformationen dazu, wie Web SDK ECIDs, FPIDs und andere Identitätssignale verarbeitet, finden Sie unter [Identität in der Datenerfassung](./overview.md).

## Wie sich Einverständnis auf die Identität auswirkt {#how-consent-affects-identity}

Die Web-SDK verwendet sowohl die Konfigurationsvariable [`defaultConsent`](/help/collection/js/commands/configure/defaultconsent.md) als auch den Befehl [`setConsent`](/help/collection/js/commands/setconsent.md) , um zu steuern, ob Daten an die Edge Network gesendet werden. Der Einverständnisstatus bestimmt direkt, wann eine ECID generiert wird und wann Identitäts-Cookies gesetzt werden.

Die folgende Tabelle zeigt die kombinierten Auswirkungen von `defaultConsent` und `setConsent` auf die Datenerfassung, die Cookie-Einstellung und das Identitätsverhalten.

| `defaultConsent` | `setConsent` | Datenerfassung findet statt | Browser-Cookies gesetzt | Identitätsverhalten |
| --- | --- | --- | --- | --- |
| `in` | Nicht festgelegt | Ja | Ja | Bei der ersten Anfrage wird sofort eine ECID generiert. Identitäts-Cookies werden beim Laden der Seite gesetzt. |
| `in` | `in` | Ja | Ja | Die vorhandene ECID des Besuchers wird beibehalten. Das Identitätsverhalten bleibt unverändert. |
| `in` | `out` | Nein | Ja | Datenerfassung stoppt. Die vorhandenen ECID- und `kndctr_`-Identitäts-Cookies verbleiben im Browser, bis sie ablaufen. |
| `pending` | Nicht festgelegt | Nein | Nein | Es wird keine ECID generiert. Es werden keine Cookies gesetzt. Ereignisse werden lokal in die Warteschlange gestellt, bis `setConsent` aufgerufen wird. |
| `pending` | `in` | Ja | Ja | Ereignisse in der Warteschlange werden gesendet. Bei der ersten Anfrage wird eine ECID generiert und Identitäts-Cookies werden gesetzt. |
| `pending` | `out` | Nein | Ja | Warteschlangenereignisse werden verworfen. Es wird keine ECID generiert. Das Einverständnis-Cookie wird gesetzt, um die Voreinstellung des Besuchers aufzuzeichnen. |
| `out` | Nicht festgelegt | Nein | Nein | Es wird keine ECID generiert. Es werden keine Cookies gesetzt. Keine Ereignisse gesendet. |
| `out` | `in` | Ja | Ja | Bei der ersten Anfrage wird eine ECID generiert und Identitäts-Cookies werden gesetzt. |
| `out` | `out` | Nein | Ja | Es wird keine ECID generiert. Das Einverständnis-Cookie wird gesetzt, um die Voreinstellung des Besuchers aufzuzeichnen. |

>[!NOTE]
>
>Identitäts- und Einverständnis-Cookies werden auch dann gesetzt, wenn ein Besucher eine Abwahl trifft. Diese Cookies sind erforderlich, um die Voreinstellungen des Besuchers für die Datenerfassung zu berücksichtigen. Siehe [Web SDK-Cookies](https://experienceleague.adobe.com/de/docs/core-services/interface/data-collection/cookies/web-sdk), um eine vollständige Liste der Cookies zu erhalten, die von Web SDK gesetzt werden.

Wenn ein Besucher sein Einverständnis erneut erteilt, nachdem er es zuvor widerrufen hat (indem er `setConsent` nach dem `"general": "in"` mit `"general": "out"` aufruft), sendet die Web-SDK erneut Ereignisse und verwendet die vorhandene ECID aus dem Cookie, wenn sie nicht abgelaufen ist. Die Identität des Besuchers wird beibehalten.

Nachdem ein Besucher sein Einverständnis erteilt oder verweigert, behält die Web-SDK ihre Voreinstellung in einem `kndctr_` Einverständnis-Cookie bei. Beim nachfolgenden Laden der Seite liest die SDK dieses Cookie und wendet die gespeicherte Voreinstellung automatisch an. Sie müssen `setConsent` nicht erneut aufrufen, es sei denn, die Voreinstellung der Besucherin oder des Besuchers ändert sich. Beachten Sie, dass der `defaultConsent` Konfigurationswert zwischen dem Laden der Seite nicht beibehalten wird, das aufgelöste Einverständnis des Besuchers (festgelegt durch `setConsent`) jedoch nicht.

>[!NOTE]
>
>Ereignisse, die sich in der Warteschlange befinden, während das Einverständnis `pending` wird, werden im Speicher abgelegt und überleben das erneute Laden der Seite nicht. Wenn ein Besucher zu einer neuen Seite navigiert, bevor das Einverständnis aufgelöst wird, gehen Ereignisse aus der Warteschlange der vorherigen Seite verloren.

## Implementierungsmuster {#implementation-patterns}

### Opt-in-Modell (Einverständnis vor der Erfassung erforderlich) {#opt-in}

Verwenden Sie dieses Muster, wenn Vorschriften (z. B. die DSGVO) vor der Erfassung von Daten eine ausdrückliche Zustimmung erfordern.

```js
alloy("configure", {
  orgId: "YOUR_ORG_ID@AdobeOrg",
  edgeDomain: "data.example.com",
  defaultConsent: "pending"
});

// When the visitor grants consent:
alloy("setConsent", {
  consent: [{
    standard: "Adobe",
    version: "1.0",
    value: { general: "in" }
  }]
});
```

Mit diesem Muster:
* Es wird keine ECID generiert, bis das Einverständnis erteilt wird.
* Ereignisse, die vor dem Einverständnis ausgelöst werden (z. B. die anfängliche Seitenansicht), werden in die Warteschlange gestellt und gesendet, nachdem das Einverständnis erteilt wurde.
* Identitäts-Cookies werden erst nach der ersten erfolgreichen Edge Network-Anfrage gesetzt.

### Opt-out-Modell (Sammlung standardmäßig, bei Ablehnung stoppen) {#opt-out}

Verwenden Sie dieses Muster, wenn Vorschriften die Datenerfassung standardmäßig mit einer Option zum Opt-out zulassen.

```js
alloy("configure", {
  orgId: "YOUR_ORG_ID@AdobeOrg",
  edgeDomain: "data.example.com",
  defaultConsent: "in"
});

// If the visitor opts out:
alloy("setConsent", {
  consent: [{
    standard: "Adobe",
    version: "1.0",
    value: { general: "out" }
  }]
});
```

Mit diesem Muster:
* Eine ECID wird sofort beim ersten Laden der Seite generiert.
* Alle Ereignisse werden gesendet, bis der Besucher sich abmeldet.
* Nach dem Opt-out sendet der Web-SDK keine Ereignisse mehr, aber vorhandene Cookies bleiben bestehen.

## Einverständnis mit First-Party-Geräte-IDs {#consent-with-fpids}

Wenn Ihre Implementierung [Erstanbieter-Geräte-IDs (FPIDs)](./fpid.md) verwendet, wird das FPID-Cookie von Ihrem -Server unabhängig vom Einverständnisstatus der Web-SDK gesetzt. Das FPID-Cookie ist eine Kennung, die Sie in Ihrer eigenen Infrastruktur verwalten. Die FPID wird jedoch nur dann an die Edge Network gesendet, wenn die Web-SDK eine -Anfrage stellt (die durch Einverständnis geprüft wird):

* Bei `defaultConsent: "pending"` ist der FPID im Browser vorhanden, wird jedoch erst zum Testen einer ECID verwendet, wenn das Einverständnis erteilt wurde.
* Bei `defaultConsent: "in"` wird der FPID bei der ersten Anfrage verwendet und die ECID wird sofort gesendet.

Wenn Ihre Einwilligungsimplementierung erfordert, dass vor dem Einverständnis keine Kennung festgelegt wird, verzögern Sie das Setzen des FPID-Cookies, bis das Einverständnis mitgeteilt wurde. Das Einverständnis-Gating von Web SDK allein verhindert nicht, dass das FPID-Cookie gesetzt wird, da es von Ihrem Server verwaltet wird.

## Häufige Fehler {#common-pitfalls}

+++**Einverständnisbanner löscht Identitäts-Cookies**

**Problem**: Einige Einverständnisverwaltungsplattformen (CMPs) löschen alle Cookies - einschließlich `kndctr_` Identitäts-Cookies - bei der Präsentation des Einverständnisbanners, bevor der Besucher eine Entscheidung trifft. Wenn der Besucher sein Einverständnis erteilt, generiert Web SDK eine neue ECID, da die vorherige gelöscht wurde. Der Besucher wird in Berichten als neue Person angezeigt.

**Symptome**:
* Nach der Bereitstellung eines Einverständnisbanners wird ein Anstieg der Unique Visitor -Zahlen verzeichnet.
* Wiederkehrende Besucher werden jedes Mal als neue Besucher gezählt, wenn ihr Einverständnis abläuft und sie erneut mit dem Banner interagieren.

**Lösung**: Konfigurieren Sie Ihre CMP, um `kndctr_` Cookies beizubehalten. Diese Cookies sind Identitäts-Cookies, keine Tracking-Cookies - sie identifizieren das Gerät und enthalten keine Verhaltensdaten. Wenn Ihre CMP das Löschen von Cookies erfordert, fügen Sie `kndctr_` mit dem Präfix versehenen Cookies zu einer Ausschlussliste hinzu. Alternativ können Sie das Löschen von Cookies verzögern, bis der Besucher die Zustimmung explizit verweigert, anstatt sie vorzeitig zu löschen.

+++

+++**Verzögertes Einverständnis führt zu doppelter Identität**

**Problem**: Wenn `defaultConsent` auf &quot;`pending`&quot; gesetzt ist, wartet die Web-SDK auf das Einverständnis, bevor Daten gesendet werden. Wenn das Einverständnis erst spät im Lebenszyklus der Seite erteilt wird (z. B. nach einer Bannerinteraktion, durch die ein Neuladen der Seite Trigger wird), kann die folgende Sequenz Probleme verursachen:

1. Seite wird geladen. `defaultConsent: "pending"`. Web SDK sendet keine Anfragen.
2. Der Besucher erteilt die Zustimmung. CMP-Trigger laden eine Seite neu.
3. Seite wird erneut geladen. Web SDK wird mit nun erteilter Zustimmung initialisiert und generiert eine ECID.

Dieser Fluss ist normal und funktioniert ordnungsgemäß. Das Problem tritt auf, wenn die CMP oder Ihre Implementierung unbeabsichtigt Cookies zwischen den Schritten 2 und 3 löscht oder wenn die Web-SDK beim Neuladen anders konfiguriert ist.

**Lösung**: Stellen Sie sicher, dass die Web SDK-Konfiguration (insbesondere `orgId` und `defaultConsent`) beim Laden der Seite identisch ist. Wenn Ihre CMP-Trigger nach dem Einverständnis ein Neuladen durchführen, stellen Sie sicher, dass die Identitäts-Cookies das Neuladen überleben.

+++

+++**Verwenden von `defaultConsent: "in"` mit einem Einverständnisbanner**

**Problem**: Einige Implementierungen setzen `defaultConsent: "in"` und rufen dann `setConsent` mit `"general": "out"` auf, wenn der Besucher ablehnt. Bei diesem Ansatz wird eine ECID generiert und mindestens eine Anfrage gesendet, bevor die Zustimmung verweigert wird. Abhängig von Ihren rechtlichen Anforderungen entspricht diese anfängliche Datenerfassung möglicherweise nicht den Datenschutzrichtlinien Ihrer Organisation.

**Lösung**: Wenn Ihre behördliche Umgebung eine Zustimmung vor der Datenerfassung oder ECID-Generierung erfordert, verwenden Sie stattdessen `defaultConsent: "pending"`. Diese Einstellung stellt sicher, dass die Web-SDK erst dann mit der Edge Network kommuniziert, wenn das Einverständnis ausdrücklich erteilt wurde.

+++
