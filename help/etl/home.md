---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen von ETL-Integrationen
topic: overview
translation-type: tm+mt
source-git-commit: 4817162fe2b7cbf4ae4c1ed325db2af31da5b5d3
workflow-type: tm+mt
source-wordcount: '4227'
ht-degree: 0%

---


# Entwickeln von ETL-Integrationen für Adobe Experience Platform

Das Handbuch zur ETL-Integration beschreibt allgemeine Schritte zum Erstellen von leistungsstarken, sicheren Connectors für Experience Platform und zum Integrieren von Daten in die Plattform.


- [Katalog](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)
- [Datenzugriff](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml)
- [Dateneinbindung](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)
- [Authentication and Authorization APIs](../tutorials/authentication.md)
- [Schema-Registrierung](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)

Dieses Handbuch enthält auch Beispiel-API-Aufrufe, die beim Entwerfen eines ETL-Connectors verwendet werden, sowie Links zur Dokumentation, in der die einzelnen Experience Platform-Dienste skizziert werden, und die Verwendung seiner API im Detail.

Eine Beispielintegration ist auf GitHub über den [ETL Ecosystem Integration Reference Code](https://github.com/adobe/acp-data-services-etl-reference) unter der Apache License Version 2.0 verfügbar.

## Arbeitsablauf

Das folgende Workflow-Diagramm bietet eine allgemeine Übersicht zur Integration von Adobe Experience Platform-Komponenten mit einer ETL-Anwendung und einem Connector.

![](images/etl.png)

## Adobe Experience Platform-Komponenten

An ETL-Connector-Integrationen sind mehrere Experience Platform-Komponenten beteiligt. In der folgenden Liste werden mehrere Schlüsselkomponenten und -funktionen vorgestellt:

- **Adobe Identity Management System (IMS)** - Bietet ein Framework für die Authentifizierung von Adobe-Diensten.
- **IMS-Organisation** - Eine Unternehmenseinheit, die Produkte und Dienstleistungen besitzen oder lizenzieren und Zugriff auf ihre Mitglieder gewähren kann.
- **IMS-Benutzer** - Mitglieder einer IMS-Organisation. Die Beziehung zwischen Organisation und Benutzer ist viele zu viele.
- **Sandbox** - Eine virtuelle Partition eine einzige Plattform-Instanz, die bei der Entwicklung und Entwicklung digitaler Erlebnisanwendungen hilft.
- **Data Discovery** - zeichnet die Metadaten von erfassten und transformierten Daten in Experience Platform auf.
- **Datenzugriff** - Bietet Benutzern eine Oberfläche, auf die sie in Experience Platform zugreifen können.
- **Dateneinbettung** - Übergibt Daten an Experience Platform mit Data Ingestion-APIs.
- **Schema Registry** - Definiert und speichert Schema, das die Struktur der in Experience Platform zu verwendenden Daten beschreibt.

## Erste Schritte mit Experience Platform-APIs

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um Experience Platform-APIs erfolgreich aufrufen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Handbuch finden Sie Beispiele für API-Aufrufe, die zeigen, wie Sie Ihre Anforderungen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anforderungs-Nutzdaten. Beispiel-JSON, die in API-Antworten zurückgegeben wird, wird ebenfalls bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für Experience Platform.

### Werte für erforderliche Kopfzeilen sammeln

Um Aufrufe an Plattform-APIs durchführen zu können, müssen Sie zunächst das [Authentifizierungslehrgang](../tutorials/authentication.md)abschließen. Das Abschließen des Authentifizierungstreutorials stellt die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform API-Aufrufen bereit, wie unten dargestellt:

- Genehmigung: Träger `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in Experience Platform werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an Plattform-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Weitere Informationen zu Sandboxes in Platform finden Sie in der [Sandbox-Übersichtsdokumentation](../sandboxes/home.md).

Für alle Anforderungen mit einer Payload (POST, PUT, PATCH) ist ein zusätzlicher Header erforderlich:

- Content-Type: application/json

## Allgemeiner Benutzerfluss

Zunächst meldet sich ein ETL-Benutzer bei der Benutzeroberfläche von Experience Platform an und erstellt Datensätze für die Erfassung mit einem Standard-Connector oder einem Push-Service-Connector.

In der Benutzeroberfläche erstellt der Benutzer den Ausgabedatensatz, indem er ein DataSet-Schema auswählt. Die Auswahl des Schemas hängt davon ab, welche Art von Daten (Datensatz oder Zeitreihen) in die Plattform aufgenommen werden. Durch Klicken auf die Registerkarte &quot;Schema&quot;in der Benutzeroberfläche können alle verfügbaren Schema einschließlich des vom Schema unterstützten Verhaltenstyps Ansicht werden.

Im ETL-Tool entwirft der Beginn die Zuordnungstransformationen nach der Konfiguration der entsprechenden Verbindung (unter Verwendung seiner Anmeldeinformationen). Für das ETL-Tool werden bereits Experience Platform-Connectors installiert (Prozess, der in diesem Integrationsleitfaden nicht definiert ist).

Im [ETL-Arbeitsablauf](./workflow.md)wurden die Modelle für ein Beispiel-ETL-Tool und einen Workflow bereitgestellt. Die ETL-Werkzeuge unterscheiden sich zwar im Format, aber die meisten bieten ähnliche Funktionen.

>[!NOTE] Der ETL-Connector muss einen Zeitstempelfilter angeben, der das Datum zum Erfassen von Daten und zum Versatz kennzeichnet (d. h. das Fenster, für das Daten gelesen werden sollen). Das ETL-Tool sollte die Verwendung dieser beiden Parameter in dieser oder einer anderen relevanten Benutzeroberfläche unterstützen. In Adobe Experience Platform werden diese Parameter entweder den verfügbaren Daten (sofern vorhanden) oder dem erfassten Datum im Stapelobjekt des Datensatzes zugeordnet.

### Liste der Ansicht von Datensätzen

Mithilfe der Datenquelle für die Zuordnung kann eine Liste aller verfügbaren Datensätze mit der [Katalog-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)abgerufen werden.

Sie können eine einzige API-Anfrage zur Ansicht aller verfügbaren Datensätze (z. `GET /dataSets`), wobei es sich bewährt hat, Abfragen einzubeziehen, die die Größe der Antwort beschränken.

In Fällen, in denen _vollständige_ Datensatzinformationen angefordert werden, kann die Antwortnutzlast größer als 3 GB sein, was die Gesamtleistung verlangsamen kann. Die Verwendung von Abfragen-Parametern zum Filtern nur der benötigten Informationen macht die Abfragen des Katalogs effizienter.

#### Filterung von Listen

Beim Filtern von Antworten können Sie mehrere Filter in einem Aufruf verwenden, indem Sie die Parameter durch ein kaufmännisches Und trennen (`&`). Einige Abfrage-Parameter akzeptieren kommagetrennte Listen von Werten, z. B. den &quot;Eigenschaften&quot;-Filter in der unten stehenden Musteranforderung.

Katalogantworten werden automatisch entsprechend den konfigurierten Einschränkungen gezählt, jedoch kann der Parameter &quot;Limit&quot;-Abfrage verwendet werden, um die Einschränkungen anzupassen und die Anzahl der zurückgegebenen Objekte zu begrenzen. Die voreingestellten Antwortbeschränkungen für Kataloge sind:

- Wenn kein Limit-Parameter angegeben wird, beträgt die maximale Anzahl von Objekten pro Antwortnutzlast 20.
- Die globale Beschränkung für alle anderen Katalogobjekte beträgt 100 Abfragen.
- Bei DataSet-Abfragen beträgt die maximale Anzahl der zurückgegebenen Datensätze 20, wenn mithilfe des Parameters &quot;properties Abfrage&quot;die Angabe &quot;beobachtableSchema&quot;angefordert wird.
- Ungültige Limit-Parameter (einschließlich `limit=0`) werden mit einem HTTP 400-Fehler erfüllt, der die korrekten Bereiche umreißt.
- Wenn Beschränkungen oder Offsets als Parameter für die Abfrage übergeben werden, haben sie Vorrang vor den Überschriften.

Die Parameter der Abfrage werden in der Übersicht über den [Katalogdienst ausführlicher behandelt](../catalog/home.md).

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

Detaillierte Beispiele für Aufrufe der [Katalog-API](../catalog/home.md) finden Sie in der Übersicht [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)zum Katalogdienst.

**Antwort**

Die Antwort umfasst drei (`limit=3`) Datensätze, die den Parameter &quot;name&quot;, &quot;description&quot;und &quot;schemaRef&quot;wie vom Parameter &quot; `properties` Abfrage&quot;angegeben zeigen.

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

### Ansicht DataSet-Schema

Die Eigenschaft &quot;schemaRef&quot;eines Datensatzes enthält einen URI, der auf das XDM-Schema verweist, auf dem der Datensatz basiert. Das XDM-Schema (&quot;schemaRef&quot;) stellt alle _potenziellen_ Felder dar, die vom Dataset verwendet werden könnten, nicht notwendigerweise die Felder, die verwendet _werden_ (siehe &quot;beobachtableSchema&quot;unten).

Das XDM-Schema ist das Schema, das Sie verwenden, wenn Sie dem Benutzer eine Liste aller verfügbaren Felder präsentieren müssen, in die geschrieben werden kann.

Der erste &quot;schemaRef.id&quot;-Wert im vorherigen Antwortobjekt (`https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18`) ist ein URI, der auf ein bestimmtes XDM-Schema in der Schema-Registrierung verweist. Das Schema kann abgerufen werden, indem eine GET-Anforderung an die Schema Registry-API gesendet wird.

>[!NOTE] Die Eigenschaft &quot;schemaRef&quot;ersetzt die jetzt nicht mehr unterstützte Eigenschaft &quot;Schema&quot;. Wenn &quot;schemaRef&quot;im Datensatz fehlt oder keinen Wert enthält, müssen Sie prüfen, ob eine &quot;Schema&quot;-Eigenschaft vorhanden ist. Dies kann durch Ersetzen von &quot;schemaRef&quot;durch &quot;Schema&quot;im Parameter &quot; `properties` Abfrage&quot;im vorherigen Aufruf erfolgen. Weitere Informationen zur Eigenschaft &quot;Schema&quot;finden Sie im folgenden Abschnitt zur Eigenschaft &quot; [Schema&quot;des Datasets](#dataset-schema-property-deprecated---eol-2019-05-30) .

**API-Format**

```http
GET /schemaregistry/tenant/schemas/{url encoded schemaRef.id}
```

**Anfrage**

Die Anforderung verwendet den URL-kodierten `id` URI des Schemas (den Wert des Attributs &quot;schemaRef.id&quot;) und erfordert einen Accept-Header.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F274f17bc5807ff307a046bab1489fb18 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
```

Das Antwortformat hängt vom Typ des Accept-Headers ab, der in der Anforderung gesendet wird. Suchanfragen müssen auch im Accept-Header enthalten `version` sein. In der folgenden Tabelle sind die verfügbaren Accept-Kopfzeilen für Suchvorgänge aufgeführt:

| Accept | Beschreibung |
| ------ | ----------- |
| `application/vnd.adobe.xed-id+json` | Liste-(GET-)Anforderungen, Titel-, ID- und Versionsanforderungen |
| `application/vnd.adobe.xed-full+json; version={major version}` | $refs und allOf resolved, hat Titel und Beschreibungen |
| `application/vnd.adobe.xed+json; version={major version}` | Raw mit $ref und allOf, hat Titel und Beschreibungen |
| `application/vnd.adobe.xed-notext+json; version={major version}` | Raw mit $ref und allOf, keine Titel oder Beschreibungen |
| `application/vnd.adobe.xed-full-notext+json; version={major version}` | $refs und allOf aufgelöst, keine Titel oder Beschreibungen |
| `application/vnd.adobe.xed-full-desc+json; version={major version}` | $refs und allOf resolved, Deskriptoren enthalten |

>[!NOTE] `application/vnd.adobe.xed-id+json` und `application/vnd.adobe.xed-full+json; version={major version}` sind die am häufigsten verwendeten Accept-Header. `application/vnd.adobe.xed-id+json` wird für die Auflistung von Ressourcen in der Schema-Registrierung bevorzugt, da nur &quot;title&quot;, &quot;id&quot;und &quot;version&quot;zurückgegeben werden. `application/vnd.adobe.xed-full+json; version={major version}` wird empfohlen, eine bestimmte Ressource (durch ihre &quot;ID&quot;) anzuzeigen, da alle Felder (verschachtelt unter &quot;Eigenschaften&quot;) sowie Titel und Beschreibungen zurückgegeben werden.

**Antwort**

Das zurückgegebene JSON-Schema beschreibt die Struktur- und Feldebene-Informationen (&quot;Typ&quot;, &quot;Format&quot;, &quot;Minimum&quot;, &quot;Maximum&quot;usw.) der Daten, serialisiert als JSON. Bei Verwendung eines anderen Serialisierungsformats als JSON zur Erfassung (z. B. Parquet oder Scala) enthält das [Schema-Registrierungsleitfaden](../xdm/tutorials/create-schema-api.md) eine Tabelle mit dem gewünschten JSON-Typ (&quot;meta:xdmType&quot;) und der zugehörigen Darstellung in anderen Formaten.

Zusammen mit dieser Tabelle enthält das Schema Registry Developer Guide ausführliche Beispiele für alle möglichen Aufrufe, die mit der Schema Registry API durchgeführt werden können.

### Datenbestand &quot;Schema&quot;-Eigenschaft (DEPRECATED - EOL 2019-05-30)

Datasets können eine &quot;Schema&quot;-Eigenschaft enthalten, die jetzt nicht mehr unterstützt wird und vorübergehend für die Abwärtskompatibilität verfügbar bleibt. Beispielsweise kann eine Auflistungsanforderung (GET) ähnlich der zuvor erstellten Anforderung, bei der &quot;Schema&quot;im Parameter &quot; `properties` Abfrage&quot;durch &quot;schemaRef&quot;ersetzt wurde, Folgendes zurückgeben:

```json
{
  "5ba9452f7de80400007fc52a": {
    "name": "Sample Dataset 1",
    "description": "Description of Sample Dataset 1.",
    "schema": "@/xdms/context/person"
  }
}
```

Wenn die Eigenschaft &quot;Schema&quot;eines Datensatzes aufgefüllt wird, deutet dies darauf hin, dass das Schema ein nicht mehr unterstütztes `/xdms` Schema ist und der ETL-Connector, sofern unterstützt, den Wert in der Eigenschaft &quot;Schema&quot;mit dem `/xdms` Endpunkt (ein nicht mehr unterstützter Endpunkt in der [Katalog-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)) verwenden sollte, um das veraltete Schema abzurufen.

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

>[!NOTE] Ein optionaler Parameter für die Abfrage `expansion=xdm`weist die API an, alle referenzierten Schema vollständig zu erweitern und einzubinden. Dies sollten Sie tun, wenn Sie dem Benutzer eine Liste aller potenziellen Felder präsentieren.

**Antwort**

Ähnlich wie bei der [Anzeige des DataSet-Schemas](#view-dataset-schema)enthält die Antwort ein JSON-Schema, das die Struktur und die Informationen auf Feldebene der Daten beschreibt, serialisiert als JSON.

>[!NOTE] Wenn das Feld &quot;Schema&quot;leer ist oder nicht vollständig vorhanden ist, sollte der Connector das Feld &quot;schemaRef&quot;lesen und die [Schema-Registrierungs-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) wie in den vorherigen Schritten zur [Ansicht eines Schemas](#view-dataset-schema)verwenden.

### Die Eigenschaft &quot;beobachtableSchema&quot;

Die Eigenschaft &quot;beobachtableSchema&quot;eines Datensatzes hat eine JSON-Struktur, die mit der JSON-Struktur des XDM-Schemas übereinstimmt. Das &quot;beobachtableSchema&quot;enthält die Felder, die in den eingehenden Eingabedateien vorhanden waren. Beim Schreiben von Daten in Experience Platform ist es nicht erforderlich, dass ein Benutzer alle Felder aus dem Zielgruppe-Schema verwendet. Stattdessen sollten sie nur die verwendeten Felder bereitstellen.

Das beobachtbare Schema ist das Schema, das Sie verwenden würden, wenn Sie die Daten lesen oder eine Liste von Feldern präsentieren, die zum Lesen/Verordnen verfügbar sind.

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

### Vorschauen

Die ETL-Anwendung kann eine Funktion zur Vorschau von Daten bieten ([&quot;Abbildung 8&quot;im ETL-Arbeitsablauf](./workflow.md)). Die Datenzugriffs-API bietet verschiedene Optionen für die Vorschau von Daten.

Weitere Informationen, einschließlich einer schrittweisen Anleitung für die Vorschau von Daten mit der Datenzugriff-API, finden Sie im [Lernprogramm](../data-access/tutorials/dataset-data.md)zum Datenzugriff.

### Abrufen von Datensatzdetails mithilfe des Parameters &quot;properties&quot;-Abfrage

Wie in den obigen Schritten zur [Ansicht einer Liste von Datensätzen](#view-list-of-datasets)dargestellt, können Sie &quot;files&quot;mit dem Parameter &quot;properties&quot;zur Abfrage anfordern.

Detaillierte Informationen zum Abfragen von Datensätzen und verfügbaren Filtern für Antworten finden Sie in der Übersicht über den [Katalogdienst](../catalog/home.md) .

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

Die Antwort umfasst einen Datensatz (`limit=1`), der die Eigenschaft &quot;files&quot;anzeigt.

```json
{
  "5bf479a6a8c862000050e3c7": {
    "files": "@/dataSets/5bf479a6a8c862000050e3c7/views/5bf479a654f52014cfffe7f1/files"
  }
}
```

### Liste von Datensatzdateien mit dem Attribut &quot;files&quot;

Sie können auch eine GET-Anforderung verwenden, um Dateidetails mithilfe des Attributs &quot;files&quot;abzurufen.

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

Die Antwort enthält die DataSet-Datei-ID als Eigenschaft der obersten Ebene, wobei die Dateidetails im DataSet-Datei-ID-Objekt enthalten sind.

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

### Dateidetails abrufen

Die in der vorherigen Antwort zurückgegebenen DataSet-Datei-IDs können in einer GET-Anforderung verwendet werden, um weitere Dateidetails über die Datenzugriff-API abzurufen.

Die Übersicht über den [Datenzugriff](../data-access/home.md) enthält Details zur Verwendung der Datenzugriff-API.

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

### Vorschau der Dateidaten

Die Eigenschaft &quot;href&quot;kann verwendet werden, um Vorschauen über die [Datenzugriff-API](../data-access/home.md)abzurufen.

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

Die Antwort auf die obige Anforderung enthält eine Vorschau des Dateiinhalts.

Weitere Informationen zur Datenzugriff-API, einschließlich detaillierter Anforderungen und Antworten, finden Sie in der Übersicht über den [Datenzugriff](../data-access/home.md).

### &quot;fileDescription&quot;aus dem Datensatz abrufen

Die Zielkomponente als Ausgabe transformierter Daten, wählt der Dateningenieur ein Ausgabedataset ([&quot;Abbildung 12&quot;im ETL-Arbeitsablauf](workflow.md)). Das XDM-Schema ist mit dem Ausgabedataset verknüpft. Die zu schreibenden Daten werden durch das Attribut &quot;fileDescription&quot;der Datensatzentität der Data Discovery-APIs identifiziert. Diese Informationen können mit einer DataSet-ID abgerufen werden (`{DATASET_ID}`). Die Eigenschaft &quot;fileDescription&quot;in der JSON-Antwort enthält die angeforderten Informationen.

**API-Format**

```shell
GET /catalog/dataSets/{DATASET_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{DATASET_ID}` | Der `id` Wert des Datensatzes, auf den Sie zugreifen möchten. |

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

Daten werden mithilfe der [Dateneinbetungs-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)in Experience Platform geschrieben.  Das Schreiben von Daten ist ein asynchroner Prozess. Wenn Daten in Adobe Experience Platform geschrieben werden, wird ein Stapel erst dann erstellt und als Erfolg markiert, wenn die Daten vollständig geschrieben sind.

Daten in Experience Platform sollten in Form von Parkettdateien geschrieben werden.

## Ausführungsphase

Als Beginn der Ausführung liest der Connector (wie in der Quellkomponente definiert) die Daten aus Experience Platform mithilfe der [Datenzugriff-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml). Der Umwandlungsprozess liest die Daten für einen bestimmten Zeitraum. Intern werden Abfragen von Quelldatasets erstellt. Bei der Abfrage werden ein parametrisiertes Datumsformat (rollierend für Zeitreihendaten oder inkrementelle Daten) und Datendatensatzdateien für diese Beginn sowie Datenanforderungen für Beginn für diese Datenmenge verwendet.

### Beispieltransformationen

Das [Beispiel-ETL-Transformationen](./transformations.md) -Dokument enthält eine Reihe von Beispieltransformationen, einschließlich Identitätsverwaltung und Datentypzuordnungen. Bitte verwenden Sie diese Transformationen als Referenz.

### Daten aus Experience Platform lesen

Mithilfe der [Katalog-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)können Sie alle Stapel zwischen einer bestimmten Beginn- und Endzeit abrufen und nach der Reihenfolge sortieren, in der sie erstellt wurden.

**Anfrage**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?dataSet=DATASETID&createdAfter=START_TIMESTAMP&createdBefore=END_TIMESTAMP&sort=desc:created" \
  -H "Accept: application/json" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

Details zum Filtern von Stapeln finden Sie im [Lernprogramm](../data-access/tutorials/dataset-data.md)zum Datenzugriff.

### Dateien aus einem Stapel abrufen

Sobald Sie die ID für den gesuchten Stapel (`{BATCH_ID}`) haben, können Sie über die [Datenzugriff-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml)eine Liste von Dateien abrufen, die zu einem bestimmten Stapel gehören.  Details dazu finden Sie im [Datenzugriffs-Tutorial](../data-access/tutorials/dataset-data.md).

**Anfrage**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

### Zugriff auf Dateien mithilfe der Datei-ID

Mithilfe der eindeutigen ID einer Datei (`{FILE_ID`) kann die [Datenzugriff-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) verwendet werden, um auf die spezifischen Details der Datei zuzugreifen, einschließlich Name, Größe in Byte und Link zum Herunterladen.

**Anfrage**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{FILE_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key : {API_KEY}"
```

Die Antwort kann auf eine einzelne Datei oder einen Ordner verweisen. Details zu den einzelnen Elementen finden Sie in der [Datenzugriffsschulung](../data-access/tutorials/dataset-data.md).

### Dateiinhalt aufrufen

Die [Datenzugriffs-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) kann verwendet werden, um auf den Inhalt einer bestimmten Datei zuzugreifen. Um den Inhalt abzurufen, wird eine GET-Anforderung mit dem Wert erstellt, der `_links.self.href` beim Zugriff auf eine Datei mit der Datei-ID zurückgegeben wird.

**Anfrage**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{DATASET_FILE_ID}?path=filename1.csv" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

Die Antwort auf diese Anforderung enthält den Inhalt der Datei. Weitere Informationen, einschließlich Details zur Paginierung von Antworten, finden Sie im Lernprogramm [Datenzugriff-API](../data-access/tutorials/dataset-data.md) -Abfrage.

### Überprüfen von Datensätzen auf Einhaltung von Schemas

Wenn Daten geschrieben werden, können Benutzer Daten gemäß den im XDM-Schema definierten Validierungsregeln überprüfen. Weitere Informationen zur Validierung von Schemas finden Sie im [ETL Ecosystem Integration Reference Code on GitHub](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md#validation).

Wenn Sie die Referenzimplementierung von [GitHub](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md)verwenden, können Sie die Schema-Validierung in dieser Implementierung mithilfe der Systemeigenschaft aktivieren `-DenableSchemaValidation=true`.

Die Validierung kann für logische XDM-Typen durchgeführt werden, mit Attributen wie `minLength` und `maxlength` für Zeichenfolgen, `minimum` und `maximum` für Ganzzahlen usw. Das Entwicklerhandbuch für die [Schema Registry API enthält](../xdm/api/getting-started.md) eine Tabelle mit den XDM-Typen und den Eigenschaften, die für die Überprüfung verwendet werden können.

>[!NOTE] Die MIN- und MAX-Werte, die vom Typ unterstützt werden können, sind die MIN- und Maximalwerte für verschiedene `integer` Typen. Diese Werte können jedoch auf die Minimalwerte und die Maximierung Ihrer Wahl beschränkt werden.

### Stapel erstellen

Nach der Verarbeitung der Daten schreibt das ETL-Tool die Daten mithilfe der [Stapeleinbetungs-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)zurück an Experience Platform. Bevor Daten zu einem Datensatz hinzugefügt werden können, müssen sie mit einem Stapel verknüpft werden, der später in einen bestimmten Datensatz hochgeladen wird.

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

Details zum Erstellen eines Stapels, einschließlich Beispielanforderungen und Antworten, finden Sie in der Übersicht über die [Stapeleinbettung](../ingestion/batch-ingestion/overview.md).

### In Datensatz schreiben

Nach erfolgreicher Erstellung eines neuen Stapels können Dateien dann in einen bestimmten Datensatz hochgeladen werden. Mehrere Dateien können in einem Stapel veröffentlicht werden, bis sie beworben werden. Dateien können mit der _Small File Upload-API_ hochgeladen werden. Wenn Ihre Dateien jedoch zu groß sind und die Gateway-Grenze überschritten wird, können Sie die _Large File Upload-API_ verwenden. Details zur Verwendung von großen und kleinen Dateien finden Sie in der Übersicht über die [Stapeleinbettung](../ingestion/batch-ingestion/overview.md).

**Anfrage**

Daten in Experience Platform sollten in Form von Parkettdateien geschrieben werden.

```shell
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/dataSets/{DATASET_ID}/files/{FILE_NAME}.parquet" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id:{IMS_ORG}" \
  -H "Authorization:Bearer ACCESS_TOKEN" \
  -H "x-api-key: API_KEY" \
  -H "content-type: application/octet-stream" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

### Stapelupload als abgeschlossen markieren

Nachdem alle Dateien in den Stapel hochgeladen wurden, kann der Stapel zur Fertigstellung signalisiert werden. Auf diese Weise werden die Einträge &quot;DataSetFile&quot;des Katalogs für die abgeschlossenen Dateien erstellt und mit dem generierten Stapel verknüpft. Der Katalogstapel wird dann als erfolgreich markiert, wodurch nachgelagerte Flüsse zur Erfassung der verfügbaren Daten ausgelöst werden.

Die Daten landen zunächst am Staging-Speicherort auf der Adobe Experience Platform und werden dann nach der Katalogisierung und Validierung an den endgültigen Speicherort verschoben. Stapel werden als erfolgreich markiert, sobald alle Daten an einen dauerhaften Speicherort verschoben wurden.

**Anfrage**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

Bei erfolgreicher Ausführung gibt die Antwort HTTP-Status 200 OK zurück und der Antworttext ist leer.

Das ETL-Tool stellt sicher, dass der Zeitstempel der Quelldatasets beim Lesen der Daten notiert wird.

Bei der nächsten Ausführung der Transformation, wahrscheinlich nach Zeitplan oder Ereignis-Aufruf, fordert das ETL die Daten vom zuvor gespeicherten Zeitstempel und allen Daten in Zukunft an.

### Letzten Stapelstatus abrufen

Bevor Sie neue Aufgaben im ETL-Tool ausführen, müssen Sie sicherstellen, dass der letzte Stapel erfolgreich abgeschlossen wurde. Die [Katalogdienst-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) bietet eine stapelspezifische Option, die die Details der betreffenden Stapel enthält.

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

Neue Aufgaben können geplant werden, wenn der vorherige Batch-&quot;Status&quot;-Wert &quot;success&quot;lautet, wie unten dargestellt:

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

### Letzten Stapelstatus nach ID abrufen

Ein einzelner Stapelstatus kann über die [Katalogdienst-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) abgerufen werden, indem eine GET-Anforderung mit der `{BATCH_ID}`Methode ausgegeben wird. Die `{BATCH_ID}` verwendete ID entspricht der beim Erstellen des Stapels zurückgegebenen ID.

**Anfrage**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Antwort - Erfolg**

Die folgende Antwort zeigt einen &quot;Erfolg&quot;:

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

**Reaktion - Fehler**

Im Falle eines Fehlers können die &quot;Fehler&quot; aus der Antwort extrahiert und als Fehlermeldungen im ETL-Tool angezeigt werden.

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

## Inkrementelle oder Snapshot-Daten und Ereignis im Vergleich zu Profilen

Die Daten können wie folgt in einer Zwei-x-Matrix dargestellt werden:

| Inkrementelle Ereignis | Inkrementelle Profil |
|-------------------------------|----------------------|
| Snapshot-Ereignis (weniger wahrscheinlich) | Snapshot-Profile |

Ereignis-Daten werden in der Regel dann verwendet, wenn in jeder Zeile indizierte Zeitstempelspalten vorhanden sind.

Profil-Daten sind in der Regel dann vorhanden, wenn keine Daten einen Zeitstempel enthalten und jede Zeile mit einem primären/zusammengesetzten Schlüssel identifiziert werden kann.

Inkrementelle Daten sind Daten, bei denen nur neue/aktualisierte Daten in das System eingehen und an aktuelle Daten in den Datensätzen angehängt werden.

Snapshot-Daten sind Daten, wenn alle Daten in das System eingehen und einige oder alle vorherigen Daten in einem Datensatz ersetzen.

Bei inkrementellen Ereignissen sollte das ETL-Tool die verfügbaren Daten verwenden bzw. das Erstellungsdatum der Stapelentität verwenden. Im Falle eines Push-Dienstes sind keine verfügbaren Daten vorhanden. Daher verwendet das Tool für die Kennzeichnung von Inkrementen ein Batch-erstelltes/aktualisiertes Datum. Jeder Stapel von inkrementellen Ereignissen muss verarbeitet werden.

Für inkrementelle Profil verwendet das ETL-Tool erstellte/aktualisierte Daten der Batch-Entität. Normalerweise muss jeder Stapel von inkrementellen Profil-Daten verarbeitet werden.

Snapshot-Ereignis sind aufgrund der Größe der Daten sehr unwahrscheinlicher. Sollte dies erforderlich sein, muss das ETL-Tool nur den letzten Stapel zur Verarbeitung auswählen.

Wenn Snapshot-Profil verwendet werden, muss das ETL-Tool den letzten Stapel der Daten auswählen, die im System eintreffen. Wenn Sie jedoch die Versionen der Änderungen verfolgen möchten, müssen alle Stapel verarbeitet werden. Die Deduplizierungsverarbeitung im Rahmen des ETL-Verfahrens wird dazu beitragen, die Kosten der Datenspeicherung zu senken.

## Stapelwiedergabe und Datenverarbeitung

Die erneute Wiedergabe von Stapeln und die erneute Verarbeitung von Daten können erforderlich sein, wenn ein Kunde feststellt, dass in den letzten &#39;n&#39; Tagen die verarbeiteten Daten nicht erwartungsgemäß aufgetreten sind oder die Quelldaten selbst möglicherweise nicht korrekt waren.

Dazu verwenden die Datenadministratoren des Clients die Plattform-Benutzeroberfläche, um die Stapel mit beschädigten Daten zu entfernen. Dann wird das ETL wahrscheinlich erneut ausgeführt werden müssen und somit mit korrekten Daten repliziert werden müssen. Wenn die Quelle selbst beschädigte Daten aufwies, muss der Dateningenieur/Administrator die Quellstapel berichtigen und die Daten neu erfassen (entweder über Adobe Experience Platform oder über ETL-Connectors).

Je nach Typ der zu generierenden Daten kann der Dateningenieur einen einzelnen Stapel oder alle Stapel aus bestimmten Datensätzen entfernen. Daten werden gemäß den Richtlinien der Experience Platform entfernt/archiviert.

Es ist ein wahrscheinliches Szenario, dass die ETL-Funktion zum Bereinigen von Daten wichtig sein wird.

Nach Abschluss der Bereinigung müssen die Clientadministratoren Adobe Experience Platform neu konfigurieren, um die Verarbeitung für die Hauptdienste ab dem Zeitpunkt des Löschens der Stapel neu zu starten.

## Stapelverarbeitung gleichzeitig

Nach Ermessen des Kunden können Datenadministratoren/Ingenieure entscheiden, Daten in Abhängigkeit von den Merkmalen eines bestimmten Datensatzes sequenziell oder gleichzeitig zu extrahieren, umzuformen und zu laden. Dies basiert auch auf dem Anwendungsfall, in dem der Client auf die transformierten Daten abzielt.

Wenn der Client beispielsweise an einem aktualisierten Persistenzspeicher festhält und die Sequenz oder Reihenfolge der Ereignis wichtig ist, muss der Client möglicherweise Aufträge mit sequenziellen ETL-Transformationen streng verarbeiten.

In anderen Fällen können Daten, die nicht in der Reihenfolge vorliegen, von nachgeschalteten Anwendungen/Prozessen verarbeitet werden, die intern mit einem bestimmten Zeitstempel sortieren. In diesen Fällen können parallele ETL-Transformationen durchführbar sein, um die Verarbeitungszeit zu verbessern.

Bei Quell-Batches hängt es erneut von der Kundenpräferenz und der Kundenbeschränkung ab. Wenn die Quelldaten parallel aufgenommen werden können, ohne dass die Reihenfolge oder die Anforderung einer Zeile berücksichtigt wird, kann der Umwandlungsprozess Prozessstapel mit einem höheren Grad an Parallelität erstellen (Optimierung auf der Grundlage der Auftragsverarbeitung). Wenn die Transformation jedoch Zeitstempel berücksichtigen oder die Rangfolge ändern muss, muss die Datenzugriff-API oder die ETL-Tool-Planung/-Aufruffunktion sicherstellen, dass Stapel nach Möglichkeit nicht in der richtigen Reihenfolge verarbeitet werden.

## Zurückstellung

Bei der Aufschiebung handelt es sich um einen Prozess, bei dem Eingabedaten noch nicht vollständig genug sind, um an nachgelagerte Prozesse gesendet zu werden, aber in Zukunft verwendbar sein können. Die Kunden bestimmen ihre individuelle Toleranz für die Datenfenster für zukünftige Abgleich und die Verarbeitungskosten, um ihre Entscheidung, Daten beiseite zu legen und sie bei der nächsten Konvertierungsausführung neu zu verarbeiten, in der Hoffnung, dass sie zu einem späteren Zeitpunkt innerhalb des Retentionsfensters bereichert und miteinander abgeglichen bzw. zusammengeführt werden können, zu informieren. Dieser Zyklus dauert an, bis die Zeile ausreichend verarbeitet ist oder bis sie für eine weitere Investition als zu stabil gilt. Bei jeder Iteration werden verzögerte Daten generiert, was eine Übermenge aller verzögerten Daten in vorherigen Iterationen darstellt.

Die Adobe Experience Platform erkennt derzeit keine verzögerten Daten. Daher müssen Client-Implementierungen auf den Konfigurationen von ETL und Dataset-Handbuch zurückgreifen, um einen weiteren Datensatz in der Plattform zu erstellen, der den Quelldataset spiegelt, der zur Aufbewahrung verzögerter Daten verwendet werden kann. In diesem Fall sind verzögerte Daten ähnlich wie Snapshot-Daten. Bei jeder Ausführung der ETL-Transformation werden die Quelldaten mit verzögerten Daten verbunden und zur Verarbeitung gesendet.

## Changelog

| Datum | Aktion | Beschreibung |
| ---- | ------ | ----------- |
| 2019-01-19 | Die Eigenschaft &quot;felder&quot;wurde aus den Datensätzen entfernt | In Datasets war zuvor eine &quot;fields&quot;-Eigenschaft enthalten, die eine Kopie des Schemas enthielt. Diese Funktion sollte nicht mehr verwendet werden. Wenn die Eigenschaft &quot;fields&quot;gefunden wird, sollte sie ignoriert und stattdessen das Attribut &quot;surveillanceSchema&quot;oder &quot;schemaRef&quot;verwendet werden. |
| 2019-03-15 | Zu Datasets hinzugefügte Eigenschaft &quot;schemaRef&quot; | Die Eigenschaft &quot;schemaRef&quot;eines Datensatzes enthält einen URI, der auf das XDM-Schema verweist, auf dem der Datensatz basiert, und alle potenziellen Felder darstellt, die vom Datensatz verwendet werden könnten. |
| 2019-03-15 | Alle Endbenutzer-IDs sind der Eigenschaft &quot;identityMap&quot;zugeordnet | Die &quot;identityMap&quot;ist eine Kapselung aller eindeutigen Bezeichner eines Betreffs, wie z. B. CRM-ID, ECID oder Loyalität-Programm-ID. Diese Karte wird vom [Identitätsdienst](../identity-service/home.md) verwendet, um alle bekannten und anonymen Identitäten eines Betreffs aufzulösen und für jeden Endbenutzer ein einheitliches Identitätsdiagramm zu erstellen. |
| 2019-05-30 | EOL- und Entfernen der Eigenschaft &quot;Schema&quot;aus den Datensätzen | Die Eigenschaft &quot;Schema&quot;des Datensatzes stellte einen Verweis auf das Schema mit dem nicht mehr unterstützten `/xdms` Endpunkt in der Katalog-API bereit. Dies wurde durch einen &quot;schemaRef&quot; ersetzt, der die Optionen &quot;id&quot;, &quot;version&quot;und &quot;contentType&quot;des Schemas bereitstellt, wie in der neuen Schema-Registrierungs-API referenziert. |