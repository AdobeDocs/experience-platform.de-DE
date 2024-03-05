---
title: defaultConsent
description: Legen Sie die standardmäßige Methode zur Einverständniserfassung fest.
source-git-commit: b9db136a9077e3420bfeb44ae45e7d72c322acbb
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# `defaultConsent`

Die `defaultConsent` -Eigenschaft bestimmt, wie Sie die Datenerfassungszustimmung verarbeiten, bevor Sie [`setConsent`](../setconsent.md) Befehl. Diese Eigenschaft ist nützlich, wenn Sie nicht versehentlich Daten von Einzelpersonen erfassen möchten, die sich in Bereichen befinden, in denen vor der Datenerfassung eine Einwilligung erforderlich ist.

Diese Eigenschaft erlaubt drei Werte:

* **In**: Die Datenerfassung wird wie gewohnt fortgesetzt, bis der Benutzer sich abmeldet.
* **Out**: Die Daten werden dauerhaft verworfen, bis der Benutzer sich anmeldet.
* **Ausstehend**: Die Daten werden lokal gespeichert, bis sich der Benutzer für die Verwendung der [`setConsent`](../setconsent.md) Befehl. Die Daten bleiben nicht zwischen den Seitenladevorgängen erhalten.

Wenn Sie einen Besucher haben, der nicht in die Rechtsprechung der Datenschutz-Grundverordnung (DSGVO) fällt, kann die Standardzustimmung auf `in`. Besucher, die sich in der Gerichtsbarkeit der DSGVO befinden, können ihre standardmäßige Einwilligung auf `pending`. Ihre Consent Management Platform (CMP) kann die Region des Kunden erkennen und das Flag bereitstellen `gdprApplies` nach IAB TCF 2.0. Mit diesem Flag können Sie die Standardzustimmung festlegen.

## Festlegen der Standardzustimmung mit der Web SDK-Tag-Erweiterung

Wählen Sie das gewünschte Optionsfeld unter **[!UICONTROL Standardzustimmung]** when [Konfigurieren der Tag-Erweiterung](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Anmelden bei [experience.adobe.com](https://experience.adobe.com) mit Ihren Adobe ID-Anmeldedaten.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** Klicken Sie auf **[!UICONTROL Konfigurieren]** auf [!UICONTROL Adobe Experience Platform Web SDK] Karte.
1. Scrollen Sie nach unten zum [!UICONTROL Datenschutz] und wählen Sie dann die gewünschte **[!UICONTROL Standardzustimmung]**.
1. Klicks **[!UICONTROL Speichern]** und veröffentlichen Sie dann Ihre Änderungen.

## Festlegen der Standardzustimmung mithilfe der Web SDK-JavaScript-Bibliothek

Legen Sie die `defaultConsent` Zeichenfolgeneigenschaft auf die gewünschte Zustimmungsstufe beim Ausführen der `configure` Befehl. Diese Eigenschaft unterscheidet zwischen Groß- und Kleinschreibung und unterstützt nur die folgenden drei Werte: `"in"`, `"out"`, und `"pending"`. Wenn Sie versuchen, einen anderen Wert zu verwenden, gibt die Bibliothek einen Fehler aus.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": "pending"
});
```
