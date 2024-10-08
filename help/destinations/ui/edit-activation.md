---
keywords: Aktivierung bearbeiten, Ziel bearbeiten, Ziel bearbeiten
title: Bearbeiten von Aktivierungsdatenflüssen
type: Tutorial
description: Führen Sie die Schritte in diesem Artikel aus, um einen vorhandenen Aktivierungsdatenfluss in Adobe Experience Platform zu bearbeiten.
exl-id: 0d79fbff-bfde-4109-8353-c7530e9719fb
source-git-commit: ca33131c505803b74075f6d8331095b016a301a0
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 18%

---

# Bearbeiten von Aktivierungsdatenflüssen {#edit-activation-flows}

In Adobe Experience Platform können Sie verschiedene Komponenten vorhandener Aktivierungsdatenflüsse zu Zielen konfigurieren, z. B.:

* [Aktivierungsdataflows aktivieren oder deaktivieren](#enable-disable-dataflows);
* [Hinzufügen zusätzlicher Zielgruppen und Profilattribute](#add-audiences) zu Aktivierungsdatenflüssen;
* [Fügen Sie zusätzliche Datensätze ](#add-datasets) zu Aktivierungs-Workflows hinzu.
* [Bearbeiten von Namen und Beschreibungen](#edit-names-descriptions) für Ihre Aktivierungsdatenflüsse;

<!-- * [Apply access labels](#apply-access-labels) to exported data; -->

## Datenflüsse zur Browseraktivierung {#browse-activation-dataflows}

Gehen Sie wie folgt vor, um die vorhandenen Aktivierungsdaten zu durchsuchen und den zu bearbeitenden zu identifizieren.

1. Melden Sie sich bei der [Experience Platform-Benutzeroberfläche](https://platform.adobe.com/) an und wählen Sie **[!UICONTROL Ziele]** über die linke Navigationsleiste aus. Wählen Sie **[!UICONTROL Durchsuchen]** in der oberen Kopfzeile aus, um Ihre vorhandenen Ziel-Datenflüsse anzuzeigen.

   ![Ziele durchsuchen](../assets/ui/edit-activation/browse-destinations.png)

2. Wählen Sie das Symbol ![Filter](../../images/icons/filter.png) oben links, um das Sortier-Bedienfeld zu öffnen. Das Sortier-Bedienfeld bietet eine Liste aller Ihrer Ziele. Sie können mehr als ein Ziel aus der Liste auswählen, um eine gefilterte Auswahl von Datenflüssen anzuzeigen, die mit dem ausgewählten Ziel verknüpft sind.

   ![Ziele filtern](../assets/ui/edit-activation/filter-destinations.png)

3. Wählen Sie den Namen des Ziel-Datenflusses aus, den Sie bearbeiten möchten.

   ![Auswählen des Ziels](../assets/ui/edit-activation/destination-select.png)

4. Die Seite **[!UICONTROL Datenfluss wird ausgeführt]** für das Ziel wird angezeigt und zeigt die verfügbaren Steuerelemente an. Je nach Zieltyp können Sie verschiedene Datenflussvorgänge ausführen. Weitere Informationen finden Sie in den nächsten Abschnitten für jeden unterstützten Datenfluss-Vorgang.

## Aktivierungs-Datenflüsse aktivieren oder deaktivieren {#enable-disable-dataflows}

Mit dem Umschalter **[!UICONTROL Aktiviert]/[!UICONTROL Deaktiviert]** können Sie alle Datenexporte an das Ziel starten oder anhalten.

![Experience Platform UI-Bild, das den Umschalter für die Ausführung des Datenflusses &quot;Aktiviert/Deaktiviert&quot;anzeigt.](../assets/ui/edit-activation/enable-toggle.png)

## Hinzufügen von Zielgruppen zu einem Aktivierungsdatenfluss {#add-audiences}

Wählen Sie in der rechten Leiste die Option **[!UICONTROL Zielgruppen aktivieren]** aus, um zu ändern, welche Zielgruppen oder Profilattribute an das Ziel gesendet werden. Dadurch gelangen Sie zum Aktivierungs-Workflow, der sich je nach Zieltyp unterscheidet.

![Experience Platform UI-Bild, das die Option zum Ausführen des Datenflusses &quot;Zielgruppen aktivieren&quot;anzeigt.](../assets/ui/edit-activation/activate-audiences.png)

Weitere Informationen zu den Aktivierungs-Workflows für jeden Zieltyp finden Sie in den folgenden Handbüchern:

* [Aktivieren von Zielgruppen für Streaming-Ziele ](./activate-segment-streaming-destinations.md) (z. B. Facebook oder Twitter);
* [Aktivieren von Zielgruppen für Batch-Profilexportziele ](./activate-batch-profile-destinations.md) (z. B. Amazon S3 oder Oracle Eloqua);
* [Aktivieren Sie Zielgruppen für Streaming-Profilexportziele ](./activate-streaming-profile-destinations.md) (z. B. HTTP-API oder Amazon Kinesis).

## Hinzufügen von Datensätzen zu einem Aktivierungs-Datenfluss {#add-datasets}

Wählen Sie in der rechten Leiste **[!UICONTROL Datensätze exportieren]** aus, um zusätzliche Datensätze auszuwählen, die an Ihr Ziel exportiert werden sollen. Mit dieser Option gelangen Sie zum Workflow [Datensatzexport](export-datasets.md) .

>[!NOTE]
>
>Diese Option ist nur für [Ziele sichtbar, die den Datensatzexport unterstützen](export-datasets.md#supported-destinations).

![Experience Platform UI-Bild, das die Ausführungsoption &quot;Datensatz-Datenfluss exportieren&quot;anzeigt.](../assets/ui/edit-activation/export-datasets.png)

<!-- ## Apply access labels {#apply-access-labels}

Select **[!UICONTROL Apply access labels]** to edit the data usage labels for the exported data. See the [data usage labels documentation](../../data-governance/labels/overview.md) to learn more.

![Experience Platform UI image showing the Export datasets dataflow run option.](../assets/ui/edit-activation/apply-access-labels.png) -->

## Bearbeiten der Namen und Beschreibungen des Aktivierungsdatafs {#edit-names-descriptions}

Verwenden Sie die Felder **[!UICONTROL Zielname]** und **[!UICONTROL Beschreibung]**, um den Namen und die Beschreibung des Aktivierungsdataflods zu bearbeiten.

![Zieldetails](../assets/ui/edit-activation/edit-destination-name-description.png)

## Nächste Schritte {#next-steps}

In diesem Tutorial haben Sie erfolgreich den Arbeitsbereich **[!UICONTROL Ziele]** verwendet, um vorhandene Ziel-Datenflüsse zu aktualisieren.

Weitere Informationen zu Zielen finden Sie in der [Zielübersicht](../catalog/overview.md).
