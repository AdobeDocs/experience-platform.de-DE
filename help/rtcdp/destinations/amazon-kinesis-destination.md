---
title: Amazon-Kinesis-Ziel
seo-title: Amazon-Kinesis-Ziel
description: Erstellen Sie eine ausgehende Echtzeitverbindung zu Ihrer Amazon-Kinesis-Datenspeicherung, um Daten von Adobe Experience Platform zu streamen.
seo-description: Erstellen Sie eine ausgehende Echtzeitverbindung zu Ihrer Amazon-Kinesis-Datenspeicherung, um Daten von Adobe Experience Platform zu streamen.
translation-type: tm+mt
source-git-commit: a18f89531cf024f61b054b47a660bd26766bebf6
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 5%

---


# Amazon-Kinesis-Ziel

## Übersicht {#overview}

Mit dem [!DNL Kinesis Data Streams] Dienst von Amazon Web Services können Sie große Datenströme in Echtzeit erfassen und verarbeiten.

Sie können eine ausgehende Echtzeitverbindung zu Ihrer [!DNL Amazon Kinesis] Datenspeicherung erstellen, um Daten von Adobe Experience Platform zu streamen.

* Weitere Informationen finden Sie [!DNL Amazon Kinesis]in der [Amazon-Dokumentation](https://docs.aws.amazon.com/streams/latest/dev/introduction.html).
* Informationen zum Herstellen einer Verbindung mit [!DNL Amazon Kinesis] API-Aufrufen finden Sie im [Streaming-Ziel-API-Lernprogramm].
* Informationen zum Herstellen einer Verbindung mit der [!DNL Amazon Kinesis] CDP-Benutzeroberfläche von Adobe in Echtzeit finden Sie in den folgenden Abschnitten.

![Amazon-Kinesis in der Benutzeroberfläche](/help/rtcdp/destinations/assets/aws-kinesis-destination.png)


## Nutzungsszenarien {#use-cases}

Durch die Verwendung von Streaming-Zielen wie Amazon Kinesis können Sie einfach hochwertige Segmentierungssysteme und zugehörige Profil-Attribute in Ihre bevorzugten Ereignis einspeisen.

Beispielsweise hat ein Potenzieller Kunde ein White Paper heruntergeladen, das sie in ein &quot;hohes Konversionssegment&quot;einordnet. Durch Zuordnung des Segments, in das der Potenzieller Kunde zum Amazon Kinesis-Ziel fällt, erhalten Sie dieses Ereignis in Amazon Kinesis. Dort können Sie einen Do-it-self-Ansatz verwenden und die Geschäftslogik über das Ereignis beschreiben, da Sie denken, dass dies am besten mit Ihren IT-Systemen im Unternehmen funktionieren würde.

## Ziel verbinden {#connect-destination}

See [Cloud storage destinations workflow ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)for instructions on how to connect to your cloud storage destinations, including those supported by [!DNL Amazon].

For [!DNL Amazon Kinesis] destinations, enter the following information in the create destination workflow:

### Im Kontoschritt {#account-step}

* **Zugriffsschlüssel und geheimer Schlüssel** für Amazon Web Services: Generieren Sie in [!DNL Amazon Web Services]diesem Fall einen Zugriffsschlüssel - ein Schlüssel-Paar für den geheimen Zugriff, um Adobe CDP-Zugriff auf Ihr [!DNL Amazon Kinesis] Konto zu gewähren. Weitere Informationen finden Sie in der Dokumentation zu [Amazon Web Services](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **Region**: Geben Sie an, zu welcher [!DNL Amazon Web Services] Region Daten gestreamt werden sollen.

![Eingabefelder im Kontoschritt](/help/rtcdp/destinations/assets/aws-kinesis-account-step.png)

### Im Authentifizierungsschritt {#authentication-step}

* **Name**: Geben Sie einen Namen für Ihre Verbindung ein, um [!DNL Amazon Kinesis]
* **Beschreibung**: Geben Sie eine Beschreibung für Ihre Verbindung ein [!DNL Amazon Kinesis].
* **stream**: Geben Sie den Namen Ihres vorhandenen Datenstroms in Ihrem [!DNL Amazon Kinesis] Konto an. Adobe Echtzeit-CDP exportiert Daten in diesen Stream.

![Eingabefelder im Authentifizierungsschritt](/help/rtcdp/destinations/assets/aws-kinesis-authentication-step.png)

<!--

>[!IMPORTANT]
>
>Adobe Real-time CDP needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Aktivieren von Segmenten {#activate-segments}

Informationen zum Workflow für die Segmentaktivierung finden Sie unter [Profile und Segmente für ein Ziel aktivieren](/help/rtcdp/destinations/activate-destinations.md).

## Exportierte Daten {#exported-data}

Ihre exportierten Experience Platform-Daten werden im JSON- [!DNL Amazon Kinesis] Format gespeichert. Ein Ereignis mit der Hash-E-Mail-Identität einer Audience, die ein bestimmtes Segment verlassen hat, könnte z. B. wie folgt aussehen:

```
{
   "segmentMembership":{
      "ups":{
         "7841ba61-23c1-4bb3-a495-00d695fe1e93":{
            "lastQualificationTime":"2020-03-03T21:24:39Z",
            "status":"exited"
         }
      }
   }
},
"identityMap":{
   "email_lc_sha256":[
      {
         "id":"655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
         "id":"66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
   ]
},
```



>[!MORELIKETHIS]
>
>* Link zum Amazon Kinesis API-Lernprogramm
>* [Azurblauer Ereignis Hubs Ziel](/help/rtcdp/destinations/azure-event-hubs-destination.md)
>* [Zieltypen und Kategorien](/help/rtcdp/destinations/destination-types.md)

