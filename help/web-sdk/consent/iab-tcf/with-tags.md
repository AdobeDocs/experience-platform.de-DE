---
title: Integrieren der IAB TCF 2.0-Unterstützung mithilfe von Tags und der Experience Platform Web SDK-Erweiterung
description: Erfahren Sie, wie Sie das IAB TCF 2.0-Einverständnis mit Tags und der Adobe Experience Platform Web SDK-Erweiterung einrichten.
exl-id: dc0e6b68-8257-4862-9fc4-50b370ef204f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 0%

---

# Integrieren der IAB TCF 2.0-Unterstützung mithilfe von Tags und der Experience Platform Web SDK-Erweiterung

Adobe Experience Platform Web SDK unterstützt das Interactive Advertising Bureau Transparency &amp; Consent Framework, Version 2.0 (IAB TCF 2.0). In diesem Handbuch erfahren Sie, wie Sie mithilfe der Tag-Erweiterung &quot;Adobe Experience Platform Web SDK&quot; eine Tag-Eigenschaft für das Senden von IAB TCF 2.0-Einverständnisinformationen an Adobe einrichten.

Wenn Sie keine Tags verwenden möchten, lesen Sie bitte das Handbuch unter [Verwenden von IAB TCF 2.0 ohne Tags](./without-tags.md).

## Erste Schritte

Um IAB TCF 2.0 mit Tags und der Experience Platform Web SDK-Erweiterung verwenden zu können, benötigen Sie ein XDM-Schema und einen Datensatz.

Darüber hinaus setzt dieses Handbuch ein Grundverständnis für Adobe Experience Platform Web SDK voraus. Zur schnellen Auffrischung lesen Sie bitte die [Übersicht über Adobe Experience Platform Web SDK](../../home.md) und die Dokumentation [Häufig gestellte Fragen](../../faq.md) .

## Festlegen des Standardeinverständnisses

Innerhalb der Erweiterungskonfiguration gibt es eine Einstellung für das standardmäßige Einverständnis. Dies steuert das Verhalten von Kunden, die kein Einverständnis-Cookie haben. Wenn Sie Erlebnisereignisse für Kunden in die Warteschlange stellen möchten, die kein Einverständnis-Cookie haben, setzen Sie dies auf `pending`. Wenn Sie Erlebnisereignisse für Kunden verwerfen möchten, die kein Einverständnis-Cookie haben, setzen Sie dies auf `out`. Sie können auch ein Datenelement verwenden, um den standardmäßigen Einverständniswert dynamisch festzulegen. Weitere Informationen finden Sie unter [`defaultConsent`](/help/web-sdk/commands/configure/defaultconsent.md) .

## Aktualisieren des Profils mit Einverständnisinformationen {#consent-code-1}

Um die Aktion &quot;[`setConsent`](/help/web-sdk/commands/setconsent.md)&quot; aufzurufen, wenn sich die Einverständnisvoreinstellungen Ihrer Kunden geändert haben, erstellen Sie eine Tag-Regel. Fügen Sie zunächst ein neues Ereignis hinzu und wählen Sie den Ereignistyp „Benutzerdefinierter Code“ der Core-Erweiterung aus.

Verwenden Sie das folgende Codebeispiel für Ihr neues Ereignis:

```javascript
// Wait for window.__tcfapi to be defined, then trigger when the customer has completed their consent and preferences.
function addEventListener() {
  if (window.__tcfapi) {
    window.__tcfapi("addEventListener", 2, function (tcData, success) {
      if (success && tcData.eventStatus === "useractioncomplete") {
        // save the tcData.tcString in a data element
        _satellite.setVar("IAB TCF Consent String", tcData.tcString);
        _satellite.setVar("IAB TCF Consent GDPR", tcData.gdprApplies);
        trigger();
      }
    });
  } else {
    // window.__tcfapi wasn't defined. Check again in 100 milliseconds
    setTimeout(addEventListener, 100);
  }
}
addEventListener();
```

Dieser benutzerdefinierte Code hat zwei Aufgaben:

* Legt zwei Datenelemente fest, eines mit der Einverständniszeichenfolge und eines mit der `gdprApplies`. Dies ist später beim Ausfüllen der Aktion „Einverständnis festlegen“ nützlich.

* Trigger bei der Regel, wenn sich die Einverständnisvoreinstellungen geändert haben. Die Aktion „Einverständnis festlegen“ sollte immer verwendet werden, wenn sich die Einverständnisvoreinstellungen geändert haben. Fügen Sie eine Aktion „Einverständnis festlegen“ in die Erweiterung ein und füllen Sie das Formular wie folgt aus:

* Standard: „IAB TCF“
* Version: „2.0“
* Wert: &quot;%IAB TCF Consent String%&quot;
* Es gilt die DSGVO: &quot;%IAB TCF Consent GDPR%&quot;

![IAB-Einverständnisaktion festlegen](../../assets/consent/iab-tcf/with-launch/iab-action.png)

