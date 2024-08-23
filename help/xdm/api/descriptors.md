---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM;XDM-System;Experience-Datenmodell;Experience-Datenmodell;Experience-Datenmodell;Datenmodell;Datenmodell;Schemaregistrierung;Schema;Deskriptor;Deskriptoren;Identität;Anzeigename;Anzeigename;alternativeDisplayInfo;Referenz;Beziehung;Beziehung
solution: Experience Platform
title: Deskriptoren-API-Endpunkt
description: Mit dem Endpunkt /descriptors in der Schema Registry-API können Sie XDM-Deskriptoren in Ihrer Erlebnisanwendung programmgesteuert verwalten.
exl-id: bda1aabd-5e6c-454f-a039-ec22c5d878d2
source-git-commit: 866e00459c66ea4678cd98d119a7451fd8e78253
workflow-type: tm+mt
source-wordcount: '1920'
ht-degree: 40%

---

# Deskriptoren-Endpunkt

Schemata definieren eine statische Ansicht von Datenentitäten, geben jedoch nicht spezifisch an, wie sich Daten, die auf diesen Schemata basieren (z. B. Datensätze), zueinander verhalten. Mit Adobe Experience Platform können Sie diese Beziehungen und andere interpretative Metadaten über ein Schema mithilfe von Deskriptoren beschreiben.

Schemadeskriptoren sind Metadaten auf Mandantenebene, d. h. sie sind für Ihre Organisation eindeutig und alle Deskriptorvorgänge finden im Mandanten-Container statt.

Auf jedes Schema können eine oder mehrere Schemadeskriptorentitäten angewendet werden. Jede Schemadeskriptorentität enthält einen Deskriptor `@type` und das `sourceSchema`, auf das er angewendet wird. Nach der Anwendung gelten diese Deskriptoren für alle mit dem Schema erstellten Datensätze.

Mit dem Endpunkt `/descriptors` in der API [!DNL Schema Registry] können Sie Deskriptoren in Ihrer Erlebnisanwendung programmgesteuert verwalten.

## Erste Schritte

