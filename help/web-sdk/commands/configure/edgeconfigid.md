---
title: edgeConfigId
description: Bestimmen Sie die Datastream-ID, an die Sie Daten senden möchten.
exl-id: 2d709f70-c014-4868-b2f5-17e8b88343d1
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# `edgeConfigId`

Die `edgeConfigId` -Eigenschaft ist eine Zeichenfolge, die bestimmt, an welchen [Datastraam](../../../datastreams/overview.md) in Adobe Experience Platform Daten gesendet werden sollen. Diese Eigenschaft ist beim Senden von Daten an Adobe erforderlich.

So suchen Sie eine Datastream-ID:

1. Melden Sie sich mit Ihren Adobe ID-Anmeldedaten bei [experience.adobe.com](https://experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Datenspeicher]**.
1. Verwenden Sie das Suchfeld, um den gewünschten Datastream zu suchen, und wählen Sie dann neben der Datastream-ID **[!UICONTROL Copy]** ![Copy](../../assets/copy.png) aus.

Sie können auch den gewünschten Datastream-Namen auswählen und die Datastream-ID wird in der rechten Spalte angezeigt, die Sie kopieren können.

## Wählen Sie die Datastraam-ID mithilfe der Web SDK-Tag-Erweiterung aus.

Wählen Sie aus einer Liste der verfügbaren Datenspeicher aus oder geben Sie eine Datastraam-ID direkt ein, wenn [die Tag-Erweiterung konfigurieren](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Melden Sie sich mit Ihren Adobe ID-Anmeldedaten bei [experience.adobe.com](https://experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** und klicken Sie dann auf der Karte [!UICONTROL Adobe Experience Platform Web SDK] auf **[!UICONTROL Konfigurieren]** .
1. Suchen Sie den Abschnitt [!UICONTROL Datastreams] und wählen Sie dann die gewünschte Methode zur Bestimmung des Datastreams aus.
   * Wenn Sie aus einer Liste auswählen, wählen Sie die Sandbox und den Datastream aus den jeweiligen Dropdown-Listen aus.
   * Geben Sie bei der Eingabe von Werten die gewünschte Datastream-ID ein.
1. Klicken Sie auf **[!UICONTROL Speichern]** und veröffentlichen Sie dann Ihre Änderungen.

Sie können Daten für Produktions-, Staging- und Entwicklungs-Tag-Umgebungen an verschiedene Datastreams senden.

## Auswählen der Datastraam-ID mithilfe der Web SDK JavaScript-Bibliothek

Legen Sie die String-Eigenschaft `edgeConfigId` fest, wenn Sie den Befehl `configure` ausführen. Diese Eigenschaft ist für alle Web SDK-Implementierungen erforderlich. Wenn Sie diese Eigenschaft weglassen, weiß das Web SDK nicht, an welchen Datenspeicher Daten gesendet werden sollen, was dazu führt, dass diese Daten dauerhaft verloren gehen.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```

Wenn Sie mehrere Instanzen des Web SDK auf einer einzelnen Seite konfigurieren, müssen Sie für jede Instanz ein anderes `edgeConfigId` konfigurieren.
