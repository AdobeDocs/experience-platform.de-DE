---
title: API-Endpunkt für berechnete Attribute
description: Erfahren Sie, wie Sie berechnete Attribute mithilfe der Echtzeit-Kundenprofil-API erstellen, anzeigen, aktualisieren und löschen können.
exl-id: f217891c-574d-4a64-9d04-afc436cf16a9
source-git-commit: 49196473f304585193e87393f8dc5dc37be7e4d9
workflow-type: tm+mt
source-wordcount: '1664'
ht-degree: 10%

---

# API-Endpunkt für berechnete Attribute

>[!IMPORTANT]
>
>Der Zugriff auf die API ist eingeschränkt. Wenden Sie sich an den Adobe-Support, um zu erfahren, wie Sie Zugriff auf die API für berechnete Attribute erhalten.

Berechnete Attribute sind Funktionen, mit denen Daten auf Ereignisebene in Attribute auf Profilebene aggregiert werden. Diese Funktionen werden automatisch berechnet, sodass sie für die Segmentierung, Aktivierung und Personalisierung verwendet werden können. Dieses Handbuch enthält Beispiel-API-Aufrufe zum Ausführen grundlegender CRUD-Vorgänge mit dem `/attributes`-Endpunkt.

Um mehr über berechnete Attribute zu erfahren, lesen Sie zunächst den Abschnitt [Berechnete Attribute - Übersicht](overview.md).

## Erste Schritte

