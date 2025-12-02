---
title: setConsent
description: Wird auf jeder Seite verwendet, um die Einverständnisvoreinstellungen Ihrer Benutzer zu verfolgen.
exl-id: d01a6ef1-4fa7-4a60-a3a1-19568b4e0d23
source-git-commit: 364b9adc406f732ea5ba450730397c4ce1bf03cf
workflow-type: tm+mt
source-wordcount: '1289'
ht-degree: 3%

---


# `setConsent`

Der Befehl `setConsent` teilt der Web-SDK mit, ob Daten gesendet (Opt-in), Daten verworfen (Opt-out) oder [`defaultConsent`](configure/defaultconsent.md) verwendet werden sollen (Einverständnis unbekannt).

Web SDK unterstützt die folgenden Standards:

* **[Adobe Standard](/help/landing/governance-privacy-security/consent/adobe/overview.md)**: Es werden sowohl 1.0- als auch 2.0-Standards unterstützt.
* **[IAB Transparency &amp; Consent Framework](/help/landing/governance-privacy-security/consent/iab/overview.md)**: Wenn Sie diesen Standard verwenden, wird das Echtzeit-Kundenprofil des Besuchers mit den Einverständnisinformationen aktualisiert, sofern Ihre Implementierung korrekt konfiguriert ist:
   1. Das Schema Individuelles XDM-Profil enthält die Feldergruppe [IAB TCF 2.0-Einverständnis](/help/xdm/field-groups/profile/iab.md).
   1. Das Erlebnisereignis-Schema enthält die [IAB TCF 2.0-Einverständnis-Feldergruppe](/help/xdm/field-groups/event/iab.md).
   1. Sie schließen die IAB-Einverständnisinformationen in das Ereignis (XDM[Objekt) &#x200B;](sendevent/xdm.md). Web SDK enthält die Einverständnisinformationen beim Senden von Ereignisdaten nicht automatisch.

Nach Verwendung dieses Befehls schreibt die Web-SDK die Benutzereinstellungen in ein Cookie. Wenn der Benutzer das nächste Mal Ihre Website im Browser lädt, ruft die SDK diese persistierten Voreinstellungen ab, um zu ermitteln, ob Ereignisse an Adobe gesendet werden können.

Adobe empfiehlt, alle Voreinstellungen für das Einverständnisdialogfeld getrennt vom Einverständnis für Web SDK zu speichern. Web SDK bietet keine Möglichkeit, Einverständnis abzurufen. Um sicherzustellen, dass die Benutzereinstellungen mit der SDK synchron bleiben, können Sie bei jedem Laden der Seite den Befehl `setConsent` aufrufen. Web SDK führt nur dann einen Server-Aufruf durch, wenn sich das Einverständnis ändert.

## Überlegungen zur Identitätssynchronisierung {#identity-considerations}

Der Befehl `setConsent` verwendet nur die `ECID` aus der Identitätszuordnung, da der Befehl auf Geräteebene ausgeführt wird. Andere Identitäten aus der Identitätszuordnung werden vom `setConsent`-Befehl nicht berücksichtigt.

## Verwenden von `defaultConsent` zusammen mit `setConsent` {#using-consent}

Web SDK bietet zwei komplementäre Einverständniskonfigurationsbefehle:

* [`defaultConsent`](configure/defaultconsent.md): Dieser Befehl soll die Einverständnisvoreinstellungen von Adobe-Kunden erfassen, die Web-SDK verwenden.
* [`setConsent`](setconsent.md): Dieser Befehl soll die Einverständnisvoreinstellungen Ihrer Site-Besucher erfassen.

Wenn diese Einstellungen zusammen verwendet werden, können sie je nach den konfigurierten Werten zu unterschiedlichen Ergebnissen bei der Datenerfassung und der Cookie-Einstellung führen.

In der folgenden Tabelle erfahren Sie, wann eine Datenerfassung erfolgt und wann Cookies gesetzt werden, basierend auf den Einstellungen für das Einverständnis.

| `defaultConsent` | `setConsent` | Datenerfassung findet statt | Web SDK setzt Browser-Cookies |
|---------|----------|---------|---------|
| `in` | `in` | Ja | Ja |
| `in` | `out` | Nein | Ja |
| `in` | Nicht festgelegt | Ja | Ja |
| `pending` | `in` | Ja | Ja |
| `pending` | `out` | Nein | Ja |
| `pending` | Nicht festgelegt | Nein | Nein |
| `out` | `in` | Ja | Ja |
| `out` | `out` | Nein | Ja |
| `out` | Nicht festgelegt | Nein | Nein |

Die folgenden Cookies werden gesetzt, wenn die Einverständniskonfiguration Folgendes zulässt:

| Name | Maximales Alter | Beschreibung |
|---|---|---|
| **`AMCV_###@AdobeOrg`** | 34128000 (395 Tage) | Bei aktiviertem [`idMigrationEnabled`](configure/idmigrationenabled.md) vorhanden. Dies ist hilfreich bei der Umstellung auf Web SDK, während einige Teile der Site noch `visitor.js` verwenden. |
| **`Demdex cookie`** | 15552000 (180 Tage) | Vorhanden, wenn ID-Synchronisierung aktiviert ist. Audience Manager setzt dieses Cookie, um einem Site-Besucher eine eindeutige ID zuzuweisen. Das demdex -Cookie hilft Audience Manager bei der Ausführung grundlegender Funktionen wie Besucheridentifizierung, ID-Synchronisierung, Segmentierung, Modellierung, Berichterstellung usw. |
| **`kndctr_orgid_cluster`** | 1800 (30 Minuten) | Speichert die Edge Network-Region, die die Anfragen des aktuellen Benutzers verarbeitet. Die Region wird im URL-Pfad verwendet, damit der Edge Network die Anfrage an die richtige Region weiterleiten kann. Wenn ein(e) Benutzende(r) eine Verbindung mit einer anderen IP-Adresse oder in einer anderen Sitzung herstellt, wird die Anfrage erneut an die nächstgelegene Region weitergeleitet. |
| **`kndct_orgid_identity`** | 34128000 (395 Tage) | Speichert die ECID sowie andere Informationen im Zusammenhang mit der ECID. |
| **`kndctr_orgid_consent`** | 15552000 (180 Tage) | Speichert die Einverständnisvoreinstellungen der Benutzer für die Website. |
| **`s_ecid`** | 63115200 (2 Jahre) | Enthält eine Kopie der Experience Cloud ID ([!DNL ECID]) oder MID. Die MID wird in einem Schlüssel-Wert-Paar gespeichert, das dieser Syntax folgt: `s_ecid=MCMID\|<ECID>`. |

Führen Sie den `setConsent` Befehl aus, wenn Sie Ihre konfigurierte Instanz der Web-SDK aufrufen. Sie können die folgenden Objekte in diesen Befehl einbeziehen:

* **`consent[]`**: Ein Array von `consent`. Das Einverständnisobjekt wird je nach ausgewähltem Standard und Version unterschiedlich formatiert. Auf den folgenden Registerkarten finden Sie Beispiele für jedes Einverständnisobjekt, abhängig vom Einverständnisstandard.
* **`identityMap`**: Ein Objekt, das steuert, wie eine ECID generiert wird und mit welchen IDs Einverständnisinformationen verknüpft sind. Adobe empfiehlt, dieses Objekt einzubeziehen, wenn `setConsent` vor anderen Befehlen wie [`sendEvent`](sendevent/overview.md) ausgeführt wird.
* **`edgeConfigOverrides`**: Ein Objekt, das [Überschreibungen der Datenstromkonfiguration](configure/edgeconfigoverrides.md) enthält.

>[!BEGINTABS]

>[!TAB Adobe 2.0]

### Adobe 2.0-`consent`

Wenn Sie Daten an Adobe Experience Platform senden, sollten Sie eine Datenschutzschemafeldgruppe in Ihr Profilschema aufnehmen. Weitere [&#x200B; zum Adobe 2.0-Standard finden Sie unter &#x200B;](/help/landing/governance-privacy-security/overview.md)Governance, Datenschutz und Sicherheit in Adobe Experience Platform&quot;. Sie können im unten stehenden Wertobjekt Daten hinzufügen, die dem Schema des `consents` Felds der [!UICONTROL Consents and Preferences] Profilfeldgruppe entsprechen.

* **`standard`**: Der von Ihnen gewählte Einverständnisstandard. Legen Sie diese Eigenschaft für den Adobe 2.0-Standard auf `"Adobe"` fest.
* **`version`**: Eine Zeichenfolge, die die Version des Einverständnisstandards darstellt. Legen Sie diese Eigenschaft für den Adobe 2.0-Standard auf `"2.0"` fest.
* **`value`**: Ein Objekt, das Einverständniswerte enthält.
   * **`value.collect.val`**: Der Einverständniswert. Legen Sie dies auf `"y"` beim Opt-in des Benutzers und auf `"n"` beim Opt-out des Benutzers fest.
   * **`value.metadata.time`**: Der Zeitstempel, zu dem Benutzer ihre Einverständniseinstellungen zuletzt aktualisiert haben.

```js
// Set consent using the Adobe 2.0 standard
alloy("setConsent", {
  "consent": [{
    "standard": "Adobe",
    "version": "2.0",
    "value": {
      "collect": {
        "val": "y"
      },
      "metadata": {
        "time": "YYYY-03-17T15:48:42-07:00"
      }
    }
  }]
});
```

>[!TAB IAB TCF 2.0]

### IAB TCF 2.0-`consent`

Um die Benutzereinverständnisvoreinstellungen aufzuzeichnen, die über den Standard des Transparency and Consent Framework (TCF) des Interactive Advertising Bureau Europe (IAB) bereitgestellt werden, legen Sie die Einverständniszeichenfolge wie unten dargestellt fest.

Wenn das Einverständnis auf diese Weise festgelegt wird, wird das Echtzeit-Kundenprofil mit den Einverständnisinformationen aktualisiert. Dazu muss das Profil-XDM-Schema die Feldergruppe [Profil-Datenschutzschema“ enthalten](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md). Beim Senden von Ereignissen müssen die IAB-Einverständnisinformationen manuell zum Ereignis-XDM-Objekt hinzugefügt werden. Web SDK enthält die Einverständnisinformationen nicht automatisch in die Ereignisse.

Um die Einverständnisinformationen in -Ereignissen zu senden, müssen Sie die Feldergruppe Erlebnisereignis-Datenschutz zu Ihrem [!DNL Profile] aktivierten [!DNL XDM ExperienceEvent] hinzufügen. Anweisungen zur Konfiguration finden [&#x200B; im Abschnitt zum Aktualisieren &#x200B;](/help/landing/governance-privacy-security/consent/iab/dataset.md#event-schema) ExperienceEvent-Schemas im Handbuch zur Datensatzvorbereitung.

* **`standard`**: Der von Ihnen gewählte Einverständnisstandard. Legen Sie diese Eigenschaft für den IAB TCF 2.0-Standard auf `"IAB TCF"` fest.
* **`version`**: Eine Zeichenfolge, die die Version des Einverständnisstandards darstellt. Legen Sie diese Eigenschaft für den IAB TCF 2.0-Standard auf `"2.0"` fest.
* **`value`**: Eine Zeichenfolge, die den Einverständniswert enthält.
* **`gdprApplies`**: Ein boolescher Wert, der bestimmt, ob die DSGVO für diesen Einverständniswert gilt. Der Standardwert lautet `true`.
* **`gdprContainsPersonalData`**: Ein boolescher Wert, der bestimmt, ob die mit diesem Benutzer verknüpften Ereignisdaten personenbezogene Daten enthalten. Der Standardwert lautet `false`.

```js
// Set consent using the IAB TCF 2.0 standard
alloy("setConsent", {
  consent: [{
    "standard": "IAB TCF",
    "version": "2.0",
    "value": "CO052l-O052l-DGAMBFRACBgAIBAAAAABIYgEawAQEagAAAA",
    "gdprApplies": true,
    "gdprContainsPersonalData": true
  }]
});
```

Die IAB TCF 2.0-API stellt ein Ereignis bereit, für das das Einverständnis vom Kunden aktualisiert wird. Dies tritt auf, wenn der Kunde anfänglich seine Voreinstellungen festlegt und wenn der Kunde seine Voreinstellungen aktualisiert. Sie können einen Ereignis-Listener hinzufügen, um den `setConsent`-Befehl auszuführen:

```js
const identityMap = { ... };
window.__tcfapi('addEventListener', 2, function (tcData, success) {
  if (success && tcData.eventStatus === 'useractioncomplete') {
    window.alloy("setConsent", {
      identityMap,
      consent: [
        {
          standard: "IAB TCF",
          version: "2.0",
          value: tcData.tcString,
          gdprApplies: tcData.gdprApplies
        }
      ]
    });
  }
});
```

Der obige Code-Block überwacht das `useractioncomplete`-Ereignis und legt dann das Einverständnis fest, wobei die Einverständniszeichenfolge und das `gdprApplies`-Flag übergeben werden. Wenn Sie benutzerdefinierte Identitäten für Ihre Kunden haben, stellen Sie sicher, dass Sie die `identityMap` Variable ausfüllen.

>[!TAB Adobe 1.0]

### Adobe 1.0-`consent`

* **`standard`**: Der von Ihnen gewählte Einverständnisstandard. Legen Sie diese Eigenschaft für den Adobe 1.0-Standard auf `"Adobe"` fest.
* **`version`**: Eine Zeichenfolge, die die Version des Einverständnisstandards darstellt. Legen Sie diese Eigenschaft für den Adobe 1.0-Standard auf `"1.0"` fest.
* **`value.general`**: Der Einverständniswert. Legen Sie dies auf `"in"` beim Opt-in des Benutzers und auf `"out"` beim Opt-out des Benutzers fest.

```js
// Set consent using the Adobe 1.0 standard
alloy("setConsent", {
  "consent": [{
    "standard": "Adobe",
    "version": "1.0",
    "value": {
      "general": "in"
    }
  }]
});
```

>[!ENDTABS]

### Mehrere Standards in einer Anfrage senden {#multiple-standards}

Web SDK unterstützt auch das Senden von mehr als einem Einverständnisobjekt in einer Anfrage, wie im folgenden Beispiel gezeigt.

```js
alloy("setConsent", {
    consent: [{
        standard: "Adobe",
        version: "2.0",
        value: {
            collect: {
                val: "y"
            },
            metadata: {
                time: "YYYY-03-17T15:48:42-07:00"
            }
        }
    }, {
        standard: "IAB TCF",
        version: "2.0",
        value: "CO1Z4yuO1Z4yuAcABBENArCsAP_AAH_AACiQGCNX_T5eb2vj-3Zdt_tkaYwf55y3o-wzhhaIse8NwIeH7BoGP2MwvBX4JiQCGBAkkiKBAQdtHGhcCQABgIhRiTKMYk2MjzNKJLJAilsbe0NYCD9mnsHT3ZCY70--u__7P3fAwQgkwVLwCRIWwgJJs0ohTABCOICpBwCUEIQEClhoACAnYFAR6gAAAIDAACAAAAEEEBAIABAAAkIgAAAEBAKACIBAACAEaAhAARIEAsAJEgCAAVA0JACKIIQBCDgwCjlACAoAAAAA.YAAAAAAAAAAA",
        gdprApplies: true
    }]
});
```

## Beständigkeit der Zustimmungseinstellungen {#persistence}

Nachdem Sie Benutzereinstellungen mithilfe des `setConsent`-Befehls an die Web-SDK übermittelt haben, behält die SDK Benutzereinstellungen für ein Cookie bei. Wenn der Benutzer das nächste Mal Ihre Website im Browser lädt, ruft die Web-SDK diese persistenten Voreinstellungen ab und verwendet sie, um zu bestimmen, ob Ereignisse an Adobe gesendet werden können.

Speichern Sie die Benutzereinstellungen unabhängig, damit Sie das Einverständnisdialogfeld mit den aktuellen Einstellungen anzeigen können. Es gibt keine Möglichkeit, die Benutzereinstellungen von der Web-SDK abzurufen. Um sicherzustellen, dass die Benutzereinstellungen mit der SDK synchron bleiben, können Sie bei jedem Laden der Seite den Befehl `setConsent` aufrufen. Web SDK führt nur dann einen Server-Aufruf durch, wenn sich die Voreinstellungen ändern.

## Festlegen des Einverständnisses mit der Tag-Erweiterung „Web SDK&quot;

Die diesem Befehl entsprechende Web SDK-Tag-Erweiterung ist die [**[!UICONTROL Set consent]**](/help/tags/extensions/client/web-sdk/actions/set-consent.md).
