---
title: Callback-Endpunkt
description: Erfahren Sie, wie Sie den /callback-Endpunkt in der Reactor-API aufrufen.
exl-id: dd980f91-89e3-4ba0-a6fc-64d66b288a22
source-git-commit: 7f3b9ef9270b7748bc3366c8c39f503e1aee2100
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 97%

---

# Callback-Endpunkt

Ein Callback ist eine Nachricht, die die Reactor-API an eine bestimmte URL sendet (normalerweise eine, die von Ihrer Organisation gehostet wird).

Callbacks sind dazu gedacht, in Verbindung mit [Audit-Ereignissen](./audit-events.md) verwendet zu werden, um Aktivitäten in der Reactor-API zu verfolgen. Jedes Mal, wenn ein Audit-Ereignis eines bestimmten Typs erzeugt wird, kann ein Callback eine passende Nachricht an die angegebene URL senden.

Der Service hinter der im Callback angegebenen URL muss mit dem HTTP-Status-Code 200 (OK) oder 201 (Erstellt) antworten. Wenn der Service nicht mit einem dieser Status-Codes antwortet, wird die Nachrichtenzustellung in den folgenden Abständen erneut versucht:

* 1 Minute
* 5 Minuten
* 30 Minuten
* 1 Stunde
* 12 Stunden
* 1 Tag
* 3 Tage

>[!NOTE]
>
>Wiederholungsintervalle sind relativ zum vorherigen Intervall. Wenn z. B. der Wiederholungsversuch nach einer Minute fehlschlägt, wird der nächste Versuch für fünf Minuten nach dem fehlgeschlagenen einminütigen Versuch geplant (sechs Minuten, nachdem die Nachricht generiert wurde).

Wenn alle Zustellversuche erfolglos sind, wird die Nachricht verworfen.

Ein Callback gehört zu genau einer [Eigenschaft](./properties.md). Eine Eigenschaft kann viele Callbacks haben.

## Erste Schritte

