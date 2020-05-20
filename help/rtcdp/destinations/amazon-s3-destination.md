---
title: Amazon S3-Ziel
seo-title: Amazon S3-Ziel
description: Erstellen Sie eine aktive ausgehende Verbindung zu Ihrem Amazon Web Services (AWS) S3-Speicher, um in regelmäßigen Abständen tabulatorgetrennte oder CSV-Datendateien aus Adobe Experience Platform in Ihre eigenen S3-Buckets zu exportieren.
seo-description: Erstellen Sie eine aktive ausgehende Verbindung zu Ihrem Amazon Web Services (AWS) S3-Speicher, um in regelmäßigen Abständen tabulatorgetrennte oder CSV-Datendateien aus Adobe Experience Platform in Ihre eigenen S3-Buckets zu exportieren.
translation-type: tm+mt
source-git-commit: f3c6c27b7ad07ada0df18aabe0e8503253b38342
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 82%

---


# Amazon S3-Ziel

## Übersicht

Erstellen Sie eine aktive ausgehende Verbindung zu Ihrem Amazon Web Services (AWS) S3-Speicher, um in regelmäßigen Abständen tabulatorgetrennte oder CSV-Datendateien aus Adobe Experience Platform in Ihre eigenen S3-Buckets zu exportieren.

## Ziel verbinden {#connect-destination}

Anweisungen zum Herstellen einer Verbindung mit Ihren Cloud-Speicher-Zielen, einschließlich Amazon S3, finden Sie unter [Workflow für Cloud-Speicher-Ziele](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md).

Geben Sie für Amazon S3-Ziele im Workflow zum Erstellen des Ziels die folgenden Informationen ein:

* **Amazon S3-Zugriffsschlüssel und Amazon S3-geheimer Schlüssel**: Generieren Sie in Amazon S3 einen Zugriffsschlüssel - das Schlüsselpaar für den geheimen Zugriff, um Adobe Echtzeit-CDP Zugriff auf Ihr Amazon S3-Konto zu gewähren.



>[!IMPORTANT]
>
>Die Adobe-Echtzeit-CDP benötigt `write`-Berechtigungen für das Bucket-Objekt, für das die Exportdateien bereitgestellt werden.
