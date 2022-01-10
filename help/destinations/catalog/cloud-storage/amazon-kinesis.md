---
keywords: Amazon Kinesis; Kinesis-Ziel; Kinesis
title: Amazon Kinesis-Verbindung
description: Erstellen Sie eine ausgehende Echtzeitverbindung zu Ihrem Amazon Kinesis-Speicher, um Daten von Adobe Experience Platform zu streamen.
exl-id: b40117ef-6ad0-48a9-bbcb-97c6f6d1dce3
source-git-commit: ba338972be13c7afa6720bba3f0fc96d244b8f9f
workflow-type: tm+mt
source-wordcount: '835'
ht-degree: 2%

---

# (Beta) [!DNL Amazon Kinesis] connection

## Übersicht {#overview}

>[!IMPORTANT]
>
>Die [!DNL Amazon Kinesis] Das Ziel in Platform befindet sich derzeit in der Beta-Phase. Die Dokumentation und Funktionalität können sich ändern.

Die [!DNL Kinesis Data Streams] von [!DNL Amazon Web Services] ermöglicht die Erfassung und Verarbeitung großer Datenströme in Echtzeit.

Sie können eine ausgehende Echtzeitverbindung zu Ihrem [!DNL Amazon Kinesis] Speicher zum Streamen von Daten aus Adobe Experience Platform.