Der in diesem Handbuch verwendete Endpunkt ist Teil der [Reactor-API](https://www.adobe.io/experience-platform-apis/references/reactor/). Bevor Sie fortfahren, lesen Sie zunächst das [Erste-Schritte-Handbuch](../getting-started.md), um wichtige Informationen zur Authentifizierung bei der API zu erhalten.

## Auflisten von Callbacks {#list}

Sie können alle Callbacks unter einer Eigenschaft auflisten, indem Sie eine GET-Anfrage stellen.

**API-Format**

```http
GET  /properties/{PROPERTY_ID}/callbacks
```

| Parameter | Beschreibung |
| --- | --- |
| `{PROPERTY_ID}` | Die `id` der Eigenschaft, deren Callbacks Sie auflisten möchten. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Mithilfe von Abfrageparametern können die aufgelisteten Callbacks anhand der folgenden Attribute gefiltert werden:<ul><li>`created_at`</li><li>`updated_at`</li></ul>Weiterführende Informationen finden Sie im Handbuch zum [Filtern von Antworten](../guides/filtering.md).

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR66a3356c73fc4aabb67ee22caae53d70/callbacks \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von Callbacks für die angegebene Eigenschaft zurück.

```json
{
  "data": [
    {
      "id": "CB26edef8d709243579589107bcda034da",
      "type": "callbacks",
      "attributes": {
        "created_at": "2020-12-14T17:34:47.082Z",
        "subscriptions": [
          "rule.created"
        ],
        "updated_at": "2020-12-14T17:34:47.082Z",
        "url": "https://www.example.com"
      },
      "relationships": {
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/callbacks/CB26edef8d709243579589107bcda034da/property"
          },
          "data": {
            "id": "PR66a3356c73fc4aabb67ee22caae53d70",
            "type": "properties"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR66a3356c73fc4aabb67ee22caae53d70",
        "self": "https://reactor.adobe.io/callbacks/CB26edef8d709243579589107bcda034da"
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

## Suchen eines Callbacks {#lookup}

Sie können einen Callback suchen, indem Sie seine ID im Pfad einer GET-Anfrage angeben.

**API-Format**

```http
GET /callbacks/{CALLBACK_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `CALLBACK_ID` | Die `id` des Callbacks, den Sie suchen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/callbacks/CBeef389cee8d84e69acef8665e4dcbef6 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details des Callbacks zurück.

```json
{
  "data": {
    "id": "CBeef389cee8d84e69acef8665e4dcbef6",
    "type": "callbacks",
    "attributes": {
      "created_at": "2020-12-14T17:34:36.872Z",
      "subscriptions": [
        "rule.created"
      ],
      "updated_at": "2020-12-14T17:34:36.872Z",
      "url": "https://www.example.com"
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/callbacks/CBeef389cee8d84e69acef8665e4dcbef6/property"
        },
        "data": {
          "id": "PRb513bbab52114573ac87f9848eea6ead",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRb513bbab52114573ac87f9848eea6ead",
      "self": "https://reactor.adobe.io/callbacks/CBeef389cee8d84e69acef8665e4dcbef6"
    }
  }
}
```

## Erstellen eines Callbacks {#create}

Sie können einen neuen Callback erstellen, indem Sie eine POST-Anfrage stellen.

**API-Format**

```http
POST /properties/{PROPERTY_ID}/callbacks
```

| Parameter | Beschreibung |
| --- | --- |
| `PROPERTY_ID` | Die `id` der [Eigenschaft](./properties.md), unter der Sie den Callback definieren. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PR5e22de986a7c4070965e7546b2bb108d/callbacks \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "attributes": {
            "url": "https://www.example.com",
            "subscriptions": [
              "rule.created"
            ]
          }
        }
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `url` | Das URL-Ziel für die Callback-Nachricht. Die URL muss die HTTPS-Protokollerweiterung verwenden. |
| `subscriptions` | Ein Array von Strings, das die Audit-Ereignistypen angibt, die den Callback auslösen werden. Eine Liste der möglichen Ereignistypen finden Sie im [Handbuch zum audit events-Endpunkt](./audit-events.md). |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt die Details des neu erstellten Callbacks zurück.

```json
{
  "data": {
    "id": "CB32d8f23d5ee548278d32076af4c442a0",
    "type": "callbacks",
    "attributes": {
      "created_at": "2020-12-14T17:34:27.059Z",
      "subscriptions": [
        "rule.created"
      ],
      "updated_at": "2020-12-14T17:34:27.059Z",
      "url": "https://www.example.com"
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/callbacks/CB32d8f23d5ee548278d32076af4c442a0/property"
        },
        "data": {
          "id": "PR5e22de986a7c4070965e7546b2bb108d",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR5e22de986a7c4070965e7546b2bb108d",
      "self": "https://reactor.adobe.io/callbacks/CB32d8f23d5ee548278d32076af4c442a0"
    }
  }
}
```

## Aktualisieren eines Callbacks

Sie können einen Rückruf aktualisieren, indem Sie dessen ID in den Pfad einer PATCH-Anfrage einschließen.

**API-Format**

```http
PATCH /callbacks/{CALLBACK_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `CALLBACK_ID` | Die `id` des Callbacks, den Sie aktualisieren möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Die folgende Anfrage aktualisiert das `subscriptions`-Array für einen vorhandenen Callback.

```shell
curl -X PATCH \
  https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "attributes": {
            "url": "https://www.example.net",
            "subscriptions": [
              "rule.created",
              "build.created"
            ]
          },
          "type": "callbacks",
          "id": "CB4310904d415549888cc9e31ebe1e1e45"
        }
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `attributes` | Ein Objekt, dessen Eigenschaften die zu aktualisierenden Attribute für den Callback darstellen. Jeder Schlüssel steht für das jeweilige Callback-Attribut, das aktualisiert werden soll, zusammen mit dem entsprechenden Wert, auf den es aktualisiert werden soll.<br><br>Die folgenden Attribute können für Callbacks aktualisiert werden:<ul><li>`subscriptions`</li><li>`url`</li></ul> |
| `id` | Die `id` des Callbacks, den Sie aktualisieren möchten. Diese sollte mit dem `{CALLBACK_ID}`-Wert übereinstimmen, der im Anfragepfad angegeben ist. |
| `type` | Der Typ der zu aktualisierenden Ressource. Für diesen Endpunkt muss der Wert `callbacks` lauten. |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt die Details des aktualisierten Callbacks zurück.

```json
{
  "data": {
    "id": "CB4310904d415549888cc9e31ebe1e1e45",
    "type": "callbacks",
    "attributes": {
      "created_at": "2020-12-14T17:34:56.884Z",
      "subscriptions": [
        "rule.created",
        "build.created"
      ],
      "updated_at": "2020-12-14T17:34:57.614Z",
      "url": "https://www.example.net"
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45/property"
        },
        "data": {
          "id": "PR0a8ef3ca31dc456a8566e9288960bd79",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR0a8ef3ca31dc456a8566e9288960bd79",
      "self": "https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45"
    }
  }
}
```

## Löschen eines Callbacks

Sie können einen Callback löschen, indem Sie seine ID im Pfad einer DELETE-Anfrage angeben.

**API-Format**

```http
DELETE /callbacks/{CALLBACK_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `CALLBACK_ID` | Die `id` des Callbacks, den Sie löschen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X DELETE \
  https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 204 (Kein Inhalt) ohne Antworttext zurück und zeigt damit an, dass der Callback gelöscht wurde.
