---
title: (Beta) Azurblauer Ereignis Hubs-Ziel
seo-title: (Beta) Azurblauer Ereignis Hubs-Ziel
description: Erstellen Sie eine ausgehende Echtzeitverbindung zur Azurblauen Ereignis Hubs-Datenspeicherung, um Daten aus der Experience Platform zu streamen.
seo-description: Erstellen Sie eine ausgehende Echtzeitverbindung zur Azurblauen Ereignis Hubs-Datenspeicherung, um Daten aus der Experience Platform zu streamen.
translation-type: tm+mt
source-git-commit: e93bfc028d5e23c3add55677c4003ca549a902c6
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 6%

---


# (Beta) Azurblauer Ereignis Hubs-Ziel

>[!IMPORTANT]
>
>Das [!DNL Azure Event Hubs] Ziel in Adobe Echtzeit-CDP befindet sich derzeit in der Betaphase. Dokumentation und Funktionalität können sich ändern.

## Übersicht {#overview}

[!DNL Azure Event Hubs] ist eine große Datenstreaming-Plattform und ein Ereignis-Erfassungsdienst. Es kann Millionen von Ereignissen pro Sekunde empfangen und verarbeiten. Daten, die an einen Ereignis-Hub gesendet werden, können mithilfe eines beliebigen Echtzeitanalyseanbieters oder von Batch-/Datenspeicherung-Adaptern transformiert und gespeichert werden.

Sie können eine ausgehende Echtzeitverbindung zu Ihrer [!DNL Azure Event Hubs] Datenspeicherung erstellen, um Daten aus der Adobe Experience Platform zu streamen.

* Weitere Informationen finden Sie [!DNL Azure Event Hubs]in der [Microsoft-Dokumentation](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about).
* Informationen zum Herstellen einer Verbindung mit [!DNL Azure Event Hubs] API-Aufrufen finden Sie im [Streaming-Ziel-API-Lernprogramm](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md).
* Informationen zum Herstellen einer Verbindung mit der [!DNL Azure Event Hubs] CDP-Benutzeroberfläche von Adobe in Echtzeit finden Sie in den folgenden Abschnitten.

![AWS-Kinesis in der Benutzeroberfläche](/help/rtcdp/destinations/assets/azure-event-hubs-destination.png)

## Nutzungsszenarien {#use-cases}

Durch Streaming-Ziele wie beispielsweise Azurblase-Ereignis-Hubs können Sie hochwertige Segmentierungssysteme und zugehörige Profil-Attribute problemlos in Ihre bevorzugten Ereignis einspeisen.

Beispielsweise hat ein Potenzieller Kunde ein White Paper heruntergeladen, das sie in ein &quot;hohes Konversionssegment&quot;einordnet. Durch die Zuordnung des Segments, in das der Potenzieller Kunde in das Ereignis Hubs-Ziel des Azurblaus fällt, erhalten Sie dieses Ereignis in den Azurblauen Ereignis Hubs. Dort können Sie einen Do-it-self-Ansatz verwenden und die Geschäftslogik über das Ereignis beschreiben, da Sie denken, dass dies am besten mit Ihren IT-Systemen im Unternehmen funktionieren würde.

## Ziel verbinden {#connect-destination}

See [Cloud storage destinations workflow ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)for instructions on how to connect to your cloud storage destinations, including [!DNL Azure Event Hubs].

For [!DNL Azure Event Hubs] destinations, enter the following information in the create destination workflow:

### Im Authentifizierungsschritt {#authentication-step}

* **[!UICONTROL SAS-Schlüsselname]** und **[!UICONTROL SAS-Schlüssel]**: Geben Sie den Namen und die Taste Ihres SAS-Schlüssels ein. Informationen zur Authentifizierung mit [!DNL Azure Event Hubs] SAS-Schlüsseln finden Sie in der [Microsoft-Dokumentation](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL Namensraum]**: Füllen Sie Ihren [!DNL Azure Event Hubs] Namensraum aus. Informationen zu [!DNL Azure Event Hubs] Namensräumen finden Sie in der [Microsoft-Dokumentation](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).

![Im Authentifizierungsschritt erforderliche Eingabe](/help/rtcdp/destinations/assets/event-hubs-authentication.png)

### Im Setup-Schritt {#setup-step}

* **[!UICONTROL Name]**: Geben Sie einen Namen für die Verbindung ein [!DNL Azure Event Hubs].
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung der Verbindung ein.  Beispiele: &quot;Premium-Tier-Kunden&quot;, &quot;Männer, die am Kitesurfen interessiert sind&quot;.
* **[!UICONTROL eventHubName]**: Geben Sie einen Namen für den Stream zu Ihrem [!DNL Azure Event Hubs] Ziel ein.

![Im Setup-Schritt erforderliche Daten](/help/rtcdp/destinations/assets/event-hubs-setup-step.png)

## Aktivieren von Segmenten {#activate-segments}

Informationen zum Workflow für die Segmentaktivierung finden Sie unter [Profile und Segmente für ein Ziel aktivieren](/help/rtcdp/destinations/activate-destinations.md).


## Exportierte Daten {#exported-data}

Ihre exportierten Experience Platformen werden im JSON- [!DNL Azure Event Hubs] Format gespeichert. Das folgende Ereignis enthält beispielsweise das Segmentattribut &quot;E-Mail-Adresse&quot;einer Audience, die sich für ein bestimmtes Profil qualifiziert und ein anderes Segment verlassen hat. Die Identitäten für diesen Potenzieller Kunde sind ECID und E-Mail.

```
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
>* [Verbindung zu Azurblauen Ereignis-Hubs und Aktivierung von Daten mithilfe von API-Aufrufen](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md)
>* [AWS-Kinesis-Ziel](/help/rtcdp/destinations/amazon-kinesis-destination.md)
>* [Zieltypen und Kategorien](/help/rtcdp/destinations/destination-types.md)