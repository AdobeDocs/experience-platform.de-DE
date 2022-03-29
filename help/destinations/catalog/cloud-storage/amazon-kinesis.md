---
keywords: Amazon Kinesis; Kinesis-Ziel; Kinesis
title: (Beta) Amazon Kinesis-Verbindung
description: Erstellen Sie eine ausgehende Echtzeitverbindung zu Ihrem Amazon Kinesis-Speicher, um Daten von Adobe Experience Platform zu streamen.
exl-id: b40117ef-6ad0-48a9-bbcb-97c6f6d1dce3
source-git-commit: b2ac26589527313ec9f3cf84126e3e23da6c7b83
workflow-type: tm+mt
source-wordcount: '1340'
ht-degree: 1%

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

## Exportart und -frequenz {#export-type-frequency}

Informationen zum Zielexporttyp und zur Häufigkeit finden Sie in der unten stehenden Tabelle.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B.: E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm Profilattribute im [Zielaktivierungs-Workflow](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind &quot;immer auf&quot;-API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Segmentbewertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Mehr dazu [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## IP-Adressen-Zulassungsliste {#ip-address-allowlist}

Um die Sicherheits- und Compliance-Anforderungen von Kunden zu erfüllen, bietet Experience Platform eine Liste statischer IPs, die Sie für die [!DNL Amazon Kinesis] Ziel. Siehe [IP-Adressen-Zulassungsliste für Streaming-Ziele](/help/destinations/catalog/streaming/ip-address-allow-list.md) für die vollständige Liste der IP-Adressen in Zulassungsliste.

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

Experience Platform optimiert das Exportverhalten von Profilen für Ihre [!DNL Amazon Kinesis] Ziel, um Daten nur dann an Ihr Ziel zu exportieren, wenn relevante Aktualisierungen an einem Profil nach der Segmentqualifizierung oder anderen wichtigen Ereignissen stattgefunden haben. Profile werden in den folgenden Situationen an Ihr Ziel exportiert:

* Die Aktualisierung des Profils wurde durch eine Änderung der Segmentzugehörigkeit für mindestens eines der dem Ziel zugeordneten Segmente bestimmt. Beispielsweise hat sich das Profil für eines der Segmente qualifiziert, die dem Ziel zugeordnet sind, oder eines der dem Ziel zugeordneten Segmente verlassen.
* Die Aktualisierung des Profils wurde durch eine Änderung der [Identitätszuordnung](/help/xdm/field-groups/profile/identitymap.md). Beispielsweise wurde einem Profil, das sich bereits für eines der dem Ziel zugeordneten Segmente qualifiziert hatte, eine neue Identität im Identitätszuordnungsattribut hinzugefügt.
* Die Aktualisierung des Profils wurde durch eine Änderung der Attribute für mindestens eines der dem Ziel zugeordneten Attribute bestimmt. Beispielsweise wird eines der Attribute, die dem Ziel im Zuordnungsschritt zugeordnet sind, einem Profil hinzugefügt.

In allen oben beschriebenen Fällen werden nur die Profile exportiert, in denen relevante Aktualisierungen vorgenommen wurden. Wenn beispielsweise ein Segment, das dem Zielfluss zugeordnet ist, aus hundert Mitgliedern besteht und fünf neue Profile für das Segment qualifiziert sind, ist der Export in Ihr Ziel inkrementell und umfasst nur die fünf neuen Profile.

Beachten Sie, dass alle zugeordneten Attribute unabhängig vom Speicherort der Änderungen für ein Profil exportiert werden. Daher werden im Beispiel vor allem alle zugeordneten Attribute für diese fünf neuen Profile exportiert, selbst wenn sich die Attribute selbst nicht geändert haben.

### Was bestimmt einen Datenexport und was ist im Export enthalten? {#what-determines-export-what-is-included}

Für die Daten, die für ein bestimmtes Profil exportiert werden, ist es wichtig, die beiden verschiedenen Konzepte von *was den Datenexport für Ihre [!DNL Amazon Kinesis] Ziel* und *welche Daten im Export enthalten sind*.

| Was bestimmt den Zielexport? | Im Zielexport enthaltene Informationen |
|---------|----------|
| <ul><li>Zugeordnete Attribute und Segmente dienen als Hinweis für einen Zielexport. Das bedeutet, dass ein Zielexport gestartet wird, wenn zugeordnete Segmente den Status ändern (von null zu realisiert oder von realisiert/existiert zu ausstieg) oder alle zugeordneten Attribute aktualisiert werden.</li><li>Da Identitäten derzeit nicht zugeordnet werden können [!DNL Amazon Kinesis] Ziele, Änderungen an einer Identität in einem bestimmten Profil bestimmen auch die Zielexporte.</li><li>Eine Änderung für ein Attribut wird als jede Aktualisierung des Attributs definiert, unabhängig davon, ob es sich um denselben Wert handelt oder nicht. Das bedeutet, dass eine Überschreiben eines Attributs als Änderung gilt, selbst wenn sich der Wert selbst nicht geändert hat.</li></ul> | <ul><li>Alle Segmente (mit dem aktuellen Mitgliedschaftsstatus), unabhängig davon, ob sie im Datenfluss zugeordnet sind oder nicht, werden im `segmentMembership` -Objekt.</li><li>Alle Identitäten in der `identityMap` -Objekt wird ebenfalls einbezogen (Experience Platform unterstützt derzeit keine Identitätszuordnung in der [!DNL Amazon Kinesis] Ziel).</li><li>Nur die zugeordneten Attribute werden in den Zielexport einbezogen.</li></ul> |

{style=&quot;table-layout:fixed&quot;}

Betrachten Sie diesen Datenfluss beispielsweise als [!DNL Amazon Kinesis] Ziel, bei dem im Datenfluss drei Segmente ausgewählt und dem Ziel vier Attribute zugeordnet sind.

![Amazon Kinesis-Ziel-Datenfluss](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Ein Profilexport an das Ziel kann durch ein Profil bestimmt werden, das für eines der *drei zugeordnete Segmente*. Im Datenexport jedoch wird im `segmentMembership` -Objekt (siehe [Exportierte Daten](#exported-data) unten), können weitere nicht zugeordnete Segmente angezeigt werden, wenn dieses bestimmte Profil Mitglied ist. Wenn ein Profil für den Kunden mit dem Segment &quot;DeLorean Cars&quot;qualifiziert ist, aber auch Mitglied der Segmente &quot;Zurück zur Zukunft&quot;für Film- und Science Fiction-Fans ist, sind diese beiden anderen Segmente auch in den Segmenten `segmentMembership` -Objekt des Datenexports, auch wenn diese nicht im Datenfluss zugeordnet sind.

Aus Sicht der Profilattribute bestimmen alle Änderungen an den vier oben zugeordneten Attributen einen Zielexport und eines der vier im Profil vorhandenen zugeordneten Attribute wird im Datenexport vorhanden sein.

## Exportierte Daten {#exported-data}

Ihr exportiert [!DNL Experience Platform] Daten landen in Ihrer [!DNL Amazon Kinesis] Ziel im JSON-Format. Beispielsweise enthält der unten stehende Export ein Profil, das sich für ein bestimmtes Segment qualifiziert hat, Mitglied weiterer zwei Segmente ist und ein weiteres Segment verlassen hat. Der Export umfasst auch das Profilattribut mit Vorname, Nachname, Geburtsdatum und persönlicher E-Mail-Adresse. Die Identitäten für dieses Profil sind ECID und E-Mail.

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
   "ups":{
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93":{
         "lastQualificationTime":"2022-01-11T21:24:39Z",
         "status":"exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae":{
         "lastQualificationTime":"2022-01-02T23:37:33Z",
         "status":"existing"
      },
      "947c1c46-008d-40b0-92ec-3af86eaf41c1":{
         "lastQualificationTime":"2021-08-25T23:37:33Z",
         "status":"existing"
      },
      "5114d758-ce71-43ba-b53e-e2a91d67b67f":{
         "lastQualificationTime":"2022-01-11T23:37:33Z",
         "status":"realized"
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

