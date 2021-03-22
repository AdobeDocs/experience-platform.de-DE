---
keywords: Amazon S3;S3-Ziel;s3;Amazon s3
title: Amazon S3-Verbindung
description: Erstellen Sie eine aktive ausgehende Verbindung zu Ihrem Amazon Web Services (AWS) S3-Speicher, um in regelmäßigen Abständen tabulatorgetrennte oder CSV-Datendateien aus Adobe Experience Platform in Ihre eigenen S3-Buckets zu exportieren.
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '223'
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

>[!IMPORTANT]
>
>Die Plattform benötigt für das Behälterobjekt, für das die Exportdateien bereitgestellt werden, `write` Berechtigungen.

## Exportierte Daten {#exported-data}

Für [!DNL Amazon S3]-Ziele erstellt Platform eine tabulatorgetrennte `.txt`- oder `.csv`-Datenspeicherung im angegebenen Speicherort. Weitere Informationen zu den Aktivierungen finden Sie unter [E-Mail-Marketing-Ziele und Cloud-Datenspeicherung-Ziele](../../ui/activate-destinations.md#esp-and-cloud-storage) im Tutorial zur Segmentbildung.
