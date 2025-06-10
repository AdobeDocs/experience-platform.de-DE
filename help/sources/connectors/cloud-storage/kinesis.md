---
title: Übersicht über den Amazon Kinesis Source Connector
description: Erfahren Sie, wie Sie Amazon Kinesis mithilfe von APIs oder der Benutzeroberfläche mit Adobe Experience Platform verbinden.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: b71fc922-7722-4279-8fc6-e5d7735e1ebb
source-git-commit: bad1e0a9d86dcce68f1a591060989560435070c5
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 12%

---

# [!DNL Amazon Kinesis]

>[!IMPORTANT]
>
>- Die [!DNL Amazon Kinesis] ist im Quellkatalog für Benutzende verfügbar, die Real-Time CDP Ultimate erworben haben.
>
>- Sie können jetzt die [!DNL Amazon Kinesis]-Quelle verwenden, wenn Sie Adobe Experience Platform auf Amazon Web Services (AWS) ausführen. Experience Platform, das auf AWS ausgeführt wird, steht derzeit einer begrenzten Anzahl von Kunden zur Verfügung. Weitere Informationen zur unterstützten Experience Platform-Infrastruktur finden Sie in der Übersicht zur [Experience Platform Multi-Cloud](../../../landing/multi-cloud.md).


Adobe Experience Platform bietet native Konnektivität für Cloud-Anbieter wie AWS, [!DNL Google Cloud Platform] und [!DNL Azure]. Sie können Ihre Daten aus diesen Systemen in [!DNL Experience Platform] bringen.

Mit Cloud-Speicherquellen können Sie Ihre eigenen Daten in [!DNL Experience Platform] übertragen, ohne sie herunterladen, formatieren oder hochladen zu müssen. Aufgenommene Daten können als XDM JSON, XDM Parquet oder mit Trennzeichen formatiert werden. Jeder Schritt des Prozesses wird in den Quell-Workflow integriert. Mit [!DNL Experience Platform] können Sie Daten aus [!DNL Amazon Kinesis] in Echtzeit importieren.

>[!NOTE]
>
>Der Skalierungsfaktor für [!DNL Kinesis] muss erhöht werden, wenn Daten mit hohem Volumen aufgenommen werden sollen. Derzeit beträgt die maximale Datenmenge, die Sie von Ihrem [!DNL Kinesis]-Konto an Experience Platform übertragen können, 4.000 Datensätze pro Sekunde. Wenden Sie sich an Ihren Adobe-Support-Mitarbeiter, um Daten mit einem größeren Datenvolumen zu skalieren und aufzunehmen.

## Voraussetzungen

Im folgenden Abschnitt finden Sie weitere Informationen zur erforderlichen Einrichtung, bevor Sie eine [!DNL Kinesis] Quellverbindung erstellen können.

### Einrichten der Zugriffsrichtlinie

Ein [!DNL Kinesis]-Stream benötigt die folgenden Berechtigungen, um eine Quellverbindung zu erstellen:

- `GetShardIterator`
- `GetRecords`
- `DescribeStream`
- `ListStreams`

Diese Berechtigungen werden über die [!DNL Kinesis] Console angeordnet und von Experience Platform überprüft, sobald Sie Ihre Anmeldeinformationen eingeben und Ihren Daten-Stream auswählen.

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
| `kinesis:GetShardIterator` | Eine Aktion, die zum Durchlaufen von Datensätzen erforderlich ist. |
| `kinesis:GetRecords` | Eine Aktion, die erforderlich ist, um Datensätze von einer bestimmten Offset- oder Shard-ID abzurufen. |
| `kinesis:DescribeStream` | Eine Aktion, die Informationen zum Stream zurückgibt, einschließlich der Shard-Zuordnung, die zum Generieren einer Shard-ID erforderlich ist. |
| `kinesis:ListStreams` | Eine Aktion, die erforderlich ist, um verfügbare Streams aufzulisten, die Sie in der Benutzeroberfläche auswählen können. |

Weitere Informationen zum Steuern des Zugriffs für [!DNL Kinesis] Datenströme finden Sie im folgenden [[!DNL Kinesis] Dokument](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

### Iterationstyp konfigurieren

[!DNL Kinesis] unterstützt die folgenden Iteratortypen, mit denen Sie die Reihenfolge angeben können, in der Ihre Daten gelesen werden:

| Iteratortyp | Beschreibung |
| ------------- | ----------- |
| `AT_SEQUENCE_NUMBER` | Das Auslesen der Daten erfolgt ausgehend von einer durch eine bestimmte Ablaufnummer identifizierten Position. |
| `AFTER_SEQUENCE_NUMBER` | Die Daten werden nach einer durch eine bestimmte Folgenummer identifizierten Position ausgelesen. |
| `AT_TIMESTAMP` | Die Daten werden ausgehend von einer Position gelesen, die durch einen bestimmten Zeitstempel identifiziert wird. |
| `TRIM_HORIZON` | Die Daten werden ausgehend vom ältesten Datensatz gelesen. |
| `LATEST` | Die Daten werden ab dem letzten Datensatz gelesen. |

Eine [!DNL Kinesis] UI-Quelle unterstützt derzeit nur `TRIM_HORIZON`, während die API sowohl `TRIM_HORIZON` als auch `LATEST` als Modus unterstützt, um Daten abzurufen. Der standardmäßige Iteratorwert, den Experience Platform für die [!DNL Kinesis] verwendet, ist `TRIM_HORIZON`.

Weitere Informationen zu Iteratortypen finden Sie im folgenden [[!DNL Kinesis] Dokument](https://docs.aws.amazon.com/kinesis/latest/APIReference/API_GetShardIterator.html#API_GetShardIterator_RequestSyntax).

## [!DNL Amazon Kinesis] mit [!DNL Experience Platform] verbinden

>[!NOTE]
>
>Nachdem Sie einen Streaming-Datenfluss erstellt oder aktualisiert haben, ist eine kurze 5-minütige Pause bei der Datenaufnahme erforderlich, um potenzielle Instanzen von Datenverlust oder Datenverlust zu verhindern.

Die folgende Dokumentation enthält Informationen zum Verbinden von [!DNL Amazon Kinesis] mit [!DNL Experience Platform] mithilfe von APIs oder der Benutzeroberfläche:

### Verwenden von APIs

- [Erstellen einer Amazon Kinesis-Quellverbindung mithilfe der Flow Service-API](../../tutorials/api/create/cloud-storage/kinesis.md)
- [Erfassen von Streaming-Daten mit der Flow Service-API](../../tutorials/api/collect/streaming.md)

### Verwenden der Benutzeroberfläche

- [Erstellen einer Amazon Kinesis-Quellverbindung über die Benutzeroberfläche](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [Konfigurieren eines Datenflusses für eine Cloud-Speicherverbindung über die Benutzeroberfläche](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
