---
keywords: Amazon S3;S3 destination;s3;amazon s3
title: Amazon S3-Ziel
seo-title: Amazon S3-Ziel
description: Erstellen Sie eine aktive ausgehende Verbindung zu Ihrem Amazon Web Services (AWS) S3-Speicher, um in regelmäßigen Abständen tabulatorgetrennte oder CSV-Datendateien aus Adobe Experience Platform in Ihre eigenen S3-Buckets zu exportieren.
seo-description: Erstellen Sie eine aktive ausgehende Verbindung zu Ihrem Amazon Web Services (AWS) S3-Speicher, um in regelmäßigen Abständen tabulatorgetrennte oder CSV-Datendateien aus Adobe Experience Platform in Ihre eigenen S3-Buckets zu exportieren.
translation-type: tm+mt
source-git-commit: f2fdc3b75d275698a4b1e4c8969b1b840429c919
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 27%

---


# [!DNL Amazon S3] Ziel

## Übersicht

Create a live outbound connection to your [!DNL Amazon Web Services] (AWS) S3 storage to periodically export tab-delimited or CSV data files from Adobe Experience Platform into your own S3 buckets.

## Exporttyp {#export-type}

**Profil-basiert** - Sie exportieren alle Segmentmitglieder zusammen mit den gewünschten Segmentfeldern (z. B.: E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm &quot;Attribute auswählen&quot;des Arbeitsablaufs für die [Ziel-Aktivierung](../../ui/activate-destinations.md#select-attributes)ausgewählt.

![Amazon S3-Profil-basierter Exporttyp](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## Ziel verbinden {#connect-destination}

See [Cloud storage destinations workflow ](./workflow.md) for instructions on how to connect to your cloud storage destinations, including [!DNL Amazon S3].

For [!DNL Amazon S3] destinations, enter the following information in the create destination workflow:

* **[!DNL Amazon S3]Zugriffsschlüssel und [!DNL Amazon S3] geheimer Schlüssel**: Generieren Sie [!DNL Amazon S3]ein `access key - secret access key` Paar, um CDP-Echtzeitzugriff auf Ihr [!DNL Amazon S3] Konto zu gewähren. Weitere Informationen finden Sie in der Dokumentation zu [Amazon Web Services](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

>[!IMPORTANT]
>
>Real-time CDP needs `write` permissions on the bucket object where the export files will be delivered.

## Exportierte Daten {#exported-data}

For [!DNL Amazon S3] destinations, Real-time CDP creates a tab-delimited `.txt` or `.csv` file in the storage location that you provided. Weitere Informationen zu den Dateien finden Sie unter [E-Mail-Marketing-Ziele und Cloud-Datenspeicherung-Ziele](../../ui/activate-destinations.md#esp-and-cloud-storage) im Tutorial zur Aktivierung von Segmenten.
