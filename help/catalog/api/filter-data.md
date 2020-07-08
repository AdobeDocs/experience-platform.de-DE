---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Filtern von Katalogdaten mithilfe von Abfrage-Parametern
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '2060'
ht-degree: 1%

---


# Filtern von Katalogdaten mithilfe von Abfrage-Parametern

Die Catalog Service API ermöglicht das Filtern von Antwortdaten mithilfe von Anforderungsparametern für die Abfrage. Zu den Best Practices für Catalog gehört die Verwendung von Filtern in allen API-Aufrufen, da sie die Belastung der API reduzieren und die Gesamtleistung verbessern.

In diesem Dokument werden die am häufigsten verwendeten Methoden zum Filtern von Katalogobjekten in der API beschrieben. Es wird empfohlen, dass Sie dieses Dokument beim Lesen des Entwicklerhandbuchs für [Kataloge](getting-started.md) referenzieren, um mehr über die Interaktion mit der Katalog-API zu erfahren. Allgemeine Informationen zum Katalogdienst finden Sie in der [Katalogübersicht](../home.md).

## Zurückgegebene Objekte beschränken

Der Parameter `limit` Abfrage beschränkt die Anzahl der in einer Antwort zurückgegebenen Objekte. Die Katalogantworten werden automatisch nach konfigurierten Beschränkungen gemessen:

* Wenn kein `limit` Parameter angegeben ist, beträgt die maximale Anzahl von Objekten pro Antwortnutzlast 20.
* Bei DataSet-Abfragen `observableSchema` beträgt die maximale Anzahl der zurückgegebenen Datensätze 20, wenn der Parameter `properties` Abfrage verwendet wird.
* Die globale Beschränkung für alle anderen Katalogobjekte beträgt 100 Abfragen.
* Ungültige `limit` Parameter (einschließlich `limit=0`) führen zu 400-stufigen Fehlerantworten, die die richtigen Bereiche umreißen.
* Einschränkungen oder Offsets, die als Parameter für die Abfrage übergeben werden, haben Vorrang vor denen, die als Kopfzeilen übergeben werden.

**API-Format**

```http
GET /{OBJECT_TYPE}?limit={LIMIT}
```

| Parameter | Beschreibung |
| --- | --- |
| `{OBJECT_TYPE}` | Der Typ des abzurufenden Katalogobjekts. Gültige Objekte sind: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{LIMIT}` | Eine Ganzzahl, die die Anzahl der zurückzugebenden Objekte im Bereich von 1 bis 100 angibt. |

**Anfrage**

Mit der folgenden Anforderung wird eine Liste von Datensätzen abgerufen, während die Antwort auf drei Objekte beschränkt wird.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?limit=3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von Datensätzen zurück, die auf die vom Parameter &quot; `limit` Abfrage&quot;angegebene Anzahl beschränkt ist.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset 1",
        "description": "Description of dataset.",
        "files": "@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"
    },
    "5bb276b03a14440000971552": {
        "name": "Sample Dataset 2",
        "description": "Description of dataset.",
        "files": "@/dataSets/5bb276b03a14440000971552/views/5bb276b01250b012f9acc75b/files"
    },
    "5bceaa4c26c115000039b24b": {
        "name": "Sample Dataset 3"
    }
}
```

## Anzeigen von Eigenschaften begrenzen

Selbst beim Filtern der Anzahl der zurückgegebenen Objekte mithilfe des `limit` Parameters können die zurückgegebenen Objekte häufig mehr Informationen enthalten, als Sie tatsächlich benötigen. Um die Belastung des Systems weiter zu reduzieren, sollten Sie die Antworten so filtern, dass nur die Eigenschaften einbezogen werden, die Sie benötigen.

Der `properties` Parameter Filters antwortet Objekte, die nur eine Reihe von angegebenen Eigenschaften zurückgeben. Der Parameter kann so eingestellt werden, dass eine oder mehrere Eigenschaften zurückgegeben werden.

Der `properties` Parameter akzeptiert nur Objekteigenschaften der obersten Ebene, d. h. für das folgende Beispielobjekt können Sie Filter für `name`, `description`und `subItem`, jedoch NICHT für anwenden `sampleKey`.

```json
{
  "5ba9452f7de80400007fc52a": {
      "name": "Sample Dataset",
      "description": "Sample dataset containing important data",
      "subitem": {
          "sampleKey": "sampleValue"
      }
  }
}
```

**API-Format**

