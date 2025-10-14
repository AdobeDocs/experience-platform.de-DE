---
keywords: Azure Event Hub-Ziel;Azure Event Hub;Azure Event Hub
title: Azure Event Hubs-Verbindung
description: Stellen Sie eine ausgehende Echtzeit-Verbindung zu Ihrem - [!DNL Azure Event Hubs]  her, um Daten von Experience Platform zu streamen.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: f98a389a-bce3-4a80-9452-6c7293d01de3
source-git-commit: d0ee4b30716734b8fce3509a6f3661dfa572cc9f
workflow-type: tm+mt
source-wordcount: '2212'
ht-degree: 45%

---

# [!DNL Azure Event Hubs]-Verbindung

## Übersicht {#overview}

>[!IMPORTANT]
>
> Dieses Ziel ist nur für Kunden von [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform.html) verfügbar.

[!DNL Azure Event Hubs] ist eine Big-Data-Streaming-Plattform und ein Service zur Ereignisaufnahme. Es kann Millionen von Ereignissen pro Sekunde empfangen und verarbeiten. Daten, die an einen Ereignis-Hub gesendet werden, können mithilfe eines beliebigen Echtzeit-Analyseanbieters oder Batch-/Speicheradapters transformiert und gespeichert werden.

Sie können eine ausgehende Echtzeit-Verbindung zu Ihrem [!DNL Azure Event Hubs]-Speicher herstellen, um Daten von Adobe Experience Platform zu streamen.

* Weitere Informationen zu [!DNL Azure Event Hubs] finden Sie in der [Dokumentation zu Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about).
* Informationen zum programmgesteuerten Herstellen einer Verbindung zu [!DNL Azure Event Hubs] finden Sie im [Tutorial zur Streaming-Ziele-API](../../api/streaming-destinations.md).
* Informationen zum Verbinden von mit [!DNL Azure Event Hubs] über die Benutzeroberfläche von Experience Platform finden Sie in den folgenden Abschnitten.

![AWS Kinesis in der Benutzeroberfläche](../../assets/catalog/cloud-storage/event-hubs/catalog.png)

## Anwendungsfälle {#use-cases}

Durch die Verwendung von Streaming-Zielen wie [!DNL Azure Event Hubs] können Sie einfach hochwertige Segmentierungsereignisse und zugehörige Profilattribute in Ihre gewünschten Systeme einspeisen.

Ein potenzieller Kunde hat beispielsweise ein Whitepaper heruntergeladen, in dem er in ein Segment mit einer hohen Konversionsneigung eingestuft wird. Wenn Sie die Zielgruppe, zu der der Interessent gehört, dem [!DNL Azure Event Hubs] Ziel zuordnen, erhalten Sie dieses Ereignis in [!DNL Azure Event Hubs]. Dort können Sie einen Do-it-yourself-Ansatz verwenden und zusätzlich zur Veranstaltung die Geschäftslogik beschreiben, die Ihrer Meinung nach am besten mit Ihren Unternehmens-IT-Systemen funktionieren würde.

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Arten von Zielgruppen Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die über den Experience Platform-[&#x200B; (Segmentierungs-Service) generiert &#x200B;](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/audience-portal.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B. E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm „Auswählen der Profilattribute“ im [Zielaktivierungs-Workflow](../../ui/activate-batch-profile-destinations.md#select-attributes) festgelegt. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Zulassungsliste von IP-Adressen {#ip-address-allowlist}

Um die Sicherheits- und Compliance-Anforderungen von Kundinnen und Kunden zu erfüllen, stellt Experience Platform auf die Zulassungsliste setzen eine Liste mit statischen IPs bereit, die Sie für das [!DNL Azure Event Hubs]-Ziel auswählen können. Siehe [Zulassungsliste von IP-Adressen für Streaming-Ziele](/help/destinations/catalog/streaming/ip-address-allow-list.md), um die vollständige Liste der IP-Adressen in der Zulassungsliste einzusehen.

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung mit dem Ziel herzustellen, benötigen Sie **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Beim Herstellen einer Verbindung zu diesem Ziel müssen Sie die folgenden Informationen angeben:

### Authentifizierungsinformationen {#authentication-information}

#### Standardauthentifizierung {#standard-authentication}

![Abbildung des Bildschirms der Benutzeroberfläche mit ausgefüllten Feldern für die Standardauthentifizierungsdetails von Azure Event Hubs](../../assets/catalog/cloud-storage/event-hubs/event-hubs-standard-authentication.png)

Wenn Sie den Typ **[!UICONTROL Standardauthentifizierung]** für die Verbindung mit Ihrem HTTP-Endpunkt auswählen, füllen Sie die unten stehenden Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]**:

