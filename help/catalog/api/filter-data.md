---
keywords: Experience Platform;Startseite;beliebte Themen;filter;filter;filter;daten filtern;datumsbereich
solution: Experience Platform
title: Filtern von Katalogdaten mithilfe von Abfrageparametern
description: Verwenden Sie Abfrageparameter, um Antwortdaten in der Catalog Service-API zu filtern und nur die benötigten Informationen abzurufen. Wenden Sie Filter auf Ihre API-Aufrufe an, um die Auslastung zu reduzieren und die Leistung zu verbessern, sodass Daten schneller und effizienter abgerufen werden können.
exl-id: 0cdb5a7e-527b-46be-9ad8-5337c8dc72b7
source-git-commit: 14ecb971af3f6cdcc605caa05ef6609ecb9b38fd
workflow-type: tm+mt
source-wordcount: '2339'
ht-degree: 68%

---

# Filtern [!DNL Catalog] Daten mithilfe von Abfrageparametern

Um die Leistung zu verbessern und relevante Ergebnisse abzurufen, verwenden Sie Abfrageparameter zum Filtern [!DNL Catalog Service] API-Antwortdaten.

Erfahren Sie mehr über gängige Filtermethoden für [!DNL Catalog] in der API. Verwenden Sie dieses Dokument zusammen mit dem [Katalog-Entwicklerhandbuch](getting-started.md) für weitere Informationen zu API-Interaktionen. Allgemeine [!DNL Catalog Service] finden Sie unter [[!DNL Catalog] Übersicht](../home.md).

## Zurückgegebene Objekte begrenzen {#limit-returned-objects}

Der `limit` Abfrageparameter beschränkt die Anzahl der in einer Antwort zurückgegebenen Objekte. [!DNL Catalog] Antworten folgen vordefinierten Grenzwerten:

* Wenn der `limit` nicht angegeben ist, beträgt die maximale Anzahl von Objekten pro Antwort 20.
* Bei Datensatzabfragen beträgt die maximale Zahl der zurückgegebenen Datensätze 20, wenn `observableSchema` mit dem `properties`-Abfrageparameter angefragt wird.
* Für Benutzer-Token ist die Obergrenze 1.
* Für Service-Token beträgt die Obergrenze 20.
* Die globale Begrenzung für andere Katalogabfragen beträgt 100 Objekte.
* Ungültige `limit` (einschließlich `limit=0`) führen zu Fehlerantworten auf 400-Ebene, die die richtigen Bereiche angeben.
* Als Abfrageparameter übergebene Limits oder Offsets haben Vorrang vor denen in Kopfzeilen.

**API-Format**

```http
GET /{OBJECT_TYPE}?limit={LIMIT}
```

| Parameter | Beschreibung |
| --- | --- |
| `{OBJECT_TYPE}` | Der Typ [!DNL Catalog] abzurufenden Objekts. Gültige Objekte: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{LIMIT}` | Eine Ganzzahl, die die Anzahl der zurückzugebenden Objekte angibt (Bereich: 1-100). |

**Anfrage**

Mit der folgenden Anfrage wird eine Liste von Datensätzen abgerufen, während die Antwort auf drei Objekte beschränkt wird.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?limit=3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste mit Datensätzen zurück, die auf die vom Abfrageparameter `limit` angegebene Zahl beschränkt ist.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset 1",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5ba9452f7de80400007fc52a"
    },
    "5bb276b03a14440000971552": {
        "name": "Sample Dataset 2",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5bb276b03a14440000971552"
    },
    "5bceaa4c26c115000039b24b": {
        "name": "Sample Dataset 3"
    }
}
```

## Angezeigte Eigenschaften beschränken {#limit-displayed-properties}

Trotz Filterns der Zahl der zurückgegebenen Objekte mithilfe des `limit`-Parameters können die zurückgegebenen Objekte häufig mehr Daten enthalten, als Sie in Wahrheit benötigen. Um die Systemlast weiter zu verringern, sollten Sie Antworten so filtern, dass nur die Eigenschaften einbezogen werden, die Sie tatsächlich brauchen.

