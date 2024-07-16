---
keywords: Ziele aktivieren;Daten aktivieren
title: Aktivierungsübersicht
type: Tutorial
description: Erfahren Sie, wie Sie die in Adobe Experience Platform vorhandenen Zielgruppen für verschiedene Zieltypen aktivieren.
exl-id: 987af401-2d93-45b4-a8f9-191e6058e4da
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 25%

---

# Aktivierungsübersicht

>[!IMPORTANT]
> 
>* Um Daten zu aktivieren, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Um *identities* zu exportieren, benötigen Sie die Zugriffssteuerungsberechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [ ](/help/access-control/home.md#permissions). <br> ![Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Adobe Experience Platform unterstützt eine breite Palette von Zielen. Der Workflow für die Zielgruppenaktivierung variiert je nach dem Typ der von ihnen unterstützten Zielgruppendaten und der Häufigkeit des Datenexports.

## Aktivierungsmethoden {#activation-methods}

Nachdem Sie [Ihr Ziel ](connect-destination.md) konfiguriert haben, können Sie Zielgruppen auf verschiedene Arten aktivieren:

### Aktivieren von Zielgruppen aus dem Zielkatalog

Detaillierte Informationen zum Aktivieren von Zielgruppen für Ihr Ziel im Zielkatalog finden Sie in den folgenden Handbüchern:

* [Aktivieren von Zielgruppendaten für Streaming-Zielgruppen-Exportziele](activate-segment-streaming-destinations.md)
* [Aktivieren von Zielgruppendaten für Exportziele von Streaming-Profilen](activate-streaming-profile-destinations.md)
* [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](activate-batch-profile-destinations.md)

### Aktivieren von Zielgruppen über die Seite [!UICONTROL Durchsuchen]

Gehen Sie wie folgt vor, um Daten für Ihre Ziele über die Seite **[!UICONTROL Durchsuchen]** zu aktivieren.

1. Wechseln Sie zu **[!UICONTROL Verbindungen > Ziele]** und wählen Sie die Registerkarte **[!UICONTROL Durchsuchen]** aus.

   ![Registerkarte &quot;Durchsuchen&quot;](../assets/ui/activation-overview/browse-tab.png)

1. Suchen Sie die Zielverbindung, die Sie zum Aktivieren Ihrer Segmente verwenden möchten, wählen Sie die drei Punkte in der Spalte [!UICONTROL Name] aus und wählen Sie dann **[!UICONTROL Zielgruppen aktivieren]** aus.

   ![Schaltfläche &quot;Zielgruppen aktivieren&quot;](../assets/ui/activation-overview/activate-segments.png)

1. Führen Sie je nach ausgewähltem Ziel die in den folgenden Artikeln beschriebenen Schritte aus, beginnend mit dem Schritt **[!UICONTROL Segmente auswählen]** , um den Aktivierungs-Workflow abzuschließen:

   * [Aktivieren von Zielgruppendaten für Streaming-Zielgruppen-Exportziele](activate-segment-streaming-destinations.md)
   * [Aktivieren von Zielgruppendaten für Exportziele von Streaming-Profilen](activate-streaming-profile-destinations.md)
   * [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](activate-batch-profile-destinations.md)

### Aktivieren von Zielgruppen über die Seite mit den Zielgruppendetails {#activate-audience-details}

Auf der Seite mit den Zielgruppendetails können Sie Zielgruppen für Ziele aktivieren. Weitere Informationen finden Sie unter [Zielgruppendetails](../../segmentation/ui/audience-portal.md#audience-details) .

Führen Sie je nach ausgewähltem Ziel die in den folgenden Artikeln beschriebenen Schritte aus, um den Aktivierungs-Workflow abzuschließen:

* [Aktivieren von Zielgruppendaten für Streaming-Zielgruppen-Exportziele](activate-segment-streaming-destinations.md)
* [Aktivieren von Zielgruppendaten für Exportziele von Streaming-Profilen](activate-streaming-profile-destinations.md)
* [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](activate-batch-profile-destinations.md)