* **[!UICONTROL SAS-Schlüsselname]**: Der Name der Autorisierungsregel, auch als SAS-Schlüsselname bezeichnet.
* **[!UICONTROL SAS-Schlüssel]** Der Primärschlüssel des Event Hubs-Namespace. Die `sasPolicy`, der die `sasKey` entspricht, müssen **Verwalten**-Rechte konfiguriert haben, damit die Event Hubs-Liste ausgefüllt wird. Erfahren Sie mehr über die Authentifizierung bei [!DNL Azure Event Hubs] mit SAS-Schlüsseln in der [Dokumentation zu Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL Namespace]**: Füllen Sie Ihren [!DNL Azure Event Hubs]-Namespace aus. Weitere Informationen zu [!DNL Azure Event Hubs]-Namespaces finden Sie in der [Dokumentation zu Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).

#### SAS-Authentifizierung (Shared Access Signature) {#sas-authentication}

![Abbildung des Bildschirms der Benutzeroberfläche mit ausgefüllten Feldern für die Standardauthentifizierungsdetails von Azure Event Hubs](../../assets/catalog/cloud-storage/event-hubs/event-hubs-sas-authentication.png)

Wenn Sie den Typ **[!UICONTROL Standardauthentifizierung]** für die Verbindung mit Ihrem HTTP-Endpunkt auswählen, füllen Sie die unten stehenden Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]**:

* **[!UICONTROL SAS-Schlüsselname]**: Der Name der Autorisierungsregel, auch als SAS-Schlüsselname bezeichnet.
* **[!UICONTROL SAS-Schlüssel]** Der Primärschlüssel des Event Hubs-Namespace. Die `sasPolicy`, der die `sasKey` entspricht, müssen **Verwalten**-Rechte konfiguriert haben, damit die Event Hubs-Liste ausgefüllt wird. Erfahren Sie mehr über die Authentifizierung bei [!DNL Azure Event Hubs] mit SAS-Schlüsseln in der [Dokumentation zu Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL Namespace]**: Füllen Sie Ihren [!DNL Azure Event Hubs]-Namespace aus. Weitere Informationen zu [!DNL Azure Event Hubs]-Namespaces finden Sie in der [Dokumentation zu Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).
* **[!UICONTROL Event Hub-Name]**: Geben Sie Ihren [!DNL Azure Event Hub] ein. Erfahren Sie mehr über [!DNL Azure Event Hubs] Namen in der [Dokumentation zu Microsoft](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub).

### Ausfüllen der Zieldetails {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_eventhubs_includesegmentnames"
>title="Segmentnamen einschließen"
>abstract="Schalten Sie diese Option ein, wenn der Datenexport die Namen der zu exportierenden Zielgruppen enthalten soll. In der Dokumentation finden Sie ein Beispiel für einen Datenexport mit dieser Option."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_eventhubs_includesegmenttimestamps"
>title="Zeitstempel für Segmente einschließen"
>abstract="Schalten Sie diese Option ein, wenn der Datenexport den UNIX-Zeitstempel enthalten soll, an dem die Zielgruppen erstellt und aktualisiert wurden, sowie den UNIX-Zeitstempel, an dem die Zielgruppen dem Ziel für die Aktivierung zugeordnet wurden. In der Dokumentation finden Sie ein Beispiel für einen Datenexport mit dieser Option."

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

![Abbildung des Bildschirms der Benutzeroberfläche mit ausgefüllten Feldern für die Zieldetails der Azure Event Hubs](../../assets/catalog/cloud-storage/event-hubs/event-hubs-destination-details.png)

