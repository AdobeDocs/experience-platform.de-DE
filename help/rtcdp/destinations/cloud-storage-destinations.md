---
keywords: cloud storage destination;cloud storage
title: Cloud-Speicher-Ziele
seo-title: Cloud-Speicher-Ziele
description: Adobe Echtzeit-CDP kann Ihre Segmente als Datendateien an Ihre Standorte Amazon S3, AWS Kinesis, AWS Ereignis Hubs oder SFTP-Cloud-Datenspeicherung liefern.
seo-description: Adobe Echtzeit-CDP kann Ihre Segmente als Datendateien an Ihre Standorte Amazon S3, AWS Kinesis, AWS Ereignis Hubs oder SFTP-Cloud-Datenspeicherung liefern.
translation-type: tm+mt
source-git-commit: 15323134f0c626cad2c4e90b3e1c0662cf7e57dd
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 35%

---


# Cloud-Speicher-Ziele {#cloud-storage-destinations}

Adobe Echtzeit-CDP kann Ihre Segmente als Datendateien an Ihre Cloud-Datenspeicherung-Speicherorte liefern. This enables you to send audiences and their profile attributes to your internal systems, via CSV or tab-delimited files for [!DNL Amazon S3] and SFTP. Für [!DNL AWS Kinesis] und [!DNL Azure Event Hubs] Ziele werden Daten im JSON-Format aus der Experience Platform gestreamt.

![Adobe-Cloud-Speicher-Ziele](/help/rtcdp/destinations/assets/cloud-storage-destinations.png)

Informationen zum Herstellen einer Verbindung zu Cloud-Speicher-Zielen finden Sie unter [Workflow zum Erstellen von Cloud-Speicher-Zielen](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md).

## Datenexporttyp

**Profil-basierter Export** – Sie exportieren Details zu den Einzelpersonen in der Zielgruppe. Diese Details sind für die Personalisierung erforderlich und können Attribute, Ereignisse, Segmentabos usw. umfassen.

## Verfügbare Cloud-Datenspeicherung-Ziele

* [Amazon S3-Ziel](/help/rtcdp/destinations/amazon-s3-destination.md)
* [SFTP-Ziel](/help/rtcdp/destinations/sftp-destination.md)

## Verfügbare Streaming-Ziele für Cloud-Datenspeicherung

* [Amazon Kinesis-Ziel](/help/rtcdp/destinations/amazon-kinesis-destination.md)
* [Azurblauer Ereignis Hubs Ziel](/help/rtcdp/destinations/azure-event-hubs-destination.md)