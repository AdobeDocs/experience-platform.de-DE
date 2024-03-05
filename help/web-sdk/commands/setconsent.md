---
title: setConsent
description: Wird auf jeder Seite verwendet, um die Zustimmung des Benutzers zu verfolgen.
source-git-commit: 90493d179e620604337bda96cb3b7f5401ca4a81
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 1%

---

# setConsent

Die `setConsent` gibt dem Web SDK an, ob es Daten senden (Opt-in), Daten verwerfen (Opt-out) oder verwenden soll [`defaultConsent`](configure/defaultconsent.md) (Einverständnis unbekannt).

Das Web SDK unterstützt die folgenden Standards:

* **[Adobe-Standard](/help/landing/governance-privacy-security/consent/adobe/overview.md)**: Sowohl 1.0- als auch 2.0-Standards werden unterstützt.
* **[IAB Transparency &amp; Consent Framework](/help/landing/governance-privacy-security/consent/iab/overview.md)**: Wenn Sie diesen Standard verwenden, wird das Echtzeit-Kundenprofil des Besuchers mit den Zustimmungsinformationen aktualisiert, wenn Ihre Implementierung richtig konfiguriert ist:
   1. Das individuelle XDM-Profilschema enthält die [IAB TCF 2.0-Feldergruppe &quot;Einwilligung&quot;](/help/xdm/field-groups/profile/iab.md).
   1. Das Schema Erlebnisereignis enthält die [IAB TCF 2.0-Feldergruppe &quot;Einwilligung&quot;](/help/xdm/field-groups/event/iab.md).
   1. Sie fügen die IAB-Zustimmungsinformationen in das Ereignis ein. [XDM-Objekt](sendevent/xdm.md). Das Web SDK enthält beim Senden von Ereignisdaten nicht automatisch die Zustimmungsinformationen.

Nach Verwendung dieses Befehls schreibt das Web SDK die Voreinstellungen des Benutzers in ein Cookie. Wenn der Benutzer das nächste Mal Ihre Website im Browser lädt, ruft das SDK diese beibehaltenen Voreinstellungen ab, um zu bestimmen, ob Ereignisse an Adobe gesendet werden können.

Adobe empfiehlt, dass Sie alle Voreinstellungen für das Einwilligungsdialogfeld getrennt von der Web SDK-Zustimmung speichern. Das Web SDK bietet keine Möglichkeit, die Zustimmung abzurufen. Sie können die `setConsent` -Befehl bei jedem Laden der Seite. Das Web SDK führt nur dann einen Server-Aufruf durch, wenn sich die Zustimmung ändert.

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

* **`consent[]`**: Ein Array von `consent` Objekte. Das Objekt für die Zustimmung wird je nach gewähltem Standard und Version unterschiedlich formatiert.
* **`identityMap`**: Ein Objekt, das steuert, wie eine ECID generiert wird und an welche IDs die Einwilligungsinformationen gebunden sind. Adobe empfiehlt, dieses Objekt einzuschließen, wenn `setConsent` vor anderen Befehlen ausgeführt wird, z. B. [`sendEvent`](sendevent/overview.md).
* **`edgeConfigOverrides`**: Ein Objekt, das [Überschreibungen der Datenspeicherkonfiguration](datastream-overrides.md).

>[!BEGINTABS]

>[!TAB Adobe 2.0]

### Adobe 2.0-Standard `consent` Objekt

* **`standard`**: Der von Ihnen ausgewählte Zustimmungsstandard. Legen Sie diese Eigenschaft auf `"Adobe"` für den Adobe 2.0-Standard.
* **`version`**: Eine Zeichenfolge, die die Version des Zustimmungsstandards darstellt. Legen Sie diese Eigenschaft auf `"2.0"` für den Adobe 2.0-Standard.
* **`value`**: Ein Objekt, das Zustimmungswerte enthält.
   * **`value.collect.val`**: Der Zustimmungswert. Gültige Werte sind `"y"` (Opt-in) `"n"` (Abmeldung).
   * **`value.metadata.time`**: Der Zeitstempel, mit dem der Benutzer den Zustimmungswert festlegt.

```js
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

* **`standard`**: Der von Ihnen ausgewählte Zustimmungsstandard. Legen Sie diese Eigenschaft auf `"IAB TCF"` für den IAB TCF 2.0-Standard.
* **`version`**: Eine Zeichenfolge, die die Version des Zustimmungsstandards darstellt. Legen Sie diese Eigenschaft auf `"2.0"` für den IAB TCF 2.0-Standard.
* **`value`**: Eine Zeichenfolge, die den Zustimmungswert enthält.
* **`gdprApplies`**: Ein boolescher Wert, der bestimmt, ob die DSGVO für diesen Zustimmungswert gilt. Der Standardwert lautet `true`.
* **`gdprContainsPersonalData`**: Ein boolescher Wert, der bestimmt, ob die mit diesem Benutzer verknüpften Ereignisdaten personenbezogene Daten enthalten. Der Standardwert lautet `false`.

```js
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
* **`value.general`**: Der Zustimmungswert. Gültige Werte sind `"in"` (Opt-in) `"out"` (Abmeldung).

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
