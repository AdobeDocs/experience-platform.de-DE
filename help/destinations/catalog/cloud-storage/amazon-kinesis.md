---
keywords: Amazon Kinesis; Kinesis-Ziel; Kinesis
title: Amazon Kinesis-Verbindung
description: Erstellen Sie eine ausgehende Echtzeitverbindung zu Ihrem Amazon Kinesis-Speicher, um Daten von Adobe Experience Platform zu streamen.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: b40117ef-6ad0-48a9-bbcb-97c6f6d1dce3
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '1984'
ht-degree: 54%

---

# [!DNL Amazon Kinesis]-Verbindung

## Übersicht {#overview}

>[!IMPORTANT]
>
> Dieses Ziel ist nur für Kunden von [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform.html) verfügbar.

Die [!DNL Kinesis Data Streams] Dienst von [!DNL Amazon Web Services] ermöglicht die Erfassung und Verarbeitung großer Datenströme in Echtzeit.

Sie können eine ausgehende Echtzeitverbindung zu Ihrem [!DNL Amazon Kinesis] Speicher zum Streamen von Daten aus Adobe Experience Platform.

* Weitere Informationen finden Sie unter [!DNL Amazon Kinesis], siehe [Amazon-Dokumentation](https://docs.aws.amazon.com/streams/latest/dev/introduction.html).
* So stellen Sie eine Verbindung her [!DNL Amazon Kinesis] sehen Sie programmatisch die [Tutorial zur Streaming-Ziele-API](../../api/streaming-destinations.md).
* So stellen Sie eine Verbindung her [!DNL Amazon Kinesis] Informationen zur Verwendung der Benutzeroberfläche von Platform finden Sie in den folgenden Abschnitten.

![Amazon Kinesis in der Benutzeroberfläche](../../assets/catalog/cloud-storage/amazon-kinesis/catalog.png)

## Anwendungsfälle {#use-cases}

Durch Verwendung von Streaming-Zielen wie [!DNL Amazon Kinesis]können Sie einfach hochwertige Segmentierungsereignisse und zugehörige Profilattribute in Ihre bevorzugten Systeme einspeisen.

Beispielsweise hat ein Interessent ein Whitepaper heruntergeladen, das ihn in ein Segment mit hoher Konversionsneigung qualifiziert. Durch Zuordnung der Zielgruppe, in die der Interessent fällt, zum [!DNL Amazon Kinesis] Ziel, erhalten Sie dieses Ereignis in [!DNL Amazon Kinesis]. Dort können Sie zusätzlich zu dem Ereignis einen &quot;do-it-self&quot;-Ansatz verwenden und die Geschäftslogik beschreiben, da Sie denken, dass dies am besten mit Ihren Enterprise-IT-Systemen funktionieren würde.

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Zielgruppentypen Sie an dieses Ziel exportieren können.

| Audience Origin | Unterstützt | Beschreibung |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Über die Experience Platform generierte Zielgruppen [Segmentierungsdienst](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/overview.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B. E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm „Auswählen der Profilattribute“ im [Zielaktivierungs-Workflow](../../ui/activate-batch-profile-destinations.md#select-attributes) festgelegt. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Zulassungsliste von IP-Adressen {#ip-address-allowlist}

Um die Sicherheits- und Compliance-Anforderungen von Kunden zu erfüllen, stellt Experience Platform eine Liste statischer IPs bereit, die Sie für die [!DNL Amazon Kinesis] Ziel. Siehe [Zulassungsliste von IP-Adressen für Streaming-Ziele](/help/destinations/catalog/streaming/ip-address-allow-list.md), um die vollständige Liste der IP-Adressen in der Zulassungsliste einzusehen.

## Erforderliche [!DNL Amazon Kinesis]-Berechtigungen {#required-kinesis-permission}

So verbinden Sie Daten erfolgreich mit Ihren [!DNL Amazon Kinesis] -Streams, Experience Platform benötigt Berechtigungen für die folgenden Aktionen:

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

{style="table-layout:auto"}

Weitere Informationen zur Zugriffskontrolle für [!DNL Kinesis] Datenströme, lesen Sie Folgendes [[!DNL Kinesis] Dokument](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Beim Herstellen einer Verbindung zu diesem Ziel müssen Sie die folgenden Informationen angeben:

### Authentifizierungsinformationen {#authentication-information}

Füllen Sie die Felder unten aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]**:

![Bild des UI-Bildschirms mit ausgefüllten Feldern für die Authentifizierungsdetails der Amazon Kinesis](../../assets/catalog/cloud-storage/amazon-kinesis/kinesis-authentication-fields.png)

* **[!DNL Amazon Web Services]Zugriffsschlüssel und geheimer Schlüssel**: In [!DNL Amazon Web Services], generieren Sie eine `access key - secret access key` , um Platform Zugriff auf Ihre [!DNL Amazon Kinesis] -Konto. Weitere Informationen finden Sie in der [Amazon Web Services-Dokumentation](https://docs.aws.amazon.com/de_de/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL Region]**: Geben Sie an, welche [!DNL Amazon Web Services] region zum Streamen von Daten an.

### Ausfüllen der Zieldetails {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_kinesis_includesegmentnames"
>title="Segmentnamen einschließen"
>abstract="Schalten Sie diese Option ein, wenn der Datenexport die Namen der zu exportierenden Zielgruppen enthalten soll. In der Dokumentation finden Sie ein Beispiel für einen Datenexport mit dieser Option."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_kinesis_includesegmenttimestamps"
>title="Zeitstempel für Segmente einschließen"
>abstract="Schalten Sie diese Option ein, wenn der Datenexport den UNIX-Zeitstempel enthalten soll, an dem die Zielgruppen erstellt und aktualisiert wurden, sowie den UNIX-Zeitstempel, an dem die Zielgruppen dem Ziel für die Aktivierung zugeordnet wurden. In der Dokumentation finden Sie ein Beispiel für einen Datenexport mit dieser Option."

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

![Bild des UI-Bildschirms mit ausgefüllten Feldern für die Zieldetails von Amazon Kinesis](../../assets/catalog/cloud-storage/amazon-kinesis/kinesis-destination-details.png)

* **[!UICONTROL Name]**: Geben Sie einen Namen für Ihre Verbindung zu [!DNL Amazon Kinesis]
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung für Ihre Verbindung zu [!DNL Amazon Kinesis].
* **[!UICONTROL Stream]**: Geben Sie den Namen eines vorhandenen Datenstreams in Ihrer [!DNL Amazon Kinesis] -Konto. Platform exportiert Daten in diesen Stream.
* **[!UICONTROL Segmentnamen einschließen]**: Schalten Sie ein, wenn der Datenexport die Namen der Zielgruppen enthalten soll, die exportiert werden sollen. Ein Beispiel für einen Datenexport, bei dem diese Option aktiviert ist, finden Sie im Abschnitt [Exportierte Daten](#exported-data) weiter unten.
* **[!UICONTROL Segmentzeitstempel einschließen]**: Schalten Sie ein, wenn der Datenexport zum Zeitpunkt der Erstellung und Aktualisierung der Zielgruppen den UNIX-Zeitstempel sowie den UNIX-Zeitstempel enthalten soll, zu dem die Zielgruppen zur Aktivierung dem Ziel zugeordnet wurden. Ein Beispiel für einen Datenexport, bei dem diese Option aktiviert ist, finden Sie im Abschnitt [exportierte Daten](#exported-data) weiter unten.

<!--

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Anzeigen von Profilen]**, und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* [Beurteilung der Einwilligungsrichtlinie](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) wird derzeit beim Export in das Amazon Kinesis-Ziel nicht unterstützt. [Weitere Informationen](/help/destinations/ui/activate-streaming-profile-destinations.md#consent-policy-evaluation).

Siehe [Aktivieren von Zielgruppendaten für Streaming-Profil-Export-Ziele](../../ui/activate-streaming-profile-destinations.md) für Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel.

## Profilexportverhalten {#profile-export-behavior}

Experience Platform optimiert das Profil-Exportverhalten für Ihre [!DNL Amazon Kinesis] Ziel, um Daten nur dann an Ihr Ziel zu exportieren, wenn nach der Zielgruppenqualifizierung oder anderen wichtigen Ereignissen relevante Aktualisierungen an einem Profil stattgefunden haben. Profile werden in den folgenden Situationen an Ihr Ziel exportiert:

* Die Aktualisierung des Profils wurde durch eine Änderung der Zielgruppenzugehörigkeit für mindestens eine der Zielgruppen bestimmt. Beispielsweise hat sich das Profil für eine der Zielgruppen qualifiziert, die dem Ziel zugeordnet sind, oder es hat eine der dem Ziel zugeordneten Zielgruppen verlassen.
* Die Aktualisierung des Profils wurde durch eine Änderung der [Identitätszuordnung](/help/xdm/field-groups/profile/identitymap.md) bestimmt. Beispielsweise wurde einem Profil, das sich bereits für eine der dem Ziel zugeordneten Zielgruppen qualifiziert hatte, eine neue Identität im Identitätszuordnungsattribut hinzugefügt.
* Die Aktualisierung des Profils wurde durch eine Änderung der Attribute für mindestens eines der dem Ziel zugeordneten Attribute bestimmt. Beispielsweise wird eines der Attribute, die dem Ziel im Zuordnungsschritt zugeordnet sind, einem Profil hinzugefügt.

In allen oben beschriebenen Fällen werden nur die Profile exportiert, in denen relevante Aktualisierungen vorgenommen wurden. Wenn beispielsweise eine Zielgruppe, die dem Zielfluss zugeordnet ist, aus hundert Mitgliedern besteht und fünf neue Profile sich für das Segment qualifizieren, ist der Export in Ihr Ziel inkrementell und umfasst nur die fünf neuen Profile.

Beachten Sie, dass alle zugeordneten Attribute unabhängig vom Speicherort der Änderungen für ein Profil exportiert werden. Daher werden im obigen Beispiel alle zugeordneten Attribute für diese fünf neuen Profile exportiert, selbst wenn sich die Attribute selbst nicht geändert haben.

### Was bestimmt einen Datenexport und was ist im Export enthalten? {#what-determines-export-what-is-included}

Für die Daten, die für ein bestimmtes Profil exportiert werden, ist es wichtig, die beiden verschiedenen Konzepte von *was den Datenexport für Ihre [!DNL Amazon Kinesis] Ziel* und *welche Daten im Export enthalten sind*.

| Was einen Zielexport bestimmt | Im Zielexport enthaltene Informationen |
|---------|----------|
| <ul><li>Zugeordnete Attribute und Zielgruppen dienen als Hinweis für einen Zielexport. Das bedeutet, dass ein Zielexport ausgelöst wird, wenn sich der Status einer zugeordneten Zielgruppe ändert (von `null` auf `realized` oder von `realized` auf `exiting`) oder wenn zugeordnete Attribute aktualisiert werden.</li><li>Da Identitäten derzeit nicht zugeordnet werden können [!DNL Amazon Kinesis] Ziele, Änderungen an einer Identität in einem bestimmten Profil bestimmen auch die Zielexporte.</li><li>Als Änderung für ein Attribut wird jede Aktualisierung des Attributs definiert, unabhängig davon, ob es sich um denselben Wert handelt oder nicht. Das bedeutet, dass das Überschreiben eines Attributs als Änderung gilt, selbst wenn sich der Wert selbst nicht geändert hat.</li></ul> | <ul><li>Das `segmentMembership`-Objekt enthält die Zielgruppe, die im Aktivierungsdatenfluss zugeordnet ist und für die sich der Status des Profils nach einem Qualifikations- oder Zielgruppenaustrittsereignis geändert hat. Beachten Sie, dass andere nicht zugeordnete Zielgruppen, für die sich das Profil qualifiziert hat, Teil des Zielexports sein können, wenn diese Zielgruppen zu derselben [Zusammenführungsrichtlinie](/help/profile/merge-policies/overview.md) gehören wie die im Aktivierungsdatenfluss zugeordnete Zielgruppe. </li><li>Alle Identitäten in der `identityMap` -Objekt wird ebenfalls einbezogen (Experience Platform unterstützt derzeit keine Identitätszuordnung in der [!DNL Amazon Kinesis] Ziel).</li><li>Nur die zugeordneten Attribute werden in den Zielexport einbezogen.</li></ul> |

{style="table-layout:fixed"}

Betrachten Sie diesen Datenfluss beispielsweise als [!DNL Amazon Kinesis] Ziel, bei dem im Datenfluss drei Zielgruppen ausgewählt und dem Ziel vier Attribute zugeordnet sind.

![Amazon Kinesis-Ziel-Datenfluss](../../assets/catalog/http/profile-export-example-dataflow.png)

Ein Profilexport an das Ziel kann durch ein Profil bestimmt werden, das sich für eines der *drei zugeordneten Segmente* qualifiziert. Im Datenexport jedoch wird im `segmentMembership` -Objekt (siehe [Exportierte Daten](#exported-data) unten), können weitere nicht zugeordnete Zielgruppen angezeigt werden, wenn dieses bestimmte Profil Mitglied dieser Zielgruppe ist und diese dieselbe Zusammenführungsrichtlinie wie die Zielgruppe nutzen, die den Export ausgelöst hat. Wenn ein Profil für die **Kunde mit DeLorean Cars** Zielgruppe, aber auch Mitglied der **&quot;Zurück in die Zukunft&quot;** Film und **Fans von Science-Fiction** Zielgruppen verwenden, sind diese beiden anderen Zielgruppen auch in der `segmentMembership` -Objekt des Datenexports, auch wenn diese nicht im Datenfluss zugeordnet sind, wenn diese dieselbe Zusammenführungsrichtlinie mit der **Kunde mit DeLorean Cars** Segment.

Aus Sicht der Profilattribute bestimmen alle Änderungen an den vier oben zugeordneten Attributen einen Zielexport, und eines der vier im Profil vorhandenen zugeordneten Attribute wird im Datenexport vorhanden sein.

## Aufstockung historischer Daten {#historical-data-backfill}

Wenn Sie eine neue Zielgruppe zu einem vorhandenen Ziel hinzufügen oder wenn Sie ein neues Ziel erstellen und ihm Zielgruppen zuordnen, exportiert Experience Platform historische Zielgruppenqualifizierungsdaten an das Ziel. Profile, die sich für die Zielgruppe qualifiziert haben *before* die Zielgruppe, die zum Ziel hinzugefügt wurde, innerhalb von etwa einer Stunde an das Ziel exportiert werden.

## Exportierte Daten {#exported-data}

Ihre exportierten [!DNL Experience Platform]-Daten landen in Ihrem [!DNL Amazon Kinesis]-Ziel im JSON-Format. Beispielsweise enthält der folgende Export ein Profil, das sich für ein bestimmtes Segment qualifiziert hat, Mitglied zweier weiterer Segmente ist und ein weiteres Segment verlassen hat. Der Export umfasst außerdem Vorname, Nachname, Geburtsdatum und persönliche E-Mail-Adresse des Profilattributs. Die Identitäten für dieses Profil sind ECID und E-Mail.

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
         "status":"realized"
      },
      "947c1c46-008d-40b0-92ec-3af86eaf41c1":{
         "lastQualificationTime":"2021-08-25T23:37:33Z",
         "status":"realized"
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

Im Folgenden finden Sie weitere Beispiele für exportierte Daten, abhängig von den Benutzeroberflächeneinstellungen, die Sie im Fluss „Ziel verbinden“ für die Optionen **[!UICONTROL Segmentnamen einschließen]** und **[!UICONTROL Zeitstempel für Segmente einschließen]** auswählen.

+++ Im folgenden Beispiel für den Datenexport finden Sie Zielgruppennamen im `segmentMembership` Abschnitt

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "realized",
            "createdAt": 1648553325000,
            "updatedAt": 1648553330000,
            "mappingCreatedAt": 1649856570000,
            "mappingUpdatedAt": 1649856570000,
            "name": "First name equals John"
          }
        }
      }
```

+++

+++ Das folgende Beispiel für den Datenexport enthält Zeitstempel der Zielgruppe im `segmentMembership` Abschnitt

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "realized",
            "createdAt": 1648553325000,
            "updatedAt": 1648553330000,
            "mappingCreatedAt": 1649856570000,
            "mappingUpdatedAt": 1649856570000,
          }
        }
      }
```

+++

## Beschränkungen und Wiederholungsrichtlinien {#limits-retry-policy}

Experience Platform versucht, in 95 Prozent der Fälle eine Durchsatzlatenz von weniger als 10 Minuten für erfolgreich gesendete Nachrichten mit einer Rate von weniger als 10.000 Anfragen pro Sekunde für jeden Datenfluss an ein HTTP-Ziel zu bieten.

Bei fehlgeschlagenen Anfragen an Ihr HTTP-API-Ziel speichert Experience Platform die fehlgeschlagenen Anfragen und versucht es zweimal erneut, die Anfragen an Ihren Endpunkt zu senden.

>[!MORELIKETHIS]
>
>* [Verbindung zu Amazon Kinesis herstellen und Daten mithilfe der Flow Service-API aktivieren](../../api/streaming-destinations.md)
>* [Azure Event Hub-Ziel](./azure-event-hubs.md)
>* [Zieltypen und Kategorien](../../destination-types.md)
