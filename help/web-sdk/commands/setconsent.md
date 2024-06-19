---
title: setConsent
description: Wird auf jeder Seite verwendet, um die Zustimmungsvoreinstellungen Ihrer Benutzer zu verfolgen.
exl-id: d01a6ef1-4fa7-4a60-a3a1-19568b4e0d23
source-git-commit: d3591053939147589dae24e1e4c20d53b1f87dd3
workflow-type: tm+mt
source-wordcount: '1372'
ht-degree: 3%

---


# `setConsent`

Die `setConsent` gibt dem Web SDK an, ob es Daten senden (Opt-in), Daten verwerfen (Opt-out) oder verwenden soll [`defaultConsent`](configure/defaultconsent.md) (Einverständnis unbekannt).

Das Web SDK unterstützt die folgenden Standards:

* **[Adobe-Standard](/help/landing/governance-privacy-security/consent/adobe/overview.md)**: Sowohl 1.0- als auch 2.0-Standards werden unterstützt.
* **[IAB Transparency &amp; Consent Framework](/help/landing/governance-privacy-security/consent/iab/overview.md)**: Wenn Sie diesen Standard verwenden, wird das Echtzeit-Kundenprofil des Besuchers mit den Zustimmungsinformationen aktualisiert, wenn Ihre Implementierung richtig konfiguriert ist:
   1. Das individuelle XDM-Profilschema enthält die [IAB TCF 2.0-Feldergruppe &quot;Einwilligung&quot;](/help/xdm/field-groups/profile/iab.md).
   1. Das Schema Erlebnisereignis enthält die [IAB TCF 2.0-Feldergruppe &quot;Einwilligung&quot;](/help/xdm/field-groups/event/iab.md).
   1. Sie fügen die IAB-Zustimmungsinformationen in das Ereignis ein. [XDM-Objekt](sendevent/xdm.md). Das Web SDK enthält beim Senden von Ereignisdaten nicht automatisch die Zustimmungsinformationen.

Nach Verwendung dieses Befehls schreibt das Web SDK die Voreinstellungen des Benutzers in ein Cookie. Wenn der Benutzer das nächste Mal Ihre Website im Browser lädt, ruft das SDK diese beibehaltenen Voreinstellungen ab, um zu bestimmen, ob Ereignisse an Adobe gesendet werden können.

Adobe empfiehlt, dass Sie alle Voreinstellungen für das Einwilligungsdialogfeld getrennt von der Web SDK-Zustimmung speichern. Das Web SDK bietet keine Möglichkeit, die Zustimmung abzurufen. Sie können die `setConsent` -Befehl bei jedem Laden der Seite. Das Web SDK führt nur dann einen Server-Aufruf durch, wenn sich die Zustimmung ändert.

## Verwenden `defaultConsent` zusammen mit `setConsent` {#using-consent}

Das Web SDK bietet zwei komplementäre Konfigurationsbefehle für die Zustimmung:

* [`defaultConsent`](configure/defaultconsent.md): Dieser Befehl dient zum Erfassen der Zustimmungsvoreinstellungen von Adobe-Kunden, die das Web SDK verwenden.
* [`setConsent`](setconsent.md): Mit diesem Befehl können Sie die Zustimmungsvoreinstellungen Ihrer Site-Besucher erfassen.

Wenn diese Einstellungen zusammen verwendet werden, können sie je nach konfigurierten Werten zu unterschiedlichen Ergebnissen bei der Datenerfassung und Cookie-Einstellung führen.

Die nachstehende Tabelle zeigt, wann und wann Cookies basierend auf den Zustimmungseinstellungen erfasst werden.

| defaultConsent | setConsent | Datenerfassung | Web SDK setzt Browser-Cookies |
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

Die folgenden Cookies werden gesetzt, wenn die Konfiguration der Zustimmung Folgendes zulässt:

