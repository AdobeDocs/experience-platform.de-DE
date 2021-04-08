---
keywords: Amazon S3;S3-Ziel;s3;Amazon s3
title: Amazon S3-Verbindung
description: Erstellen Sie eine aktive ausgehende Verbindung zu Ihrem Amazon Web Services (AWS) S3-Speicher, um in regelmäßigen Abständen tabulatorgetrennte oder CSV-Datendateien aus Adobe Experience Platform in Ihre eigenen S3-Buckets zu exportieren.
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
translation-type: tm+mt
source-git-commit: d77cd063e61118631b757d9821267b2fd6ab0148
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 14%

---

# [!DNL Amazon S3] connection  {#s3-connection}

## Übersicht {#overview}

Erstellen Sie eine Live-Ausgehende Verbindung zu Ihrer [!DNL Amazon Web Services] (AWS) S3-Datenspeicherung, um in regelmäßigen Abständen tabulatorgetrennte oder CSV-Datendateien aus Adobe Experience Platform in Ihre eigenen S3-Behälter zu exportieren.

## Exporttyp {#export-type}

**Profil-basiert** : Sie exportieren alle Segmentmitglieder zusammen mit den gewünschten Segmentfeldern (z. B.: E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm &quot;Attribute auswählen&quot;des Arbeitsablaufs für die  [Ziel-Aktivierung](../../ui/activate-destinations.md#select-attributes) ausgewählt.

![Amazon S3-Profil-basierter Exporttyp](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## Ziel verbinden {#connect-destination}

Anweisungen zum Herstellen einer Verbindung mit Ihren Cloud-Datenspeicherung-Zielen, einschließlich [!DNL Amazon S3], finden Sie unter [Arbeitsablauf für Cloud-Datenspeicherung-Ziele ](./workflow.md).

Geben Sie für [!DNL Amazon S3]-Ziele im Arbeitsablauf zum Erstellen von Zielen die folgenden Informationen ein:

* **[!DNL Amazon S3]Zugriffsschlüssel und  [!DNL Amazon S3] geheimer Schlüssel**: Generieren Sie  [!DNL Amazon S3]ein  `access key - secret access key` Paar, um Platform Zugriff auf Ihr  [!DNL Amazon S3] Konto zu gewähren. Weitere Informationen finden Sie in der Dokumentation zu Amazon Web Services](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).[

## Erforderliche [!DNL Amazon S3] Berechtigungen {#required-s3-permission}

Um Daten erfolgreich an den Speicherort der [!DNL Amazon S3]-Datenspeicherung zu verbinden und zu exportieren, erstellen Sie einen IAM-Benutzer für [!DNL Platform] in [!DNL Amazon S3] und weisen Sie Berechtigungen für folgende Aktionen zu:

* `s3:DeleteObject`
* `s3:DeleteObjectVersion`
* `s3:GetBucketLocation`
* `s3:GetObject`
* `s3:GetObjectVersion`
* `s3:ListBucket`
* `s3:ListBuckets`
* `s3:PutBucketVersioning`
* `s3:PutObject`
* `s3:ReplicateObject`
* `s3:RestoreObject`


<!--

Commenting out this note, as write permissions are assigned through the s3:PutObject permission.

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->


## Exportierte Daten {#exported-data}

Für [!DNL Amazon S3]-Ziele erstellt [!DNL Platform] eine tabulatorgetrennte `.txt`- oder `.csv`-Datenspeicherung im angegebenen Speicherort. Weitere Informationen zu den Aktivierungen finden Sie unter [E-Mail-Marketing-Ziele und Cloud-Datenspeicherung-Ziele](../../ui/activate-destinations.md#esp-and-cloud-storage) im Tutorial zur Segmentbildung.
