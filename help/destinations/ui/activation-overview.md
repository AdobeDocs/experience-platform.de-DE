---
keywords: Ziele aktivieren;Daten aktivieren
title: Aktivierungsübersicht
type: Tutorial
description: Erfahren Sie, wie Sie die in Adobe Experience Platform vorhandenen Zielgruppen für verschiedene Zieltypen aktivieren.
exl-id: 987af401-2d93-45b4-a8f9-191e6058e4da
source-git-commit: fbc2a6c81682797af4674adabff358a62d973007
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 25%

---

# Aktivierungsübersicht

>[!IMPORTANT]
> 
>* Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Anzeigen von Profilen]**, und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Export *identities*, benötigen Sie die **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). <br> ![Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Adobe Experience Platform unterstützt eine breite Palette von Zielen. Der Workflow für die Zielgruppenaktivierung variiert je nach dem Typ der von ihnen unterstützten Zielgruppendaten und der Häufigkeit des Datenexports.

## Aktivierungsmethoden {#activation-methods}

Nach [Ziel konfigurieren](connect-destination.md)können Sie Zielgruppen auf verschiedene Weise aktivieren:

### Aktivieren von Zielgruppen aus dem Zielkatalog

Detaillierte Informationen zum Aktivieren von Zielgruppen für Ihr Ziel im Zielkatalog finden Sie in den folgenden Handbüchern:

* [Aktivieren von Zielgruppendaten für Streaming-Zielgruppen-Exportziele](activate-segment-streaming-destinations.md)
* [Aktivieren von Zielgruppendaten für Exportziele von Streaming-Profilen](activate-streaming-profile-destinations.md)
* [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](activate-batch-profile-destinations.md)

### Aktivieren Sie Zielgruppen über die [!UICONTROL Durchsuchen] page

Führen Sie die folgenden Schritte aus, um Daten für Ihre Ziele über die **[!UICONTROL Durchsuchen]** Seite.

1. Navigieren Sie zu **[!UICONTROL Verbindungen > Ziele]** und wählen Sie die **[!UICONTROL Durchsuchen]** Registerkarte.

   ![Registerkarte &quot;Durchsuchen&quot;](../assets/ui/activation-overview/browse-tab.png)

1. Suchen Sie die Zielverbindung, die Sie zum Aktivieren Ihrer Segmente verwenden möchten, und wählen Sie die drei Punkte im [!UICONTROL Name] und wählen Sie **[!UICONTROL Aktivieren von Zielgruppen]**.

   ![Schaltfläche &quot;Zielgruppen aktivieren&quot;](../assets/ui/activation-overview/activate-segments.png)

1. Führen Sie je nach ausgewähltem Ziel die in den folgenden Artikeln beschriebenen Schritte aus, beginnend mit dem **[!UICONTROL Segmente auswählen]** Schritt, um den Aktivierungs-Workflow abzuschließen:

   * [Aktivieren von Zielgruppendaten für Streaming-Zielgruppen-Exportziele](activate-segment-streaming-destinations.md)
   * [Aktivieren von Zielgruppendaten für Exportziele von Streaming-Profilen](activate-streaming-profile-destinations.md)
   * [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](activate-batch-profile-destinations.md)

### Aktivieren von Zielgruppen über die Seite mit den Zielgruppendetails {#activate-audience-details}

Auf der Seite mit den Zielgruppendetails können Sie Zielgruppen für Ziele aktivieren. Siehe [Zielgruppendetails](../../segmentation/ui/overview.md#audience-details) für weitere Informationen.

Führen Sie je nach ausgewähltem Ziel die in den folgenden Artikeln beschriebenen Schritte aus, um den Aktivierungs-Workflow abzuschließen:

* [Aktivieren von Zielgruppendaten für Streaming-Zielgruppen-Exportziele](activate-segment-streaming-destinations.md)
* [Aktivieren von Zielgruppendaten für Exportziele von Streaming-Profilen](activate-streaming-profile-destinations.md)
* [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](activate-batch-profile-destinations.md)