| Name | Max. Alter | Beschreibung |
|---|---|---|
| **AMCV_###@AdobeOrg** | 34128000 (395 Tage) | Vorhanden, wenn [`idMigrationEnabled`](configure/idmigrationenabled.md) aktiviert ist. Dies ist beim Übergang zum Web SDK hilfreich, während einige Teile der Site weiterhin verwenden `visitor.js`. |
| **Demdex-Cookie** | 15552000 (180 Tage) | Vorhanden bei aktivierter ID-Synchronisierung. Audience Manager setzt dieses Cookie, um Site-Besuchern eine eindeutige ID zuzuweisen. Das demdex-Cookie hilft Audience Manager bei der Ausführung grundlegender Funktionen wie Besucheridentifizierung, ID-Synchronisierung, Segmentierung, Modellierung, Berichterstellung usw. |
| **kndctr_orgid_cluster** | 1800 (30 Minuten) | Speichert den Edge Network-Bereich, der den Anforderungen des aktuellen Benutzers entspricht. Der Bereich wird im URL-Pfad verwendet, damit das Edge Network die Anfrage an den richtigen Bereich weiterleiten kann. Wenn ein Benutzer eine Verbindung mit einer anderen IP-Adresse oder in einer anderen Sitzung herstellt, wird die Anforderung erneut an den nächsten Bereich weitergeleitet. |
| **kndct_orgid_identity** | 34128000 (395 Tage) | Speichert die ECID sowie andere Informationen zur ECID. |
| **kndctr_orgid_consent** | 15552000 (180 Tage) | Speichert die Voreinstellung der Benutzerzustimmung für die Website. |
| **s_ecid** | 63115200 (2 Jahre) | Enthält eine Kopie der Experience Cloud-ID ([!DNL ECID]) oder MID. Die MID wird in einem Schlüssel-Wert-Paar gespeichert, das dieser Syntax folgt: `s_ecid=MCMID\|<ECID>`. |

## Festlegen der Zustimmung mithilfe der Web SDK-Tag-Erweiterung

Das Festlegen der Zustimmung wird als Aktion innerhalb einer Regel in der Adobe Experience Platform-Oberfläche für Datenerfassungs-Tags durchgeführt.

