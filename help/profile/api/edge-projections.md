---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Entwicklerhandbuch für Customer Profil-API in Echtzeit
topic: guide
translation-type: tm+mt
source-git-commit: bb7aad4de681316cc9f9fd1d9310695bd220adb1
workflow-type: tm+mt
source-wordcount: '1873'
ht-degree: 2%

---


# Edge-Ziele und -Projektionen

Um koordinierte, konsistente und personalisierte Erlebnisse für Ihre Kunden über mehrere Kanal hinweg in Echtzeit zu ermöglichen, müssen die richtigen Daten jederzeit verfügbar sein und im Zuge von Änderungen kontinuierlich aktualisiert werden. Adobe Experience Platform ermöglicht diesen Echtzeitzugriff auf Daten durch die Verwendung von so genannten Kanten. Ein Edge ist ein geografisch platzierter Server, der Daten speichert und für Anwendungen leicht zugänglich macht. Adobe-Anwendungen wie Adobe Zielgruppe und Adobe Campaign verwenden beispielsweise Kanten, um personalisierte Kundenerlebnisse in Echtzeit bereitzustellen. Die Daten werden durch eine Projektion an eine Kante geleitet, wobei ein Projektionsziel die Kante definiert, an die die Daten gesendet werden, und eine Projektionskonfiguration, die die spezifischen Informationen definiert, die an der Kante zur Verfügung gestellt werden. In diesem Handbuch finden Sie detaillierte Anweisungen zur Verwendung der Echtzeit-API für das Profil von Kunden, um mit Edge-Projektionen, einschließlich Zielen und Konfigurationen, zu arbeiten.

## Erste Schritte