Der `properties`-Parameter filtert Antwortobjekte so, dass nur bestimmte angegebene Eigenschaften zurückgeben werden. Der Parameter kann so eingerichtet werden, dass eine oder mehrere Eigenschaften zurückgegeben werden.

Der `properties`-Parameter akzeptiert Eigenschaften von Objekten beliebiger Ebenen. `sampleKey` können mit `?properties=subItem.sampleKey` extrahiert werden.

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
| `{OBJECT_TYPE}` | Der Typ [!DNL Catalog] abzurufenden Objekts. Gültige Objekte sind: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{PROPERTY}` | Der Name eines Attributs, das im Antworttext enthalten sein soll. |
| `{OBJECT_ID}` | Die eindeutige Kennung eines bestimmten abgerufenen [!DNL Catalog]. |

**Anfrage**

Die folgende Anfrage ruft eine Liste mit Datensätzen ab. Die kommagetrennte Liste mit Eigenschaftsnamen, die unter dem Parameter `properties` zu finden ist, gibt die Eigenschaften an, die in der Antwort zurückgegeben werden sollen. Es wird auch ein `limit`-Parameter einbezogen, der die Zahl der zurückgegebenen Datensätze begrenzt. Wenn die Anfrage keinen `limit`-Parameter beinhaltet, enthält die Antwort maximal 20 Objekte.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=4&properties=name,schemaRef' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von [!DNL Catalog]-Objekten zurück, wobei nur die angeforderten Eigenschaften angezeigt werden.

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

Auf Grundlage der obigen Antwort kann Folgendes abgeleitet werden:

* Wenn bei einem Objekt angefragte Eigenschaften fehlen, werden nur die angefragten Eigenschaften angezeigt, die es tatsächlich enthält. (`Dataset1`)
* Wenn ein Objekt keine der angefragten Eigenschaften enthält, wird es als leeres Objekt angezeigt. (`Dataset2`)
* Ein Datensatz kann eine angefragte Eigenschaft als leeres Objekt zurückgeben, wenn er die Eigenschaft enthält, aber kein Wert vorhanden ist. (`Dataset3`)
* Andernfalls zeigt der Datensatz den ganzen Wert aller angefragten Eigenschaften an. (`Dataset4`)

>[!NOTE]
>
>In der `schemaRef`-Eigenschaft für jeden Datensatz gibt die Versionsnummer die neueste Nebenversion des Schemas an. Weitere Informationen finden Sie im Abschnitt zur [Schemaversionierung](../../xdm/api/getting-started.md#versioning) im XDM-API-Handbuch.

## Startindex von Antwortliste versetzen {#offset-starting-index}

Der Abfrageparameter `start` versetzt die Antwortliste um eine angegebene Zahl vorwärts, wobei Zahlen bei 0 beginnen. Beispielsweise würde `start=2` die Antwort so versetzen, dass mit dem dritten aufgelisteten Objekt begonnen wird.

Wenn der `start`-Parameter nicht zusammen mit einem `limit`-Parameter genutzt wird, beträgt die maximale Zahl der zurückgegebenen Objekte 20.

**API-Format**

```http
GET /{OBJECT_TYPE}?start={OFFSET}
```

| Parameter | Beschreibung |
| --- | --- |
| `{OBJECT_TYPE}` | Der Typ des abzurufenden Catalog-Objekts. Gültige Objekte sind: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OFFSET}` | Eine Ganzzahl, die die Zahl der Objekte angibt, um die die Antwort versetzt werden soll. |

**Anfrage**

Mit der folgenden Anfrage wird eine Liste von Datensätzen abgerufen, wobei auf das fünfte Objekt versetzt (`start=4`) und die Antwort auf zwei zurückgegebene Datensätze beschränkt wird (`limit=2`).

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?start=4&limit=2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Die Antwort enthält ein JSON-Objekt mit zwei Elementen der obersten Ebene (`limit=2`) – eines für jeden Datensatz – und ihren Details (die Details wurden im Beispiel gekürzt). Die Antwort wird um vier (`start=4`) versetzt, d. h. die angezeigten Datensätze sind chronologisch die Nummern 5 und 6.

