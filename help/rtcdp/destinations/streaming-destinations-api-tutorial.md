---
keywords: Experience Platform;home;popular topics; API tutorials; streaming destinations API; Real-time CDP
solution: Experience Platform
title: Mit Streaming-Zielen verbinden und Daten aktivieren
topic: tutorial
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '1810'
ht-degree: 61%

---


# Stellen Sie eine Verbindung zu Streaming-Zielen her und aktivieren Sie Daten in der Echtzeit-Kundendatenplattform von Adobe mithilfe von APIs

>[!NOTE]
>
>Die CDP-Dateien [!DNL Amazon Kinesis] und die [!DNL Azure Event Hubs] Ziele in Adobe Echtzeit sind derzeit in der Betaphase. Dokumentation und Funktionalität können sich ändern.

Dieses Lernprogramm zeigt, wie Sie mit API-Aufrufen eine Verbindung zu Ihren Adobe Experience Platformen herstellen, eine Verbindung zu einem Streaming Cloud-Datenspeicherung-Ziel herstellen ([Amazon Kinesis](/help/rtcdp/destinations/amazon-kinesis-destination.md) oder [Azurblauer Ereignis-Hubs](/help/rtcdp/destinations/azure-event-hubs-destination.md)), einen Datenfluss zu Ihrem neu erstellten Ziel erstellen und Daten zu Ihrem neu erstellten Ziel aktivieren können.

Dieses Lernprogramm verwendet das [!DNL Amazon Kinesis] Ziel in allen Beispielen, aber die Schritte sind für [!DNL Azure Event Hubs]identisch.

![Übersicht - Schritte zum Erstellen eines Streaming-Ziels und Aktivieren von Segmenten](/help/rtcdp/destinations/assets/flow-prelim.png)

If you prefer to use the user interface in Adobe&#39;s Real-time CDP to connect to a destination and activate data, see the [Connect a destination](../../rtcdp/destinations/connect-destination.md) and [Activate profiles and segments to a destination](../../rtcdp/destinations/activate-destinations.md) tutorials.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [!DNL Experience Data Model (XDM) System](../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
* [!DNL Catalog Service](../../catalog/home.md): [!DNL Catalog] ist das Datensatzsystem für die Datenposition und -linie innerhalb der Experience Platform.
* [Sandbox-Umgebungen](../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen für die Entwicklung und Erweiterung von Anwendungen für digitale Erlebnisse unterteilen.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie zur Aktivierung von Daten an Streaming-Ziele in Adobe Echtzeit-CDP kennen müssen.

### Erforderliche Anmeldedaten sammeln

Um die Schritte in dieser Anleitung abzuschließen, benötigen Sie die folgenden Anmeldedaten, je nach Art der Ziele, mit denen Sie Segmente verbinden und aktivieren möchten.

* Für [!DNL Amazon Kinesis] Verbindungen: `accessKeyId`, `secretKey`oder `region` oder `connectionUrl`
* Für [!DNL Azure Event Hubs] Verbindungen: `sasKeyName`, `sasKey`, `namespace`

### Lesehilfe für Beispiel-API-Aufrufe {#reading-sample-api-calls}

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dabei wird auf Pfade ebenso eingegangen wie auf die erforderlichen Kopfzeilen und die für Anfrage-Payloads zu verwendende Formatierung. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für Experience Platform.

### Werte für erforderliche und optionale Kopfzeilen sammeln {#gather-values}

Machen Sie sich über das [Tutorial zur Authentifizierung](/help/tutorials/authentication.md) zunächst damit vertraut, wie Sie Aufrufe auf Platform-APIs ausführen. Im Rahmen des Tutorials zur Authentifizierung werden die für Aufrufe an alle Experience Platform-APIs zu verwendenden Werte im Einzelnen erläutert. Dazu gehören:

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Ressourcen in Experience Platform lassen sich in spezifischen virtuellen Sandboxes isolieren. Bei Anfragen an Platform-APIs können Sie den Namen und die Kennung der Sandbox angeben, in der der Vorgang ausgeführt werden soll. Dies sind optionale Parameter.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NHinweis]
>Weiterführende Informationen zu Sandboxes in Experience Platform finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

* Content-Type: `application/json`

### Swagger-Dokumentation {#swagger-docs}

