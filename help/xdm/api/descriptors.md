---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Deskriptoren
topic: developer guide
translation-type: tm+mt
source-git-commit: 599991af774e283d9fb60216e3d3bd5b17cf8193
workflow-type: tm+mt
source-wordcount: '1420'
ht-degree: 1%

---


# Deskriptoren

Schema definieren eine statische Ansicht von Datenentitäten, geben jedoch keine spezifischen Informationen darüber an, wie sich Daten, die auf diesen Schemas basieren (z. B. Datensätze), zueinander verhalten können. Mit Adobe Experience Platform können Sie diese Beziehungen und andere interpretative Metadaten zu einem Schema mithilfe von Deskriptoren beschreiben.

Schema-Deskriptoren sind Metadaten auf Pächter-Ebene, d. h. sie sind für Ihre IMS-Organisation eindeutig und alle Deskriptorvorgänge finden im Pächter-Container statt.

Auf jedes Schema können eine oder mehrere Schema-Deskriptorentitäten angewendet werden. Jede Schema-Deskriptor-Entität enthält einen Deskriptor `@type` und die `sourceSchema` zutreffende. Nach der Anwendung gelten diese Deskriptoren für alle mit dem Schema erstellten Datensätze.

Dieses Dokument enthält Beispiel-API-Aufrufe für Deskriptoren sowie eine vollständige Liste der verfügbaren Deskriptoren und der für die Definition der einzelnen Typen erforderlichen Felder.

>[!NOTE] Deskriptoren erfordern eindeutige Accept-Header, die `xed` `xdm`durch ersetzt werden, aber ansonsten sehr ähnlich aussehen wie Accept-Header, die andernorts in der Schema-Registrierung verwendet werden. Die folgenden Beispielaufrufe enthalten die richtigen Accept-Header. Achten Sie jedoch besonders darauf, dass die richtigen Header verwendet werden.

## Deskriptoren für Listen

Eine einzelne GET-Anforderung kann verwendet werden, um eine Liste aller von Ihrem Unternehmen definierten Deskriptoren zurückzugeben.

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

Das Antwortformat hängt vom Accept-Header ab, der in der Anforderung gesendet wird. Beachten Sie, dass der `/descriptors` Endpunkt Accept-Kopfzeilen verwendet, die sich von allen anderen Endpunkten in der Schema Registry-API unterscheiden.

Die Kopfzeilen des Beschreibers mit Akzeptanz ersetzen `xed` durch `xdm`und Angebot eine `link` Option, die für Deskriptoren eindeutig ist.

| Accept | Beschreibung |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | Gibt ein Array mit Deskriptor-IDs zurück |
| `application/vnd.adobe.xdm-link+json` | Gibt ein Array mit Deskriptor-API-Pfaden zurück |
| `application/vnd.adobe.xdm+json` | Gibt ein Array mit erweiterten Deskriptorobjekten zurück |

**Antwort**

Die Antwort enthält ein Array für jeden Deskriptortyp mit definierten Deskriptoren. Wenn also keine Deskriptoren einer bestimmten `@type` Definition vorhanden sind, gibt die Registrierung kein leeres Array für diesen Deskriptortyp zurück.

Bei Verwendung der Kopfzeile &quot; `link` Accept&quot;wird jeder Deskriptor als Array-Element im Format `/{CONTAINER}/descriptors/{DESCRIPTOR_ID}`

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

Wenn Sie die Details eines bestimmten Deskriptors Ansicht wünschen, können Sie einen einzelnen Deskriptor mit dessen `@id`Funktion nachschlagen (GET).

**API-Format**

```http
GET /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{DESCRIPTOR_ID}` | Der `@id` Deskriptor, den Sie suchen möchten. |

**Anfrage**

Deskriptoren sind nicht versioniert. Daher ist in der Suchanfrage kein Accept-Header erforderlich.

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details des Deskriptors zurück, einschließlich der zugehörigen `@type` und `sourceSchema`sowie zusätzliche Informationen, die je nach Deskriptortyp variieren. Die zurückgegebene Datei `@id` sollte mit dem in der Anforderung `@id` bereitgestellten Deskriptor übereinstimmen.

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