```json
{
    "Dataset5": {},
    "Dataset6": {}
}
```

## Anhand von Tag filtern

Einige Catalog-Objekte unterstützen die Verwendung eines `tags`-Attributs. Tags können Daten an ein Objekt anhängen und später zum Abrufen des Objekts verwendet werden. Welche Tags wie genutzt werden sollten, hängt von den Prozessen in Ihrer Organisation ab.

Bei Verwendung von Tags sind einige Einschränkungen zu beachten:

* Die einzigen Catalog-Objekte, die derzeit Tags unterstützen, sind Datensätze, Batches und Verbindungen.
* Tag-Namen sind für Ihr Unternehmen eindeutig.
* Adobe-Prozesse können Tags für bestimmte Verhaltensweisen nutzen. Den Namen dieser Tags wird standardmäßig „adobe“ vorangestellt. Daher sollten Sie diese Konvention beim Deklarieren von Tag-Namen vermeiden.
* Die folgenden Tag-Namen sind für die Verwendung in [!DNL Experience Platform] reserviert und können daher nicht als Tag-Name für Ihr Unternehmen deklariert werden:
   * `unifiedProfile`: Dieser Tag-Name ist für Datensätze reserviert, die von [[!DNL Real-Time Customer Profile]](../../profile/home.md) aufgenommen werden sollen.
   * `unifiedIdentity`: Dieser Tag-Name ist für Datensätze reserviert, die von [[!DNL Identity Service]](../../identity-service/home.md) aufgenommen werden sollen.

Nachfolgend finden Sie ein Beispiel für einen Datensatz, der eine `tags`-Eigenschaft enthält. Die Tags in dieser Eigenschaft haben die Form von Schlüssel-Wert-Paaren, wobei jeder Tag-Wert als Array mit einer einzelnen Zeichenfolge angezeigt wird:

```json
{
    "5be1f2ecc73c1714ceba66e2": {
        "imsOrg": "{ORG_ID}",
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

Werte für den `tags`-Parameter haben die Form von Schlüssel-Wert-Paaren, wobei das Format `{TAG_NAME}:{TAG_VALUE}` zum Einsatz kommt. Mehrere Schlüssel-Wert-Paare können in Form einer kommagetrennten Liste angegeben werden. Wenn verschiedene Tags angegeben werden, wird eine UND-Beziehung angenommen.

Der Parameter unterstützt Platzhalterzeichen (`*`) für Tag-Werte. Die Suchzeichenfolge `test*` beispielsweise gibt alle Objekte zurück, bei denen der Tag-Wert mit „test“ beginnt. Eine ausschließlich aus einem Platzhalter bestehende Suchzeichenfolge kann dazu dienen, Objekte unabhängig von ihrem Wert danach zu filtern, ob sie ein bestimmtes Tag enthalten oder nicht.

```http
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}
GET /{OBJECT_TYPE}?tags={TAG_NAME_1}:{TAG_VALUE_1},{TAG_NAME_2}:{TAG_VALUE_2}
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}*
GET /{OBJECT_TYPE}?tags={TAG_NAME}:*
```

| Parameter | Beschreibung |
| --- | --- |
| `{OBJECT_TYPE}` | Der Typ [!DNL Catalog] abzurufenden Objekts. Gültige Objekte sind: <ul><li>`batches`</li><li>`dataSets`</li></ul> |
| `{TAG_NAME}` | Der Name des Tags, nach dem gefiltert werden soll. |
| `{TAG_VALUE}` | Der Wert des Tags, nach dem gefiltert werden soll. Unterstützt Platzhalterzeichen (`*`). |

**Anfrage**

Mit der folgenden Anfrage wird eine Liste von Datensätzen abgerufen, wobei danach gefiltert wird, ob ein Tag einen bestimmten Wert hat UND das zweite Tag vorhanden ist.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?tags=sampleTag:123456,secondTag:* \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste mit Datensätzen zurück, die `sampleTag` mit einem Wert von „123456“ UND `secondTag` mit einem beliebigen Wert enthalten. Sofern keine Begrenzung angegeben wurde, enthält die Antwort maximal 20 Objekte.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
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
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.0",
            "imsOrg": "{ORG_ID}",
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
    }
}
```

