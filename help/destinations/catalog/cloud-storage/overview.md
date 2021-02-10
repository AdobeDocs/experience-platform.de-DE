---
keywords: Ziel der Cloud-Datenspeicherung;Cloud-Datenspeicherung
title: Übersicht über die Ziele der Cloud-Datenspeicherung
description: Adobe Experience Platform kann Ihre Segmente als Datendateien an Ihre Standorte Amazon S3, AWS Kinesis, AWS Ereignis Hubs oder SFTP-Cloud-Datenspeicherung liefern.
translation-type: tm+mt
source-git-commit: 48c5f6d6a45de5f7982543f7a43cb4ece8cf3a9f
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 31%

---


# Übersicht über die Cloud-Speicher-Ziele {#cloud-storage-destinations}

Adobe Experience Platform kann Ihre Segmente als Datendateien an Ihre Cloud-Datenspeicherung-Speicherorte liefern. Auf diese Weise können Sie Audiencen und deren Profil-Attribute über CSV- oder tabulatorgetrennte Dateien für [!DNL Amazon S3] und SFTP an Ihre internen Systeme senden. Bei [!DNL AWS Kinesis]- und [!DNL Azure Event Hubs]-Zielen werden die Daten aus der Experience Platform im JSON-Format gestreamt.

![Ziele der Adobe Cloud-Datenspeicherung](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

Informationen zum Herstellen einer Verbindung zu Cloud-Speicher-Zielen finden Sie unter [Workflow zum Erstellen von Cloud-Speicher-Zielen](./workflow.md).

## Datenexporttyp

**Profil-basierter Export** – Sie exportieren Details zu den Einzelpersonen in der Zielgruppe. Diese Details sind für die Personalisierung erforderlich und können Attribute, Ereignisse, Segmentabos usw. umfassen.

## Verfügbare Cloud-Datenspeicherung-Ziele

- [Amazon S3-Verbindung](./amazon-s3.md)
- [Azurblauch-Verbindung](./azure-blob.md)
- [SFTP-Verbindung](./sftp.md)

## Verfügbare Streaming-Ziele für Cloud-Datenspeicherung

- [Amazon Kinesis-Anschluss](./amazon-kinesis.md)
- [Azurblauer Ereignis Hubs](./azure-event-hubs.md)