>[!IMPORTANT]
>
>Sie können diese Datenelemente nicht mit der Datenelementauswahl auswählen, da sie mit benutzerdefiniertem Code erstellt wurden. Sie müssen den Datenelementnamen mit den Prozentzeichen eingeben. Dieser Code aktualisiert das Profil Ihres Kunden bei jeder Änderung mit seinen neuen Einverständnisvoreinstellungen. Darüber hinaus gibt der Server einen Cookie-Wert zurück, der verhindern könnte, dass Adobe Experience Platform Web SDK Erlebnisereignisse aufzeichnet.

## Erstellen eines XDM-Datenelements für Erlebnisereignisse

Die Einverständniszeichenfolge sollte in das XDM-Erlebnisereignis aufgenommen werden. Verwenden Sie dazu das Datenelement XDM-Objekt . Erstellen Sie zunächst ein neues XDM-Objektdatenelement oder verwenden Sie ein bereits erstelltes zum Senden von Ereignissen. Wenn Sie Ihrem Schema die Feldergruppe des Experience-Ereignis-Datenschutzschemas hinzugefügt haben, sollten Sie über einen `consentStrings` Schlüssel im XDM-Objekt verfügen.

1. Wählen Sie **[!UICONTROL consentStrings]** aus.

1. Wählen Sie **[!UICONTROL Einzelne Elemente angeben]** und wählen Sie **[!UICONTROL Element hinzufügen]**.

1. Erweitern Sie die **[!UICONTROL consentString]**, erweitern Sie das erste Element und füllen Sie dann die folgenden Werte aus:

* `consentStandard`: IAB TCF
* `consentStandardVersion`: 2.0
* `consentStringValue`: %IAB TCF-Einverständniszeichenfolge%
* `gdprApplies`: %IAB TCF Consent GDPR%

>[!IMPORTANT]
>
>Sie können diese Datenelemente nicht mit der Datenelementauswahl auswählen, da sie mit benutzerdefiniertem Code erstellt wurden. Sie müssen den Datenelementnamen mit den Prozentzeichen eingeben.

## Senden eines ersten Erlebnisereignisses mit IAB TCF 2.0-Einverständnisinformationen

Wenn das anfängliche Erlebnisereignis auf der Seite durch ein Seitenladeereignis ausgelöst wird, wurde die Einverständniszeichenfolge möglicherweise noch nicht geladen. Diese Regel soll Ihr aktuelles Seitenladeereignis ersetzen. Um sicherzustellen, dass die Einverständnisinformationen zuerst geladen werden, erstellen Sie eine neue Regel und fügen Sie den folgenden Code als benutzerspezifisches Code-Ereignis hinzu:

```javascript
// Wait for window.__tcfapi to be defined, then trigger when there is a consent string
function addEventListener() {
  if (window.__tcfapi) {
    window.__tcfapi("addEventListener", 2, function (tcData, success) {
      if (success && (tcData.eventStatus === "useractioncomplete" || tcData.eventStatus === "tcloaded")) {
        // save the tcData.tcString in a data element
        _satellite.setVar("IAB TCF Consent String", tcData.tcString);
        _satellite.setVar("IAB TCF GDPR Applies", tcData.gdprApplies);
        trigger();
      }
    });
  } else {
    // window.__tcfapi wasn"t defined. Check again in 100 milliseconds
    setTimeout(addEventListener, 100);
  }
}
addEventListener();
```

Dieser Code ist identisch mit dem vorherigen benutzerdefinierten Code, mit dem Unterschied, dass sowohl `useractioncomplete`- als auch `tcloaded`-Ereignisse behandelt werden. Der [vorherige benutzerspezifische Code](#consent-code-1) ist nur dann Trigger, wenn der Kunde seine Voreinstellungen zum ersten Mal auswählt. Dieser Code ist auch dann Trigger, wenn der Kunde seine Präferenzen bereits ausgewählt hat. Beispielsweise beim zweiten Laden der Seite.

Fügen Sie die Aktion „Ereignis senden“ über die Experience Platform Web SDK-Erweiterung hinzu. Wählen Sie innerhalb des XDM-Felds das XDM-Datenelement aus, das Sie im vorherigen Abschnitt erstellt haben.

## Senden anderer Ereignisse mit Informationen zum IAB TCF 2.0-Einverständnis

Wenn Ereignisse nach dem ersten Erlebnisereignis ausgelöst werden, sind die beiden Datenelemente weiterhin definiert und können zum Senden der IAB-Einverständnisinformationen verwendet werden. Verwenden Sie dasselbe XDM-Datenelement, um zukünftige Ereignisse zu senden. IAB TCF 2.0-Informationen sind enthalten.

## Nächste Schritte

Nachdem Sie nun gelernt haben, wie Sie IAB TCF 2.0 mit der Experience Platform Web SDK-Erweiterung verwenden, können Sie auch eine Integration mit anderen Adobe-Lösungen wie Adobe Analytics oder Adobe Real-Time Customer Data Platform wählen. Weitere Informationen finden [ in der Übersicht zum IAB Transparency &amp; Consent Framework ](./overview.md).0 .
