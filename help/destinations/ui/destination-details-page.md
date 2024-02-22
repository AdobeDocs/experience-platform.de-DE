---
keywords: Ziele; Ziel; Zieldetailseite; Zieldetailseite; Zieldetailseite
title: Anzeigen von Zieldetails
description: Die Detailseite für ein einzelnes Ziel bietet einen Überblick über die Zieldetails. Zu den Zieldetails gehören der Zielname, die ID, die dem Ziel zugeordneten Zielgruppen und die Steuerelemente zum Bearbeiten der Aktivierung und zum Aktivieren und Deaktivieren des Datenflusses.
exl-id: e44e2b2d-f477-4516-8a47-3e95c2d85223
source-git-commit: 5e3c4f5c9a5540e0a796785c743a77c1e11821f8
workflow-type: tm+mt
source-wordcount: '1100'
ht-degree: 10%

---

# Anzeigen von Zieldetails

## Übersicht {#overview}

In der Adobe Experience Platform-Benutzeroberfläche können Sie die Attribute und Aktivitäten Ihrer Ziele anzeigen und überwachen. Zu diesen Details gehören der Name und die ID des Ziels, Steuerelemente zum Aktivieren oder Deaktivieren der Ziele und mehr. Zu den Details gehören auch Metriken für aktivierte Profildatensätze, aktivierte, fehlgeschlagene und ausgeschlossene Identitäten sowie ein Verlauf der Datenfluss-Läufe.

>[!NOTE]
>
>Die Zieldetailseite ist Teil der [!UICONTROL Ziele] Arbeitsbereich im [!DNL Platform] [!DNL UI]. Siehe [[!UICONTROL Ziele] Arbeitsbereich - Übersicht](./destinations-workspace.md) für weitere Informationen.

## Anzeigen von Zieldetails {#view-details}

Gehen Sie wie folgt vor, um weitere Details zu einem vorhandenen Ziel anzuzeigen.

