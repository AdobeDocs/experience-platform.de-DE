---
title: Callback-Endpunkt
description: Erfahren Sie, wie Sie Aufrufe an den /callbacks-Endpunkt in der Reactor-API durchführen.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 10%

---

# Callback-Endpunkt

Ein Rückruf ist eine Nachricht, die die Reactor-API an eine bestimmte URL sendet (normalerweise eine URL, die von Ihrem Unternehmen gehostet wird).

Rückrufe sollen zusammen mit [Prüfereignissen](./audit-events.md) verwendet werden, um Aktivitäten in der Reactor-API zu verfolgen. Jedes Mal, wenn ein Prüfereignis eines bestimmten Typs generiert wird, kann ein Rückruf eine passende Nachricht an die angegebene URL senden.

Der Dienst hinter der im Rückruf angegebenen URL muss mit dem HTTP-Status-Code 200 (OK) oder 201 (Erstellt) antworten. Wenn der Dienst mit keinem dieser Status-Codes antwortet, wird der Nachrichtenversand in den folgenden Intervallen wiederholt:

* 1 Minute
* 5 Minuten
* 30 Minuten
* 1 Stunde
* 12 Stunden
* 1 Tag
* 3 Tage

>[!NOTE]
>
>Wiederholungsintervalle sind relativ zum vorherigen Intervall. Wenn beispielsweise der Neuversuch mit einer Minute fehlschlägt, wird der nächste Versuch für fünf Minuten nach dem fehlgeschlagenen einmaligen Versuch (sechs Minuten nach der Erstellung der Nachricht) geplant.

Wenn alle Versandversuche nicht erfolgreich sind, wird die Nachricht verworfen.

Ein Rückruf gehört genau zu einer [Eigenschaft](./properties.md). Eine Eigenschaft kann viele Rückrufe aufweisen.

## Erste Schritte

Der in diesem Handbuch verwendete Endpunkt ist Teil der [Reactor-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml). Bevor Sie fortfahren, lesen Sie zunächst das [Erste-Schritte-Handbuch](../getting-started.md) , um wichtige Informationen zur Authentifizierung bei der API zu erhalten.

## Auflisten von Callbacks {#list}

Sie können alle Rückrufe unter einer Eigenschaft auflisten, indem Sie eine GET-Anfrage ausführen.

**API-Format**

```http
GET  /properties/{PROPERTY_ID}/callbacks
```

| Parameter | Beschreibung |
| --- | --- |
| `{PROPERTY_ID}` | Die `id` der Eigenschaft, deren Rückrufe Sie auflisten möchten. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Mithilfe von Abfrageparametern können aufgelistete Rückrufe anhand der folgenden Attribute gefiltert werden:<ul><li>`created_at`</li><li>`updated_at`</li></ul>Weitere Informationen finden Sie im Handbuch zu [Filterantworten](../guides/filtering.md) .

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR66a3356c73fc4aabb67ee22caae53d70/callbacks \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von Rückrufen für die angegebene Eigenschaft zurück.

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

## Rückruf nachschlagen {#lookup}

Sie können einen Rückruf nachschlagen, indem Sie dessen Kennung im Pfad einer GET-Anfrage angeben.

**API-Format**

```http
GET /callbacks/{CALLBACK_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `CALLBACK_ID` | Die `id` des Rückrufs, den Sie nachschlagen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/callbacks/CBeef389cee8d84e69acef8665e4dcbef6 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details des Rückrufs zurück.

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

## Callback erstellen {#create}

Sie können einen neuen Rückruf erstellen, indem Sie eine POST-Anfrage stellen.

**API-Format**

```http
POST /properties/{PROPERTY_ID}/callbacks
```

| Parameter | Beschreibung |
| --- | --- |
| `PROPERTY_ID` | Die `id` der [Eigenschaft](./properties.md), unter der Sie den Rückruf definieren. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PR5e22de986a7c4070965e7546b2bb108d/callbacks \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
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
| `url` | Das URL-Ziel für die Rückruffunktion. Die URL muss die HTTPS-Protokollerweiterung verwenden. |
| `subscriptions` | Ein Array von Zeichenfolgen, das die Prüfereignistypen angibt, die den Rückruf Trigger. Eine Liste der möglichen Ereignistypen finden Sie im [Endpunktleitfaden zu Prüfereignissen](./audit-events.md) . |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt die Details des neu erstellten Rückrufs zurück.

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

## Callback aktualisieren

Sie können einen Rückruf aktualisieren, indem Sie dessen ID in den Pfad einer PUT-Anfrage einschließen.

**API-Format**

```http
PUT /callbacks/{CALLBACK_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `CALLBACK_ID` | Die `id` des Rückrufs, den Sie aktualisieren möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Die folgende Anfrage aktualisiert das `subscriptions` -Array für einen vorhandenen Rückruf.

```shell
curl -X PUT \
  https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
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
| `attributes` | Ein Objekt, dessen Eigenschaften die Attribute darstellen, die für den Rückruf aktualisiert werden sollen. Jeder Schlüssel stellt das betreffende Callback-Attribut dar, das aktualisiert werden soll, sowie den entsprechenden Wert, auf den es aktualisiert werden soll.<br><br>Die folgenden Attribute können für Rückrufe aktualisiert werden:<ul><li>`subscriptions`</li><li>`url`</li></ul> |
| `id` | Die `id` des Rückrufs, den Sie aktualisieren möchten. Dies sollte mit dem Wert `{CALLBACK_ID}` übereinstimmen, der im Anfragepfad bereitgestellt wird. |
| `type` | Der Typ der zu aktualisierenden Ressource. Für diesen Endpunkt muss der Wert `callbacks` lauten. |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt die Details des aktualisierten Rückrufs zurück.

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

## Callback löschen

Sie können einen Callback löschen, indem Sie dessen ID in den Pfad einer DELETE-Anfrage einschließen.

**API-Format**

```http
DELETE /callbacks/{CALLBACK_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `CALLBACK_ID` | Die `id` des Rückrufs, den Sie löschen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X DELETE \
  https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 204 (Kein Inhalt) ohne Antworttext zurück und zeigt an, dass der Rückruf gelöscht wurde.
