---
title: Unified Tags Endpoint
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-APIs Tag-Kategorien und Tags erstellen, aktualisieren, verwalten und löschen.
role: Developer
source-git-commit: ede314d0cbe50514090915fccf7ef3c2a5254b7a
workflow-type: tm+mt
source-wordcount: '1860'
ht-degree: 4%

---


# Unified-Tags-Endpunkt

>[!IMPORTANT]
>
>Die Endpunkt-URL für diesen Satz von Endpunkten lautet `https://experience.adobe.io`.

Tags sind eine Funktion, mit der Sie Metadaten-Taxonomien verwalten können, um Geschäftsobjekte zu klassifizieren und so die Erkennung und Kategorisierung zu erleichtern. Anschließend können Sie diese Tags in weiteren Gruppen organisieren, indem Sie sie zu Tag-Kategorien hinzufügen.

Dieses Handbuch enthält Informationen zum besseren Verständnis von Tags und Tag-Kategorien sowie Beispiel-API-Aufrufe für die Durchführung grundlegender Aktionen mithilfe der API.

## Erste Schritte

Die in diesem Handbuch verwendeten Endpunkte sind Teil der Adobe Experience Platform-APIs. Bevor Sie fortfahren, lesen Sie bitte die [Erste Schritte](./getting-started.md) für wichtige Informationen, die Sie benötigen, um die API erfolgreich aufrufen zu können, einschließlich erforderlicher Kopfzeilen und Informationen zum Lesen von Beispiel-API-Aufrufen

### Glossar

Im folgenden Glossar wird der Unterschied zwischen einem **Tag** und **Tag-Kategorie**.

- **Tag**: Mit einem -Tag können Sie die Metadaten-Taxonomie für Geschäftsobjekte verwalten, sodass Sie diese Objekte klassifizieren können, um eine einfachere Erkennung und Kategorisierung zu ermöglichen.
   - **Nicht kategorisiertes Tag**: Ein nicht kategorisiertes Tag ist ein Tag, das nicht zu einer Tag-Kategorie gehört. Standardmäßig werden erstellte Tags nicht kategorisiert.
- **Tag-Kategorie**: Mit einer Tag-Kategorie können Sie Ihre Tags in aussagekräftige Sets gruppieren, sodass Sie mehr Kontext für den Zweck des Tags bereitstellen können.

## Abrufen einer Liste von Tag-Kategorien {#get-tag-categories}

Sie können eine Liste von Tag-Kategorien abrufen, die zu Ihrem Unternehmen gehören, indem Sie eine GET-Anfrage an die `/tagCategory` -Endpunkt.

**API-Format**

```http
GET /tagCategory
GET /tagCategory?{QUERY_PARAMETERS}
```

Die folgenden optionalen Abfrageparameter können beim Abrufen von Tag-Kategorien verwendet werden.

| Abfrageparameter | Beschreibung | Beispiel |
| --------------- | ----------- | ------- |
| `start` | Der Ort, an dem die Liste der Ergebnisse beginnt. Sie können dies verwenden, um den Startindex für die Paginierung der Ergebnisse anzugeben. | `start=a` |
| `limit` | Die maximale Anzahl von Tag-Kategorien, die pro Seite abgerufen werden sollen. | `limit=20` |
| `property` | Das Attribut, nach dem Sie beim Abrufen von Tag-Kategorien filtern möchten. Zu den unterstützten Werten gehören: &lt;ul><li>`name`: Der Name der Tag-Kategorie.</li></ul> | `property=name==category` |
| `sortBy` | Die Reihenfolge, in der die Tag-Kategorien sortiert werden. Zu den unterstützten Werten gehören `name`, `createdAt`, und `modifiedAt`. | `sortBy=name` |
| `sortOrder` | Die Richtung, nach der die Tag-Kategorien sortiert werden. Zu den unterstützten Werten gehören `asc` und `desc`. | `sortOrder=asc` |

**Anfrage**

