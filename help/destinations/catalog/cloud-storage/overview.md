---
keywords: Cloud-Speicherziel;Cloud-Speicher
title: Übersicht über die Cloud-Speicher-Ziele
description: Adobe Experience Platform kann Ihre Zielgruppen als Datendateien an Ihre Amazon S3-, AWS Kinesis-, Azure Event Hubs- oder SFTP-Cloud-Speicherorte senden.
exl-id: d29f0a6e-b323-4f78-bbd0-dee2f1e0fedb
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 38%

---

# Übersicht über die Cloud-Speicher-Ziele {#cloud-storage-destinations}

## Übersicht {#overview}

Adobe Experience Platform kann Ihre Zielgruppen als Datendateien an Ihre Cloud-Speicherorte senden. Auf diese Weise können Sie Zielgruppen und deren Profilattribute über CSV-Dateien für [!DNL Amazon S3], [!DNL Azure Blob], [!DNL Azure Data Lake Storage Gen2], [!DNL Data Landing Zone], [!DNL Google Cloud Storage] und SFTP an Ihre internen Systeme senden. Für [!DNL Amazon Kinesis]- und [!DNL Azure Event Hubs]-Ziele werden Daten aus Experience Platform im [!DNL JSON]-Format gestreamt.

![Adobe-Cloud-Speicherzele](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

## Unterstützte Cloud-Speicherziele {#supported-destinations}

Adobe Experience Platform unterstützt Datenexporte an die folgenden Cloud-Speicher-Ziele:

* [Amazon Kinesis-Verbindung](amazon-kinesis.md)
* [Amazon S3-Verbindung](amazon-s3.md)
* [Azure Blob-Verbindung](azure-blob.md)
* [Azure Data Lake Storage Gen2](adls-gen2.md)
* [Azure Event Hubs-Verbindung](azure-event-hubs.md)
* [Data Landing Zone](data-landing-zone.md)
* [Google Cloud Storage](google-cloud-storage.md)
* [SFTP-Verbindung](sftp.md)

## Verbinden mit einem neuen Cloud-Speicherziel {#connect-destination}

Um Zielgruppen an Cloud-Speicher-Ziele für Ihre Kampagnen zu senden, muss Experience Platform zunächst eine Verbindung mit dem Ziel herstellen. Siehe das [Tutorial zur Zielerstellung](../../ui/connect-destination.md) für detaillierte Informationen zur Einrichtung eines neuen Ziels.


## Verwenden von Makros zum Erstellen eines Ordners an Ihrem Speicherort {#use-macros}

>[!NOTE]
>
> Die in diesem Abschnitt beschriebene Funktion ist für alle Cloud-Speicher-Ziele verfügbar. Das Ziel [Amazon S3](amazon-s3.md) unterstützt jedoch derzeit nur die `%SEGMENT_ID%`- und `%SEGMENT_NAME%`.

Um einen benutzerdefinierten Ordner pro Zielgruppendatei an Ihrem Speicherort zu erstellen, können Sie Makros im Eingabefeld Ordnerpfad verwenden. Fügen Sie die Makros am Ende des Eingabefelds ein, wie unten dargestellt.

![Verwenden von Makros zum Erstellen eines Ordners in Ihrem Speicher](../../assets/catalog/cloud-storage/workflow/macros-folder-path.png)

Die folgenden Beispiele verweisen auf eine Beispiel-Zielgruppe `Luxury Audience` mit der ID `25768be6-ebd5-45cc-8913-12fb3f348615`.

**Makro 1:`%SEGMENT_NAME%`**

Eingabe: `acme/campaigns/2021/%SEGMENT_NAME%`
Ordnerpfad an Ihrem Speicherort: `acme/campaigns/2021/Luxury Audience`

**Makro 2:`%SEGMENT_ID%`**

Eingabe: `acme/campaigns/2021/%SEGMENT_ID%`
Ordnerpfad an Ihrem Speicherort: `acme/campaigns/2021/25768be6-ebd5-45cc-8913-12fb3f348615`

**Makro 3:`%SEGMENT_NAME%/%SEGMENT_ID%`**

Eingabe: `acme/campaigns/2021/%SEGMENT_NAME%/%SEGMENT_ID%`
Ordnerpfad an Ihrem Speicherort: `acme/campaigns/2021/Luxury Audience/25768be6-ebd5-45cc-8913-12fb3f348615`

**Weitere Makros**

Ähnlich wie in den obigen Beispielen können Sie weitere Makros verwenden, um eine benutzerdefinierte Ordnerstruktur an Ihrem Ordnerspeicherort zu erstellen:

* `%DATETIME%` oder `%TIMESTAMP%` Sie einen benutzerdefinierten Ordnernamen basierend auf der Exportzeit der Dateien hinzufügen. Das Format für das erste Makro ist `MMDDYYYY_HHMMSS` und das UNIX-10-stellige Format für das zweite Makro.
* `%DESTINATION_NAME%`, einen benutzerdefinierten Ordner auf Grundlage des Namens des Ziel-Datenflusses hinzuzufügen.

## Datenexporttyp {#export-type}

Cloud-Speicher-Ziele unterstützen die folgenden Exporttypen:

* **Profil-basierter Export**. Das bedeutet, dass Sie Details zu den Einzelpersonen in der Zielgruppe exportieren. Diese Details sind für die Personalisierung erforderlich und können Attribute, Ereignisse, Zielgruppenmitgliedschaften und mehr umfassen.
* **Datensatzexport**. Mit dieser Funktion können Sie ganze Datensätze in Cloud-Speicher-Ziele exportieren. [Weitere Informationen](/help/destinations/ui/export-datasets.md) über die Funktion.

## Nächste Schritte {#next-steps}

Nachdem Sie ausgewählt haben, welches der [unterstützten Cloud-Ziele](#supported-destinations) Sie verwenden möchten, lesen Sie das [Tutorial zum Herstellen einer Verbindung mit Zielen](/help/destinations/ui/connect-destination.md) um zu erfahren, wie Sie eine Verbindung zum Ziel herstellen. Lesen Sie dann das Aktivierungs-Tutorial für dateibasierte Ziele, um zu erfahren, wie Sie mit dem [ (Exportieren](/help/destinations/ui/activate-batch-profile-destinations.md) von Daten in Ihr Cloud-Speicherziel beginnen.
