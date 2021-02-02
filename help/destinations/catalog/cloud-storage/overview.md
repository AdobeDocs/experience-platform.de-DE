---
keywords: Ziel der Cloud-Datenspeicherung;Cloud-Datenspeicherung
title: Cloud-Speicher-Ziele
seo-title: Cloud-Speicher-Ziele
description: Die Plattform kann Ihre Segmente als Datendateien an Ihre Amazon S3-, AWS Kinesis-, Azurblauen Ereignis-Hubs- oder SFTP-Cloud-Datenspeicherung liefern.
seo-description: Die Plattform kann Ihre Segmente als Datendateien an Ihre Amazon S3-, AWS Kinesis-, Azurblauen Ereignis-Hubs- oder SFTP-Cloud-Datenspeicherung liefern.
translation-type: tm+mt
source-git-commit: b348a5493b13112291dd8e9234d457ff8c694147
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 32%

---


# Cloud-Speicher-Ziele {#cloud-storage-destinations}

Adobe Experience Platform kann Ihre Segmente als Datendateien an Ihre Cloud-Datenspeicherung-Speicherorte liefern. Auf diese Weise können Sie Audiencen und deren Profil-Attribute über CSV- oder tabulatorgetrennte Dateien für [!DNL Amazon S3] und SFTP an Ihre internen Systeme senden. Bei [!DNL AWS Kinesis]- und [!DNL Azure Event Hubs]-Zielen werden die Daten aus der Experience Platform im JSON-Format gestreamt.

![Ziele der Adobe Cloud-Datenspeicherung](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

Informationen zum Herstellen einer Verbindung zu Cloud-Speicher-Zielen finden Sie unter [Workflow zum Erstellen von Cloud-Speicher-Zielen](./workflow.md).

## Datenexporttyp

**Profil-basierter Export** – Sie exportieren Details zu den Einzelpersonen in der Zielgruppe. Diese Details sind für die Personalisierung erforderlich und können Attribute, Ereignisse, Segmentabos usw. umfassen.

## Verfügbare Cloud-Datenspeicherung-Ziele

- [Amazon S3-Ziel](./amazon-s3.md)
- [Blumenziel](./azure-blob.md)
- [SFTP-Ziel](./sftp.md)

## Verfügbare Streaming-Ziele für Cloud-Datenspeicherung

- [Amazon Kinesis-Ziel](./amazon-kinesis.md)
- [Azurblauer Ereignis Hubs Ziel](./azure-event-hubs.md)