++ + Eine Beispielanfrage zum Auflisten aller Tag-Kategorien in Ihrer Organisation

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tagCategory
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit einer Liste aller Tag-Kategorien für Ihr Unternehmen zurück.

+++ Eine Beispielantwort mit einer Liste aller Tag-Kategorien in Ihrer Organisation.

```json
{
    "_page": {
        "count": 1,
        "limit": 10,
        "property": []
    },
    "tags": [
        {
            "id": "e2b7c656-067b-4413-a366-adde0401df50",
            "name": "Test Category",
            "description": "A sample description for the test tag category.",
            "org": "{ORG_ID}",
            "createdBy": "{USER_ID}",
            "createdAt": "1661752268000",
            "modifiedBy": "{USER_ID}",
            "modifiedAt": "1661752268000",
            "tagCount": 0
        }
    ]
}
```

+++

## Neue Tag-Kategorie erstellen {#create-tag-category}

>[!IMPORTANT]
>
>Nur der Systemadministrator und der Produkt-Administrator können diesen API-Aufruf verwenden.

Sie können eine neue Tag-Kategorie erstellen, indem Sie eine POST-Anfrage an die `/tagCategory` -Endpunkt.

**API-Format**

```http
POST /tagCategory
```

**Anfrage**

++ + Eine Beispielanfrage zum Erstellen einer neuen Tag-Kategorie.

