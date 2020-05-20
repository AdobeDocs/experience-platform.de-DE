---
keywords: Experience Platform;home;popular topics; API tutorials; streaming destinations API; Real-time CDP
solution: Experience Platform
title: Mit Streaming-Zielen verbinden und Daten aktivieren
topic: tutorial
translation-type: tm+mt
source-git-commit: 47e03d3f58bd31b1aec45cbf268e3285dd5921ea
workflow-type: tm+mt
source-wordcount: '1861'
ht-degree: 2%

---


# Stellen Sie eine Verbindung zu Streaming-Zielen her und aktivieren Sie Daten in der Echtzeit-Kundendatenplattform von Adobe mithilfe von APIs

>[!NOTE]
>
>Die CDP-Dateien [!DNL Amazon Kinesis] und die [!DNL Azure Event Hubs] Ziele in Adobe Echtzeit sind derzeit in der Betaphase. Dokumentation und Funktionalität können sich ändern.

In diesem Lernprogramm wird gezeigt, wie Sie mithilfe von API-Aufrufen eine Verbindung zu Ihren Adobe Experience Platform-Daten herstellen, eine Verbindung zu einem Streaming Cloud-Datenspeicherung-Ziel herstellen ([Amazon Kinesis](/help/rtcdp/destinations/amazon-kinesis-destination.md) oder [Azurblauer Ereignis-Hubs](/help/rtcdp/destinations/azure-event-hubs-destination.md)), einen Datenfluss zu Ihrem neu erstellten Ziel erstellen und Daten an Ihr neu erstelltes Ziel aktivieren können.

Dieses Lernprogramm verwendet das [!DNL Amazon Kinesis] Ziel in allen Beispielen, aber die Schritte sind für [!DNL Azure Event Hubs]identisch.

![Übersicht - Schritte zum Erstellen eines Streaming-Ziels und Aktivieren von Segmenten](/help/rtcdp/destinations/assets/flow-prelim.png)

Wenn Sie die Benutzeroberfläche in der Echtzeit-CDP von Adobe verwenden möchten, um eine Verbindung zu einem Ziel herzustellen und Daten zu aktivieren, finden Sie weitere Informationen unter [Verbinden eines Ziels](../../rtcdp/destinations/connect-destination.md) und [Aktivieren von Profilen und Segmenten mit einem Ziel](../../rtcdp/destinations/activate-destinations.md) -Lernprogramm.

## Erste Schritte

Dieses Handbuch erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