## Nach Datumsbereich filtern

Einige Endpunkte in der [!DNL Catalog]-API verfügen über Abfrageparameter, die - meist im Falle von Datumsangaben - bereichsbezogene Abfragen ermöglichen.

**API-Format**

```http
GET /batches?createdAfter={TIMESTAMP_1}&createdBefore={TIMESTAMP_2}
```

| Parameter | Beschreibung |
| --- | --- |
| `{TIMESTAMP }` | Eine Datum/Uhrzeit-Ganzzahl in Unix Epoch-Zeit. |

**Anfrage**

Mit der folgenden Anfrage wird eine Liste der im April 2019 erstellten Batches abgerufen.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/batches?createdAfter=1554076800000&createdBefore=1556668799000' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort enthält eine Liste von [!DNL Catalog], die innerhalb des angegebenen Datumsbereichs liegen. Sofern keine Begrenzung angegeben wurde, enthält die Antwort maximal 20 Objekte.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
            "name": "Example Dataset 1",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.0",
            "imsOrg": "{ORG_ID}",
            "name": "Example Dataset 2",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
    }
}
```

## Nach Eigenschaft sortieren

Mit dem Abfrageparameter `orderBy` können Sie Antwortdaten basierend auf einem angegebenen Eigenschaftswert sortieren (anordnen). Dieser Parameter erfordert eine „Richtung“ (`asc` für aufsteigende oder `desc` für absteigende Werte), gefolgt von einem Doppelpunkt (`:`) und einer Eigenschaft, anhand der die Ergebnisse sortiert werden sollen. Wenn keine Richtung angegeben ist, lautet die Standardrichtung „aufsteigend“.

Mehrere Sortiereigenschaften können in einer kommagetrennten Liste angegeben werden. Wenn die erste Sortiereigenschaft mehrere Objekte ergibt, die denselben Wert für diese Eigenschaft enthalten, wird die zweite Sortiereigenschaft genutzt, um die übereinstimmenden Objekte weiter zu sortieren.

Betrachten Sie beispielsweise die folgende Abfrage: `orderBy=name,desc:created`. Ergebnisse werden anhand der ersten Sortiereigenschaft (`name`) in aufsteigender Reihenfolge sortiert. Falls mehrere Datensätze dieselbe `name`-Eigenschaft aufweisen, werden die übereinstimmenden Datensätze dann anhand der zweiten Sortiereigenschaft (`created`) sortiert. Wenn keine der zurückgegebenen Datensätze denselben `name` aufweisen, wird die Eigenschaft `created` bei der Sortierung nicht berücksichtigt.


**API-Format**

```http
GET /{OBJECT_TYPE}?orderBy=asc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy=desc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy={PROPERTY_NAME_1},desc:{PROPERTY_NAME_2}
```

| Parameter | Beschreibung |
| --- | --- |
| `{OBJECT_TYPE}` | Der Typ des abzurufenden Catalog-Objekts. Gültige Objekte sind: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{PROPERTY_NAME}` | Der Name einer Eigenschaft, anhand der die Ergebnisse sortiert werden sollen. |

**Anfrage**

