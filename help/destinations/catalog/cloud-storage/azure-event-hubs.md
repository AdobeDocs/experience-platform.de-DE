---
keywords: Azurblauer Ereignis Hub Destination;Azurer Ereignis Hub;Azurabend
title: (Beta) !DNL-Ereignis-Hubs]-Verbindung
description: Erstellen Sie eine ausgehende Echtzeitverbindung zu Ihrer !DNL-Ereignis-Hubs]-Datenspeicherung, um Daten von der Experience Platform zu streamen.
exl-id: f98a389a-bce3-4a80-9452-6c7293d01de3
translation-type: tm+mt
source-git-commit: ce5001d0a1c95901089915ae9836fdd436f12297
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 6%

---

# (Beta) [!DNL Azure Event Hubs]-Verbindung

## Übersicht {#overview}

>[!IMPORTANT]
>
>Das [!DNL Azure Event Hubs]-Ziel in der Plattform befindet sich derzeit in der Betaphase. Die Dokumentation und Funktionalität können sich ändern.

[!DNL Azure Event Hubs] ist eine große Datenstreaming-Plattform und ein Ereignis-Erfassungsdienst. Es kann Millionen von Ereignissen pro Sekunde empfangen und verarbeiten. Daten, die an einen Ereignis-Hub gesendet werden, können mithilfe eines beliebigen Echtzeitanalyseanbieters oder von Batch-/Datenspeicherung-Adaptern transformiert und gespeichert werden.

Sie können eine ausgehende Echtzeitverbindung zu Ihrer [!DNL Azure Event Hubs]-Datenspeicherung erstellen, um Daten von Adobe Experience Platform zu streamen.

* Weitere Informationen zu [!DNL Azure Event Hubs] finden Sie in der [Microsoft-Dokumentation](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about).
* Informationen zum programmgesteuerten Herstellen einer Verbindung mit [!DNL Azure Event Hubs] finden Sie im Lehrgang [Streaming-Ziel-API](../../api/streaming-destinations.md).
* Informationen zum Herstellen einer Verbindung mit [!DNL Azure Event Hubs] mithilfe der Plattform-Benutzeroberfläche finden Sie in den folgenden Abschnitten.

![AWS Kinesis in der Benutzeroberfläche](../../assets/catalog/cloud-storage/event-hubs/catalog.png)

## Nutzungsszenarien {#use-cases}

Durch die Verwendung von Streaming-Zielen wie [!DNL Azure Event Hubs] können Sie einfach hochwertige Segmentierungssysteme und zugehörige Profil-Attribute in Ihre bevorzugten Ereignis einspeisen.

Beispielsweise hat ein Potenzieller Kunde ein White Paper heruntergeladen, das sie in ein &quot;hohes Konversionssegment&quot;einordnet. Wenn Sie das Segment zuordnen, in das der Potenzieller Kunde zum [!DNL Azure Event Hubs]-Ziel gehört, erhalten Sie dieses Ereignis in [!DNL Azure Event Hubs]. Dort können Sie einen Do-it-self-Ansatz verwenden und die Geschäftslogik über das Ereignis beschreiben, da Sie denken, dass dies am besten mit Ihren IT-Systemen im Unternehmen funktionieren würde.

## Exporttyp {#export-type}

**Profil-basiert** : Sie exportieren alle Segmentmitglieder zusammen mit den gewünschten Segmentfeldern (z. B.: E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm &quot;Attribute auswählen&quot;des Arbeitsablaufs für die  [Ziel-Aktivierung](../../ui/activate-destinations.md#select-attributes) ausgewählt.

## Ziel verbinden {#connect-destination}

Anweisungen zum Herstellen einer Verbindung mit Ihren Cloud-Datenspeicherung-Zielen, einschließlich [!DNL Azure Event Hubs], finden Sie unter [Arbeitsablauf für Cloud-Datenspeicherung-Ziele ](./workflow.md).

Geben Sie für [!DNL Azure Event Hubs]-Ziele im Arbeitsablauf zum Erstellen von Zielen die folgenden Informationen ein:

## Authentifizierungsschritt {#authentication-step}

* **[!UICONTROL SAS-Key-]** Namen und  **[!UICONTROL SAS-Schlüssel]**: Geben Sie den Namen und die Taste Ihres SAS-Schlüssels ein. Erfahren Sie mehr über die Authentifizierung für [!DNL Azure Event Hubs] mit SAS-Schlüsseln in der [Microsoft-Dokumentation](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL Namensraum]**: Füllen Sie Ihren  [!DNL Azure Event Hubs] Namensraum aus. Erfahren Sie mehr über die [!DNL Azure Event Hubs]-Namensraum in der [Microsoft-Dokumentation](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).

![Im Authentifizierungsschritt erforderliche Eingabe](../../assets/catalog/cloud-storage/event-hubs/authentication.png)

## Setup-Schritt {#setup-step}

* **[!UICONTROL Name]**: Geben Sie einen Namen für die Verbindung ein  [!DNL Azure Event Hubs].
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung der Verbindung ein.  Beispiele: &quot;Premium-Tier-Kunden&quot;, &quot;Männer, die am Kitesurfen interessiert sind&quot;.
* **[!UICONTROL eventHubName]**: Geben Sie einen Namen für den Stream zu Ihrem  [!DNL Azure Event Hubs] Ziel ein.
* **[!UICONTROL Marketingaktionen]**: Marketingaktionen geben die Absicht an, für die Daten an das Ziel exportiert werden. Sie können aus von der Adobe definierten Marketingaktionen auswählen oder eine eigene Marketingaktion erstellen. Weitere Informationen zu Marketingaktionen finden Sie auf der Seite [Datenverwaltung in Adobe Experience Platform](../../../data-governance/policies/overview.md). Informationen zu den einzelnen, von der Adobe definierten Marketingaktionen finden Sie unter [Übersicht über Datenverwendungsrichtlinien](../../../data-governance/policies/overview.md).

![Im Setup-Schritt erforderliche Daten](../../assets/catalog/cloud-storage/event-hubs/setup.png)

## Aktivieren von Segmenten {#activate-segments}

Informationen zum Workflow für die Segmentaktivierung finden Sie unter [Profile und Segmente für ein Ziel aktivieren](../../ui/activate-destinations.md).

## Exportierte Daten {#exported-data}

Ihre exportierten [!DNL Experience Platform]-Daten landen im JSON-Format. [!DNL Azure Event Hubs] Das folgende Ereignis enthält beispielsweise das Segmentattribut &quot;E-Mail-Adresse&quot;einer Audience, die sich für ein bestimmtes Profil qualifiziert und ein anderes Segment verlassen hat. Die Identitäten für diesen Potenzieller Kunde sind ECID und E-Mail.

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
>* [Stellen Sie eine Verbindung zu den Ereignis-Hubs her und aktivieren Sie Daten mithilfe der Flow Service API](../../api/streaming-destinations.md)
>* [AWS Kinesis-Ziel](./amazon-kinesis.md)
>* [Zieltypen und Kategorien](../../destination-types.md)