1. Melden Sie sich bei der [Experience Platform-Benutzeroberfläche](https://platform.adobe.com/) an und wählen Sie **[!UICONTROL Ziele]** über die linke Navigationsleiste aus. Auswählen **[!UICONTROL Durchsuchen]** aus der oberen Kopfzeile, um Ihre vorhandenen Ziele anzuzeigen.

   ![Ziele durchsuchen](../assets/ui/details-page/browse-destinations.png)

1. Wählen Sie das Symbol ![Filter](../assets/ui/details-page/filter.png) oben links, um das Sortier-Bedienfeld zu öffnen. Das Sortier-Bedienfeld bietet eine Liste aller Ihrer Ziele. Sie können mehr als ein Ziel aus der Liste auswählen, um eine gefilterte Auswahl von Datenflüssen anzuzeigen, die mit dem ausgewählten Ziel verknüpft sind.

   ![Ziele filtern](../assets/ui/details-page/filter-destinations.png)

1. Wählen Sie den Namen des Ziels aus, das Sie anzeigen möchten.

   ![Auswählen des Ziels](../assets/ui/details-page/destination-select.png)

1. Die Detailseite für das Ziel wird mit den verfügbaren Steuerelementen angezeigt.

   ![Zieldetails](../assets/ui/details-page/destination-details.png)

## rechte Leiste {#right-rail}

In der rechten Leiste werden die grundlegenden Informationen zum ausgewählten Ziel angezeigt.

![rechte Leiste](../assets/ui/details-page/right-sidebar.png)

Die folgende Tabelle enthält die von der rechten Leiste bereitgestellten Steuerelemente und Details:

| Element in der rechten Leiste | Beschreibung |
| --- | --- |
| [!UICONTROL Aktivieren von Zielgruppen] | Wählen Sie dieses Steuerelement aus, um zu bearbeiten, welche Zielgruppen dem Ziel zugeordnet sind, Exportpläne zu aktualisieren oder zugeordnete Attribute und Identitäten hinzuzufügen und zu entfernen. Die Handbücher finden Sie in [Aktivieren von Zielgruppendaten für Zielgruppen-Streaming-Ziele](./activate-segment-streaming-destinations.md), [Aktivieren von Zielgruppendaten für profilbasierte Batch-Ziele](./activate-batch-profile-destinations.md), und [Aktivieren von Zielgruppendaten für Streaming profilbasierter Ziele](./activate-streaming-profile-destinations.md) für weitere Informationen. |
| [!UICONTROL Löschen] | Ermöglicht das Löschen dieses Datenflusses und die Aufhebung der Zuordnung der zuvor aktivierten Zielgruppen, falls vorhanden. |
| [!UICONTROL Zielname] | Dieses Feld kann bearbeitet werden, um den Zielnamen zu aktualisieren. |
| [!UICONTROL Beschreibung] | Dieses Feld kann bearbeitet werden, um eine optionale Beschreibung zum Ziel zu aktualisieren oder hinzuzufügen. |
| [!UICONTROL Ziel] | Die Zielplattform, an die Zielgruppen gesendet werden. Siehe [Zielkatalog](../catalog/overview.md) für weitere Informationen. |
| [!UICONTROL Status] | Gibt an, ob das Ziel aktiviert oder deaktiviert ist. |
| [!UICONTROL Marketing-Aktionen] | Gibt die Marketing-Aktionen (Anwendungsfälle) an, die für dieses Ziel aus Data-Governance-Gründen gelten. |
| [!UICONTROL Kategorie] | Gibt den Zieltyp an. Siehe [Zielkatalog](../catalog/overview.md) für weitere Informationen. |
| [!UICONTROL Verbindungstyp] | Gibt das Formular an, mit dem Ihre Zielgruppen an das Ziel gesendet werden. Mögliche Werte sind [!UICONTROL Cookie] und [!UICONTROL Profilbasiert]. |
| [!UICONTROL Häufigkeit] | Gibt an, wie oft die Zielgruppen an das Ziel gesendet werden. Mögliche Werte sind [!UICONTROL Streaming] und [!UICONTROL Batch]. |
| [!UICONTROL Identität] | Stellt den vom Ziel akzeptierten Identitäts-Namespace dar, z. B. `GAID`, `IDFA`oder `email`. Weitere Informationen zu akzeptierten Identitäts-Namespaces finden Sie im Abschnitt [Übersicht über Identitäts-Namespace](../../identity-service/features/namespaces.md). |
| [!UICONTROL Erstellt von] | Gibt den Benutzer an, der dieses Ziel erstellt hat. |
| [!UICONTROL Erstellt] | Gibt den UTC-Datum an, zu dem dieses Ziel erstellt wurde. |

{style="table-layout:auto"}

## [!UICONTROL Aktiviert]/[!UICONTROL Behinderte] Umschalten {#enabled-disabled-toggle}

Sie können die **[!UICONTROL Aktiviert]/[!UICONTROL Behinderte]** Umschalten, um alle Datenexporte an das Ziel zu starten und anzuhalten.

![Umschalten zwischen Datenfluss und Datenfluss aktivieren oder deaktivieren](../assets/ui/details-page/enable-disable.png)

## [!UICONTROL Datenfluss-Abläufe] {#dataflow-runs}

Die [!UICONTROL Datenfluss-Abläufe] -Tab enthält Metrikdaten zu Ihren Datenflüssen, die an Batch- und Streaming-Ziele ausgeführt werden. Siehe Abschnitt [Überwachen von Datenflüssen](monitor-dataflows.md) für Details und Metrikdefinitionen.

>[!NOTE]
>
>* Die Funktion zur Zielüberwachung wird derzeit für alle Ziele in Experience Platform unterstützt *Außer* die [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md), [Benutzerdefinierte Personalisierung](/help/destinations/catalog/personalization/custom-personalization.md) und [Experience Cloud Audiences](/help/destinations/catalog/adobe/experience-cloud-audiences.md) Ziele.
>* Für [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md), [Azure Event Hubs](/help/destinations/catalog/cloud-storage/azure-event-hubs.md), und [HTTP-API](/help/destinations/catalog/streaming/http-destination.md) Ziele, werden die Metriken geschätzt, die sich auf ausgeschlossene, fehlgeschlagene und aktivierte Identitäten beziehen. Höhere Volumina von Aktivierungsdaten führen zu einer höheren Genauigkeit der Metriken.

![Datenfluss-Ausführungsansicht](../assets/ui/details-page/dataflow-runs.png)

### Dauer der Datenflüsse {#dataflow-runs-duration}

Es gibt einen Unterschied in der angezeigten Dauer von Datenfluss-Läufen zwischen Streaming- und dateibasierten Zielen.

### Streaming-Ziele {#streaming}

Während **[!UICONTROL Verarbeitungsdauer]** für die meisten Streaming-Datenfluss-Läufe etwa vier Stunden beträgt, wie in der Abbildung unten dargestellt, ist die tatsächliche Verarbeitungszeit für jeden Datenfluss viel kürzer. Dataflow-Run-Fenster bleiben länger geöffnet, falls Experience Platform erneut Aufrufe an das Ziel tätigen muss, und stellen Sie sicher, dass es keine verspäteten Daten für das gleiche Zeitfenster verpasst.

![Bild der Seite &quot;Datenfluss&quot;, auf der die Spalte Verarbeitungszeit für ein Streaming-Ziel hervorgehoben ist.](/help/destinations/assets/ui/details-page/processing-time-dataflow-run-streaming.png)

Weitere Informationen finden Sie unter [Datenfluss läuft zu Streaming-Zielen](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-streaming-destinations) in der Überwachungsdokumentation.

### Dateibasierte Ziele {#file-based}

Für Datenflüsse, die an dateibasierte Ziele ausgeführt werden, muss die Variable **[!UICONTROL Verarbeitungsdauer]** hängt von der Größe der zu exportierenden Daten und der Systemlast ab. Beachten Sie außerdem, dass der Datenfluss zu dateibasierten Zielen nach Zielgruppen aufgeschlüsselt wird.

![Bild der Seite Datenfluss wird ausgeführt, wobei die Spalte Verarbeitungszeit für ein dateibasiertes Ziel hervorgehoben ist.](/help/destinations/assets/ui/details-page/processing-time-dataflow-run-file-based.png)

Weitere Informationen finden Sie unter [Datenfluss wird an Batch-(dateibasierte) Ziele ausgeführt](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) in der Überwachungsdokumentation.

## [!UICONTROL Aktivierungsdaten] {#activation-data}

Die [!UICONTROL Aktivierungsdaten] zeigt eine Liste der Zielgruppen an, die dem Ziel zugeordnet wurden, einschließlich des Anfangs- und Enddatums (falls zutreffend) sowie anderer relevanter Informationen für den Datenexport, wie Exporttyp, -zeitplan und -frequenz. Um Details zu einer bestimmten Zielgruppe anzuzeigen, wählen Sie deren Namen aus der Liste aus.

>[!TIP]
>
>Um Details zu den Attributen und Identitäten anzuzeigen und zu bearbeiten, die einem Ziel zugeordnet sind, wählen Sie **[!UICONTROL Aktivieren von Zielgruppen]** im [rechte Leiste](#right-rail).

![Batch-Ziel für die Aktivierungsdatenansicht](../assets/ui/details-page/activation-data-batch.png)

![Streaming-Ziel für Aktivierungsdaten-Ansicht](../assets/ui/details-page/activation-data-streaming.png)

<!-- ### Remove multiple audiences from activation flows {#bulk-remove}

To remove multiple audiences from existing activation flows, select the audiences and then select **[!UICONTROL Remove audiences]**.

![Activation data screen highlighting the Remove audiences option.](../assets/ui/details-page/bulk-remove-audiences.png) -->

### [!BADGE Beta]{type=Informative} Export mehrerer Dateien On-Demand an Batch-Ziele {#bulk-export}

>[!NOTE]
>
Diese Funktion befindet sich in der Beta-Phase und steht nur ausgewählten Kunden zur Verfügung. Wenden Sie sich an Ihren Adobe-Support-Mitarbeiter, um Zugriff auf diese Funktion anzufordern.

Sie können [mehrere Dateien On-Demand exportieren](../ui/export-file-now.md) aus dem **[!UICONTROL Aktivierungsdaten]** Seite. Wählen Sie dazu die Zielgruppen aus, für die Sie Dateien bei Bedarf exportieren möchten, und wählen Sie die **[!UICONTROL Datei jetzt exportieren]** -Steuerelement, um einen einmaligen Export Trigger, der eine Datei für jede ausgewählte Zielgruppe an Ihr Batch-Ziel sendet.

![Bild, das die Schaltfläche Datei jetzt exportieren markiert](../assets/ui/details-page/bulk-export-file-now.png)

### [!BADGE Beta]{type=Informative} Bearbeiten Sie die Aktivierungszeitpläne für mehrere Zielgruppen, die an Batch-Ziele exportiert werden {#bulk-edit-schedule}

>[!NOTE]
>
Diese Funktion befindet sich in der Beta-Phase und steht nur ausgewählten Kunden zur Verfügung. Wenden Sie sich an Ihren Adobe-Support-Mitarbeiter, um Zugriff auf diese Funktion anzufordern.

Um den vorhandenen Aktivierungszeitplan für mehrere Zielgruppen gleichzeitig zu bearbeiten, wählen Sie die gewünschten Zielgruppen aus und klicken Sie auf **[!UICONTROL Zeitplan bearbeiten]**. Ausführliche Informationen zum Definieren oder Bearbeiten eines Exportzeitplans finden Sie im Abschnitt [Zielgruppenexport planen](../ui/activate-batch-profile-destinations.md#scheduling) Abschnitt.

![Aktivierungsdatenbildschirm, der die Option zum Bearbeiten von Aktivierungszeitplänen für mehrere Zielgruppen hervorhebt.](../assets/ui/details-page/bulk-edit-schedule.png)

>[!NOTE]
>
Weitere Informationen zum Erkunden der Detailseite einer Audience finden Sie im Abschnitt [Übersicht über die Segmentierungsbenutzeroberfläche](../../segmentation/ui/overview.md#segment-details).
