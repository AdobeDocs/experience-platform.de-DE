---
keywords: Cloud-Speicher-Ziel; Cloud-Speicher
title: Übersicht über Cloud-Speicher-Ziele
description: Adobe Experience Platform kann Ihre Segmente als Datendateien an Ihre Amazon S3-, AWS Kinesis-, Azure Event Hubs- oder SFTP-Cloud-Speicherorte senden.
exl-id: d29f0a6e-b323-4f78-bbd0-dee2f1e0fedb
source-git-commit: 802b1844bec1e577e978da5d5a69de87278c04b9
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 2%

---

# Übersicht über die Cloud-Speicher-Ziele {#cloud-storage-destinations}

## Übersicht {#overview}

Adobe Experience Platform kann Ihre Segmente als Datendateien an Ihre Cloud-Speicherorte senden. Dadurch können Sie Zielgruppen und ihre Profilattribute über CSV- oder tabulatorgetrennte Dateien für [!DNL Amazon S3], [!DNL Azure Blob] und SFTP an Ihre internen Systeme senden. Bei [!DNL Amazon Kinesis]- und [!DNL Azure Event Hubs]-Zielen werden die Daten aus der Experience Platform im [!DNL JSON]-Format gestreamt.

![Adobe Cloud-Speicher-Ziele](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

## Unterstützte Cloud-Speicher-Ziele {#supported-destinations}

Adobe Experience Platform unterstützt die folgenden Cloud-Speicher-Ziele:

* [Amazon Kinesis-Verbindung](amazon-kinesis.md)
* [Amazon S3-Verbindung](amazon-s3.md)
* [Azure Blob-Verbindung](azure-blob.md)
* [Azure Event Hubs-Verbindung](azure-event-hubs.md)
* [SFTP-Verbindung](sftp.md)

## Verbindung zu einem neuen Cloud-Speicher-Ziel herstellen {#connect-destination}

Um Segmente für Ihre Kampagnen an Cloud-Speicher-Ziele zu senden, muss Platform zunächst eine Verbindung zum Ziel herstellen. Detaillierte Informationen zum Einrichten eines neuen Ziels finden Sie im [Tutorial zur Zielerstellung](../../ui/connect-destination.md) .


## Verwenden von Makros zum Erstellen eines Ordners in Ihrem Speicherort {#use-macros}

>[!NOTE]
>
> Die in diesem Abschnitt beschriebene Funktion ist derzeit nur für [Amazon S3](amazon-s3.md)-Ziele verfügbar.

Um einen benutzerdefinierten Ordner pro Segmentdatei in Ihrem Speicherort zu erstellen, können Sie Makros im Eingabefeld Ordnerpfad verwenden. Fügen Sie die Makros am Ende des Eingabefelds ein, wie unten dargestellt.

![Verwenden von Makros zum Erstellen eines Ordners in Ihrem Speicher](../../assets/catalog/cloud-storage/workflow/macros-folder-path.png)

Die folgenden Beispiele verweisen auf ein Beispielsegment `Luxury Audience` mit der ID `25768be6-ebd5-45cc-8913-12fb3f348615`.

**Makro 1:`%SEGMENT_NAME%`**

Eingabe: `acme/campaigns/2021/%SEGMENT_NAME%`
Ordnerpfad in Ihrem Speicherort: `acme/campaigns/2021/Luxury Audience`

**Makro 2:`%SEGMENT_ID%`**

Eingabe: `acme/campaigns/2021/%SEGMENT_ID%`
Ordnerpfad in Ihrem Speicherort: `acme/campaigns/2021/25768be6-ebd5-45cc-8913-12fb3f348615`

**Makro 3:`%SEGMENT_NAME%/%SEGMENT_ID%`**

Eingabe: `acme/campaigns/2021/%SEGMENT_NAME%/%SEGMENT_ID%`
Ordnerpfad in Ihrem Speicherort: `acme/campaigns/2021/Luxury Audience/25768be6-ebd5-45cc-8913-12fb3f348615`

## Datenexporttyp {#export-type}

Cloud-Speicher-Ziele unterstützen **Profil-basierter Export**. Das bedeutet, dass Sie Details über die Kontakte in der Audience exportieren. Diese Details sind für die Personalisierung erforderlich und können Attribute, Ereignisse, Segmentmitgliedschaften und mehr umfassen.