---
keywords: Ziele aktivieren;Daten aktivieren
title: Aktivierungsübersicht
type: Tutorial
description: Erfahren Sie, wie Sie die Zielgruppendaten, die Sie in Adobe Experience Platform haben, für verschiedene Zieltypen aktivieren.
exl-id: 987af401-2d93-45b4-a8f9-191e6058e4da
source-git-commit: a6fe0f5a0c4f87ac265bf13cb8bba98252f147e0
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 34%

---

# Aktivierungsübersicht

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die [Zugriffskontrollberechtigungen](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**. Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Adobe Experience Platform unterstützt eine breite Palette von Zielen. Der Workflow für die Zielgruppenaktivierung variiert je nach dem Typ der von ihnen unterstützten Zielgruppendaten und der Häufigkeit des Datenexports.

## Aktivierungsmethoden {#activation-methods}

Nach [Ziel konfigurieren](connect-destination.md)können Sie Zielgruppensegmente auf mehrere Arten aktivieren:

### Aktivieren von Zielgruppen aus dem Zielkatalog

Detaillierte Informationen zum Aktivieren von Zielgruppen für Ihr Ziel im Zielkatalog finden Sie in den folgenden Handbüchern:

* [Aktivieren von Zielgruppendaten für Streaming-Segmentexportziele](activate-segment-streaming-destinations.md)
* [Aktivieren von Zielgruppendaten für Exportziele von Streaming-Profilen](activate-streaming-profile-destinations.md)
* [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](activate-batch-profile-destinations.md)

### Aktivieren Sie Zielgruppen über die [!UICONTROL Durchsuchen] page

Führen Sie die folgenden Schritte aus, um Daten für Ihre Ziele über die **[!UICONTROL Durchsuchen]** Seite.

1. Navigieren Sie zu **[!UICONTROL Verbindungen > Ziele]** und wählen Sie die **[!UICONTROL Durchsuchen]** Registerkarte.

   ![Registerkarte &quot;Durchsuchen&quot;](../assets/ui/activation-overview/browse-tab.png)

1. Suchen Sie die Zielverbindung, die Sie zum Aktivieren Ihrer Segmente verwenden möchten, und wählen Sie die drei Punkte im [!UICONTROL Name] und wählen Sie **[!UICONTROL Segmente aktivieren]**.

   ![Schaltfläche „Segmente aktivieren“](../assets/ui/activation-overview/activate-segments.png)

1. Führen Sie je nach ausgewähltem Ziel die in den folgenden Artikeln beschriebenen Schritte aus, beginnend mit dem **[!UICONTROL Segmente auswählen]** Schritt, um den Aktivierungs-Workflow abzuschließen:

   * [Aktivieren von Zielgruppendaten für Streaming-Segmentexportziele](activate-segment-streaming-destinations.md)
   * [Aktivieren von Zielgruppendaten für Exportziele von Streaming-Profilen](activate-streaming-profile-destinations.md)
   * [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](activate-batch-profile-destinations.md)

### Aktivieren von Zielgruppen über die Segmentdetailseite {#activate-segment-details}

Sie können Segmente für Ziele über die Segmentdetailseite aktivieren. Siehe [Segmentdetails](../../segmentation/ui/overview.md#segment-details) für weitere Informationen.

Führen Sie je nach ausgewähltem Ziel die in den folgenden Artikeln beschriebenen Schritte aus, um den Aktivierungs-Workflow abzuschließen:

* [Aktivieren von Zielgruppendaten für Streaming-Segmentexportziele](activate-segment-streaming-destinations.md)
* [Aktivieren von Zielgruppendaten für Exportziele von Streaming-Profilen](activate-streaming-profile-destinations.md)
* [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](activate-batch-profile-destinations.md)