```http
GET /{OBJECT_TYPE}?properties={PROPERTY}
GET /{OBJECT_TYPE}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| Parameter | Beschreibung |
| --- | --- |
| `{OBJECT_TYPE}` | Der Typ des abzurufenden Katalogobjekts. Gültige Objekte sind: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY}` | Der Name eines Attributs, das im Antworttext enthalten sein soll. |
| `{OBJECT_ID}` | Die eindeutige Kennung eines bestimmten Katalogobjekts, das abgerufen wird. |

**Anfrage**

Die folgende Anforderung ruft eine Liste von Datensätzen ab. Die kommagetrennte Liste der Eigenschaftsnamen, die unter dem `properties` Parameter bereitgestellt werden, gibt die Eigenschaften an, die in der Antwort zurückgegeben werden sollen. Es wird auch ein `limit` Parameter einbezogen, der die Anzahl der zurückgegebenen Datensätze begrenzt. Wenn die Anforderung keinen `limit` Parameter enthält, enthält die Antwort maximal 20 Objekte.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=4&properties=name,schemaRef' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von Katalogobjekten zurück, bei der nur die angeforderten Eigenschaften angezeigt werden.

```json
{
    "Dataset1": {
        "name": "Dataset 1",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/bc82c518380478b59a95c63e0f843121",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    },
    "Dataset2": {},
    "Dataset3": {
        "name": {},
    },
    "Dataset4": {
        "name": "Dataset 4",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/142afb78d8b368a5ba97a6cc8fc7e033",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    }
}
```

Auf der Grundlage der obigen Antwort kann Folgendes abgeleitet werden:

* Wenn einem Objekt angeforderte Eigenschaften fehlen, werden nur die angeforderten Eigenschaften angezeigt, die es enthält. (`Dataset1`)
* Wenn ein Objekt keine der angeforderten Eigenschaften enthält, wird es als leeres Objekt angezeigt. (`Dataset2`)
* Ein Datensatz gibt möglicherweise eine angeforderte Eigenschaft als leeres Objekt zurück, wenn er die Eigenschaft enthält, aber kein Wert vorhanden ist. (`Dataset3`)
* Andernfalls zeigt der Datensatz den vollständigen Wert aller angeforderten Eigenschaften an. (`Dataset4`)

## Offset-Startindex der Antwort-Liste

Der Parameter `start` &quot;Abfrage&quot;versetzt die Liste der Antwort mit einer angegebenen Anzahl vorwärts, wobei eine Nummerierung mit Null verwendet wird. Beispielsweise `start=2` würde die Antwort auf Beginn auf dem dritten aufgelisteten Objekt versetzt.

Wenn der `start` Parameter nicht mit einem `limit` Parameter gepaart wird, beträgt die maximale Anzahl der zurückgegebenen Objekte 20.

**API-Format**

```http
GET /{OBJECT_TYPE}?start={OFFSET}
```