Die folgende Anfrage ruft eine Liste von Datensätzen ab, sortiert anhand ihrer `name`-Eigenschaft. Wenn Datensätze denselben `name` aufweisen, werden diese Datensätze anhand ihrer `updated`-Eigenschaft in absteigender Reihenfolge sortiert.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?orderBy=name,desc:updated' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort enthält eine Liste von [!DNL Catalog], die nach dem `orderBy`-Parameter sortiert sind. Sofern keine Begrenzung angegeben wurde, enthält die Antwort maximal 20 Objekte.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
            "name": "0405",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.3",
            "imsOrg": "{ORG_ID}",
            "name": "AAM Dataset",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
    },
    "5cd3a129ec106214b722a939": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
            "name": "AAM Dataset",
            "created": 1554028394852,
            "updated": 1554130582960,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
    }
}
```

## Nach Eigenschaft filtern

[!DNL Catalog] bietet zwei Methoden zum Filtern nach Eigenschaft, die in den folgenden Abschnitten näher beschrieben werden:

* [Verwenden einfacher Filter](#using-simple-filters): Filtern Sie danach, ob eine bestimmte Eigenschaft mit einem bestimmten Wert übereinstimmt.
* [Verwenden des Eigenschaftsparameters](#using-the-property-parameter): Nutzen Sie bedingte Ausdrücke, um danach zu filtern, ob eine Eigenschaft vorhanden ist oder ob der Wert einer Eigenschaft mit einem anderen angegebenen Wert oder regulären Ausdruck übereinstimmt bzw. sich diesem nähert oder mit diesem vergleichbar ist.

>[!NOTE]
>
>Jedes Attribut eines Catalog-Objekts kann zum Filtern von Ergebnissen in der Catalog Service-API verwendet werden.

### Verwenden einfacher Filter {#using-simple-filters}

Mit einfachen Filtern können Sie Antworten anhand einzelner Eigenschaftswerte filtern. Ein einfacher Filter hat die Form `{PROPERTY_NAME}={VALUE}`.

Beispielsweise gibt die Abfrage `name=exampleName` nur Objekte zurück, deren `name`-Eigenschaft den Wert „exampleName“ enthält. Im Gegensatz dazu gibt die Abfrage `name=!exampleName` nur Objekte zurück, deren `name`-Eigenschaft **nicht** „exampleName“ lautet.

Darüber hinaus erlauben es einfache Filter, verschiedene Werte für eine Eigenschaft abzufragen. Wenn mehrere Werte bereitgestellt werden, gibt die Antwort Objekte zurück, deren Eigenschaft mit **beliebigen** Werten in der angegebenen Liste übereinstimmt. Sie können eine Abfrage mit mehreren Werten umkehren, indem Sie der Liste ein `!`-Zeichen voranstellen. So werden nur Objekte zurückgegeben, deren Eigenschaftswert **nicht** in der angegebenen Liste enthalten ist (z. B. `name=!exampleName,anotherName`).

**API-Format**

```http
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE_1},{VALUE_2},{VALUE_3}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE_1},{VALUE_2},{VALUE_3}
```

| Parameter | Beschreibung |
| --- | --- |
| `{OBJECT_TYPE}` | Der Typ [!DNL Catalog] abzurufenden Objekts. Gültige Objekte sind: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{PROPERTY_NAME}` | Der Name der Eigenschaft, nach deren Wert Sie filtern möchten. |
| `{VALUE}` | Ein Eigenschaftswert, der bestimmt, welche Ergebnisse ein- oder ausgeschlossen werden (je nach Abfrage). |

**Anfrage**

