---
keywords: Ziele;Ziel;Detailseite Ziele;Detailseite Ziele
title: Anzeigen von Zieldetails
description: Die Detailseite für ein einzelnes Ziel bietet einen Überblick über die Zieldetails. Zu den Zieldetails gehören der Zielname, die ID, die dem Ziel zugeordneten Zielgruppen sowie Steuerelemente zum Bearbeiten der Aktivierung und zum Aktivieren und Deaktivieren des Datenflusses.
exl-id: e44e2b2d-f477-4516-8a47-3e95c2d85223
source-git-commit: 20427c4c8826905a77fac04d055d523b12a6f739
workflow-type: tm+mt
source-wordcount: '1206'
ht-degree: 6%

---

# Anzeigen von Zieldetails

## Überblick {#overview}

In der [!DNL Adobe Experience Platform] Benutzeroberfläche können Sie die Attribute und Aktivitäten Ihrer Ziele anzeigen und überwachen. Zu diesen Details gehören der Name und die ID des Ziels, Steuerelemente zum Aktivieren oder Deaktivieren der Ziele und mehr. Zu den Details gehören auch Metriken für aktivierte Profildatensätze, aktivierte, fehlgeschlagene und ausgeschlossene Identitäten und ein Verlauf der Datenflussausführungen.