| Parameter | Beschreibung |
| --- | --- |
| `{OBJECT_TYPE}` | Der Typ des abzurufenden Katalogobjekts. Gültige Objekte sind: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OFFSET}` | Eine Ganzzahl, die die Anzahl der Objekte angibt, um die die Antwort versetzt werden soll. |

**Anfrage**

Mit der folgenden Anforderung wird eine Liste von Datensätzen abgerufen, wobei der Vergleich zum fünften Objekt (`start=4`) erfolgt und die Antwort auf zwei zurückgegebene Datensätze beschränkt wird (`limit=2`).

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?start=4&limit=2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Die Antwort enthält ein JSON-Objekt mit zwei Elementen der obersten Ebene (`limit=2`), einem für jeden Datensatz und seinen Details (Details wurden im Beispiel zusammengefasst). Die Antwort wird um vier (`start=4`) verschoben, d. h. die angezeigten Datensätze sind chronologisch die Nummern fünf und sechs.

```json
{
    "Dataset5": {},
    "Dataset6": {}
}
```

## Nach Tag filtern

Einige Katalogobjekte unterstützen die Verwendung eines `tags` Attributs. Tags können Informationen an ein Objekt anhängen und später zum Abrufen dieses Objekts verwendet werden. Welche Tags verwendet und wie sie angewendet werden sollen, hängt von Ihren organisatorischen Prozessen ab.

Bei der Verwendung von Tags sind einige Einschränkungen zu beachten:

* Die einzigen Katalogobjekte, die Tags derzeit unterstützen, sind Datensätze, Stapel und Verbindungen.
* Tag-Namen sind für Ihre IMS-Organisation eindeutig.
* Adobe-Prozesse können Tags für bestimmte Verhaltensweisen nutzen. Den Namen dieser Tags wird standardmäßig &quot;adobe&quot;vorangestellt. Daher sollten Sie diese Konvention beim Deklarieren von Tag-Namen vermeiden.
* Die folgenden Tag-Namen sind für die Verwendung in der gesamten Experience Platform reserviert und können daher nicht als Tag-Name für Ihr Unternehmen deklariert werden:
   * `unifiedProfile`: Dieser Tag-Name ist für Datasets reserviert, die vom [Echtzeit-Kunden-Profil](../../profile/home.md)erfasst werden sollen.
   * `unifiedIdentity`: Dieser Tag-Name ist für Datensätze reserviert, die vom [Identitätsdienst](../../identity-service/home.md)erfasst werden sollen.

Nachfolgend finden Sie ein Beispiel für einen Datensatz, der eine `tags` Eigenschaft enthält. Die Tags in dieser Eigenschaft haben die Form von Schlüssel-Wert-Paaren, wobei jeder Tag-Wert als Array mit einer einzelnen Zeichenfolge angezeigt wird:

```json
{
    "5be1f2ecc73c1714ceba66e2": {
        "imsOrg": "{IMS_ORG}",
        "tags": {
            "sampleTag": [
                "123456"
            ],
            "secondTag": [
                "sample_tag_value"
            ]
        },
        "name": "Sample Dataset",
        "description": "Same dataset containing sample data.",
        "dule": {
            "identity": [
                "I1"
            ]
        },
        "statsCache": {},
        "state": "DRAFT",
        "lastBatchId": "ca12b29612bf4052872edad59573703c",
        "lastBatchStatus": "success",
        "lastSuccessfulBatch": "ca12b29612bf4052872edad59573703c",
        "namespace": "{NAMESPACE}",
        "createdUser": "{CREATED_USER}",
        "createdClient": "{CREATED_CLIENT}",
        "updatedUser": "{UPDATED_USER}",
        "version": "1.0.0",
        "created": 1541534444286,
        "updated": 1541534444286
    }
}
```

**API-Format**

Die Werte für den `tags` Parameter werden in Form von Schlüssel-Wert-Paaren im Format `{TAG_NAME}:{TAG_VALUE}`verwendet. Mehrere Schlüssel/Wert-Paare können in Form einer kommagetrennten Liste bereitgestellt werden. Wenn mehrere Tags bereitgestellt werden, wird eine UND-Beziehung angenommen.

Der Parameter unterstützt Platzhalterzeichen (`*`) für Tag-Werte. Eine Suchzeichenfolge von `test*` gibt beispielsweise jedes Objekt zurück, bei dem der Tag-Wert mit &quot;test&quot;beginnt. Eine Suchzeichenfolge, die ausschließlich aus einem Platzhalter besteht, kann verwendet werden, um Objekte unabhängig von ihrem Wert zu filtern, je nachdem, ob sie ein bestimmtes Tag enthalten oder nicht.

```http
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}
GET /{OBJECT_TYPE}?tags={TAG_NAME_1}:{TAG_VALUE_1},{TAG_NAME_2}:{TAG_VALUE_2}
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}*
GET /{OBJECT_TYPE}?tags={TAG_NAME}:*
```

| Parameter | Beschreibung |
| --- | --- |
| `{OBJECT_TYPE}` | Der Typ des abzurufenden Katalogobjekts. Gültige Objekte sind: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li></ul> |
| `{TAG_NAME}` | Der Name des Tags, nach dem gefiltert werden soll. |
| `{TAG_VALUE}` | Der Wert des Tags, nach dem gefiltert werden soll. Unterstützt Platzhalterzeichen (`*`). |

**Anfrage**

Mit der folgenden Anforderung wird eine Liste von Datensätzen abgerufen, die nach einem Tag mit einem bestimmten Wert gefiltert werden, wobei das zweite Tag vorhanden ist.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?tags=sampleTag:123456,secondTag:* \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von Datensätzen zurück, die `sampleTag` den Wert &quot;123456&quot;und `secondTag` einen beliebigen Wert enthalten. Sofern keine Begrenzung angegeben ist, enthält die Antwort maximal 20 Objekte.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{IMS_ORG}",
            "name": "Example Dataset 1",
            "created": 1533539550237,
            "updated": 1533539552416,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "tags": {
                "sampleTag": [
                    "123456"
                ],
                "secondTag": [
                    "Example tag value"
                ]
            },
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.0",
            "imsOrg": "{IMS_ORG}",
            "name": "Example Dataset 2",
            "created": 1533539550237,
            "updated": 1533539552416,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "tags": {
                "sampleTag": [
                    "123456"
                ],
                "secondTag": [
                    "A different tag value"
                ],
                "anotherTag": [
                    "2.0"
                ]
            },
            "dule": {},
            "statsCache": {}
    }
}
```

