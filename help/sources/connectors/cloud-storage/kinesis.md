---
keywords: Experience Platform; Startseite; beliebte Themen; Amazon Kinesis; amazon kinesis; Kinesis; Kinesis
solution: Experience Platform
title: Übersicht über den Quell-Connector für Amazon Kinesis
topic-legacy: overview
description: Erfahren Sie, wie Sie mit APIs oder der Benutzeroberfläche eine Verbindung zwischen Amazon Kinesis und Adobe Experience Platform herstellen.
exl-id: b71fc922-7722-4279-8fc6-e5d7735e1ebb
source-git-commit: 481f72c5c630f6dbcbbfd3eee11c91787e780f3f
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 2%

---

# [!DNL Amazon Kinesis] Connector

Adobe Experience Platform bietet native Konnektivität für Cloud-Anbieter wie AWS, [!DNL Google Cloud Platform] und [!DNL Azure]. Sie können Ihre Daten aus diesen Systemen in [!DNL Platform] übertragen.

Cloud-Speicher-Quellen können Ihre eigenen Daten in [!DNL Platform] übertragen, ohne herunterladen, formatieren oder hochladen zu müssen. Aufgenommene Daten können als XDM JSON-, XDM Parquet- oder als Trennzeichen formatiert werden. Jeder Schritt des Prozesses wird in den Sources-Workflow integriert. [!DNL Platform] ermöglicht Ihnen, Daten aus  [!DNL Amazon Kinesis] in Echtzeit einzubringen.

## Voraussetzungen

Im folgenden Abschnitt finden Sie weitere Informationen zur erforderlichen Einrichtung, bevor Sie eine [!DNL Kinesis]-Quellverbindung erstellen können.

### Zugriffsrichtlinie einrichten

Ein [!DNL Kinesis]-Stream erfordert die folgenden Berechtigungen, um eine Quellverbindung zu erstellen:

- `GetShardIterator`
- `GetRecords`
- `DescribeStream`
- `ListStreams`

Diese Berechtigungen werden über die Konsole [!DNL Kinesis] angeordnet und von Platform überprüft, sobald Sie Ihre Anmeldedaten eingeben und Ihren Daten-Stream auswählen.

Im folgenden Beispiel werden die Mindestzugriffsrechte angezeigt, die zum Erstellen einer [!DNL Kinesis]-Quellverbindung erforderlich sind.

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

Weitere Informationen zum Steuern des Zugriffs für [!DNL Kinesis]-Datenströme finden Sie im folgenden [[!DNL Kinesis] Dokument](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

### Iterator-Typ konfigurieren

[!DNL Kinesis] unterstützt die folgenden Iteratortypen, mit denen Sie die Reihenfolge angeben können, in der Ihre Daten gelesen werden:

| Iterator-Typ | Beschreibung |
| ------------- | ----------- |
| `AT_SEQUENCE_NUMBER` | Die Daten werden ausgehend von einer Position gelesen, die durch eine bestimmte Sequenznummer identifiziert wird. |
| `AFTER_SEQUENCE_NUMBER` | Die Daten werden nach Position gelesen, die durch eine bestimmte Sequenznummer identifiziert wird. |
| `AT_TIMESTAMP` | Die Daten werden ausgehend von einer Position gelesen, die durch einen bestimmten Zeitstempel identifiziert wird. |
| `TRIM_HORIZON` | Die Daten werden ab dem ältesten Datensatz gelesen. |
| `LATEST` | Die Daten werden ab dem letzten Datensatz gelesen. |

Eine [!DNL Kinesis] UI-Quelle unterstützt derzeit nur `TRIM_HORIZON`, während die API sowohl `TRIM_HORIZON` als auch `LATEST` als Modi zum Abrufen von Daten unterstützt. Der standardmäßige Iteratorwert, den Platform für die Quelle [!DNL Kinesis] verwendet, ist `TRIM_HORIZON`.

Weitere Informationen zu Iteratortypen finden Sie im folgenden [[!DNL Kinesis] Dokument](https://docs.aws.amazon.com/kinesis/latest/APIReference/API_GetShardIterator.html#API_GetShardIterator_RequestSyntax).

## Verbinden Sie [!DNL Amazon Kinesis] mit [!DNL Platform]

Die folgende Dokumentation enthält Informationen dazu, wie Sie mithilfe von APIs oder der Benutzeroberfläche eine Verbindung zwischen [!DNL Amazon Kinesis] und [!DNL Platform] herstellen:

### Verwenden von APIs

- [Erstellen einer Amazon Kinesis-Quellverbindung mit der Flow Service-API](../../tutorials/api/create/cloud-storage/kinesis.md)
- [Erfassen von Streaming-Daten mithilfe der Flow Service-API](../../tutorials/api/collect/streaming.md)

### Verwenden der UI

- [Erstellen einer Amazon Kinesis-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [Konfigurieren eines Datenflusses für eine Cloud-Speicherverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