Mit der Schema-Registrierung können Sie verschiedene Deskriptortypen definieren. Jeder Deskriptortyp erfordert eigene spezifische Felder, die in der POST-Anforderung gesendet werden. Eine vollständige Liste der Deskriptoren und der zu ihrer Definition erforderlichen Felder finden Sie im Anhang zur [Definition der Deskriptoren](#defining-descriptors).

**API-Format**

```http
POST /tenant/descriptors
```

**Anfrage**

Die folgende Anforderung definiert einen Identitätsdeskriptor für ein &quot;E-Mail-Adresse&quot;-Feld in einem Beispiel-Schema. Dadurch wird Experience Platform angewiesen, die E-Mail-Adresse als ID zu verwenden, um Informationen über die Person zusammenzufügen.

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

Eine erfolgreiche Antwort gibt HTTP-Status 201 (Erstellt) und die Details des neu erstellten Deskriptors zurück, einschließlich dessen `@id`. Das `@id` ist ein schreibgeschütztes Feld, das von der Schema-Registrierung zugewiesen wurde und zum Verweisen auf den Deskriptor in der API verwendet wird.

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

## Updatedeskriptor

Sie können einen Deskriptor aktualisieren, indem Sie eine PUT-Anforderung erstellen, die auf die Beschreibung `@id` des Deskriptors verweist, den Sie im Anforderungspfad aktualisieren möchten.

**API-Format**

```http
PUT /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{DESCRIPTOR_ID}` | Der `@id` Deskriptor, den Sie aktualisieren möchten. |

**Anfrage**

Bei dieser Anforderung wird der Deskriptor im Wesentlichen _neu geschrieben_ , sodass der Anforderungstext alle Felder enthalten muss, die zur Definition eines Deskriptors dieses Typs erforderlich sind. Anders ausgedrückt, ist die Anforderungs-Nutzlast zum Aktualisieren (PUT) eines Deskriptors mit der Nutzlast identisch, um einen Deskriptor desselben Typs zu erstellen (POST).

In diesem Beispiel wird der Identitätsdeskriptor aktualisiert, um auf ein anderes `xdm:sourceProperty` (&quot;Mobiltelefon&quot;) zu verweisen und es in &quot;Telefon&quot; `xdm:namespace` zu ändern.

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

Details zu den Eigenschaften `xdm:namespace` und `xdm:property`wie auf sie zugegriffen werden kann, finden Sie im Anhang zur [Definition von Deskriptoren](#defining-descriptors).

**Antwort**

Bei einer erfolgreichen Antwort werden HTTP-Status 201 (Erstellt) und der Name `@id` des aktualisierten Deskriptors zurückgegeben (der mit dem in der Anforderung gesendeten `@id` Wert übereinstimmen sollte).

```JSON
{
    "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

Wenn Sie eine Nachschlageanforderung (GET) zur Ansicht des Deskriptors ausführen, zeigt der Deskriptor, dass die Felder jetzt aktualisiert wurden, um die in der PUT-Anforderung gesendeten Änderungen widerzuspiegeln.

## Deskriptor löschen

Gelegentlich müssen Sie einen von Ihnen definierten Deskriptor aus der Schema-Registrierung entfernen. Dies erfolgt durch eine DELETE-Anforderung, die auf die Beschreibung `@id` des zu entfernenden Deskriptors verweist.

**API-Format**

```http
DELETE /tenant/descriptors/{DESCRIPTOR_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{DESCRIPTOR_ID}` | Der `@id` Deskriptor, den Sie löschen möchten. |

**Anfrage**

Akzeptierte Kopfzeilen sind beim Löschen von Deskriptoren nicht erforderlich.

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/ca921946fb5281cbdb8ba5e07087486ce531a1f2  \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 204 (Kein Inhalt) und einen leeren Text zurück.

Um zu bestätigen, dass der Deskriptor gelöscht wurde, können Sie eine Suchanfrage für den Deskriptor durchführen `@id`. Die Antwort gibt HTTP-Status 404 (Nicht gefunden) zurück, da der Deskriptor aus der Schema-Registrierung entfernt wurde.

## Anhang

Im folgenden Abschnitt finden Sie weitere Informationen zum Arbeiten mit Deskriptoren in der Schema Registry API.

### Definieren von Deskriptoren

Die folgenden Abschnitte enthalten eine Übersicht der verfügbaren Deskriptortypen, einschließlich der erforderlichen Felder zum Definieren eines Deskriptors für jeden Typ.

#### Identitätsdeskriptor

Ein Identitätsdeskriptor signalisiert, dass &quot;sourceProperty&quot;des &quot;sourceSchema&quot;ein Identitätsfeld ist, wie vom [Adobe Experience Platform-Identitätsdienst](../../identity-service/home.md)beschrieben.

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
| `xdm:sourceSchema` | Der `$id` URI des Schemas, in dem der Deskriptor definiert wird. |
| `xdm:sourceVersion` | Die Hauptversion des Quell-Schemas. |
| `xdm:sourceProperty` | Der Pfad zur spezifischen Eigenschaft, die die Identität sein soll. Pfad sollte mit einem &quot;/&quot;beginnen und nicht mit einem enden. &quot;Eigenschaften&quot;nicht in den Pfad einschließen (z. B. &quot;/personalEmail/address&quot;anstelle von &quot;/properties/personalEmail/properties/address&quot;) |
| `xdm:namespace` | Der `id` oder `code` -Wert des Identitäts-Namensraums. Eine Liste von Namensräumen finden Sie mit der [Identitätsdienst-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml). |
| `xdm:property` | Entweder `xdm:id` oder `xdm:code`, je nach `xdm:namespace` verwendetem Gerät. |
| `xdm:isPrimary` | Ein optionaler boolescher Wert. Wenn &quot;true&quot;, wird das Feld als primäre Identität angezeigt. Schema dürfen nur eine primäre Identität enthalten. |

#### Anzeigename-Deskriptor

Mit benutzerfreundlichen Namensdeskriptoren können Sie die `title` und `description` Werte der Schema-Kernfelder der Bibliothek ändern. Besonders nützlich bei der Arbeit mit &quot;eVars&quot;und anderen &quot;generischen&quot;Feldern, die als mit unternehmensspezifischen Informationen gekennzeichnete Felder gekennzeichnet werden sollen. Die Benutzeroberfläche kann diese verwenden, um einen benutzerfreundlicheren Namen anzuzeigen oder nur Felder mit einem benutzerfreundlichen Namen anzuzeigen.

```json
{
  "@type": "xdm:alternateDisplayInfo",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
  "xdm:sourceVersion": 1
  "xdm:sourceProperty": "/eVars/eVar1",
  "xdm:title": {
    "en_us":{"Loyalty ID"}
  },
  "xdm:description": {
    "en_us":{"Unique ID of loyalty program member."}
  },
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `@type` | Der Typ des zu definierenden Deskriptors. |
| `xdm:sourceSchema` | Der `$id` URI des Schemas, in dem der Deskriptor definiert wird. |
| `xdm:sourceVersion` | Die Hauptversion des Quell-Schemas. |
| `xdm:sourceProperty` | Der Pfad zur spezifischen Eigenschaft, die die Identität sein soll. Pfad sollte mit einem &quot;/&quot;beginnen und nicht mit einem enden. &quot;Eigenschaften&quot;nicht in den Pfad einschließen (z. B. &quot;/personalEmail/address&quot;anstelle von &quot;/properties/personalEmail/properties/address&quot;) |
| `xdm:title` | Der neue Titel, den Sie für dieses Feld anzeigen möchten, geschrieben in der Titelleiste. |
| `xdm:description` | Eine optionale Beschreibung kann zusammen mit dem Titel hinzugefügt werden. |

#### Beziehungsdeskriptor

Beziehungsdeskriptoren beschreiben eine Beziehung zwischen zwei verschiedenen Schemas, die auf den unter `sourceProperty` und `destinationProperty`beschriebenen Eigenschaften keyed sind. Weitere Informationen finden Sie im Lernprogramm zum [Definieren einer Beziehung zwischen zwei Schemas](../tutorials/relationship-api.md) .

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
| `xdm:sourceSchema` | Der `$id` URI des Schemas, in dem der Deskriptor definiert wird. |
| `xdm:sourceVersion` | Die Hauptversion des Quell-Schemas. |
| `xdm:sourceProperty` | Pfad zum Feld im Quellfeld, in dem die Beziehung definiert wird. Sollte mit einem &quot;/&quot;beginnen und nicht mit einem enden. Schließen Sie nicht &quot;Eigenschaften&quot;in den Pfad ein (z. B. &quot;/personalEmail/address&quot;anstelle von &quot;/properties/personalEmail/properties/address&quot;). |
| `xdm:destinationSchema` | Der `$id` URI des Ziel-Schemas, mit dem dieser Deskriptor eine Beziehung definiert. |
| `xdm:destinationVersion` | Die Hauptversion des Ziel-Schemas. |
| `xdm:destinationProperty` | Optionaler Pfad zu einem Feld &quot;Zielgruppe&quot;im Schema &quot;Ziel&quot;. Wenn diese Eigenschaft weggelassen wird, wird das Feld &quot;Zielgruppe&quot;durch alle Felder mit einem entsprechenden Referenz-Identitätsdeskriptor abgeleitet (siehe unten). |


#### Referenz-Identitätsdeskriptor

Referenz-Identitätsdeskriptoren stellen einen Referenzkontext zu einem Schema-Feld bereit, sodass es mit dem primären Identitätsfeld eines Ziel-Schemas verknüpft werden kann. Felder müssen bereits mit einem Identitätsdeskriptor beschriftet sein, bevor ein Referenzdeskriptor darauf angewendet werden kann.

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
| `xdm:sourceSchema` | Der `$id` URI des Schemas, in dem der Deskriptor definiert wird. |
| `xdm:sourceVersion` | Die Hauptversion des Quell-Schemas. |
| `xdm:sourceProperty` | Pfad zum Feld im Quellfeld, in dem der Deskriptor definiert wird. Sollte mit einem &quot;/&quot;beginnen und nicht mit einem enden. Schließen Sie nicht &quot;Eigenschaften&quot;in den Pfad ein (z. B. &quot;/personalEmail/address&quot;anstelle von &quot;/properties/personalEmail/properties/address&quot;). |
| `xdm:identityNamespace` | Der Identitäts-Namensraum-Code für die source-Eigenschaft. |