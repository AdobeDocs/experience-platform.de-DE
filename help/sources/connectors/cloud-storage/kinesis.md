---
title: Übersicht über Amazon Kinesis Source Connector
description: Erfahren Sie, wie Sie mit APIs oder der Benutzeroberfläche eine Verbindung zwischen Amazon Kinesis und Adobe Experience Platform herstellen.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: b71fc922-7722-4279-8fc6-e5d7735e1ebb
source-git-commit: 9a8139c26b5bb5ff937a51986967b57db58aab6c
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 14%

---

# [!DNL Amazon Kinesis] source

>[!IMPORTANT]
>
>Die Quelle &quot;[!DNL Amazon Kinesis]&quot; steht Benutzern, die Real-time Customer Data Platform Ultimate erworben haben, im Quellkatalog zur Verfügung.

Adobe Experience Platform bietet native Konnektivität für Cloud-Anbieter wie AWS, [!DNL Google Cloud Platform] und [!DNL Azure]. Sie können Ihre Daten aus diesen Systemen in [!DNL Platform] übertragen.

Mit Cloud-Speicherquellen können Sie Ihre eigenen Daten in [!DNL Platform] übertragen, ohne sie herunterladen, formatieren oder hochladen zu müssen. Aufgenommene Daten können als XDM JSON, XDM Parquet oder mit Trennzeichen formatiert werden. Jeder Schritt des Prozesses wird in den Quell-Workflow integriert. Mit [!DNL Platform] können Sie Daten von [!DNL Amazon Kinesis] in Echtzeit einbringen.

>[!NOTE]
>
>Der Skalierungsfaktor für [!DNL Kinesis] muss erhöht werden, wenn Sie Daten mit hohem Volumen erfassen müssen. Derzeit beträgt das maximale Datenvolumen, das Sie von Ihrem [!DNL Kinesis] -Konto an Platform übermitteln können, 4.000 Datensätze pro Sekunde. Wenden Sie sich an Ihren Adobe-Support-Mitarbeiter, um Daten mit höherem Datenvolumen zu skalieren und aufzunehmen.

## Voraussetzungen

Im folgenden Abschnitt finden Sie weitere Informationen zur erforderlichen Einrichtung, bevor Sie eine [!DNL Kinesis]-Quellverbindung erstellen können.

### Zugriffsrichtlinie einrichten

Ein [!DNL Kinesis] -Stream erfordert die folgenden Berechtigungen, um eine Quellverbindung zu erstellen:

- `GetShardIterator`
- `GetRecords`
- `DescribeStream`
- `ListStreams`

Diese Berechtigungen werden über die Konsole [!DNL Kinesis] angeordnet und von Platform überprüft, sobald Sie Ihre Anmeldeinformationen eingeben und Ihren Daten-Stream auswählen.

Im folgenden Beispiel werden die Mindestzugriffsberechtigungen angezeigt, die zum Erstellen einer Quellverbindung mit dem Wert [!DNL Kinesis] erforderlich sind.

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

| Trennzeichentyp | Beschreibung |
| ------------- | ----------- |
| `AT_SEQUENCE_NUMBER` | Die Daten werden ausgehend von einer Position gelesen, die durch eine bestimmte Sequenznummer identifiziert wird. |
| `AFTER_SEQUENCE_NUMBER` | Die Daten werden ab der Position gelesen, die durch eine bestimmte Sequenznummer identifiziert wird. |
| `AT_TIMESTAMP` | Die Daten werden ausgehend von einer Position gelesen, die durch einen bestimmten Zeitstempel identifiziert wird. |
| `TRIM_HORIZON` | Die Daten werden ab dem ältesten Datensatz gelesen. |
| `LATEST` | Die Daten werden ab dem letzten Datensatz gelesen. |

Eine [!DNL Kinesis] UI-Quelle unterstützt derzeit nur `TRIM_HORIZON`, während die API sowohl `TRIM_HORIZON` als auch `LATEST` als Modi zum Abrufen von Daten unterstützt. Der standardmäßige Iteratorwert, den Platform für die [!DNL Kinesis] -Quelle verwendet, ist `TRIM_HORIZON`.

Weitere Informationen zu Iteratortypen finden Sie im folgenden [[!DNL Kinesis] Dokument](https://docs.aws.amazon.com/kinesis/latest/APIReference/API_GetShardIterator.html#API_GetShardIterator_RequestSyntax).

## [!DNL Amazon Kinesis] mit [!DNL Platform] verbinden

Die folgende Dokumentation enthält Informationen dazu, wie Sie mithilfe von APIs oder der Benutzeroberfläche [!DNL Amazon Kinesis] mit [!DNL Platform] verbinden:

### Verwenden von APIs

- [Erstellen einer Amazon Kinesis-Quellverbindung mit der Flow Service-API](../../tutorials/api/create/cloud-storage/kinesis.md)
- [Erfassen von Streaming-Daten mit der Flow Service-API](../../tutorials/api/collect/streaming.md)

### Verwenden der Benutzeroberfläche

- [Erstellen einer Amazon Kinesis-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [Konfigurieren eines Datenflusses für eine Cloud-Speicherverbindung über die Benutzeroberfläche](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