Der in diesem Handbuch verwendete API-Endpunkt ist Teil der [Echtzeit-Kundenprofil-API](https://www.adobe.com/go/profile-apis-en).

Bevor Sie fortfahren, lesen Sie das Handbuch [Erste Schritte mit der Profil-API](../api/getting-started.md) mit Links zur empfohlenen Dokumentation, einer Anleitung zum Lesen der Beispiel-API-Aufrufe, die in diesem Dokument angezeigt werden, und wichtigen Informationen zu erforderlichen Kopfzeilen, die für das erfolgreiche Aufrufen einer Experience Platform-API erforderlich sind.

Lesen Sie außerdem die Dokumentation für den folgenden Service:

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten von [!DNL Experience Platform] organisiert werden.
   - [Erste Schritte mit der Schemaregistrierung](../../xdm/api/getting-started.md#know-your-tenant_id): Informationen zu Ihrer `{TENANT_ID}`, die in den Antworten in diesem Handbuch enthalten sind, werden bereitgestellt.

## Abrufen einer Liste berechneter Attribute {#list}

Sie können eine Liste aller berechneten Attribute für Ihr Unternehmen abrufen, indem Sie eine GET-Anfrage an den `/attributes`-Endpunkt senden.

**API-Format**

Der `/attributes`-Endpunkt unterstützt verschiedene Abfrageparameter, mit denen Sie Ihre Ergebnisse filtern können. Obwohl diese Parameter optional sind, wird ihre Verwendung dringend empfohlen, um kostspieligen Aufwand bei der Auflistung von Ressourcen zu reduzieren. Wenn Sie diesen Endpunkt ohne Parameter aufrufen, werden alle für Ihre Organisation verfügbaren berechneten Attribute abgerufen. Es können mehrere Parameter eingeschlossen werden, die durch kaufmännische Und-Zeichen (`&`) voneinander getrennt werden.

```http
GET /attributes
GET /attributes?{QUERY_PARAMETERS}
```

Beim Abrufen einer Liste von berechneten Attributen können die folgenden Abfrageparameter verwendet werden:

| Abfrageparameter | Beschreibung | Beispiel |
| --------------- | ----------- | ------- |
| `limit` | Ein -Parameter, der die maximale Anzahl der als Teil der Antwort zurückgegebenen Elemente angibt. Der Mindestwert dieses Parameters ist 1 und der Höchstwert 40. Wenn dieser Parameter nicht enthalten ist, werden standardmäßig 20 Elemente zurückgegeben. | `limit=20` |
| `offset` | Ein -Parameter, der die Anzahl der Elemente angibt, die übersprungen werden sollen, bevor die Elemente zurückgegeben werden. | `offset=5` |
| `sortBy` | Ein -Parameter, der die Reihenfolge angibt, in der die zurückgegebenen Elemente sortiert werden. Zu den verfügbaren Optionen gehören `name`, `status`, `updateEpoch` und `createEpoch`. Sie können auch auswählen, ob in auf- oder absteigender Reihenfolge sortiert werden soll, indem Sie keine `-` vor der Sortieroption einfügen oder einfügen. Standardmäßig werden die Elemente nach `updateEpoch` in absteigender Reihenfolge sortiert. | `sortBy=name` |
| `property` | Ein Parameter, mit dem Sie nach verschiedenen berechneten Attributfeldern filtern können. Zu den unterstützten Eigenschaften gehören `name`, `createEpoch`, `mergeFunction.value`, `updateEpoch` und `status`. Die unterstützten Vorgänge hängen von der aufgelisteten Eigenschaft ab. <ul><li>`name`: `EQUAL` (=), `NOT_EQUAL` (!=), `CONTAINS` (=contains()), `NOT_CONTAINS` (=!contains())</li><li>`createEpoch`: `GREATER_THAN_OR_EQUALS` (&lt;=), `LESS_THAN_OR_EQUALS` (>=) </li><li>`mergeFunction.value`: `EQUAL` (=), `NOT_EQUAL` (!=), `CONTAINS` (=contains()), `NOT_CONTAINS` (=!contains())</li><li>`updateEpoch`: `GREATER_THAN_OR_EQUALS` (&lt;=), `LESS_THAN_OR_EQUALS` (>=)</li><li>`status`: `EQUAL` (=), `NOT_EQUAL` (!=), `CONTAINS` (=contains()), `NOT_CONTAINS` (=!contains())</li></ul> | `property=updateEpoch>=1683669114845`<br/>`property=name!=testingrelease`<br/>`property=status=contains(new,processing,disabled)` |

**Anfrage**

Die folgende Anfrage ruft die letzten drei berechneten Attribute ab, die in Ihrer Organisation aktualisiert wurden.

+++ Eine Beispielanfrage zum Abrufen einer Liste berechneter Attribute.

```shell
curl -X GET https://platform.adobe.io/data/core/ca/attributes?limit=3 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit einer Liste der letzten 3 aktualisierten berechneten Attribute zurückgegeben, die zu Ihrer Organisation und Sandbox gehören.

+++ Eine Beispielantwort zum Abrufen einer Liste berechneter Attribute.

```json
{
    "_links": {
        "last": {
            "href": "/attributes?offset=3&limit=1"
        },
        "next": {
            "href": "/attributes?offset=20&limit=20"
        },
        "prev": {
            "href": "/attributes?offset=0&limit=20"
        },
        "self": {
            "href": "/attributes?offset=0&limit=20"
        }
    },
    "computedAttributes": [
        {
            "id": "2e3bf98c-5840-4eb5-98c9-fcd7bde82188",
            "type": "ComputedAttribute",
            "name": "multipleFilterClauses19",
            "displayName": "Multiple Filter Clauses 19",
            "description": "Multiple Filter Clauses 19",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "e4f64b40-d8d9-11e9-a7ce-f3356ed0508b",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "path": "{TENANT_ID}/ComputedAttributes",
            "keepCurrent": false,
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0)",
            },
            "mergeFunction": {
                "value": "SUM"
            },
            "status": "DRAFT",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "duration": {
                "count": 7,
                "unit": "DAYS"
            },
            "lastEvaluationTs": "",
            "createEpoch": 1671223530322,
            "updateEpoch": 1673043640946,
            "createdBy": "{USER_ID}"
        },
        {
            "id": "d9fbbd3d-049a-4561-b826-adc162511950",
            "type": "ComputedAttribute",
            "name": "multipleFilterClauses20",
            "displayName": "Multiple Filter Clauses 20",
            "description": "Multiple Filter Clauses 20",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "e4f64b40-d8d9-11e9-a7ce-f3356ed0508b",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "path": "{TENANT_ID}/ComputedAttributes",
            "keepCurrent": true,
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "xEvent[eventType.equals(\"commerce.backofficeOrderPlaced\", false)].topN(timestamp, 1).map({\"timestamp\": timestamp, \"value\": producedBy}).head()"
            },
            "mergeFunction": {
                "value": "MOST_RECENT"
            },
            "status": "DRAFT",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "duration": {
                "count": 7,
                "unit": "DAYS"
            },
            "lastEvaluationTs": "",
            "createEpoch": 1671223586455,
            "updateEpoch": 1671223586455,
            "createdBy": "{USER_ID}"
        },
        {
            "id": "afedff07-9d15-4385-b181-49708229d73b",
            "type": "ComputedAttribute",
            "name": "multipleFilterClauses18",
            "displayName": "Multiple Filter Clauses 18",
            "description": "Multiple Filter Clauses 18",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "e4f64b40-d8d9-11e9-a7ce-f3356ed0508b",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "path": "{TENANT_ID}/ComputedAttributes",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0)",
            },
            "mergeFunction": {
                "value": "SUM"
            },
            "status": "PROCESSED",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "duration": {
                "count": 7,
                "unit": "DAYS"
            },
            "lastEvaluationTs": "2023-08-27T00:14:55.028",
            "createEpoch": 1671220358902,
            "updateEpoch": 1671220358902,
            "createdBy": "{USER_ID}"
        }
    ],
    "_page": {
        "offset": 0,
        "limit": 20,
        "count": 3,
        "totalCount": 3
    }
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `_links` | Ein Objekt, das die Paginierungsinformationen enthält, die für den Zugriff auf die letzte Ergebnisseite, die nächste Ergebnisseite, die vorherige Ergebnisseite oder die aktuelle Ergebnisseite erforderlich sind. |
| `computedAttributes` | Ein Array, das die auf der Grundlage Ihrer Abfrageparameter berechneten Attribute enthält. Weitere Informationen zum Array der berechneten Attribute finden Sie im Abschnitt [Abrufen eines bestimmten berechneten Attributs](#get). |
| `_page` | Ein -Objekt, das Metadaten zu den zurückgegebenen Ergebnissen enthält. Dazu gehören Informationen über den aktuellen Offset, die Anzahl der zurückgegebenen berechneten Attribute, die Gesamtzahl der berechneten Attribute sowie die Beschränkung der zurückgegebenen berechneten Attribute. |

+++

## Berechnetes Attribut erstellen {#create}

Um ein berechnetes Attribut zu erstellen, stellen Sie zunächst eine POST-Anfrage an den `/attributes`-Endpunkt mit einem Anfragetext, der die Details des berechneten Attributs enthält, das Sie erstellen möchten.

**API-Format**

```http
POST /attributes
```

**Anfrage**

+++ Beispielanfrage zum Erstellen eines neuen berechneten Attributs.

```shell
curl -X POST https://platform.adobe.io/data/core/ca/attributes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}'\
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "testing",
        "displayName": "Sample Display Name",
        "description": "Sample Description",
        "expression": {
            "type": "PQL", 
            "format": "pql/text", 
            "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0)].sum(commerce.order.priceTotal)"
        },
        "keepCurrent": false,
        "duration": {
            "count": 4,
            "unit": "DAYS"
        },
        "status": "DRAFT"
      }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `name` | Der Name des berechneten Feldnamenfelds als Zeichenfolge. Der Name des berechneten Attributs darf nur aus alphanumerischen Zeichen ohne Leerzeichen oder Unterstriche bestehen. Dieser Wert **muss** unter allen berechneten Attributen eindeutig sein. Als Best Practice sollte dieser Name eine CamelCase-Version des `displayName` sein. |
| `description` | Eine Beschreibung des berechneten Attributs. Dies ist besonders nützlich, wenn mehrere berechnete Attribute definiert wurden, da es anderen in Ihrer Organisation helfen kann, das richtige zu verwendende berechnete Attribut zu ermitteln. |
| `displayName` | Der Anzeigename für das berechnete Attribut. Dies ist der Name, der angezeigt wird, wenn Ihre berechneten Attribute in der Adobe Experience Platform-Benutzeroberfläche aufgelistet werden. |
| `expression` | Ein -Objekt, das den Abfrageausdruck des berechneten Attributs darstellt, das Sie erstellen möchten. |
| `expression.type` | Der Typ des Ausdrucks. Derzeit wird nur PQL unterstützt. |
| `expression.format` | Das Format des Ausdrucks. Derzeit wird nur `pql/text` unterstützt. |
| `expression.value` | Der Wert des Ausdrucks. |
| `keepCurrent` | Ein boolescher Wert, der darüber bestimmt, ob der Wert des berechneten Attributs durch schnelle Aktualisierung auf dem neuesten Stand gehalten wird oder nicht. Derzeit sollte dieser Wert auf `false` gesetzt werden. |
| `duration` | Ein -Objekt, das den Lookback-Zeitraum für das berechnete Attribut darstellt. Der Lookback-Zeitraum gibt an, wie weit das berechnete Attribut zurückgeschaut werden kann. |
| `duration.count` | Eine Zahl, die die Dauer für den Lookback-Zeitraum darstellt. Die möglichen Werte hängen vom Wert des `duration.unit` ab. <ul><li>`HOURS`: 1-24</li><li>`DAYS`: 1-7</li><li>`WEEKS`: 1-4</li><li>`MONTHS`: 1-6</li></ul> |
| `duration.unit` | Eine Zeichenfolge, die die Zeiteinheit darstellt, die für den Lookback-Zeitraum verwendet wird. Mögliche Werte sind: `HOURS`, `DAYS`, `WEEKS` und `MONTHS`. |
| `status` | Der Status des berechneten Attributs. Mögliche Werte sind `DRAFT` und `NEW`. |

+++

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit Informationen zu Ihrem neu erstellten berechneten Attribut zurückgegeben.

+++ Beispielantwort beim Erstellen eines neuen berechneten Attributs.

```json
{
    "id": "1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631",
    "type": "ComputedAttribute",
    "name": "testing",
    "displayName": "Sample Display Name",
    "description": "Sample Description",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "02dd69f0-da73-11e9-9ea1-af59ce7c24e8",
        "sandboxName": "prod",
        "type": "production",
        "isDefault": true
    },
    "path": "{TENANT_ID}/ComputedAttributes",
    "keepCurrent": false,
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0)].sum(commerce.order.priceTotal)"
    },
    "mergeFunction": {
        "value": "SUM"
    },
    "status": "DRAFT",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "lastEvaluationTs": "",
    "createEpoch": 1680070188696,
    "updateEpoch": 1680070188696,
    "createdBy": "{USER_ID}"
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `id` | Die systemgenerierte ID Ihres neu erstellten berechneten Attributs. |
| `status` | Der Status des berechneten Attributs. Dies kann entweder `DRAFT` oder `NEW` sein. |
| `createEpoch` | Der Zeitpunkt, zu dem das berechnete Attribut erstellt wurde, in Sekunden. |
| `updateEpoch` | Der Zeitpunkt, zu dem das berechnete Attribut zuletzt aktualisiert wurde, in Sekunden. |
| `createdBy` | Die ID des Benutzers, der das berechnete Attribut erstellt hat. |

