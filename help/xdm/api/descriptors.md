---
keywords: Experience Platform;Startseite;beliebte Themen;API;API;XDM;XDM-System;Experience-Datenmodell;Experience-Datenmodell;Experience-Datenmodell;Datenmodell;Datenmodell;Schema Registry;Schemaregistrierung;Schema Registry;Deskriptor;Deskriptoren;Deskriptoren;Identität;Identität;Anzeigename;Anzeigename;alternativeDisplayInfo;Referenz;Referenz;Beziehung;Beziehung
solution: Experience Platform
title: API-Endpunkt für Deskriptoren
description: Mit dem Endpunkt /descriptors in der Schema Registry-API können Sie XDM-Deskriptoren in Ihrer Erlebnisanwendung programmgesteuert verwalten.
exl-id: bda1aabd-5e6c-454f-a039-ec22c5d878d2
source-git-commit: d6015125e3e29bdd6a6c505b5f5ad555bd17a0e0
workflow-type: tm+mt
source-wordcount: '2192'
ht-degree: 38%

---

# Descriptors-Endpunkt

Schemata definieren eine statische Ansicht von Datenentitäten, geben jedoch nicht spezifisch an, wie sich Daten, die auf diesen Schemata basieren (z. B. Datensätze), zueinander verhalten. Mit Adobe Experience Platform können Sie diese Beziehungen und andere interpretative Metadaten über ein Schema mithilfe von Deskriptoren beschreiben.

Schemadeskriptoren sind Metadaten auf Mandantenebene, d. h. sie sind für Ihre Organisation eindeutig, und alle Deskriptorvorgänge finden im Mandanten-Container statt.

Auf jedes Schema können eine oder mehrere Schemadeskriptorentitäten angewendet werden. Jede Schemadeskriptorentität enthält einen Deskriptor `@type` und das `sourceSchema`, auf das er angewendet wird. Nach der Anwendung gelten diese Deskriptoren für alle mit dem Schema erstellten Datensätze.

Mit dem `/descriptors`-Endpunkt in der [!DNL Schema Registry]-API können Sie Deskriptoren in Ihrem Erlebnisprogramm programmgesteuert verwalten.

## Erste Schritte

