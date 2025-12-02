---
title: datastreamId
description: Bestimmen Sie die Datenstrom-ID, an die Sie Daten senden möchten.
exl-id: 2d709f70-c014-4868-b2f5-17e8b88343d1
source-git-commit: b9fea4833c4fe869b27c1270aafd3f7ed62d59db
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 1%

---

# `datastreamId`

Die `datastreamId`-Eigenschaft ist eine Zeichenfolge, die bestimmt[ an welchen ](/help/datastreams/overview.md)Datenstrom) in Adobe Experience Platform Sie Daten senden möchten. Diese Eigenschaft ist erforderlich, wenn Daten an Adobe gesendet werden. Web SDK-Versionen 2.20.0 oder früher verwenden stattdessen `edgeConfigId`.

So suchen Sie eine Datenstrom-ID:

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei ](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Data Collection]** > **[!UICONTROL Datastreams]**.
1. Verwenden Sie das Suchfeld, um den gewünschten Datenstrom zu finden, und wählen Sie dann **[!UICONTROL Copy]** ![Kopieren](../../assets/copy.png) neben der Datenstrom-ID aus.

Alternativ können Sie den gewünschten Datenstromnamen auswählen. Die Datenstrom-ID wird dann in der rechten Spalte angezeigt, damit Sie sie kopieren können.

## Code-Beispiel

Legen Sie beim Ausführen des `datastreamID`-Befehls die `configure`-Zeichenfolgeneigenschaft fest. Diese Eigenschaft ist für alle Implementierungen von Web SDK erforderlich. Wenn Sie diese Eigenschaft auslassen, weiß Web SDK nicht, an welchen Datenstrom Daten gesendet werden sollen, sodass diese Daten dauerhaft verloren gehen.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
});
```

>[!NOTE]
>
>Wenn Sie mehrere Instanzen von Web SDK auf einer Seite konfigurieren, müssen Sie für jede Instanz einen anderen `datastreamId` konfigurieren.

## Wählen Sie die Datenstrom-ID mithilfe der Tag-Erweiterung „Web SDK&quot; aus

Siehe [Datenstromkonfigurationseinstellungen](/help/tags/extensions/client/web-sdk/configure/datastreams.md) in der Tag-Erweiterungsdokumentation für Web SDK , um zu erfahren, wie Sie den gewünschten Datenstrom für jede Umgebung mithilfe von Tags festlegen. Sie können Daten an verschiedene Datenströme für Produktions-, Staging- und Entwicklungs-Tag-Umgebungen senden.
