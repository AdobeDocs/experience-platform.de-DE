---
keywords: Amazon Kinesis; Kinesis-Ziel; Kinesis
title: Amazon Kinesis-Verbindung
description: Erstellen Sie eine ausgehende Echtzeitverbindung zu Ihrem Amazon Kinesis-Speicher, um Daten von Adobe Experience Platform zu streamen.
exl-id: b40117ef-6ad0-48a9-bbcb-97c6f6d1dce3
source-git-commit: 4febcef82c6da4534051cbe68820984814786224
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 5%

---

# (Beta) [!DNL Amazon Kinesis] Verbindung

## Übersicht {#overview}

>[!IMPORTANT]
>
>Das [!DNL Amazon Kinesis]-Ziel in Platform befindet sich derzeit in der Betaphase. Die Dokumentation und Funktionalität können sich ändern.

Mit dem Dienst [!DNL Kinesis Data Streams] von [!DNL Amazon Web Services] können Sie große Datenströme von Datensätzen in Echtzeit erfassen und verarbeiten.

Sie können eine ausgehende Echtzeitverbindung zu Ihrem [!DNL Amazon Kinesis]-Speicher erstellen, um Daten von Adobe Experience Platform zu streamen.

* Weitere Informationen zu [!DNL Amazon Kinesis] finden Sie in der [Amazon-Dokumentation](https://docs.aws.amazon.com/streams/latest/dev/introduction.html).
* Informationen zum programmgesteuerten Herstellen einer Verbindung zu [!DNL Amazon Kinesis] finden Sie im [Tutorial zur Streaming-Ziel-API](../../api/streaming-destinations.md).
* Informationen zum Herstellen einer Verbindung zu [!DNL Amazon Kinesis] mithilfe der Benutzeroberfläche von Platform finden Sie in den folgenden Abschnitten.

![Amazon Kinesis in der Benutzeroberfläche](../../assets/catalog/cloud-storage/amazon-kinesis/catalog.png)

## Nutzungsszenarien {#use-cases}

Durch die Verwendung von Streaming-Zielen wie [!DNL Amazon Kinesis] können Sie einfach hochwertige Segmentierungsereignisse und zugehörige Profilattribute in Ihre bevorzugten Systeme einspeisen.

Beispielsweise hat ein Interessent ein Whitepaper heruntergeladen, das ihn in ein Segment mit hoher Konversionsneigung qualifiziert. Wenn Sie das Segment zuordnen, in das der Interessent zum [!DNL Amazon Kinesis]-Ziel gehört, erhalten Sie dieses Ereignis in [!DNL Amazon Kinesis]. Dort können Sie zusätzlich zu dem Ereignis einen &quot;do-it-self&quot;-Ansatz verwenden und die Geschäftslogik beschreiben, da Sie denken, dass dies am besten mit Ihren Enterprise-IT-Systemen funktionieren würde.

## Exporttyp {#export-type}

**Profilbasiert**  - Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B.: E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm &quot;Attribute auswählen&quot;des  [Zielaktivierungs-Workflows](../../ui/activate-destinations.md#select-attributes) ausgewählt.

## Erforderliche [!DNL Amazon Kinesis] Berechtigungen {#required-kinesis-permission}

Um Daten erfolgreich mit [!DNL Amazon Kinesis]-Streams zu verbinden und zu exportieren, benötigt Experience Platform Berechtigungen für die folgenden Aktionen:

* `kinesis:ListStreams`
* `kinesis:PutRecord`
* `kinesis:PutRecords`

Diese Berechtigungen werden über die Konsole [!DNL Kinesis] angeordnet und von Platform überprüft, sobald Sie Ihr Kinesis-Ziel in der Benutzeroberfläche von Platform konfigurieren.

Im folgenden Beispiel werden die Mindestzugriffsrechte angezeigt, die erforderlich sind, um Daten erfolgreich an ein [!DNL Kinesis]-Ziel zu exportieren.

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
| `kinesis:ListStreams` | Eine Aktion, die Ihre Amazon Kinesis-Datenströme auflistet. |
| `kinesis:PutRecord` | Eine Aktion, die einen einzelnen Datensatz in einen Kinesis-Datenstrom schreibt. |
| `kinesis:PutRecords` | Eine Aktion, die mehrere Datendatensätze in einen Kinesis-Datenstrom in einem einzelnen Aufruf schreibt. |

Weitere Informationen zum Steuern des Zugriffs für [!DNL Kinesis]-Datenströme finden Sie im folgenden [[!DNL Kinesis] Dokument](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

## Ziel verbinden {#connect-destination}

Anweisungen zum Herstellen einer Verbindung mit Ihren Cloud-Speicher-Zielen, einschließlich der von [!DNL Amazon] unterstützten Ziele, finden Sie unter [Workflow für Cloud-Speicher ](./workflow.md).

Geben Sie für [!DNL Amazon Kinesis]-Ziele im Workflow &quot;Ziel erstellen&quot;die folgenden Informationen ein:

## Kontoschritt {#account-step}

* **[!DNL Amazon Web Services]Zugriffsschlüssel und geheimer Schlüssel**: Generieren Sie  [!DNL Amazon Web Services]in ein  `access key - secret access key` Paar, um Platform Zugriff auf Ihr  [!DNL Amazon Kinesis] Konto zu gewähren. Weitere Informationen finden Sie in der [Dokumentation zu Amazon Web Services](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **region**: Geben Sie an, zu welcher  [!DNL Amazon Web Services] Region Daten gestreamt werden sollen.

![Eingabefelder im Kontoschritt](../../assets/catalog/cloud-storage/amazon-kinesis/account.png)

## Authentifizierungsschritt {#authentication-step}

* **Name**: Geben Sie einen Namen für Ihre Verbindung an  [!DNL Amazon Kinesis]
* **Beschreibung**: Geben Sie eine Beschreibung für Ihre Verbindung zu  [!DNL Amazon Kinesis]an.
* **stream**: Geben Sie den Namen eines vorhandenen Datenstreams in Ihrem  [!DNL Amazon Kinesis] Konto an. Platform exportiert Daten in diesen Stream.
* **[!UICONTROL Marketing-Aktionen]**: Marketing-Aktionen geben die Absicht an, für die Daten an das Ziel exportiert werden. Sie können aus von der Adobe definierten Marketing-Aktionen auswählen oder eine eigene Marketing-Aktion erstellen. Weitere Informationen zu Marketing-Aktionen finden Sie auf der Seite [Data Governance in Adobe Experience Platform](../../../data-governance/policies/overview.md) . Informationen zu den einzelnen von der Adobe definierten Marketing-Aktionen finden Sie unter [Übersicht über Datennutzungsrichtlinien](../../../data-governance/policies/overview.md).

![Eingabefelder im Authentifizierungsschritt](../../assets/catalog/cloud-storage/amazon-kinesis/authentication.png)

<!--

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Aktivieren von Segmenten {#activate-segments}

Informationen zum Workflow für die Segmentaktivierung finden Sie unter [Profile und Segmente für ein Ziel aktivieren](../../ui/activate-destinations.md).

## Exportierte Daten {#exported-data}

Ihre exportierten [!DNL Experience Platform]-Daten werden im JSON-Format [!DNL Amazon Kinesis] angezeigt. Beispielsweise enthält das nachstehende Ereignis das E-Mail-Adressen-Profilattribut einer Zielgruppe, die sich für ein bestimmtes Segment qualifiziert und ein anderes Segment verlassen hat. Die Identitäten für diesen Interessenten sind ECID und E-Mail.

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
>* [Verbindung zu Amazon Kinesis herstellen und Daten mithilfe der Flow Service-API aktivieren](../../api/streaming-destinations.md)
* [Azure Event Hub-Ziel](./azure-event-hubs.md)
* [Zieltypen und Kategorien](../../destination-types.md)

