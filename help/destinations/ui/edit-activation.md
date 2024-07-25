---
keywords: Aktivierung bearbeiten, Ziel bearbeiten, Ziel bearbeiten
title: Bearbeiten von Aktivierungsdatenflüssen
type: Tutorial
description: Führen Sie die Schritte in diesem Artikel aus, um einen vorhandenen Aktivierungsdatenfluss in Adobe Experience Platform zu bearbeiten.
exl-id: 0d79fbff-bfde-4109-8353-c7530e9719fb
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 25%

---

# Bearbeiten von Aktivierungsdatenflüssen {#edit-activation-flows}

In Adobe Experience Platform können Sie verschiedene Komponenten vorhandener Aktivierungsdatenflüsse an Ziele bearbeiten, z. B. die exportierten Zielgruppen und Profilattribute, die Exportfrequenz, ob der Aktivierungsdataflow aktiviert oder deaktiviert ist usw.

## Datenflüsse bearbeiten {#edit-dataflows}

Gehen Sie wie folgt vor, um vorhandene Aktivierungsdatenflüsse zu bearbeiten:

1. Melden Sie sich bei der [Experience Platform-Benutzeroberfläche](https://platform.adobe.com/) an und wählen Sie **[!UICONTROL Ziele]** über die linke Navigationsleiste aus. Wählen Sie **[!UICONTROL Durchsuchen]** in der oberen Kopfzeile aus, um Ihre vorhandenen Ziel-Datenflüsse anzuzeigen.

   ![Ziele durchsuchen](../assets/ui/edit-activation/browse-destinations.png)

2. Wählen Sie das Symbol ![Filter](/help/images/icons/filter.png) oben links, um das Sortier-Bedienfeld zu öffnen. Das Sortier-Bedienfeld bietet eine Liste aller Ihrer Ziele. Sie können mehr als ein Ziel aus der Liste auswählen, um eine gefilterte Auswahl von Datenflüssen anzuzeigen, die mit dem ausgewählten Ziel verknüpft sind.

   ![Ziele filtern](../assets/ui/edit-activation/filter-destinations.png)

3. Wählen Sie den Namen des Ziel-Datenflusses aus, den Sie bearbeiten möchten.

   ![Auswählen des Ziels](../assets/ui/edit-activation/destination-select.png)

4. Die Seite **[!UICONTROL Datenfluss wird ausgeführt]** für das Ziel wird angezeigt und zeigt die verfügbaren Steuerelemente an. An dieser Stelle können Sie mehrere Komponenten des Ziel-Datenflusses bearbeiten:

   * Wählen Sie in der rechten Leiste die Option **[!UICONTROL Zielgruppen aktivieren]** aus, um zu ändern, welche Zielgruppen oder Profilattribute an das Ziel gesendet werden. Dadurch gelangen Sie zum Aktivierungs-Workflow, der sich je nach Zieltyp unterscheidet. Weitere Informationen finden Sie in den Handbüchern zu:
      * [Aktivieren von Zielgruppendaten für Zielgruppen-Streaming-Ziele](./activate-segment-streaming-destinations.md) (z. B. Facebook oder Twitter);
      * [Aktivieren von Zielgruppendaten für profilbasierte Batch-Ziele](./activate-batch-profile-destinations.md) (z. B. Amazon S3 oder Oracle Eloqua);
      * [Aktivieren von Zielgruppendaten für Streaming-profilbasierte Ziele](./activate-streaming-profile-destinations.md) (z. B. HTTP-API oder Amazon Kinesis).

   * Darüber hinaus können Sie den Namen und die Beschreibung des Ziel-Datenflusses bearbeiten.
   * Sie können den Umschalter **[!UICONTROL Aktiviert]/[!UICONTROL Deaktiviert]** verwenden, um alle Datenexporte an das Ziel zu starten und anzuhalten.

   ![Zieldetails](../assets/ui/edit-activation/destination-details.png)

## Nächste Schritte {#next-steps}

In diesem Tutorial haben Sie erfolgreich den Arbeitsbereich **[!UICONTROL Ziele]** verwendet, um vorhandene Ziel-Datenflüsse zu aktualisieren.

Weitere Informationen zu Zielen finden Sie in der [Zielübersicht](../catalog/overview.md).