* **[!UICONTROL Name]**: Geben Sie einen Namen für die zu [!DNL Azure Event Hubs] Verbindung ein.
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung der Verbindung an.  Beispiele: „Premium-Kunden“, „Kunden, die sich für Kitesurfen interessieren“.
* **[!UICONTROL eventHubName]**: Geben Sie einen Namen für den Stream zu Ihrem [!DNL Azure Event Hubs] Ziel an.
* **[!UICONTROL Segmentnamen einschließen]**: Schalten Sie diese Option ein, wenn der Datenexport die Namen der zu exportierenden Zielgruppen enthalten soll. Ein Beispiel für einen Datenexport, bei dem diese Option aktiviert ist, finden Sie im Abschnitt [Exportierte Daten](#exported-data) weiter unten.
* **[!UICONTROL Segmentzeitstempel einschließen]**: Schalten Sie diese Option ein, wenn der Datenexport den UNIX-Zeitstempel enthalten soll, an dem die Zielgruppen erstellt und aktualisiert wurden, sowie den UNIX-Zeitstempel, an dem die Zielgruppen dem Ziel für die Aktivierung zugeordnet wurden. Ein Beispiel für einen Datenexport, bei dem diese Option aktiviert ist, finden Sie im Abschnitt [exportierte Daten](#exported-data) weiter unten.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Zum Aktivieren von Daten benötigen Sie die Berechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**&#x200B;[Zugriffssteuerung](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* [Bewertung der Einverständnisrichtlinie](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) wird derzeit nicht in Exporten zum Azure Event Hubs-Ziel unterstützt. [Weitere Informationen](/help/destinations/ui/activate-streaming-profile-destinations.md#consent-policy-evaluation).

Anweisungen [&#x200B; Aktivieren von Zielgruppen für dieses Ziel finden Sie &#x200B;](../../ui/activate-streaming-profile-destinations.md) „Aktivieren von Zielgruppendaten für Streaming Profilexportziele“.

## Profilexportverhalten {#profile-export-behavior}

Experience Platform optimiert das Verhalten beim Profilexport für Ihr [!DNL Azure Event Hubs] Ziel, sodass nur Daten an Ihr Ziel exportiert werden, wenn relevante Profilaktualisierungen nach der Zielgruppenqualifizierung oder anderen wichtigen Ereignissen durchgeführt wurden. Profile werden in den folgenden Situationen an Ihr Ziel exportiert:

* Die Aktualisierung des Profils wurde durch eine Änderung der Zielgruppenzugehörigkeit für mindestens eine der dem Ziel zugeordneten Zielgruppen bestimmt. Beispielsweise hat sich das Profil für eine der Zielgruppen qualifiziert, die dem Ziel zugeordnet sind, oder es hat eine der dem Ziel zugeordneten Zielgruppen verlassen.
* Die Aktualisierung des Profils wurde durch eine Änderung der [Identitätszuordnung](/help/xdm/field-groups/profile/identitymap.md) bestimmt. Beispielsweise wurde einem Profil, das sich bereits für eine der dem Ziel zugeordneten Zielgruppen qualifiziert hatte, eine neue Identität im Identitätszuordnungsattribut hinzugefügt.
* Die Aktualisierung des Profils wurde durch eine Änderung der Attribute für mindestens eines der dem Ziel zugeordneten Attribute bestimmt. Beispielsweise wird eines der Attribute, die dem Ziel im Zuordnungsschritt zugeordnet sind, einem Profil hinzugefügt.

In allen oben beschriebenen Fällen werden nur die Profile exportiert, in denen relevante Aktualisierungen vorgenommen wurden. Wenn beispielsweise eine Zielgruppe, die dem Zielfluss zugeordnet ist, aus hundert Mitgliedern besteht und fünf neue Profile sich für das Segment qualifizieren, ist der Export in Ihr Ziel inkrementell und umfasst nur die fünf neuen Profile.

Beachten Sie, dass alle zugeordneten Attribute unabhängig vom Speicherort der Änderungen für ein Profil exportiert werden. Daher werden im obigen Beispiel alle zugeordneten Attribute für diese fünf neuen Profile exportiert, selbst wenn sich die Attribute selbst nicht geändert haben.

### Was bestimmt einen Datenexport und was ist im Export enthalten? {#what-determines-export-what-is-included}

Was die Daten betrifft, die für ein bestimmtes Profil exportiert werden, ist es wichtig, die beiden verschiedenen Konzepte zu verstehen, nämlich *was den Datenexport an Ihr [!DNL Azure Event Hubs]-Ziel bestimmt* und *welche Daten im Export enthalten sind*.

| Was einen Zielexport bestimmt | Im Zielexport enthaltene Informationen |
|---------|----------|
| <ul><li>Zugeordnete Attribute und Segmente dienen als Hinweis für einen Zielexport. Das bedeutet, dass ein Zielexport gestartet wird, wenn sich der `segmentMembership` eines Profils in `realized` oder `exiting` ändert oder zugeordnete Attribute aktualisiert werden.</li><li>Da Identitäten derzeit nicht [!DNL Azure Event Hubs] Zielen zugeordnet werden können, bestimmen Änderungen an der Identität eines bestimmten Profils auch die Zielexporte.</li><li>Als Änderung für ein Attribut wird jede Aktualisierung des Attributs definiert, unabhängig davon, ob es sich um denselben Wert handelt oder nicht. Das bedeutet, dass das Überschreiben eines Attributs als Änderung gilt, selbst wenn sich der Wert selbst nicht geändert hat.</li></ul> | <ul><li>**Hinweis**: Das Exportverhalten für Azure Event Hubs-Ziele wurde mit der Version vom September 2025 aktualisiert. Das unten hervorgehobene neue Verhalten gilt derzeit nur für neue Azure Event Hubs-Ziele, die nach dieser Version erstellt wurden. Bei bestehenden Azure Event Hubs-Zielen können Sie weiterhin das alte Exportverhalten verwenden oder Adobe kontaktieren, um zu dem neuen Verhalten zu migrieren, in dem nur zugeordnete Zielgruppen exportiert werden. Alle Organisationen werden 2026 schrittweise auf das neue Verhalten umgestellt. <br><br> <span class="preview"> **Neues Exportverhalten**: Die Segmente, die dem Ziel zugeordnet sind und sich geändert haben, werden in das segmentMembership-Objekt aufgenommen. In einigen Szenarien können sie mit mehreren Aufrufen exportiert werden. In einigen Szenarien können auch bestimmte Segmente, die sich nicht geändert haben, in den Aufruf eingeschlossen werden. In jedem Fall werden nur Segmente exportiert, die im Datenfluss zugeordnet sind.</span></li><br>**Altes Verhalten**: Das `segmentMembership` enthält das Segment, das im Aktivierungsdatenfluss zugeordnet ist und für das sich der Status des Profils nach einem Qualifikations- oder Segmentaustrittsereignis geändert hat. Andere nicht zugeordnete Segmente, für die sich das Profil qualifiziert hat, können Teil des Zielexports sein, wenn diese Segmente zu derselben [Zusammenführungsrichtlinie](/help/profile/merge-policies/overview.md) wie das im Aktivierungsdatenfluss zugeordnete Segment gehören. <li>Alle Identitäten im `identityMap` Objekt sind ebenfalls enthalten (Experience Platform unterstützt derzeit keine Identitätszuordnung im [!DNL Azure Event Hubs]).</li><li>Nur die zugeordneten Attribute werden in den Zielexport einbezogen.</li></ul> |

{style="table-layout:fixed"}

>[!BEGINSHADEBOX]

Betrachten Sie beispielsweise diesen Datenfluss zu einem [!DNL Azure Event Hubs] Ziel, bei dem drei Zielgruppen im Datenfluss ausgewählt sind und dem Ziel vier Attribute zugeordnet sind.

![Ziel-Datenfluss von Amazon Kinesis](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Ein Profilexport an das Ziel kann durch ein Profil bestimmt werden, das sich für eines der *drei zugeordneten Segmente* qualifiziert. Im Datenexport können im `segmentMembership` (siehe [Exportierte Daten](#exported-data) Abschnitt unten) weitere zugeordnete Zielgruppen angezeigt werden, wenn dieses bestimmte Profil zu diesen Profil gehört und diese Zielgruppen dieselbe Zusammenführungsrichtlinie verwenden wie die Zielgruppe, die den Export ausgelöst hat. Wenn ein Profil sich für das Segment **Kunde mit DeLorean-**) qualifiziert und auch Mitglied der Segmente **Grundlegende Site-Aktivität und Stadt - Dallas** ist, sind diese beiden anderen Zielgruppen ebenfalls im `segmentMembership` des Datenexports vorhanden, da diese im Datenfluss zugeordnet sind, falls diese dieselbe Zusammenführungsrichtlinie wie das Segment **Kunde mit DeLorean-Autos** verwenden.

Aus Sicht der Profilattribute bestimmen alle Änderungen an den vier oben zugeordneten Attributen einen Zielexport, und eines der vier im Profil vorhandenen zugeordneten Attribute wird im Datenexport vorhanden sein.

>[!ENDSHADEBOX]

## Aufstockung historischer Daten {#historical-data-backfill}

Wenn Sie eine neue Zielgruppe zu einem vorhandenen Ziel hinzufügen oder wenn Sie ein neues Ziel erstellen und diesem Zielgruppen zuordnen, exportiert Experience Platform historische Zielgruppen-Qualifizierungsdaten an das Ziel. Profile, die sich für die Zielgruppe qualifiziert haben *zuvor* wurde die Zielgruppe zum Ziel hinzugefügt, werden innerhalb von etwa einer Stunde an das Ziel exportiert.

## Exportierte Daten {#exported-data}

Ihre exportierten [!DNL Experience Platform]-Daten landen in Ihrem [!DNL Azure Event Hubs]-Ziel im JSON-Format. Beispielsweise enthält der folgende Export ein Profil, das sich für ein bestimmtes Segment qualifiziert hat, Mitglied zweier weiterer Segmente ist und ein weiteres Segment verlassen hat. Der Export umfasst außerdem Vorname, Nachname, Geburtsdatum und persönliche E-Mail-Adresse des Profilattributs. Die Identitäten für dieses Profil sind ECID und E-Mail.

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

+++ Das folgende Beispiel für den Datenexport enthält Zielgruppennamen im Abschnitt `segmentMembership` .

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

+++ Das folgende Beispiel für den Datenexport enthält Zielgruppen-Zeitstempel im Abschnitt `segmentMembership` .

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
>* [Verbinden mit Azure Event Hubs und Aktivieren von Daten mithilfe der Flow Service-API](../../api/streaming-destinations.md)
>* [AWS Kinesis-Ziel](./amazon-kinesis.md)
>* [Zieltypen und Kategorien](../../destination-types.md)