## Nach Datumsbereich filtern

Einige Endpunkte in der Katalog-API verfügen über Abfragen-Parameter, die eine Abfrage in einem bestimmten Bereich zulassen, meist bei Datumsangaben.

**API-Format**

```http
GET /batches?createdAfter={TIMESTAMP_1}&createdBefore={TIMESTAMP_2}
```

| Parameter | Beschreibung |
| --- | --- |
| `{TIMESTAMP }` | Eine datetime integer in Unix Epoch time. |

**Anfrage**

Mit der folgenden Anforderung wird eine Liste der im April 2019 erstellten Stapel abgerufen.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/batches?createdAfter=1554076800000&createdBefore=1556668799000' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort enthält eine Liste von Katalogobjekten, die innerhalb des angegebenen Datumsbereichs liegen. Sofern keine Begrenzung angegeben ist, enthält die Antwort maximal 20 Objekte.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{IMS_ORG}",
            "name": "Example Dataset 1",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.0",
            "imsOrg": "{IMS_ORG}",
            "name": "Example Dataset 2",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    }
}
```

## Nach Eigenschaft sortieren

Mit dem Parameter &quot; `orderBy` Abfrage&quot;können Sie Antwortdaten basierend auf einem angegebenen Eigenschaftswert sortieren. Dieser Parameter erfordert eine &quot;Richtung&quot;(`asc` für aufsteigende oder absteigende Werte), gefolgt von einem Doppelpunkt ( `desc``:`) und dann einer Eigenschaft, nach der die Ergebnisse sortiert werden. Wenn keine Richtung angegeben ist, wird die Standardrichtung aufsteigend festgelegt.

Mehrere Sortiereigenschaften können in einer kommagetrennten Liste bereitgestellt werden. Wenn die erste Sortiereigenschaft mehrere Objekte erzeugt, die denselben Wert für diese Eigenschaft enthalten, wird die zweite Sortiereigenschaft verwendet, um diese übereinstimmenden Objekte weiter zu sortieren.

Betrachten Sie beispielsweise die folgende Abfrage: `orderBy=name,desc:created`. Die Ergebnisse werden in aufsteigender Reihenfolge nach der ersten Sortiereigenschaft sortiert `name`. In Fällen, in denen mehrere Datensätze dieselbe `name` Eigenschaft haben, werden diese übereinstimmenden Datensätze nach der zweiten Sortiereigenschaft sortiert `created`. Wenn keine zurückgegebenen Datensätze dasselbe aufweisen `name`, wird die Sortierung von der `created` Eigenschaft nicht berücksichtigt.


**API-Format**

```http
GET /{OBJECT_TYPE}?orderBy=asc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy=desc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy={PROPERTY_NAME_1},desc:{PROPERTY_NAME_2}
```

| Parameter | Beschreibung |
| --- | --- |
| `{OBJECT_TYPE}` | Der Typ des abzurufenden Katalogobjekts. Gültige Objekte sind: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY_NAME}` | Der Name einer Eigenschaft, nach der die Ergebnisse sortiert werden sollen. |

**Anfrage**

