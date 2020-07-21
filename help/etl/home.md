---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen von ETL-Integrationen
topic: overview
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '4102'
ht-degree: 80%

---


# Entwickeln von ETL-Integrationen für Adobe Experience Platform

The ETL integration guide outlines general steps for creating high-performance, secure connectors for [!DNL Experience Platform] and ingesting data into [!DNL Platform].


- [!DNL Catalog](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)
- [!DNL Data Access](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml)
- [!DNL Data Ingestion](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)
- [APIs für Authentifizierung und Autorisierung](../tutorials/authentication.md)
- [!DNL Schema Registry](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)

This guide also includes sample API calls to use when designing an ETL connector, with links to documentation that outlines each [!DNL Experience Platform] service, and use of its API, in more detail.

A sample integration is available on [!DNL GitHub] via the [ETL Ecosystem Integration Reference Code](https://github.com/adobe/acp-data-services-etl-reference) under the [!DNL Apache] License Version 2.0.

## Workflow

Das folgende Diagramm skizziert den allgemeinen Workflow für die Integration der Komponenten von Adobe Experience Platform mit einer ETL-Anwendung und einem ETL-Connector.

![](images/etl.png)

## Komponenten von Adobe Experience Platform

An der Integration mit ETL-Connectoren ist eine Vielzahl der Komponenten von Experience Platform beteiligt. Die folgende Liste zeigt einige der zentralen Komponenten und ihre Funktionalitäten:

- **Adobe Identity Management System (IMS)**: Bietet ein Framework für die Authentifizierung bei Adobe-Services.
- **IMS-Organisation**: Eine Unternehmens-Entität, die Produkte und Services besitzen oder lizenzieren und Zugriff auf ihre Mitglieder gewähren kann.
- **IMS-Anwender**: Die Mitglieder einer IMS-Organisation. Organisation und Anwender stehen in einer m:n-Beziehung zueinander.
- **[!DNL Sandbox]** - Eine virtuelle Partition eine einzelne [!DNL Platform] Instanz, um die Entwicklung und Entwicklung digitaler Erlebnisanwendungen zu unterstützen.
- **Datenerkennung**: Erfasst die Metadaten von aufgenommenen und umgewandelten Daten in [!DNL Experience Platform].
- **[!DNL Data Access]** - Bietet Benutzern eine Oberfläche zum Zugriff auf ihre Daten in [!DNL Experience Platform].
- **[!DNL Data Ingestion]** - Überträgt Daten [!DNL Experience Platform] mit [!DNL Data Ingestion] APIs.
- **[!DNL Schema Registry]** - Definiert und speichert Schema, das die Struktur der zu verwendenden Daten beschreibt [!DNL Experience Platform].

## Getting started with [!DNL Experience Platform] APIs

The following sections provide additional information that you will need to know or have on-hand in order to successfully make calls to [!DNL Experience Platform] APIs.

### Lesehilfe für Beispiel-API-Aufrufe

In diesem Handbuch wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dabei wird auf Pfade ebenso eingegangen wie auf die erforderlichen Kopfzeilen und die für Anfrage-Payloads zu verwendende Formatierung. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Die in der Dokumentation zu Beispielen für API-Aufrufe verwendeten Konventionen werden im Handbuch zur Fehlerbehebung für unter [Lesehilfe für Beispiel-API-Aufrufe](../landing/troubleshooting.md#how-do-i-format-an-api-request) erläutert.[!DNL Experience Platform]

### Werte der zu verwendenden Kopfzeilen

In order to make calls to [!DNL Platform] APIs, you must first complete the [authentication tutorial](../tutorials/authentication.md). Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../sandboxes/home.md).

Alle Anfragen, die eine Payload enthalten (also POST-, PUT- und PATCH-Anfragen), erfordern eine zusätzliche Kopfzeile:

- Content-Type: application/json

## Allgemeiner Ablauf

To begin, an ETL user logs into the [!DNL Experience Platform] user interface (UI) and creates datasets for ingestion using a standard connector or push-service connector.

In der Benutzeroberfläche erstellt der Anwender den Ausgabedatensatz, indem er ein Datensatzschema auswählt. The choice of schema depends on the type of data (record or time series) being ingested into [!DNL Platform]. In der Benutzeroberfläche können alle verfügbaren Schemas einschließlich des vom Schema unterstützten Verhaltenstyps über die Registerkarte „Schemas“ eingesehen werden.

Beginnt der Anwender im ETL-Tool mit der Konzeptionierung, wird seine Zuordnung nach Konfiguration der entsprechenden Verbindung (unter Verwendung seiner Anmeldeinformationen) umgewandelt. The ETL tool is assumed to already have [!DNL Experience Platform] connectors installed (process not defined in this Integration Guide).

Modelldarstellungen eines Beispiel-ETL-Tools und -Workflows stehen unter [ETL-Workflow](./workflow.md) zur Verfügung. Die einzelnen ETL-Tools unterscheiden sich zwar in ihrem Format, sind sich in ihrer Funktion aber größtenteils ähnlich.

>[!NOTE]
>
> Der ETL-Connector muss einen Filter für den Zeitstempel definieren, der das Datum zur Aufnahme von Daten und Offset (d. h. das Fenster, für das Daten gelesen werden sollen) kennzeichnet. Das ETL-Tool sollte die Aufnahme dieser beiden Parameter in dieser oder einer anderen relevanten Benutzeroberfläche unterstützen. In Adobe Experience Platform werden diese Parameter entweder Informationen zum Verfügbarkeitsdatum (sofern vorhanden) oder zum Erfassungsdatum im Batch-Objekt des Datensatzes zugeordnet.

### Anzeigen einer Liste von Datensätzen

Using the source of data for mapping, a list of all available datasets can be fetched using the [!DNL Catalog API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml).

Sie können zur Auflistung aller verfügbaren Datensätze eine einzelne API-Anfrage (z. B. `GET /dataSets`) ausführen. Dabei empfiehlt sich als Best Practice die Angabe von Abfrageparametern, durch die die Größe der Antwort beschränkt wird.

Werden _vollständige_ Datensatzinformationen angefragt, wächst die Größe der Antwort-Payload unter Umständen auf mehr als 3 GB an, was zu einer insgesamt verlangsamten Leistung führen kann. Therefore, using query parameters to filter only the information needed will make [!DNL Catalog] queries more efficient.

#### Filtern von Listen

Sie können mehrere Filter für die Antwortausgabe verwenden, indem sie die entsprechenden Parameter durch ein kaufmännisches Und-Zeichen (`&`) voneinander trennen. Einige Abfrageparameter akzeptieren eine durch Komma getrennte Liste von Werten, darunter etwa der für die Eigenschaften verwendete „properties“-Filter in der unten dargestellten Beispielanfrage.

[!DNL Catalog] Antworten werden automatisch entsprechend den konfigurierten Einschränkungen gezählt. Der Parameter &quot;Limit&quot;-Abfrage kann jedoch verwendet werden, um die Einschränkungen anzupassen und die Anzahl der zurückgegebenen Objekte zu begrenzen. The pre-configured [!DNL Catalog] response limits are:

- Wenn kein Limit-Parameter angegeben wird, beträgt die maximale Anzahl von Objekten pro Antwort-Payload 20.
- The global limit for all other [!DNL Catalog] queries is 100 objects.
- Bei Datensatzabfragen „observableSchema“ unter Angabe des „properties“-Abfrageparameters beträgt die maximale Anzahl der zurückgegebenen Datensätze 20.
- Bei Angabe ungültiger Parameter für die Begrenzung (einschließlich `limit=0`) wird ein HTTP-Fehler mit dem Statuscode 400 zurückgegeben, in dem die korrekten Bereiche angezeigt werden.
- Als Abfrageparameter angegebene Begrenzungen oder Offsets haben Vorrang vor den angegebenen Kopfzeilen.

Einzelheiten zu Abfrageparametern finden Sie unter [Übersicht über Catalog Service](../catalog/home.md).

**API-Format**

```http
GET /catalog/dataSets
GET /catalog/dataSets?{filter1}={value1},{value2}&{filter2}={value3}
```

**Anfrage**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets?limit=3&properties=name,description,schemaRef" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

Please refer to the [Catalog Service overview](../catalog/home.md) for detailed examples of how to make calls to the [!DNL Catalog API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml).

**Antwort**

Die Antwort umfasst drei (`limit=3`) Datensätze, die dem Abfrageparameter `properties` entsprechend die Objekte „name“, „description“ und „schemaRef“, also Name, Beschreibung und Schema-Verweis, umfassen.

```json
{
    "5b95b155419ec801e6eee780": {
        "name": "Store Transactions",
        "description": "Retails Store Transactions",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    },
    "5c351fa2f5fee300000fa9e8": {
        "name": "Loyalty Members",
        "description": "Loyalty Program Members",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    },
    "5c1823b19e6f400000993885": {
        "name": "Web Traffic",
        "description": "Retail Web Traffic",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/2025a705890c6d4a4a06b16f8cf6f4ca",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    }
}
```

### Anzeigen des Datensatzschemas

Die Eigenschaft „schemaRef“ eines Datensatzes enthält einen URI, der auf das XDM-Schema verweist, auf dem der Datensatz basiert. Das XDM-Schema („schemaRef“) umfasst alle vom Datensatz _potenziell_ verwendbaren Felder, also nicht zwingend nur die, die _tatsächlich_ verwendet werden (siehe „observableSchema“ weiter unten).

Das XDM-Schema ist das Schema, das Sie verwenden, wenn Sie dem Anwender eine Liste aller verfügbaren Felder anzeigen möchten, die ausgefüllt werden können.

The first &quot;schemaRef.id&quot; value in the previous response object (`https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18`) is a URI that points to a specific XDM schema in the [!DNL Schema Registry]. The schema can be retrieved by making a lookup (GET) request to the [!DNL Schema Registry] API.

>[!NOTE]
>
> Die Eigenschaft „schema“ ist veraltet und wurde ersetzt durch die Eigenschaft „schemaRef“. Fehlt „schemaRef“ im Datensatz oder enthält keinen Wert, müssen Sie prüfen, ob eine „schema“-Eigenschaft vorhanden ist. Ersetzen Sie dazu im Abfrageparameter `properties` des vorherigen Aufrufs „schemaRef“ durch „Schema“. Näheres zur Eigenschaft „Schema“ finden Sie im nachfolgenden Abschnitt [Eigenschaft „Schema“ des Datensatzes](#dataset-schema-property-deprecated---eol-2019-05-30).

**API-Format**

```http
GET /schemaregistry/tenant/schemas/{url encoded schemaRef.id}
```

**Anfrage**

Die Anfrage erfolgt über den URL-codierten `id`-URI des Schemas (der Wert des Attributs „schemaRef.id“) und erfordert eine Accept-Kopfzeile.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F274f17bc5807ff307a046bab1489fb18 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
```

Das Format der Antwort hängt von der in der Anfrage verwendeten Accept-Kopfzeile ab. In Anfragen zum Nachschlagen muss außerdem die `version` in der Accept-Kopfzeile angegeben werden. In der folgenden Tabelle sind die für Anfragen zum Nachschalgen verfügbaren Accept-Kopfzeilen aufgeführt:

| Accept | Beschreibung |
| ------ | ----------- |
| `application/vnd.adobe.xed-id+json` | Auflisten (GET) von Anfragen, Titeln, IDs und Versionen |
| `application/vnd.adobe.xed-full+json; version={major version}` | $refs und allOf aufgelöst, einschließlich Titeln und Beschreibungen |
| `application/vnd.adobe.xed+json; version={major version}` | Rohdaten mit $ref und allOf, einschließlich Titeln und Beschreibungen |
| `application/vnd.adobe.xed-notext+json; version={major version}` | Rohdaten mit $ref und allOf, ohne Titel und Beschreibungen |
| `application/vnd.adobe.xed-full-notext+json; version={major version}` | $refs und allOf aufgelöst, ohne Titel und Beschreibungen |
| `application/vnd.adobe.xed-full-desc+json; version={major version}` | $refs und allOf aufgelöst, beinhaltet Deskriptoren |

>[!NOTE]
>
>`application/vnd.adobe.xed-id+json` Die Accept-Kopfzeilen  und `application/vnd.adobe.xed-full+json; version={major version}` werden am häufigsten verwendet. `application/vnd.adobe.xed-id+json`[!DNL Schema Registry] wird empfohlen, wenn eine Liste der in der enthaltenen Ressourcen angezeigt werden soll, da über sie nur Titel, ID und Version zurückgegeben werden. `application/vnd.adobe.xed-full+json; version={major version}` wird empfohlen, wenn nur eine einzelne Ressource (über ihre „id“) angezeigt werden soll, da über sie alle (unter „properties“ verschachtelten) Felder sowie Titel und Beschreibungen zurückgegeben werden.

**Antwort**

Das zurückgegebene JSON-Schema beschreibt die Struktur sowie Feldebenen-Informationen wie Typ, Format, Minimum, Maximum usw. der Daten, dies serialisiert als JSON. Für den Fall, dass für die Datenaufnahme ein anderes Serialisierungsformat als JSON verwendet wird (z. B. Parquet oder Scala), steht im [Handbuch zur Schema Registry](../xdm/tutorials/create-schema-api.md) eine Tabelle mit dem gewünschten JSON-Typ („meta:xdmType“) und der entsprechenden Darstellung in anderen Formaten zur Verfügung.

Along with this table, the [!DNL Schema Registry] Developer Guide contains in-depth examples of all possible calls that can be made using the [!DNL Schema Registry] API.

### Eigenschaft „Schema“ des Datensatzes (VERALTET, EINGESTELLT AM 30.05.2019)

Datensätze enthalten unter Umständen die Eigenschaft „schema“, die inzwischen eingestellt wurde und nur vorübergehend zum Zwecke der Abwärtskompatibilität verfügbar bleibt. So würde eine Anfrage zum Auflisten (GET) wie die zuvor ausgeführte, bei der im Abfrageparameter `properties` „schema“ durch „schemaRef“ ersetzt wurde, etwa Folgendes zurückgeben:

```json
{
  "5ba9452f7de80400007fc52a": {
    "name": "Sample Dataset 1",
    "description": "Description of Sample Dataset 1.",
    "schema": "@/xdms/context/person"
  }
}
```

If the &quot;schema&quot; property of a dataset is populated, this signals that the schema is a deprecated `/xdms` schema and, where supported, the ETL connector should use the value in the &quot;schema&quot; property with the `/xdms` endpoint (a deprecated endpoint in the [!DNL Catalog API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)) to retrieve the legacy schema.

**API-Format**

```http
GET /catalog/{"schema" property without the "@"}
```

**Anfrage**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/xdms/context/person?expansion=xdm" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

>[!NOTE]
>
>Der optionale Abfrageparameter `expansion=xdm` weist die API an, alle referenzierten Schemas vollständig zu erweitern und einzubinden. Dies empfiehlt sich, wenn Sie eine Liste aller potenziellen Felder anzeigen möchten.

**Antwort**

Ähnlich den Schritten zum [Anzeigen des Datensatzschemas](#view-dataset-schema), liefert auch diese Antwort ein JSON-Schema, das, ebenfalls als JSON serialisiert, die Struktur und die Feldebenen-Informationen der Daten beschreibt.

>[!NOTE]
>
>Wenn das Feld „schema“ leer oder überhaupt nicht vorhanden ist, sollte der Connector das Feld „schemaRef“ lesen und die [Schema Registry API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) verwenden, wie in den vorherigen Schritten zum [Anzeigen eines Datensatzschemas](#view-dataset-schema) ausgeführt.

### Die Eigenschaft „observableSchema“

Die Eigenschaft „observableSchema“ eines Datensatzes weist eine JSON-Struktur auf, die mit der JSON-Struktur des XDM-Schemas übereinstimmt. Das „observableSchema“ enthält die in den eingehenden Eingabedateien vorhandenen Felder. When writing data to [!DNL Experience Platform], a user is not required to use every field from the target schema. Tatsächlich sollten sie nur diejenigen Felder bereitstellen, die tatsächlich verwendetet werden.

Das beobachtbare Schema ist das Schema, das Sie verwenden würden, wenn Sie die Daten lesen oder eine Liste von zum Lesen/Zuordnen verfügbaren Feldern präsentieren.

```json
{
    "598d6e81b2745f000015edcb": {
        "observableSchema": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "name": {
                    "type": "string",
                },
                "age": {
                    "type": "string",
                }
            }
        }
    }
}
```

### Vorschau der Daten

Die ETL-Anwendung kann eine Funktion zur Vorschau von Daten bereitstellen (siehe [Abbildung 8 im ETL-Workflow](./workflow.md)). Die Data Access API bietet verschiedene Optionen für die Vorschau von Daten.

Weiterführende Informationen, einschließlich einer Schritt-für-Schritt-Anleitung für die Vorschau von Daten mithilfe der Data Access API, finden Sie im [Tutorial zum Datenzugriff](../data-access/tutorials/dataset-data.md).

### Abrufen von Details zum Datensatz mithilfe des Abfrageparameters „properties“

Wie weiter oben in den Schritten zur [Ansicht einer Liste von Datensätzen](#view-list-of-datasets) dargestellt, können Sie „files“, also Dateien, über den Abfrageparameter „properties“ abrufen.

Einzelheiten zur Abfrage von Datensätzen und den verfügbaren Antwortfiltern finden Sie in unter [Übersicht über den Katalog-Service](../catalog/home.md).

**API-Format**

```http
GET /catalog/dataSets?limit={value}&properties={value}
```

**Anfrage**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets?limit=1&properties=files" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

**Antwort**

Die Antwort umfasst einen Datensatz (`limit=1`), der die Eigenschaft „files“ anzeigt.

```json
{
  "5bf479a6a8c862000050e3c7": {
    "files": "@/dataSets/5bf479a6a8c862000050e3c7/views/5bf479a654f52014cfffe7f1/files"
  }
}
```

### Anzeigen einer Liste von Datensatzdateien mithilfe des Attributs „files“

Sie können Dateien auch mittels GET-Anfrage unter Verwendung des Attributs „files“ abrufen.

**API-Format**

```http
GET /catalog/dataSets/{DATASET_ID}/views/{VIEW_ID}/files
```

**Anfrage**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets/5bf479a6a8c862000050e3c7/views/5bf479a654f52014cfffe7f1/files" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

**Antwort**

Die Antwort enthält die Datensatzdatei-ID als übergeordnete Eigenschaft, wobei die Dateidetails im ID-Objekt der Datensatzdatei enthalten sind.

```json
{
    "194e89b976494c9c8113b968c27c1472-1": {
        "batchId": "194e89b976494c9c8113b968c27c1472",
        "dataSetViewId": "5bf479a654f52014cfffe7f1",
        "imsOrg": "{IMS_ORG}",
        "availableDates": {},
        "createdUser": "{USER_ID}",
        "createdClient": "{API_KEY}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1542749145828,
        "updated": 1542749145828
    },
    "14d5758c107443e1a83c714e56ca79d0-1": {
        "batchId": "14d5758c107443e1a83c714e56ca79d0",
        "dataSetViewId": "5bf479a654f52014cfffe7f1",
        "imsOrg": "{IMS_ORG}",
        "availableDates": {},
        "createdUser": "{USER_ID}",
        "createdClient": "{API_KEY}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1542752699111,
        "updated": 1542752699111
    },
    "ea40946ac03140ec8ac4f25da360620a-1": {
        "batchId": "ea40946ac03140ec8ac4f25da360620a",
        "dataSetViewId": "5bf479a654f52014cfffe7f1",
        "imsOrg": "{IMS_ORG}",
        "availableDates": {},
        "createdUser": "{USER_ID}",
        "createdClient": "{API_KEY}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1542756935535,
        "updated": 1542756935535
    }
}
```

### Abrufen von Dateidetails

The dataset file IDs returned in the previous response can be used in a GET request to fetch further file details via the [!DNL Data Access] API.

Einzelheiten zur Arbeit mit der API finden Sie unter [Übersicht über den Datenzugriff](../data-access/home.md).[!DNL Data Access]

**API-Format**

```http
GET /export/files/{DATASET_FILE_ID}
```

**Anfrage**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

**Antwort**

```json
[
    {
    "name": "{FILE_NAME}.parquet",
    "length": 2576,
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1?path=samplefile.parquet"
            }
        }
    }
]
```

### Vorschau von Dateidaten

The &quot;href&quot; property can be used to fetch preview data via the [!DNL Data Access API](../data-access/home.md).

**API-Format**

```http
GET /export/files/{FILE_ID}?path={FILE_NAME}.{FILE_FORMAT}
```

**Anfrage**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1?path=samplefile.parquet" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

Die Antwort auf die obige Anfrage enthält eine Vorschau des Dateiinhalts.

More information on the [!DNL Data Access] API, including detailed requests and responses, is available in the [data access overview](../data-access/home.md).

### Abrufen von „fileDescription“ aus dem Datensatz

Dies ist die Zielkomponente als Ausgabe der umgewandelten Daten, für die der Data Engineer einen Ausgabedatensatz auswählt (siehe [Abbildung 12 im ETL-Workflow](workflow.md)). Das XDM-Schema ist dem Ausgabedatensatz zugeordnet. Die zu schreibenden Daten werden durch das Attribut „fileDescription“, also Dateibeschreibung, der Datensatz-Entität aus den Datenerkennungs-APIs gekennzeichnet. Diese Informationen können über eine Datensatz-ID abgerufen werden (`{DATASET_ID}`). Die Eigenschaft „fileDescription“ in der JSON-Antwort liefert die angefragten Informationen.

**API-Format**

```shell
GET /catalog/dataSets/{DATASET_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{DATASET_ID}` | Der `id`-Wert des Datensatzes, auf den Sie zugreifen möchten. |

**Anfrage**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets/59c93f3da7d0c00000798f68" \
-H "accept: application/json" \
-H "x-gw-ims-org-id: {IMS_ORG}" \
-H "x-sandbox-name: {SANDBOX_NAME}" \
-H "Authorization: Bearer {ACCESS_TOKEN}" \
-H "x-api-key : {API_KEY}"
```

**Antwort**

```JSON
{
  "59c93f3da7d0c00000798f68": {
    "version": "1.0.4",
    "fileDescription": {
        "persisted": false,
        "format": "parquet"
    }
  }
}
```

Data will be written to [!DNL Experience Platform] using [Data Ingestion API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml).  Das Schreiben von Daten ist ein asynchroner Prozess. Werden Daten in Adobe Experience Platform geschrieben, wird ein Batch erst dann erstellt und als erfolgreich markiert, wenn der Schreibvorgang der Daten vollständig abgeschlossen ist.

Data in [!DNL Experience Platform] should be written in the form of parquet files.

## Ausführungsphase

As the execution starts, the connector (as defined in the source component) will read the data from [!DNL Experience Platform] using the [!DNL Data Access API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml). Beim Umwandlungsprozess werden die in einer bestimmten Zeitspanne erfassten Daten gelesen. Intern werden dabei Batches von Quelldatensätzen abgefragt. Bei der Abfrage werden ein parametrisiertes Datumsformat (rollierend für Zeitreihen- oder inkrementelle Daten) verwendet und Datensatzdateien für diese Batches aufgelistet sowie Anfragen für Daten dieser Datensatzdateien eingeleitet.

### Beispiele für Umwandlungen

Das Dokument [Beispiele für ETL-Umwandlungen](./transformations.md) enthält eine Reihe von Beispiel-Umwandlungen und geht dabei auch auf die Handhabung von Identitäten und die Zuordnung von Datentypen ein. Diese Umwandlungen können sie als Referenz verwenden.

### Read data from [!DNL Experience Platform]

Using the [!DNL Catalog API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml), you can fetch all batches between a specified start time and end time, and sort them by the order they were created.

**Anfrage**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?dataSet=DATASETID&createdAfter=START_TIMESTAMP&createdBefore=END_TIMESTAMP&sort=desc:created" \
  -H "Accept: application/json" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

Details on filtering batches can be found in the [Data Access tutorial](../data-access/tutorials/dataset-data.md).

### Aufrufen von Dateien aus einem Batch

Sobald Sie die ID für den gesuchten Batch (`{BATCH_ID}`) vorliegen haben, können Sie über die [!DNL Data Access API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) eine Liste der einem bestimmten Datensatz zugehörigen Dateien abrufen.  Details for doing so are available in the [Data Access tutorial](../data-access/tutorials/dataset-data.md).

**Anfrage**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

### Zugreifen auf Dateien mittels Datei-ID

Unter Verwendung der eindeutigen ID einer Datei (`{FILE_ID`) kann über die [!DNL Data Access API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) auf spezifische Dateidetails zugegriffen werden, darunter ihr Name, ihre Größe in Byte und ein Link, unter dem sie heruntergeladen werden kann.

**Anfrage**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{FILE_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key : {API_KEY}"
```

Die Antwort verweist entweder auf eine einzelne Datei oder auf ein Verzeichnis. Details on each can be found in the [Data Access tutorial](../data-access/tutorials/dataset-data.md).

### Zugreifen auf den Dateiinhalt

The [!DNL Data Access API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) can be used to access the contents of a specific file. Um den Inhalt abzurufen, wird eine GET-Anfrage unter Verwendung des für `_links.self.href` beim Zugriff auf eine Datei mittels Datei-ID zurückgegebenen Werts gesendet.

**Anfrage**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{DATASET_FILE_ID}?path=filename1.csv" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

Die Antwort auf diese Anfrage liefert den Inhalt der Datei. Weitere Informationen, darunter auch Einzelheiten zur Paginierung von Antworten, finden Sie im Tutorial zur [Datenabfrage mittels Data Access API](../data-access/tutorials/dataset-data.md).

### Validieren von Datensätzen auf Einhaltung von Schema-Vorgaben

Beim Schreiben von Daten können Anwender bestimmen, dass Daten entsprechend den im XDM-Schema definierten Validierungsregeln geprüft werden. Weitere Informationen zur Validierung von Schemas finden Sie auf GitHub im [ETL Ecosystem Integration Reference Code](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md#validation).

Wenn Sie die auf [!DNL GitHub](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md) bereitgestellte Referenzimplementierung nutzen, können Sie für diese Implementierung die Schemavalidierung mithilfe der Systemeigenschaft `-DenableSchemaValidation=true` aktivieren.

Die Validierung kann für logische XDM-Typen durchgeführt werden, dies unter Verwendung von Attributen wie `minLength` und `maxlength` für Zeichenfolgen, `minimum` und `maximum` für Ganzzahlen und mehr. Eine Tabelle mit den für die Validierung verwendbaren XDM-Typen und Eigenschaften finden Sie im [Schema Registry API-Entwicklerhandbuch](../xdm/api/getting-started.md).

>[!NOTE]
>
>Die für verschiedene `integer`-Typen bereitgestellten MIN- und MAX-Werte sind die vom jeweiligen Typ unterstützten Werte. Diese können jedoch auch auf Minimal- und Maximalwerte Ihrer Wahl beschränkt werden.

### Erstellen eines Batches

Once the data is processed, the ETL tool will write the data back to [!DNL Experience Platform] using the [Batch Ingestion API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml). Bevor einem Datensatz Daten hinzugefügt werden können, müssen sie mit einem Batch verknüpft werden, der später in einen bestimmten Datensatz hochgeladen wird.

**Anfrage**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -d '{
        "datasetId":"{DATASET_ID}"
      }'
```

Einzelheiten zur Erstellung eines Batches, einschließlich Beispiel-Anfragen und -Antworten, finden Sie unter [Übersicht über die Batch-Aufnahme](../ingestion/batch-ingestion/overview.md).

### Schreiben in einen Datensatz

Nach erfolgreicher Erstellung eines neuen Batches können Dateien in einen bestimmten Datensatz hochgeladen werden. In einen Batch können mehrere Dateien aufgenommen werden, dies so lange, bis dieser zur Aufnahme verwendet wird. Dateien können mithilfe der _Small File Upload API_ hochgeladen werden. Überschreitet die Größe Ihrer Dateien jedoch den Grenzwert des Gateways, müssen Sie die _Large File Upload API_ verwenden. Einzelheiten zum Upload kleiner und großer Dateien finden Sie unter [Übersicht über die Batch-Aufnahme](../ingestion/batch-ingestion/overview.md).

**Anfrage**

Data in [!DNL Experience Platform] should be written in the form of parquet files.

```shell
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/dataSets/{DATASET_ID}/files/{FILE_NAME}.parquet" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id:{IMS_ORG}" \
  -H "Authorization:Bearer ACCESS_TOKEN" \
  -H "x-api-key: API_KEY" \
  -H "content-type: application/octet-stream" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

### Kennzeichnen des Batch-Uploads als fertiggestellt

Nachdem alle Dateien in den Batch hochgeladen wurden, kann dieser als fertiggestellt gekennzeichnet werden. By doing this, the [!DNL Catalog] &quot;DataSetFile&quot; entries are created for the completed files and associated with the generate batch. The [!DNL Catalog] batch is then marked as successful, which triggers downstream flows to ingest the available data.

Die Daten werden in Adobe Experience Platform zunächst in der Staging-Umgebung abgelegt, um dann nach Katalogisierung und Validierung an ihren endgültigen Speicherort verschoben zu werden. Sobald alle Daten eines Batches an einen dauerhaften Speicherort verschoben wurden, wird dieser als erfolgreich markiert.

**Anfrage**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

Bei erfolgreicher Ausführung wird der HTTP-Statuscode 200 (OK) zurückgegeben, wobei der Antworttext leer bleibt.

Das ETL-Tool hält den Zeitstempel der Quelldatensätze beim Lesen der Daten fest.

Wird die Umwandlung das nächste Mal ausgeführt, dies etwa nach Zeitplan oder durch Ereignisaufruf, fordert das ETL-Tool die Daten mit dem zuvor gespeicherten Zeitstempel sowie allen darauf folgenden Daten an.

### Abrufen des Status des letzten Batches

Bevor Sie neue Aufgaben im ETL-Tool ausführen können, müssen Sie sicherstellen, dass der letzte Batch erfolgreich abgeschlossen wurde. Die [!DNL Catalog Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) bietet eine Option, mit deren Hilfe die spezifischen Details der betreffenden Batches abgerufen werden können.

**Anfrage**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?limit=1&sort=desc:created" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Antwort**

Neue Aufgaben können terminiert werden, wenn der Wert „status“ des vorherigen Batches „success“, also Erfolg, lautet (wie unten dargestellt):

```json
"{BATCH_ID}": {
    "imsOrg": "{IMS_ORG}",
    "created": 1494349962314,
    "createdClient": "{API_KEY}",
    "createdUser": "CLIENT_USER_ID@AdobeID",
    "updatedUser": "CLIENT_USER_ID@AdobeID",
    "updated": 1494349963467,
    "status": "success",
    "errors": [],
    "version": "1.0.1",
    "availableDates": {}
}
```

### Abrufen des Status des letzten Batches via ID

Der Status einzelner Batches kann über die [!DNL Catalog Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) mittels GET-Anfrage unter Verwendung der `{BATCH_ID}` abgerufen werden. Für die `{BATCH_ID}` ist dabei die ID anzugeben, die beim Erstellen des Batches zurückgegebenen wurde.

**Anfrage**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Antwort – erfolgreich**

Die nachfolgende Antwort zeigt mit „success“ einen Batch, der erfolgreich war.

```json
"{BATCH_ID}": {
    "imsOrg": "{IMS_ORG}",
    "created": 1494349962314,
    "createdClient": "{API_KEY}",
    "createdUser": "{CREATED_USER}",
    "updatedUser": "{UPDATED_USER}",
    "updated": 1494349962314,
    "status": "success",
    "errors": [],
    "version": "1.0.1",
    "availableDates": {}
}
```

**Antwort – fehlgeschlagen**

Für fehlgeschlagene Batches können die unter „errors“ beschriebenen Fehler aus der Antwort extrahiert und als Fehlermeldungen im ETL-Tool angezeigt werden.

```json
"{BATCH_ID}": {
    "imsOrg": "{IMS_ORG}",
    "created": 1494349962314,
    "createdClient": "{API_KEY}",
    "createdUser": "{CREATED_USER}",
    "updatedUser": "{UPDATED_USER}",
    "updated": 1494349962314,
    "status": "failure",
    "errors": [
        {
            "code": "200",
            "description": "Error in validating schema for file: 'adl://dataLake.azuredatalakestore.net/connectors-dev/stage/BATCHID/dataSetId/contact.csv' with errorMessage=adl://dataLake.azuredatalakestore.net/connectors-dev/stage/BATCHID/dataSetId/contact.csv is not a Parquet file. expected magic number at tail [80, 65, 82, 49] but found [57, 98, 55, 10] and errorType=java.lang.RuntimeException",
            "rows": []
        }
    ],
    "version": "1.0.1",
    "availableDates": {}
}
```

## Inkrementelle gegenüber Momentaufnahmen-Daten und Ereignisse gegenüber Profilen

Daten können in einer 2-mal-2-Matrix wie folgt dargestellt werden:

| Inkrementelle Ereignisse | Inkrementelle Profile |
|-------------------------------|----------------------|
| Momentaufnahmen-Ereignisse (weniger wahrscheinlich) | Momentaufnahmen-Profile |

Ereignisdaten werden in der Regel verwendet, wenn jede Zeile über eine indizierte Spalte mit Zeitstempel verfügt.

Profildaten werden in der Regel nur verwendet, wenn für sie kein Zeitstempel vorhanden ist und jede Zeile mit einem Primärschlüssel/zusammengesetzten Schlüssel identifiziert werden kann.

Inkrementelle Daten sind Daten, bei denen nur neue/aktualisierte Daten in das System eingehen und an aktuelle Daten in den Datensätzen angehängt werden.

Momentaufnahmen-Daten liegen vor, wenn alle in das System eingehenden Daten alle in einem Datensatz vorhandenen Daten ersetzen.

Im Falle von inkrementellen Ereignissen sollte das ETL-Tool die verfügbaren Datumsinformationen bzw. das Erstellungsdatum der Batch-Entität verwenden. Bei einem Push-Service sind keine Informationen zum Verfügbarkeitsdatum vorhanden, daher kennzeichnet das Tool die Inkremente über das Datum der Batch-Erstellung/-Aktualisierung. Batches mit inkrementellen Ereignissen müssen allesamt verarbeitet werden.

Für inkrementelle Profile verwendet das ETL-Tool das Erstellungs-/Aktualisierungsdatum der Batch-Entität. In der Regel müssen Batches mit inkrementellen Ereignissen allesamt verarbeitet werden.

Momentaufnahmen-Ereignisse sind aufgrund des Datenvolumens eher unwahrscheinlich. Wenn aber doch erforderlich, muss das ETL-Tool für die Verarbeitung nur den letzten Batch auswählen.

Wenn Momentaufnahmen-Profile verwendet werden, muss das ETL-Tool die Daten aus dem letzten Batch auswählen, der im System eingegangen sind. Besteht jedoch die Anforderung, Versionsänderungen zu dokumentieren, müssen alle Batches verarbeitet werden. Der ETL-Prozess beinhaltet eine Deduplizierung, durch die die Kosten der Datenspeicherung in Grenzen gehalten werden.

## Batch-Wiederholung und erneute Datenverarbeitung

Die Wiederholung von Batches und erneute Datenverarbeitung sind unter Umständen erforderlich, wenn ein Client feststellt, dass die in den letzten „n“ Tagen mittels ETL verarbeiteten Daten nicht wie erwartet aufgetreten sind oder möglicherweise die Quelldaten selbst nicht korrekt waren.

To do this, the client&#39;s data administrators will use the [!DNL Platform] UI to remove the batches containing corrupt data. Dann muss der ETL-Prozess wahrscheinlich erneut ausgeführt und somit mit korrekten Daten ausgefüllt werden. Wenn die Quelle selbst beschädigte Daten aufwies, muss der Data Engineer/Datenadministrator die Quell-Batches berichtigen und die Datenaufnahme erneut durchführen (entweder in Adobe Experience Platform oder mittels ETL-Connectoren).

Je nach Typ der zu generierenden Daten kann der Data Engineer einen einzelnen Batch oder alle Batches aus spezifischen Datensätzen entfernen. Data will be removed/archived as per [!DNL Experience Platform] guidelines.

Ein wahrscheinliches Szenario ist, dass die ETL-Funktionen zum Bereinigen von Daten benötigt werden.

Nach Abschluss der Bereinigung müssen die Client-Administratoren Adobe Experience Platform dahingehend neu konfigurieren, dass die Verarbeitung für Core Services ab dem Zeitpunkt des Löschens der Batches neu gestartet wird.

## Gleichzeitige Verarbeitung von Batches

Nach Ermessen des Client können Datenadministratoren/Data Engineers Daten in Abhängigkeit von den Merkmalen eines bestimmten Datensatzes entweder sequenziell oder gleichzeitig extrahieren, umwandeln und laden. Die Entscheidung hängt ab vom Anwendungsfall, auf den die umgewandelten Daten abzielen.

Wenn beispielsweise ein aktualisierbarer, persistenter Speicher beibehalten werden soll und die Sequenz oder Reihenfolge der Ereignisse wichtig ist, ist eine ausschließlich sequenzielle Verarbeitung von ETL-Umwandlungen erforderlich.

In anderen Fällen können Daten, die nicht in Reihenfolge vorliegen, von nachgelagerten Anwendungen/Prozessen verarbeitet werden, die anhand eines festgelegten Zeitstempels intern die Sortierung vornehmen. In diesen Fällen können gleichzeitige ETL-Umwandlungen zur Verbesserung der Verarbeitungszeit beitragen.

Bei Quell-Batches hängt die Entscheidung ebenfalls von der Präferenz des Client sowie von Begrenzungen seitens Verbrauchern ab. Wenn eine gleichzeitige Erfassung von Quelldaten ohne Berücksichtigung von Hierarchie/Reihenfolge einer Zeile möglich ist, kann der Umwandlungsprozess Batches für die Verarbeitung mit einem höheren Grad an Parallelität erstellen (Optimierung basierend Auftragsverarbeitung ohne Reihenfolge). Wenn bei der Umwandlung jedoch Zeitstempel berücksichtigt oder die Rangfolge geändert werden muss, muss die Data Access API oder für die Planung/den Aufruf des ETL-Tools sichergestellt sein, dass Batches soweit möglich nicht in Reihenfolge verarbeitet werden.

## Rückstellung

Der Prozess der Rückstellung wird angewendet, wenn Eingabedaten noch nicht vollständig genug sind, um an nachgelagerte Prozesse übergeben zu werden, jedoch in Zukunft nützlich sein könnten. Clients legen ihre individuelle Toleranz hinsichtlich des Daten-Windowing für den zukünftigen Abgleich gegenüber den Verarbeitungskosten fest, um über ihre Entscheidung zu informieren, Daten beiseite zu legen und sie bei der nächsten Umwandlung neu zu verarbeiten. Dies geschieht in der Hoffnung, sie zu einem späteren Zeitpunkt innerhalb des Aufbewahrungsfensters anreichern und abstimmen/zusammenführen zu können. Dieser Zyklus dauert so lange an, bis die Zeile entweder ausreichend verarbeitet oder als veraltet gilt. Im letzteren Fall ist sie dann keine weitere Investition mehr wert. Bei jeder Iteration werden zurückgestellte Daten generiert, die ein Superset aller zurückgestellten Daten der vorherigen Iterationen darstellen.

Adobe Experience Platform does not identify deferred data currently, so client implementations must rely on the ETL and Dataset manual configurations to create another dataset in [!DNL Platform] mirroring the source dataset which can be used to keep deferred data. In diesem Fall sind zurückgestellte Daten Momentaufnahmen-Daten ähnlich: Bei jeder Ausführung der ETL-Umwandlung werden die Quelldaten mit verzögerten Daten zusammengeführt und zur Verarbeitung übergeben.

## Änderungsprotokoll

| Datum | Aktion | Beschreibung |
| ---- | ------ | ----------- |
| 19.01.2019 | Eigenschaft „fields“ aus Datensätzen entfernt | Bislang umfassten Datensätze eine „fields“-Eigenschaft, die eine Kopie des Schemas enthielt. Diese Funktion sollte nicht mehr verwendet werden. Ist die Eigenschaft „fields“ vorhanden, sollte sie ignoriert und stattdessen das Attribut „surveillanceSchema“ oder „schemaRef“ verwendet werden. |
| 15.03.2019 | Datensätze ergänzt um Eigenschaft „schemaRef“ | Die Eigenschaft „schemaRef“ eines Datensatzes enthält einen URI, der auf das XDM-Schema verweist, auf dem der Datensatz basiert, und der alle vom Datensatz potenziell verwendbaren Felder repräsentiert. |
| 15.03.2019 | Alle Endbenutzer-IDs der Eigenschaft „identityMap“ zugeordnet | Bei der „identityMap“ handelt es sich um eine Kapselung aller eindeutigen Kennungen eines Subjekts, z. B. CRM-ID, ECID oder Treueprogramm-ID. This map is used by [!DNL Identity Service](../identity-service/home.md) to resolve all known and anonymous identities of a subject, forming a single identity graph for each end-user. |
| 30.05.2019 | Eigenschaft „Schema“ wurde eingestellt und aus Datensätzen entfernt | Anhand der Eigenschaft „Schema“ des Datensatzes wurde ein Verweis auf das Schema mit dem veralteten Endpunkt `/xdms` in der Service API bereitgestellt. [!DNL Catalog] This has been replaced by a &quot;schemaRef&quot; that provides the &quot;id&quot;, &quot;version&quot;, and &quot;contentType&quot; of the schema as referenced in the new [!DNL Schema Registry] API. |