---
keywords: cloud storage destination;cloud storage
title: Cloud-Speicher-Ziele
seo-title: Cloud-Speicher-Ziele
description: Mit CDP in Echtzeit können Sie Ihre Segmente als Datendateien an Ihre Amazon S3-, AWS Kinesis-, AWS Ereignis-Hubs- oder SFTP-Cloud-Datenspeicherung-Speicherorte senden.
seo-description: Mit CDP in Echtzeit können Sie Ihre Segmente als Datendateien an Ihre Amazon S3-, AWS Kinesis-, AWS Ereignis-Hubs- oder SFTP-Cloud-Datenspeicherung-Speicherorte senden.
translation-type: tm+mt
source-git-commit: 0bb1622895b1e0f97fc47b5c61d456bc369746c8
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 36%

---


# Cloud-Speicher-Ziele {#cloud-storage-destinations}

Echtzeit-CDP kann Ihre Segmente als Datendateien an Ihre Cloud-Datenspeicherung-Speicherorte liefern. This enables you to send audiences and their profile attributes to your internal systems, via CSV or tab-delimited files for [!DNL Amazon S3] and SFTP. Für [!DNL AWS Kinesis] und [!DNL Azure Event Hubs] Ziele werden Daten im JSON-Format aus der Experience Platform gestreamt.

![Adobe-Cloud-Speicher-Ziele](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

Informationen zum Herstellen einer Verbindung zu Cloud-Speicher-Zielen finden Sie unter [Workflow zum Erstellen von Cloud-Speicher-Zielen](./workflow.md).

## Datenexporttyp

**Profil-basierter Export** – Sie exportieren Details zu den Einzelpersonen in der Zielgruppe. Diese Details sind für die Personalisierung erforderlich und können Attribute, Ereignisse, Segmentabos usw. umfassen.

## Verfügbare Cloud-Datenspeicherung-Ziele

- [Amazon S3-Ziel](./amazon-s3.md)
- [SFTP-Ziel](./sftp.md)

## Verfügbare Streaming-Ziele für Cloud-Datenspeicherung

- [Amazon Kinesis-Ziel](./amazon-kinesis.md)
- [Azurblauer Ereignis Hubs Ziel](./azure-event-hubs.md)