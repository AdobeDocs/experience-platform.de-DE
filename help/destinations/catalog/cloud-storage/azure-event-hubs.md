---
keywords: Azure Event Hub-Ziel; Azure Event Hub; Azure Event Event Event Hub
title: (Beta) !DNL Azure Event Hubs]-Verbindung
description: Erstellen Sie eine ausgehende Echtzeitverbindung zu Ihrem !DNL Azure Event Hubs]-Speicher, um Daten von Experience Platform zu streamen.
exl-id: f98a389a-bce3-4a80-9452-6c7293d01de3
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 3%

---

# (Beta) [!DNL Azure Event Hubs] Verbindung

## Übersicht {#overview}

>[!IMPORTANT]
>
>Das [!DNL Azure Event Hubs]-Ziel in Platform befindet sich derzeit in der Betaphase. Die Dokumentation und Funktionalität können sich ändern.

[!DNL Azure Event Hubs] ist eine Big-Data-Streaming-Plattform und ein Event-Erfassungsdienst. Es kann Millionen von Ereignissen pro Sekunde empfangen und verarbeiten. An einen Ereignis-Hub gesendete Daten können mithilfe eines beliebigen Echtzeit-Analytics-Anbieters oder von Batch-/Speicheradaptern umgewandelt und gespeichert werden.

Sie können eine ausgehende Echtzeitverbindung zu Ihrem [!DNL Azure Event Hubs]-Speicher erstellen, um Daten von Adobe Experience Platform zu streamen.

* Weitere Informationen zu [!DNL Azure Event Hubs] finden Sie in der [Microsoft-Dokumentation](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about).
* Informationen zum programmgesteuerten Herstellen einer Verbindung zu [!DNL Azure Event Hubs] finden Sie im [Tutorial zur Streaming-Ziel-API](../../api/streaming-destinations.md).
* Informationen zum Herstellen einer Verbindung zu [!DNL Azure Event Hubs] mithilfe der Benutzeroberfläche von Platform finden Sie in den folgenden Abschnitten.

![AWS Kinesis in der Benutzeroberfläche](../../assets/catalog/cloud-storage/event-hubs/catalog.png)

## Nutzungsszenarios {#use-cases}

Durch die Verwendung von Streaming-Zielen wie [!DNL Azure Event Hubs] können Sie einfach hochwertige Segmentierungsereignisse und zugehörige Profilattribute in Ihre bevorzugten Systeme einspeisen.

Beispielsweise hat ein Interessent ein Whitepaper heruntergeladen, das ihn in ein Segment mit hoher Konversionsneigung qualifiziert. Wenn Sie das Segment zuordnen, in das der Interessent zum [!DNL Azure Event Hubs]-Ziel gehört, erhalten Sie dieses Ereignis in [!DNL Azure Event Hubs]. Dort können Sie zusätzlich zu dem Ereignis einen &quot;do-it-self&quot;-Ansatz verwenden und die Geschäftslogik beschreiben, da Sie denken, dass dies am besten mit Ihren Enterprise-IT-Systemen funktionieren würde.

## Exporttyp {#export-type}

**Profilbasiert**  - Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B.: E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm &quot;Attribute auswählen&quot;des  [Zielgruppenaktivierungs-Workflows](../../ui/activate-streaming-profile-destinations.md#select-attributes) ausgewählt.

## Mit Ziel verbinden {#connect}

Um eine Verbindung zu diesem Ziel herzustellen, führen Sie die Schritte aus, die im Tutorial [Zielkonfiguration](../../ui/connect-destination.md) beschrieben sind.

### Verbindungsparameter {#parameters}

Während [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL SAS-]** Schlüsselname und  **[!UICONTROL SAS-Schlüssel]**: Geben Sie Ihren SAS-Schlüsselnamen und -Schlüssel ein. Informationen zur Authentifizierung bei [!DNL Azure Event Hubs] mit SAS-Schlüsseln finden Sie in der [Microsoft-Dokumentation](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL Namespace]**: Füllen Sie Ihren  [!DNL Azure Event Hubs] Namespace aus. Weitere Informationen zu [!DNL Azure Event Hubs]-Namespaces finden Sie in der [Microsoft-Dokumentation](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).
* **[!UICONTROL Name]**: Geben Sie einen Namen für die Verbindung zu  [!DNL Azure Event Hubs]ein.
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung der Verbindung an.  Beispiele: &quot;Premium-Tier-Kunden&quot;, &quot;Männchen für Kitesurfen interessiert&quot;.
* **[!UICONTROL eventHubName]**: Geben Sie einen Namen für den Stream an Ihr  [!DNL Azure Event Hubs] Ziel an.

## Aktivieren von Segmenten für dieses Ziel {#activate}

Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Streaming-Profilexport-Ziele](../../ui/activate-streaming-profile-destinations.md) .

## Exportierte Daten {#exported-data}

Ihre exportierten [!DNL Experience Platform]-Daten werden im JSON-Format [!DNL Azure Event Hubs] angezeigt. Beispielsweise enthält das nachstehende Ereignis das E-Mail-Adressen-Profilattribut einer Zielgruppe, die sich für ein bestimmtes Segment qualifiziert und ein anderes Segment verlassen hat. Die Identitäten für diesen Interessenten sind ECID und E-Mail.

```json
{
  "person": {
    "email": "yourstruly@adobe.con"
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
>* [Verbindung zu Azure Event Hubs herstellen und Daten mithilfe der Flow Service-API aktivieren](../../api/streaming-destinations.md)
* [AWS Kinesis-Ziel](./amazon-kinesis.md)
* [Zieltypen und Kategorien](../../destination-types.md)

