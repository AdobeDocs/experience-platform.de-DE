---
keywords: Experience Platform;Profil;Echtzeit-Profil von Kunden;Fehlerbehebung;API
title: Edge Promotion API-Endpunkte
topic-legacy: guide
type: Documentation
description: Mit Adobe Experience Platform können Sie koordinierte, konsistente und personalisierte Erlebnisse für Ihre Kunden über mehrere Kanal hinweg in Echtzeit bereitstellen, indem Sie die richtigen Daten bereitstellen und im Zuge von Änderungen kontinuierlich aktualisieren. Dies geschieht durch die Verwendung von Kanten, einem geografisch platzierten Server, der Daten speichert und für Anwendungen leicht zugänglich macht.
exl-id: ce429164-8e87-412d-9a9d-e0d4738c7815
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1964'
ht-degree: 7%

---

# Endpunkte für Edge-Projektionen und Ziele

Um koordinierte, konsistente und personalisierte Erlebnisse für Ihre Kunden über mehrere Kanal hinweg in Echtzeit zu ermöglichen, müssen die richtigen Daten jederzeit verfügbar sein und im Zuge von Änderungen kontinuierlich aktualisiert werden. Adobe Experience Platform ermöglicht diesen Echtzeitzugriff auf Daten mithilfe sogenannter Edges. Ein Edge ist ein regional aufgestellter Server, der Daten erfasst und direkt für Anwendungen abrufbar macht. Adoben wie Adobe Target und Adobe Campaign verwenden beispielsweise Kanten, um personalisierte Kundenerlebnisse in Echtzeit bereitzustellen. Die Daten werden mittels Projektion an einen Edge übermittelt, wobei ein Projektionsziel den Edge definiert, an den die Daten gesendet werden, und eine Projektionskonfiguration, die die Informationen spezifiziert, die am Edge zur Verfügung gestellt werden. In diesem Handbuch finden Sie detaillierte Anweisungen zur Verwendung der API [!DNL Real-time Customer Profile] für die Verwendung von Edge-Projektionen, einschließlich Zielen und Konfigurationen.

## Erste Schritte