Die in diesem Handbuch verwendeten API-Endpunkte sind Teil der Real-time Customer Profil API. Bevor Sie fortfahren, lesen Sie sich bitte das Entwicklerhandbuch für [Echtzeit-Profil durch](getting-started.md). Insbesondere enthält der [Abschnitt](getting-started.md#getting-started) &quot;Erste Schritte&quot;des Profil-Entwicklerhandbuchs Links zu verwandten Themen, eine Anleitung zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtige Informationen zu erforderlichen Kopfzeilen, die für das erfolgreiche Aufrufen von Experience Platform-APIs benötigt werden.

## Projektionsziele

Eine Projektion kann zu einer oder mehreren Kanten geleitet werden, indem die Stellen angegeben werden, an denen Daten gesendet werden sollen. Jedes erstellte Projektionsziel hat eine eindeutige ID, die dann zur Erstellung der Projektionskonfiguration verwendet wird.

### Liste aller Ziele

Sie können die Edge-Ziele, die für Ihr Unternehmen bereits erstellt wurden, durch eine GET-Anforderung an den `/config/destinations` Endpunkt Liste haben.

**API-Format**

```http
GET /config/destinations
```

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/destinations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Die Antwort enthält ein `projectionDestinations` Array mit den Details für jedes Ziel, das als einzelnes Objekt im Array angezeigt wird. Wenn keine Prognosen konfiguriert wurden, gibt das `projectionDestinations` Array leer zurück.

>[!NOTE]
>Diese Antwort wurde für Leerzeichen verkürzt und zeigt nur zwei Ziele an.

```json
{
    "_links": {
        "self": {
            "href": "/data/core/ups/config/destinations",
            "templated": false
        }
    },
    "_embedded": {
        "projectionDestinations": [
            {
                "_links": {
                    "self": {
                        "href": "/data/core/ups/config/destinations/cef0e2ef-5249-4e25-be90-94f5797a2841",
                        "templated": false
                    }
                },
                "id": "cef0e2ef-5249-4e25-be90-94f5797a2841",
                "type": "EDGE",
                "ttl": 3600,
                "dataCenters": [
                    "VA5"
                ],
                "version": 1
            },
            {
                "_links": {
                    "self": {
                        "href": "/data/core/ups/config/destinations/7d26263f-a5df-43ce-b088-7f70e187f549",
                        "templated": false
                    }
                },
                "id": "7d26263f-a5df-43ce-b088-7f70e187f549",
                "type": "EDGE",
                "ttl": 3600,
                "dataCenters": [
                    "OR1"
                ],
                "version": 1
            }
        ]
    }
}
```

| Eigenschaft | Beschreibung |
|---|---|
| `_links.self.href` | Entspricht auf der obersten Ebene dem Pfad, der für die GET-Anforderung verwendet wird. Innerhalb jedes einzelnen Zielobjekts kann dieser Pfad in einer GET-Anforderung verwendet werden, um die Details eines bestimmten Ziels direkt zu suchen. |
| `id` | Innerhalb jedes Zielobjekts `"id"` zeigt die Variable die schreibgeschützte, systemgenerierte eindeutige ID für das Ziel an. Diese ID wird beim Referenzieren eines bestimmten Ziels und beim Erstellen von Projektionskonfigurationen verwendet. |

Weitere Informationen zu den Attributen eines einzelnen Ziels finden Sie im Abschnitt zum [Erstellen eines nachfolgenden Ziels](#create-a-destination) .

### Ziel erstellen {#create-a-destination}

Wenn das gewünschte Ziel noch nicht vorhanden ist, können Sie ein neues Projektionsziel erstellen, indem Sie eine POST-Anforderung an den `/config/destinations` Endpunkt senden.

**API-Format**

```http
POST /config/destinations
```

**Anfrage**

Mit der folgenden Anforderung wird ein neues Edge-Ziel erstellt.

>[!NOTE]
>Die POST-Anfrage zum Erstellen eines Ziels erfordert einen bestimmten `Content-Type` Header, wie unten dargestellt. Die Verwendung eines falschen `Content-Type` Headers führt zu einem HTTP-Status-415-Fehler (nicht unterstützter Medientyp).

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/destinations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/vnd.adobe.platform.projectionDestination+json; version=1' \
  -d '{
        "type": "EDGE",
        "dataCenters": [ 
          "OR1" 
        ],
        "ttl": 3600,
        "replicationPolicy": REACTIVE
      }'
```

| Eigenschaft | Beschreibung |
|---|---|
| `type` **(Erforderlich)** | Der zu erstellende Zieltyp. Der einzige akzeptierte Wert, &quot;EDGE&quot;, erstellt ein Kantenziel. |
| `dataCenters` **(Erforderlich)** | Ein Zeichenfolgen-Array, das die Kanten Liste, in die die Projektionen gedreht werden sollen. Kann einen oder mehrere der folgenden Werte enthalten: &quot;OR1&quot; - Western United States, &quot;VA5&quot; - Eastern United States, &quot;NLD1&quot; - EMEA. |
| `ttl` **(Erforderlich)** | Gibt den Projektionsablauf an. Akzeptierter Wertebereich: 600 bis 604800. Standardwert: 3600. |
| `replicationPolicy` **(Erforderlich)** | Definiert das Verhalten der Datenreplikation vom Hub bis zu den Kanten.  Unterstützte Werte: PROAKTIV, REAKTIV. Standardwert: REAKTIV. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details des neu erstellten Edge-Ziels zurück, einschließlich der schreibgeschützten, systemgenerierten eindeutigen ID (`id`).

```json
{
    "self": {
        "href": "/data/core/ups/config/destinations/cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
        "templated": false
    },
    "id": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
    "type": "EDGE",
    "dataCenters": [
       "OR1"
    ],
    "ttl": 3600,
    "version": 1
}
```

| Eigenschaft | Beschreibung |
|---|---|
| `self.href` | Dieser Pfad wird zum direkten Nachschlagen (GET) des Ziels verwendet und kann auch zum Aktualisieren (PUT) oder Löschen (DELETE) des Ziels verwendet werden. |
| `id` | Die schreibgeschützte, systemgenerierte eindeutige ID für das Ziel. Diese ID dient zum direkten Verweis auf das Ziel und zum Erstellen von Projektionskonfigurationen. |
| `version` | Dieser schreibgeschützte Wert zeigt die aktuelle Version des Ziels. Wenn ein Ziel aktualisiert wird, wird die Versionsnummer automatisch inkrementiert. |

### Ansicht eines Ziels

Wenn Sie die eindeutige ID eines Projektionsziels kennen, können Sie eine Suchanfrage ausführen, um die Details Ansicht. Dies geschieht, indem eine GET-Anforderung an den `/config/destinations` Endpunkt gesendet wird und die ID des Ziels im Anforderungspfad enthalten ist.

**API-Format**

```http
GET /config/destinations/{DESTINATION_ID}
```

| Parameter | Beschreibung |
|---|---|
| `{DESTINATION_ID}` | Die eindeutige ID des Projektionsziels, das Ansicht werden soll. |

**Anfrage**

Die folgende Anforderung führt eine Suche (GET) durch, um das Ziel für die im Anforderungspfad bereitgestellte ID Ansicht.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/destinations/9d66c06e-c745-480c-b64c-1d5234d25f4b \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Das Antwortobjekt zeigt die Details des Projektionsziels an. Das `id` Attribut sollte mit der ID des Projektionsziels übereinstimmen, das in der Anforderung bereitgestellt wurde.

```json
{
    "self": {
        "href": "/data/core/ups/config/destinations/cef0e2ef-5249-4e25-be90-94f5797a2841",
        "templated": false
    },
    "id": "cef0e2ef-5249-4e25-be90-94f5797a2841",
    "type": "EDGE",
    "ttl": 3600,
    "dataCenters": [
        "OR1"
    ],
    "version": 1
}
```

### Ziel aktualisieren

Ein vorhandenes Ziel kann aktualisiert werden, indem eine PUT-Anforderung an den `/config/destinations` Endpunkt gesendet wird und die ID des Ziels, das im Anforderungspfad aktualisiert werden soll, einbezogen wird. Bei diesem Vorgang wird das Ziel im Wesentlichen _umgeschrieben_ , daher müssen im Hauptteil der Anforderung dieselben Attribute bereitgestellt werden, wie bei der Erstellung eines neuen Ziels.

>[!CAUTION]
>Die API-Antwort auf die Aktualisierungsanforderung ist sofort verfügbar, die Änderungen an den Projektionen werden jedoch asynchron angewendet. Mit anderen Worten, es gibt einen zeitlichen Unterschied zwischen dem Zeitpunkt, zu dem die Definition des Ziels aktualisiert wird, und dem Zeitpunkt, zu dem sie angewendet wird.

**API-Format**

```
PUT /config/destinations/{DESTINATION_ID}
```

| Parameter | Beschreibung |
|---|---|
| `{DESTINATION_ID}` | Die eindeutige ID des Projektionsziels, das aktualisiert werden soll. |

**Anfrage**

Die folgende Anforderung aktualisiert das vorhandene Ziel, um einen zweiten Speicherort (`dataCenters`) einzuschließen.

>[!IMPORTANT]
>Die PUT-Anforderung erfordert eine bestimmte `Content-Type` Kopfzeile, wie unten dargestellt. Die Verwendung eines falschen `Content-Type` Headers führt zu einem HTTP-Status-415-Fehler (nicht unterstützter Medientyp).

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/vnd.adobe.platform.projectionDestination+json' \
  -d '{
        "type": "EDGE",
        "dataCenters": [ 
          "OR1",
          "VA5" 
        ],
        "replicationPolicy": REACTIVE,
        "currentVersion": 1
      }'
```

| Eigenschaft | Beschreibung |
|---|---|
| `currentVersion` | Die aktuelle Version des vorhandenen Ziels. Der Wert des `version` Attributs bei einer Suchanfrage für das Ziel. |

**Antwort**

Die Antwort enthält die aktualisierten Details zum Ziel, einschließlich der ID und des neuen Ziels `version` .

```json
{
    "self": {
        "href": "/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7",
        "templated": false
    },
    "id": "8b90ce19-e7dd-403a-ae24-69683a6674e7",
    "type": "EDGE",
    "ttl": 8000,
    "dataCenters": [
        "OR1",
        "VA5"
    ],
    "version": 2
}
```

### Ziel löschen

Wenn Ihr Unternehmen kein Projektionsziel mehr benötigt, kann es gelöscht werden, indem eine DELETE-Anforderung an den `/config/destinations` Endpunkt gesendet wird und die ID des Ziels, das Sie löschen möchten, im Anforderungspfad enthalten ist.

>[!CAUTION]
>Die API-Antwort auf die Löschanforderung erfolgt sofort, die tatsächlichen Änderungen an den Daten an den Rändern werden jedoch asynchron ausgeführt. Das heißt, die Profil-Daten werden von allen Kanten entfernt (die im Projektionsziel `dataCenters` angegeben sind), aber der Vorgang dauert einige Zeit.

**API-Format**

```
DELETE /config/destinations/{DESTINATION_ID}
```

| Parameter | Beschreibung |
|---|---|
| `{DESTINATION_ID}` | Die eindeutige ID des Projektionsziels, das Sie löschen möchten. |


**Anfrage**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/destinations/8b90ce19-e7dd-403a-ae24-69683a6674e7 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Die Löschanforderung gibt HTTP-Status 204 (Kein Inhalt) und einen leeren Antworttext zurück. Sie können bestätigen, dass der Löschvorgang erfolgreich war, indem Sie eine Suchanfrage für das Ziel mit seiner ID durchführen. Die Suche sollte den HTTP-Status 404 zurückgeben (nicht gefunden).

## Projektierungskonfigurationen

Projektionskonfigurationen liefern Informationen darüber, welche Daten an jeder Kante verfügbar sein sollten. Statt ein vollständiges Experience Data Model (XDM)-Schema an die Kante zu projizieren, stellt eine Projektion nur bestimmte Daten oder Felder aus dem Schema bereit. Ihr Unternehmen kann mehr als eine Projektionskonfiguration für jedes XDM-Schema definieren.

### Liste aller Projektionskonfigurationen

Sie können alle Projektionskonfigurationen, die für Ihr Unternehmen erstellt wurden, durch eine GET-Anforderung an den `/config/projections` Endpunkt Liste haben. Sie können dem Anforderungspfad auch optionale Parameter hinzufügen, um auf Projektionskonfigurationen für ein bestimmtes Schema zuzugreifen oder eine einzelne Projektion anhand ihres Namens zu suchen.

**API-Format**

```http
GET /config/projections
GET /config/projections?schemaName={SCHEMA_NAME}
GET /config/projections?schemaName={SCHEMA_NAME}&name={PROJECTION_NAME}
```

| Parameter | Beschreibung |
|---|---|
| `{SCHEMA_NAME}` | Der Name der Schema-Klasse, die der Projektionskonfiguration zugeordnet ist, auf die Sie zugreifen möchten. |
| `{PROJECTION_NAME}` | Der Name der Projektionskonfiguration, auf die Sie zugreifen möchten. |

>[!NOTE]
>`schemaName` ist bei Verwendung des `name` Parameters erforderlich, da ein Projektionskonfigurationsname nur im Kontext einer Schema-Klasse eindeutig ist.

**Anfrage**

Die folgende Anforderung Liste alle Projektionskonfigurationen, die mit der Experience Data Model Schema-Klasse, XDM Individuelles Profil, verknüpft sind. Für weitere Informationen über XDM und seine Rolle innerhalb der Plattform, lesen Sie bitte zunächst die [XDM System Übersicht](../../xdm/home.md).

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von Projektionskonfigurationen im Stammattribut `_embedded` zurück, die im `projectionConfigs` Array enthalten sind. Wenn keine Projektionskonfigurationen für Ihr Unternehmen vorgenommen wurden, ist das `projectionConfigs` Array leer.

```json
{
    "_links": {
        "self": {
            "href": "/data/core/ups/config/projections",
            "templated": false
        }
    },
    "_embedded": {
        "projectionConfigs": [
            {
                "_links": {
                    "destination": {
                        "href": "/data/core/ups/config/destinations/a689248a-5d2b-44af-bb70-c8f17f97011b",
                        "templated": false
                    },
                    "self": {
                        "href": "/data/core/ups/config/projections/99aed0bc-c183-4997-ada7-7843642e08f6",
                        "templated": false
                    }
                },
                "_embedded": {
                    "destination": {
                        "self": {
                            "href": "/data/core/ups/config/destinations/a689248a-5d2b-44af-bb70-c8f17f97011b",
                            "templated": false
                        },
                        "id": "a689248a-5d2b-44af-bb70-c8f17f97011b",
                        "type": "EDGE",
                        "ttl": 1000,
                        "dataCenters": [
                            "OR1"
                        ],
                        "version": 1
                    }
                },
                "selector": "strategy",
                "version": 2,
                "id": "99aed0bc-c183-4997-ada7-7843642e08f6",
                "schemaName": "_xdm.context.profile",
                "name": "adcloud_rlsa",
                "destinationId": "a689248a-5d2b-44af-bb70-c8f17f97011b"
            },
        ]
    }
}
```

### Erstellen einer Projektionskonfiguration

Sie können eine neue Projektionskonfiguration erstellen (POST), die vorgibt, welche XDM-Felder an den Kanten verfügbar gemacht werden.

**API-Format**

```http
POST /config/projections?schemaName={SCHEMA_NAME}
```

| Parameter | Beschreibung |
|---|---|
| `{SCHEMA_NAME}` | Der Name der Schema-Klasse, die der Projektionskonfiguration zugeordnet ist, auf die Sie zugreifen möchten. |

**Anfrage**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "selector": "emails,person(firstName)",
        "name": "my_test_projection",
        "destinationId": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4"
      }'
```

| Eigenschaft | Beschreibung |
|---|---|
| `selector` | Eine Zeichenfolge, die eine Liste von Eigenschaften innerhalb des Schemas enthält, die an die Kanten repliziert werden sollen. Bewährte Verfahren zum Arbeiten mit Selektoren finden Sie im Abschnitt [Selektoren](#selectors) dieses Dokuments. |
| `name` | Ein beschreibender Name für die neue Projektionskonfiguration. |
| `destinationId` | Der Bezeichner für das Edge-Ziel, auf das die Daten projiziert werden. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details der neu erstellten Projektionskonfiguration zurück.

```json
{
    "_links": {
        "destination": {
            "href": "/data/core/ups/config/destinations/cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
            "templated": false
        },
        "self": {
            "href": "/data/core/ups/config/projections/87fcd0bc-c183-4997-daf9-7843642g95a1",
            "templated": false
        }
    },
    "_embedded": {
        "destination": {
            "self": {
                "href": "/data/core/ups/config/destinations/cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
                "templated": false
            },
            "id": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4",
            "type": "EDGE",
            "ttl": 1000,
            "dataCenters": [
                "OR1"
            ],
            "version": 1
        }
    },
    "selector": "emails,person(firstName)",
    "version": 2,
    "id": "87fcd0bc-c183-4997-daf9-7843642g95a1",
    "schemaName": "_xdm.context.profile",
    "name": "my_test_projection",
    "destinationId": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4"
}
```

## Selektoren {#selectors}

Ein Selektor ist eine kommagetrennte Liste von XDM-Feldnamen. In einer Projektionskonfiguration gibt der Selektor die Eigenschaften an, die in Projektionen einbezogen werden sollen. Das Format des `selector` Parameterwerts basiert lose auf der XPath-Syntax. Die unterstützte Syntax wird unten zusammengefasst, wobei zusätzliche Beispiele als Referenz bereitgestellt werden.

### Unterstützte Syntax

* Verwenden Sie Kommas, um mehrere Felder auszuwählen. Verwenden Sie keine Leerzeichen.
* Verwenden Sie die Punktnotation, um verschachtelte Felder auszuwählen.
   * Wenn Sie beispielsweise ein Feld mit dem Namen auswählen möchten, `field` das in einem Feld mit dem Namen `foo`verschachtelt ist, verwenden Sie die Auswahl `foo.field`.
* Wenn Sie ein Feld mit Unterfeldern einbeziehen, werden alle Unterfelder standardmäßig ebenfalls projiziert. Sie können die zurückgegebenen Unterfelder jedoch mit Klammern filtern `"( )"`.
   * Gibt beispielsweise `addresses(type,city.country)` nur den Adresstyp und das Land zurück, in dem sich die Adresse für jedes `addresses` Array-Element befindet.
   * Das obige Beispiel entspricht `addresses.type,addresses.city.country`dem Szenario

>[!NOTE]
>Sowohl die Punktnotation als auch die Klammernnotation werden für das Referenzieren von Unterfeldern unterstützt. Es empfiehlt sich jedoch, die Punktnotation zu verwenden, da sie präziser ist und eine bessere Darstellung der Feldhierarchie bietet.

* Jedes Feld in einem Selektor wird relativ zum Stammverzeichnis der Antwort angegeben.
   * Wenn es sich bei den Daten um eine Sammlung von Ressourcen handelt, enthält die Projektion ein Array von Ressourcen.
   * Wenn es sich bei den Daten um eine einzelne Ressource handelt, enthält die Projektion Felder, die relativ zu dieser Ressource sind.
   * Wenn das ausgewählte Feld ein Array ist (oder Teil eines Arrays ist), enthält die Projektion den ausgewählten Teil aller Elemente im Array.

### Beispiele für den Parameter &quot;selector&quot;

Die folgenden Beispiele zeigen Beispielparameter, gefolgt von `selector` den strukturierten Werten, die sie darstellen.

**person.lastName**

Gibt das `lastName` Unterfeld des `person` Objekts in der angeforderten Ressource zurück.

```json
{
  "person": {
    "lastName": "Smith"
  }
}
```

**Adressen**

Gibt alle Elemente im `addresses` Array zurück, einschließlich aller Felder in jedem Element, jedoch keine anderen Felder.

```json
{
  "addresses": [
    {
      "type": "home",
      "street1": "100 Great Mall Parkway",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    },
    {
      "type": "work",
      "street1": "1 Main Street",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    }
  ]
}
```

**person.lastName,address**

Gibt das `person.lastName` Feld und alle Elemente im `addresses` Array zurück.

```json
{
  "person": {
    "lastName": "Smith"
  },
  "addresses": [
    {
      "type": "home",
      "street1": "100 Great Mall Parkway",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    },
    {
      "type": "work",
      "street1": "1 Main Street",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    }
  ]
}
```

**address.city**

Gibt nur das Ortsfeld für alle Elemente im Adressarray zurück.

```json
{
  "addresses": [
    {
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    },
    {
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    }
  ]
}
```

>[!NOTE]
>Wenn ein verschachteltes Feld zurückgegeben wird, enthält die Projektion die zugehörigen übergeordneten Objekte. Die übergeordneten Felder enthalten keine anderen untergeordneten Felder, es sei denn, sie werden explizit ausgewählt.

**address(type,city)**

Gibt nur die Werte der Felder `type` und `city` Felder für jedes Element im `addresses` Array zurück. Alle anderen Unterfelder, die in jedem `addresses` Element enthalten sind, werden herausgefiltert.

```json
{
  "addresses": [
    {
      "type": "home",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    },
    {
      "type": "work",
      "city": {
        "name": "San Jose",
        "country": "United States"
      }
    }
  ]
}
```

## Nächste Schritte

In diesem Handbuch werden die Schritte zum Konfigurieren von Edge-Projektionen und -Zielen beschrieben, einschließlich der richtigen Formatierung des `selector` Parameters. Sie können jetzt neue Edgeziele und Projektionen erstellen, die speziell auf die Anforderungen Ihres Unternehmens zugeschnitten sind. Weitere über die Profil-API verfügbare Aktionen finden Sie im Entwicklerhandbuch [zur](getting-started.md)Echtzeit-Client-Profil-API.