>[!NOTE]
>
>Die Seite mit den Zieldetails ist Teil des [!UICONTROL Destinations] Arbeitsbereichs im [!DNL Experience Platform] [!DNL UI]. Weiterführende Informationen dazu finden Sie in der Übersicht [[!UICONTROL Destinations] &#x200B;](./destinations-workspace.md) Workspace .

## Anzeigen von Zieldetails {#view-details}

Gehen Sie wie folgt vor, um weitere Details zu einem vorhandenen Ziel anzuzeigen. Sie können die Ziel-ID eines Ziels, den Benutzer, der das Ziel erstellt hat, den Zeitpunkt seiner Erstellung und weitere Informationen ermitteln.

1. Wechseln Sie zur [Experience Platform](https://platform.adobe.com/)Benutzeroberfläche und wählen Sie **[!UICONTROL Destinations]** über die linke Navigationsleiste aus. Wählen Sie **[!UICONTROL Browse]** in der oberen Kopfzeile aus, um Ihre vorhandenen Ziele anzuzeigen.

   ![Ziele durchsuchen](../assets/ui/details-page/browse-destinations.png)

2. Wählen Sie das Symbol ![Filter](../../images/icons/filter.png) oben links, um das Sortier-Bedienfeld zu öffnen. Das Sortier-Bedienfeld bietet eine Liste aller Ihrer Ziele. Sie können mehr als ein Ziel aus der Liste auswählen, um eine gefilterte Auswahl von Datenflüssen anzuzeigen, die mit dem ausgewählten Ziel verknüpft sind.

   ![Ziele filtern](../assets/ui/details-page/filter-destinations.png)

3. Wählen Sie die Zeile des Ziels aus, für die Sie weitere Informationen aufrufen möchten. Dadurch wird eine rechte Leiste mit Informationen zum Ziel angezeigt, einschließlich der Ziel-ID, des Benutzers, der die Zielverbindung erstellt hat, und anderer Informationen.

   ![Ziel-ID in der rechten Leiste](../assets/ui/details-page/right-rail-info-including-destination-id.png)

4. Alternativ können Sie auch andere Informationen zum Ziel aufrufen, indem Sie *den Namen des Ziels* auswählen, das Sie anzeigen möchten.

   ![Auswählen des Ziels](../assets/ui/details-page/destination-select.png)

5. Die Detailseite für das Ziel wird in der rechten Leiste mit den verfügbaren Steuerelementen angezeigt.

   ![Zieldetails](../assets/ui/details-page/destination-details.png)

## Rechte Leiste {#right-rail}

In der rechten Leiste werden die grundlegenden Informationen zum ausgewählten Ziel angezeigt.

![Rechte Leiste](../assets/ui/details-page/right-sidebar.png)

Die folgende Tabelle enthält die Steuerelemente und Details, die von der rechten Leiste bereitgestellt werden:

| Element in der rechten Leiste | Beschreibung |
| --- | --- |
| [!UICONTROL Activate audiences] | Wählen Sie dieses Steuerelement aus, um zu bearbeiten, welche Zielgruppen dem Ziel zugeordnet sind, Exportpläne zu aktualisieren oder zugeordnete Attribute und Identitäten hinzuzufügen und zu entfernen. Weitere Informationen finden Sie in [&#x200B; Handbüchern unter „Aktivieren von Zielgruppendaten für Zielgruppen](./activate-segment-streaming-destinations.md) &quot;[&#x200B; Aktivieren von Zielgruppendaten für Batch](./activate-batch-profile-destinations.md)Profil-basierte Ziele“ und [Aktivieren von Zielgruppendaten für Streaming-](./activate-streaming-profile-destinations.md) Ziele“. |
| [!UICONTROL Delete] | Löscht diesen Datenfluss und hebt die Zuordnung zuvor aktivierter Zielgruppen auf. |
| [!UICONTROL Destination name] | Dieses Feld kann bearbeitet werden, um den Namen des Ziels zu aktualisieren. |
| [!UICONTROL Description] | Dieses Feld kann bearbeitet werden, um eine optionale Beschreibung des Ziels zu aktualisieren oder hinzuzufügen. |
| [!UICONTROL Destination] | Die Zielplattform, an die Zielgruppen gesendet werden. Weitere Informationen finden [&#x200B; im &#x200B;](../catalog/overview.md)Zielkatalog“. |
| [!UICONTROL Status] | Gibt an, ob das Ziel aktiviert oder deaktiviert ist. |
| [!UICONTROL Marketing actions] | Gibt die Marketing-Aktionen (Anwendungsfälle) an, die für dieses Ziel zu Data-Governance-Zwecken gelten. |
| [!UICONTROL Category] | Gibt den Zieltyp an. Weitere Informationen finden [&#x200B; im &#x200B;](../catalog/overview.md)Zielkatalog“. |
| [!UICONTROL Connection type] | Gibt das Formular an, mit dem Ihre Zielgruppen an das Ziel gesendet werden. Mögliche Werte sind [!UICONTROL Cookie] und [!UICONTROL Profile-based]. |
| [!UICONTROL Frequency] | Gibt an, wie oft die Zielgruppen an das Ziel gesendet werden. Mögliche Werte sind [!UICONTROL Streaming] und [!UICONTROL Batch]. |
| [!UICONTROL Identity] | Stellt den vom Ziel akzeptierten Identity-Namespace dar, z. B. `GAID`, `IDFA` oder `email`. Weitere Informationen zu zulässigen Identity-Namespaces finden Sie unter [Übersicht zu Identity-Namespaces](../../identity-service/features/namespaces.md). |
| [!UICONTROL Created by] | Gibt den Benutzer an, der dieses Ziel erstellt hat. |
| [!UICONTROL Created] | Gibt das UTC-Datum/die UTC-Uhrzeit an, zu der dieses Ziel erstellt wurde. |

{style="table-layout:auto"}

## Umschalter [!UICONTROL Enabled]/[!UICONTROL Disabled] {#enabled-disabled-toggle}

Sie können den Umschalter **[!UICONTROL Enabled]/[!UICONTROL Disabled]** verwenden, um alle Datenexporte an das Ziel zu starten und anzuhalten.

![Datenfluss-Umschalter aktivieren oder deaktivieren](../assets/ui/details-page/enable-disable.png)

## [!UICONTROL Dataflow runs] {#dataflow-runs}

Die Registerkarte [!UICONTROL Dataflow runs] enthält Metrikdaten zu Ihren Datenflussausführungen zu Batch- und Streaming-Zielen. Siehe [Überwachen von &#x200B;](monitor-dataflows.md)&quot; für Details und Metrikdefinitionen.

>[!NOTE]
>
>* Die Zielüberwachungsfunktion wird derzeit für alle Ziele in Experience Platform unterstützt *mit Ausnahme* Ziele [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md), [Benutzerdefinierte &#x200B;](/help/destinations/catalog/personalization/custom-personalization.md) und [Experience Cloud Audiences](/help/destinations/catalog/adobe/experience-cloud-audiences.md).
>* Für die [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md)-, [Azure Event Hubs](/help/destinations/catalog/cloud-storage/azure-event-hubs.md)- und [HTTP API](/help/destinations/catalog/streaming/http-destination.md)-Ziele werden die Metriken in Bezug auf ausgeschlossene, fehlgeschlagene und aktivierte Identitäten geschätzt. Ein höheres Volumen an Aktivierungsdaten führt zu einer höheren Genauigkeit der Metriken.

![Datenflussausführungsansicht](../assets/ui/details-page/dataflow-runs.png)

### Dauer der Datenflussausführungen {#dataflow-runs-duration}

Die angezeigte Dauer der Datenflussausführungen zwischen Streaming- und dateibasierten Zielen unterscheidet sich.

### Streaming-Ziele {#streaming}

Während die für die meisten Streaming-Datenflussausführungen angegebene **[!UICONTROL Processing duration]** etwa vier Stunden beträgt, wie in der Abbildung unten dargestellt, ist die tatsächliche Verarbeitungszeit für jede Datenflussausführung viel kürzer. Datenflussausführungsfenster bleiben länger offen, falls Experience Platform erneut versuchen muss, das Ziel aufzurufen, und stellen Sie außerdem sicher, dass es keine spät ankommenden Daten für dasselbe Zeitfenster verpasst.

![Bild der Seite mit den Datenflussausführungen, wobei die Spalte „Verarbeitungszeit“ für ein Streaming-Ziel hervorgehoben ist.](/help/destinations/assets/ui/details-page/processing-time-dataflow-run-streaming.png)

Weitere Informationen zu „Datenflussausführungen [&#x200B; Streaming-Ziele“ finden &#x200B;](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-streaming-destinations) in der Dokumentation zur Überwachung.

### Dateibasierte Ziele {#file-based}

Bei Datenflussausführungen zu dateibasierten Zielen hängt die **[!UICONTROL Processing duration]** von der Größe der exportierten Daten und der Systemlast ab. Beachten Sie außerdem, dass die Datenflussausführungen zu dateibasierten Zielen nach Zielgruppe aufgeschlüsselt sind.

![Bild der Seite mit den Datenflussausführungen, wobei die Spalte „Verarbeitungszeit“ für ein dateibasiertes Ziel hervorgehoben ist.](../assets/ui/details-page/processing-time-dataflow-run-file-based.png)

Weitere Informationen zu [Datenflussausführungen zu Batch-Zielen (dateibasiert)) finden &#x200B;](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) in der Monitoring-Dokumentation.

## [!UICONTROL Activation data] {#activation-data}

Auf der Registerkarte **[!UICONTROL Activation data]** wird eine Liste der Zielgruppen angezeigt, die dem Ziel zugeordnet wurden, einschließlich des Start- und Enddatums (falls zutreffend) sowie anderer relevanter Informationen für den Datenexport, wie Exporttyp, -zeitplan und -frequenz. Um die Details zu einer bestimmten Zielgruppe anzuzeigen, wählen Sie den Namen aus der Liste aus.

>[!TIP]
>
>Um Details zu den Attributen und Identitäten, die einem Ziel zugeordnet sind, anzuzeigen und zu bearbeiten, wählen Sie **[!UICONTROL Activate audiences]** in der [&#x200B; Leiste &#x200B;](#right-rail).

>[!BEGINSHADEBOX]

Die Registerkarte **[!UICONTROL Activation data]** für ein dateibasiertes Ziel.

![Aktivierungsdatenansicht-Batch-Ziel](../assets/ui/details-page/activation-data-batch.png)

>[!ENDSHADEBOX]


>[!BEGINSHADEBOX]

Die Registerkarte **[!UICONTROL Activation data]** für ein Streaming-Ziel.

![Streaming-Ziel für Datenansicht aktivieren](../assets/ui/details-page/activation-data-streaming.png)

>[!ENDSHADEBOX]

### Filtern von aktivierten Zielgruppen {#filter-audiences}

Um durch die Liste der für ein Ziel aktivierten Zielgruppen zu filtern, geben Sie im Suchfeld einen Zielgruppennamen ein. Die Liste der Zielgruppen wird automatisch mit den Suchergebnissen aktualisiert.

![Suchfeld zum Filtern von Zielgruppen.](../assets/ui/details-page/filter-audiences.png)

### Entfernen mehrerer Zielgruppen aus Aktivierungsflüssen {#bulk-remove}

Um mehrere Zielgruppen aus vorhandenen Aktivierungsflüssen zu entfernen, wählen Sie die Zielgruppen aus und klicken Sie dann auf **[!UICONTROL Remove audiences]**.

![Aktivierungsdaten-Bildschirm mit hervorgehobener Option „Zielgruppen entfernen“](../assets/ui/details-page/bulk-remove-audiences.png)

### Exportieren mehrerer Dateien nach Bedarf an Batch-Ziele {#bulk-export}

Sie können [mehrere Dateien bei Bedarf exportieren](../ui/export-file-now.md) von der **[!UICONTROL Activation data]** Seite aus. Wählen Sie dazu die Zielgruppen aus, für die Sie Dateien bei Bedarf exportieren möchten, und wählen Sie das **[!UICONTROL Export file now]**-Steuerelement aus, um einen einmaligen Trigger zu erstellen, mit dem für jede ausgewählte Zielgruppe eine Datei an Ihr Batch-Ziel gesendet wird.

![Abbildung mit hervorgehobener Schaltfläche „Datei jetzt exportieren“](../assets/ui/details-page/bulk-export-file-now.png)

### Bearbeiten von Aktivierungszeitplänen für mehrere Zielgruppen, die an Batch-Ziele exportiert werden {#bulk-edit-schedule}

Um den vorhandenen Aktivierungsplan für mehrere Zielgruppen gleichzeitig zu bearbeiten, wählen Sie die gewünschten Zielgruppen aus und klicken Sie dann auf **[!UICONTROL Edit schedule]**. Ausführliche Informationen zum Definieren oder Bearbeiten eines Exportzeitplans finden Sie im Abschnitt [Planen &#x200B;](../ui/activate-batch-profile-destinations.md#scheduling) Zielgruppenexports.

![Aktivierungsdatenbildschirm mit hervorgehobener Option zum Bearbeiten von Aktivierungszeitplänen für mehrere Zielgruppen.](../assets/ui/details-page/bulk-edit-schedule.png)

>[!NOTE]
>
>Weitere Informationen zur Seite mit Zielgruppendetails finden Sie unter [Zielgruppenportal - Übersicht](../../segmentation/ui/audience-portal.md#audience-details).

### Bearbeiten von Dateinamen für mehrere Zielgruppen, die an Batch-Ziele exportiert wurden {#bulk-edit-file-names}

Um die Namen mehrerer exportierter Zielgruppen gleichzeitig zu bearbeiten, wählen Sie die gewünschten Zielgruppen aus und klicken Sie dann auf **[!UICONTROL Edit file name]**. Detaillierte Informationen zum Definieren oder Bearbeiten eines Dateinamens finden Sie im Abschnitt [Konfigurieren von Dateinamen](../ui/activate-batch-profile-destinations.md#configure-file-names) .

![Aktivierungsdaten-Bildschirm mit hervorgehobener Option zur Bearbeitung von Dateinamen für mehrere Zielgruppen.](../assets/ui/details-page/bulk-edit-file-name.png)