Der in diesem Handbuch verwendete Endpunkt ist Teil der [[!DNL Schema Registry] API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Bevor Sie fortfahren, lesen Sie das Handbuch [Erste Schritte](./getting-started.md) mit Links zur zugehörigen Dokumentation, einer Anleitung zum Lesen der API-Beispielaufrufe in diesem Dokument und wichtigen Informationen zu den erforderlichen Kopfzeilen, die für die erfolgreiche Ausführung von Aufrufen an eine Experience Platform-API erforderlich sind.

## Abrufen einer Liste von Deskriptoren {#list}

Sie können alle Deskriptoren auflisten, die von Ihrem Unternehmen definiert wurden, indem Sie eine GET-Anfrage an `/tenant/descriptors` stellen.

**API-Format**

```http
GET /tenant/descriptors
```

**Anfrage**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xdm-link+json'
```

Das Format der Antwort hängt von der in der Anfrage gesendeten `Accept`-Kopfzeile ab. Beachten Sie, dass der `/descriptors`-Endpunkt `Accept` Kopfzeilen verwendet, die sich von allen anderen Endpunkten in der [!DNL Schema Registry]-API unterscheiden.

>[!IMPORTANT]
>
>Deskriptoren erfordern eindeutige `Accept`, die `xed` durch `xdm` ersetzen, und bieten außerdem eine für Deskriptoren eindeutige `link`. Die richtigen `Accept`-Kopfzeilen wurden in die folgenden Beispielaufrufe aufgenommen, Sie müssen jedoch besonders vorsichtig sein, um sicherzustellen, dass beim Arbeiten mit Deskriptoren die richtigen Kopfzeilen verwendet werden.

| `Accept`-Kopfzeile | Beschreibung |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | Gibt ein Array mit Deskriptorkennungen zurück |
| `application/vnd.adobe.xdm-link+json` | Gibt ein Array mit Deskriptor-API-Pfaden zurück |
| `application/vnd.adobe.xdm+json` | Gibt ein Array mit erweiterten Deskriptorobjekten zurück |
| `application/vnd.adobe.xdm-v2+json` | Dieser `Accept`-Header muss verwendet werden, um Paging-Funktionen zu nutzen. |

{style="table-layout:auto"}

**Antwort**

Die Antwort enthält ein Array für jeden Deskriptortyp, der über definierte Deskriptoren verfügt. Wenn keine Deskriptoren eines bestimmten `@type` definiert sind, gibt die Registrierung also kein leeres Array für diesen Deskriptortyp zurück.

Bei Verwendung der `link` `Accept`-Kopfzeile wird jeder Deskriptor als Array-Element im Format `/{CONTAINER}/descriptors/{DESCRIPTOR_ID}` angezeigt

```JSON
{
  "xdm:alternateDisplayInfo": [
    "/tenant/descriptors/85dc1bc8b91516ac41163365318e38a9f1e4f351",
    "/tenant/descriptors/49bd5abb5a1310ee80ebc1848eb508d383a462cf",
    "/tenant/descriptors/b3b3e548f1c653326bcf5459ceac4140fc0b9e08"
  ],
  "xdm:descriptorIdentity": [
    "/tenant/descriptors/f7a4bc25429496c4740f8f9a7a49ba96862c5379"
  ],
  "xdm:descriptorOneToOne": [
    "/tenant/descriptors/cb509fd6f8ab6304e346905441a34b58a0cd481a"
  ]
}
```

## Deskriptor nachschlagen {#lookup}

Wenn Sie die Details eines bestimmten Deskriptors anzeigen möchten, können Sie einen einzelnen Deskriptor mit dessen `@id` nachschlagen (GET).

**API-Format**

```http
GET /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{DESCRIPTOR_ID}` | Die `@id` des Deskriptors, den Sie suchen möchten. |

{style="table-layout:auto"}

**Anfrage**

Die folgende Anfrage ruft einen Deskriptor anhand seines `@id` ab. Deskriptoren sind nicht versioniert, daher ist in der Suchanfrage keine `Accept`-Kopfzeile erforderlich.

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details des Deskriptors zurück, einschließlich des zugehörigen `@type` und `sourceSchema` sowie zusätzlicher Informationen, die je nach Deskriptortyp variieren. Die zurückgegebene `@id` sollte mit der in der Anfrage angegebenen `@id` des Deskriptors übereinstimmen.

```JSON
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false,
  "createdUser": "{CREATED_USER}",
  "imsOrg": "{ORG_ID}",
  "createdClient": "{CREATED_CLIENT}",
  "updatedUser": "{UPDATED_USER}",
  "created": 1548899346989,
  "updated": 1548899346989,
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## Erstellen eines Deskriptors {#create}

Sie können einen neuen Deskriptor erstellen, indem Sie eine POST-Anfrage an den `/tenant/descriptors`-Endpunkt senden.

>[!IMPORTANT]
>
>Mit dem [!DNL Schema Registry] können Sie mehrere verschiedene Deskriptortypen definieren. Jeder Deskriptortyp erfordert, dass seine eigenen spezifischen Felder im Anfragetext gesendet werden. Eine vollständige Liste der Deskriptoren [ die Felder, die ](#defining-descriptors) Definieren der Deskriptoren erforderlich sind, finden Sie im Anhang .

**API-Format**

```http
POST /tenant/descriptors
```

**Anfrage**

Die folgende Anfrage definiert einen Identitätsdeskriptor für ein Feld „E-Mail-Adresse“ in einem Beispielschema. Dadurch wird [!DNL Experience Platform] angewiesen, die E-Mail-Adresse als Kennung zu verwenden, um Informationen über die Person zusammenzufügen.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
      {
        "@type": "xdm:descriptorIdentity",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/personalEmail/address",
        "xdm:namespace": "Email",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": false
      }'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 201 (Erstellt) und die Details des neu erstellten Deskriptors zurück, einschließlich dessen `@id`. Der `@id` ist ein schreibgeschütztes Feld, das vom [!DNL Schema Registry] zugewiesen wird und für die Referenzierung des Deskriptors in der API verwendet wird.

```JSON
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false,
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## Aktualisieren eines Deskriptors {#put}

Sie können einen Deskriptor aktualisieren, indem Sie seinen `@id` im Pfad einer PUT-Anfrage angeben.

**API-Format**

```http
PUT /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{DESCRIPTOR_ID}` | Die `@id` des Deskriptors, den Sie aktualisieren möchten. |

{style="table-layout:auto"}

**Anfrage**

Diese Anfrage schreibt den Deskriptor im Wesentlichen neu. Daher muss der Anfragetext alle Felder enthalten, die zum Definieren eines Deskriptors dieses Typs erforderlich sind. Mit anderen Worten, die Anfrage-Payload zum Aktualisieren (PUT) eines Deskriptors ist identisch mit der Payload zum [ (POST) eines Deskriptors](#create) desselben Typs.

>[!IMPORTANT]
>
>Wie beim Erstellen von Deskriptoren mithilfe von POST-Anfragen ist es erforderlich, dass für jeden Deskriptortyp eigene spezifische Felder in den Payloads von PUT-Anfragen gesendet werden. Eine vollständige Liste der Deskriptoren [ die Felder, die ](#defining-descriptors) Definieren der Deskriptoren erforderlich sind, finden Sie im Anhang .

Im folgenden Beispiel wird ein Identitätsdeskriptor aktualisiert, um auf einen anderen `xdm:sourceProperty` (`mobile phone`) zu verweisen und die `xdm:namespace` in `Phone` zu ändern.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "@type": "xdm:descriptorIdentity",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/mobilePhone/number",
        "xdm:namespace": "Phone",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": false
      }'
```

**Antwort**

Bei einer erfolgreichen Antwort werden der HTTP-Status 201 (Erstellt) und die `@id` des aktualisierten Deskriptors zurückgegeben (sie sollte mit der in der Anfrage gesendeten `@id` übereinstimmen).

```JSON
{
    "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

Wenn Sie eine [Suchanfrage (GET) ](#lookup), um den Deskriptor anzuzeigen, werden die Felder jetzt aktualisiert, damit die in der PUT-Anfrage gesendeten Änderungen widergespiegelt werden.

## Löschen eines Deskriptors {#delete}

Gelegentlich müssen Sie möglicherweise einen Deskriptor entfernen, den Sie aus der [!DNL Schema Registry] definiert haben. Dies geschieht, indem Sie eine DELETE-Anfrage stellen, die auf die `@id` des Deskriptors verweist, den Sie entfernen möchten.

**API-Format**

```http
DELETE /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{DESCRIPTOR_ID}` | Die `@id` des Deskriptors, den Sie löschen möchten. |

{style="table-layout:auto"}

**Anfrage**

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/ca921946fb5281cbdb8ba5e07087486ce531a1f2  \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 204 (Kein Inhalt) und leeren Text zurück.

Um zu bestätigen, dass der Deskriptor gelöscht wurde, können Sie eine [Suchanfrage](#lookup) für den `@id` durchführen. Die Antwort gibt den HTTP-Status 404 (Nicht gefunden) zurück, da der Deskriptor aus der [!DNL Schema Registry] entfernt wurde.

## Anhang

Der folgende Abschnitt enthält zusätzliche Informationen zum Arbeiten mit Deskriptoren in der [!DNL Schema Registry]-API.

### Deskriptoren definieren {#defining-descriptors}

>[!NOTE]
>
>Die maximale Anzahl von Deskriptoren, die auf die Sandbox einer Organisation angewendet werden können, beträgt 4.000.

Die folgenden Abschnitte bieten eine Übersicht über die verfügbaren Deskriptortypen, einschließlich der erforderlichen Felder zum Definieren eines Deskriptors für die einzelnen Typen.

>[!IMPORTANT]
>
>Sie können das Namespace-Objekt des Mandanten nicht beschriften, da das System diese Beschriftung auf jedes benutzerdefinierte Feld in dieser Sandbox anwenden würde. Stattdessen müssen Sie den Endknoten unter dem Objekt angeben, das Sie beschriften müssen.

#### Identitätsdeskriptor

Ein Identitätsdeskriptor signalisiert, dass &quot;[!UICONTROL sourceProperty]&quot; von &quot;[!UICONTROL sourceSchema]&quot; ein [!DNL Identity] ist, wie vom [Adobe Experience Platform Identity Service](../../identity-service/home.md) beschrieben.

```json
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema":
    "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `@type` | Der Typ des zu definierenden Deskriptors. Für einen Identitätsdeskriptor muss dieser Wert auf `xdm:descriptorIdentity` gesetzt werden. |
| `xdm:sourceSchema` | Der `$id`-URI des Schemas, wo der Deskriptor definiert wird. |
| `xdm:sourceVersion` | Die Hauptversion des Quellschemas. |
| `xdm:sourceProperty` | Der Pfad zur spezifischen Eigenschaft, die die Identität sein wird. Der Pfad sollte mit einem „/“ beginnen und nicht mit einem enden. Fügen Sie keine „Eigenschaften“ in den Pfad ein (verwenden Sie beispielsweise &quot;/personalEmail/address“ anstelle von &quot;/properties/personalEmail/properties/address„) |
| `xdm:namespace` | Der `id`- oder `code`-Wert des Identitäts-Namespace. Eine Liste der Namespaces finden Sie unter Verwendung des [[!DNL Identity Service API]](https://developer.adobe.com/experience-platform-apis/references/identity-service) . |
| `xdm:property` | Entweder `xdm:id` oder `xdm:code`, je nach verwendetem `xdm:namespace`. |
| `xdm:isPrimary` | Ein optionaler boolescher Wert. Wenn „true“, wird das Feld als primäre Identität angezeigt. Schemata dürfen nur eine primäre Identität enthalten. |

{style="table-layout:auto"}

#### Anzeigenamendeskriptor {#friendly-name}

Mit Deskriptoren für benutzerfreundliche Namen können Benutzende die `title`-, `description`- und `meta:enum` der Schemafelder der Hauptbibliothek ändern. Besonders nützlich sind sie bei der Arbeit mit „eVars“ und anderen „generischen“ Feldern, um Felder zu kennzeichnen, die organisationsspezifische Daten enthalten. Die Benutzeroberfläche kann so einen benutzerfreundlicheren Namen anzeigen oder nur Felder mit einem Anzeigenamen anzeigen.

```json
{
  "@type": "xdm:alternateDisplayInfo",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/xdm:eventType",
  "xdm:title": {
    "en_us": "Event Type"
  },
  "xdm:description": {
    "en_us": "The type of experience event detected by the system."
  },
  "meta:enum": {
    "click": "Mouse Click",
    "addCart": "Add to Cart",
    "checkout": "Cart Checkout"
  },
  "xdm:excludeMetaEnum": {
    "web.formFilledOut": "Web Form Filled Out",
    "media.ping": "Media ping"
  }
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `@type` | Der Typ des zu definierenden Deskriptors. Für einen Deskriptor mit benutzerfreundlichem Namen muss dieser Wert auf `xdm:alternateDisplayInfo` gesetzt werden. |
| `xdm:sourceSchema` | Der `$id`-URI des Schemas, wo der Deskriptor definiert wird. |
| `xdm:sourceVersion` | Die Hauptversion des Quellschemas. |
| `xdm:sourceProperty` | Der Pfad zur spezifischen Eigenschaft, deren Details Sie ändern möchten. Der Pfad sollte mit einem Schrägstrich (`/`) beginnen und nicht mit einem Schrägstrich enden. Fügen Sie keine `properties` in den Pfad ein (verwenden Sie beispielsweise `/personalEmail/address` statt `/properties/personalEmail/properties/address`). |
| `xdm:title` | Der neue Titel, den Sie für dieses Feld anzeigen möchten, in Großschreibung des ersten Buchstaben jedes Worts geschrieben. |
| `xdm:description` | Zusammen mit dem Titel kann eine optionale Beschreibung hinzugefügt werden. |
| `meta:enum` | Wenn das durch `xdm:sourceProperty` angegebene Feld ein Zeichenfolgenfeld ist, kann `meta:enum` verwendet werden, um in der Segmentierungs-Benutzeroberfläche vorgeschlagene Werte für das Feld hinzuzufügen. Beachten Sie, dass `meta:enum` keine Auflistung deklariert und keine Datenvalidierung für das XDM-Feld bereitstellt.<br><br>Dies sollte nur für von Adobe definierte XDM-Kernfelder verwendet werden. Wenn die Quelleigenschaft ein benutzerdefiniertes Feld ist, das von Ihrer Organisation definiert wurde, sollten Sie stattdessen die `meta:enum`-Eigenschaft des Felds direkt über eine PATCH-Anfrage an die übergeordnete Ressource des Felds bearbeiten. |
| `meta:excludeMetaEnum` | Wenn das durch `xdm:sourceProperty` angegebene Feld ein Zeichenfolgenfeld ist, das vorhandene vorgeschlagene Werte unter einem `meta:enum` Feld bereitgestellt hat, können Sie dieses Objekt in einen Deskriptor für benutzerfreundliche Namen aufnehmen, um einige oder alle diese Werte aus der Segmentierung auszuschließen. Schlüssel und Wert jedes Eintrags müssen mit denen übereinstimmen, die in der ursprünglichen `meta:enum` des Felds enthalten sind, damit der Eintrag ausgeschlossen wird. |

{style="table-layout:auto"}

#### Beziehungsdeskriptor {#relationship-descriptor}

Beziehungsdeskriptoren beschreiben eine Beziehung zwischen zwei verschiedenen Schemata. Sie werden in die Eigenschaften eingegeben, die in `sourceProperty` und `destinationProperty` beschrieben werden. Weiterführende Informationen finden Sie in der Anleitung zum [Definieren einer Beziehung zwischen zwei Schemata](../tutorials/relationship-api.md).

```json
{
  "@type": "xdm:descriptorOneToOne",
  "xdm:sourceSchema":
    "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/parentField/subField",
  "xdm:destinationSchema": 
    "https://ns.adobe.com/{TENANT_ID}/schemas/78bab6346b9c5102b60591e15e75d254",
  "xdm:destinationVersion": 1,
  "xdm:destinationProperty": "/parentField/subField"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `@type` | Der Typ des zu definierenden Deskriptors. Für einen Beziehungsdeskriptor muss dieser Wert auf `xdm:descriptorOneToOne` festgelegt werden, es sei denn, Sie haben Zugriff auf Real-Time CDP B2B edition. Mit B2B edition haben Sie die Möglichkeit, `xdm:descriptorOneToOne` oder [`xdm:descriptorRelationship`](#b2b-relationship-descriptor) zu verwenden. |
| `xdm:sourceSchema` | Der `$id`-URI des Schemas, wo der Deskriptor definiert wird. |
| `xdm:sourceVersion` | Die Hauptversion des Quellschemas. |
| `xdm:sourceProperty` | Der Pfad zum Feld im Quellschema, in dem die Beziehung definiert wird. Sollte mit &quot;/&quot; beginnen und nicht mit &quot;/&quot; enden. Schließen Sie „properties“ nicht in den Pfad ein (z. B. „/personalEmail/address“ anstelle von „/properties/personalEmail/properties/address“). |
| `xdm:destinationSchema` | Der `$id`-URI des Referenzschemas, mit dem dieser Deskriptor eine Beziehung definiert. |
| `xdm:destinationVersion` | Die Hauptversion des Referenzschemas. |
| `xdm:destinationProperty` | (Optional) Pfad zu einem Zielfeld im Referenzschema. Wenn diese Eigenschaft weggelassen wird, wird das Zielfeld von allen Feldern mit einem entsprechenden Referenzidentitätsdeskriptor abgeleitet (siehe unten). |

{style="table-layout:auto"}

##### B2B-Beziehungsdeskriptor {#B2B-relationship-descriptor}

Real-Time CDP B2B edition führt eine alternative Methode zur Definition von Beziehungen zwischen Schemata ein, die Viele-zu-Eins-Beziehungen ermöglicht. Diese neue Beziehung muss den `@type: xdm:descriptorRelationship` aufweisen, und die Payload muss mehr Felder als die `@type: xdm:descriptorOneToOne` enthalten. Weitere Informationen finden Sie im Tutorial [Definieren einer Schemabeziehung für ](../tutorials/relationship-b2b.md)B2B edition&quot;.

```json
{
   "@type": "xdm:descriptorRelationship",
   "xdm:sourceSchema" : "https://ns.adobe.com/{TENANT_ID}/schemas/9f2b2f225ac642570a110d8fd70800ac0c0573d52974fa9a",
   "xdm:sourceVersion" : 1,
   "xdm:sourceProperty" : "/person-ref",
   "xdm:destinationSchema" : "https://ns.adobe.com/{TENANT_ID/schemas/628427680e6b09f1f5a8f63ba302ee5ce12afba8de31acd7",
   "xdm:destinationVersion" : 1,
   "xdm:destinationProperty": "/personId",
   "xdm:destinationNamespace" : "People", 
   "xdm:destinationToSourceTitle" : "Opportunity Roles",
   "xdm:sourceToDestinationTitle" : "People",
   "xdm:cardinality": "M:1"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `@type` | Der Typ des zu definierenden Deskriptors. Für uns mit den folgenden Feldern muss der Wert auf `xdm:descriptorRelationship` gesetzt werden. Weitere Informationen zu zusätzlichen Typen finden Sie [ Abschnitt ](#relationship-descriptor)Beziehungsdeskriptoren“. |
| `xdm:sourceSchema` | Der `$id`-URI des Schemas, wo der Deskriptor definiert wird. |
| `xdm:sourceVersion` | Die Hauptversion des Quellschemas. |
| `xdm:sourceProperty` | Der Pfad zum Feld im Quellschema, in dem die Beziehung definiert wird. Sollte mit &quot;/&quot; beginnen und nicht mit &quot;/&quot; enden. Schließen Sie „properties“ nicht in den Pfad ein (z. B. „/personalEmail/address“ anstelle von „/properties/personalEmail/properties/address“). |
| `xdm:destinationSchema` | Der `$id`-URI des Referenzschemas, mit dem dieser Deskriptor eine Beziehung definiert. |
| `xdm:destinationVersion` | Die Hauptversion des Referenzschemas. |
| `xdm:destinationProperty` | (Optional) Pfad zu einem Zielfeld im Referenzschema, das die primäre ID des Schemas sein muss. Wenn diese Eigenschaft weggelassen wird, wird das Zielfeld von allen Feldern mit einem entsprechenden Referenzidentitätsdeskriptor abgeleitet (siehe unten). |
| `xdm:destinationNamespace` | Der Namespace der primären ID aus dem Referenzschema. |
| `xdm:destinationToSourceTitle` | Der Anzeigename der Beziehung vom Referenzschema zum Quellschema. |
| `xdm:sourceToDestinationTitle` | Der Anzeigename der Beziehung vom Quellschema zum Referenzschema. |
| `xdm:cardinality` | Die Verknüpfungsbeziehung zwischen den Schemas. Dieser Wert sollte auf `M:1` gesetzt werden und sich auf eine Viele-zu-eins-Beziehung beziehen. |

{style="table-layout:auto"}

#### Referenzidentitätsdeskriptor

Referenz-Identitätsdeskriptoren bieten einen Referenzkontext für die primäre Identität eines Schemafelds, sodass diese von Feldern in anderen Schemata referenziert werden kann. Für das Referenzschema muss bereits ein primäres Identitätsfeld definiert sein, bevor es von anderen Schemata über diesen Deskriptor referenziert werden kann.

```json
{
  "@type": "xdm:descriptorReferenceIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/78bab6346b9c5102b60591e15e75d254",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/parentField/subField",
  "xdm:identityNamespace": "Email"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `@type` | Der Typ des zu definierenden Deskriptors. Für einen Referenz-Identitätsdeskriptor muss dieser Wert auf `xdm:descriptorReferenceIdentity` gesetzt werden. |
| `xdm:sourceSchema` | Der `$id`-URI des Schemas, wo der Deskriptor definiert wird. |
| `xdm:sourceVersion` | Die Hauptversion des Quellschemas. |
| `xdm:sourceProperty` | Pfad zum Feld im Quellschema, das für den Verweis auf das Referenzschema verwendet wird. Sollte mit einem „/“ beginnen und nicht mit einem solchen enden. Schließen Sie keine „Eigenschaften“ in den Pfad ein (z. B. `/personalEmail/address` statt `/properties/personalEmail/properties/address`). |
| `xdm:identityNamespace` | Der Identitäts-Namespace-Code für die Quelleigenschaft. |

{style="table-layout:auto"}

#### Veralteter Felddeskriptor

Sie können [ein Feld in einer benutzerdefinierten XDM-Ressource verwerfen](../tutorials/field-deprecation-api.md#custom) indem Sie dem betreffenden Feld ein `meta:status`-Attribut hinzufügen, das auf `deprecated` gesetzt ist. Wenn Sie Felder verwerfen möchten, die von standardmäßigen XDM-Ressourcen in Ihren Schemata bereitgestellt werden, können Sie dem betreffenden Schema jedoch einen verworfenen Felddeskriptor zuweisen, um dieselbe Wirkung zu erzielen. Mithilfe der [korrekten `Accept`-Kopfzeile](../tutorials/field-deprecation-api.md#verify-deprecation) können Sie dann in der API anzeigen, welche Standardfelder für ein Schema veraltet sind.

```json
{
  "@type": "xdm:descriptorDeprecated",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/c65ddf08cf2d4a2fe94bd06113bf4bc4c855e12a936410d5",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/faxPhone"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `@type` | Der Typ des Deskriptors. Für einen Deskriptor zum Verwerfen von Feldern muss dieser Wert auf `xdm:descriptorDeprecated` gesetzt werden. |
| `xdm:sourceSchema` | Der URI `$id` des Schemas, auf das Sie den Deskriptor anwenden. |
| `xdm:sourceVersion` | Die Version des Schemas, auf das Sie den Deskriptor anwenden. Sollte auf `1` gesetzt werden. |
| `xdm:sourceProperty` | Der Pfad zur Eigenschaft innerhalb des Schemas, auf das Sie den Deskriptor anwenden. Wenn Sie den Deskriptor auf mehrere Eigenschaften anwenden möchten, können Sie eine Liste von Pfaden in Form eines Arrays bereitstellen (z. B. `["/firstName", "/lastName"]`). |

{style="table-layout:auto"}