Folgende Anfrage ruft eine Liste von Datensätzen ab, die so gefiltert ist, dass nur Datensätze eingeschlossen werden, deren `name`-Eigenschaft den Wert „exampleName“ oder „anotherName“ hat.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?name=exampleName,anotherName' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort enthält eine Liste von Datensätzen, wobei alle Datensätze ausgeschlossen sind, deren `name` „exampleName“ oder „anotherName“ lautet. Sofern keine Begrenzung angegeben wurde, enthält die Antwort maximal 20 Objekte.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
            "name": "exampleName",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.3",
            "imsOrg": "{ORG_ID}",
            "name": "anotherName",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
    }
}
```

### Verwenden des `property` {#using-the-property-parameter}

Der Abfrageparameter `property` bietet bei eigenschaftsbasierter Filterung mehr Flexibilität als einfache Filter. Neben einer Filterung danach, ob eine Eigenschaft einen bestimmten Wert aufweist oder nicht, kann der `property`-Parameter auch andere Vergleichsoperatoren wie „größer als“ (`>`) und „kleiner als“ (`<`) sowie reguläre Ausdrücke verwenden, um anhand von Eigenschaftswerten zu filtern. Es kann auch nach dem Vorhandensein oder Nichtvorhandensein einer Eigenschaft gefiltert werden, unabhängig von ihrem Wert.

Verwenden Sie ein kaufmännisches Und-Zeichen (`&`), um mehrere Filter zu kombinieren und Ihre Abfrage in einer einzigen Anfrage zu verfeinern. Wenn Sie nach mehreren Feldern filtern, wird standardmäßig eine `AND` angewendet.

>[!NOTE]
>
>Wenn Sie mehrere `property` in einer einzigen Abfrage kombinieren, muss mindestens einer auf das `id`- oder `created` angewendet werden. Die folgende Abfrage gibt Objekte zurück, bei denen `id` `abc123` ist **AND** `name` nicht `test` ist:
>
>```http
>GET /datasets?property=id==abc123&property=name!=test
>```

Wenn Sie mehrere `property` für dasselbe Feld verwenden, wird nur der zuletzt angegebene Parameter wirksam.

>[!IMPORTANT]
>
>Sie **nicht** einen einzelnen `property` verwenden, um mehrere Felder gleichzeitig zu filtern. Jedes Feld muss über einen eigenen `property` verfügen. Das folgende Beispiel (`property=id>abc,name==myDataset`) ist **nicht** zulässig, da es versucht, Bedingungen auf `id` und `name` innerhalb eines **einzelnen `property`-Parameters anzuwenden**.

Der `property`-Parameter akzeptiert Eigenschaften von Objekten beliebiger Ebenen. `sampleKey` können zum Filtern mithilfe von `?properties=subItem.sampleKey` verwendet werden.

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
| `{OBJECT_TYPE}` | Der Typ [!DNL Catalog] abzurufenden Objekts. Gültige Objekte sind: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{CONDITION}` | Ein bedingter Ausdruck, der angibt, welche Eigenschaft abgefragt und wie ihr Wert ausgewertet werden soll. Nachfolgend finden Sie verschiedene Beispiele. |

Der Wert des `property`-Parameters unterstützt unterschiedliche Typen von bedingten Ausdrücken. Folgende Tabelle enthält die grundlegende Syntax für unterstützte Ausdrücke:

| Symbol(e) | Beschreibung | Beispiel |
| --- | --- | --- |
| (Keine) | Wenn Sie den Eigenschaftsnamen ohne Operator festlegen, werden nur Objekte zurückgegeben, bei denen die Eigenschaft vorhanden ist (unabhängig von ihrem Wert). | `property=name` |
| ! | Wenn Sie dem Wert eines `property`-Parameters ein „`!`“ voranstellen, werden nur Objekte zurückgegeben, bei denen die Eigenschaft **nicht** vorhanden ist. | `property=!name` |
| ~ | Gibt nur Objekte zurück, deren Eigenschaftswerte (Zeichenfolge) mit einem regulären Ausdruck übereinstimmen, der nach dem Tilde-Symbol (`~`) angegeben ist. | `property=name~^example` |
| == | Gibt nur Objekte zurück, deren Eigenschaftswerte genau mit der Zeichenfolge übereinstimmen, die nach dem doppelten Gleichheitszeichen (`==`) angegeben ist. | `property=name==exampleName` |
| != | Gibt nur Objekte zurück, deren Eigenschaftswerte **nicht** mit der Zeichenfolge übereinstimmen, die nach dem Ungleichheitszeichen (`!=`) angegeben ist. | `property=name!=exampleName` |
| &lt; | Gibt nur Objekte zurück, deren Eigenschaftswerte kleiner als ein angegebener Betrag sind (aber nicht gleich). | `property=version<1.0.0` |
| &lt;= | Gibt nur Objekte zurück, deren Eigenschaftswerte kleiner als ein angegebener Betrag sind (oder gleich). | `property=version<=1.0.0` |
| > | Gibt nur Objekte zurück, deren Eigenschaftswerte größer als ein angegebener Betrag sind (aber nicht gleich). | `property=version>1.0.0` |
| >= | Gibt nur Objekte zurück, deren Eigenschaftswerte größer als ein angegebener Betrag sind (oder gleich). | `property=version>=1.0.0` |
| * | Ein Platzhalter gilt für jede Zeichenfolgeneigenschaft und entspricht jeder Zeichenfolge. Verwenden Sie `**`, um einem literalen Sternchen zu entgehen. | `property=name==te*st` |
| und | Kombiniert mehrere `property` Parameter mit einer `AND` Beziehung zwischen ihnen. | `property=id==abc&property=name!=test` |