+++

## Abrufen eines bestimmten berechneten Attributs {#get}

Sie können detaillierte Informationen zu einem bestimmten berechneten Attribut abrufen, indem Sie eine GET-Anfrage an den `/attributes`-Endpunkt senden und im Anfragepfad die ID des berechneten Attributs angeben, das Sie abrufen möchten.

**API-Format**

```http
GET /attributes/{ATTRIBUTE_ID}
```

**Anfrage**

+++ Eine Beispielanfrage zum Abrufen eines bestimmten berechneten Attributs.

```shell
curl -X GET 'https://platform.adobe.io/data/core/ca/attributes/1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status-Code 200 mit detaillierten Informationen zum angegebenen berechneten Attribut zurück.

+++ Eine Beispielantwort beim Abrufen eines bestimmten berechneten Attributs.

```json
{
    "id": "1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631",
    "type": "ComputedAttribute",
    "name": "testing",
    "displayName": "Sample Display Name",
    "description": "Sample Description",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "02dd69f0-da73-11e9-9ea1-af59ce7c24e8",
        "sandboxName": "prod",
        "type": "production",
        "isDefault": true
    },
    "path": "{TENANT_ID}/ComputedAttributes",
    "keepCurrent": false,
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0) and (timestamp occurs <= 7 days before now)].sum(commerce.order.priceTotal)"
    },
    "mergeFunction": {
        "value": "SUM"
    },
    "status": "DRAFT",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "lastEvaluationTs": "",
    "createEpoch": 1680070188696,
    "updateEpoch": 1680070188696,
    "createdBy": "{USER_ID}"
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `id` | Eine eindeutige, schreibgeschützte, systemgenerierte ID, die bei anderen API-Vorgängen zum Verweisen auf das berechnete Attribut genutzt werden kann. |
| `type` | Eine Zeichenfolge, die anzeigt, dass das zurückgegebene -Objekt ein berechnetes Attribut ist. |
| `name` | Der Name für das berechnete Attribut. |
| `displayName` | Der Anzeigename für das berechnete Attribut. Dies ist der Name, der angezeigt wird, wenn Ihre berechneten Attribute in der Adobe Experience Platform-Benutzeroberfläche aufgelistet werden. |
| `description` | Eine Beschreibung des berechneten Attributs. Dies ist besonders nützlich, wenn mehrere berechnete Attribute definiert wurden, da es anderen in Ihrer Organisation helfen kann, das richtige zu verwendende berechnete Attribut zu ermitteln. |
| `imsOrgId` | Die ID der Organisation, zu der das berechnete Attribut gehört. |
| `sandbox` | Das Sandbox-Objekt enthält Details zur Sandbox, in der das berechnete Attribut konfiguriert wurde. Diese Daten werden aus der in der Anfrage gesendeten Sandbox-Kopfzeile extrahiert. Weiterführende Informationen dazu finden Sie in der [Sandbox-Übersicht](../../sandboxes/home.md). |
| `path` | Die `path` zum berechneten Attribut. |
| `keepCurrent` | Ein boolescher Wert, der darüber bestimmt, ob der Wert des berechneten Attributs durch schnelle Aktualisierung auf dem neuesten Stand gehalten wird oder nicht. |
| `expression` | Ein -Objekt, das den Ausdruck des berechneten Attributs enthält. |
| `mergeFunction` | Ein Objekt, das die Zusammenführungsfunktion für das berechnete Attribut enthält. Dieser Wert basiert auf dem entsprechenden Aggregationsparameter im Ausdruck des berechneten Attributs. Zu den möglichen Werten gehören `SUM`, `MIN`, `MAX` und `MOST_RECENT`. |
| `status` | Der Status des berechneten Attributs. Dies kann einer der folgenden Werte sein: `DRAFT`, `NEW`, `INITIALIZING`, `PROCESSING`, `PROCESSED`, `FAILED` oder `DISABLED`. |
| `schema` | Ein Objekt, das Informationen zum Schema enthält, in dem der Ausdruck ausgewertet wird. Derzeit wird nur `_xdm.context.profile` unterstützt. |
| `lastEvaluationTs` | Ein Zeitstempel, der angibt, wann das berechnete Attribut zuletzt ausgewertet wurde. |
| `createEpoch` | Der Zeitpunkt, zu dem das berechnete Attribut erstellt wurde, in Sekunden. |
| `updateEpoch` | Der Zeitpunkt, zu dem das berechnete Attribut zuletzt aktualisiert wurde, in Sekunden. |
| `createdBy` | Die ID des Benutzers, der das berechnete Attribut erstellt hat. |

