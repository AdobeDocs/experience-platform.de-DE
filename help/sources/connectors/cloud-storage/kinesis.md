---
keywords: Experience Platform;Home;beliebte Themen;Amazon Kinesis;Amazonaskinese;Kinesis;Kininose
solution: Experience Platform
title: Amazon Kinesis Source Connector - Übersicht
topic-legacy: overview
description: Erfahren Sie, wie Sie Amazon Kinesis mit APIs oder der Benutzeroberfläche mit Adobe Experience Platform verbinden.
exl-id: b71fc922-7722-4279-8fc6-e5d7735e1ebb
translation-type: tm+mt
source-git-commit: af11bc966889be54fc27e02f3eee321519cef88f
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 1%

---

# [!DNL Amazon Kinesis] connector

Adobe Experience Platform bietet native Konnektivität für Cloud-Anbieter wie AWS, [!DNL Google Cloud Platform] und [!DNL Azure]. Sie können Ihre Daten von diesen Systemen in [!DNL Platform] übertragen.

Cloud-Datenspeicherung-Quellen können Ihre eigenen Daten in [!DNL Platform] übertragen, ohne dass Sie sie herunterladen, formatieren oder hochladen müssen. Ingetierte Daten können als XDM-JSON, XDM-Parquet oder als Trennzeichen formatiert werden. Jeder Schritt des Prozesses ist in den Sources-Workflow integriert. [!DNL Platform] ermöglicht es Ihnen, Daten  [!DNL Amazon Kinesis] in Echtzeit einzubringen.

## Zulassungsliste der IP-Adresse

Eine Liste von IP-Adressen muss einer Zulassungsliste hinzugefügt werden, bevor Sie mit Quellschnittstellen arbeiten können. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Leistungseinbußen führen. Weitere Informationen finden Sie auf der Zulassungsliste [IP-Adresse](../../ip-address-allow-list.md).

## Voraussetzungen

Im folgenden Abschnitt finden Sie weitere Informationen zur erforderlichen Einrichtung, bevor Sie eine [!DNL Kinesis]-Quellverbindung erstellen können.

### Zugriffsrichtlinie einrichten

Ein [!DNL Kinesis]-Stream erfordert die folgenden Berechtigungen, um eine Quellverbindung zu erstellen:

- `GetShardIterator`
- `GetRecords`
- `DescribeStream`
- `ListStreams`

Diese Berechtigungen werden über die Konsole [!DNL Kinesis] angeordnet und von der Plattform überprüft, sobald Sie Ihre Anmeldeinformationen eingegeben und den Datenstrom ausgewählt haben.

Im folgenden Beispiel werden die Mindestzugriffsrechte angezeigt, die erforderlich sind, um eine [!DNL Kinesis]-Quellverbindung zu erstellen.

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
| `kinesis:GetRecords` | Eine Aktion, die erforderlich ist, um Datensätze von einer bestimmten Offset- oder freigegebenen ID abzurufen. |
| `kinesis:DescribeStream` | Eine Aktion, die Informationen zum Stream einschließlich der gemeinsamen Zuordnung zurückgibt, die zum Generieren einer gemeinsamen ID erforderlich sind. |
| `kinesis:ListStreams` | Eine erforderliche Aktion zur Liste der verfügbaren Streams, die Sie in der Benutzeroberfläche auswählen können. |

Weitere Informationen zum Steuern des Zugriffs für [!DNL Kinesis]-Datenströme finden Sie im folgenden [[!DNL Kinesis] Dokument](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

### Iterator-Typ konfigurieren

[!DNL Kinesis] unterstützt die folgenden Iterator-Typen, damit Sie die Reihenfolge angeben können, in der Ihre Daten gelesen werden:

| Iterator-Typ | Beschreibung |
| ------------- | ----------- |
| `AT_SEQUENCE_NUMBER` | Die Daten werden ausgehend von einer durch eine bestimmte Sequenznummer identifizierten Position gelesen. |
| `AFTER_SEQUENCE_NUMBER` | Die Daten werden ab der durch eine bestimmte Sequenznummer identifizierten Position gelesen. |
| `AT_TIMESTAMP` | Die Daten werden ausgehend von einer durch einen bestimmten Zeitstempel identifizierten Position gelesen. |
| `TRIM_HORIZON` | Die Daten werden ausgehend vom ältesten Datensatz gelesen. |
| `LATEST` | Die Daten werden ab dem neuesten Datensatz gelesen. |

Eine [!DNL Kinesis]-UI-Quelle unterstützt derzeit nur `TRIM_HORIZON`, während die API sowohl `TRIM_HORIZON` als auch `LATEST` als Modi zum Abrufen von Daten unterstützt. Der standardmäßige Iterator-Wert, den Platform für die [!DNL Kinesis]-Quelle verwendet, ist `TRIM_HORIZON`.

Weitere Informationen zu Iteratortypen finden Sie im folgenden [[!DNL Kinesis] Dokument](https://docs.aws.amazon.com/kinesis/latest/APIReference/API_GetShardIterator.html#API_GetShardIterator_RequestSyntax).

## Verbinden Sie [!DNL Amazon Kinesis] mit [!DNL Platform]

Die nachstehende Dokumentation enthält Informationen dazu, wie [!DNL Amazon Kinesis] mithilfe von APIs oder der Benutzeroberfläche mit [!DNL Platform] verbunden wird:

### APIs verwenden

- [Erstellen einer Amazon Kinesis-Quellverbindung mit der Flow Service API](../../tutorials/api/create/cloud-storage/kinesis.md)
- [Erfassen von Streaming-Daten mithilfe der Flow Service API](../../tutorials/api/collect/streaming.md)

### Verwenden der UI

- [Erstellen einer Amazon Kinesis-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/create/cloud-storage/kinesis.md)
- [Konfigurieren eines Datenflusses für eine Cloud-Datenspeicherung-Verbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