Die folgende Anforderung ruft eine Liste von Datensätzen ab, die nach ihrer `name` Eigenschaft sortiert sind. Wenn Datasets dasselbe aufweisen `name`werden diese Datensätze in absteigender Reihenfolge nach ihrer `updated` Eigenschaft sortiert.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?orderBy=name,desc:updated' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort enthält eine Liste von Katalogobjekten, die gemäß dem `orderBy` Parameter sortiert werden. Sofern keine Begrenzung angegeben ist, enthält die Antwort maximal 20 Objekte.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{IMS_ORG}",
            "name": "0405",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.3",
            "imsOrg": "{IMS_ORG}",
            "name": "AAM Dataset",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5cd3a129ec106214b722a939": {
            "version": "1.0.2",
            "imsOrg": "{IMS_ORG}",
            "name": "AAM Dataset",
            "created": 1554028394852,
            "updated": 1554130582960,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    }
}
```

## Nach Eigenschaft filtern

Der Katalog bietet zwei Methoden zum Filtern nach Eigenschaft, die in den folgenden Abschnitten näher erläutert werden:

* [Verwenden einfacher Filter](#using-simple-filters): Filtern Sie, ob eine bestimmte Eigenschaft mit einem bestimmten Wert übereinstimmt.
* [Verwenden des Eigenschaftsparameters](#using-the-property-parameter): Verwenden Sie bedingte Ausdruck, um zu filtern, ob eine Eigenschaft vorhanden ist oder ob der Wert einer Eigenschaft mit einem anderen angegebenen Wert oder einem regulären Ausdruck übereinstimmt, einen Näherungswert erreicht oder mit diesem vergleicht.

### Verwenden einfacher Filter {#using-simple-filters}

Mit einfachen Filtern können Sie Antworten basierend auf bestimmten Eigenschaftswerten filtern. Ein einfacher Filter hat die Form `{PROPERTY_NAME}={VALUE}`.

Beispielsweise `name=exampleName` gibt die Abfrage nur Objekte zurück, deren `name` Eigenschaft den Wert &quot;exampleName&quot;enthält. Im Gegensatz dazu `name=!exampleName` gibt die Abfrage nur Objekte zurück, deren `name` Eigenschaft **nicht** &quot;exampleName&quot;lautet.

Darüber hinaus unterstützen einfache Filter die Möglichkeit, mehrere Werte für eine Eigenschaft Abfrage. Wenn mehrere Werte angegeben sind, gibt die Antwort Objekte zurück, deren Eigenschaft mit **einem** der Werte in der bereitgestellten Liste übereinstimmt. Sie können eine Abfrage mit mehreren Werten umkehren, indem Sie der Liste ein `!` Zeichen voranstellen und nur Objekte zurückgeben, deren Eigenschaftswert **nicht** in der angegebenen Liste enthalten ist (z. B. `name=!exampleName,anotherName`).

**API-Format**

```http
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE_1},{VALUE_2},{VALUE_3}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE_1},{VALUE_2},{VALUE_3}
```

| Parameter | Beschreibung |
| --- | --- |
| `{OBJECT_TYPE}` | Der Typ des abzurufenden Katalogobjekts. Gültige Objekte sind: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY_NAME}` | Der Name der Eigenschaft, nach deren Wert Sie filtern möchten. |
| `{VALUE}` | Ein Eigenschaftswert, der bestimmt, welche Ergebnisse je nach Abfrage ein- oder ausgeschlossen werden sollen. |

**Anfrage**

Die folgende Anforderung ruft eine Liste von Datensätzen ab, die gefiltert werden, um nur Datensätze einzuschließen, deren `name` Eigenschaft den Wert &quot;exampleName&quot;oder &quot;anotherName&quot;hat.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?name=exampleName,anotherName' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort enthält eine Liste von Datensätzen, wobei alle Datensätze ausgeschlossen sind, deren Name `name` &quot;exampleName&quot;oder &quot;anotherName&quot;lautet. Sofern keine Begrenzung angegeben ist, enthält die Antwort maximal 20 Objekte.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{IMS_ORG}",
            "name": "exampleName",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.3",
            "imsOrg": "{IMS_ORG}",
            "name": "anotherName",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    }
}
```

### Verwenden des `property` Parameters {#using-the-property-parameter}

Der Parameter `property` &quot;Abfrage&quot;bietet mehr Flexibilität bei der eigenschaftsbasierten Filterung als einfache Filter. Neben der Filterung, die darauf basiert, ob eine Eigenschaft einen bestimmten Wert hat, kann der `property` Parameter auch andere Vergleichsoperatoren (wie &quot;Größer-als&quot;(`>`) und &quot;Kleiner-als&quot;(`<`)) sowie reguläre Ausdruck verwenden, um nach Eigenschaftswerten zu filtern. Sie kann auch nach dem Vorhandensein oder Nichtvorhandensein einer Eigenschaft filtern, unabhängig vom Wert.

Der `property` Parameter akzeptiert nur Objekteigenschaften der obersten Ebene. Das bedeutet, dass Sie für das folgende Beispielobjekt nach Eigenschaften, Eigenschaften `name`und `description`, jedoch NICHT nach `subItem``sampleKey`filtern können.

```json
{
  "5ba9452f7de80400007fc52a": {
      "name": "Sample Dataset",
      "description": "Sample dataset containing important data",
      "subitem": {
          "sampleKey": "sampleValue"
      }
  }
}
```

**API-Format**

```http
GET /{OBJECT_TYPE}?property={CONDITION}
```

| Parameter | Beschreibung |
| --- | --- |
| `{OBJECT_TYPE}` | Der Typ des abzurufenden Katalogobjekts. Gültige Objekte sind: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{CONDITION}` | Ein bedingter Ausdruck, der angibt, für welche Eigenschaft eine Abfrage erfolgen soll und wie deren Wert ausgewertet werden soll. Nachfolgend finden Sie Beispiele. |

