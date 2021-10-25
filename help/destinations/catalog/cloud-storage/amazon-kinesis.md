---
keywords: Amazon Kinesis;Kinsis destination;kinesis
title: Verbindung Amazon Kinesis
description: Erstellen Sie eine ausgehende Echtzeit-Verbindung mit Ihrer Amazon Kinesis-Datenspeicherung, um Daten von Adobe Experience Platform zu streamen.
exl-id: b40117ef-6ad0-48a9-bbcb-97c6f6d1dce3
source-git-commit: 2b1cde9fc913be4d3bea71e7d56e0e5fe265a6be
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 3%

---

# (Beta) [!DNL Amazon Kinesis] Verbindung

## Übersicht {#overview}

>[!IMPORTANT]
>
>Die [!DNL Amazon Kinesis] Ziel in Platform befindet sich derzeit in der Beta-Version. Die Dokumentation und Funktionalität können sich ändern.

Die [!DNL Kinesis Data Streams] Dienst von [!DNL Amazon Web Services] ermöglicht die Erfassung und Verarbeitung großer Datenströme in Echtzeit.

Sie können eine ausgehende Echtzeitverbindung zu Ihrem [!DNL Amazon Kinesis] Datenspeicherung zum Streamen von Daten aus Adobe Experience Platform.

* Für weitere Informationen über [!DNL Amazon Kinesis], siehe [Amazon-Dokumentation](https://docs.aws.amazon.com/streams/latest/dev/introduction.html).
* Verbindung herstellen zu [!DNL Amazon Kinesis] im [Übungen zur Streaming-Ziel-API](../../api/streaming-destinations.md).
* Verbindung herstellen zu [!DNL Amazon Kinesis] unter Verwendung der Platform-Benutzeroberfläche, siehe die Abschnitte unten.

![Amazon Kinesis in der UI](../../assets/catalog/cloud-storage/amazon-kinesis/catalog.png)

## Anwendungsfälle {#use-cases}

Durch Streaming-Ziele wie [!DNL Amazon Kinesis], können Sie problemlos hochwertige Segmentierungsattribute und zugehörige Profil-Attribute in Ihre bevorzugten Ereignis einspeisen.

Ein Potenzieller Kunde hat beispielsweise ein Whitepaper heruntergeladen, das sie in ein Segment mit hoher Konversionsneigung einordnet. Durch Zuordnen des Segments, in das der Potenzieller Kunde fällt, zum [!DNL Amazon Kinesis] Ziel, erhalten Sie dieses Ereignis in [!DNL Amazon Kinesis]. Hier können Sie einen Do-it-yourself-Ansatz verwenden und die Geschäftslogik zusätzlich zum Ereignis beschreiben, da Sie denken, dass Sie am besten mit Ihren Enterprise-IT-Systemen arbeiten würden.

## Exporttyp {#export-type}

**Profil-basiert** - Sie exportieren alle Segmentmitglieder zusammen mit den gewünschten Segmentfeldern (z. B.: E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm mit den ausgewählten Attributen des [Workflow für Audience Aktivierung](../../ui/activate-streaming-profile-destinations.md#select-attributes).

## Erforderlich [!DNL Amazon Kinesis] Berechtigungen {#required-kinesis-permission}

So verbinden Sie erfolgreich Daten mit [!DNL Amazon Kinesis] Streams, benötigt die Experience Platform Berechtigungen für die folgenden Aktionen:

* `kinesis:ListStreams`
* `kinesis:PutRecord`
* `kinesis:PutRecords`

Diese Berechtigungen werden über die [!DNL Kinesis] -Konsole und werden von Platform aktiviert, sobald Sie Ihr Kinesis-Ziel in der Platform-Benutzeroberfläche konfigurieren.

Im folgenden Beispiel werden die Mindestzugriffsrechte angezeigt, die erforderlich sind, um Daten erfolgreich in ein [!DNL Kinesis] Ziel.

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "kinesis:ListStreams",
                "kinesis:PutRecord",
                "kinesis:PutRecords"
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
| `kinesis:ListStreams` | Eine Aktion, die Ihre Amazon Kinesis-Datenströme Liste. |
| `kinesis:PutRecord` | Eine Aktion, die einen einzelnen Datensatz in einen Kinesis-Datenstrom schreibt. |
| `kinesis:PutRecords` | Eine Aktion, die mehrere Datensätze in einem einzigen Aufruf in einen Kinesis-Datenstrom schreibt. |

Weitere Informationen zur Zugangskontrolle für [!DNL Kinesis] Datenströme, lesen Sie Folgendes [[!DNL Kinesis] Dokument](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

## Mit Ziel verbinden {#connect}

Um eine Verbindung zu diesem Ziel herzustellen, führen Sie die Schritte aus, die in der [Übungen zur Zielkonfiguration](../../ui/connect-destination.md).

### Verbindungsparameter {#parameters}

Während [einrichten](../../ui/connect-destination.md) an diesem Ziel angeben, müssen Sie die folgenden Informationen angeben:

* **[!DNL Amazon Web Services]Zugriffsschlüssel und geheimer Schlüssel**: In [!DNL Amazon Web Services], erstellen Sie `access key - secret access key` , um Plattformzugriff auf Ihre [!DNL Amazon Kinesis] Konto. Weitere Informationen unter [Amazon Web Services-Dokumentation](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **Region**: Geben Sie an, welche [!DNL Amazon Web Services] Bereich, in den Daten gestreamt werden sollen.
* **Name**: Geben Sie einen Namen für die Verbindung ein, zu der [!DNL Amazon Kinesis]
* **Beschreibung**: Geben Sie eine Beschreibung für die Verbindung an, zu der [!DNL Amazon Kinesis].
* **Stream**: Geben Sie den Namen eines vorhandenen Datenstroms in Ihrem [!DNL Amazon Kinesis] Konto. Die Plattform exportiert Daten in diesen Stream.

<!--

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Segmente zu diesem Ziel aktivieren {#activate}

Siehe [Audience-Daten in Streaming-Profil-Exportziele aktivieren](../../ui/activate-streaming-profile-destinations.md) für Anweisungen zum Aktivieren von Audiencen-Segmenten für dieses Ziel.

## Exportierte Daten {#exported-data}

Ihr exportiert [!DNL Experience Platform] Daten landen in [!DNL Amazon Kinesis] im JSON-Format. Das folgende Ereignis enthält beispielsweise das E-Mail-Adressattribut einer Audience, die sich für ein bestimmtes Profil qualifiziert und ein anderes Segment verlassen hat. Die Identitäten für diesen Potenzieller Kunde sind ECID und E-Mail.

```json
{
  "person": {
    "email": "yourstruly@adobe.com"
  },
  "segmentMembership": {
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "existing"
      }
    }
  },
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```



>[!MORELIKETHIS]
>
>* [Mit Amazon Kinesis verbinden und Daten mithilfe der Flow Service API aktivieren](../../api/streaming-destinations.md)
>* [Azure Ereignis Hubs-Ziel](./azure-event-hubs.md)
>* [Zieltypen und Kategorien](../../destination-types.md)

