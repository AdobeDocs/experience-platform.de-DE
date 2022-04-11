---
description: Mit dieser Konfiguration können Sie grundlegende Informationen wie Zielname, Kategorie, Beschreibung, Logo und mehr angeben. Die Einstellungen in dieser Konfiguration bestimmen auch, wie Experience Platform-Benutzer sich bei Ihrem Ziel authentifizieren, wie es in der Experience Platform-Benutzeroberfläche angezeigt wird und welche Identitäten an Ihr Ziel exportiert werden können.
title: Konfigurationsoptionen für Streaming-Ziele für das Destination SDK
exl-id: b7e4db67-2981-4f18-b202-3facda5c8f0b
source-git-commit: 51417bee5dba7a96d3a7a7eb507fc95711fad4a5
workflow-type: tm+mt
source-wordcount: '1787'
ht-degree: 98%

---

# Konfiguration des Streaming-Ziels {#destination-configuration}

## Übersicht {#overview}

Mit dieser Konfiguration können Sie wichtige Informationen für Ihr Streaming-Ziel angeben, z. B. Ihren Zielnamen, Ihre Kategorie, eine Beschreibung und mehr. Die Einstellungen in dieser Konfiguration bestimmen auch, wie Experience Platform-Benutzer sich bei Ihrem Ziel authentifizieren, wie es in der Experience Platform-Benutzeroberfläche angezeigt wird und welche Identitäten an Ihr Ziel exportiert werden können.

