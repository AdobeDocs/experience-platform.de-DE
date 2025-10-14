---
keywords: Ziele aktivieren;Daten aktivieren
title: Aktivierungsübersicht
type: Tutorial
description: Erfahren Sie, wie Sie die Zielgruppen in Adobe Experience Platform für verschiedene Zieltypen aktivieren.
exl-id: 987af401-2d93-45b4-a8f9-191e6058e4da
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 25%

---

# Aktivierungsübersicht

>[!IMPORTANT]
> 
>* Zum Aktivieren von Daten benötigen Sie die Berechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**&#x200B;[Zugriffssteuerung](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die Berechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffssteuerung](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Adobe Experience Platform unterstützt eine Vielzahl von Zielen. Der Zielgruppen-Aktivierungs-Workflow variiert je nach Ziel und Art der unterstützten Zielgruppendaten sowie der Häufigkeit des Datenexports.

## Aktivierungsmethoden {#activation-methods}

Nach dem [Konfigurieren Ihres Ziels](connect-destination.md) können Sie Zielgruppen auf verschiedene Arten aktivieren:

### Aktivieren von Zielgruppen über den Zielkatalog

In den folgenden Handbüchern finden Sie detaillierte Informationen zum Aktivieren von Zielgruppen für Ihr Ziel aus dem Zielkatalog:

* [Aktivieren von Zielgruppendaten für Streaming-Zielgruppen-Exportziele](activate-segment-streaming-destinations.md)
* [Aktivieren von Zielgruppendaten für Exportziele von Streaming-Profilen](activate-streaming-profile-destinations.md)
* [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](activate-batch-profile-destinations.md)

### Aktivieren von Zielgruppen über die Seite [!UICONTROL Durchsuchen]

Gehen Sie wie folgt vor, um von der Seite „Durchsuchen **[!UICONTROL Daten für Ihre Ziele]** aktivieren.

1. Navigieren Sie **[!UICONTROL Verbindungen > Ziele]** und wählen Sie die Registerkarte **[!UICONTROL Durchsuchen]** aus.

   ![Registerkarte „Durchsuchen“](../assets/ui/activation-overview/browse-tab.png)

1. Suchen Sie die Zielverbindung, die Sie zum Aktivieren Ihrer Segmente verwenden möchten, wählen Sie die drei Punkte in der Spalte [!UICONTROL Name] und dann **[!UICONTROL Zielgruppen aktivieren]** aus.

   ![Schaltfläche „Zielgruppen aktivieren“](../assets/ui/activation-overview/activate-segments.png)

1. Führen Sie je nach ausgewähltem Ziel die in den folgenden Artikeln beschriebenen Schritte aus, beginnend mit dem Schritt **[!UICONTROL Segmente auswählen]**, um den Aktivierungs-Workflow abzuschließen:

   * [Aktivieren von Zielgruppendaten für Streaming-Zielgruppen-Exportziele](activate-segment-streaming-destinations.md)
   * [Aktivieren von Zielgruppendaten für Exportziele von Streaming-Profilen](activate-streaming-profile-destinations.md)
   * [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](activate-batch-profile-destinations.md)

### Aktivieren von Zielgruppen über die Seite mit den Zielgruppendetails {#activate-audience-details}

Sie können Zielgruppen für Ziele über die Seite mit den Zielgruppendetails aktivieren. Weitere Informationen finden [&#x200B; unter &#x200B;](../../segmentation/ui/audience-portal.md#audience-details)Zielgruppendetails“.

Führen Sie je nach ausgewähltem Ziel die in den folgenden Artikeln beschriebenen Schritte aus, um den Aktivierungs-Workflow abzuschließen:

* [Aktivieren von Zielgruppendaten für Streaming-Zielgruppen-Exportziele](activate-segment-streaming-destinations.md)
* [Aktivieren von Zielgruppendaten für Exportziele von Streaming-Profilen](activate-streaming-profile-destinations.md)
* [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](activate-batch-profile-destinations.md)
