---
keywords: Experience Platform; Startseite; beliebte Themen; Filter; Filtern; Daten filtern; Daten filtern; Datumsbereich
solution: Experience Platform
title: Filtern von Katalogdaten mithilfe von Abfrageparametern
topic-legacy: developer guide
description: Die Catalog Service-API ermöglicht ein Filtern von Antwortdaten mithilfe von Abfrageparametern für Anfragen. Zu den Best Practices bei Catalog gehört die Verwendung von Filtern in allen API-Aufrufen, da sie die Last der API reduzieren und die Gesamtleistung verbessern.
exl-id: 0cdb5a7e-527b-46be-9ad8-5337c8dc72b7
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '2121'
ht-degree: 88%

---

# Filter [!DNL Catalog] Daten mithilfe von Abfrageparametern

Die [!DNL Catalog Service] API ermöglicht die Filterung von Antwortdaten mithilfe von Abfrageparametern für Anfragen. Teil der Best Practices für [!DNL Catalog] verwendet Filter in allen API-Aufrufen, da sie die Auslastung der API reduzieren und die Gesamtleistung verbessern.

In diesem Dokument werden die gängigsten Filtermethoden beschrieben [!DNL Catalog] -Objekte in der API. Wir empfehlen Ihnen, dieses Dokument beim Lesen des [Entwicklerhandbuchs zu ](getting-started.md) als Referenz zu nutzen, um mehr über die Interaktion mit der Catalog-API zu erfahren.[!DNL Catalog] Allgemeine Informationen: [!DNL Catalog Service], siehe [[!DNL Catalog] Übersicht](../home.md).

## Zurückgegebene Objekte begrenzen

Der Abfrageparameter `limit` begrenzt die Zahl der in einer Antwort zurückgegebenen Objekte. [!DNL Catalog] -Antworten werden automatisch entsprechend den konfigurierten Beschränkungen gemessen:

* Wenn kein `limit`-Parameter angegeben ist, beträgt die maximale Zahl von Objekten pro Antwort-Payload 20.
* Bei Datensatzabfragen beträgt die maximale Zahl der zurückgegebenen Datensätze 20, wenn `observableSchema` mit dem `properties`-Abfrageparameter angefragt wird.
* Die globale Begrenzung für alle anderen Catalog-Abfragen beträgt 100 Objekte.
* Ungültige `limit`-Parameter (einschließlich `limit=0`) führen zu Fehlerantworten der Stufe 400, in der richtige Bereiche angegeben werden.
* Beschränkungen oder Verschiebungen, die als Abfrageparameter übergeben werden, haben Vorrang vor jenen, die als Kopfzeilen übergeben werden.

**API-Format**

```http
GET /{OBJECT_TYPE}?limit={LIMIT}
```

| Parameter | Beschreibung |
| --- | --- |
| `{OBJECT_TYPE}` | Der Typ von [!DNL Catalog] -Objekt, das abgerufen werden soll. Gültige Objekte sind: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{LIMIT}` | Eine Ganzzahl, die die Zahl der zurückzugebenden Objekte angibt (im Bereich von 1 bis 100). |

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

## Angezeigte Eigenschaften beschränken

Trotz Filterns der Zahl der zurückgegebenen Objekte mithilfe des `limit`-Parameters können die zurückgegebenen Objekte häufig mehr Daten enthalten, als Sie in Wahrheit benötigen. Um die Systemlast weiter zu verringern, sollten Sie Antworten so filtern, dass nur die Eigenschaften einbezogen werden, die Sie tatsächlich brauchen.

Der `properties`-Parameter filtert Antwortobjekte so, dass nur bestimmte angegebene Eigenschaften zurückgeben werden. Der Parameter kann so eingerichtet werden, dass eine oder mehrere Eigenschaften zurückgegeben werden.

Der `properties`-Parameter akzeptiert nur Objekteigenschaften der obersten Ebene. Für das folgende Beispielobjekt können Sie Filter also auf `name`, `description` und `subItem`, NICHT aber auf `sampleKey` anwenden.

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
| `{OBJECT_TYPE}` | Der Typ von [!DNL Catalog] -Objekt, das abgerufen werden soll. Gültige Objekte sind: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY}` | Der Name eines Attributs, das im Antworttext enthalten sein soll. |
| `{OBJECT_ID}` | Die eindeutige Kennung eines bestimmten [!DNL Catalog] -Objekt abgerufen werden. |

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