Eine zugehörige Referenzdokumentation für alle API-Aufrufe finden Sie in dieser Anleitung in Swagger. Weitere Informationen finden Sie in der Dokumentation zur [Flow Service API unter Adobe.io](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml). Es wird empfohlen, diese Anleitung sowie die Seite mit der Swagger-Dokumentation parallel zu verwenden.

## Get the list of available streaming destinations {#get-the-list-of-available-streaming-destinations}

![Übersicht über die Zielschritte – Schritt 1](/help/rtcdp/destinations/assets/step1-create-streaming-destination-api.png)

Als ersten Schritt sollten Sie entscheiden, in welchem Streaming-Ziel Daten aktiviert werden sollen. Führen Sie also zunächst einen Aufruf durch, um eine Liste der verfügbaren Ziele anzufordern, mit denen Sie eine Verbindung herstellen und Segmente aktivieren können. Führen Sie die folgende GET-Anfrage an den `connectionSpecs`-Endpunkt aus, um eine Liste der verfügbaren Ziele zu erhalten:

**API-Format**

```http
GET /connectionSpecs
```

**Anfrage**

```
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
--header 'accept: application/json' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```


**Antwort**

Eine erfolgreiche Antwort enthält eine Liste der verfügbaren Ziele und ihre eindeutigen Kennungen (`id`). Notieren Sie sich den Wert des Ziels, das Sie verwenden möchten, da Sie ihn in weiteren Schritten benötigen werden. For example, if you want to connect and deliver segments to [!DNL Amazon Kinesis] or [!DNL Azure Event Hubs], look for the following snippet in the response:

```json
{
    "id": "86043421-563b-46ec-8e6c-e23184711bf6",
  "name": "Amazon Kinesis",
  ...
  ...
}

{
    "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
  "name": "Azure Event Hubs",
  ...
  ...
}
```

## Verbindung zu Ihren Experience Platform-Daten herstellen {#connect-to-your-experience-platform-data}

![Übersicht über die Zielschritte – Schritt 2](/help/rtcdp/destinations/assets/step2-create-streaming-destination-api.png)

Als Nächstes müssen Sie eine Verbindung zu Ihren Experience Platform-Daten herstellen, um Profildaten exportieren und in Ihrem bevorzugten Ziel aktivieren zu können. Das umfasst zwei Unterschritte, die nachfolgend beschrieben werden.

1. Sie müssen zunächst einen Aufruf ausführen, um den Zugriff auf Ihre Daten in Experience Platform zu autorisieren, indem Sie eine Basisverbindung einrichten.
2. Anschließend führen Sie mit der Kennung der Basisverbindung einen weiteren Aufruf aus, mit dem Sie eine Quellverbindung einrichten, die die Verbindung zu Ihren Experience Platform-Daten herstellt.


### Zugriff auf Ihre Daten in Experience Platform genehmigen

**API-Format**

```http
POST /connections
```

**Anfrage**

```
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME} \
--header 'Content-Type: application/json' \
--data-raw '{
            "name": "Base connection to Experience Platform",
            "description": "This call establishes the connection to Experience Platform data",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC_ID}",
                "version": "1.0"
            }
}'
```


* `{CONNECTION_SPEC_ID}`: Verwenden Sie die Verbindungsspezifikations-ID für Unified Profil Service - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**Antwort**

Eine erfolgreiche Antwort enthält die eindeutige Kennung der Basisverbindung (`id`). Notieren Sie sich diesen Wert, da Sie ihn im nächsten Schritt zum Erstellen der Quellverbindung benötigen werden.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Verbindung zu Ihren Experience Platform-Daten herstellen

**API-Format**

```http
POST /sourceConnections
```

**Anfrage**

```
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
            "name": "Connecting to Unified Profile Service",
            "description": "Optional",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC_ID}",
                "version": "1.0"
            },
            "baseConnectionId": "{BASE_CONNECTION_ID}",
            "data": {
                "format": "json"
            },
            "params" : {}
}'
```