+++

## Bestimmtes berechnetes Attribut löschen {#delete}

Sie können ein bestimmtes berechnetes DELETE löschen, indem Sie eine Attributanfrage an den `/attributes`-Endpunkt stellen und im Anfragepfad die Kennung des berechneten Attributs angeben, das Sie löschen möchten.

>[!IMPORTANT]
>
>Die Löschanfrage kann nur zum Löschen berechneter Attribute mit dem Status **Entwurf)**`DRAFT`) verwendet werden. Dieser Endpunkt **kann** nicht verwendet werden, um berechnete Attribute in einem anderen Status zu löschen.

**API-Format**

```http
DELETE /attributes/{ATTRIBUTE_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{ATTRIBUTE_ID}` | Der `id` des berechneten Attributs, das Sie löschen möchten. |

**Anfrage**

+++ Eine Beispielanfrage zum Löschen eines berechneten Attributs.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ca/attributes/1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 202 mit Details zum gelöschten berechneten Attribut zurückgegeben.

+++ Eine Beispielantwort beim Löschen eines berechneten Attributs.

```json
{
    "id": "03ae581b-5f7b-48da-a9eb-4ef0daf4bc3c",
    "type": "ComputedAttribute",
    "name": "testdemopd2",
    "displayName": "testdemopd2",
    "description": "testdemopd2",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "02dd69f0-da73-11e9-9ea1-af59ce7c24e8",
        "sandboxName": "prod",
        "type": "production",
        "isDefault": true
    },
    "path": "{TENANT_ID}/ComputedAttributes",
    "keepCurrent": false,
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.shipping.shipDate occurs <= 1 days before now) and (timestamp occurs <= 1 days before now)].min(commerce.shipping.shipDate)"
    },
    "mergeFunction": {
        "value": "MIN"
    },
    "status": "DRAFT",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "lastEvaluationTs": "",
    "createEpoch": 1681365690928,
    "updateEpoch": 1681365690928,
    "createdBy": "{USER_ID}"
}
```

