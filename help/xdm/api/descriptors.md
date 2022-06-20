---
keywords: Experience Platform;Startseite;beliebte Themen;API;XDM;XDM-System;Experience-Datenmodell;Experience-Datenmodell;Experience-Datenmodell;Datenmodell;Datenmodell;Schemaregistrierung;Schema Registry;Deskriptor;Deskriptoren;Deskriptoren;Identität;Anzeigename;Anzeigename;alternativeDisplayInfo;Referenz;Beziehung;Beziehung
solution: Experience Platform
title: Descriptors-API-Endpunkt
description: Mit dem Endpunkt /descriptors in der Schema Registry-API können Sie XDM-Deskriptoren in Ihrer Erlebnisanwendung programmgesteuert verwalten.
topic-legacy: developer guide
exl-id: bda1aabd-5e6c-454f-a039-ec22c5d878d2
source-git-commit: b92246e729ca26387a3d375e5627165a29956e52
workflow-type: tm+mt
source-wordcount: '1836'
ht-degree: 51%

---

# Deskriptorendpunkt

Schemas definieren eine statische Ansicht von Datenentitäten, geben jedoch nicht spezifisch an, wie sich Daten, die auf diesen Schemas basieren (z. B. Datensätze), zueinander verhalten. Mit Adobe Experience Platform können Sie diese Beziehungen und andere interpretative Metadaten über ein Schema mithilfe von Deskriptoren beschreiben.

Schemadeskriptoren sind Metadaten auf Mandantenebene, das heißt, sie sind für Ihre IMS-Organisation eindeutig und alle Deskriptorvorgänge finden im Mandanten-Container statt.

Auf jedes Schema können eine oder mehrere Schemadeskriptorentitäten angewendet werden. Jede Schemadeskriptorentität enthält einen Deskriptor `@type` und das `sourceSchema`, auf das er angewendet wird. Nach der Anwendung gelten diese Deskriptoren für alle mit dem Schema erstellten Datensätze.

Die `/descriptors` -Endpunkt im [!DNL Schema Registry] Mit der API können Sie Deskriptoren in Ihrer Erlebnisanwendung programmgesteuert verwalten.

## Erste Schritte