Diese Konfiguration verbindet auch die anderen Konfigurationen, die für das Funktionieren Ihres Ziels erforderlich sind (Ziel-Server und Zielgruppen-Metadaten), mit dieser Konfiguration. Wie Sie die beiden Konfigurationen referenzieren können, erfahren Sie in einem [Abschnitt weiter unten](./destination-configuration.md#connecting-all-configurations).

Sie können die in diesem Dokument beschriebenen Funktionen mithilfe des `/authoring/destinations`-API-Endpunkts konfigurieren. Eine vollständige Liste der Vorgänge, die Sie mit dem Endpunkt durchführen können, finden Sie unter [API-Endpunktvorgänge für Ziele](./destination-configuration-api.md).

## Beispiel für eine Streaming-Konfiguration {#example-configuration}

Dies ist eine Beispielkonfiguration des fiktiven Streaming-Ziels Moviestar, das Endpunkte an vier Orten auf der Welt hat. Das Ziel gehört zur Kategorie der mobilen Ziele.

```json
{
   "name":"Moviestar",
   "description":"Moviestar is a fictional destination, used for this example.",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ],
   "customerDataFields":[
      {
         "name":"endpointsInstance",
         "type":"string",
         "title":"Select Endpoint",
         "description":"Moviestar manages several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
         "isRequired":true,
         "enum":[
            "US",
            "EU",
            "APAC",
            "NZ"
         ]
      },
      {
         "name":"customerID",
         "type":"string",
         "title":"Moviestar Customer ID",
         "description":"Your customer ID in the Moviestar destination (e.g. abcdef).",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$"
      }
   ],
   "uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
               
            }
         }
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      }
   },
   "schemaConfig":{
      "profileRequired":false,
      "segmentRequired":true,
      "identityRequired":true
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
   "aggregation":{
      "aggregationType":"CONFIGURABLE_AGGREGATION",
      "configurableAggregation":{
         "splitUserById":true,
         "maxBatchAgeInSecs":2400,
         "maxNumEventsInBatch":5000,
         "aggregationKey":{
            "includeSegmentId":true,
            "includeSegmentStatus":true,
            "includeIdentity":true,
            "oneIdentityPerGroup":false,
            "groups":[
               {
                  "namespaces":[
                     "IDFA",
                     "GAID"
                  ]
               },
               {
                  "namespaces":[
                     "EMAIL"
                  ]
               }
            ]
         }
      }
   },
   "backfillHistoricalProfileData":true
}
```

| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `name` | Zeichenfolge | Gibt den Titel Ihres Ziels im Experience Platform-Katalog an. |
| `description` | Zeichenfolge | Geben Sie im Zielkatalog von Experience Platform eine Beschreibung für Ihre Zielkarte ein. Es sollten nicht mehr als 4–5 Sätze sein. |
| `status` | Zeichenfolge | Gibt den Lebenszyklusstatus der Zielkarte an. Zulässige Werte sind `TEST`, `PUBLISHED` und `DELETED`. Verwenden Sie `TEST`, wenn Sie Ihr Ziel zum ersten Mal konfigurieren. |

{style=&quot;table-layout:auto&quot;}

## Konfigurationen der Benutzerauthentifizierung {#customer-authentication-configurations}

Mit diesem Abschnitt in der Zielkonfiguration wird die Seite [Neues Ziel konfigurieren](/help/destinations/ui/connect-destination.md) in der Experience Platform-Benutzeroberfläche generiert, auf der Benutzer Experience Platform mit den Konten verbinden, die sie an Ihrem Ziel haben. Je nachdem, welche Authentifizierungsoption Sie im Feld `authType` angeben, wird die Experience Platform-Seite für die Benutzer folgendermaßen generiert:

### Bearer-Authentifizierung

Wenn Sie den Bearer-Authentifizierungstyp konfigurieren, müssen Benutzer das Bearer-Token eingeben, das sie von Ihrem Ziel erhalten.

![UI-Rendering mit Bearer-Authentifizierung](assets/bearer-authentication-ui.png)

### OAuth 2-Authentifizierung

Benutzer wählen **[!UICONTROL Mit Ziel verbinden]** aus, um den OAuth 2-Authentifizierungsfluss für Ihr Ziel auszulösen (siehe folgendes Beispiel für das Ziel „Twitter Custom Audiences“). Detaillierte Informationen zum Konfigurieren der OAuth 2-Authentifizierung für Ihren Ziel-Endpunkt finden Sie in der entsprechenden [Authentifizierungsseite für Destination SDK OAuth 2](./oauth2-authentication.md).

![UI-Rendering mit OAuth 2-Authentifizierung](assets/oauth2-authentication-ui.png)

| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `customerAuthenticationConfigurations` | Zeichenfolge | Gibt die Konfiguration an, die zum Authentifizieren von Experience Platform-Kunden auf Ihrem Server verwendet wird. Siehe `authType` unten für gültige Werte. |
| `authType` | Zeichenfolge | Zulässige Werte für Streaming-Ziele sind:<ul><li>`BEARER`. Wenn Ihr Ziel die Bearer-Authentifizierung unterstützt, legen Sie `"authType":"Bearer"` und `"authenticationRule":"CUSTOMER_AUTHENTICATION"` im [Zielbereitstellungs-Abschnitt](./destination-configuration.md) fest.</li><li>`OAUTH2`. Wenn Ihr Ziel die OAuth 2-Authentifizierung unterstützt, legen Sie `"authType":"OAUTH2"` fest und fügen Sie, wie auf der Seite zur [OAuth 2-Authentifizierung mit dem Destination SDK](./oauth2-authentication.md) beschrieben, die erforderlichen Felder für OAuth 2 hinzu. Wählen Sie außerdem `"authenticationRule":"CUSTOMER_AUTHENTICATION"` im [Zielbereitstellungs-Abschnitt](./destination-configuration.md).</li> |

{style=&quot;table-layout:auto&quot;}

## Benutzerdefinierte Datenfelder {#customer-data-fields}

Verwenden Sie diesen Abschnitt, um Benutzer aufzufordern, benutzerdefinierte Felder für Ihr Ziel auszufüllen, wenn sie in der Experience Platform-Benutzeroberfläche eine Verbindung zum Ziel herstellen. Die Konfiguration wird wie unten dargestellt im Authentifizierungsfluss sichtbar:

![Benutzerdefinierter Feldauthentifizierungsfluss](./assets/custom-field-authentication-flow.png)

| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `name` | Zeichenfolge | Geben Sie einen Namen für das benutzerdefinierte Feld ein, das Sie einführen. |
| `type` | Zeichenfolge | Gibt an, welchen Typ von benutzerdefiniertem Feld Sie einführen. Akzeptierte Werte sind `string`, `object`, `integer`. |
| `title` | Zeichenfolge | Gibt den Feldnamen an, wie er für den Kunden in der Experience Platform-Benutzeroberfläche angezeigt wird. |
| `description` | Zeichenfolge | Geben Sie eine Beschreibung für das benutzerdefinierte Feld ein. |
| `isRequired` | Boolesch | Gibt an, ob dieses Feld im Ziel-Setup-Workflow erforderlich ist. |
| `enum` | Zeichenfolge | Rendert das benutzerdefinierte Feld als Dropdown-Menü und listet die für den Benutzer verfügbaren Optionen auf. |
| `pattern` | Zeichenfolge | Erzwingt bei Bedarf ein Muster für das benutzerdefinierte Feld. Verwenden Sie reguläre Ausdrücke, um ein Muster zu erzwingen. Wenn Ihre Kunden-IDs beispielsweise keine Zahlen oder Unterstriche enthalten, geben Sie `^[A-Za-z]+$` in dieses Feld ein. |

{style=&quot;table-layout:auto&quot;}

## Benutzeroberflächenattribute {#ui-attributes}

Dieser Abschnitt bezieht sich auf die Benutzeroberflächenelemente in der obigen Konfiguration, die von Adobe für Ihr Ziel in der Adobe Experience Platform-Benutzeroberfläche verwendet werden sollte. Siehe unten:

| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `documentationLink` | Zeichenfolge | Weitere Informationen finden Sie auf der Dokumentationsseite im [Zielkatalog](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=de#catalog) für Ihr Ziel. Verwenden Sie `http://www.adobe.com/go/destinations-YOURDESTINATION-en`, wobei `YOURDESTINATION` für den Namen Ihres Ziels steht. Für ein Ziel mit dem Namen Moviestar würden Sie `http://www.adobe.com/go/destinations-moviestar-en` verwenden. |
| `category` | Zeichenfolge | Bezieht sich auf die Ihrem Ziel in Adobe Experience Platform zugewiesene Kategorie. Weitere Informationen finden Sie unter [Zielkategorien](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html?lang=de). Verwenden Sie einen der folgenden Werte: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. |
| `connectionType` | Zeichenfolge | `Server-to-server` ist derzeit die einzige verfügbare Option. |
| `frequency` | Zeichenfolge | Bezieht sich auf die Art des Datenexports, die vom Ziel unterstützt wird. Unterstützte Werte: <ul><li>`Streaming`</li><li>`Batch`</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Schemakonfiguration im Zuordnungsschritt {#schema-configuration}

![Zuordnungsschritt aktivieren](./assets/enable-mapping-step.png)

Verwenden Sie die Parameter in `schemaConfig`, um den Zuordnungsschritt des Zielaktivierungs-Workflows zu aktivieren. Mithilfe der unten beschriebenen Parameter können Sie bestimmen, ob Experience Platform-Benutzer Profilattribute und/oder Identitäten dem gewünschten Schema auf der Zielseite zuordnen können.

| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `profileFields` | Array | *Wird in der obigen Beispielkonfiguration nicht angezeigt.* Wenn Sie vordefinierte `profileFields` hinzufügen, können Experience Platform-Benutzer Platform-Attribute den vordefinierten Attributen auf der Zielseite zuordnen. |
| `profileRequired` | Boolesch | Verwenden Sie `true`, wenn Benutzer die Zuordnung von Profilattributen aus Experience Platform zu benutzerdefinierten Attributen des Ziels vornehmen dürfen, wie in der obigen Beispielkonfiguration dargestellt. |
| `segmentRequired` | Boolesch | Verwenden Sie immer `segmentRequired:true`. |
| `identityRequired` | Boolesch | Verwenden Sie `true`, wenn Benutzer in der Lage sein sollen, Identitäts-Namespaces von Experience Platform Ihrem gewünschten Schema zuzuordnen. |

{style=&quot;table-layout:auto&quot;}


## Identitäten und Attribute {#identities-and-attributes}

Die Parameter in diesem Abschnitt bestimmen, welche Identitäten Ihr Ziel akzeptiert. Durch diese Konfiguration werden auch die Zielidentitäten und -attribute im [Zuordnungsschritt](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) der Experience Platform-Benutzeroberfläche ausgefüllt, in dem Benutzer Identitäten und Attribute aus ihren XDM-Schemata dem Schema in Ihrem Ziel zuordnen.

Sie müssen angeben, welche [!DNL Platform]-Identitäten Kunden in Ihr Ziel exportieren können. Einige Beispiele: [!DNL Experience Cloud ID], gehashte E-Mail, Geräte-ID ([!DNL IDFA], [!DNL GAID]). Diese Werte sind Identitäts-Namespaces von [!DNL Platform], die Kunden von Ihrem Ziel aus Identitäts-Namespaces zuordnen können. Sie können auch angeben, ob Kunden die Möglichkeit haben, Identitäten, die von Ihrem Ziel unterstützt werden, benutzerdefinierte Namespaces zuzuordnen.

Identitäts-Namespaces erfordern keine 1:1-Korrespondenz zwischen [!DNL Platform] und Ihrem Ziel.
Kunden können beispielsweise einen [!DNL Platform]-[!DNL IDFA]-Namespace einem [!DNL IDFA]-Namespace in Ihrem Ziel zuordnen oder sie können denselben [!DNL Platform]-[!DNL IDFA]-Namespace einem [!DNL Customer ID]-Namespace in Ihrem Ziel zuordnen.

Mehr dazu in der [Übersicht über Identitäts-Namespaces](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=de).

![Rendern von Zielidentitäten in der Benutzeroberfläche](./assets/target-identities-ui.png)

| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `acceptsAttributes` | Boolesch | Gibt an, ob Ihr Ziel Standardprofilattribute akzeptiert. Normalerweise werden diese Attribute in der Dokumentation der Partner genannt. |
| `acceptsCustomNamespaces` | Boolesch | Gibt an, ob Kunden benutzerdefinierte Namespaces in Ihrem Ziel einrichten können. |
| `allowedAttributesTransformation` | Zeichenfolge | *Wird in der Beispielkonfiguration nicht angezeigt*. Wird beispielsweise verwendet, wenn der [!DNL Platform]-Kunde einfache E-Mail-Adressen als Attribut verwendet und Ihre Plattform nur gehashte E-Mails akzeptiert. In diesem Objekt können Sie die Transformation spezifizieren, die angewendet werden muss (z. B. E-Mail in Kleinbuchstaben umwandeln und dann hashen). Ein Beispiel finden Sie unter `requiredTransformation` in der [API-Referenz zur Zielkonfiguration](./destination-configuration-api.md#update). |
| `acceptedGlobalNamespaces` | – | Wird für Fälle verwendet, in denen Ihre Plattform [Standard-Identitäts-Namespaces](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=de#standard-namespaces) (z. B. IDFA) akzeptiert, sodass Sie Platform-Benutzer darauf beschränken können, nur diese Identitäts-Namespaces auszuwählen. |

{style=&quot;table-layout:auto&quot;}

## Zielbereitstellung {#destination-delivery}

| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `authenticationRule` | Zeichenfolge | Gibt an, wie [!DNL Platform]-Kunden eine Verbindung zu Ihrem Ziel herstellen. Akzeptierte Werte sind `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Verwenden Sie `CUSTOMER_AUTHENTICATION`, wenn sich Platform-Kunden über einen Benutzernamen und ein Kennwort, ein Träger-Token oder eine andere Authentifizierungsmethode bei Ihrem System anmelden. Sie würden diese Option beispielsweise auswählen, wenn Sie auch `authType: OAUTH2` oder `authType:BEARER` in `customerAuthenticationConfigurations` ausgewählt haben. </li><li> Verwenden Sie `PLATFORM_AUTHENTICATION`, wenn ein globales Authentifizierungssystem zwischen Adobe und Ihrem Ziel existiert und der [!DNL Platform]-Kunde keine Authentifizierungsdaten bereitstellen muss, um eine Verbindung zu Ihrem Ziel herzustellen. In diesem Fall müssen Sie ein Objekt für die [Anmeldeinformationen](./credentials-configuration-api.md) mithilfe der Konfiguration erstellen. </li><li>Verwenden Sie `NONE`, wenn keine Authentifizierung erforderlich ist, um Daten an Ihre Zielplattform zu senden. </li></ul> |
| `destinationServerId` | Zeichenfolge | Die `instanceId` der [Ziel-Server-Konfiguration](./destination-server-api.md), die für dieses Ziel verwendet wird. |

{style=&quot;table-layout:auto&quot;}

## Konfiguration der Segmentzuordnung {#segment-mapping}

![Abschnitt zur Konfiguration der Segmentzuordnung](./assets/segment-mapping-configuration.png)

Dieser Abschnitt der Zielkonfiguration bezieht sich darauf, wie Segmentmetadaten, etwa Segmentnamen oder IDs, zwischen Experience Platform und Ihrem Ziel freigegeben werden sollen.

Durch die `audienceTemplateId` verknüpft dieser Abschnitt diese Konfiguration auch mit der [Konfiguration von Zielgruppen-Metadaten](./audience-metadata-management.md).

Die in der obigen Konfiguration angezeigten Parameter werden im Abschnitt [Referenz für die Ziel-Endpunkt-API](./destination-configuration-api.md) beschrieben.

## Aggregationsrichtlinie {#aggregation}

![Aggregationsrichtlinie in der Konfigurationsvorlage](./assets/aggregation-configuration.png)

In diesem Abschnitt können Sie die Aggregationsrichtlinien festlegen, die Experience Platform beim Exportieren von Daten in Ihr Ziel verwenden soll.

Eine Aggregationsrichtlinie bestimmt, wie die exportierten Profile in den Datenexporten kombiniert werden. Verfügbare Optionen sind:
* Best-Effort-Aggregation
* Konfigurierbare Aggregation (siehe Konfiguration oben)

Lesen Sie den Abschnitt über die [Verwendung von Vorlagen](./message-format.md#using-templating) und die [Aggregations-Beispiele](./message-format.md#template-aggregation-key), um zu verstehen, wie Sie die Aggregationsrichtlinie basierend auf Ihrer ausgewählten Aggregationsrichtlinie in Ihre Nachrichten-Umwandlungsvorlage einschließen.

### Best-Effort-Aggregation {#best-effort-aggregation}

>[!TIP]
>
>Verwenden Sie diese Option, wenn Ihr API-Endpunkt weniger als 100 Profile pro API-Aufruf akzeptiert.

Diese Option eignet sich am besten für Ziele, die weniger Profile pro Anfrage bevorzugen und lieber mehr Anfragen mit weniger Daten als weniger Anfragen mit mehr Daten hätten.

Geben Sie über den Parameter `maxUsersPerRequest` die maximale Anzahl der Profile an, die Ihr Ziel in einer Anfrage aufnehmen kann.

### Konfigurierbare Aggregation {#configurable-aggregation}

Diese Option eignet sich am besten, wenn Sie im selben Aufruf große Batches mit Tausenden Profilen verwenden möchten. Mit dieser Option können Sie die exportierten Profile auch anhand komplexer Aggregationsregeln aggregieren.

Diese Option ermöglicht Ihnen Folgendes:
* Legen Sie vor einem eines API-Aufruf an Ihr Ziel die maximale Zeit und die maximale Anzahl von Profilen fest, die aggregiert werden sollen.
* Aggregieren Sie die exportierten, dem Ziel zugeordneten Profile anhand folgender Kriterien:
   * Segment-ID;
   * Segmentstatus;
   * Identität oder Gruppen von Identitäten.

>[!NOTE]
>
>Achten Sie bei Verwendung der konfigurierbaren Aggregationsoption für Ihr Ziel auf die Mindest- und Höchstwerte, die Sie für die beiden Parameter verwenden können `maxBatchAgeInSecs` (mindestens 1 800 und höchstens 3 600) und `maxNumEventsInBatch` (mindestens 1.000, höchstens 10.000).

Ausführliche Erläuterungen der Aggregationsparameter finden Sie auf der Seite [API-Endpunktvorgänge für Ziele](./destination-configuration-api.md), wo jeder Parameter beschrieben wird.

## Historische Profilqualifikationen {#profile-backfill}

Sie können den Parameter `backfillHistoricalProfileData` in der Zielkonfiguration verwenden, um festzulegen, ob historische Profilqualifikationen in Ihr Ziel exportiert werden sollen.

| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `backfillHistoricalProfileData` | Boolesch | Steuert, ob historische Profildaten exportiert werden, wenn Segmente für das Ziel aktiviert werden. <br> <ul><li> `true`: [!DNL Platform] sendet die historischen Benutzerprofile, die sich für das Segment qualifiziert haben, bevor das Segment aktiviert wird. </li><li> `false`: [!DNL Platform] enthält nur Benutzerprofile, die sich für das Segment qualifizieren, nachdem das Segment aktiviert wurde. </li></ul> |

## Wie diese Konfiguration alle erforderlichen Informationen für Ihr Ziel verbindet  {#connecting-all-configurations}

Einige Ihrer Zieleinstellungen müssen über den [Ziel-Server](./server-and-template-configuration.md) oder die [Zielgruppen-Metadatenkonfiguration](./audience-metadata-management.md) konfiguriert werden. Die hier beschriebene Zielkonfiguration verbindet alle diese Einstellungen, indem sie wie folgt auf die beiden anderen Konfigurationen verweist:

* Verwenden Sie die `destinationServerId`, um auf den Ziel-Server und die Vorlagenkonfiguration zu verweisen, die für Ihr Ziel eingerichtet sind.
* Verwenden Sie die `audienceMetadataId`, um auf die für Ihr Ziel eingerichtete Zielgruppen-Metadatenkonfiguration zu verweisen.