---
title: Erweitern der Zeitpläne für den Datensatzexport für Datenflüsse, die vor November 2024 erstellt wurden
description: Erfahren Sie, wie Sie den Exportzeitplan für Datensatzexport-Datenflüsse verlängern, die vor November 2024 erstellt wurden und am 1. September 2025 nicht mehr funktionieren.
type: Tutorial
exl-id: a756886b-3f4b-4427-bd26-817221ba68aa
source-git-commit: 0da592dd2846ed0f1eeb31102842c8895cac6952
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 0%

---

# Erweitern der Zeitpläne für den Datensatzexport für Datenflüsse, die vor November 2024 erstellt wurden

>[!IMPORTANT]
>
>**Aktion erforderlich**: Wenn Ihre Organisation vor November 2024 [Datenflüsse für den Datensatzexport](export-datasets.md) erstellt hat, funktionieren diese Datenflüsse ab dem 1. September 2025 nicht mehr. In diesem Handbuch wird erläutert, wie Sie den Exportplan für die Datenflüsse, die Sie beibehalten möchten, über dieses Datum hinaus verlängern können.

## Überblick {#overview}

In der Version [September 2024 von Experience Platform](/help/release-notes/2024/september-2024.md#destinations) führte Adobe das standardmäßige Enddatum **1. Mai 2025)** alle Datensatzexport-Datenflüsse ein, die vor der Version September 2024 erstellt wurden.

**Dieses Datum wurde seitdem für alle Datensatzexport-Datenflüsse, die vor**. November 2024 erstellt wurden, **1. September 2025**.

Datenflüsse für den Datensatzexport, die vor November 2024 erstellt wurden, werden den Datenexport am 1. **2025**, es sei denn, das Ablaufdatum wird manuell verlängert.

Wenn Sie die Datenflüsse benötigen, um nach dem 1. **2025 weiterhin Daten** exportieren, müssen Sie ihre Zeitpläne für jedes Ziel erweitern, an das Sie Datensätze exportieren, indem Sie die Schritte in diesem Handbuch befolgen.

## Betroffene Ziele {#affected-destinations}

Ihr Unternehmen verfügt möglicherweise über aktive Datensatz-Export-Datenflüsse, die Daten an die unten aufgeführten Ziele senden. Führen Sie die Schritte in den nächsten Abschnitten aus und sehen Sie sich das Video mit den exemplarischen Vorgehensweisen an, um zu erfahren, welche Datensätze ablaufen.

* [[!DNL Azure Data Lake Storage Gen2]](../catalog/cloud-storage/adls-gen2.md)
* [[!DNL Data Landing Zone]](../catalog/cloud-storage/data-landing-zone.md)
* [[!DNL Google Cloud Storage]](../catalog/cloud-storage/google-cloud-storage.md)
* [[!DNL Amazon S3]](../catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL Azure Blob]](../catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL SFTP]](../catalog/cloud-storage/sftp.md#changelog)
* [[!DNL Marketo Measure Ultimate]](../catalog/adobe/marketo-measure-ultimate.md)

## Video-Tutorial {#video}

Sehen Sie sich das folgende Video an, um eine schrittweise Veranschaulichung dazu zu erhalten, wie Sie Datensatzexporte mit bevorstehenden Enddaten identifizieren und den Exportzeitplan für die Datenflüsse erweitern, die Sie beibehalten möchten.

>[!VIDEO](https://video.tv.adobe.com/v/3470518/)

## Schritt 1: Identifizieren Sie die betroffenen Datenflüsse {#identify-dataflows}

Bevor Sie den Exportzeitplan für Ihre Datensatzexport-Datenflüsse verlängern, müssen Sie zunächst feststellen, welche Datenflüsse vom bevorstehenden Ablaufdatum betroffen sind. Gehen Sie wie folgt vor, um Datenflüsse zu finden, die eine Aktion erfordern.

1. Navigieren Sie **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]** in der Experience Platform-Benutzeroberfläche.
2. Wählen Sie **[!UICONTROL Aktivieren]** für ein Ziel aus, das aktive Datensatzexport-Datenflüsse hat.

   >[!TIP]
   >
   >Verwenden Sie den **[!UICONTROL Datentypen]** Filter auf der linken Seite des Katalogs, um verfügbare Ziele nach **[!UICONTROL Datensätzen]** zu filtern.

3. Wählen Sie **[!UICONTROL Datentyp]**Datensätze“ aus, um nur die Datenflüsse mit Datensatzexporten anzuzeigen.
   ![Screenshot, der zeigt, wie Datenflüsse nach Datentyp gefiltert werden.](/help/destinations/assets/ui/export-datasets/dataset-type.png)
4. Wählen Sie die Spaltenüberschrift **[!UICONTROL Erstellt]** und dann **[!UICONTROL Aufsteigend sortieren]**, um ältere Datenflüsse anzuzeigen.
   ![Screenshot, der zeigt, wie Datenflüsse in aufsteigender Reihenfolge sortiert werden.](/help/destinations/assets/ui/export-datasets/sort-ascending.png)
5. Ermitteln Sie, welchen der vor November 2024 erstellten Datenflüsse Sie beibehalten möchten.

## Schritt 2: Zugriff auf den Workflow zum Exportieren von Datensätzen {#access-workflow}

Für jeden Datenfluss, den Sie beibehalten möchten, müssen Sie auf den Workflow zum Exportieren von Datensätzen zugreifen, um den Zeitplan zu ändern.

1. Wählen Sie den Datenflussnamen in der Spalte **[!UICONTROL Name]** aus. Dadurch gelangen Sie zur Seite **[!UICONTROL Datenflussausführungen]**.
2. Wählen Sie auf dieser Seite die Option **[!UICONTROL Datensätze exportieren]** aus.
   ![Screenshot mit der Option „Datensätze exportieren“ auf der Seite mit den Datenflussausführungen.](/help/destinations/assets/ui/export-datasets/export-datasets-option.png)
3. Klicken Sie auf der **[!UICONTROL Datensätze auswählen]** auf **[!UICONTROL Weiter]**. Sie müssen keine neuen Datensätze zum Datenfluss hinzufügen.
4. Dadurch gelangen Sie zur Seite **[!UICONTROL Planung]** auf der Sie auch eine Benachrichtigung sehen, die Sie über das Ablaufdatum des Datensatzexports informiert.
   ![Datenflüsse für den Datensatzexport mit Ablaufbenachrichtigung](/help/destinations/assets/ui/export-datasets/dataset-export-notification.png)

## Schritt 3: Exportzeitplan verlängern {#extend-export-schedule}

Jetzt können Sie den Exportzeitplan ändern, um ihn über den 1. September 2025 hinaus zu verlängern.

1. Wählen Sie **[!UICONTROL Zeitplan bearbeiten]** aus.
   ![Screenshot des Planungsschritts mit der Schaltfläche „Zeitplan bearbeiten“.](/help/destinations/assets/ui/export-datasets/edit-schedule.png)
2. Wählen Sie einen neuen Exportzeitplan und dann **[!UICONTROL Speichern]**.
   ![Screenshot des Planungsschritts mit den Planungsoptionen.](/help/destinations/assets/ui/export-datasets/edit-schedule-calendar.png)

   >[!TIP]
   >
   >Lesen Sie die [Dokumentation zum Datensatzexport](export-datasets.md#scheduling), um detaillierte Anleitungen zum Konfigurieren von Zeitplänen für den Datensatzexport zu erhalten.

## Was passiert, wenn ich die Frist vom 1. September 2025 verpasse? {#missed-deadline}

Wenn Ihre Datenflüsse für den Datensatzexport am 1. September 2025 abgelaufen sind und Sie sie dennoch verlängern möchten, führen Sie die Schritte in den obigen Abschnitten aus, um ihren Zeitplan zu verlängern.

Wenn Sie den Exportzeitplan innerhalb von 30 Tagen erweitern (oder weniger, wenn der [Time-to-Live-Satz im exportierten Datensatz](/help/catalog/datasets/experience-event-dataset-retention-ttl-guide.md) weniger als 30 Tage beträgt), können Sie trotzdem eine Aufstockung der Daten erhalten, die zwischen dem 1. September und dem Datum, an dem Sie den Export erneut aktivieren, nicht exportiert wurden. Bei der Festlegung einer neuen Endzeit *zuerst* vollständiger Dateiexport erfolgen. Stattdessen werden die Exporte schrittweise von dort aus fortgesetzt, wo sie am 1. September aufgehört haben.