Der `property` Parameterwert unterstützt mehrere verschiedene Typen von bedingten Ausdrücken. Die folgende Tabelle enthält eine grundlegende Syntax für unterstützte Ausdruck:

| Symbol(e) | Beschreibung | Beispiel |
| --- | --- | --- |
| (None) | Wenn Sie den Eigenschaftsnamen ohne Operator festlegen, werden nur Objekte zurückgegeben, bei denen die Eigenschaft vorhanden ist, unabhängig von ihrem Wert. | `property=name` |
| ! | Wenn Sie dem Wert eines`!`Parameters ein &quot; `property` &quot;voranstellen, werden nur Objekte zurückgegeben, für die die Eigenschaft **nicht** vorhanden ist. | `property=!name` |
| ~ | Gibt nur Objekte zurück, deren Eigenschaftswerte (Zeichenfolge) mit einem regulären Ausdruck übereinstimmen, der nach dem Tilde-Symbol (`~`) angegeben wurde. | `property=name~^example` |
| == | Gibt nur Objekte zurück, deren Eigenschaftswerte exakt mit der Zeichenfolge übereinstimmen, die nach dem Dublette-gleich-Symbol (`==`) angegeben wurde. | `property=name==exampleName` |
| != | Gibt nur Objekte zurück, deren Eigenschaftswerte **nicht** mit der Zeichenfolge übereinstimmen, die nach dem Symbol nicht gleich angegeben wird (`!=`). | `property=name!=exampleName` |
| &lt; | Gibt nur Objekte zurück, deren Eigenschaftswerte kleiner als (aber nicht gleich) ein angegebener Betrag sind. | `property=version<1.0.0` |
| &lt;= | Gibt nur Objekte zurück, deren Eigenschaftswerte kleiner als (oder gleich) ein angegebener Betrag sind. | `property=version<=1.0.0` |
| > | Gibt nur Objekte zurück, deren Eigenschaftswerte einen angegebenen Betrag überschreiten (jedoch nicht gleich). | `property=version>1.0.0` |
| >= | Gibt nur Objekte zurück, deren Eigenschaftswerte größer als (oder gleich) ein angegebener Betrag sind. | `property=version>=1.0.0` |

>[!NOTE]
>
>Die `name` Eigenschaft unterstützt die Verwendung eines Platzhalters `*`, entweder als gesamte Suchzeichenfolge oder als Teil davon. Platzhalter entsprechen leeren Zeichen, sodass die Suchzeichenfolge mit dem Wert &quot;test&quot;übereinstimmt. `te*st` Sterbliche Risiken werden durch Verdopplung entkommen (`**`). Ein Dublette-Sternchen in einer Suchzeichenfolge stellt ein einzelnes Sternchen als Zeichenfolge dar.

**Anfrage**

Die folgende Anforderung gibt alle Datensätze mit einer Versionsnummer über 1.0.3 zurück.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?property=version>1.0.3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort enthält eine Liste von Datensätzen, deren Versionsnummern größer als 1.0.3 sind. Sofern keine Begrenzung angegeben ist, enthält die Antwort maximal 20 Objekte.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.1.2",
            "imsOrg": "{IMS_ORG}",
            "name": "sampleDataset",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.6",
            "imsOrg": "{IMS_ORG}",
            "name": "exampleDataset",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5cd3a129ec106214b722a939": {
            "version": "1.0.4",
            "imsOrg": "{IMS_ORG}",
            "name": "anotherDataset",
            "created": 1554028394852,
            "updated": 1554130582960,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    }
}
```

## Mehrere Filter kombinieren

Mit einem kaufmännischen kaufmännischen Und (`&`) können Sie mehrere Filter in einer einzigen Anforderung kombinieren. Wenn einer Anforderung zusätzliche Bedingungen hinzugefügt werden, wird eine UND-Beziehung angenommen.

**API-Format**

```http
GET /{OBJECT_TYPE}?{FILTER_1}={VALUE}&{FILTER_2}={VALUE}&{FILTER_3}={VALUE}
```