* `{BASE_CONNECTION_ID}`: Verwenden Sie die Kennung, die Sie im vorherigen Schritt erhalten haben.
* `{CONNECTION_SPEC_ID}`: Verwenden Sie die Verbindungsspezifikations-ID für Unified Profil Service - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung (`id`) für die neu erstellte Quellverbindung zu Unified Profile Service zurück. Dadurch wird bestätigt, dass Sie erfolgreich eine Verbindung zu Ihren Experience Platform-Daten hergestellt haben. Notieren Sie sich diesen Wert, da Sie ihn in einem späteren Schritt benötigen werden.

```json
{
    "id": "ed48ae9b-c774-4b6e-88ae-9bc7748b6e97"
}
```


## Connect to streaming destination {#connect-to-streaming-destination}

![Übersicht über die Zielschritte – Schritt 3](/help/rtcdp/destinations/assets/step3-create-streaming-destination-api.png)

In diesem Schritt richten Sie eine Verbindung zu Ihrem gewünschten Streaming-Ziel ein. Das umfasst zwei Unterschritte, die nachfolgend beschrieben werden.

1. Zunächst müssen Sie einen Aufruf ausführen, um den Zugriff auf das Streaming-Ziel zu autorisieren, indem Sie eine Basisverbindung einrichten.
2. Mithilfe der Kennung der Basisverbindung führen Sie dann einen weiteren Aufruf aus, mit dem Sie eine Zielverbindung erstellen. In dem Aufruf sind der Ort in Ihrem Speicherkonto, an dem die exportierten Daten bereitgestellt werden, sowie das Format der zu exportierenden Daten angegeben.

### Zugriff auf das Streaming-Ziel genehmigen

**API-Format**

```http
POST /connections
```

**Anfrage**

```
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connection for Amazon Kinesis/ Azure Event Hubs",
    "description": "your company's holiday campaign",
    "connectionSpec": {
        "id": "{_CONNECTION_SPEC_ID}",
        "version": "1.0"
    },
    "auth": {
        "specName": "{AUTHENTICATION_CREDENTIALS}",
        "params": { // use these values for Amazon Kinesis connections
            "accessKeyId": "{ACCESS_ID}",
            "secretKey": "{SECRET_KEY}",
            "region": "{REGION}"
        },
        "params": { // use these values for Azure Event Hubs connections
            "sasKeyName": "{SAS_KEY_NAME}",
            "sasKey": "{SAS_KEY}",
            "namespace": "{EVENT_HUB_NAMESPACE}"
        }        
    }
}'
```

