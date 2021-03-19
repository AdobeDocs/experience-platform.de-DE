---
keywords: Ziel der Cloud-Datenspeicherung;Cloud-Datenspeicherung
title: Übersicht über die Ziele der Cloud-Datenspeicherung
description: Adobe Experience Platform kann Ihre Segmente als Datendateien an Ihre Standorte Amazon S3, AWS Kinesis, AWS Ereignis Hubs oder SFTP-Cloud-Datenspeicherung liefern.
translation-type: tm+mt
source-git-commit: 4f636de9f0cac647793564ce37c6589d096b61f7
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 22%

---


# Übersicht über die Cloud-Speicher-Ziele {#cloud-storage-destinations}

Adobe Experience Platform kann Ihre Segmente als Datendateien an Ihre Cloud-Datenspeicherung-Speicherorte liefern. Auf diese Weise können Sie Audiencen und deren Profil-Attribute über CSV- oder tabulatorgetrennte Dateien für [!DNL Amazon S3], [!DNL Azure Blob] und SFTP an Ihre internen Systeme senden. Bei [!DNL Amazon Kinesis]- und [!DNL Azure Event Hubs]-Zielen werden die Daten aus der Experience Platform im JSON-Format gestreamt.

![Ziele der Adobe Cloud-Datenspeicherung](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

Informationen zum Herstellen einer Verbindung zu Cloud-Speicher-Zielen finden Sie unter [Workflow zum Erstellen von Cloud-Speicher-Zielen](./workflow.md).

## Datenexporttyp

**Profil-basierter Export** – Sie exportieren Details zu den Einzelpersonen in der Zielgruppe. Diese Details sind für die Personalisierung erforderlich und können Attribute, Ereignis, Segmentmitgliedschaften und mehr umfassen.

## Verfügbare Cloud-Datenspeicherung-Ziele

- [Amazon S3-Verbindung](./amazon-s3.md)
- [Azurblauch-Verbindung](./azure-blob.md)
- [SFTP-Verbindung](./sftp.md)

## Verfügbare Streaming-Ziele für Cloud-Datenspeicherung

- [Amazon Kinesis-Anschluss](./amazon-kinesis.md)
- [Azurblauer Ereignis Hubs](./azure-event-hubs.md)