Der in diesem Handbuch verwendete Endpunkt ist Teil der [[!DNL Schema Registry] API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Bevor Sie fortfahren, lesen Sie das Handbuch [Erste Schritte](./getting-started.md) mit Links zur zugehörigen Dokumentation, einer Anleitung zum Lesen der API-Beispielaufrufe in diesem Dokument und wichtigen Informationen zu den erforderlichen Kopfzeilen, die für die erfolgreiche Ausführung von Aufrufen an eine Experience Platform-API erforderlich sind.

## Abrufen einer Liste von Deskriptoren {#list}

Sie können alle von Ihrem Unternehmen definierten Deskriptoren auflisten, indem Sie eine GET-Anfrage an `/tenant/descriptors` richten.

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

Das Antwortformat hängt von der in der Anfrage gesendeten `Accept` -Kopfzeile ab. Beachten Sie, dass der Endpunkt `/descriptors` `Accept` -Kopfzeilen verwendet, die sich von allen anderen Endpunkten in der [!DNL Schema Registry] -API unterscheiden.

>[!IMPORTANT]
>
>Deskriptoren erfordern eindeutige `Accept` -Header, die `xed` durch `xdm` ersetzen, und bieten außerdem eine `link` -Option, die für Deskriptoren eindeutig ist. Die korrekten `Accept` -Header wurden in den Beispielaufrufen unten aufgeführt. Achten Sie jedoch besonders darauf, dass beim Arbeiten mit Deskriptoren die richtigen Header verwendet werden.

| `Accept`-Kopfzeile | Beschreibung |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | Gibt ein Array mit Deskriptorkennungen zurück |
| `application/vnd.adobe.xdm-link+json` | Gibt ein Array mit Deskriptor-API-Pfaden zurück |
| `application/vnd.adobe.xdm+json` | Gibt ein Array mit erweiterten Deskriptorobjekten zurück |
| `application/vnd.adobe.xdm-v2+json` | Diese `Accept` -Kopfzeile muss verwendet werden, um Paging-Funktionen zu verwenden. |

{style="table-layout:auto"}

**Antwort**

Die Antwort enthält ein Array für jeden Deskriptortyp, der über definierte Deskriptoren verfügt. Wenn keine Deskriptoren eines bestimmten `@type` definiert sind, gibt die Registrierung also kein leeres Array für diesen Deskriptortyp zurück.

Bei Verwendung der Kopfzeile `link` `Accept` wird jeder Deskriptor als Array-Element im Format `/{CONTAINER}/descriptors/{DESCRIPTOR_ID}` angezeigt

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

{style="table-layout:auto"}

**Anfrage**

Die folgende Anfrage ruft einen Deskriptor anhand seines `@id` -Werts ab. Deskriptoren werden nicht versioniert, daher ist in der Suchanfrage kein `Accept` -Header erforderlich.

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

Sie können einen neuen Deskriptor erstellen, indem Sie eine POST-Anfrage an den Endpunkt `/tenant/descriptors` senden.

>[!IMPORTANT]
>
>Mit dem [!DNL Schema Registry] können Sie mehrere verschiedene Deskriptortypen definieren. Jeder Deskriptortyp erfordert eigene spezifische Felder, die im Anfragetext gesendet werden. Eine vollständige Liste der Deskriptoren und der zu ihrer Definition erforderlichen Felder finden Sie im [Anhang](#defining-descriptors) .

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

Eine erfolgreiche Antwort gibt den HTTP-Status 201 (Erstellt) und die Details des neu erstellten Deskriptors zurück, einschließlich dessen `@id`. Die `@id` ist ein schreibgeschütztes Feld, das von der [!DNL Schema Registry] zugewiesen und zum Verweisen auf den Deskriptor in der API verwendet wird.

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

Sie können einen Deskriptor aktualisieren, indem Sie dessen `@id` in den Pfad einer PUT-Anfrage einschließen.

**API-Format**

```http
PUT /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{DESCRIPTOR_ID}` | Die `@id` des Deskriptors, den Sie aktualisieren möchten. |

{style="table-layout:auto"}

**Anfrage**

Diese Anfrage schreibt den Deskriptor im Wesentlichen neu, sodass der Anfragetext alle Felder enthalten muss, die zum Definieren eines Deskriptors dieses Typs erforderlich sind. Anders ausgedrückt: Die Anfrage-Payload zum Aktualisieren (PUT) eines Deskriptors entspricht der Payload zum Erstellen (POST) eines Deskriptors](#create) desselben Typs durch [Erstellen (Deskriptor).

>[!IMPORTANT]
>
>Wie beim Erstellen von Deskriptoren mithilfe von POST-Anfragen erfordert jeder Deskriptortyp, dass eigene spezifische Felder in PUT-Anfrage-Payloads gesendet werden. Eine vollständige Liste der Deskriptoren und der zu ihrer Definition erforderlichen Felder finden Sie im [Anhang](#defining-descriptors) .

Im folgenden Beispiel wird ein Identitätsdeskriptor aktualisiert, um auf einen anderen `xdm:sourceProperty` (`mobile phone`) zu verweisen, und der `xdm:namespace` wird in `Phone` geändert.

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

Wenn Sie eine [Nachschlageanfrage (GET)](#lookup) zum Anzeigen des Deskriptors ausführen, wird angezeigt, dass die Felder jetzt aktualisiert wurden, um die in der PUT-Anfrage gesendeten Änderungen widerzuspiegeln.

## Deskriptor löschen {#delete}

Gelegentlich müssen Sie möglicherweise einen von Ihnen definierten Deskriptor aus dem [!DNL Schema Registry] entfernen. Dies geschieht durch eine DELETE-Anfrage, die auf die `@id` des Deskriptors verweist, den Sie entfernen möchten.

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

Um zu bestätigen, dass der Deskriptor gelöscht wurde, können Sie eine [Suchanfrage](#lookup) für den Deskriptor `@id` ausführen. Die Antwort gibt den HTTP-Status 404 (Nicht gefunden) zurück, da der Deskriptor aus dem [!DNL Schema Registry] entfernt wurde.

## Anhang

Im folgenden Abschnitt finden Sie zusätzliche Informationen zum Arbeiten mit Deskriptoren in der [!DNL Schema Registry]-API.

### Deskriptoren definieren {#defining-descriptors}

>[!NOTE]
>
>Die maximale Anzahl von Deskriptoren, die auf die Sandbox eines Unternehmens angewendet werden können, beträgt 4000.

Die folgenden Abschnitte bieten eine Übersicht über die verfügbaren Deskriptortypen, einschließlich der erforderlichen Felder zum Definieren eines Deskriptors für die einzelnen Typen.

>[!IMPORTANT]
>
>Sie können das Namespace-Objekt des Mandanten nicht beschriften, da das System diese Beschriftung auf jedes benutzerdefinierte Feld in dieser Sandbox anwenden würde. Stattdessen müssen Sie den Blattknoten unter dem Objekt angeben, das Sie beschriften müssen.

#### Identitätsdeskriptor

Ein Identitätsdeskriptor signalisiert, dass &quot;[!UICONTROL sourceProperty]&quot;des &quot;[!UICONTROL sourceSchema]&quot;ein [!DNL Identity] -Feld ist, wie in [Adobe Experience Platform Identity Service](../../identity-service/home.md) beschrieben.

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
| `@type` | Der Typ des definierten Deskriptors. Für einen Identitätsdeskriptor muss dieser Wert auf `xdm:descriptorIdentity` gesetzt werden. |
| `xdm:sourceSchema` | Der `$id`-URI des Schemas, wo der Deskriptor definiert wird. |
| `xdm:sourceVersion` | Die Hauptversion des Quellschemas. |
| `xdm:sourceProperty` | Der Pfad zur spezifischen Eigenschaft, die die Identität sein wird. Der Pfad sollte mit einem „/“ beginnen und nicht mit einem enden. Schließen Sie &quot;properties&quot;nicht in den Pfad ein (verwenden Sie beispielsweise &quot;/personalEmail/address&quot;anstelle von &quot;/properties/personalEmail/properties/address&quot;) |
| `xdm:namespace` | Der `id`- oder `code`-Wert des Identitäts-Namespace. Eine Liste von Namespaces finden Sie mit dem Tag [[!DNL Identity Service API]](https://developer.adobe.com/experience-platform-apis/references/identity-service). |
| `xdm:property` | Entweder `xdm:id` oder `xdm:code`, je nach verwendetem `xdm:namespace`. |
| `xdm:isPrimary` | Ein optionaler boolescher Wert. Wenn „true“, wird das Feld als primäre Identität angezeigt. Schemata dürfen nur eine primäre Identität enthalten. |

{style="table-layout:auto"}

#### Anzeigenamendeskriptor {#friendly-name}

Mit Anzeigenamendeskriptoren können Benutzer die Werte `title`, `description` und `meta:enum` der Schemafelder der Hauptbibliothek ändern. Besonders nützlich sind sie bei der Arbeit mit „eVars“ und anderen „generischen“ Feldern, um Felder zu kennzeichnen, die organisationsspezifische Daten enthalten. Die Benutzeroberfläche kann so einen benutzerfreundlicheren Namen anzeigen oder nur Felder mit einem Anzeigenamen anzeigen.

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
| `@type` | Der Typ des definierten Deskriptors. Für einen Anzeigenamendeskriptor muss dieser Wert auf `xdm:alternateDisplayInfo` gesetzt werden. |
| `xdm:sourceSchema` | Der `$id`-URI des Schemas, wo der Deskriptor definiert wird. |
| `xdm:sourceVersion` | Die Hauptversion des Quellschemas. |
| `xdm:sourceProperty` | Der Pfad zur spezifischen Eigenschaft, deren Details Sie ändern möchten. Der Pfad sollte mit einem Schrägstrich (`/`) beginnen und nicht mit einem Schrägstrich enden. Fügen Sie im Pfad nicht `properties` ein (verwenden Sie beispielsweise `/personalEmail/address` anstelle von `/properties/personalEmail/properties/address`). |
| `xdm:title` | Der neue Titel, den Sie für dieses Feld anzeigen möchten, geschrieben in Titelschreibweise. |
| `xdm:description` | Zusammen mit dem Titel kann eine optionale Beschreibung hinzugefügt werden. |
| `meta:enum` | Wenn das durch `xdm:sourceProperty` angegebene Feld ein Zeichenfolgenfeld ist, kann `meta:enum` verwendet werden, um die vorgeschlagenen Werte für das Feld in der Segmentierungsbenutzeroberfläche hinzuzufügen. Beachten Sie, dass `meta:enum` keine Auflistung deklariert oder keine Datenvalidierung für das XDM-Feld bereitstellt.<br><br>Dies sollte nur für von Adobe definierte Core-XDM-Felder verwendet werden. Wenn es sich bei der Quelleigenschaft um ein von Ihrem Unternehmen definiertes benutzerdefiniertes Feld handelt, sollten Sie stattdessen die Eigenschaft `meta:enum` des Felds direkt über eine PATCH-Anfrage an die übergeordnete Ressource des Felds bearbeiten. |
| `meta:excludeMetaEnum` | Wenn das durch `xdm:sourceProperty` angegebene Feld ein Zeichenfolgenfeld ist, für das unter einem `meta:enum` -Feld vorhandene empfohlene Werte bereitgestellt werden, können Sie dieses Objekt in einen Anzeigenamendeskriptor einschließen, um einige oder alle dieser Werte aus der Segmentierung auszuschließen. Schlüssel und Wert für jeden Eintrag müssen mit denen im ursprünglichen Feld `meta:enum` übereinstimmen, damit der Eintrag ausgeschlossen wird. |

{style="table-layout:auto"}

#### Beziehungsdeskriptor

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
| `@type` | Der Typ des definierten Deskriptors. Für einen Beziehungsdeskriptor muss dieser Wert auf `xdm:descriptorOneToOne` gesetzt werden. |
| `xdm:sourceSchema` | Der `$id`-URI des Schemas, wo der Deskriptor definiert wird. |
| `xdm:sourceVersion` | Die Hauptversion des Quellschemas. |
| `xdm:sourceProperty` | Der Pfad zum Feld im Quellschema, in dem die Beziehung definiert wird. Sollte mit einem „/“ beginnen und nicht mit einem solchen enden. Schließen Sie „properties“ nicht in den Pfad ein (z. B. „/personalEmail/address“ anstelle von „/properties/personalEmail/properties/address“). |
| `xdm:destinationSchema` | Der `$id` -URI des Referenzschemas, mit dem dieser Deskriptor eine Beziehung definiert. |
| `xdm:destinationVersion` | Die Hauptversion des Referenzschemas. |
| `xdm:destinationProperty` | Optionaler Pfad zu einem Zielfeld im Referenzschema. Wenn diese Eigenschaft weggelassen wird, wird das Zielfeld von allen Feldern mit einem entsprechenden Referenzidentitätsdeskriptor abgeleitet (siehe unten). |

{style="table-layout:auto"}

#### Referenzidentitätsdeskriptor

Referenzidentitätsdeskriptoren stellen einen Referenzkontext für die primäre Identität eines Schemafelds bereit, der es ermöglicht, von Feldern in anderen Schemas darauf zu verweisen. Das Referenzschema muss bereits über ein primäres Identitätsfeld verfügen, bevor über diesen Deskriptor andere Schemas auf dieses Feld verweisen können.

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
| `@type` | Der Typ des definierten Deskriptors. Für einen Referenzidentitätsdeskriptor muss dieser Wert auf `xdm:descriptorReferenceIdentity` gesetzt werden. |
| `xdm:sourceSchema` | Der `$id`-URI des Schemas, wo der Deskriptor definiert wird. |
| `xdm:sourceVersion` | Die Hauptversion des Quellschemas. |
| `xdm:sourceProperty` | Pfad zum Feld im Quellschema, das zum Verweis auf das Referenzschema verwendet wird. Sollte mit einem „/“ beginnen und nicht mit einem solchen enden. Schließen Sie &quot;properties&quot;nicht in den Pfad ein (z. B. `/personalEmail/address` anstelle von `/properties/personalEmail/properties/address`). |
| `xdm:identityNamespace` | Der Identitäts-Namespace-Code für die Quelleigenschaft. |

{style="table-layout:auto"}

#### Veralteter Felddeskriptor

Sie können ein Feld innerhalb einer benutzerdefinierten XDM-Ressource ](../tutorials/field-deprecation-api.md#custom) [ als veraltet kennzeichnen, indem Sie dem betreffenden Feld ein auf `deprecated` eingestelltes `meta:status` -Attribut hinzufügen. Wenn Sie Felder, die von standardmäßigen XDM-Ressourcen in Ihren Schemas bereitgestellt werden, veraltet sein möchten, können Sie dem betreffenden Schema jedoch einen veralteten Felddeskriptor zuweisen, um denselben Effekt zu erzielen. Mithilfe der [korrekten `Accept` -Kopfzeile](../tutorials/field-deprecation-api.md#verify-deprecation) können Sie dann anzeigen, welche Standardfelder für ein Schema veraltet sind, wenn Sie es in der API nachschlagen.

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
