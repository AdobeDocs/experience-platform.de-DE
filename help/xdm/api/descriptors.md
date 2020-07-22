---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Deskriptoren
topic: developer guide
translation-type: tm+mt
source-git-commit: b021b6813af18e29f544dc55541f23dd7dd57d47
workflow-type: tm+mt
source-wordcount: '1477'
ht-degree: 81%

---


# Deskriptoren

Schemas definieren eine statische Ansicht von Datenentitäten, geben jedoch nicht spezifisch an, wie sich Daten, die auf diesen Schemas basieren (z. B. Datensätze), zueinander verhalten. Mit Adobe Experience Platform können Sie diese Beziehungen und andere interpretative Metadaten über ein Schema mithilfe von Deskriptoren beschreiben.

Schemadeskriptoren sind Metadaten auf Mandantenebene, das heißt, sie sind für Ihre IMS-Organisation eindeutig und alle Deskriptorvorgänge finden im Mandanten-Container statt.

Auf jedes Schema können eine oder mehrere Schemadeskriptorentitäten angewendet werden. Jede Schemadeskriptorentität enthält einen Deskriptor `@type` und das `sourceSchema`, auf das er angewendet wird. Nach der Anwendung gelten diese Deskriptoren für alle mit dem Schema erstellten Datensätze.

Dieses Dokument enthält Beispiel-API-Aufrufe für Deskriptoren sowie eine vollständige Liste der verfügbaren Deskriptoren und der für die Definition der einzelnen Typen erforderlichen Felder.

>[!NOTE]
>
>Descriptors require unique Accept headers that replace `xed` with `xdm`, but otherwise look very similar to Accept headers used elsewhere in the [!DNL Schema Registry]. Die folgenden Beispielaufrufe enthalten die richtigen Accept-Kopfzeilen. Achten Sie besonders darauf, die richtigen Kopfzeilen zu verwenden.

## Deskriptoren auflisten