Der in diesem Handbuch verwendete Endpunkt ist Teil der [[!DNL Schema Registry] API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Bevor Sie fortfahren, lesen Sie das Handbuch [Erste Schritte](./getting-started.md) mit Links zur zugehörigen Dokumentation, einer Anleitung zum Lesen der API-Beispielaufrufe in diesem Dokument und wichtigen Informationen zu den erforderlichen Kopfzeilen, die für die erfolgreiche Ausführung von Aufrufen an eine Experience Platform-API erforderlich sind.

## Abrufen einer Liste von Deskriptoren {#list}

Sie können alle von Ihrem Unternehmen definierten Deskriptoren auflisten, indem Sie eine GET-Anfrage an `/tenant/descriptors`.

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

Das Antwortformat hängt von der `Accept` -Kopfzeile, die in der Anfrage gesendet wird. Beachten Sie, dass `/descriptors` Endpunktverwendungen `Accept` Kopfzeilen, die sich von allen anderen Endpunkten im [!DNL Schema Registry] API.

>[!IMPORTANT]
>
>Deskriptoren erfordern eindeutige `Accept` Header, die `xed` mit `xdm`, und bieten auch eine `link` -Option, die für Deskriptoren eindeutig ist. Die `Accept` -Kopfzeilen wurden in den Beispielaufrufen unten aufgeführt. Achten Sie jedoch besonders darauf, sicherzustellen, dass beim Arbeiten mit Deskriptoren die richtigen Kopfzeilen verwendet werden.

| `Accept`-Kopfzeile | Beschreibung |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | Gibt ein Array mit Deskriptorkennungen zurück |
| `application/vnd.adobe.xdm-link+json` | Gibt ein Array mit Deskriptor-API-Pfaden zurück |
| `application/vnd.adobe.xdm+json` | Gibt ein Array mit erweiterten Deskriptorobjekten zurück |
| `application/vnd.adobe.xdm-v2+json` | Diese `Accept` -Kopfzeile muss verwendet werden, um Paging-Funktionen nutzen zu können. |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Die Antwort enthält ein Array für jeden Deskriptortyp, der über definierte Deskriptoren verfügt. Wenn keine Deskriptoren eines bestimmten `@type` definiert sind, gibt die Registrierung also kein leeres Array für diesen Deskriptortyp zurück.

Bei Verwendung von `link` `Accept` -Kopfzeile wird jeder Deskriptor als Array-Element im Format angezeigt `/{CONTAINER}/descriptors/{DESCRIPTOR_ID}`

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
| `{DESCRIPTOR_ID}` | Die `@id` des Deskriptors, den Sie nachschlagen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Mit der folgenden Anfrage wird ein Deskriptor durch seine `@id` -Wert. Deskriptoren sind nicht versioniert, daher keine `Accept` -Kopfzeile ist in der Suchanfrage erforderlich.

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

## Deskriptor erstellen {#create}

Sie können einen neuen Deskriptor erstellen, indem Sie eine POST-Anfrage an die `/tenant/descriptors` -Endpunkt.

>[!IMPORTANT]
>
>Die [!DNL Schema Registry] ermöglicht die Definition verschiedener Deskriptortypen. Jeder Deskriptortyp erfordert eigene spezifische Felder, die im Anfragetext gesendet werden. Siehe [Anhang](#defining-descriptors) für eine vollständige Liste der Deskriptoren und der für ihre Definition erforderlichen Felder.

**API-Format**

```http
POST /tenant/descriptors
```

**Anfrage**

Die folgende Anfrage definiert einen Identitätsdeskriptor für ein Feld „E-Mail-Adresse“ in einem Beispielschema. Diese Funktion [!DNL Experience Platform] , um die E-Mail-Adresse als Kennung zu verwenden, um Informationen über die Person zusammenzufügen.

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

Eine erfolgreiche Antwort gibt den HTTP-Status 201 (Erstellt) und die Details des neu erstellten Deskriptors zurück, einschließlich dessen `@id`. Die `@id` ist ein schreibgeschütztes Feld, das von der [!DNL Schema Registry] und verwendet, um auf den Deskriptor in der API zu verweisen.

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

## Deskriptor aktualisieren {#put}

Sie können einen Deskriptor aktualisieren, indem Sie dessen `@id` im Pfad einer PUT-Anfrage.

**API-Format**

```http
PUT /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{DESCRIPTOR_ID}` | Die `@id` des Deskriptors, den Sie aktualisieren möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Bei dieser Anfrage wird der Deskriptor im Grunde neu geschrieben, sodass der Anfragetext alle Felder enthalten muss, die zur Definition eines Deskriptors dieses Typs erforderlich sind. Anders ausgedrückt: Die Anfrage-Payload zum Aktualisieren (PUT) eines Deskriptors entspricht der Payload zu [Erstellen (POST) eines Deskriptors](#create) denselben Typ aufweisen.

>[!IMPORTANT]
>
>Wie beim Erstellen von Deskriptoren mithilfe von POST-Anfragen erfordert jeder Deskriptortyp, dass eigene spezifische Felder in PUT-Anfrage-Payloads gesendet werden. Siehe [Anhang](#defining-descriptors) für eine vollständige Liste der Deskriptoren und der für ihre Definition erforderlichen Felder.

Im folgenden Beispiel wird ein Identitätsdeskriptor aktualisiert, um auf eine andere `xdm:sourceProperty` (`mobile phone`) und ändern Sie die `xdm:namespace` nach `Phone`.

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

Führen Sie eine [Anfrage zum Nachschlagen (GET)](#lookup) um den Deskriptor anzuzeigen, wird angezeigt, dass die Felder jetzt aktualisiert wurden, um die in der PUT-Anfrage gesendeten Änderungen widerzuspiegeln.

## Deskriptor löschen {#delete}

Gelegentlich müssen Sie möglicherweise einen von Ihnen definierten Deskriptor aus der [!DNL Schema Registry]. Dies erfolgt durch eine DELETE-Anfrage, die auf die `@id` des zu entfernenden Deskriptors verweist.

**API-Format**

```http
DELETE /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{DESCRIPTOR_ID}` | Die `@id` des Deskriptors, den Sie löschen möchten. |

{style=&quot;table-layout:auto&quot;}

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

Um zu bestätigen, dass der Deskriptor gelöscht wurde, können Sie eine [Suchanfrage](#lookup) gegen den Deskriptor `@id`. Die Antwort gibt den HTTP-Status 404 (Nicht gefunden) zurück, da der Deskriptor aus der [!DNL Schema Registry].

## Anhang

Im folgenden Abschnitt finden Sie zusätzliche Informationen zum Arbeiten mit Deskriptoren im [!DNL Schema Registry] API.

### Deskriptoren definieren {#defining-descriptors}

Die folgenden Abschnitte bieten eine Übersicht über die verfügbaren Deskriptortypen, einschließlich der erforderlichen Felder zum Definieren eines Deskriptors für die einzelnen Typen.

#### Identitätsdeskriptor

Ein Identitätsdeskriptor signalisiert, dass der[!UICONTROL sourceProperty]&quot; der &quot;[!UICONTROL sourceSchema]&quot; ist ein [!DNL Identity] -Feld, beschrieben durch [Adobe Experience Platform Identity Service](../../identity-service/home.md).

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
| `@type` | Der Typ des zu definierenden Deskriptors. Für einen Identitätsdeskriptor muss dieser Wert auf `xdm:descriptorIdentity`. |
| `xdm:sourceSchema` | Der `$id`-URI des Schemas, wo der Deskriptor definiert wird. |
| `xdm:sourceVersion` | Die Hauptversion des Quellschemas. |
| `xdm:sourceProperty` | Der Pfad zur spezifischen Eigenschaft, die die Identität sein wird. Der Pfad sollte mit einem „/“ beginnen und nicht mit einem enden. Schließen Sie „properties“ nicht in den Pfad ein (verwenden Sie z. B. „/personalEmail/address“ anstelle von „/properties/personalEmail/properties/address“). |
| `xdm:namespace` | Der `id`- oder `code`-Wert des Identitäts-Namespace. Eine Liste von Namespaces finden Sie unter Verwendung der Variablen [[!DNL Identity Service API]](https://www.adobe.io/experience-platform-apis/references/identity-service). |
| `xdm:property` | Entweder `xdm:id` oder `xdm:code`, je nach verwendetem `xdm:namespace`. |
| `xdm:isPrimary` | Ein optionaler boolescher Wert. Wenn „true“, wird das Feld als primäre Identität angezeigt. Schemas dürfen nur eine primäre Identität enthalten. |

{style=&quot;table-layout:auto&quot;}

#### Anzeigenamendeskriptor {#friendly-name}

Mit Anzeigenamendeskriptoren können Benutzer die `title`, `description`und `meta:enum` -Werte der Schemafelder der Hauptbibliothek. Besonders nützlich sind sie bei der Arbeit mit „eVars“ und anderen „generischen“ Feldern, um Felder zu kennzeichnen, die organisationsspezifische Daten enthalten. Die Benutzeroberfläche kann so einen benutzerfreundlicheren Namen anzeigen oder nur Felder mit einem Anzeigenamen anzeigen.

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
  }
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `@type` | Der Typ des zu definierenden Deskriptors. Bei einem Anzeigenamendeskriptor muss dieser Wert auf `xdm:alternateDisplayInfo`. |
| `xdm:sourceSchema` | Der `$id`-URI des Schemas, wo der Deskriptor definiert wird. |
| `xdm:sourceVersion` | Die Hauptversion des Quellschemas. |
| `xdm:sourceProperty` | Der Pfad zur spezifischen Eigenschaft, die die Identität sein wird. Der Pfad sollte mit einem „/“ beginnen und nicht mit einem enden. Schließen Sie „properties“ nicht in den Pfad ein (verwenden Sie z. B. „/personalEmail/address“ anstelle von „/properties/personalEmail/properties/address“). |
| `xdm:title` | Der neue Titel, den Sie für dieses Feld anzeigen möchten, geschrieben mit großem Anfangsbuchstaben. |
| `xdm:description` | Zusammen mit dem Titel kann eine optionale Beschreibung hinzugefügt werden. |
| `meta:enum` | Wenn das Feld durch `xdm:sourceProperty` ein Zeichenfolgenfeld ist, `meta:enum` bestimmt die Liste der vorgeschlagenen Werte für das Feld im [!DNL Experience Platform] Benutzeroberfläche. Es ist wichtig festzustellen, dass `meta:enum` deklariert keine Auflistung oder stellt keine Datenvalidierung für das XDM-Feld bereit.<br><br>Dies sollte nur für von Adobe definierte Core-XDM-Felder verwendet werden. Wenn die Quelleigenschaft ein von Ihrer Organisation definiertes benutzerdefiniertes Feld ist, sollten Sie stattdessen die `meta:enum` -Eigenschaft direkt über eine PATCH-Anfrage an die übergeordnete Ressource des Felds. |

{style=&quot;table-layout:auto&quot;}

#### Beziehungsdeskriptor

Beziehungsdeskriptoren beschreiben eine Beziehung zwischen zwei verschiedenen Schemas. Sie werden in die Eigenschaften eingegeben, die in `sourceProperty` und `destinationProperty` beschrieben werden. Weiterführende Informationen finden Sie in der Anleitung zum [Definieren einer Beziehung zwischen zwei Schemas](../tutorials/relationship-api.md).

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
| `@type` | Der Typ des zu definierenden Deskriptors. Für einen Beziehungsdeskriptor muss dieser Wert auf `xdm:descriptorOneToOne`. |
| `xdm:sourceSchema` | Der `$id`-URI des Schemas, wo der Deskriptor definiert wird. |
| `xdm:sourceVersion` | Die Hauptversion des Quellschemas. |
| `xdm:sourceProperty` | Der Pfad zum Feld im Quellschema, in dem die Beziehung definiert wird. Sollte mit einem „/“ beginnen und nicht mit einem solchen enden. Schließen Sie „properties“ nicht in den Pfad ein (z. B. „/personalEmail/address“ anstelle von „/properties/personalEmail/properties/address“). |
| `xdm:destinationSchema` | Der `$id`-URI des Zielschemas, mit dem dieser Deskriptor eine Beziehung definiert. |
| `xdm:destinationVersion` | Die Hauptversion des Zielschemas. |
| `xdm:destinationProperty` | Optionaler Pfad zu einem Zielfeld im Zielschema. Wenn diese Eigenschaft weggelassen wird, wird das Zielfeld von allen Feldern mit einem entsprechenden Referenzidentitätsdeskriptor abgeleitet (siehe unten). |

{style=&quot;table-layout:auto&quot;}

#### Referenzidentitätsdeskriptor

Referenzidentitätsdeskriptoren stellen einen Referenzkontext für die primäre Identität eines Schemafelds bereit, der es ermöglicht, von Feldern in anderen Schemas darauf zu verweisen. Felder müssen bereits mit einem Identitätsdeskriptor gekennzeichnet sein, bevor ein Referenzdeskriptor auf sie angewendet werden kann.

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
| `@type` | Der Typ des zu definierenden Deskriptors. Für einen Referenzidentitätsdeskriptor muss dieser Wert auf `xdm:descriptorReferenceIdentity`. |
| `xdm:sourceSchema` | Der `$id`-URI des Schemas, wo der Deskriptor definiert wird. |
| `xdm:sourceVersion` | Die Hauptversion des Quellschemas. |
| `xdm:sourceProperty` | Der Pfad zum Feld im Quellschema, in dem der Deskriptor definiert wird. Sollte mit einem „/“ beginnen und nicht mit einem solchen enden. Schließen Sie „properties“ nicht in den Pfad ein (z. B. „/personalEmail/address“ anstelle von „/properties/personalEmail/properties/address“). |
| `xdm:identityNamespace` | Der Identitäts-Namespace-Code für die Quelleigenschaft. |

{style=&quot;table-layout:auto&quot;}

#### Veralteter Felddeskriptor

Sie können [Verwerfen eines Felds in einer benutzerdefinierten XDM-Ressource](../tutorials/field-deprecation.md#custom) durch Hinzufügen eines `meta:status` -Attribut auf `deprecated` auf das entsprechende Feld. Wenn Sie Felder, die von standardmäßigen XDM-Ressourcen in Ihren Schemas bereitgestellt werden, veraltet sein möchten, können Sie dem betreffenden Schema jedoch einen veralteten Felddeskriptor zuweisen, um denselben Effekt zu erzielen. Verwenden der [korrekt `Accept` header](../tutorials/field-deprecation.md#verify-deprecation)können Sie dann anzeigen, welche Standardfelder für ein Schema nicht mehr unterstützt werden, wenn Sie es in der API nachschlagen.

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
| `@type` | Der Typ des Deskriptors. Für einen Deskriptor zur Einstellung von Feldern muss dieser Wert auf `xdm:descriptorDeprecated`. |
| `xdm:sourceSchema` | Der URI `$id` des Schemas, auf das Sie den Deskriptor anwenden. |
| `xdm:sourceVersion` | Die Version des Schemas, auf das Sie den Deskriptor anwenden. Sollte auf `1`. |
| `xdm:sourceProperty` | Der Pfad zur Eigenschaft innerhalb des Schemas, auf das Sie den Deskriptor anwenden. Wenn Sie den Deskriptor auf mehrere Eigenschaften anwenden möchten, können Sie eine Liste von Pfaden in Form eines Arrays bereitstellen (z. B. `["/firstName", "/lastName"]`). |

{style=&quot;table-layout:auto&quot;}
