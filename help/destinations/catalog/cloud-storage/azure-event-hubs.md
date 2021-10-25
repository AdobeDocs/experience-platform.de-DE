---
keywords: Azure Ereignis Hub destination;azure Ereignis Hub;azure eventhub
title: (Beta)!DNL Azure Ereignis Hubs]-Verbindung
description: Erstellen Sie eine ausgehende Echtzeit-Verbindung zu Ihrer $$ DNL Azure Ereignis Hubs]-Datenspeicherung, um Daten von der Experience Platform zu streamen.
exl-id: f98a389a-bce3-4a80-9452-6c7293d01de3
source-git-commit: 2b1cde9fc913be4d3bea71e7d56e0e5fe265a6be
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 3%

---

# (Beta) [!DNL Azure Event Hubs] Verbindung

## Übersicht {#overview}

>[!IMPORTANT]
>
>Die [!DNL Azure Event Hubs] Ziel in Platform befindet sich derzeit in der Beta-Version. Die Dokumentation und Funktionalität können sich ändern.

[!DNL Azure Event Hubs] ist eine große Datenstreaming-Plattform und ein Ereignis-Aufnahmedienst. Es kann Millionen von Ereignissen pro Sekunde empfangen und verarbeiten. Daten, die an einen Ereignis-Hub gesendet werden, können mithilfe eines beliebigen Echtzeitanalyseanbieters oder von Batch-/Datenspeicherung-Adaptern transformiert und gespeichert werden.

Sie können eine ausgehende Echtzeitverbindung zu Ihrem [!DNL Azure Event Hubs] Datenspeicherung zum Streamen von Daten aus Adobe Experience Platform.

* Für weitere Informationen über [!DNL Azure Event Hubs], siehe [Microsoft-Dokumentation](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about).
* Verbindung herstellen zu [!DNL Azure Event Hubs] im [Übungen zur Streaming-Ziel-API](../../api/streaming-destinations.md).
* Verbindung herstellen zu [!DNL Azure Event Hubs] unter Verwendung der Platform-Benutzeroberfläche, siehe die Abschnitte unten.

![AWS Kinesis in der UI](../../assets/catalog/cloud-storage/event-hubs/catalog.png)

## Anwendungsfälle {#use-cases}

Durch Streaming-Ziele wie [!DNL Azure Event Hubs], können Sie problemlos hochwertige Segmentierungsattribute und zugehörige Profil-Attribute in Ihre bevorzugten Ereignis einspeisen.

Ein Potenzieller Kunde hat beispielsweise ein Whitepaper heruntergeladen, das sie in ein Segment mit hoher Konversionsneigung einordnet. Durch Zuordnen des Segments, in das der Potenzieller Kunde fällt, zum [!DNL Azure Event Hubs] Ziel, erhalten Sie dieses Ereignis in [!DNL Azure Event Hubs]. Hier können Sie einen Do-it-yourself-Ansatz verwenden und die Geschäftslogik zusätzlich zum Ereignis beschreiben, da Sie denken, dass Sie am besten mit Ihren Enterprise-IT-Systemen arbeiten würden.

## Exporttyp {#export-type}

**Profil-basiert** - Sie exportieren alle Segmentmitglieder zusammen mit den gewünschten Segmentfeldern (z. B.: E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm mit den ausgewählten Attributen des [Workflow für Audience Aktivierung](../../ui/activate-streaming-profile-destinations.md#select-attributes).

## Mit Ziel verbinden {#connect}

Um eine Verbindung zu diesem Ziel herzustellen, führen Sie die Schritte aus, die in der [Übungen zur Zielkonfiguration](../../ui/connect-destination.md).

### Verbindungsparameter {#parameters}

Während [einrichten](../../ui/connect-destination.md) an diesem Ziel angeben, müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL SAS-Schlüsselname]** und **[!UICONTROL SAS-Schlüssel]**: Geben Sie Ihren SAS-Schlüsselnamen und -Schlüssel ein. Informationen zur Authentifizierung bei [!DNL Azure Event Hubs] mit SAS-Tasten in [Microsoft-Dokumentation](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL Namensraum]**: Füllen Sie Ihre [!DNL Azure Event Hubs] Namensraum. Weitere Informationen [!DNL Azure Event Hubs] Namensraum in [Microsoft-Dokumentation](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).
* **[!UICONTROL Name]**: Geben Sie einen Namen für die Verbindung ein zu [!DNL Azure Event Hubs].
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung der Verbindung an.  Beispiele: &quot;Premium-Tier-Kunden&quot;, &quot;Männlich am Kitesurfen interessiert&quot;.
* **[!UICONTROL eventHubName]**: Geben Sie Ihrem [!DNL Azure Event Hubs] Ziel.

## Segmente zu diesem Ziel aktivieren {#activate}

Siehe [Audience-Daten in Streaming-Profil-Exportziele aktivieren](../../ui/activate-streaming-profile-destinations.md) für Anweisungen zum Aktivieren von Audiencen-Segmenten für dieses Ziel.

## Exportierte Daten {#exported-data}

Ihr exportiert [!DNL Experience Platform] Daten landen in [!DNL Azure Event Hubs] im JSON-Format. Das folgende Ereignis enthält beispielsweise das E-Mail-Adressattribut einer Audience, die sich für ein bestimmtes Profil qualifiziert und ein anderes Segment verlassen hat. Die Identitäten für diesen Potenzieller Kunde sind ECID und E-Mail.

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
>* [Stellen Sie eine Verbindung zu Azure Ereignis Hubs her und aktivieren Sie Daten mithilfe der Flow Service API.](../../api/streaming-destinations.md)
>* [AWS Kinesis-Ziel](./amazon-kinesis.md)
>* [Zieltypen und Kategorien](../../destination-types.md)