* [Erlebnis-Datenmodell (XDM)-System](../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
* [Katalogdienst](../../catalog/home.md): Catalog ist das Datensatzsystem für die Datenposition und -linie in der Experience Platform.
* [Sandboxen](../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Plattforminstanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie zur Aktivierung von Daten an Streaming-Ziele in Adobe Echtzeit-CDP kennen müssen.

### Erforderliche Berechtigungen erfassen

Um die Schritte in diesem Lernprogramm abzuschließen, sollten Sie die folgenden Anmeldeinformationen entsprechend der Art der Ziele, mit denen Sie Segmente verbinden und aktivieren, bereitstellen.

* Für [!DNL Amazon Kinesis] Verbindungen: `accessKeyId`, `secretKey`oder `region` oder `connectionUrl`
* Für [!DNL Azure Event Hubs] Verbindungen: `sasKeyName`, `sasKey`, `namespace`

### Lesen von Beispiel-API-Aufrufen {#reading-sample-api-calls}

In diesem Lernprogramm finden Sie Beispiele für API-Aufrufe, die zeigen, wie Sie Ihre Anforderungen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anforderungs-Nutzdaten. Beispiel-JSON, die in API-Antworten zurückgegeben wird, wird ebenfalls bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für Experience Platform.

### Werte für erforderliche und optionale Überschriften sammeln {#gather-values}

Um Aufrufe an Plattform-APIs durchzuführen, müssen Sie zunächst das [Authentifizierungstraining](/help/tutorials/authentication.md)abschließen. Das Abschließen des Authentifizierungstreutorials stellt die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform API-Aufrufen bereit, wie unten dargestellt:

* Genehmigung: Träger `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Ressourcen in Experience Platform können zu bestimmten virtuellen Sandboxen isoliert werden. Bei Anforderungen an Plattform-APIs können Sie den Namen und die ID der Sandbox angeben, in der der Vorgang ausgeführt wird. Dies sind optionale Parameter.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!Note]
>Weitere Informationen zu Sandboxes in Experience Platform finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Für alle Anforderungen, die eine Payload enthalten (POST, PUT, PATCH), ist ein zusätzlicher Medientyp-Header erforderlich:

* Content-Type: `application/json`

### Swagger-Dokumentation {#swagger-docs}

Die zugehörige Referenzdokumentation für alle API-Aufrufe finden Sie in diesem Tutorial in Swagger. Siehe https://platform.adobe.io/data/foundation/flowservice/swagger#/. Es wird empfohlen, dieses Tutorial und die Seite Swagger-Dokumentation parallel zu verwenden.

## Liste der verfügbaren Streaming-Ziele {#get-the-list-of-available-streaming-destinations}

![Übersichtsschritt zu den Zielschritten 1](/help/rtcdp/destinations/assets/step1-create-streaming-destination-api.png)

Als ersten Schritt sollten Sie entscheiden, in welchem Streaming-Ziel Daten aktiviert werden sollen. Zunächst führen Sie einen Aufruf durch, um eine Liste der verfügbaren Ziele anzufordern, mit denen Sie eine Verbindung herstellen und Segmente aktivieren können. Führen Sie die folgende GET-Anforderung an den `connectionSpecs` Endpunkt aus, um eine Liste der verfügbaren Ziele zurückzugeben:

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

Eine erfolgreiche Antwort enthält eine Liste der verfügbaren Ziele und ihrer eindeutigen Bezeichner (`id`). Speichern Sie den Wert des Ziels, das Sie verwenden möchten, wie in weiteren Schritten erforderlich. Wenn Sie z. B. eine Verbindung herstellen und Segmente bereitstellen möchten [!DNL Amazon Kinesis] oder [!DNL Azure Event Hubs], suchen Sie in der Antwort nach folgendem Codefragment:

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

## Verbindung zu den Daten Ihrer Experience Platform {#connect-to-your-experience-platform-data}

![Übersichtsschritt zu den Zielschritten 2](/help/rtcdp/destinations/assets/step2-create-streaming-destination-api.png)

Als Nächstes müssen Sie eine Verbindung zu Ihren Experience Platform-Daten herstellen, damit Sie Profil-Daten exportieren und sie in Ihrem bevorzugten Ziel aktivieren können. Diese besteht aus zwei Unterteilen, die nachfolgend beschrieben werden.

1. Zunächst müssen Sie einen Aufruf ausführen, um den Zugriff auf Ihre Daten in Experience Platform zu autorisieren, indem Sie eine Basisverbindung einrichten.
2. Anschließend führen Sie mit der Basis-Verbindungs-ID einen weiteren Aufruf durch, bei dem Sie eine Quellverbindung erstellen, die die Verbindung zu Ihren Experience Platform-Daten herstellt.


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

Eine erfolgreiche Antwort enthält die eindeutige Kennung der Basisverbindung (`id`). Speichern Sie diesen Wert so, wie er im nächsten Schritt zum Erstellen der Quellverbindung erforderlich ist.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Verbindung zu den Daten Ihrer Experience Platform

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

* `{BASE_CONNECTION_ID}`: Verwenden Sie die ID, die Sie im vorherigen Schritt erhalten haben.
* `{CONNECTION_SPEC_ID}`: Verwenden Sie die Verbindungsspezifikations-ID für Unified Profil Service - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung (`id`) für die neu erstellte Quellverbindung zum Unified Profil Service zurück. Dadurch wird bestätigt, dass Sie erfolgreich eine Verbindung zu Ihren Experience Platform-Daten hergestellt haben. Speichern Sie diesen Wert so, wie er in einem späteren Schritt erforderlich ist.

```json
{
    "id": "ed48ae9b-c774-4b6e-88ae-9bc7748b6e97"
}
```


## Connect to streaming destination {#connect-to-streaming-destination}

![Übersichtsschritt zu den Zielschritten 3](/help/rtcdp/destinations/assets/step3-create-streaming-destination-api.png)

In diesem Schritt richten Sie eine Verbindung zu Ihrem gewünschten Streaming-Ziel ein. Diese besteht aus zwei Unterteilen, die nachfolgend beschrieben werden.

1. Zunächst müssen Sie einen Aufruf ausführen, um den Zugriff auf das Streaming-Ziel zu autorisieren, indem Sie eine Basisverbindung einrichten.
2. Mithilfe der Basis-Verbindungs-ID führen Sie dann einen weiteren Aufruf durch, bei dem Sie eine Zielgruppe erstellen, die den Speicherort in Ihrem Datenspeicherung-Konto, an dem die exportierten Daten bereitgestellt werden, sowie das Format der zu exportierenden Daten angibt.

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

* `{CONNECTION_SPEC_ID}`: Verwenden Sie die Verbindungsspezifikations-ID, die Sie im Schritt [Liste der verfügbaren Ziele](#get-the-list-of-available-destinations)erhalten haben.
* `{AUTHENTICATION_CREDENTIALS}`: Geben Sie den Namen Ihres Streaming-Ziels ein, z. B.: `Amazon Kinesis authentication credentials` oder `Azure Event Hubs authentication credentials`.
* `{ACCESS_ID}`: *Für Amazon-Kinesis-Verbindungen.* Ihre Zugriffs-ID für Ihren Amazon Kinesis Datenspeicherung-Speicherort.
* `{SECRET_KEY}`: *Für Amazon-Kinesis-Verbindungen.* Ihr geheimer Schlüssel für Ihre Amazon Kinesis Datenspeicherung.
* `{REGION}`: *Für Amazon-Kinesis-Verbindungen.* Die Region in Ihrem Amazon Kinesis-Konto, in der Adobe Echtzeit-CDP Ihre Daten streamen wird.
* `{SAS_KEY_NAME}`: *Für das Ereignis sind Verbindungen möglich.* Geben Sie den Namen Ihres SAS-Schlüssels ein. Informationen zur Authentifizierung mit [!DNL Azure Event Hubs] SAS-Schlüsseln finden Sie in der [Microsoft-Dokumentation](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* `{SAS_KEY}`: *Für das Ereignis sind Verbindungen möglich.* Geben Sie Ihren SAS-Schlüssel ein. Informationen zur Authentifizierung mit [!DNL Azure Event Hubs] SAS-Schlüsseln finden Sie in der [Microsoft-Dokumentation](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* `{EVENT_HUB_NAMESPACE}`: *Für das Ereignis sind Verbindungen möglich.* Füllen Sie den Namensraum der Azurblauen Ereignis Hubs aus, in dem Adobe Echtzeit-CDP Ihre Daten streamen wird. Weitere Informationen finden Sie unter Ereignis-Hubs-Namensraum [](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace) erstellen in der Microsoft-Dokumentation.

**Antwort**

Eine erfolgreiche Antwort enthält die eindeutige Kennung der Basisverbindung (`id`). Speichern Sie diesen Wert so, wie er im nächsten Schritt erforderlich ist, um eine Zielgruppe-Verbindung zu erstellen.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Speicherort und Datenformat der Datenspeicherung angeben

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
        "eventHubName": "{EVENT_HUB_NAME}",
        "namespace": "EVENT_HUB_NAMESPACE"
    }
}'
```

* `{BASE_CONNECTION_ID}`: Verwenden Sie die Basis-Verbindungs-ID, die Sie im obigen Schritt erhalten haben.
* `{CONNECTION_SPEC_ID}`: Verwenden Sie die Verbindungsspezifikation, die Sie im Schritt erhalten haben [Sie die Liste der verfügbaren Ziele](#get-the-list-of-available-destinations).
* `{NAME_OF_DATA_STREAM}`: *Für Amazon-Kinesis-Verbindungen.* Geben Sie den Namen Ihres vorhandenen Datenstroms in Ihrem Amazon Kinesis-Konto ein. Adobe Echtzeit-CDP exportiert Daten in diesen Stream.
* `{REGION}`: *Für Amazon-Kinesis-Verbindungen.* Die Region in Ihrem Amazon Kinesis-Konto, in der Adobe Echtzeit-CDP Ihre Daten streamen wird.
* `{EVENT_HUB_NAME}`: *Für das Ereignis sind Verbindungen möglich.* Füllen Sie den Azurblauen Ereignis Hub-Namen aus, unter dem Adobe Echtzeit-CDP Ihre Daten streamen wird. Weitere Informationen finden Sie unter Ereignis-Hub [](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub) erstellen in der Microsoft-Dokumentation.
* `{EVENT_HUB_NAMESPACE}`: *Für das Ereignis sind Verbindungen möglich.* Füllen Sie den Namensraum der Azurblauen Ereignis Hubs aus, in dem Adobe Echtzeit-CDP Ihre Daten streamen wird. Weitere Informationen finden Sie unter Ereignis-Hubs-Namensraum [](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace) erstellen in der Microsoft-Dokumentation.

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung (`id`) für die neu erstellte Zielgruppe-Verbindung mit Ihrem Streaming-Ziel zurück. Speichern Sie diesen Wert so, wie er in späteren Schritten erforderlich ist.

```json
{
    "id": "12ab90c7-519c-4291-bd20-d64186b62da8"
}
```

## Datenfluss erstellen

![Übersichtsschritt zu den Zielschritten 4](/help/rtcdp/destinations/assets/step4-create-streaming-destination-api.png)

Mithilfe der IDs, die Sie in den vorherigen Schritten erhalten haben, können Sie jetzt einen Datenflug zwischen Ihren Experience Platform-Daten und dem Ziel erstellen, an das Sie Daten aktivieren möchten. Stellen Sie sich diesen Schritt als eine Konstruktion der Pipeline vor, durch die Daten später zwischen der Experience Platform und dem gewünschten Ziel fließen.

Um einen Datenflug zu erstellen, führen Sie eine POST-Anforderung wie unten dargestellt durch und geben Sie dabei die unten genannten Werte innerhalb der Nutzlast ein.

Führen Sie die folgende POST-Anforderung aus, um einen Datenflug zu erstellen.

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

* `{FLOW_SPEC_ID}`: Verwenden Sie den Fluss für das Streaming-Ziel, mit dem Sie eine Verbindung herstellen möchten. Um die Flussspezifikation abzurufen, führen Sie einen GET-Vorgang am `flowspecs` Endpunkt durch. Weitere Informationen finden Sie in der Swagger-Dokumentation: https://platform.adobe.io/data/foundation/flowservice/swagger#/Flow%20Specs%20API/getFlowSpecs. Suchen `upsTo` und kopieren Sie in der Antwort die entsprechende ID des Streaming-Ziels, mit dem Sie eine Verbindung herstellen möchten.
* `{SOURCE_CONNECTION_ID}`: Verwenden Sie die Quell-Verbindungs-ID, die Sie im Schritt [Verbindung zu Ihrer Experience Platform](#connect-to-your-experience-platform-data)herstellen erhalten haben.
* `{TARGET_CONNECTION_ID}`: Verwenden Sie die Zielgruppe-Verbindungs-ID, die Sie im Schritt [Verbinden mit Streaming-Ziel](#connect-to-streaming-destination)erhalten haben.

**Antwort**

Bei einer erfolgreichen Antwort werden die ID (`id`) des neu erstellten Datenflusses und eine `etag`zurückgegeben. Beachten Sie beide Werte. wie im nächsten Schritt beschrieben, um Segmente zu aktivieren.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```


## Aktivieren von Daten an Ihrem neuen Ziel

![Übersichtsschritt zu den Zielschritten 5](/help/rtcdp/destinations/assets/step5-create-streaming-destination-api.png)

Nachdem Sie alle Verbindungen und den Datenfluss erstellt haben, können Sie jetzt Ihre Profil-Daten auf die Streaming-Plattform aktivieren. In diesem Schritt wählen Sie aus, welche Segmente und welche Profil-Attribute Sie an das Ziel senden, und Sie können Daten planen und an das Ziel senden.

Um Segmente an Ihrem neuen Ziel zu aktivieren, müssen Sie einen JSON-PATCH-Vorgang ausführen, ähnlich dem Beispiel unten. Sie können mehrere Profil- und Segmentattribute in einem Aufruf aktivieren. Weitere Informationen zu JSON PATCH finden Sie in der [RFC-Spezifikation](https://tools.ietf.org/html/rfc6902).

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
    }
]
```

* `{DATAFLOW_ID}`: Verwenden Sie den Datenfluss, den Sie im vorherigen Schritt erhalten haben.
* `{ETAG}`: Verwenden Sie das Tag, das Sie im vorherigen Schritt erhalten haben.
* `{SEGMENT_ID}`: Geben Sie die Segment-ID an, die Sie an dieses Ziel exportieren möchten. Um Segment-IDs für die Segmente abzurufen, die Sie aktivieren möchten, gehen Sie zu https://www.adobe.io/apis/experienceplatform/home/api-reference.html#/, wählen Sie im linken Navigationsmenü die Option **Segmentierungsdienst-API** und suchen Sie nach dem `GET /segment/jobs` Vorgang.
* `{PROFILE_ATTRIBUTE}`: Beispiel, `"person.lastName"`

**Antwort**

Suchen Sie nach einer OK-Antwort für 202. Es wird kein Antwortkörper zurückgegeben. Um zu überprüfen, ob die Anforderung korrekt war, lesen Sie den nächsten Schritt Validieren des Datenflusses.

## Datenfluss überprüfen

![Übersichtsschritt zu den Zielschritten 6](/help/rtcdp/destinations/assets/step6-create-streaming-destination-api.png)

Als letzten Schritt im Lernprogramm sollten Sie überprüfen, ob die Segmente und Profil-Attribute dem Datenfluss korrekt zugeordnet wurden.

Führen Sie zur Validierung dieser Funktion die folgende GET-Anforderung aus:

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
* `{ETAG}`: Verwenden Sie das Tag aus dem vorherigen Schritt.

**Antwort**

Die zurückgegebene Antwort sollte die Segmente und Profil-Attribute, die Sie im vorherigen Schritt gesendet haben, in den `transformations` Parameter aufnehmen. Ein Beispielparameter `transformations` in der Antwort könnte wie folgt aussehen:

```
"transformations": [
    {
        "name": "GeneralTransform",
        "params": {
            "profileSelectors": {
                "selectors": []
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

## Nächste Schritte

In diesem Lernprogramm haben Sie CDP in Echtzeit erfolgreich mit einem Ihrer bevorzugten Streaming-Ziele verbunden und einen Datenfluss zum entsprechenden Ziel eingerichtet. Ausgehende Daten können jetzt im Ziel für Kundenanalysen oder andere Datenoperationen verwendet werden, die Sie durchführen möchten. Weitere Informationen finden Sie auf den folgenden Seiten:

* [Ziele – Übersicht](../../rtcdp/destinations/destinations-overview.md)
* [Zielkatalog - Übersicht](../../rtcdp/destinations/destinations-catalog.md)