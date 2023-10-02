---
keywords: Cloud-Speicherziel;Cloud-Speicher
title: Übersicht über die Cloud-Speicher-Ziele
description: Adobe Experience Platform kann Ihre Zielgruppen als Datendateien an Ihre Amazon S3-, AWS Kinesis-, Azure Event Hubs- oder SFTP-Cloud-Speicherorte senden.
exl-id: d29f0a6e-b323-4f78-bbd0-dee2f1e0fedb
source-git-commit: 8b8abea65ee0448594113ca77f75b84293646146
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 49%

---

# Übersicht über die Cloud-Speicher-Ziele {#cloud-storage-destinations}

## Übersicht {#overview}

Adobe Experience Platform kann Ihre Zielgruppen als Datendateien an Ihre Cloud-Speicherorte übermitteln. Auf diese Weise können Sie Zielgruppen und deren Profilattribute über CSV-Dateien für [!DNL Amazon S3], [!DNL Azure Blob], [!DNL Azure Data Lake Storage Gen2], [!DNL Data Landing Zone], [!DNL Google Cloud Storage] und SFTP an Ihre internen Systeme senden. Für [!DNL Amazon Kinesis]- und [!DNL Azure Event Hubs]-Ziele werden Daten aus Experience Platform im [!DNL JSON]-Format gestreamt.

![Adobe-Cloud-Speicherzele](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

## Unterstützte Cloud-Speicherziele {#supported-destinations}

Adobe Experience Platform unterstützt Datenexporte in die folgenden Cloud-Speicher-Ziele:

* [Amazon Kinesis-Verbindung](amazon-kinesis.md)
* [Amazon S3-Verbindung](amazon-s3.md)
* [Azure Blob-Verbindung](azure-blob.md)
* [Azure Data Lake Storage Gen2](adls-gen2.md)
* [Azure Event Hubs-Verbindung](azure-event-hubs.md)
* [Data Landing Zone](data-landing-zone.md)
* [Google Cloud Storage](google-cloud-storage.md)
* [SFTP-Verbindung](sftp.md)

## Verbinden mit einem neuen Cloud-Speicherziel {#connect-destination}

Um Zielgruppen an Cloud-Speicher-Ziele für Ihre Kampagnen zu senden, muss Platform zunächst eine Verbindung zum Ziel herstellen. Siehe das [Tutorial zur Zielerstellung](../../ui/connect-destination.md) für detaillierte Informationen zur Einrichtung eines neuen Ziels.


## Verwenden von Makros zum Erstellen eines Ordners an Ihrem Speicherort {#use-macros}

>[!NOTE]
>
> Die in diesem Abschnitt beschriebene Funktion ist derzeit nur für [Amazon S3](amazon-s3.md)-Ziele verfügbar.

Um einen benutzerdefinierten Ordner pro Zielgruppendatei in Ihrem Speicherort zu erstellen, können Sie Makros im Eingabefeld Ordnerpfad verwenden. Fügen Sie die Makros am Ende des Eingabefelds ein, wie unten dargestellt.

![Verwenden von Makros zum Erstellen eines Ordners in Ihrem Speicher](../../assets/catalog/cloud-storage/workflow/macros-folder-path.png)

Die folgenden Beispiele verweisen auf eine Beispielzielgruppe `Luxury Audience` mit ID `25768be6-ebd5-45cc-8913-12fb3f348615`.

**Makro 1:`%SEGMENT_NAME%`**

Eingabe: `acme/campaigns/2021/%SEGMENT_NAME%`
Ordnerpfad an Ihrem Speicherort: `acme/campaigns/2021/Luxury Audience`

**Makro 2:`%SEGMENT_ID%`**

Eingabe: `acme/campaigns/2021/%SEGMENT_ID%`
Ordnerpfad an Ihrem Speicherort: `acme/campaigns/2021/25768be6-ebd5-45cc-8913-12fb3f348615`

**Makro 3:`%SEGMENT_NAME%/%SEGMENT_ID%`**

Eingabe: `acme/campaigns/2021/%SEGMENT_NAME%/%SEGMENT_ID%`
Ordnerpfad an Ihrem Speicherort: `acme/campaigns/2021/Luxury Audience/25768be6-ebd5-45cc-8913-12fb3f348615`

## Datenexporttyp {#export-type}

Cloud-Speicher-Ziele unterstützen die folgenden Exporttypen:
* **Profilbasierter Export**. Das bedeutet, dass Sie Details zu den Einzelpersonen in der Zielgruppe exportieren. Diese Details sind für die Personalisierung erforderlich und können Attribute, Ereignisse, Zielgruppenmitgliedschaften und mehr umfassen.
* **Datensatzexport**. Mit dieser Funktion können Sie ganze Datensätze in Cloud-Speicher-Ziele exportieren. [Mehr dazu](/help/destinations/ui/export-datasets.md) über die Funktionalität.

## Nächste Schritte {#next-steps}

Nach Auswahl der [unterstützte Cloud-Ziele](#supported-destinations) lesen Sie die [Tutorial zum Verbinden mit Zielen](/help/destinations/ui/connect-destination.md) , um zu erfahren, wie eine Verbindung zum Ziel hergestellt wird. Lesen Sie dann das Aktivierungs-Tutorial zu dateibasierten Zielen , um zu erfahren, wie Sie beginnen [exportieren](/help/destinations/ui/activate-batch-profile-destinations.md) Daten zu Ihrem Cloud-Speicher-Ziel.