Eine erfolgreiche Antwort gibt eine Liste von [!DNL Catalog] -Objekte, bei denen nur die angeforderten Eigenschaften angezeigt werden.

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
>Im `schemaRef` -Eigenschaft für jeden Datensatz angeben, zeigt die Versionsnummer die neueste Nebenversion des Schemas an. Weitere Informationen finden Sie im Abschnitt zur [Schemaversionierung](../../xdm/api/getting-started.md#versioning) im XDM-API-Handbuch.

## Startindex von Antwortliste versetzen

Der Abfrageparameter `start` versetzt die Antwortliste um eine angegebene Zahl vorwärts, wobei Zahlen bei 0 beginnen. Beispielsweise würde `start=2` die Antwort so versetzen, dass mit dem dritten aufgelisteten Objekt begonnen wird.

Wenn der `start`-Parameter nicht zusammen mit einem `limit`-Parameter genutzt wird, beträgt die maximale Zahl der zurückgegebenen Objekte 20.

**API-Format**

```http
GET /{OBJECT_TYPE}?start={OFFSET}
```

| Parameter | Beschreibung |
| --- | --- |
| `{OBJECT_TYPE}` | Der Typ des abzurufenden Catalog-Objekts. Gültige Objekte sind: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
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
* Tag-Namen sind für Ihre IMS-Organisation eindeutig.
* Adobe-Prozesse können Tags für bestimmte Verhaltensweisen nutzen. Den Namen dieser Tags wird standardmäßig „adobe“ vorangestellt. Daher sollten Sie diese Konvention beim Deklarieren von Tag-Namen vermeiden.
* Die folgenden Tag-Namen sind für die Verwendung in allen [!DNL Experience Platform]und kann daher nicht als Tag-Name für Ihre Organisation deklariert werden:
   * `unifiedProfile`: Dieser Tag-Name ist für Datensätze reserviert, die von [[!DNL Real-time Customer Profile]](../../profile/home.md) erfasst werden sollen.
   * `unifiedIdentity`: Dieser Tag-Name ist für Datensätze reserviert, die von [[!DNL Identity Service]](../../identity-service/home.md) erfasst werden sollen.

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
| `{OBJECT_TYPE}` | Der Typ von [!DNL Catalog] -Objekt, das abgerufen werden soll. Gültige Objekte sind: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li></ul> |
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
            "dule": {},
            "statsCache": {}
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
            "dule": {},
            "statsCache": {}
    }
}
```

## Nach Datumsbereich filtern

Einige Endpunkte im [!DNL Catalog] API verfügt über Abfrageparameter, die Abfragen in verschiedenen Bereichen ermöglichen, meist bei Datumsangaben.

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

Eine erfolgreiche Antwort enthält eine Liste von [!DNL Catalog] Objekte, die in den angegebenen Datumsbereich fallen. Sofern keine Begrenzung angegeben wurde, enthält die Antwort maximal 20 Objekte.

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
            "dule": {},
            "statsCache": {}
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
            "dule": {},
            "statsCache": {}
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
| `{OBJECT_TYPE}` | Der Typ des abzurufenden Catalog-Objekts. Gültige Objekte sind: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
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

Eine erfolgreiche Antwort enthält eine Liste von [!DNL Catalog] Objekte, die nach `orderBy` Parameter. Sofern keine Begrenzung angegeben wurde, enthält die Antwort maximal 20 Objekte.

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
            "dule": {},
            "statsCache": {}
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
            "dule": {},
            "statsCache": {}
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
            "dule": {},
            "statsCache": {}
    }
}
```

## Nach Eigenschaft filtern

[!DNL Catalog] bietet zwei Methoden zum Filtern anhand von Eigenschaften, die in den folgenden Abschnitten genauer erläutert werden:

* [Verwenden einfacher Filter](#using-simple-filters): Filtern Sie danach, ob eine bestimmte Eigenschaft mit einem bestimmten Wert übereinstimmt.
* [Verwenden des Eigenschaftsparameters](#using-the-property-parameter): Nutzen Sie bedingte Ausdrücke, um danach zu filtern, ob eine Eigenschaft vorhanden ist oder ob der Wert einer Eigenschaft mit einem anderen angegebenen Wert oder regulären Ausdruck übereinstimmt bzw. sich diesem nähert oder mit diesem vergleichbar ist.

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
| `{OBJECT_TYPE}` | Der Typ von [!DNL Catalog] -Objekt, das abgerufen werden soll. Gültige Objekte sind: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
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
            "dule": {},
            "statsCache": {}
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
            "dule": {},
            "statsCache": {}
    }
}
```

### Verwenden des `property`-Parameters {#using-the-property-parameter}

Der Abfrageparameter `property` bietet bei eigenschaftsbasierter Filterung mehr Flexibilität als einfache Filter. Neben einer Filterung danach, ob eine Eigenschaft einen bestimmten Wert aufweist oder nicht, kann der `property`-Parameter auch andere Vergleichsoperatoren wie „größer als“ (`>`) und „kleiner als“ (`<`) sowie reguläre Ausdrücke verwenden, um anhand von Eigenschaftswerten zu filtern. Es kann auch nach dem Vorhandensein oder Nichtvorhandensein einer Eigenschaft gefiltert werden, unabhängig von ihrem Wert.

Der `property`-Parameter akzeptiert nur Objekteigenschaften der obersten Ebene. Das bedeutet, dass Sie beim folgenden Beispielobjekt anhand der Eigenschaft für `name`, `description` und `subItem`, NICHT aber für `sampleKey` filtern können.

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
| `{OBJECT_TYPE}` | Der Typ von [!DNL Catalog] -Objekt, das abgerufen werden soll. Gültige Objekte sind: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
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

>[!NOTE]
>
> Die `name`-Eigenschaft unterstützt die Verwendung eines Platzhalters `*`, entweder als gesamte Suchzeichenfolge oder als Teil davon. Platzhalter entsprechen leeren Zeichen, sodass die Suchzeichenfolge `te*st` mit dem Wert „test“ übereinstimmt. Bei Sternchen muss durch Verdopplung (`**`) ein Escape durchgeführt werden. Ein doppeltes Sternchen in einer Suchzeichenfolge stellt ein einzelnes Sternchen als literale Zeichenfolge dar.

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
            "dule": {},
            "statsCache": {}
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
            "dule": {},
            "statsCache": {}
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
            "dule": {},
            "statsCache": {}
    }
}
```

## Mehrere Filter kombinieren

Mit einem kaufmännischen Und-Zeichen (`&`) können Sie mehrere Filter in einer Anfrage kombinieren. Wenn einer Anfrage zusätzliche Bedingungen hinzugefügt werden, wird eine UND-Beziehung angenommen.

**API-Format**

```http
GET /{OBJECT_TYPE}?{FILTER_1}={VALUE}&{FILTER_2}={VALUE}&{FILTER_3}={VALUE}
```