Mit einer einzelnen GET-Anfrage können Sie eine Liste aller von Ihrer Organisation definierten Deskriptoren zurückgeben.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xdm-link+json'
```

Das Antwortformat hängt von der Accept-Kopfzeile ab, die in der Anfrage gesendet wird. Notice that the `/descriptors` endpoint uses Accept headers that are different than all other endpoints in the [!DNL Schema Registry] API.

Accept-Kopfzeilen des Deskriptors ersetzen `xed` durch `xdm` und bieten eine `link`-Option, die es nur bei Deskriptoren gibt.

| Accept | Beschreibung |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | Gibt ein Array mit Deskriptorkennungen zurück |
| `application/vnd.adobe.xdm-link+json` | Gibt ein Array mit Deskriptor-API-Pfaden zurück |
| `application/vnd.adobe.xdm+json` | Gibt ein Array mit erweiterten Deskriptorobjekten zurück |

**Antwort**

Die Antwort enthält ein Array für jeden Deskriptortyp, der über definierte Deskriptoren verfügt. Wenn keine Deskriptoren eines bestimmten `@type` definiert sind, gibt die Registrierung also kein leeres Array für diesen Deskriptortyp zurück.

Bei Verwendung der Accept-Kopfzeile `link` wird jeder Deskriptor als Array-Element im Format `/{CONTAINER}/descriptors/{DESCRIPTOR_ID}` angezeigt.

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

## Deskriptor nachschlagen

Wenn Sie die Details eines bestimmten Deskriptors anzeigen möchten, können Sie einen einzelnen Deskriptor mit dessen `@id` nachschlagen (GET).

**API-Format**

```http
GET /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{DESCRIPTOR_ID}` | Die `@id` des Deskriptors, den Sie nachschlagen möchten. |

**Anfrage**

Deskriptoren werden nicht versioniert. Daher ist in der Suchanfrage keine Accept-Kopfzeile erforderlich.

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
  "imsOrg": "{IMS_ORG}",
  "createdClient": "{CREATED_CLIENT}",
  "updatedUser": "{UPDATED_USER}",
  "created": 1548899346989,
  "updated": 1548899346989,
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## Deskriptor erstellen

The [!DNL Schema Registry] allows you to define several different descriptor types. Jeder Deskriptortyp erfordert eigene spezifische Felder, die in der POST-Anfrage gesendet werden. Eine vollständige Liste der Deskriptoren und der für ihre Definition erforderlichen Felder finden Sie im Anhang zum [Definieren von Deskriptoren](#defining-descriptors).

**API-Format**

```http
POST /tenant/descriptors
```

**Anfrage**

Die folgende Anfrage definiert einen Identitätsdeskriptor für ein Feld „E-Mail-Adresse“ in einem Beispielschema. This tells [!DNL Experience Platform] to use the email address as an identifier to help stitch together information about the individual.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Eine erfolgreiche Antwort gibt den HTTP-Status 201 (Erstellt) und die Details des neu erstellten Deskriptors zurück, einschließlich dessen `@id`. The `@id` is a read-only field assigned by the [!DNL Schema Registry] and used for referencing the descriptor in the API.

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

## Deskriptor aktualisieren

Sie können einen Deskriptor aktualisieren, indem Sie im Anfragepfad eine PUT-Anfrage stellen, die auf die `@id` des Deskriptors verweist, den Sie aktualisieren möchten.

**API-Format**

```http
PUT /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{DESCRIPTOR_ID}` | Die `@id` des Deskriptors, den Sie aktualisieren möchten. |

**Anfrage**

Bei dieser Anfrage wird der Deskriptor im Grunde _neu geschrieben_, sodass der Anfragetext alle Felder enthalten muss, die zur Definition eines Deskriptors dieses Typs erforderlich sind. Anders ausgedrückt: Die Anfrage-Payload zum Aktualisieren (PUT) eines Deskriptors ist mit der Payload zum Erstellen (POST) eines Deskriptors desselben Typs identisch.

In diesem Beispiel wird der Identitätsdeskriptor aktualisiert, um auf eine andere `xdm:sourceProperty` („Mobiltelefon“) zu verweisen und den `xdm:namespace` in „Telefon“ zu ändern.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Details zu den Eigenschaften `xdm:namespace` und `xdm:property`, darunter auch über ihren Zugriff, finden Sie im Anhang zum [Definieren von Deskriptoren](#defining-descriptors).

**Antwort**

Bei einer erfolgreichen Antwort werden der HTTP-Status 201 (Erstellt) und die `@id` des aktualisierten Deskriptors zurückgegeben (sie sollte mit der in der Anfrage gesendeten `@id` übereinstimmen).

```JSON
{
    "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

Wenn Sie eine Nachschlageanfrage (GET) zum Anzeigen des Deskriptors ausführen, zeigt sich, dass die Felder jetzt aktualisiert wurden und die in der PUT-Anfrage gesendeten Änderungen widerspiegeln.

## Deskriptor löschen

Occasionally you may need to remove a descriptor that you have defined from the [!DNL Schema Registry]. Dies erfolgt durch eine DELETE-Anfrage, die auf die `@id` des zu entfernenden Deskriptors verweist.

**API-Format**

```http
DELETE /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{DESCRIPTOR_ID}` | Die `@id` des Deskriptors, den Sie löschen möchten. |

**Anfrage**

Accept-Kopfzeilen sind beim Löschen von Deskriptoren nicht erforderlich.

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/ca921946fb5281cbdb8ba5e07087486ce531a1f2  \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 204 (Kein Inhalt) und einen leeren Text zurück.

Um sich zu vergewissern, dass der Deskriptor gelöscht wurde, können Sie eine Suchanfrage nach der `@id` des Deskriptors durchführen. The response returns HTTP status 404 (Not Found) because the descriptor has been removed from the [!DNL Schema Registry].

## Anhang

The following section provides additional information regarding working with descriptors in the [!DNL Schema Registry] API.

### Deskriptoren definieren

Die folgenden Abschnitte bieten eine Übersicht über die verfügbaren Deskriptortypen, einschließlich der erforderlichen Felder zum Definieren eines Deskriptors für die einzelnen Typen.

#### Identitätsdeskriptor

An identity descriptor signals that the &quot;[!UICONTROL sourceProperty]&quot; of the &quot;[!UICONTROL sourceSchema]&quot; is an [!DNL Identity] field as described by [Adobe Experience Platform Identity Service](../../identity-service/home.md).

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
| `@type` | Der Typ des zu definierenden Deskriptors. |
| `xdm:sourceSchema` | Der `$id`-URI des Schemas, wo der Deskriptor definiert wird. |
| `xdm:sourceVersion` | Die Hauptversion des Quellschemas. |
| `xdm:sourceProperty` | Der Pfad zur spezifischen Eigenschaft, die die Identität sein wird. Der Pfad sollte mit einem „/“ beginnen und nicht mit einem enden. Schließen Sie „properties“ nicht in den Pfad ein (verwenden Sie z. B. „/personalEmail/address“ anstelle von „/properties/personalEmail/properties/address“). |
| `xdm:namespace` | Der `id`- oder `code`-Wert des Identitäts-Namespace. A list of namespaces can be found using the [!DNL Identity Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml). |
| `xdm:property` | Entweder `xdm:id` oder `xdm:code`, je nach verwendetem `xdm:namespace`. |
| `xdm:isPrimary` | Ein optionaler boolescher Wert. Wenn „true“, wird das Feld als primäre Identität angezeigt. Schemas dürfen nur eine primäre Identität enthalten. |

#### Anzeigenamendeskriptor

Friendly name descriptors allow a user to modify the `title`, `description`, and `meta:enum` values of the core library schema fields. Besonders nützlich sind sie bei der Arbeit mit „eVars“ und anderen „generischen“ Feldern, um Felder zu kennzeichnen, die organisationsspezifische Daten enthalten. Die Benutzeroberfläche kann so einen benutzerfreundlicheren Namen anzeigen oder nur Felder mit einem Anzeigenamen anzeigen.

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
| `@type` | Der Typ des zu definierenden Deskriptors. |
| `xdm:sourceSchema` | Der `$id`-URI des Schemas, wo der Deskriptor definiert wird. |
| `xdm:sourceVersion` | Die Hauptversion des Quellschemas. |
| `xdm:sourceProperty` | Der Pfad zur spezifischen Eigenschaft, die die Identität sein wird. Der Pfad sollte mit einem „/“ beginnen und nicht mit einem enden. Schließen Sie „properties“ nicht in den Pfad ein (verwenden Sie z. B. „/personalEmail/address“ anstelle von „/properties/personalEmail/properties/address“). |
| `xdm:title` | Der neue Titel, den Sie für dieses Feld anzeigen möchten, geschrieben mit großem Anfangsbuchstaben. |
| `xdm:description` | Zusammen mit dem Titel kann eine optionale Beschreibung hinzugefügt werden. |
| `meta:enum` | Wenn das angegebene Feld ein Zeichenfolgenfeld `xdm:sourceProperty` ist, `meta:enum` bestimmt es die Liste der vorgeschlagenen Werte für das Feld in der [!DNL Experience Platform] Benutzeroberfläche. Beachten Sie, dass keine Auflistung deklariert oder eine Datenvalidierung für das XDM-Feld bereitgestellt `meta:enum` wird.<br><br>Dies sollte nur für von Adobe definierte Kern-XDM-Felder verwendet werden. Wenn es sich bei der source-Eigenschaft um ein von Ihrer Organisation definiertes benutzerdefiniertes Feld handelt, sollten Sie stattdessen die `meta:enum` Eigenschaft des Felds direkt über eine [PATCH-Anforderung](./update-resource.md)bearbeiten. |

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
| `@type` | Der Typ des zu definierenden Deskriptors. |
| `xdm:sourceSchema` | Der `$id`-URI des Schemas, wo der Deskriptor definiert wird. |
| `xdm:sourceVersion` | Die Hauptversion des Quellschemas. |
| `xdm:sourceProperty` | Der Pfad zum Feld im Quellschema, in dem die Beziehung definiert wird. Sollte mit einem „/“ beginnen und nicht mit einem solchen enden. Schließen Sie „properties“ nicht in den Pfad ein (z. B. „/personalEmail/address“ anstelle von „/properties/personalEmail/properties/address“). |
| `xdm:destinationSchema` | Der `$id`-URI des Zielschemas, mit dem dieser Deskriptor eine Beziehung definiert. |
| `xdm:destinationVersion` | Die Hauptversion des Zielschemas. |
| `xdm:destinationProperty` | Optionaler Pfad zu einem Zielfeld im Zielschema. Wenn diese Eigenschaft weggelassen wird, wird das Zielfeld von allen Feldern mit einem entsprechenden Referenzidentitätsdeskriptor abgeleitet (siehe unten). |


#### Referenzidentitätsdeskriptor

Referenz-Identitätsdeskriptoren stellen einen Referenzkontext zur primären Identität eines Schema-Felds bereit, sodass auf dieses durch Felder in anderen Schemas verwiesen werden kann. Felder müssen bereits mit einem Identitätsdeskriptor gekennzeichnet sein, bevor ein Referenzdeskriptor auf sie angewendet werden kann.

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
| `@type` | Der Typ des zu definierenden Deskriptors. |
| `xdm:sourceSchema` | Der `$id`-URI des Schemas, wo der Deskriptor definiert wird. |
| `xdm:sourceVersion` | Die Hauptversion des Quellschemas. |
| `xdm:sourceProperty` | Der Pfad zum Feld im Quellschema, in dem der Deskriptor definiert wird. Sollte mit einem „/“ beginnen und nicht mit einem solchen enden. Schließen Sie „properties“ nicht in den Pfad ein (z. B. „/personalEmail/address“ anstelle von „/properties/personalEmail/properties/address“). |
| `xdm:identityNamespace` | Der Identitäts-Namespace-Code für die Quelleigenschaft. |