```shell
curl -X POST https://experience.adobe.io/unifiedtags/tagCategory
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '{
    "name": "Sample Test Category",
    "description": "Sample test category"
 }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `name` | Der Name der Tag-Kategorie, die Sie erstellen möchten. |
| `description` | Eine Beschreibung der Tag-Kategorie, die Sie erstellen möchten. |

+++

**Antwort**

Eine Beispielantwort gibt den HTTP-Status 200 mit Details zur neu erstellten Tag-Kategorie zurück.

++ + Eine Beispielantwort mit Details zur neu erstellten Tag-Kategorie.

```json
{
    "id": "e2b7c656-067b-4413-a366-adde0401df50",
    "name": "Sample Test Category",
    "description": "Sample test category",
    "org": "{ORG_ID}",
    "createdBy": "{USER_ID}",
    "createdAt": "1661752268000",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "1661752268000",
    "tagCount": 0
}
```

+++

## Bestimmte Tag-Kategorie abrufen {#get-tag-category}

Sie können eine bestimmte Tag-Kategorie abrufen, die zu Ihrem Unternehmen gehört, indem Sie eine GET-Anfrage an die `/tagCategory` -Endpunkt und die ID der Tag-Kategorie angeben.

**API-Format**

```http
GET /tagCategory/{TAG_CATEGORY_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{TAG_CATEGORY_ID}` | Die ID der Tag-Kategorie, die Sie abrufen. |

**Anfrage**

++ + Eine Beispielanfrage zum Abrufen einer bestimmten Tag-Kategorie

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tagCategory/e2b7c656-067b-4413-a366-adde0401df50 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zur angegebenen Tag-Kategorie zurück.

++ + Eine Beispielantwort mit Details zur angegebenen Tag-Kategorie.

```json
{
    "id": "e2b7c656-067b-4413-a366-adde0401df50",
    "name": "Test Category",
    "description": "A sample description for the test tag category.",
    "org": "{ORG_ID}",
    "createdBy": "{USER_ID}",
    "createdAt": "1661752268000",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "1661752268000",
    "tagCount": 0
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `id` | Die ID der angeforderten Tag-Kategorie. |
| `name` | Der Name der angeforderten Tag-Kategorie. |
| `description` | Die Beschreibung der angeforderten Tag-Kategorie. |
| `createdBy` | Die ID des Benutzers, der die Tag-Kategorie erstellt hat. |
| `createdAt` | Der Zeitstempel, mit dem die Tag-Kategorie erstellt wurde. |
| `modifiedBy` | Die ID des Benutzers, der die Tag-Kategorie zuletzt aktualisiert hat. |
| `modifiedAt` | Der Zeitstempel der letzten Aktualisierung der Tag-Kategorie. |
| `tagCount` | Die Anzahl der Tags, die zur Tag-Kategorie gehören. |

+++

## Aktualisieren einer bestimmten Tag-Kategorie {#update-tag-category}

>[!IMPORTANT]
>
>Nur der Systemadministrator und der Produkt-Administrator können diesen API-Aufruf verwenden.

Sie können Details einer bestimmten Tag-Kategorie, die zu Ihrem Unternehmen gehört, aktualisieren, indem Sie eine PATCH-Anfrage an die `/tagCategory` -Endpunkt und die ID der Tag-Kategorie angeben.

**API-Format**

```http
PATCH /tagCategory/{TAG_CATEGORY_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{TAG_CATEGORY_ID}` | Die ID der Tag-Kategorie, die Sie abrufen. |

**Anfrage**

++ + Eine Beispielanfrage zum Aktualisieren einer bestimmten Tag-Kategorie

```shell
curl -X PATCH https://experience.adobe.io/unifiedtags/tagCategory/e2b7c656-067b-4413-a366-adde0401df50 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '[{
    "op": "replace",
    "path": "description",
    "value": "Updated sample description",
    "from": "Sample description"
 }]'
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `op` | Der abgeschlossene Vorgang. Um eine bestimmte Tag-Kategorie zu aktualisieren, setzen Sie diesen Wert auf `replace`. |
| `path` | Der Pfad des zu aktualisierenden Felds. Zu den unterstützten Werten gehören `name` und `description`. |
| `value` | Der aktualisierte Wert des Felds, das Sie aktualisieren möchten. |
| `from` | Der ursprüngliche Wert des Felds, das Sie aktualisieren möchten. |

+++

**Antwort**

Eine erfolgreiche Antwort HTTP-Status 200 mit Informationen zu Ihrer neu aktualisierten Tag-Kategorie.

+++ Eine Beispielantwort mit Details zu Ihrer neu aktualisierten Tag-Kategorie.

```json
{
    "id": "e2b7c656-067b-4413-a366-adde0401df50",
    "name": "Test Category",
    "description": "Updated sample description",
    "org": "{ORG_ID}",
    "createdBy": "{USER_ID}",
    "createdAt": "1661752268000",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "1661752268000",
    "tagCount": 0
}
```

+++

## Löschen einer bestimmten Tag-Kategorie {#delete-tag-category}

>[!IMPORTANT]
>
>Nur der Systemadministrator und der Produkt-Administrator können diesen API-Aufruf verwenden.

Sie können eine bestimmte Tag-Kategorie, die zu Ihrem Unternehmen gehört, löschen, indem Sie eine DELETE-Anfrage an die `/tagCategory` -Endpunkt und die ID der Tag-Kategorie angeben.

**API-Format**

```http
DELETE /tagCategory/{TAG_CATEGORY_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{TAG_CATEGORY_ID}` | Die ID der Tag-Kategorie, die Sie abrufen. |

**Anfrage**

++ + Eine Beispielanfrage zum Löschen einer bestimmten Tag-Kategorie

```shell
curl -X DELETE https://experience.adobe.io/unifiedtags/tagCategory/e2b7c656-067b-4413-a366-adde0401df50 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 zusammen mit einer leeren Antwort zurück.

## Liste von Tags abrufen {#get-tags}

Sie können eine Liste von Tags abrufen, die zu Ihrem Unternehmen gehören, indem Sie eine GET-Anfrage an die `/tags` -Endpunkt und die ID der Tag-Kategorie.

**API-Format**

```http
GET /tags
GET /tags?{QUERY_PARAMETERS}
```

Beim Abrufen von Tags können die folgenden optionalen Abfrageparameter verwendet werden.

| Abfrageparameter | Beschreibung | Beispiel |
| --------------- | ----------- | ------- |
| `start` | Der Ort, an dem die Liste der Ergebnisse beginnt. Sie können dies verwenden, um den Startindex für die Paginierung der Ergebnisse anzugeben. | `start=a` |
| `limit` | Die maximale Anzahl von Tags, die pro Seite abgerufen werden sollen. | `limit=20` |
| `property` | Das Attribut, nach dem Sie beim Abrufen von Tags filtern möchten. Zu den unterstützten Werten gehören:<ul><li>`name`: Der Name des Tags.</li><li>`archived`: Gibt an, ob die Tags archiviert oder nicht archiviert werden. Sie können diesen Wert auf Folgendes festlegen: `true` oder `false`.</li><li>`tagCategoryId`: Die ID der Tag-Kategorie, zu der das Tag gehört.</li></ul> | <ul><li>`property=name==TestTag`</li><li>`property=archived==false`</li><li>`property=tagCategoryId==e2b7c656-067b-4413-a366-adde0401df50`</li> |
| `sortBy` | Die Reihenfolge, in der die Tags sortiert werden. Zu den unterstützten Werten gehören `name`, `createdAt`, und `modifiedAt`. | `sortBy=name` |
| `sortOrder` | Die Richtung, nach der die Tag-Kategorien sortiert werden. Zu den unterstützten Werten gehören `asc` und `desc`. | `sortOrder=asc` |


**Anfrage**

++ + Eine Beispielanfrage zum Abrufen aller Tags, die zu einer bestimmten Tag-Kategorie gehören

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tags?property=tagCategoryId=e2b7c656-067b-4413-a366-adde0401df50
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zu den Tags zurück, die zu dieser Tag-Kategorie gehören.

+++ Eine Beispielantwort mit Details zu den angeforderten Tags.

```json
{
    "_page": {
        "count": 166,
        "limit": 10,
        "next": "eyJjb21wb3NpdGVUb2tlbiI6IntcInRva2VuXCI6XCIrUklEOn52a0owQUp3WDRrVko1d0FBQUFBQUFBPT0jUlQ6MiNUUkM6MjAjUlREOnVDTmQyWlAvWjV6TGdvUGVGR1JHQk1KNVExVmR6Mnc9I0lTVjoyI0lFTzo2NTU2NyNRQ0Y6OCNGUEM6QWdFQ0J3TG1BQ1NmQnNBQ0JBb0FBQVFBQ0FBQUNJQVlnQWVBRElBTmdBWEFFTUJCUUVBQUFBQkFRQkdBSElBR2dBQ0FENEFId0FKUkRFQUNBZ2dBUUJnQUVBQUlIb0FaZ0FDQUJNQUFRVUFBUUFCQVFScUFBc0FTQUFBRUxvQU9nQWFBQmNBQVlBQUFHSUlCUUFDQU1vQUlnQWlBQk1DQUFRQUFnZ0FnQUM2QURZQTNnQWlBR1lBQWdCZUFBY0FCZ0JlQUM4QURBQUlBQWdBQVFBQ0FBRUZBQVFFQUFBRWdBQ0FBSjRCR2dBeUFCSUFPZ0F5QU13QVNRQ0FBQUVBdGdCRUFBR0FkZ0FuQUFDZ0NBQUFBQ0lCQUFDSkFnQUJBRUFDQUg0QUhnQWFBQllBVUFFQUNCQUFFQUFRQUF4QUFzUnJBQUlFQUFBYkxoQklIQVBBQUhnUUVBTEVxQUE4RkNBQVFtcUVBd0FBTWd3Y09BSFdIa1FBZ0JGT0FTNEN4QVE0QVwiLFwicmFuZ2VcIjp7XCJtaW5cIjpcIlwiLFwibWF4XCI6XCJGRlwifX0iLCJvcmRlckJ5SXRlbXMiOlt7Iml0ZW0iOjE2OTQ0ODg2MDMwMDB9XSwicmlkIjoidmtKMEFKd1g0a1hHV2dFQUFBQUFBQT09IiwiaW5jbHVzaXZlIjp0cnVlfQ==",
        "property": [
            "tagCategoryId=e2b7c656-067b-4413-a366-adde0401df50"
        ]
    },
    "tags": [
        {
            "archived": false,
            "createdAt": 1705624523000,
            "createdBy": "{USER_ID}",
            "id": "8af14b1e-f267-44ad-b94c-9ac70274e3d5",
            "modifiedAt": 1705624523000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705624481530",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705624523000,
            "createdBy": "{USER_ID}",
            "id": "8b907a2c-0f15-4d2c-9672-bf545d5e47ab",
            "modifiedAt": 1705624523000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705624489131",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705624523000,
            "createdBy": "{USER_ID}",
            "id": "e30bd956-afad-40a1-8f4a-7e4428855856",
            "modifiedAt": 1705624523000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705624494191",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705451722000,
            "createdBy": "{USER_ID}",
            "id": "3bf6a6ba-0b11-4d83-8f35-db6e5b9652d8",
            "modifiedAt": 1705451722000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705451701640",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705422929000,
            "createdBy": "{USER_ID}",
            "id": "0910dfc8-7924-473d-afc6-1aa68337b3b6",
            "modifiedAt": 1705422929000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705422890399",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705394126000,
            "createdBy": "{USER_ID}",
            "id": "b426085e-580b-4147-9921-8ba77ffa77a9",
            "modifiedAt": 1705394126000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705394104556",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": true,
            "createdAt": 1705392795000,
            "createdBy": "{USER_ID}",
            "id": "92961035-e72b-45a0-9625-781380017585",
            "modifiedAt": 1705392832000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705392794917",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1705335274000,
            "createdBy": "{USER_ID}",
            "id": "436ce801-ef87-45fd-b34a-9ce938a447e1",
            "modifiedAt": 1705335274000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1705335252944",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1694776514000,
            "createdBy": "{USER_ID}",
            "id": "1e6e9836-5e18-4340-a959-3206c9bc3a94",
            "modifiedAt": 1694776514000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1694776510734",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        },
        {
            "archived": false,
            "createdAt": 1694488609000,
            "createdBy": "{USER_ID}",
            "id": "b8400673-2f90-48e9-b73b-cdfbba5ab361",
            "modifiedAt": 1694488609000,
            "modifiedBy": "{USER_ID}",
            "name": "xql-test-1694488608301",
            "org": "{ORG_ID}",
            "tagCategoryId": "e2b7c656-067b-4413-a366-adde0401df50",
            "tagCategoryName": "Test Category"
        }
    ]
}
```

+++

## Neues Tag erstellen {#create-tag}

>[!IMPORTANT]
>
>Nur der Systemadministrator und der Produkt-Administrator können diesen API-Aufruf verwenden, um ein neues Tag in einer bestimmten Tag-Kategorie zu erstellen.
>
>Wenn Sie ein nicht kategorisiertes Tag erstellen, tun Sie dies **not** benötigen Administratorberechtigungen.

Sie können ein neues Tag erstellen, indem Sie eine POST-Anfrage an die `/tags` -Endpunkt.

**API-Format**

```http
POST /tags
```

**Anfrage**

++ + Eine Beispielanfrage zum Erstellen eines neuen Tags.

```shell
curl -X POST https://experience.adobe.io/unifiedtags/tags
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '{
    "name": "sampleTag"
 }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `name` | **Erforderlich**. Der Name des Tags, das Sie erstellen möchten. |
| `tagCategoryId` | *Optional*. Die ID der Tag-Kategorie, zu der das Tag gehören soll. Wenn kein Wert angegeben wird, wird das Tag als Teil der Kategorie Nicht kategorisiert erstellt. |

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 201 mit Details zu Ihrem neu erstellten Tag zurück.

++ + Eine Beispielantwort mit Details zum neu erstellten Tag.

```json
{
    "name": "sampleTag",
    "id": "2bd5ddd9-7284-4767-81d9-c75b122f2a6a",
    "org": "{ORG_ID}",
    "createdAt": "1661753717000",
    "createdBy": "{USER_ID}",
    "modifiedAt": "1661753717000",
    "modifiedBy": "{USER_ID}",
    "tagCategoryId": "Uncategorized-{ORG_ID}",
    "tagCategoryName": "Uncategorized",
    "archived": false
}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `name` | Der Name des neu erstellten Tags. |
| `id` | Die ID des neu erstellten Tags. |
| `org` | Die ID der Organisation, zu der das Tag gehört. |
| `createdAt` | Der Zeitstempel der Erstellung des Tags. |
| `createdBy` | Die ID des Benutzers, der das Tag erstellt hat. |
| `modifiedAt` | Der Zeitstempel der letzten Aktualisierung des Tags. |
| `modifiedBy` | Die ID des Benutzers, der das Tag zuletzt aktualisiert hat. |
| `tagCategoryId` | Die ID der Tag-Kategorie, zu der das Tag gehört. |
| `tagCategoryName` | Der Name der Tag-Kategorie, zu der das Tag gehört. |

+++

## Abrufen eines bestimmten Tags {#get-tag}

Sie können ein bestimmtes Tag abrufen, das zu Ihrem Unternehmen gehört, indem Sie eine GET-Anfrage an die `/tags` -Endpunkt und geben Sie die ID des Tags an, das Sie abrufen möchten.

**API-Format**

```http
GET /tags/{TAG_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{TAG_ID}` | Die ID des Tags, das Sie abrufen. |

**Anfrage**

++ + Eine Beispielanfrage zum Abrufen eines bestimmten Tags

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tags/2bd5ddd9-7284-4767-81d9-c75b122f2a6a \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zum angegebenen Tag zurück.

++ + Eine Beispielantwort mit Details zum angegebenen Tag.

```json
{
    "name": "sampleTag",
    "id": "2bd5ddd9-7284-4767-81d9-c75b122f2a6a",
    "org": "{ORG_ID}",
    "createdAt": "1661753717000",
    "createdBy": "{USER_ID}",
    "modifiedAt": "1661753717000",
    "modifiedBy": "{USER_ID}",
    "tagCategoryId": "Test Category-{ORG_ID}",
    "tagCategoryName": "Test Category",
    "archived": false
}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `name` | Der Name des abgerufenen Tags. |
| `id` | Die ID des abgerufenen Tags. |
| `org` | Die ID der Organisation, zu der das Tag gehört. |
| `createdAt` | Der Zeitstempel der Erstellung des Tags. |
| `createdBy` | Die ID des Benutzers, der das Tag erstellt hat. |
| `modifiedAt` | Der Zeitstempel der letzten Aktualisierung des Tags. |
| `modifiedBy` | Die ID des Benutzers, der das Tag zuletzt aktualisiert hat. |
| `tagCategoryId` | Die ID der Tag-Kategorie, zu der das Tag gehört. |
| `tagCategoryName` | Der Name der Tag-Kategorie, zu der das Tag gehört. |
| `archived` | Der Archivierungsstatus des Tags. Wenn auf `true`bedeutet dies, dass das Tag archiviert wird. |

+++

## Tags überprüfen {#validate-tags}

Sie können überprüfen, ob Tags vorhanden sind, indem Sie eine POST-Anfrage an die `/tags/validate` -Endpunkt.

**API-Format**

```http
POST /tags/validate
```

**Anfrage**

++ + Eine Beispielanfrage zum Validieren der bereitgestellten Tag-IDs.

```shell
curl -X POST https://experience.adobe.io/unifiedtags/tags/validate
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '{
    "ids": [
        "2bd5ddd9-7284-4767-81d9-c75b122f2a6a","d113f40c-0097-4626-8d5f-6d5017694453", "invalid-tag"
    ],
    "entity": "{API_KEY}"
 }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `ids` | Ein Array, das eine Liste von Tag-IDs enthält, die Sie überprüfen möchten. |
| `entity` | Die Entität, die die Validierung anfordert. Sie können die `{API_KEY}` -Wert für diesen Parameter. |

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Informationen dazu zurück, welche Tags gültig und ungültig sind.

++ + Eine Beispielantwort, die anzeigt, welche Tags gültig und ungültig sind.

```json
{
    "invalidTags": [
        {
            "id": "invalid-tag"
        }
    ],
    "validTags": [
        {
            "id": "d113f40c-0097-4626-8d5f-6d5017694453"
        },
        {
            "id": "2bd5ddd9-7284-4767-81d9-c75b122f2a6a"
        }
    ]
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `invalidTags` | Ein Array, das eine Liste der ungültigen Tag-IDs enthält. |
| `validTags` | Ein Array, das eine Liste der gültigen Tag-IDs enthält. |

+++

## Aktualisieren eines bestimmten Tags {#update-tag}

Sie können ein bestimmtes Tag aktualisieren, indem Sie eine PATCH-Anfrage an die `/tags` -Endpunkt und geben die ID des Tags an, das Sie aktualisieren möchten.

**API-Format**

```http
PATCH /tags/{TAG_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{TAG_ID}` | Die ID des Tags, das Sie aktualisieren. |

**Anfrage**

++ + Eine Beispielanfrage zum Aktualisieren eines bestimmten Tags

```shell
curl -X GET https://experience.adobe.io/unifiedtags/tags/2bd5ddd9-7284-4767-81d9-c75b122f2a6a \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -d '[{
    "op": "replace",
    "path": "name",
    "value": "newSampleTag",
    "from": "sampleTag"
 }]'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `op` | Der Vorgang, der durchgeführt werden muss. In diesem Anwendungsfall wird er immer auf `replace`. |
| `path` | Der Pfad des zu aktualisierenden Felds. Zu den unterstützten Werten gehören `name`, `archived`, und `tagCategoryId`. |
| `value` | Der aktualisierte Wert des Felds, das Sie aktualisieren möchten. |
| `from` | Der ursprüngliche Wert des Felds, das Sie aktualisieren möchten. |

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zum neu aktualisierten Tag zurück.

++ + Eine Beispielantwort mit Details zum aktualisierten Tag.

```json
{
    "name": "newSampleTag",
    "id": "2bd5ddd9-7284-4767-81d9-c75b122f2a6a",
    "org": "{ORG_ID}",
    "createdAt": "1661753717000",
    "createdBy": "{USER_ID}",
    "modifiedAt": "1661753717000",
    "modifiedBy": "{USER_ID}",
    "tagCategoryId": "Test Category-{ORG_ID}",
    "tagCategoryName": "Test Category",
    "archived": false
}
```

+++

## Löschen eines bestimmten Tags {#delete-tag}

>[!IMPORTANT]
>
>Nur der Systemadministrator und der Produkt-Administrator können diesen API-Aufruf verwenden.
>
>Zusätzlich wird das Tag **cannot** mit allen Geschäftsobjekten verknüpft werden und **must** vor dem Löschen des Tags archiviert werden. Sie können das Tag mit dem [Tag-Endpunkt aktualisieren](#update-tag).

Sie können ein bestimmtes Tag löschen, indem Sie ein DELETE-Tag in die `/tags` -Endpunkt und geben Sie die ID des Tags an, das Sie löschen möchten.

**API-Format**

```http
DELETE /tags/{TAG_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{TAG_ID}` | Die ID des Tags, das Sie löschen. |

**Anfrage**

++ + Eine Beispielanfrage zum Löschen eines bestimmten Tags

```shell
curl -X DELETE https://experience.adobe.io/unifiedtags/tags/2bd5ddd9-7284-4767-81d9-c75b122f2a6a \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 zusammen mit einer leeren Antwort zurück.

## Nächste Schritte

Nach dem Lesen dieses Handbuchs erfahren Sie mehr darüber, wie Sie mithilfe der Adobe Experience Platform-APIs Tags und Tag-Kategorien erstellen, verwalten und löschen. Weitere Informationen zum Verwalten von Tags über die Benutzeroberfläche finden Sie im Abschnitt [Verwalten von Tags-Handbuch](../ui/managing-tags.md). Weitere Informationen zum Verwalten von Tag-Kategorien mithilfe der Benutzeroberfläche finden Sie im Abschnitt [Tag-Kategorien-Handbuch](../ui/tags-categories.md).