>[!NOTE]
>
>Die `name`-Eigenschaft unterstützt die Verwendung eines `*`, entweder als gesamte Suchzeichenfolge oder als Teil davon. Platzhalter entsprechen leeren Zeichen, sodass die Suchzeichenfolge `te*st` mit dem Wert „test“ übereinstimmt. Bei Sternchen muss durch Verdopplung (`**`) ein Escape durchgeführt werden. Ein doppeltes Sternchen in einer Suchzeichenfolge stellt ein einzelnes Sternchen als literale Zeichenfolge dar.

**Anfrage**

Die folgende Anfrage gibt alle Datensätze mit einer Versionsnummer zurück, die über 1.0.3 liegt.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?property=version>1.0.3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort enthält eine Liste von Datensätzen, deren Versionsnummern höher als 1.0.3 sind. Sofern keine Begrenzung angegeben ist, enthält die Antwort maximal 20 Objekte.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.1.2",
            "imsOrg": "{ORG_ID}",
            "name": "sampleDataset",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.6",
            "imsOrg": "{ORG_ID}",
            "name": "exampleDataset",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
    },
    "5cd3a129ec106214b722a939": {
            "version": "1.0.4",
            "imsOrg": "{ORG_ID}",
            "name": "anotherDataset",
            "created": 1554028394852,
            "updated": 1554130582960,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
    }
}
```

## Filtern von Arrays mit dem Eigenschaftsparameter {#filter-arrays}

Verwenden Sie Gleichheits- und Ungleichheitsoperatoren, um bestimmte Werte beim Filtern von Ergebnissen basierend auf Array-Eigenschaften ein- oder auszuschließen.

### Gleichheitsfilter {#equality-filters}

Um ein Array-Feld nach mehreren Werten zu filtern, verwenden Sie separate Eigenschaftsparameter für jeden Wert. Verwenden Sie Gleichheitsfilter, um nur die Einträge in den Array-Daten zurückzugeben, die den angegebenen Werten entsprechen.

>[!NOTE]
>
>Die Anforderung, beim Filtern mehrerer Felder `id` oder `created` einzuschließen, gilt **nicht** wenn mehrere Werte innerhalb eines Array-Felds gefiltert werden.

Die folgende Beispielabfrage gibt nur Ergebnisse aus dem -Array zurück, das sowohl `val1` als auch `val2` enthält.

**API-Format**

```http
GET /{OBJECT_TYPE}?property=arrayField=val1&property=arrayField=val2
```

### Ungleichheitsfilter {#inequality-filters}

Verwenden Sie Ungleichheitsoperatoren (`!=`) für ein Array-Feld, um Einträge in den Daten auszuschließen, bei denen das Array die angegebenen Werte enthält.

**API-Format**

```http
GET /{OBJECT_TYPE}?property=arrayField!=val1&property=arrayField!=val2
```

Diese Abfrage gibt Dokumente zurück, bei denen arrayField keine `val1` oder `val2` enthält.

### Einschränkungen beim Filter für Gleichheit und Ungleichheit {#equality-inequality-limitations}

Sie können nicht in einer einzigen Abfrage sowohl Gleichheit (`=`) als auch Ungleichheit (`!=`) auf dasselbe Feld anwenden.