Der in diesem Handbuch verwendete API-Endpunkt ist Teil von [[!DNL Real-time Customer Profile API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml). Bevor Sie fortfahren, lesen Sie bitte im Handbuch [Erste Schritte](getting-started.md) nach Links zu entsprechenden Dokumentationen, einem Leitfaden zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtigen Informationen zu erforderlichen Kopfzeilen, die für das erfolgreiche Aufrufen einer [!DNL Experience Platform]-API erforderlich sind.

>[!NOTE]
>
>Anforderungen, die eine Nutzlast (POST, PUT, PATCH) enthalten, erfordern einen `Content-Type`-Header. In diesem Dokument wird mehr als ein `Content-Type` verwendet. Achten Sie besonders auf die Header in den Beispielaufrufen, um sicherzustellen, dass Sie für jede Anforderung die richtige `Content-Type` verwenden.

## Projektionsziele

Eine Projektion kann zu einer oder mehreren Kanten geleitet werden, indem die Stellen angegeben werden, an denen Daten gesendet werden sollen. Jedes erstellte Projektionsziel hat eine eindeutige ID, die dann zur Erstellung der Projektionskonfiguration verwendet wird.

### Liste aller Ziele

Sie können die Edgeziele, die für Ihr Unternehmen bereits erstellt wurden, durch eine GET an den `/config/destinations`-Endpunkt Liste haben.

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

Die Antwort enthält ein `projectionDestinations`-Array mit den Details für jedes Ziel, das als einzelnes Objekt innerhalb des Arrays angezeigt wird. Wenn keine Projektionen konfiguriert wurden, gibt das `projectionDestinations`-Array leer zurück.

>[!NOTE]
>
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
| `_links.self.href` | Entspricht auf der obersten Ebene dem Pfad, der für die Anforderung des GET verwendet wurde. Innerhalb jedes einzelnen Zielobjekts kann dieser Pfad in einer GET verwendet werden, um die Details eines bestimmten Ziels direkt zu suchen. |
| `id` | Innerhalb jedes Zielobjekts zeigt `"id"` die schreibgeschützte, systemgenerierte eindeutige ID für das Ziel an. Diese ID wird beim Referenzieren eines bestimmten Ziels und beim Erstellen von Projektionskonfigurationen verwendet. |

Weitere Informationen zu den Attributen eines einzelnen Ziels finden Sie im folgenden Abschnitt unter [Erstellen eines Ziels](#create-a-destination).

### Ziel {#create-a-destination} erstellen

Wenn das gewünschte Ziel noch nicht vorhanden ist, können Sie ein neues Projektionsziel erstellen, indem Sie eine POST an den `/config/destinations`-Endpunkt anfordern.

**API-Format**

```http
POST /config/destinations
```

**Anfrage**

Mit der folgenden Anforderung wird ein neues Edge-Ziel erstellt.

>[!NOTE]
>
>Die POST-Anforderung zum Erstellen eines Ziels erfordert eine bestimmte `Content-Type`-Kopfzeile, wie unten dargestellt. Die Verwendung eines falschen `Content-Type`-Headers führt zu einem HTTP-Status-415-Fehler (nicht unterstützter Medientyp).

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

Wenn Sie die eindeutige ID eines Projektionsziels kennen, können Sie eine Suchanfrage ausführen, um die Details Ansicht. Dies geschieht, indem eine GET an den `/config/destinations`-Endpunkt und die ID des Ziels im Anforderungspfad angefordert wird.

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

Das Antwortobjekt zeigt die Details des Projektionsziels an. Das `id`-Attribut sollte mit der ID des Projektionsziels übereinstimmen, das in der Anforderung bereitgestellt wurde.

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

Ein vorhandenes Ziel kann aktualisiert werden, indem eine PUT an den `/config/destinations`-Endpunkt angefordert wird und die ID des Ziels, das im Anforderungspfad aktualisiert werden soll, einbezogen wird. Bei diesem Vorgang wird das Ziel im Wesentlichen umgeschrieben. Daher müssen im Hauptteil der Anforderung dieselben Attribute bereitgestellt werden, wie bei der Erstellung eines neuen Ziels.

>[!CAUTION]
>
>Die API-Antwort auf die Aktualisierungsanforderung ist sofort verfügbar, die Änderungen an den Projektionen werden jedoch asynchron angewendet. Mit anderen Worten, es gibt einen zeitlichen Unterschied zwischen dem Zeitpunkt, zu dem die Definition des Ziels aktualisiert wird, und dem Zeitpunkt, zu dem sie angewendet wird.

**API-Format**

```http
PUT /config/destinations/{DESTINATION_ID}
```

| Parameter | Beschreibung |
|---|---|
| `{DESTINATION_ID}` | Die eindeutige ID des Projektionsziels, das aktualisiert werden soll. |

**Anfrage**

Mit der folgenden Anforderung wird das vorhandene Ziel aktualisiert und ein zweiter Speicherort (`dataCenters`) hinzugefügt.

>[!IMPORTANT]
>
>Die PUT-Anforderung erfordert eine bestimmte `Content-Type`-Kopfzeile, wie unten dargestellt. Die Verwendung eines falschen `Content-Type`-Headers führt zu einem HTTP-Status-415-Fehler (nicht unterstützter Medientyp).

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
| `currentVersion` | Die aktuelle Version des vorhandenen Ziels. Der Wert des Attributs `version`, wenn eine Suchanfrage für das Ziel ausgeführt wird. |

**Antwort**

Die Antwort enthält die aktualisierten Details zum Ziel, einschließlich der zugehörigen ID und dem neuen `version` des Ziels.

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

Wenn Ihr Unternehmen kein Projektionsziel mehr benötigt, kann es gelöscht werden, indem Sie eine DELETE-Anforderung an den `/config/destinations`-Endpunkt richten und die ID des Ziels einschließen, das Sie im Anforderungspfad löschen möchten.

>[!CAUTION]
>
>Die API-Antwort auf die Löschanforderung erfolgt sofort, die tatsächlichen Änderungen an den Daten an den Rändern werden jedoch asynchron ausgeführt. Das heißt, die Profil-Daten werden von allen Kanten entfernt (das im Projektionsziel angegebene `dataCenters`), aber der Vorgang dauert einige Zeit.

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

Die Löschanforderung gibt HTTP-Status 204 (Kein Inhalt) und einen leeren Antworttext zurück. Sie können bestätigen, dass der Löschvorgang erfolgreich war, indem Sie eine Suchanfrage für das Ziel mit seiner ID durchführen. Die Suche sollte den HTTP-Status 404 zurückgeben (nicht gefunden).

## Projektierungskonfigurationen

Projektionskonfigurationen liefern Informationen darüber, welche Daten an jeder Kante verfügbar sein sollten. Statt ein vollständiges [!DNL Experience Data Model] (XDM)-Schema an die Kante zu projizieren, stellt eine Projektion nur bestimmte Daten oder Felder aus dem Schema bereit. Ihr Unternehmen kann mehr als eine Projektionskonfiguration für jedes XDM-Schema definieren.

### Liste aller Projektionskonfigurationen

Sie können alle Projektionskonfigurationen, die für Ihr Unternehmen erstellt wurden, durch eine GET an den `/config/projections`-Endpunkt Liste haben. Sie können dem Anforderungspfad auch optionale Parameter hinzufügen, um auf Projektionskonfigurationen für ein bestimmtes Schema zuzugreifen oder eine einzelne Projektion anhand ihres Namens zu suchen.

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
>
>`schemaName` ist bei Verwendung des  `name` Parameters erforderlich, da ein Projektionskonfigurationsname nur im Kontext einer Schema-Klasse eindeutig ist.

**Anfrage**

Die folgende Anforderung Liste alle Projektionskonfigurationen, die mit der [!DNL Experience Data Model]-Schema-Klasse, [!DNL XDM Individual Profile] verknüpft sind. Für weitere Informationen zu XDM und seiner Rolle innerhalb von [!DNL Platform], lesen Sie bitte zunächst den [XDM Systemüberblick](../../xdm/home.md).

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/projections?schemaName=_xdm.context.profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von Projektionskonfigurationen im Stammattribut `_embedded` zurück, die im Array `projectionConfigs` enthalten ist. Wenn keine Projektionskonfigurationen für Ihr Unternehmen vorgenommen wurden, ist das Array `projectionConfigs` leer.

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

>[!NOTE]
>
>Die Konfigurationsanforderung für die POST erfordert einen bestimmten `Content-Type`-Header, wie unten dargestellt. Die Verwendung eines falschen `Content-Type`-Headers führt zu einem HTTP-Status-415-Fehler (nicht unterstützter Medientyp).

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

Ein Selektor ist eine kommagetrennte Liste von XDM-Feldnamen. In einer Projektionskonfiguration gibt der Selektor die Eigenschaften an, die in Projektionen einbezogen werden sollen. Das Format des Parameters `selector` basiert lose auf der XPath-Syntax. Die unterstützte Syntax wird unten zusammengefasst, wobei zusätzliche Beispiele als Referenz bereitgestellt werden.

### Unterstützte Syntax

* Verwenden Sie Kommas, um mehrere Felder auszuwählen. Verwenden Sie keine Leerzeichen.
* Verwenden Sie die Punktnotation, um verschachtelte Felder auszuwählen.
   * Wenn Sie beispielsweise ein Feld mit dem Namen `field` auswählen möchten, das in einem Feld mit dem Namen `foo` verschachtelt ist, verwenden Sie den Selektor `foo.field`.
* Wenn Sie ein Feld mit Unterfeldern einbeziehen, werden alle Unterfelder standardmäßig ebenfalls projiziert. Sie können die zurückgegebenen Unterfelder jedoch mit Klammern `"( )"` filtern.
   * Beispiel: `addresses(type,city.country)` gibt für jedes `addresses`-Array-Element nur den Adresstyp und das Land zurück, in dem sich der Ort der Adresse befindet.
   * Das obige Beispiel entspricht `addresses.type,addresses.city.country`.

>[!NOTE]
>
>Sowohl die Punktnotation als auch die Klammernnotation werden für das Referenzieren von Unterfeldern unterstützt. Es empfiehlt sich jedoch, die Punktnotation zu verwenden, da sie präziser ist und eine bessere Darstellung der Feldhierarchie bietet.

* Jedes Feld in einem Selektor wird relativ zum Stammverzeichnis der Antwort angegeben.
   * Wenn es sich bei den Daten um eine Sammlung von Ressourcen handelt, enthält die Projektion ein Array von Ressourcen.
   * Wenn es sich bei den Daten um eine einzelne Ressource handelt, enthält die Projektion Felder, die relativ zu dieser Ressource sind.
   * Wenn das ausgewählte Feld ein Array ist (oder Teil eines Arrays ist), enthält die Projektion den ausgewählten Teil aller Elemente im Array.

### Beispiele für den Parameter &quot;selector&quot;

Die folgenden Beispiele zeigen Beispiel-Parameter `selector` gefolgt von den strukturierten Werten, die sie darstellen.

**person.lastName**

Gibt das Unterfeld `lastName` des `person`-Objekts in der angeforderten Ressource zurück.

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

**person.lastName,address**

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
>
>Wenn ein verschachteltes Feld zurückgegeben wird, enthält die Projektion die zugehörigen übergeordneten Objekte. Die übergeordneten Felder enthalten keine anderen untergeordneten Felder, es sei denn, sie werden explizit ausgewählt.

**address(type,city)**

Gibt nur die Werte der Felder `type` und `city` für jedes Element im `addresses`-Array zurück. Alle anderen Unterfelder in jedem `addresses`-Element werden herausgefiltert.

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

In diesem Handbuch werden die Schritte zum Konfigurieren von Projektionen und Zielen beschrieben, einschließlich der richtigen Formatierung des Parameters `selector`. Sie können jetzt neue Projektionsziele und -konfigurationen erstellen, die den Anforderungen Ihres Unternehmens entsprechen.