1. Anmelden bei [experience.adobe.com](https://experience.adobe.com) mit Ihren Adobe ID-Anmeldedaten.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Regeln]** und wählen Sie dann die gewünschte Regel aus.
1. under [!UICONTROL Aktionen], wählen Sie eine vorhandene Aktion aus oder erstellen Sie eine Aktion.
1. Legen Sie die [!UICONTROL Erweiterung] Dropdown-Feld zu **[!UICONTROL Adobe Experience Platform Web SDK]** und legen Sie die [!UICONTROL Aktionstyp] nach **[!UICONTROL Einverständnis festlegen]**.
1. Legen Sie die gewünschten Felder rechts fest, einschließlich **[!UICONTROL Standard]** und **[!UICONTROL Allgemeine Zustimmung]**.
1. Klicks **[!UICONTROL Änderungen beibehalten]** und führen Sie dann Ihren Veröffentlichungs-Workflow aus.

Sie können in diese Aktion mehrere Zustimmungsobjekte einfügen.

## Festlegen der Zustimmung mithilfe der Web SDK-JavaScript-Bibliothek

Führen Sie die `setConsent` beim Aufruf Ihrer konfigurierten Instanz des Web SDK. Sie können die folgenden Objekte in diesen Befehl einfügen:

* **`consent[]`**: Ein Array von `consent` Objekte. Das Objekt für die Zustimmung wird je nach gewähltem Standard und Version unterschiedlich formatiert. Auf den folgenden Registerkarten finden Sie Beispiele für jedes Einverständnisobjekt, je nach Zustimmungsstandard.
* **`identityMap`**: Ein Objekt, das steuert, wie eine ECID generiert wird und an welche IDs die Einwilligungsinformationen gebunden sind. Adobe empfiehlt, dieses Objekt einzuschließen, wenn `setConsent` vor anderen Befehlen ausgeführt wird, z. B. [`sendEvent`](sendevent/overview.md).
* **`edgeConfigOverrides`**: Ein Objekt, das [Überschreibungen der Datenspeicherkonfiguration](datastream-overrides.md).

>[!BEGINTABS]

>[!TAB Adobe 2.0]

### Adobe 2.0-Standard `consent` Objekt

Wenn Sie Adobe Experience Platform verwenden, müssen Sie eine Datenschutzschema-Feldergruppe in Ihr Profilschema aufnehmen. Siehe [Governance, Datenschutz und Sicherheit in Adobe Experience Platform](../../landing/governance-privacy-security/overview.md) für weitere Informationen zum Adobe 2.0-Standard. Sie können Daten innerhalb des Wertobjekts hinzufügen, die dem Schema des `consents` des [!UICONTROL Einverständnis und Voreinstellungen] Profilfeldgruppe.

* **`standard`**: Der von Ihnen ausgewählte Zustimmungsstandard. Legen Sie diese Eigenschaft auf `"Adobe"` für den Adobe 2.0-Standard.
* **`version`**: Eine Zeichenfolge, die die Version des Zustimmungsstandards darstellt. Legen Sie diese Eigenschaft auf `"2.0"` für den Adobe 2.0-Standard.
* **`value`**: Ein Objekt, das Zustimmungswerte enthält.
   * **`value.collect.val`**: Der Zustimmungswert. Legen Sie hier fest `"y"` , wenn sich Benutzer anmelden und `"n"` , wenn Benutzer sich abmelden.
   * **`value.metadata.time`**: Der Zeitstempel, mit dem Benutzer ihre Zustimmungseinstellungen zuletzt aktualisiert haben.

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

### IAB TCF 2.0-Standard `consent` Objekt

Legen Sie die Zustimmungszeichenfolge wie unten dargestellt fest, um die über den IAB Transparency and Consent Framework (TCF)-Standard (Interactive Advertising Bureau Europe) bereitgestellten Zustimmungsvoreinstellungen der Benutzer aufzuzeichnen.

Wenn die Zustimmung auf diese Weise festgelegt wird, wird das Echtzeit-Kundenprofil mit den Zustimmungsinformationen aktualisiert. Dazu muss das Profil-XDM-Schema die [Feldergruppe zum Profildatenschutzschema](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md). Beim Senden von Ereignissen müssen die IAB-Zustimmungsinformationen manuell zum Ereignis-XDM-Objekt hinzugefügt werden. Das Web SDK nimmt die Zustimmungsinformationen nicht automatisch in die Ereignisse auf.

Um die Einwilligungsinformationen in Ereignissen zu senden, müssen Sie die Feldergruppe &quot;Erlebnisereignis-Datenschutz&quot;zu Ihrer [!DNL Profile]-enabled [!DNL XDM ExperienceEvent] Schema. Siehe Abschnitt zu [Aktualisieren des ExperienceEvent-Schemas](../../landing/governance-privacy-security/consent/iab/dataset.md#event-schema) Anweisungen zur Konfiguration finden Sie im Leitfaden zur Datensatzvorbereitung .

* **`standard`**: Der von Ihnen ausgewählte Zustimmungsstandard. Legen Sie diese Eigenschaft auf `"IAB TCF"` für den IAB TCF 2.0-Standard.
* **`version`**: Eine Zeichenfolge, die die Version des Zustimmungsstandards darstellt. Legen Sie diese Eigenschaft auf `"2.0"` für den IAB TCF 2.0-Standard.
* **`value`**: Eine Zeichenfolge, die den Zustimmungswert enthält.
* **`gdprApplies`**: Ein boolescher Wert, der bestimmt, ob die DSGVO für diesen Zustimmungswert gilt. Der Standardwert lautet `true`.
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

>[!TAB Adobe 1.0]

### Adobe 1.0-Standard `consent` Objekt

* **`standard`**: Der von Ihnen ausgewählte Zustimmungsstandard. Legen Sie diese Eigenschaft auf `"Adobe"` für den Adobe 1.0-Standard.
* **`version`**: Eine Zeichenfolge, die die Version des Zustimmungsstandards darstellt. Legen Sie diese Eigenschaft auf `"1.0"` für den Adobe 1.0-Standard.
* **`value.general`**: Der Zustimmungswert. Legen Sie hier fest `"in"` , wenn sich Benutzer anmelden und `"out"` , wenn Benutzer sich abmelden.

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

### Senden mehrerer Standards in einer Anfrage {#multiple-standards}

Das Web SDK unterstützt auch das Senden von mehr als einem Zustimmungsobjekt in einer Anfrage, wie im folgenden Beispiel gezeigt.

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
                time: "2021-03-17T15:48:42-07:00"
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

Nachdem Sie die Benutzereinstellungen mithilfe der `setConsent` festgelegt ist, behält das SDK Benutzereinstellungen in einem Cookie bei. Wenn der Benutzer das nächste Mal Ihre Website im Browser lädt, ruft das Web SDK diese beibehaltenen Voreinstellungen ab und verwendet sie, um zu bestimmen, ob Ereignisse an Adobe gesendet werden können oder nicht.

Sie müssen die Benutzereinstellungen unabhängig speichern, um das Dialogfeld &quot;Einverständnis&quot;mit den aktuellen Voreinstellungen anzeigen zu können. Es gibt keine Möglichkeit, die Benutzereinstellungen vom Web SDK abzurufen. Sie können die `setConsent` -Befehl bei jedem Laden der Seite. Das Web SDK führt nur dann einen Server-Aufruf durch, wenn sich die Voreinstellungen geändert haben.

## Synchronisieren von Identitäten beim Festlegen der Zustimmung {#sync-identities}

Wenn die Standardzustimmung (festgelegt über die [defaultConsent](configure/defaultconsent.md) Parameter) auf `pending` oder `out`, die `setConsent` -Einstellung kann die erste Anfrage sein, die gesendet wird und die Identität festlegt. Daher kann es wichtig sein, Identitäten bei der ersten Anfrage zu synchronisieren. Sie können die Identitätszuordnung zum `setConsent` -Befehl wie auf der `sendEvent` Befehl. Siehe [Verwenden von identityMap](../identity/overview.md#using-identitymap) ein Beispiel dafür, wie Sie die Identitätszuordnung in Ihren Befehl einbeziehen.