* `{CONNECTION_SPEC_ID}`: Verwenden Sie die Verbindungsspezifikations-ID, die Sie im Schritt [Liste der verfügbaren Ziele anfordern](#get-the-list-of-available-destinations) erhalten haben.
* `{AUTHENTICATION_CREDENTIALS}`: Geben Sie den Namen Ihres Streaming-Ziels ein, z. B.: `Amazon Kinesis authentication credentials` oder `Azure Event Hubs authentication credentials`.
* `{ACCESS_ID}`: *Für[!DNL Amazon Kinesis]Verbindungen.* Ihre Zugriffs-ID für Ihren Amazon Kinesis Datenspeicherung-Speicherort.
* `{SECRET_KEY}`: *Für[!DNL Amazon Kinesis]Verbindungen.* Ihr geheimer Schlüssel für Ihre Amazon Kinesis Datenspeicherung.
* `{REGION}`: *Für[!DNL Amazon Kinesis]Verbindungen.* Die Region in Ihrem [!DNL Amazon Kinesis] Konto, in der Adobe Echtzeit-CDP Ihre Daten streamen wird.
* `{SAS_KEY_NAME}`: *Für[!DNL Azure Event Hubs]Verbindungen.* Geben Sie den Namen Ihres SAS-Schlüssels ein. Informationen zur Authentifizierung mit [!DNL Azure Event Hubs] SAS-Schlüsseln finden Sie in der [Microsoft-Dokumentation](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* `{SAS_KEY}`: *Für[!DNL Azure Event Hubs]Verbindungen.* Geben Sie Ihren SAS-Schlüssel ein. Informationen zur Authentifizierung mit [!DNL Azure Event Hubs] SAS-Schlüsseln finden Sie in der [Microsoft-Dokumentation](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* `{EVENT_HUB_NAMESPACE}`: *Für[!DNL Azure Event Hubs]Verbindungen.* Geben Sie den [!DNL Azure Event Hubs] Namensraum ein, in dem Adobe Echtzeit-CDP Ihre Daten streamen soll. Weitere Informationen finden Sie unter Ereignis-Hubs-Namensraum [](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace) erstellen in der [!DNL Microsoft] Dokumentation.

**Antwort**

Eine erfolgreiche Antwort enthält die eindeutige Kennung der Basisverbindung (`id`). Notieren Sie sich diesen Wert, da Sie ihn im nächsten Schritt benötigen, um eine Zielverbindung zu erstellen.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Speicherort und Datenformat angeben

**API-Format**

```http
POST /targetConnections
```

**Anfrage**

```
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Amazon Kinesis/ Azure Event Hubs target connection",
    "description": "Connection to Amazon Kinesis/ Azure Event Hubs",
    "baseConnection": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "{CONNECTION_SPEC_ID}",
        "version": "1.0"
    },
    "data": {
        "format": "json",
    },
    "params": { // use these values for Amazon Kinesis connections
        "stream": "{NAME_OF_DATA_STREAM}", 
        "region": "{REGION}"
    },
    "params": { // use these values for Azure Event Hubs connections
        "eventHubName": "{EVENT_HUB_NAME}"
    }
}'
```

* `{BASE_CONNECTION_ID}`: Nutzen Sie die Kennung der Basisverbindung, die Sie im obigen Schritt erhalten haben.
* `{CONNECTION_SPEC_ID}`: Verwenden Sie die Verbindungsspezifikation, die Sie im Schritt [Liste der verfügbaren Ziele abrufen](#get-the-list-of-available-destinations) erhalten haben.
* `{NAME_OF_DATA_STREAM}`: *Für[!DNL Amazon Kinesis]Verbindungen.* Geben Sie den Namen Ihres vorhandenen Datenstroms in Ihrem [!DNL Amazon Kinesis] Konto an. Adobe Echtzeit-CDP exportiert Daten in diesen Stream.
* `{REGION}`: *Für[!DNL Amazon Kinesis]Verbindungen.* Die Region in Ihrem Amazon Kinesis-Konto, in der Adobe Echtzeit-CDP Ihre Daten streamen wird.
* `{EVENT_HUB_NAME}`: *Für[!DNL Azure Event Hubs]Verbindungen.* Geben Sie den [!DNL Azure Event Hub] Namen ein, unter dem Adobe Echtzeit-CDP Ihre Daten streamen soll. Weitere Informationen finden Sie unter Ereignis-Hub [](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub) erstellen in der [!DNL Microsoft] Dokumentation.

**Antwort**

A successful response returns the unique identifier (`id`) for the newly created target connection to your streaming destination. Notieren Sie sich diesen Wert, da Sie ihn in späteren Schritten benötigen werden.

```json
{
    "id": "12ab90c7-519c-4291-bd20-d64186b62da8"
}
```

## Datenfluss erstellen

![Übersicht über die Zielschritte – Schritt 4](/help/rtcdp/destinations/assets/step4-create-streaming-destination-api.png)

Mithilfe der Kennungen, die Sie in den vorherigen Schritten erhalten haben, können Sie jetzt einen Datenfluss zwischen Ihren Experience Platform-Daten und dem Ziel erstellen, für das Sie Daten aktivieren möchten. Stellen Sie sich diesen Schritt als Bau einer Pipeline vor, durch die später Daten zwischen Experience Platform und dem gewünschten Ziel fließen werden.

Um einen Datenfluss zu erstellen, führen Sie eine POST-Anfrage durch (wie unten dargestellt) und geben Sie dabei die unten genannten Werte in der Payload an.

Führen Sie die folgende POST-Anfrage aus, um einen Datenfluss zu erstellen.

**API-Format**

```http
POST /flows
```

**Anfrage**

```shell
curl -X POST \
'https://platform.adobe.io/data/foundation/flowservice/flows' \
-H 'Authorization: Bearer {ACCESS_TOKEN}' \
-H 'x-api-key: {API_KEY}' \
-H 'x-gw-ims-org-id: {IMS_ORG}' \
-H 'x-sandbox-name: {SANDBOX_NAME}' \
-H 'Content-Type: application/json' \
-d  '{
   
        "name": "Create dataflow to Amazon Kinesis/ Azure Event Hubs",
        "description": "This operation creates a dataflow to Amazon Kinesis/ Azure Event Hubs",
        "flowSpec": {
            "id": "{FLOW_SPEC_ID}",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "{SOURCE_CONNECTION_ID}"
        ],
        "targetConnectionIds": [
            "{TARGET_CONNECTION_ID}"
        ]
    }
```

* `{FLOW_SPEC_ID}`: Die Flussspec-ID für Profil-basierte Ziele lautet `71471eba-b620-49e4-90fd-23f1fa0174d8`. Verwenden Sie diesen Wert im Aufruf.
* `{SOURCE_CONNECTION_ID}`: Verwenden Sie die Quellverbindungs-ID, die Sie im Schritt [Verbindung zu Ihren Experience Platform-Daten herstellen](#connect-to-your-experience-platform-data) erhalten haben.
* `{TARGET_CONNECTION_ID}`: Verwenden Sie die Zielgruppe-Verbindungs-ID, die Sie im Schritt [Verbinden mit Streaming-Ziel](#connect-to-streaming-destination)erhalten haben.

**Antwort**

Bei einer erfolgreichen Antwort werden die Kennung (`id`) des neu erstellten Datenflusses und ein `etag` zurückgegeben. Notieren Sie sich beide Werte. Sie werden sie im nächsten Schritt benötigen, um Segmente zu aktivieren.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```


## Daten an Ihr neues Ziel aktivieren {#activate-data}

![Übersicht über die Zielschritte – Schritt 5](/help/rtcdp/destinations/assets/step5-create-streaming-destination-api.png)

Nachdem Sie alle Verbindungen und den Datenfluss erstellt haben, können Sie jetzt Ihre Profil-Daten auf die Streaming-Plattform aktivieren. In diesem Schritt wählen Sie aus, welche Segmente und Profilattribute Sie an das Ziel senden möchten. Außerdem können Sie Daten planen und an das Ziel senden.

Um Segmente für Ihr neues Ziel zu aktivieren, müssen Sie einen JSON-PATCH-Vorgang ausführen, ähnlich dem Beispiel unten. Sie können mehrere Profil- und Segmentattribute in einem Aufruf aktivieren. Weiterführende Informationen zu JSON PATCH finden Sie in der [RFC-Spezifikation](https://tools.ietf.org/html/rfc6902).

**API-Format**

```http
PATCH /flows
```

**Anfrage**

```
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'If-Match: "{ETAG}"' \
--data-raw '[
    {
        "op": "add",
        "path": "/transformations/0/params/segmentSelectors/selectors/-",
        "value": {
            "type": "PLATFORM_SEGMENT",
            "value": {
                "name": "Name of the segment that you are activating",
                "description": "Description of the segment that you are activating",
                "id": "{SEGMENT_ID}"
            }
        }
    },
        {
        "op": "add",
        "path": "/transformations/0/params/segmentSelectors/selectors/-",
        "value": {
            "type": "PLATFORM_SEGMENT",
            "value": {
                "name": "Name of the segment that you are activating",
                "description": "Description of the segment that you are activating",
                "id": "{SEGMENT_ID}"
            }
        }
    },
        {
        "op": "add",
        "path": "/transformations/0/params/profileSelectors/selectors/-",
        "value": {
            "type": "JSON_PATH",
            "value": {
                "operator": "EXISTS",
                "path": "{PROFILE_ATTRIBUTE}"
            }
        }
    },
        },
        {
        "op": "add",
        "path": "/transformations/0/params/profileSelectors/selectors/-",
        "value": {
            "type": "JSON_PATH",
            "value": {
                "operator": "EXISTS",
                "path": "{PROFILE_ATTRIBUTE}"
            }
        }
    }
]
```

* `{DATAFLOW_ID}`: Verwenden Sie den Datenfluss, den Sie im vorherigen Schritt erstellt haben.
* `{ETAG}`: Verwenden Sie das eTag, das Sie im vorherigen Schritt erhalten haben.
* `{SEGMENT_ID}`: Geben Sie die Kennung des Segments an, das Sie an dieses Ziel exportieren möchten. Um Segment-IDs für die Segmente abzurufen, die Sie aktivieren möchten, gehen Sie zu https://www.adobe.io/apis/experienceplatform/home/api-reference.html#/, wählen Sie im linken Navigationsmenü die Option **[!UICONTROL Segmentierungsdienst-API]** und suchen Sie nach dem `GET /segment/jobs` Vorgang.
* `{PROFILE_ATTRIBUTE}`: Beispiel: `personalEmail.address` oder `person.lastName`

**Antwort**

Suchen Sie nach einer „202 OK“-Antwort. Es wird kein Antworttext zurückgegeben. Um zu überprüfen, ob die Anfrage korrekt war, lesen Sie den nächsten Schritt „Datenfluss validieren“.

## Datenfluss validieren

![Übersicht über die Zielschritte – Schritt 6](/help/rtcdp/destinations/assets/step6-create-streaming-destination-api.png)

Als letzten Schritt in der Anleitung sollten Sie überprüfen, ob die Segmente und Profilattribute dem Datenfluss korrekt zugeordnet wurden.

Führen Sie zur Validierung die folgende GET-Anfrage aus:

**API-Format**

```http
GET /flows
```

**Anfrage**

```
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--header 'x-sandbox-name: prod' \
--header 'If-Match: "{ETAG}"' 
```

* `{DATAFLOW_ID}`: Verwenden Sie den Datenfluss aus dem vorherigen Schritt.
* `{ETAG}`: Verwenden Sie das eTag aus dem vorherigen Schritt.

**Antwort**

Die zurückgegebene Antwort sollte im `transformations`-Parameter die Segmente und Profilattribute enthalten, die Sie im vorherigen Schritt gesendet haben. Ein Beispielparameter `transformations` in der Antwort könnte wie folgt aussehen:

```
"transformations": [
    {
        "name": "GeneralTransform",
        "params": {
            "profileSelectors": {
                        "selectors": [
                            {
                                "type": "JSON_PATH",
                                "value": {
                                    "path": "personalEmail.address",
                                    "operator": "EXISTS"
                                }
                            },
                            {
                                "type": "JSON_PATH",
                                "value": {
                                    "path": "person.lastname",
                                    "operator": "EXISTS"
                                }
                            }
                        ]
                    },
            "segmentSelectors": {
                "selectors": [
                    {
                        "type": "PLATFORM_SEGMENT",
                        "value": {
                            "name": "Men over 50",
                            "description": "",
                            "id": "72ddd79b-6b0a-4e97-a8d2-112ccd81bd02"
                        }
                    }
                ]
            }
        }
    }
],
```

**Exportierte Daten**

>[!IMPORTANT]
>
> Zusätzlich zu den Segmenten und Segmenten im Schritt Daten an Ihr neues Ziel [aktivieren](#activate-data), werden die exportierten Daten in [!DNL AWS Kinesis] und [!DNL Azure Event Hubs] enthalten auch Informationen zur Identitätskarte. Dies stellt die Identitäten der exportierten Profil dar (z. B. [ECID](https://docs.adobe.com/content/help/de-DE/id-service/using/intro/id-request.html), mobile ID, Google-ID, E-Mail-Adresse usw.). Siehe ein Beispiel unten.

```
{
  "person": {
    "email": "yourstruly@adobe.con"
  },
  "segmentMembership": {
    "ups": {
      "72ddd79b-6b0a-4e97-a8d2-112ccd81bd02": {
        "lastQualificationTime": "2020-03-03T21:24:39Z",
        "status": "exited"
      },
      "7841ba61-23c1-4bb3-a495-00d695fe1e93": {
        "lastQualificationTime": "2020-03-04T23:37:33Z",
        "status": "existing"
      }
    }
  },
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```

## Nächste Schritte

In diesem Lernprogramm haben Sie CDP in Echtzeit erfolgreich mit einem Ihrer bevorzugten Streaming-Ziele verbunden und einen Datenfluss zum entsprechenden Ziel eingerichtet. Ausgehende Daten können jetzt im Ziel für Kundenanalysen oder andere Datenoperationen verwendet werden, die Sie durchführen möchten. Weiterführende Informationen finden Sie auf den folgenden Seiten:

* [Ziele – Übersicht](../../rtcdp/destinations/destinations-overview.md)
* [Zielkatalog – Übersicht](../../rtcdp/destinations/destinations-catalog.md)