+++

## Spezifisches berechnetes Attribut aktualisieren

Sie können ein bestimmtes berechnetes Attribut aktualisieren, indem Sie eine PATCH-Anfrage an den `/attributes`-Endpunkt senden und im Anfragepfad die ID des berechneten Attributs angeben, das Sie aktualisieren möchten.

>[!IMPORTANT]
>
>Beim Aktualisieren eines berechneten Attributs können nur die folgenden Felder aktualisiert werden:
>
>- Wenn der aktuelle Status `NEW` ist, kann der Status nur in `DISABLED` geändert werden.
>- Wenn der aktuelle Status `DRAFT` ist, können Sie die Werte der folgenden Felder ändern: `name`, `description`, `keepCurrent`, `expression` und `duration`. Sie können auch den Status von `DRAFT` in `NEW` ändern. Alle Änderungen an systemgenerierten Feldern wie `mergeFunction` oder `path` geben einen Fehler zurück.
>- Wenn der aktuelle Status entweder `PROCESSING` oder `PROCESSED` ist, kann der Status nur in `DISABLED` geändert werden.

**API-Format**

```http
PATCH /attributes/{ATTRIBUTE_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{ATTRIBUTE_ID}` | Der `id` des berechneten Attributs, das Sie aktualisieren möchten. |

