---
keywords: Amazon S3;S3 destination;s3;amazon s3
title: Amazon S3-Ziel
seo-title: Amazon S3-Ziel
description: Erstellen Sie eine aktive ausgehende Verbindung zu Ihrem Amazon Web Services (AWS) S3-Speicher, um in regelmäßigen Abständen tabulatorgetrennte oder CSV-Datendateien aus Adobe Experience Platform in Ihre eigenen S3-Buckets zu exportieren.
seo-description: Erstellen Sie eine aktive ausgehende Verbindung zu Ihrem Amazon Web Services (AWS) S3-Speicher, um in regelmäßigen Abständen tabulatorgetrennte oder CSV-Datendateien aus Adobe Experience Platform in Ihre eigenen S3-Buckets zu exportieren.
translation-type: tm+mt
source-git-commit: 4c45da353b1deeb66b0dedb37450158f4bdc2a7c
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 39%

---


# [!DNL Amazon S3] Ziel

## Übersicht

Create a live outbound connection to your [!DNL Amazon Web Services] (AWS) S3 storage to periodically export tab-delimited or CSV data files from Adobe Experience Platform into your own S3 buckets.

## Ziel verbinden {#connect-destination}

See [Cloud storage destinations workflow ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)for instructions on how to connect to your cloud storage destinations, including [!DNL Amazon S3].

For [!DNL Amazon S3] destinations, enter the following information in the create destination workflow:

* **[!DNL Amazon S3]Zugriffsschlüssel und[!DNL Amazon S3]geheimer Schlüssel**: Erstellen Sie [!DNL Amazon S3]ein `access key - secret access key` Paar, um der Adobe Echtzeit-CDP-Zugriff auf Ihr [!DNL Amazon S3] Konto zu gewähren. Weitere Informationen finden Sie in der Dokumentation zu [Amazon Web Services](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

>[!IMPORTANT]
>
>Die Adobe-Echtzeit-CDP benötigt `write`-Berechtigungen für das Bucket-Objekt, für das die Exportdateien bereitgestellt werden.

## Exportierte Daten {#exported-data}

For [!DNL Amazon S3] destinations, Adobe Real-time CDP creates a tab-delimited `.txt` or `.csv` file in the storage location that you provided. Weitere Informationen zu den Dateien finden Sie unter [E-Mail-Marketing-Ziele und Cloud-Datenspeicherung-Ziele](/help/rtcdp/destinations/activate-destinations.md#esp-and-cloud-storage) im Tutorial zur Aktivierung von Segmenten.

<!--

Expect a new file to be created in your storage location every day. The file format is:

`amazon-s3_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

```
amazon-s3_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
amazon-s3_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
amazon-s3_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

The presence of these files in your storage location is confirmation of successful activation. To understand how the exported files are structured, you can [download a sample .csv file](/help/rtcdp/destinations/assets/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). This sample file includes the profile attributes `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`, and `personalEmail.address`.

-->
