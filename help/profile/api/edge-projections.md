---
keywords: Experience Platform; Profil; Echtzeit-Kundenprofil; Fehlerbehebung; API
title: Edge Projektions-API-Endpunkte
topic-legacy: guide
type: Documentation
description: Mit Adobe Experience Platform können Sie koordinierte, konsistente und personalisierte Erlebnisse für Ihre Kunden in mehreren Kanälen in Echtzeit bereitstellen, indem Sie die richtigen Daten bei Änderungen sofort verfügbar machen und kontinuierlich aktualisieren. Dies geschieht mithilfe von Edges, einem geografisch platzierten Server, der Daten speichert und für Anwendungen leicht zugänglich macht.
exl-id: ce429164-8e87-412d-9a9d-e0d4738c7815
source-git-commit: 4c544170636040b8ab58780022a4c357cfa447de
workflow-type: tm+mt
source-wordcount: '1959'
ht-degree: 12%

---

# Edge-Projektionskonfigurationen und -endpunkte

Um koordinierte, konsistente und personalisierte Erlebnisse für Ihre Kunden über mehrere Kanäle hinweg in Echtzeit bieten zu können, müssen die richtigen Daten jederzeit verfügbar sein und bei Änderungen kontinuierlich aktualisiert werden. Adobe Experience Platform ermöglicht diesen Echtzeitzugriff auf Daten mithilfe sogenannter Edges. Ein Edge ist ein regional aufgestellter Server, der Daten erfasst und direkt für Anwendungen abrufbar macht. Adobe-Programme wie etwa Adobe Target und Adobe Campaign nutzen beispielsweise Edges, um personalisierte Kundenerlebnisse in Echtzeit bereitzustellen. Die Daten werden mittels Projektion an einen Edge übermittelt, wobei ein Projektionsziel den Edge definiert, an den die Daten gesendet werden, und eine Projektionskonfiguration, die die Informationen spezifiziert, die am Edge zur Verfügung gestellt werden. Dieses Handbuch enthält ausführliche Anweisungen zur Verwendung der [!DNL Real-time Customer Profile]-API für die Verwendung mit Edge-Projektionen, einschließlich Zielen und Konfigurationen.

## Erste Schritte

