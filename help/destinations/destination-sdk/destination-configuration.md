---
description: Mit dieser Konfiguration können Sie grundlegende Informationen wie Zielname, Kategorie, Beschreibung, Logo und mehr angeben. Die Einstellungen in dieser Konfiguration bestimmen auch, wie Experience Platform-Benutzer sich bei Ihrem Ziel authentifizieren, wie es in der Experience Platform-Benutzeroberfläche angezeigt wird und welche Identitäten an Ihr Ziel exportiert werden können.
title: Zielkonfigurationsoptionen für Ziel-SDK
exl-id: b7e4db67-2981-4f18-b202-3facda5c8f0b
source-git-commit: 76a596166edcdbf141b5ce5dc01557d2a0b4caf3
workflow-type: tm+mt
source-wordcount: '1727'
ht-degree: 6%

---

# Zielkonfiguration {#destination-configuration}

## Übersicht {#overview}

Mit dieser Konfiguration können Sie wichtige Informationen wie Zielname, Kategorie, Beschreibung, Logo und mehr angeben. Die Einstellungen in dieser Konfiguration bestimmen auch, wie Experience Platform-Benutzer sich bei Ihrem Ziel authentifizieren, wie es in der Experience Platform-Benutzeroberfläche angezeigt wird und welche Identitäten an Ihr Ziel exportiert werden können.