**Anfrage**

Die folgende Anfrage aktualisiert den Status des berechneten Attributs von `DRAFT` auf `NEW`.

+++ Eine Beispielanfrage zum Aktualisieren eines berechneten Attributs.

```shell
curl -X PATCH https://platform.adobe.io/data/core/ca/attributes/1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
 {
    "description": "Sample Description",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0) and (timestamp occurs <= 7 days before now)].sum(commerce.order.priceTotal)"
    },
    "status": "NEW"
 }'
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status-Code 200 mit Informationen zu Ihrem neu aktualisierten berechneten Attribut zurück.

+++ Eine Beispielantwort beim Aktualisieren eines berechneten Attributs.

```json
{
    "id": "1e8d0d77-b2bb-4b17-bbe6-2dbc08c1a631",
    "type": "ComputedAttribute",
    "name": "testing123",
    "displayName": "Sample Display Name",
    "description": "Sample Description",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "02dd69f0-da73-11e9-9ea1-af59ce7c24e8",
        "sandboxName": "prod",
        "type": "production",
        "isDefault": true
    },
    "path": "{TENANT_ID}/ComputedAttributes",
    "keepCurrent": false,
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "xEvent[(commerce.checkouts.value > 0.0 or commerce.purchases.value > 1.0 or commerce.order.priceTotal >= 10.0) and (timestamp occurs <= 7 days before now)].sum(commerce.order.priceTotal)"
    },
    "mergeFunction": {
        "value": "SUM"
    },
    "status": "NEW",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "lastEvaluationTs": "",
    "createEpoch": 1680071726825,
    "updateEpoch": 1680074429192,
    "createdBy": "{USER_ID}"
}
```

+++

## Nächste Schritte

Nachdem Sie nun die Grundlagen von berechneten Attributen gelernt haben, können Sie damit beginnen, sie für Ihr Unternehmen zu definieren. Informationen zur Verwendung berechneter Attribute in der Experience Platform-Benutzeroberfläche finden Sie im [Handbuch zur Benutzeroberfläche für berechnete Attribute](./ui.md).