Der in diesem Handbuch verwendete API-Endpunkt ist Teil von [[!DNL Real-time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Bevor Sie fortfahren, schauen Sie bitte im Handbuch in [Erste Schritte](getting-started.md) nach Links zu entsprechenden Dokumentationen, einem Leitfaden zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtigen Informationen zu erforderlichen Kopfzeilen, die für das Aufrufen einer [!DNL Experience Platform]-API erforderlich sind.

>[!NOTE]
>
>Anforderungen, die eine Payload enthalten (POST, PUT, PATCH), erfordern einen `Content-Type` -Header. In diesem Dokument wird mehr als ein `Content-Type` verwendet. Achten Sie besonders auf die Header in den Beispielaufrufen, um sicherzustellen, dass Sie für jede Anfrage die richtige `Content-Type` verwenden.

## Projektionsziele

Eine Projektion kann an eine oder mehrere Edges weitergeleitet werden, indem die Orte angegeben werden, an die Daten gesendet werden sollen. Jedes Projektionsziel, das erstellt wird, verfügt über eine eindeutige ID, die dann zur Erstellung der Projektionskonfiguration verwendet wird.

### Alle Ziele auflisten

Sie können die für Ihr Unternehmen bereits erstellten Edge-Ziele auflisten, indem Sie eine GET-Anfrage an den Endpunkt `/config/destinations` stellen.

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

Die Antwort enthält ein `projectionDestinations`-Array mit den Details für jedes Ziel, das als einzelnes Objekt innerhalb des Arrays angezeigt wird. Wenn keine Projektionen konfiguriert wurden, gibt das Array `projectionDestinations` leer zurück.

>[!NOTE]
>
>Diese Antwort wurde aus Platzgründen gekürzt und zeigt nur zwei Ziele an.

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
| `_links.self.href` | Auf der obersten Ebene stimmt mit dem Pfad überein, der für die GET-Anfrage verwendet wurde. Innerhalb jedes einzelnen Zielobjekts kann dieser Pfad in einer GET-Anfrage verwendet werden, um die Details eines bestimmten Ziels direkt zu suchen. |
| `id` | Innerhalb jedes Zielobjekts zeigt `"id"` die schreibgeschützte, systemgenerierte eindeutige ID für das Ziel an. Diese ID wird verwendet, wenn auf ein bestimmtes Ziel verwiesen und Projektionskonfigurationen erstellt werden. |

Weitere Informationen zu den Attributen eines einzelnen Ziels finden Sie im folgenden Abschnitt zum Erstellen eines Ziels](#create-a-destination) .[

### Ziel erstellen {#create-a-destination}

Wenn das gewünschte Ziel noch nicht vorhanden ist, können Sie ein neues Projektionsziel erstellen, indem Sie eine POST-Anfrage an den Endpunkt `/config/destinations` senden.

**API-Format**

```http
POST /config/destinations
```

**Anfrage**

Die folgende Anfrage erstellt ein neues Edge-Ziel.

>[!NOTE]
>
>Die POST-Anfrage zum Erstellen eines Ziels erfordert eine bestimmte `Content-Type`-Kopfzeile, wie unten dargestellt. Die Verwendung einer falschen `Content-Type`-Kopfzeile führt zu einem HTTP-Status-Fehler 415 (Nicht unterstützter Medientyp).

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
| `type` **(Erforderlich)** | Der Typ des zu erstellenden Ziels. Der einzige akzeptierte Wert &quot;EDGE&quot;erstellt ein Edge-Ziel. |
| `dataCenters` **(Erforderlich)** | Ein Zeichenfolgen-Array, das die Kanten auflistet, zu denen Projektionen weitergeleitet werden sollen. Kann einen oder mehrere der folgenden Werte enthalten: &quot;OR1&quot; - Westliche Vereinigte Staaten, &quot;VA5&quot; - OstVereinigte Staaten, &quot;NLD1&quot; - EMEA. |
| `ttl` **(Erforderlich)** | Gibt den Projektionsablauf an. Zulässiger Wertebereich: 600 bis 604800. Standardwert: 3600. |
| `replicationPolicy` **(Erforderlich)** | Definiert das Verhalten der Datenreplikation vom Hub zu den Edges.  Unterstützte Werte: PROAKTIV, REAKTIV. Standardwert: REAKTIV. |

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
| `self.href` | Dieser Pfad wird verwendet, um das Ziel direkt zu suchen (GET) und kann auch zum Aktualisieren (PUT) oder Löschen (DELETE) des Ziels verwendet werden. |
| `id` | Die schreibgeschützte, systemgenerierte eindeutige ID für das Ziel. Diese ID wird verwendet, um beim Erstellen von Projektionskonfigurationen direkt auf das Ziel zu verweisen. |
| `version` | Dieser schreibgeschützte Wert zeigt die aktuelle Version des Ziels an. Wenn ein Ziel aktualisiert wird, wird die Versionsnummer automatisch inkrementiert. |

### Ziel anzeigen

Wenn Sie die eindeutige ID eines Projektionsziels kennen, können Sie eine Suchanfrage ausführen, um die Details anzuzeigen. Dies geschieht, indem Sie eine GET-Anfrage an den Endpunkt `/config/destinations` senden und die Kennung des Ziels im Anfragepfad einschließen.

**API-Format**

```http
GET /config/destinations/{DESTINATION_ID}
```

| Parameter | Beschreibung |
|---|---|
| `{DESTINATION_ID}` | Die eindeutige ID des Projektionsziels, das Sie anzeigen möchten. |

**Anfrage**

Die folgende Anfrage führt eine Suche (GET) durch, um das Ziel für die im Anfragepfad bereitgestellte ID anzuzeigen.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/destinations/9d66c06e-c745-480c-b64c-1d5234d25f4b \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Das Antwortobjekt zeigt die Details des Projektionsziels an. Das Attribut `id` sollte mit der ID des Projektionsziels übereinstimmen, das in der Anfrage angegeben wurde.

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

Ein vorhandenes Ziel kann aktualisiert werden, indem eine PUT-Anfrage an den `/config/destinations`-Endpunkt gesendet wird und die Kennung des Ziels, das im Anfragepfad aktualisiert werden soll, enthalten ist. Bei diesem Vorgang wird das Ziel im Wesentlichen neu geschrieben. Daher müssen im Text der Anfrage dieselben Attribute bereitgestellt werden, die beim Erstellen eines neuen Ziels bereitgestellt werden.

>[!CAUTION]
>
>Die API-Antwort auf die Aktualisierungsanforderung ist sofort, die Änderungen an den Projektionen werden jedoch asynchron angewendet. Das heißt, es gibt einen zeitlichen Unterschied zwischen der Aktualisierung der Zieldefinition und der Anwendung.

**API-Format**

```http
PUT /config/destinations/{DESTINATION_ID}
```

| Parameter | Beschreibung |
|---|---|
| `{DESTINATION_ID}` | Die eindeutige ID des Projektionsziels, das Sie aktualisieren möchten. |

**Anfrage**

Die folgende Anfrage aktualisiert das vorhandene Ziel, um einen zweiten Ort (`dataCenters`) einzuschließen.

>[!IMPORTANT]
>
>Die PUT-Anfrage erfordert eine bestimmte `Content-Type` -Kopfzeile, wie unten dargestellt. Die Verwendung einer falschen `Content-Type`-Kopfzeile führt zu einem HTTP-Status-Fehler 415 (Nicht unterstützter Medientyp).

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
| `currentVersion` | Die aktuelle Version des vorhandenen Ziels. Der Wert des Attributs `version` bei der Durchführung einer Suchanfrage für das Ziel. |

**Antwort**

Die Antwort enthält die aktualisierten Details für das Ziel, einschließlich der Kennung und der neuen `version` des Ziels.

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

Wenn Ihr Unternehmen kein Projektionsziel mehr benötigt, kann es gelöscht werden, indem Sie eine DELETE-Anfrage an den `/config/destinations`-Endpunkt senden und die Kennung des Ziels, das Sie löschen möchten, im Anfragepfad einschließen.

>[!CAUTION]
>
>Die API-Antwort auf die Löschanfrage ist sofort, die tatsächlichen Änderungen an den Daten an den Edges erfolgen jedoch asynchron. Mit anderen Worten: Die Profildaten werden aus allen Kanten entfernt (die im Projektionsziel angegebene `dataCenters`), aber der Prozess dauert einige Zeit.

**API-Format**

```http
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

Die Löschanfrage gibt den HTTP-Status 204 (Kein Inhalt) und einen leeren Antworttext zurück. Sie können bestätigen, dass der Löschvorgang erfolgreich war, indem Sie eine Suchanfrage nach der zugehörigen Kennung für das Ziel ausführen. Die Suche sollte den HTTP-Status 404 (Nicht gefunden) zurückgeben.

## Projektionskonfigurationen

Projektionskonfigurationen liefern Informationen dazu, welche Daten an den einzelnen Edge-Knoten verfügbar sein sollen. Statt ein vollständiges [!DNL Experience Data Model] (XDM)-Schema an den Rand zu projizieren, stellt eine Projektion nur bestimmte Daten oder Felder aus dem Schema bereit. Ihr Unternehmen kann mehr als eine Projektionskonfiguration für jedes XDM-Schema definieren.

### Alle Projektionskonfigurationen auflisten

Sie können alle Projektionskonfigurationen auflisten, die für Ihr Unternehmen erstellt wurden, indem Sie eine GET-Anfrage an den Endpunkt `/config/projections` stellen. Sie können dem Anfragepfad auch optionale Parameter hinzufügen, um auf Projektionskonfigurationen für ein bestimmtes Schema zuzugreifen oder eine einzelne Projektion anhand ihres Namens zu suchen.

**API-Format**

```http
GET /config/projections
GET /config/projections?schemaName={SCHEMA_NAME}
GET /config/projections?schemaName={SCHEMA_NAME}&name={PROJECTION_NAME}
```

| Parameter | Beschreibung |
|---|---|
| `{SCHEMA_NAME}` | Der Name der Schemaklasse, die mit der Projektionskonfiguration verknüpft ist, auf die Sie zugreifen möchten. |
| `{PROJECTION_NAME}` | Der Name der Projektionskonfiguration, auf die Sie zugreifen möchten. |

>[!NOTE]
>
>`schemaName` ist bei Verwendung des  `name` Parameters erforderlich, da ein Projektionskonfigurationsname nur im Kontext einer Schemaklasse eindeutig ist.

**Anfrage**

Die folgende Anfrage listet alle Projektionskonfigurationen auf, die mit der Schemaklasse [!DNL Experience Data Model], [!DNL XDM Individual Profile], verknüpft sind. Weitere Informationen zu XDM und seiner Rolle in [!DNL Platform] finden Sie in der [XDM-Systemübersicht](../../xdm/home.md).

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von Projektionskonfigurationen im Attribut root `_embedded` zurück, die im Array `projectionConfigs` enthalten ist. Wenn für Ihre Organisation keine Projektionskonfigurationen vorgenommen wurden, ist das `projectionConfigs` -Array leer.

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

Sie können eine neue Projektionskonfiguration erstellen (POST), die bestimmt, welche XDM-Felder an den Kanten verfügbar gemacht werden.

**API-Format**

```http
POST /config/projections?schemaName={SCHEMA_NAME}
```

| Parameter | Beschreibung |
|---|---|
| `{SCHEMA_NAME}` | Der Name der Schemaklasse, die mit der Projektionskonfiguration verknüpft ist, auf die Sie zugreifen möchten. |

**Anfrage**

>[!NOTE]
>
>Die Konfigurationsanforderung für die POST erfordert eine bestimmte `Content-Type` -Kopfzeile, wie unten dargestellt. Die Verwendung einer falschen `Content-Type`-Kopfzeile führt zu einem HTTP-Status-Fehler 415 (Nicht unterstützter Medientyp).

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/vnd.adobe.platform.projectionConfig+json; version=1' \
  -d '{
        "selector": "emails,person(firstName)",
        "name": "my_test_projection",
        "destinationId": "cc5a3bd1-f2b9-4965-b9bd-4e7416a02cd4"
      }'
```

| Eigenschaft | Beschreibung |
|---|---|
| `selector` | Eine Zeichenfolge, die eine Liste von Eigenschaften innerhalb des Schemas enthält, die an den Kanten repliziert werden sollen. Best Practices für die Arbeit mit Selektoren finden Sie im Abschnitt [Selektoren](#selectors) dieses Dokuments. |
| `name` | Ein beschreibender Name für die neue Projektionskonfiguration. |
| `destinationId` | Die Kennung für das Edge-Ziel, auf das die Daten projiziert werden. |

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

Ein Selektor ist eine kommagetrennte Liste von XDM-Feldnamen. In einer Projektionskonfiguration gibt der Selektor die Eigenschaften an, die in Projektionen einbezogen werden sollen. Das Format des Parameterwerts `selector` basiert lose auf der XPath-Syntax. Die unterstützte Syntax ist unten zusammengefasst, einschließlich zusätzlicher Beispiele als Referenz.

### Unterstützte Syntax

* Verwenden Sie Kommas, um mehrere Felder auszuwählen. Verwenden Sie keine Leerzeichen.
* Verwenden Sie Punktnotation zur Auswahl verschachtelter Felder.
   * Um beispielsweise ein Feld mit dem Namen `field` auszuwählen, das in einem Feld mit dem Namen `foo` verschachtelt ist, verwenden Sie den Selektor `foo.field`.
* Beim Einschließen eines Felds, das Unterfelder enthält, werden standardmäßig auch alle Unterfelder projiziert. Sie können die zurückgegebenen Unterfelder jedoch mit Klammern `"( )"` filtern.
   * `addresses(type,city.country)` gibt beispielsweise für jedes Array-Element `addresses` nur den Adresstyp und das Land zurück, in dem sich die Adresse &quot;city&quot;befindet.
   * Das obige Beispiel entspricht `addresses.type,addresses.city.country`.

>[!NOTE]
>
>Für das Referenzieren von Unterfeldern werden sowohl Punktnotation als auch Klammern unterstützt. Es empfiehlt sich jedoch, die Punktnotation zu verwenden, da sie kürzer ist und eine bessere Darstellung der Felderhierarchie bietet.

* Jedes Feld in einem Selektor wird relativ zum Stammverzeichnis der Antwort angegeben.
   * Wenn es sich bei den Daten um eine Sammlung von Ressourcen handelt, enthält die Projektion ein Array von Ressourcen.
   * Wenn es sich bei den Daten um eine einzelne Ressource handelt, enthält die Projektion Felder, die relativ zu dieser Ressource sind.
   * Wenn das ausgewählte Feld ein Array ist (oder Teil eines Arrays ist), enthält die Projektion den ausgewählten Teil aller Elemente im Array.

### Beispiele für den Selektorparameter

Die folgenden Beispiele zeigen Beispiel-Parameter `selector`, gefolgt von den strukturierten Werten, die sie darstellen.

**person.lastName**

Gibt das Unterfeld `lastName` des Objekts `person` in der angeforderten Ressource zurück.

```json
{
  "person": {
    "lastName": "Smith"
  }
}
```

**Adressen**

Gibt alle Elemente im Array `addresses` zurück, einschließlich aller Felder in jedem Element, jedoch keine anderen Felder.

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

**person.lastName,addresses**

Gibt das Feld `person.lastName` und alle Elemente im Array `addresses` zurück.

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

**addresses.city**

Gibt nur das Feld &quot;city&quot;für alle Elemente im Adressen-Array zurück.

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
>
>Wenn ein verschachteltes Feld zurückgegeben wird, enthält die Projektion die umschließenden übergeordneten Objekte. Die übergeordneten Felder enthalten keine anderen untergeordneten Felder, es sei denn, sie sind ebenfalls explizit ausgewählt.

**address(type,city)**

Gibt nur die Werte der Felder `type` und `city` für jedes Element im Array `addresses` zurück. Alle anderen Unterfelder, die in jedem `addresses` -Element enthalten sind, werden herausgefiltert.

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

In diesem Handbuch werden die Schritte erläutert, die zur Konfiguration von Projektionen und Zielen erforderlich sind, einschließlich der richtigen Formatierung des Parameters `selector` . Sie können jetzt neue Projektionsziele und Konfigurationen erstellen, die speziell auf die Anforderungen Ihres Unternehmens abgestimmt sind.
