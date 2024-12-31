---
title: datastreamId
description: Bestimmen Sie die Datenstrom-ID, an die Sie Daten senden möchten.
exl-id: 2d709f70-c014-4868-b2f5-17e8b88343d1
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---

# `datastreamId`

Die `datastreamId`-Eigenschaft ist eine Zeichenfolge, die bestimmt[ an welchen ](../../../datastreams/overview.md)Datenstrom) in Adobe Experience Platform Sie Daten senden möchten. Diese Eigenschaft ist erforderlich, wenn Daten an Adobe gesendet werden. Web SDK-Versionen 2.20.0 oder früher verwenden stattdessen `edgeConfigId`.

So suchen Sie eine Datenstrom-ID:

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei ](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie **[!UICONTROL Datenerfassung]** > **[!UICONTROL Datenströme]**.
1. Verwenden Sie das Suchfeld, um den gewünschten Datenstrom zu finden, und wählen Sie dann **[!UICONTROL Kopieren]** ![Kopieren](../../assets/copy.png) neben der Datenstrom-ID aus.

Alternativ können Sie den gewünschten Datenstromnamen auswählen. Die Datenstrom-ID wird dann in der rechten Spalte angezeigt, damit Sie sie kopieren können.

## Wählen Sie die Datenstrom-ID mithilfe der Tag-Erweiterung „Web SDK&quot; aus

Wählen Sie aus einer Liste der verfügbaren Datenströme aus oder geben Sie beim [Konfigurieren der Tag-Erweiterung“ direkt eine Datenstrom-ID ](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei ](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** und klicken Sie dann auf **[!UICONTROL Konfigurieren]** auf der Karte [!UICONTROL Adobe Experience Platform Web SDK].
1. Suchen Sie den Abschnitt [!UICONTROL Datenströme] und wählen Sie dann die gewünschte Methode zur Bestimmung des Datenstroms aus.
   * Wenn Sie aus einer Liste auswählen, wählen Sie die Sandbox und den Datenstrom aus der jeweiligen Dropdown-Liste aus.
   * Geben Sie bei der Eingabe von Werten die gewünschte Datenstrom-ID ein.
1. Klicken Sie **[!UICONTROL Speichern]** und veröffentlichen Sie Ihre Änderungen.

Sie können Daten an verschiedene Datenströme für Produktions-, Staging- und Entwicklungs-Tag-Umgebungen senden.

## Wählen Sie die Datenstrom-ID mithilfe der Web SDK JavaScript-Bibliothek aus

Legen Sie beim Ausführen des `configure`-Befehls die `datastreamID`-Zeichenfolgeneigenschaft fest. Diese Eigenschaft ist für alle Implementierungen von Web SDK erforderlich. Wenn Sie diese Eigenschaft auslassen, weiß Web SDK nicht, an welchen Datenstrom Daten gesendet werden sollen, sodass diese Daten dauerhaft verloren gehen.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```

Wenn Sie mehrere Instanzen von Web SDK auf einer Seite konfigurieren, müssen Sie für jede Instanz einen anderen `datastreamId` konfigurieren.
