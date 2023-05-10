---
keywords: Experience Platform;Startseite;beliebte Themen;ETL;etl;etl-Integrationen;ETL-Integrationen
solution: Experience Platform
title: Entwickeln von ETL-Integrationen für Adobe Experience Platform
description: Im Handbuch zur ETL-Integration werden die grundlegenden Schritte für die Erstellung von hochperformanten, sicheren Connectoren für Experience Platform und für die Aufnahme von Daten in Platform erläutert.
exl-id: 7d29b61c-a061-46f8-a31f-f20e4d725655
source-git-commit: 76ef5638316a89aee1c6fb33370af943228b75e1
workflow-type: tm+mt
source-wordcount: '4081'
ht-degree: 100%

---

# Entwickeln von ETL-Integrationen für Adobe Experience Platform

Im Handbuch zur ETL-Integration werden die grundlegenden Schritte für die Erstellung von leistungsstarken, sicheren Connectoren für [!DNL Experience Platform] und für die Aufnahme von Daten in [!DNL Platform] erläutert.


- [[!DNL Catalog]](https://www.adobe.io/experience-platform-apis/references/catalog/)
- [[!DNL Data Access]](https://www.adobe.io/experience-platform-apis/references/data-access/)
- [[!DNL Batch Ingestion]](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/)
- [[!DNL Streaming Ingestion]](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/)
- [Authentifizierung und Autorisierung für Experience Platform-APIs](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de)
- [[!DNL Schema Registry]](https://www.adobe.io/experience-platform-apis/references/schema-registry/)

Dieses Handbuch beinhaltet außerdem Beispiele für die zur Erstellung eines ETL-Connectors zu verwendenden API-Aufrufe sowie Links zu Dokumentationen, in denen die einzelnen [!DNL Experience Platform]-Services einschließlich der Arbeit mit der ihnen jeweils zugehörigen API erläutert werden.

Ein Beispiel für eine Integration ist auf [!DNL GitHub] über den [ETL Ecosystem Integration Reference Code](https://github.com/adobe/acp-data-services-etl-reference) unter der [!DNL Apache]-Lizenz Version 2.0 verfügbar.

## Workflow

Das folgende Diagramm skizziert den allgemeinen Workflow für die Integration der Komponenten von Adobe Experience Platform mit einer ETL-Anwendung und einem ETL-Connector.

![](images/etl.png)

## Komponenten von Adobe Experience Platform

An der Integration mit ETL-Connectoren ist eine Vielzahl der Komponenten von Experience Platform beteiligt. Die folgende Liste zeigt einige der zentralen Komponenten und ihre Funktionalitäten:

- **Adobe Identity Management System (IMS)**: Bietet ein Framework für die Authentifizierung bei Adobe-Services.
- **IMS-Organisation**: Eine Unternehmens-Entität, die Produkte und Services besitzen oder lizenzieren und Zugriff auf ihre Mitglieder gewähren kann.
- **IMS-Anwender**: Die Mitglieder einer IMS-Organisation. Organisation und Anwender stehen in einer m:n-Beziehung zueinander.
- **[!DNL Sandbox]**: Eine virtuelle Partition einer einzelnen [!DNL Platform]-Instanz, in der Programme für digitale Erlebnisse entwickelt und weiterentwickelt werden können.
- **Datenerkennung**: Erfasst die Metadaten von aufgenommenen und umgewandelten Daten in [!DNL Experience Platform].
- **[!DNL Data Access]**: Bietet eine Schnittstelle für Anwender, über die sie auf ihre Daten in [!DNL Experience Platform] zugreifen können.
- **[!DNL Data Ingestion]**: Überträgt Daten an [!DNL Experience Platform] mit [!DNL Data Ingestion]-APIs.
- **[!DNL Schema Registry]**: Definiert und speichert das Schema, das die Struktur der in [!DNL Experience Platform] zu verwendenden Daten beschreibt.

## Erste Schritte mit [!DNL Experience Platform]-APIs

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um [!DNL Experience Platform]-APIs erfolgreich aufrufen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Handbuch wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle Ressourcen in [!DNL Experience Platform] sind auf bestimmte virtuelle Sandboxes beschränkt. Bei allen Anfragen an [!DNL Platform]-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxes in [!DNL Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../sandboxes/home.md).

Bei allen Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche Kopfzeile erforderlich:

- Content-Type: application/json

## Allgemeiner Ablauf

Zunächst meldet sich ein ETL-Anwender bei der Benutzeroberfläche von [!DNL Experience Platform] an und erstellt Datensätze für die Aufnahme mit einem Standard-Connector oder einem Push-Service-Connector.

In der Benutzeroberfläche erstellt der Anwender den Ausgabedatensatz, indem er ein Datensatzschema auswählt. Die Auswahl des Schemas hängt davon ab, welcher Datentyp (Datensatz- oder Zeitreihendaten) in [!DNL Platform] aufgenommen wird. In der Benutzeroberfläche können alle verfügbaren Schemas einschließlich des vom Schema unterstützten Verhaltenstyps über die Registerkarte „Schemas“ eingesehen werden.

Beginnt der Anwender im ETL-Tool mit der Konzeptionierung, wird seine Zuordnung nach Konfiguration der entsprechenden Verbindung (unter Verwendung seiner Anmeldeinformationen) umgewandelt. Es wird hier davon ausgegangen, dass für das ETL-Tool bereits [!DNL Experience Platform]-Connectoren installiert wurden. (Auf den entsprechenden Prozess wird in diesem Integrationshandbuch nicht eingegangen.)

Modelldarstellungen eines Beispiel-ETL-Tools und -Workflows stehen unter [ETL-Workflow](./workflow.md) zur Verfügung. Die einzelnen ETL-Tools unterscheiden sich zwar in ihrem Format, sind sich in ihrer Funktion aber größtenteils ähnlich.

>[!NOTE]
>
>Der ETL-Connector muss einen Filter für den Zeitstempel definieren, der das Datum zur Aufnahme von Daten und Offset (d. h. das Fenster, für das Daten gelesen werden sollen) kennzeichnet. Das ETL-Tool sollte die Aufnahme dieser beiden Parameter in dieser oder einer anderen relevanten Benutzeroberfläche unterstützen. In Adobe Experience Platform werden diese Parameter entweder Informationen zum Verfügbarkeitsdatum (sofern vorhanden) oder zum Erfassungsdatum im Batch-Objekt des Datensatzes zugeordnet.

### Anzeigen einer Liste von Datensätzen

Über die Datenquelle für die Zuordnung kann eine Liste aller verfügbaren Datensätze anhand der [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/) abgerufen werden.

Sie können zur Auflistung aller verfügbaren Datensätze eine einzelne API-Anfrage (z. B. `GET /dataSets`) ausführen. Dabei empfiehlt sich als Best Practice die Angabe von Abfrageparametern, durch die die Größe der Antwort beschränkt wird.

Werden vollständige Datensatzinformationen angefragt, wächst die Größe der Antwort-Payload unter Umständen auf mehr als 3 GB an, was zu einer insgesamt verlangsamten Leistung führen kann. Die Verwendung von Abfrageparametern, mittels derer aus den Informationen nur die tatsächlich benötigten gefiltert werden, ist daher ein effizienterer Ansatz für [!DNL Catalog]-Abfragen.

#### Filtern von Listen

Sie können mehrere Filter für die Antwortausgabe verwenden, indem sie die entsprechenden Parameter durch ein kaufmännisches Und-Zeichen (`&`) voneinander trennen. Einige Abfrageparameter akzeptieren eine durch Komma getrennte Liste von Werten, darunter etwa der für die Eigenschaften verwendete „properties“-Filter in der unten dargestellten Beispielanfrage.

Die Zahl der [!DNL Catalog]-Antworten wird automatisch entsprechend den konfigurierten Einschränkungen begrenzt. Mithilfe des Abfrageparameters „limit“ kann jedoch die Begrenzung der Anzahl der zurückgegebenen Objekte individuell angepasst werden. Die Begrenzung der [!DNL Catalog]-Antworten ist wie folgt vorkonfiguriert:

- Wenn kein Limit-Parameter angegeben wird, beträgt die maximale Anzahl von Objekten pro Antwort-Payload 20.
- Die globale Begrenzung für alle anderen [!DNL Catalog]-Abfragen beträgt 100 Objekte.
- Bei Datensatzabfragen „observableSchema“ unter Angabe des „properties“-Abfrageparameters beträgt die maximale Anzahl der zurückgegebenen Datensätze 20.
- Bei Angabe ungültiger Parameter für die Begrenzung (einschließlich `limit=0`) wird ein HTTP-Fehler mit dem Status-Code 400 zurückgegeben, in dem die korrekten Bereiche angezeigt werden.
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
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

Unter [Catalog Service – Übersicht](../catalog/home.md) finden Sie ausführliche Beispiele dazu, wie Sie Aufrufe an die [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/) ausführen.

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

Die Eigenschaft „schemaRef“ eines Datensatzes enthält einen URI, der auf das XDM-Schema verweist, auf dem der Datensatz basiert. Das XDM-Schema („schemaRef“) umfasst alle vom Datensatz potenziell verwendbaren Felder, also nicht zwingend nur die, die tatsächlich verwendet werden (siehe „observableSchema“ weiter unten).

Das XDM-Schema ist das Schema, das Sie verwenden, wenn Sie dem Anwender eine Liste aller verfügbaren Felder anzeigen möchten, die ausgefüllt werden können.

Der erste Wert für „schemaRef.id“ im vorherigen Antwortobjekt (`https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18`) ist ein URI, der auf ein bestimmtes XDM-Schema in der [!DNL Schema Registry] verweist. Das Schema kann abgerufen werden, indem eine GET-Anfrage an die [!DNL Schema Registry]-API gesendet wird.

>[!NOTE]
>
>Die Eigenschaft „schema“ ist veraltet und wurde ersetzt durch die Eigenschaft „schemaRef“. Fehlt „schemaRef“ im Datensatz oder enthält keinen Wert, müssen Sie prüfen, ob eine „schema“-Eigenschaft vorhanden ist. Ersetzen Sie dazu im Abfrageparameter `properties` des vorherigen Aufrufs „schemaRef“ durch „Schema“. Näheres zur Eigenschaft „Schema“ finden Sie im nachfolgenden Abschnitt [Eigenschaft „Schema“ des Datensatzes](#dataset-schema-property-deprecated---eol-2019-05-30).

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
>`application/vnd.adobe.xed-id+json` Die Accept-Kopfzeilen und `application/vnd.adobe.xed-full+json; version={major version}` werden am häufigsten verwendet. `application/vnd.adobe.xed-id+json` wird empfohlen, wenn eine Liste der in der [!DNL Schema Registry] enthaltenen Ressourcen angezeigt werden soll, da über sie nur Titel, ID und Version zurückgegeben werden. `application/vnd.adobe.xed-full+json; version={major version}` wird empfohlen, wenn nur eine einzelne Ressource (über ihre „id“) angezeigt werden soll, da über sie alle (unter „properties“ verschachtelten) Felder sowie Titel und Beschreibungen zurückgegeben werden.

**Antwort**

Das zurückgegebene JSON-Schema beschreibt die Struktur sowie Feldebenen-Informationen wie Typ, Format, Minimum, Maximum usw. der Daten, dies serialisiert als JSON. Für den Fall, dass für die Datenaufnahme ein anderes Serialisierungsformat als JSON verwendet wird (z. B. Parquet oder Scala), steht im [Handbuch zur Schema Registry](../xdm/tutorials/create-schema-api.md) eine Tabelle mit dem gewünschten JSON-Typ („meta:xdmType“) und der entsprechenden Darstellung in anderen Formaten zur Verfügung.

Ergänzend zu dieser Tabelle umfasst das [!DNL Schema Registry]-Entwicklerhandbuch ausführliche Beispiele für alle mit der [!DNL Schema Registry]-API durchführbaren Aufrufe.

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

Wenn die Eigenschaft „schema“ eines Datensatzes ausgefüllt ist, bedeutet dies, dass das Schema ein veraltetes `/xdms`-Schema ist. Soweit unterstützt, sollte der ETL-Connector dann den Wert in der Eigenschaft „schema“ mit dem Endpunkt `/xdms` (ein veralteter Endpunkt in der [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/)) verwenden, um das veraltete Schema abzurufen.

**API-Format**

```http
GET /catalog/{"schema" property without the "@"}
```

**Anfrage**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/xdms/context/person?expansion=xdm" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
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
>Wenn das Feld „schema“ leer oder überhaupt nicht vorhanden ist, sollte der Connector das Feld „schemaRef“ lesen und die [Schema Registry-API](https://www.adobe.io/experience-platform-apis/references/schema-registry/) verwenden, wie in den vorherigen Schritten zum [Anzeigen eines Datensatzschemas](#view-dataset-schema) ausgeführt.

### Die Eigenschaft „observableSchema“

Die Eigenschaft „observableSchema“ eines Datensatzes weist eine JSON-Struktur auf, die mit der JSON-Struktur des XDM-Schemas übereinstimmt. Das „observableSchema“ enthält die in den eingehenden Eingabedateien vorhandenen Felder. Beim Schreiben von Daten in [!DNL Experience Platform] müssen Anwender nicht zwingend alle Felder aus dem Zielgruppenschema verwenden. Tatsächlich sollten sie nur diejenigen Felder bereitstellen, die tatsächlich verwendetet werden.

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
  -H "x-gw-ims-org-id: {ORG_ID}" \
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
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Antwort**

Die Antwort enthält die Datensatzdatei-ID als übergeordnete Eigenschaft, wobei die Dateidetails im ID-Objekt der Datensatzdatei enthalten sind.

```json
{
    "194e89b976494c9c8113b968c27c1472-1": {
        "batchId": "194e89b976494c9c8113b968c27c1472",
        "dataSetViewId": "5bf479a654f52014cfffe7f1",
        "imsOrg": "{ORG_ID}",
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
        "imsOrg": "{ORG_ID}",
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
        "imsOrg": "{ORG_ID}",
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

Die in der vorherigen Antwort zurückgegebenen Datensatzdatei-IDs können in einer GET-Anfrage verwendet werden, um über die [!DNL Data Access]-API weitere Dateidetails abzurufen.

Einzelheiten zur Arbeit mit der [!DNL Data Access] API finden Sie unter [Übersicht über den Datenzugriff](../data-access/home.md).

**API-Format**

```http
GET /export/files/{DATASET_FILE_ID}
```

**Anfrage**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
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

Um über die [[!DNL Data Access API]](../data-access/home.md) eine Vorschau von Daten abzurufen, kann die Eigenschaft „href“ verwendet werden.

**API-Format**

```http
GET /export/files/{FILE_ID}?path={FILE_NAME}.{FILE_FORMAT}
```

**Anfrage**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1?path=samplefile.parquet" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

Die Antwort auf die obige Anfrage enthält eine Vorschau des Dateiinhalts.

Weitere Informationen zur [!DNL Data Access]-API, darunter auch Einzelheiten zu Anfragen und Antworten, finden Sie unter [Datenzugriff – Übersicht](../data-access/home.md).

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
-H "x-gw-ims-org-id: {ORG_ID}" \
-H "x-sandbox-name: {SANDBOX_NAME}" \
-H "Authorization: Bearer {ACCESS_TOKEN}" \
-H "x-api-key: {API_KEY}"
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

Das Schreiben von Daten in [!DNL Experience Platform] erfolgt über die [Batch-Aufnahme-API](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/).  Das Schreiben von Daten ist ein asynchroner Prozess. Werden Daten in Adobe Experience Platform geschrieben, wird ein Batch erst dann erstellt und als erfolgreich markiert, wenn der Schreibvorgang der Daten vollständig abgeschlossen ist.

Zum Schreiben von Daten in [!DNL Experience Platform] sollte das Parquet-Dateiformat verwendet werden.

## Ausführungsphase

Bei der Ausführung liest der Connector (wie in der Quellkomponente definiert) die Daten aus [!DNL Experience Platform] mithilfe der [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/). Beim Umwandlungsprozess werden die in einer bestimmten Zeitspanne erfassten Daten gelesen. Intern werden dabei Batches von Quelldatensätzen abgefragt. Bei der Abfrage werden ein parametrisiertes Datumsformat (rollierend für Zeitreihen- oder inkrementelle Daten) verwendet und Datensatzdateien für diese Batches aufgelistet sowie Anfragen für Daten dieser Datensatzdateien eingeleitet.

### Beispiele für Umwandlungen

Das Dokument [Beispiele für ETL-Umwandlungen](./transformations.md) enthält eine Reihe von Beispiel-Umwandlungen und geht dabei auch auf die Handhabung von Identitäten und die Zuordnung von Datentypen ein. Diese Umwandlungen können sie als Referenz verwenden.

### Auslesen von Daten aus [!DNL Experience Platform]

Mithilfe der [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/) können Sie alle Batches innerhalb einer festgelegten Start- und Endzeit abrufen und nach der Reihenfolge sortieren, in der sie erstellt wurden.

**Anfrage**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?dataSet=DATASETID&createdAfter=START_TIMESTAMP&createdBefore=END_TIMESTAMP&sort=desc:created" \
  -H "Accept: application/json" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

Einzelheiten zum Filtern von Batches finden Sie im [Tutorial zum Datenzugriff](../data-access/tutorials/dataset-data.md).

### Aufrufen von Dateien aus einem Batch

Sobald Sie die ID für den gesuchten Batch (`{BATCH_ID}`) vorliegen haben, können Sie über die [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) eine Liste der einem bestimmten Datensatz zugehörigen Dateien abrufen.  Einzelheiten hierzu finden Sie im [[!DNL Data Access] -Tutorial](../data-access/tutorials/dataset-data.md).

**Anfrage**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

### Zugreifen auf Dateien mittels Datei-ID

Unter Verwendung der eindeutigen ID einer Datei (`{FILE_ID`) kann über die [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) auf spezifische Dateidetails zugegriffen werden, darunter ihr Name, ihre Größe in Byte und ein Link, unter dem sie heruntergeladen werden kann.

**Anfrage**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{FILE_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

Die Antwort verweist entweder auf eine einzelne Datei oder auf ein Verzeichnis. Einzelheiten zu jedem finden Sie im [[!DNL Data Access] -Tutorial](../data-access/tutorials/dataset-data.md).

### Zugreifen auf den Dateiinhalt

Der Zugriff auf den Inhalt einer bestimmten Datei ist über die [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) möglich. Um den Inhalt abzurufen, wird eine GET-Anfrage unter Verwendung des für `_links.self.href` beim Zugriff auf eine Datei mittels Datei-ID zurückgegebenen Werts gesendet.

**Anfrage**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{DATASET_FILE_ID}?path=filename1.csv" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

Die Antwort auf diese Anfrage liefert den Inhalt der Datei. Weitere Informationen, darunter auch Einzelheiten zur Paginierung von Antworten, finden Sie im Tutorial zur [Datenabfrage mittels Data Access API](../data-access/tutorials/dataset-data.md).

### Validieren von Datensätzen auf Einhaltung von Schema-Vorgaben

Beim Schreiben von Daten können Anwender bestimmen, dass Daten entsprechend den im XDM-Schema definierten Validierungsregeln geprüft werden. Weitere Informationen zur Validierung von Schemata finden Sie auf im [ETL Ecosystem Integration Reference Code in  [!DNL GitHub]](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md#validation).

Wenn Sie die auf [[!DNL GitHub]](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md) bereitgestellte Referenzimplementierung nutzen, können Sie für diese Implementierung die Schemavalidierung mithilfe der Systemeigenschaft `-DenableSchemaValidation=true` aktivieren.

Die Validierung kann für logische XDM-Typen durchgeführt werden, dies unter Verwendung von Attributen wie `minLength` und `maxlength` für Zeichenfolgen, `minimum` und `maximum` für Ganzzahlen und mehr. Eine Tabelle mit den für die Validierung verwendbaren XDM-Typen und Eigenschaften finden Sie im [Schema Registry-API-Entwicklerhandbuch](../xdm/api/getting-started.md).

>[!NOTE]
>
>Die für verschiedene `integer`-Typen bereitgestellten MIN- und MAX-Werte sind die vom jeweiligen Typ unterstützten Werte. Diese können jedoch auch auf Minimal- und Maximalwerte Ihrer Wahl beschränkt werden.

### Erstellen eines Batches

Hat das ETL-Tool die Daten verarbeitet, schreibt es sie mithilfe der [Batch-Aufnahme-API](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/) zurück in [!DNL Experience Platform]. Bevor einem Datensatz Daten hinzugefügt werden können, müssen sie mit einem Batch verknüpft werden, der später in einen bestimmten Datensatz hochgeladen wird.

**Anfrage**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -d '{
        "datasetId":"{DATASET_ID}"
      }'
```

Einzelheiten zur Erstellung eines Batches, einschließlich Beispiel-Anfragen und -Antworten, finden Sie unter [Batch-Erfassung – Übersicht](../ingestion/batch-ingestion/overview.md).

### Schreiben in einen Datensatz

Nach erfolgreicher Erstellung eines neuen Batches können Dateien in einen bestimmten Datensatz hochgeladen werden. In einen Batch können mehrere Dateien aufgenommen werden, dies so lange, bis dieser zur Aufnahme verwendet wird. Dateien können mithilfe der Small File Upload API hochgeladen werden. Überschreitet die Größe Ihrer Dateien jedoch den Grenzwert des Gateways, müssen Sie die Large File Upload API verwenden. Einzelheiten zum Hochladen kleiner und großer Dateien finden Sie unter [Batch-Erfassung – Übersicht](../ingestion/batch-ingestion/overview.md).

**Anfrage**

Zum Schreiben von Daten in [!DNL Experience Platform] sollte das Parquet-Dateiformat verwendet werden.

```shell
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/dataSets/{DATASET_ID}/files/{FILE_NAME}.parquet" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id:{ORG_ID}" \
  -H "Authorization:Bearer ACCESS_TOKEN" \
  -H "x-api-key: API_KEY" \
  -H "content-type: application/octet-stream" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

### Kennzeichnen des Batch-Uploads als fertiggestellt

Nachdem alle Dateien in den Batch hochgeladen wurden, kann dieser als fertiggestellt gekennzeichnet werden. Dies bewirkt, dass für die fertiggestellten Dateien die [!DNL Catalog]-Einträge „DataSetFile“ erstellt und dem erstellten Batch zugeordnet werden. Der [!DNL Catalog]-Batch wird dann als erfolgreich markiert, wodurch bei nachgelagerten Flüssen die Aufnahme der verfügbaren Daten ausgelöst wird.

Die Daten werden in Adobe Experience Platform zunächst in der Staging-Umgebung abgelegt, um dann nach Katalogisierung und Validierung an ihren endgültigen Speicherort verschoben zu werden. Sobald alle Daten eines Batches an einen dauerhaften Speicherort verschoben wurden, wird dieser als erfolgreich markiert.

**Anfrage**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

Bei erfolgreicher Ausführung wird der HTTP-Status-Code 200 (OK) zurückgegeben, wobei der Antworttext leer bleibt.

Das ETL-Tool hält den Zeitstempel der Quelldatensätze beim Lesen der Daten fest.

Wird die Umwandlung das nächste Mal ausgeführt, dies etwa nach Zeitplan oder durch Ereignisaufruf, fordert das ETL-Tool die Daten mit dem zuvor gespeicherten Zeitstempel sowie allen darauf folgenden Daten an.

### Abrufen des Status des letzten Batches

Bevor Sie neue Aufgaben im ETL-Tool ausführen können, müssen Sie sicherstellen, dass der letzte Batch erfolgreich abgeschlossen wurde. Die [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) bietet eine Option, mit deren Hilfe die spezifischen Details der betreffenden Batches abgerufen werden können.

**Anfrage**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?limit=1&sort=desc:created" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Antwort**

Neue Aufgaben können terminiert werden, wenn der Wert „status“ des vorherigen Batches „success“, also Erfolg, lautet (wie unten dargestellt):

```json
"{BATCH_ID}": {
    "imsOrg": "{ORG_ID}",
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

Der Status einzelner Batches kann über die [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) mittels GET-Anfrage unter Verwendung der `{BATCH_ID}` abgerufen werden. Für die `{BATCH_ID}` ist dabei die ID anzugeben, die beim Erstellen des Batches zurückgegebenen wurde.

**Anfrage**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Antwort – erfolgreich**

Die nachfolgende Antwort zeigt mit „success“ einen Batch, der erfolgreich war.

```json
"{BATCH_ID}": {
    "imsOrg": "{ORG_ID}",
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
    "imsOrg": "{ORG_ID}",
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

Dies erfolgt, indem die Datenadministratoren des Clients unter Verwendung der [!DNL Platform]-Benutzeroberfläche die Batches mit den beschädigten Daten entfernen. Dann muss der ETL-Prozess wahrscheinlich erneut ausgeführt und somit mit korrekten Daten ausgefüllt werden. Wenn die Quelle selbst beschädigte Daten aufwies, muss der Data Engineer/Datenadministrator die Quell-Batches berichtigen und die Datenaufnahme erneut durchführen (entweder in Adobe Experience Platform oder mittels ETL-Connectoren).

Je nach Typ der zu generierenden Daten kann der Data Engineer einen einzelnen Batch oder alle Batches aus spezifischen Datensätzen entfernen. Die Daten werden gemäß den Richtlinien von [!DNL Experience Platform] entfernt/archiviert.

Ein wahrscheinliches Szenario ist, dass die ETL-Funktionen zum Bereinigen von Daten benötigt werden.

Nach Abschluss der Bereinigung müssen die Client-Administratoren Adobe Experience Platform dahingehend neu konfigurieren, dass die Verarbeitung für Core Services ab dem Zeitpunkt des Löschens der Batches neu gestartet wird.

## Gleichzeitige Verarbeitung von Batches

Nach Ermessen des Client können Datenadministratoren/Data Engineers Daten in Abhängigkeit von den Merkmalen eines bestimmten Datensatzes entweder sequenziell oder gleichzeitig extrahieren, umwandeln und laden. Die Entscheidung hängt ab vom Anwendungsfall, auf den die umgewandelten Daten abzielen.

Wenn beispielsweise ein aktualisierbarer, persistenter Speicher beibehalten werden soll und die Sequenz oder Reihenfolge der Ereignisse wichtig ist, ist eine ausschließlich sequenzielle Verarbeitung von ETL-Umwandlungen erforderlich.

In anderen Fällen können Daten, die nicht in Reihenfolge vorliegen, von nachgelagerten Anwendungen/Prozessen verarbeitet werden, die anhand eines festgelegten Zeitstempels intern die Sortierung vornehmen. In diesen Fällen können gleichzeitige ETL-Umwandlungen zur Verbesserung der Verarbeitungszeit beitragen.

Bei Quell-Batches hängt die Entscheidung ebenfalls von der Präferenz des Client sowie von Begrenzungen seitens Verbrauchern ab. Wenn eine gleichzeitige Erfassung von Quelldaten ohne Berücksichtigung von Hierarchie/Reihenfolge einer Zeile möglich ist, kann der Umwandlungsprozess Batches für die Verarbeitung mit einem höheren Grad an Parallelität erstellen (Optimierung basierend Auftragsverarbeitung ohne Reihenfolge). Wenn bei der Umwandlung jedoch Zeitstempel berücksichtigt oder die Rangfolge geändert werden muss, muss die Data Access API oder für die Planung/den Aufruf des ETL-Tools sichergestellt sein, dass Batches soweit möglich nicht in Reihenfolge verarbeitet werden.

## Rückstellung

Der Prozess der Rückstellung wird angewendet, wenn Eingabedaten noch nicht vollständig genug sind, um an nachgelagerte Prozesse übergeben zu werden, jedoch in Zukunft nützlich sein könnten. Clients legen ihre individuelle Toleranz hinsichtlich des Daten-Windowing für den zukünftigen Abgleich gegenüber den Verarbeitungskosten fest, um über ihre Entscheidung zu informieren, Daten beiseite zu legen und sie bei der nächsten Umwandlung neu zu verarbeiten. Dies geschieht in der Hoffnung, sie zu einem späteren Zeitpunkt innerhalb des Aufbewahrungsfensters anreichern und abstimmen/zusammenführen zu können. Dieser Zyklus dauert so lange an, bis die Zeile entweder ausreichend verarbeitet oder als veraltet gilt. Im letzteren Fall ist sie dann keine weitere Investition mehr wert. Bei jeder Iteration werden zurückgestellte Daten generiert, die ein Superset aller zurückgestellten Daten der vorherigen Iterationen darstellen.

Adobe Experience Platform erkennt derzeit keine zeitversetzten Daten. Daher müssen Client-Implementierungen anhand manueller ETL- und Datensatz-Konfigurationen einen weiteren Datensatz in [!DNL Platform] erstellen, der den Quelldatensatz spiegelt. Dieser kann dann zur Aufbewahrung zeitversetzter Daten verwendet werden. In diesem Fall sind zurückgestellte Daten Momentaufnahmen-Daten ähnlich: Bei jeder Ausführung der ETL-Umwandlung werden die Quelldaten mit verzögerten Daten zusammengeführt und zur Verarbeitung übergeben.

## Änderungsprotokoll

| Datum | Aktion | Beschreibung |
| ---- | ------ | ----------- |
| 19.01.2019 | Eigenschaft „fields“ aus Datensätzen entfernt | Bislang umfassten Datensätze eine „fields“-Eigenschaft, die eine Kopie des Schemas enthielt. Diese Funktion sollte nicht mehr verwendet werden. Ist die Eigenschaft „fields“ vorhanden, sollte sie ignoriert und stattdessen das Attribut „observedSchema“ oder „schemaRef“ verwendet werden. |
| 15.03.2019 | Datensätze ergänzt um Eigenschaft „schemaRef“ | Die Eigenschaft „schemaRef“ eines Datensatzes enthält einen URI, der auf das XDM-Schema verweist, auf dem der Datensatz basiert, und der alle vom Datensatz potenziell verwendbaren Felder repräsentiert. |
| 15.03.2019 | Alle Endbenutzer-IDs der Eigenschaft „identityMap“ zugeordnet | Bei der „identityMap“ handelt es sich um eine Kapselung aller eindeutigen Kennungen eines Subjekts, z. B. CRM-ID, ECID oder Treueprogramm-ID. Diese Zuordnung wird von [[!DNL Identity Service]](../identity-service/home.md) verwendet, um alle bekannten und anonymen Identitäten eines Subjekts aufzulösen und für jeden Endbenutzer ein individuelles Identitätsdiagramm zu erstellen. |
| 30.05.2019 | Eigenschaft „Schema“ wurde eingestellt und aus Datensätzen entfernt | Anhand der Eigenschaft „Schema“ des Datensatzes wurde ein Verweis auf das Schema mit dem veralteten Endpunkt `/xdms` in der Service [!DNL Catalog] API bereitgestellt. Diese wurde ersetzt durch „schemaRef“, über das „id“, „version“ und „contentType“ des Schemas bereitgestellt wird, die in der neuen [!DNL Schema Registry]-API referenziert werden. |