Diese Konfiguration verbindet auch die anderen Konfigurationen, die erforderlich sind, damit Ihr Ziel funktioniert - Zielserver und Zielgruppen-Metadaten - mit dieser Konfiguration. Lesen Sie, wie Sie in einem [Abschnitt weiter unten](./destination-configuration.md#connecting-all-configurations) auf die beiden Konfigurationen verweisen können.

Sie können die in diesem Dokument beschriebene Funktion mithilfe des API-Endpunkts `/authoring/destinations` konfigurieren. Eine vollständige Liste der Vorgänge, die Sie für den Endpunkt ausführen können, finden Sie unter [API-Endpunktoperationen für Ziele](./destination-configuration-api.md).

## Beispielkonfiguration  {#example-configuration}

Unten finden Sie eine Beispielkonfiguration eines fiktiven Ziels, Moviestar, das Endpunkte an vier Orten auf der Welt hat. Das Ziel gehört zur Kategorie der mobilen Ziele . Die folgenden Abschnitte zeigen, wie diese Konfiguration aufgebaut ist.

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
         "maxBatchAgeInSecs":0,
         "maxNumEventsInBatch":0,
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
| `description` | Zeichenfolge | Geben Sie im Zielkatalog der Experience Platform eine Beschreibung für Ihre Zielkarte ein. Ziel für maximal 4-5 Sätze. |
| `status` | Zeichenfolge | Gibt den Lebenszyklusstatus der Zielkarte an. Zulässige Werte sind `TEST`, `PUBLISHED` und `DELETED`. Verwenden Sie `TEST`, wenn Sie Ihr Ziel zum ersten Mal konfigurieren. |

{style=&quot;table-layout:auto&quot;}

## Benutzerauthentifizierungskonfigurationen {#customer-authentication-configurations}

Dieser Abschnitt generiert die Kontoseite in der Experience Platform-Benutzeroberfläche, auf der Benutzer die Experience Platform mit den Konten verbinden, die sie mit Ihrem Ziel haben. Je nachdem, welche Authentifizierungsoption Sie im Feld `authType` angeben, wird die Experience Platform für die Benutzer wie folgt generiert:

**Bearer-Authentifizierung**

Benutzer müssen das Trägertoken eingeben, das sie von Ihrem Ziel erhalten.

![UI-Rendering mit Trägerauthentifizierung](./assets/bearer-authentication-ui.png)

**OAuth 2-Authentifizierung**

Benutzer wählen **[!UICONTROL Mit Ziel verbinden]** aus, um den OAuth 2-Authentifizierungsfluss an Ihr Ziel Trigger.

![UI-Rendering mit OAuth 2-Authentifizierung](./assets/oauth2-authentication-ui.png)


| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `customerAuthenticationConfigurations` | Zeichenfolge | Gibt die Konfiguration an, die zum Authentifizieren von Experience Platform-Kunden auf Ihrem Server verwendet wird. Zulässige Werte finden Sie unten unter `authType` . |
| `authType` | Zeichenfolge | Akzeptierte Werte sind `OAUTH2, BEARER`. <br><ul><li> Wenn Ihr Ziel die OAuth 2-Authentifizierung unterstützt, wählen Sie den Wert `OAUTH2` aus und fügen Sie die erforderlichen Felder für OAuth 2 hinzu, wie auf der Authentifizierungsseite des Destination SDK OAuth 2 dargestellt. Außerdem sollten Sie `authenticationRule=CUSTOMER_AUTHENTICATION` im Abschnitt [Zielversand](./destination-configuration.md) auswählen. </li><li>Wählen Sie für die Trägerauthentifizierung `BEARER` und dann `authenticationRule=CUSTOMER_AUTHENTICATION` im Abschnitt [Zielversand](./destination-configuration.md) aus.</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Kundendatenfelder {#customer-data-fields}

In diesem Abschnitt können Partner benutzerdefinierte Felder einführen. In der obigen Beispielkonfiguration erfordert `customerDataFields`, dass Benutzer einen Endpunkt im Authentifizierungsfluss auswählen und ihre Kunden-ID mit dem Ziel angeben. Die Konfiguration spiegelt sich im Authentifizierungsfluss wider, wie unten dargestellt:

![Benutzerdefinierter Feldauthentifizierungsfluss](./assets/custom-field-authentication-flow.png)

| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `name` | Zeichenfolge | Geben Sie einen Namen für das benutzerdefinierte Feld ein, das Sie einführen. |
| `type` | Zeichenfolge | Gibt an, welchen Typ von benutzerdefiniertem Feld Sie einführen. Akzeptierte Werte sind `string`, `object`, `integer`. |
| `title` | Zeichenfolge | Gibt den Feldnamen an, wie er von den Kunden in der Experience Platform-Benutzeroberfläche angezeigt wird. |
| `description` | Zeichenfolge | Geben Sie eine Beschreibung für das benutzerdefinierte Feld ein. |
| `isRequired` | Boolesch | Gibt an, ob dieses Feld im Ziel-Setup-Workflow erforderlich ist. |
| `enum` | Zeichenfolge | Rendert das benutzerdefinierte Feld als Dropdown-Menü und listet die für den Benutzer verfügbaren Optionen auf. |
| `pattern` | Zeichenfolge | Erzwingt bei Bedarf ein Muster für das benutzerdefinierte Feld. Verwenden Sie reguläre Ausdrücke, um ein Muster zu erzwingen. Wenn Ihre Kunden-IDs beispielsweise keine Zahlen oder Unterstriche enthalten, geben Sie `^[A-Za-z]+$` in dieses Feld ein. |

{style=&quot;table-layout:auto&quot;}

## Benutzeroberflächenattribute {#ui-attributes}

Dieser Abschnitt bezieht sich auf die UI-Elemente in der obigen Konfiguration, die von Adobe für Ihr Ziel in der Adobe Experience Platform-Benutzeroberfläche verwendet werden sollte. Siehe unten:

| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `documentationLink` | Zeichenfolge | Bezieht sich auf die Dokumentationsseite im [Zielkatalog](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) für Ihr Ziel. Verwenden Sie `http://www.adobe.com/go/destinations-YOURDESTINATION-en`, wobei `YOURDESTINATION` der Name Ihres Ziels ist. Für ein Ziel mit dem Namen Moviestar würden Sie `http://www.adobe.com/go/destinations-moviestar-en` verwenden. |
| `category` | Zeichenfolge | Bezieht sich auf die Ihrem Ziel in Adobe Experience Platform zugewiesene Kategorie. Weitere Informationen finden Sie unter [Zielkategorien](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html). Verwenden Sie einen der folgenden Werte: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. |
| `connectionType` | Zeichenfolge | `Server-to-server` ist derzeit die einzige verfügbare Option. |
| `frequency` | Zeichenfolge | `Streaming` ist derzeit die einzige verfügbare Option. |

{style=&quot;table-layout:auto&quot;}

## Schemakonfiguration im Zuordnungsschritt {#schema-configuration}

![Mapping-Schritt aktivieren](./assets/enable-mapping-step.png)

Verwenden Sie die Parameter in `schemaConfig`, um den Zuordnungsschritt des Zielaktivierungs-Workflows zu aktivieren. Mithilfe der unten beschriebenen Parameter können Sie bestimmen, ob Experience Platform-Benutzer Profilattribute und/oder Identitäten dem gewünschten Schema auf der Zielseite zuordnen können.

| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `profileFields` | Array | *Wird in der obigen Beispielkonfiguration nicht angezeigt.* Wenn Sie vordefinierte Attribute hinzufügen, haben  `profileFields`Experience Platform-Benutzer die Möglichkeit, Platform-Attribute den vordefinierten Attributen auf der Zielseite zuzuordnen. |
| `profileRequired` | Boolesch | Verwenden Sie `true` , wenn Benutzer Profilattribute von der Experience Platform benutzerdefinierten Attributen auf der Zielseite zuordnen können sollen, wie in der obigen Beispielkonfiguration dargestellt. |
| `segmentRequired` | Boolesch | Verwenden Sie immer `segmentRequired:true`. |
| `identityRequired` | Boolesch | Verwenden Sie `true` , wenn Benutzer Identitäts-Namespaces von Experience Platform Ihrem gewünschten Schema zuordnen können sollen. |

{style=&quot;table-layout:auto&quot;}

## Identitäten und Attribute {#identities-and-attributes}

Die Parameter in diesem Abschnitt bestimmen, wie die Zielidentitäten und -attribute im Zuordnungsschritt der Experience Platform-Benutzeroberfläche ausgefüllt werden, wo Benutzer ihre XDM-Schemas dem Schema in Ihrem Ziel zuordnen.

Sie müssen angeben, welche [!DNL Platform]-Identitäten Kunden zum Export in Ihr Ziel benötigen. Beispiele sind [!DNL Experience Cloud ID], Hash-E-Mail, Geräte-ID ([!DNL IDFA], [!DNL GAID]). Diese Werte sind [!DNL Platform] Identitäts-Namespaces, die Kunden Identitäts-Namespaces von Ihrem Ziel aus zuordnen können.

Identitäts-Namespaces erfordern keine 1:1-Korrespondenz zwischen [!DNL Platform] und Ihrem Ziel.
Kunden können beispielsweise einen [!DNL Platform] [!DNL IDFA]-Namespace einem [!DNL IDFA]-Namespace von Ihrem Ziel zuordnen oder denselben [!DNL Platform] [!DNL IDFA]-Namespace einem [!DNL Customer ID]-Namespace in Ihrem Ziel zuordnen.

Weitere Informationen finden Sie in der [Übersicht über Identity-Namespace](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=de).

![Rendern von Zielidentitäten in der Benutzeroberfläche](./assets/target-identities-ui.png)

| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `acceptsAttributes` | Boolesch | Gibt an, ob Ihr Ziel Standardprofilattribute akzeptiert. Normalerweise werden diese Attribute in der Dokumentation der Partner hervorgehoben. |
| `acceptsCustomNamespaces` | Boolesch | Gibt an, ob Kunden benutzerdefinierte Namespaces in Ihrem Ziel einrichten können. |
| `allowedAttributesTransformation` | Zeichenfolge | *Wird in der Beispielkonfiguration* nicht angezeigt. Wird beispielsweise verwendet, wenn der [!DNL Platform]-Kunde einfache E-Mail-Adressen als Attribut hat und Ihre Plattform nur Hash-E-Mails akzeptiert. In diesem Objekt können Sie die Transformation durchführen, die angewendet werden muss (z. B. E-Mail in Kleinbuchstaben und dann Hash). Ein Beispiel finden Sie unter `requiredTransformation` in der [API-Referenz zur Zielkonfiguration](./destination-configuration-api.md#update). |
| `acceptedGlobalNamespaces` | – | Wird in Fällen verwendet, in denen Ihre Plattform [standardmäßige Identitäts-Namespaces](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#standard-namespaces) akzeptiert (z. B. IDFA), sodass Sie Platform-Benutzer auf die Auswahl dieser Identitäts-Namespaces beschränken können. |

{style=&quot;table-layout:auto&quot;}

## Zielversand {#destination-delivery}

| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `authenticationRule` | Zeichenfolge | Gibt an, wie [!DNL Platform]-Kunden eine Verbindung zu Ihrem Ziel herstellen. Akzeptierte Werte sind `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Verwenden Sie `CUSTOMER_AUTHENTICATION` , wenn sich Platform-Kunden über einen Benutzernamen und ein Kennwort, ein Trägertoken oder eine andere Authentifizierungsmethode bei Ihrem System anmelden. Sie würden diese Option beispielsweise auswählen, wenn Sie auch `authType: OAUTH2` oder `authType:BEARER` in `customerAuthenticationConfigurations` ausgewählt haben. </li><li> Verwenden Sie `PLATFORM_AUTHENTICATION`, wenn ein globales Authentifizierungssystem zwischen Adobe und Ihrem Ziel vorhanden ist und der [!DNL Platform]-Kunde keine Authentifizierungsberechtigungen angeben muss, um eine Verbindung zu Ihrem Ziel herzustellen. In diesem Fall müssen Sie mithilfe der Konfiguration [Credentials](./credentials-configuration.md) ein Anmeldedatenobjekt erstellen. </li><li>Verwenden Sie `NONE` , wenn keine Authentifizierung erforderlich ist, um Daten an Ihre Zielplattform zu senden. </li></ul> |
| `destinationServerId` | Zeichenfolge | Die `instanceId` der [Zielserverkonfiguration](./destination-server-api.md), die für dieses Ziel verwendet wird. |
| `backfillHistoricalProfileData` | Boolesch | Steuert, ob historische Profildaten exportiert werden, wenn Segmente für das Ziel aktiviert werden. <br> <ul><li> `true`:  [!DNL Platform] sendet die historischen Benutzerprofile, die sich für das Segment qualifiziert haben, bevor das Segment aktiviert wird. </li><li> `false`:  [!DNL Platform] enthält nur Benutzerprofile, die sich für das Segment qualifizieren, nachdem das Segment aktiviert wurde. </li></ul> |

{style=&quot;table-layout:auto&quot;}

## Konfiguration der Segmentzuordnung {#segment-mapping}

![Konfigurationsabschnitt für die Segmentzuordnung](./assets/segment-mapping-configuration.png)

Dieser Abschnitt der Zielkonfiguration bezieht sich darauf, wie Segmentmetadaten wie Segmentnamen oder IDs zwischen Experience Platform und Ihrem Ziel freigegeben werden sollen.

Über `audienceTemplateId` verknüpft dieser Abschnitt auch diese Konfiguration mit der [Konfiguration der Zielgruppen-Metadaten](./audience-metadata-management.md).

Die in der obigen Konfiguration angezeigten Parameter werden in der [Ziel-Endpunkt-API-Referenz](./destination-configuration-api.md) beschrieben.

## Wie diese Konfiguration alle erforderlichen Informationen für Ihr Ziel verbindet {#connecting-all-configurations}

Einige Einstellungen für Ihr Ziel können über den Zielserver oder den Zielmetadaten-Endpunkt konfiguriert werden. Der Endpunkt für die Zielkonfiguration verbindet alle diese Einstellungen, indem er auf die Konfigurationen wie folgt verweist:

* Verwenden Sie `destinationServerId`, um auf den Zielserver und die Vorlagenkonfiguration zu verweisen, die für Ihr Ziel eingerichtet sind.
* Verwenden Sie `audienceMetadataId`, um auf die für Ihr Ziel eingerichtete Konfiguration für Zielgruppen-Metadaten zu verweisen.


## Aggregationspolitik {#aggregation}

![Aggregationsrichtlinie in der Konfigurationsvorlage](./assets/aggregation-configuration.png)

In diesem Abschnitt können Sie die Aggregationsrichtlinien festlegen, die Experience Platform beim Exportieren von Daten in Ihr Ziel verwenden sollte.

Eine Aggregationsrichtlinie bestimmt, wie die exportierten Profile in den Datenexporten kombiniert werden. Verfügbare Optionen sind:
* Aggregation des besten Aufwands
* Konfigurierbare Aggregation (siehe Konfiguration oben)

Lesen Sie den Abschnitt [Verwendung der Vorlage](./message-format.md#using-templating) und die [Beispiele für Aggregationsschlüssel](./message-format.md#template-aggregation-key) , um zu verstehen, wie Sie die Aggregationsrichtlinie basierend auf Ihrer ausgewählten Aggregationsrichtlinie in Ihre Nachrichtenumwandlungsvorlage aufnehmen können.

### Aggregation des besten Aufwands {#best-effort-aggregation}

>[!TIP]
>
>Verwenden Sie diese Option, wenn Ihr API-Endpunkt weniger als 100 Profile pro API-Aufruf akzeptiert.

Diese Option eignet sich am besten für Ziele, die weniger Profile pro Anforderung bevorzugen und stattdessen mehr Anforderungen mit weniger Daten als weniger Anforderungen mit mehr Daten benötigen.

Verwenden Sie den Parameter `maxUsersPerRequest` , um die maximale Anzahl von Profilen anzugeben, die Ihr Ziel in einer Anfrage aufnehmen kann.

### Konfigurierbare Aggregation {#configurable-aggregation}

Diese Option eignet sich am besten, wenn Sie lieber große Batches mit Tausenden von Profilen im selben Aufruf durchführen möchten. Mit dieser Option können Sie die exportierten Profile auch auf der Grundlage komplexer Aggregationsregeln aggregieren.

Diese Option ermöglicht Ihnen Folgendes:
* Legen Sie die maximale Zeit und Anzahl der Profile fest, die aggregiert werden sollen, bevor ein API-Aufruf an Ihr Ziel gesendet wird.
* Aggregieren Sie die exportierten Profile, die dem Ziel zugeordnet sind, basierend auf:
   * Segment-ID
   * Segmentstatus
   * Identität oder Identitätsgruppen

Detaillierte Erläuterungen zu Aggregationsparametern finden Sie auf der Referenzseite [API-Endpunktoperationen für Ziele](./destination-configuration-api.md), auf der jeder Parameter beschrieben wird.

## Historische Profilqualifikationen

Sie können den Parameter `backfillHistoricalProfileData` in der Zielkonfiguration verwenden, um zu bestimmen, ob historische Profilqualifikationen an Ihr Ziel exportiert werden sollen.

| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `backfillHistoricalProfileData` | Boolesch | Steuert, ob historische Profildaten exportiert werden, wenn Segmente für das Ziel aktiviert werden. <br> <ul><li> `true`:  [!DNL Platform] sendet die historischen Benutzerprofile, die sich für das Segment qualifiziert haben, bevor das Segment aktiviert wird. </li><li> `false`:  [!DNL Platform] enthält nur Benutzerprofile, die sich für das Segment qualifizieren, nachdem das Segment aktiviert wurde. </li></ul> |