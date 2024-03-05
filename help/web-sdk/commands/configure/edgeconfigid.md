---
title: edgeConfigId
description: Bestimmen Sie die Datastream-ID, an die Sie Daten senden möchten.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# `edgeConfigId`

Die `edgeConfigId` -Eigenschaft ist eine Zeichenfolge, die bestimmt, [datastream](../../../datastreams/overview.md) in Adobe Experience Platform, an die Sie Daten senden möchten. Diese Eigenschaft ist beim Senden von Daten an Adobe erforderlich.

So suchen Sie eine Datastream-ID:

1. Anmelden bei [experience.adobe.com](https://experience.adobe.com) mit Ihren Adobe ID-Anmeldedaten.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Datenspeicher]**.
1. Suchen Sie mithilfe des Suchfelds nach dem gewünschten Datastream und wählen Sie **[!UICONTROL Kopieren]** ![Kopieren](../../assets/copy.png) neben der Datastream-ID.

Sie können auch den gewünschten Datastream-Namen auswählen und die Datastream-ID wird in der rechten Spalte angezeigt, die Sie kopieren können.

## Wählen Sie die Datastraam-ID mithilfe der Web SDK-Tag-Erweiterung aus.

Wählen Sie aus einer Liste verfügbarer Datenspeicher oder geben Sie eine Datastraam-ID ein, wenn Sie [Konfigurieren der Tag-Erweiterung](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Anmelden bei [experience.adobe.com](https://experience.adobe.com) mit Ihren Adobe ID-Anmeldedaten.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** Klicken Sie auf **[!UICONTROL Konfigurieren]** auf [!UICONTROL Adobe Experience Platform Web SDK] Karte.
1. Suchen Sie die [!UICONTROL Datenspeicher] und wählen Sie dann die gewünschte Methode zur Bestimmung des Datastreams aus.
   * Wenn Sie aus einer Liste auswählen, wählen Sie die Sandbox und den Datastream aus den jeweiligen Dropdown-Listen aus.
   * Geben Sie bei der Eingabe von Werten die gewünschte Datastream-ID ein.
1. Klicks **[!UICONTROL Speichern]** und veröffentlichen Sie dann Ihre Änderungen.

Sie können Daten für Produktions-, Staging- und Entwicklungs-Tag-Umgebungen an verschiedene Datastreams senden.

## Wählen Sie die Datastraam-ID mithilfe der Web SDK JavaScript-Bibliothek aus.

Legen Sie die `edgeConfigId` Zeichenfolgeneigenschaft beim Ausführen der `configure` Befehl. Diese Eigenschaft ist für alle Web SDK-Implementierungen erforderlich. Wenn Sie diese Eigenschaft weglassen, weiß das Web SDK nicht, an welchen Datenspeicher Daten gesendet werden sollen, was dazu führt, dass diese Daten dauerhaft verloren gehen.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```

Wenn Sie mehrere Instanzen des Web SDK auf einer Seite konfigurieren, müssen Sie eine andere `edgeConfigId` für jede Instanz.
