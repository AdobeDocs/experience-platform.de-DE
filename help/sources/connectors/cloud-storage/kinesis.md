---
keywords: Experience Platform; Startseite; beliebte Themen; Amazon Kinesis; amazon kinesis; Kinesis; Kinesis
solution: Experience Platform
title: Übersicht über den Quell-Connector für Amazon Kinesis
topic-legacy: overview
description: Erfahren Sie, wie Sie mit APIs oder der Benutzeroberfläche eine Verbindung zwischen Amazon Kinesis und Adobe Experience Platform herstellen.
exl-id: b71fc922-7722-4279-8fc6-e5d7735e1ebb
source-git-commit: 5f4355a9d3ef39ee63581fc70dbf0f6e7d674814
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 1%

---

# [!DNL Amazon Kinesis] Connector

Adobe Experience Platform bietet native Konnektivität für Cloud-Anbieter wie AWS, [!DNL Google Cloud Platform]und [!DNL Azure]. Sie können Ihre Daten aus diesen Systemen in [!DNL Platform].

Cloud-Speicher-Quellen können Ihre eigenen Daten in [!DNL Platform] ohne herunterladen, formatieren oder hochladen zu müssen. Aufgenommene Daten können als XDM JSON-, XDM Parquet- oder als Trennzeichen formatiert werden. Jeder Schritt des Prozesses wird in den Sources-Workflow integriert. [!DNL Platform] ermöglicht Ihnen das Einbringen von Daten aus [!DNL Amazon Kinesis] in Echtzeit.

>[!NOTE]
>
>Der Skalierungsfaktor für [!DNL Kinesis] muss erhöht werden, wenn Sie Daten mit hohem Datenvolumen erfassen müssen. Derzeit können Sie ein Höchstvolumen an Daten aus Ihrem [!DNL Kinesis] -Konto in Platform enthält 4000 Datensätze pro Sekunde. Wenden Sie sich an Ihren Ansprechpartner bei der Adobe, um Daten mit höherem Datenvolumen zu skalieren und zu erfassen.

## Voraussetzungen

Im folgenden Abschnitt finden Sie weitere Informationen zur erforderlichen Einrichtung, bevor Sie eine [!DNL Kinesis] Quellverbindung.

### Zugriffsrichtlinie einrichten

A [!DNL Kinesis] Für den Stream sind die folgenden Berechtigungen erforderlich, um eine Quellverbindung zu erstellen:

- `GetShardIterator`
- `GetRecords`
- `DescribeStream`
- `ListStreams`

Diese Berechtigungen werden über die [!DNL Kinesis] und werden von Platform überprüft, sobald Sie Ihre Anmeldedaten eingeben und Ihren Datenstrom auswählen.

Im folgenden Beispiel werden die Mindestzugriffsrechte angezeigt, die zum Erstellen einer [!DNL Kinesis] Quellverbindung.

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "kinesis:GetShardIterator",
                "kinesis:GetRecords",
                "kinesis:DescribeStream",
                "kinesis:ListStreams"
            ],
            "Resource": [
                "arn:aws:kinesis:us-east-2:901341027596:stream/*"
            ]
        }
    ]
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `kinesis:GetShardIterator` | Eine Aktion, die erforderlich ist, um durch Datensätze zu navigieren. |
| `kinesis:GetRecords` | Eine Aktion, die erforderlich ist, um Datensätze von einer bestimmten Offset- oder Shard-ID abzurufen. |
| `kinesis:DescribeStream` | Eine Aktion, die Informationen zum Stream einschließlich der Shard Map zurückgibt, die zum Generieren einer SHARD-ID erforderlich ist. |
| `kinesis:ListStreams` | Eine Aktion, die erforderlich ist, um verfügbare Streams aufzulisten, die Sie über die Benutzeroberfläche auswählen können. |

Weitere Informationen zur Zugriffskontrolle für [!DNL Kinesis] Datenströme, siehe die folgenden [[!DNL Kinesis] Dokument](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

### Iterator-Typ konfigurieren

[!DNL Kinesis] unterstützt die folgenden Iteratortypen, mit denen Sie die Reihenfolge angeben können, in der Ihre Daten gelesen werden:

| Iterator-Typ | Beschreibung |
| ------------- | ----------- |
| `AT_SEQUENCE_NUMBER` | Die Daten werden ausgehend von einer Position gelesen, die durch eine bestimmte Sequenznummer identifiziert wird. |
| `AFTER_SEQUENCE_NUMBER` | Die Daten werden nach Position gelesen, die durch eine bestimmte Sequenznummer identifiziert wird. |
| `AT_TIMESTAMP` | Die Daten werden ausgehend von einer Position gelesen, die durch einen bestimmten Zeitstempel identifiziert wird. |
| `TRIM_HORIZON` | Die Daten werden ab dem ältesten Datensatz gelesen. |
| `LATEST` | Die Daten werden ab dem letzten Datensatz gelesen. |

A [!DNL Kinesis] Benutzeroberflächenquelle wird derzeit nur unterstützt `TRIM_HORIZON`, während die API beide `TRIM_HORIZON` und `LATEST` als Modi zum Abrufen von Daten. Der standardmäßige Iterator-Wert, den Platform für die [!DNL Kinesis] source is `TRIM_HORIZON`.

Weitere Informationen zu Iteratortypen finden Sie in den folgenden [[!DNL Kinesis] Dokument](https://docs.aws.amazon.com/kinesis/latest/APIReference/API_GetShardIterator.html#API_GetShardIterator_RequestSyntax).

## Verbinden [!DNL Amazon Kinesis] nach [!DNL Platform]

Die folgende Dokumentation enthält Informationen zur Verbindung [!DNL Amazon Kinesis] nach [!DNL Platform] Verwendung von APIs oder der Benutzeroberfläche:

### Verwenden von APIs

- [Erstellen einer Amazon Kinesis-Quellverbindung mit der Flow Service-API](../../tutorials/api/create/cloud-storage/kinesis.md)
- [Erfassen von Streaming-Daten mithilfe der Flow Service-API](../../tutorials/api/collect/streaming.md)

### Verwenden der Benutzeroberfläche

- [Erstellen einer Amazon Kinesis-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [Konfigurieren eines Datenflusses für eine Cloud-Speicherverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