* Weitere Informationen finden Sie unter [!DNL Amazon Kinesis], siehe [Amazon-Dokumentation](https://docs.aws.amazon.com/streams/latest/dev/introduction.html).
* Verbindung herstellen zu [!DNL Amazon Kinesis] sehen Sie programmatisch die [Tutorial zur Streaming-Ziele-API](../../api/streaming-destinations.md).
* Verbindung herstellen zu [!DNL Amazon Kinesis] Informationen zur Verwendung der Benutzeroberfläche von Platform finden Sie in den folgenden Abschnitten.

![Amazon Kinesis in der Benutzeroberfläche](../../assets/catalog/cloud-storage/amazon-kinesis/catalog.png)

## Anwendungsfälle {#use-cases}

Durch Verwendung von Streaming-Zielen wie [!DNL Amazon Kinesis]können Sie einfach hochwertige Segmentierungsereignisse und zugehörige Profilattribute in Ihre bevorzugten Systeme einspeisen.

Beispielsweise hat ein Interessent ein Whitepaper heruntergeladen, das ihn in ein Segment mit hoher Konversionsneigung qualifiziert. Durch Zuordnung des Segments, in das der Interessent fällt, zum [!DNL Amazon Kinesis] Ziel, erhalten Sie dieses Ereignis in [!DNL Amazon Kinesis]. Dort können Sie zusätzlich zu dem Ereignis einen &quot;do-it-self&quot;-Ansatz verwenden und die Geschäftslogik beschreiben, da Sie denken, dass dies am besten mit Ihren Enterprise-IT-Systemen funktionieren würde.

## Exporttyp {#export-type}

**Profilbasiert** - Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B.: E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm &quot;Attribute auswählen&quot;der [Zielgruppenaktivierungs-Workflow](../../ui/activate-streaming-profile-destinations.md#select-attributes).

## Erforderlich [!DNL Amazon Kinesis] Berechtigungen {#required-kinesis-permission}

So verbinden Sie Daten erfolgreich mit Ihren [!DNL Amazon Kinesis] -Streams, benötigt Experience Platform Berechtigungen für die folgenden Aktionen:

* `kinesis:ListStreams`
* `kinesis:PutRecord`
* `kinesis:PutRecords`

Diese Berechtigungen werden über die [!DNL Kinesis] und werden von Platform überprüft, sobald Sie Ihr Kinesis-Ziel in der Benutzeroberfläche von Platform konfigurieren.

Im folgenden Beispiel werden die Mindestzugriffsrechte angezeigt, die erforderlich sind, um Daten erfolgreich in eine [!DNL Kinesis] Ziel.

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

Weitere Informationen zur Zugriffskontrolle für [!DNL Kinesis] Datenströme, lesen Sie Folgendes [[!DNL Kinesis] Dokument](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

## Mit Ziel verbinden {#connect}

Gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md).

### Verbindungsparameter {#parameters}

while [Einrichten](../../ui/connect-destination.md) An diesem Ziel müssen Sie die folgenden Informationen angeben:

* **[!DNL Amazon Web Services]Zugriffsschlüssel und geheimer Schlüssel**: In [!DNL Amazon Web Services], generieren Sie eine `access key - secret access key` , um Platform Zugriff auf Ihre [!DNL Amazon Kinesis] -Konto. Weitere Informationen finden Sie unter [Amazon Web Services-Dokumentation](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **region**: Geben Sie an, [!DNL Amazon Web Services] Region, an die Daten gestreamt werden sollen.
* **Name**: Geben Sie einen Namen für Ihre Verbindung an [!DNL Amazon Kinesis]
* **Beschreibung**: Geben Sie eine Beschreibung für Ihre Verbindung zu [!DNL Amazon Kinesis].
* **stream**: Geben Sie den Namen eines vorhandenen Datenstreams in Ihrer [!DNL Amazon Kinesis] -Konto. Platform exportiert Daten in diesen Stream.

<!--

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Aktivieren von Segmenten für dieses Ziel {#activate}

Siehe [Aktivieren von Zielgruppendaten für Streaming-Profil-Export-Ziele](../../ui/activate-streaming-profile-destinations.md) für Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel.

## Profil-Exportverhalten {#profile-export-behavior}

Experience Platform optimiert das Profil-Exportverhalten für Ihr Amazon Kinesis-Ziel, sodass Daten nur dann an Ihr Ziel exportiert werden, wenn relevante Profilaktualisierungen aufgrund einer Segmentqualifikation oder anderer wichtiger Ereignisse vorgenommen wurden. Profile werden in den folgenden Situationen an Ihr Ziel exportiert:

* Das Profil-Update wurde durch eine Änderung der Segmentzugehörigkeit für mindestens eines der dem Ziel zugeordneten Segmente ausgelöst. Beispielsweise hat sich das Profil für eines der Segmente qualifiziert, die dem Ziel zugeordnet sind, oder eines der dem Ziel zugeordneten Segmente verlassen.
* Das Profil-Update wurde durch eine Änderung der [Identitätszuordnung](/help/xdm/field-groups/profile/identitymap.md). Beispielsweise wurde einem Profil, das sich bereits für eines der dem Ziel zugeordneten Segmente qualifiziert hatte, eine neue Identität im Identitätszuordnungsattribut hinzugefügt.
* Das Profil-Update wurde durch eine Änderung der Attribute für mindestens eines der dem Ziel zugeordneten Attribute ausgelöst. Beispielsweise wird eines der Attribute, die dem Ziel im Zuordnungsschritt zugeordnet sind, einem Profil hinzugefügt.

In allen oben beschriebenen Fällen werden nur die Profile exportiert, in denen relevante Aktualisierungen vorgenommen wurden. Wenn beispielsweise ein Segment, das dem Zielfluss zugeordnet ist, aus hundert Mitgliedern besteht und fünf neue Profile für das Segment qualifiziert sind, ist der Export in Ihr Ziel inkrementell und umfasst nur die fünf neuen Profile.

Beachten Sie, dass alle zugeordneten Attribute unabhängig vom Speicherort der Änderungen für ein Profil exportiert werden. Daher werden im Beispiel vor allem alle zugeordneten Attribute für diese fünf neuen Profile exportiert, selbst wenn sich die Attribute selbst nicht geändert haben.

## Exportierte Daten {#exported-data}

Ihr exportiert [!DNL Experience Platform] landet in [!DNL Amazon Kinesis] im JSON-Format. Der folgende Export enthält beispielsweise ein Profil, das sich für ein bestimmtes Segment qualifiziert und ein anderes Segment verlassen hat, und das das Profilattribut mit Vorname, Nachname, Geburtsdatum und persönlicher E-Mail-Adresse enthält. Die Identitäten für dieses Profil sind ECID und E-Mail.

```json
{
  "person": {
    "birthDate": "YYYY-MM-DD",
    "name": {
      "firstName": "John",
      "lastName": "Doe"
    }
  },
  "personalEmail": {
    "address": "john.doe@acme.com"
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
>* [Azure Event Hub-Ziel](./azure-event-hubs.md)
>* [Zieltypen und Kategorien](../../destination-types.md)

