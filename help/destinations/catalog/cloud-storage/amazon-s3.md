---
keywords: Amazon S3;S3-Ziel;s3;Amazon s3
title: Amazon S3-Verbindung
description: Erstellen Sie eine aktive ausgehende Verbindung zu Ihrem Amazon Web Services (AWS) S3-Speicher, um in regelmäßigen Abständen tabulatorgetrennte oder CSV-Datendateien aus Adobe Experience Platform in Ihre eigenen S3-Buckets zu exportieren.
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: 49a59e5b081243679f5d94b03a63d30df22cdc6a
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 12%

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

>[!TIP]
>
>Im Arbeitsablauf für das Verbindungsziel können Sie einen benutzerdefinierten Ordner in Ihrer Amazon S3-Datenspeicherung pro exportierter Segmentdatei erstellen. Lesen Sie die Anleitungen unter [Verwenden Sie Makros, um einen Datenspeicherung-Speicherort zu erstellen.](./workflow.md#use-macros)

## Erforderliche [!DNL Amazon S3] Berechtigungen {#required-s3-permission}

Um Daten erfolgreich an den Speicherort [!DNL Amazon S3] der Datenspeicherung zu verbinden und zu exportieren, erstellen Sie einen IAM-Benutzer (Identity and Access Management) für [!DNL Platform] in [!DNL Amazon S3] und weisen Sie Berechtigungen für die folgenden Aktionen zu:

* `s3:DeleteObject`
* `s3:GetBucketLocation`
* `s3:GetObject`
* `s3:ListBucket`
* `s3:PutObject`
* `s3:ListMultipartUploadParts`


<!--

Commenting out this note, as write permissions are assigned through the s3:PutObject permission.

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->


## Exportierte Daten {#exported-data}

Für [!DNL Amazon S3]-Ziele erstellt [!DNL Platform] eine tabulatorgetrennte `.txt`- oder `.csv`-Datenspeicherung im angegebenen Speicherort. Weitere Informationen zu den Aktivierungen finden Sie unter [E-Mail-Marketing-Ziele und Cloud-Datenspeicherung-Ziele](../../ui/activate-destinations.md#esp-and-cloud-storage) im Tutorial zur Segmentbildung.
