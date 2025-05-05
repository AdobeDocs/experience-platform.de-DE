---
keywords: Experience Platform;Startseite;beliebte Themen;API-Tutorials;Streaming-Ziele-API;Experience Platform
solution: Experience Platform
title: Verbinden mit Streaming-Zielen und Aktivieren von Daten mithilfe der Flow Service-API in Adobe Experience Platform
description: In diesem Dokument wird die Erstellung von Streaming-Zielen mithilfe der Adobe Experience Platform-API behandelt
type: Tutorial
exl-id: 3e8d2745-8b83-4332-9179-a84d8c0b4400
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2219'
ht-degree: 40%

---

# Verbinden Sie sich mit Streaming-Zielen und aktivieren Sie Daten über die Flow Service-API

>[!IMPORTANT]
> 
>Um eine Verbindung mit einem Ziel herzustellen, benötigen Sie **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions).
>
>Zum Aktivieren von Daten benötigen Sie die Berechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**&#x200B;[Zugriffssteuerung](/help/access-control/home.md#permissions).
>
>Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

In diesem Tutorial erfahren Sie, wie Sie API-Aufrufe verwenden, um eine Verbindung zu Ihren Adobe Experience Platform-Daten herzustellen, eine Verbindung zu einem Streaming-Cloud-Speicher-Ziel ([Amazon Kinesis](../catalog/cloud-storage/amazon-kinesis.md) oder [Azure Event Hubs](../catalog/cloud-storage/azure-event-hubs.md)) herzustellen, einen Datenfluss zu Ihrem neu erstellten Ziel zu erstellen und Daten für Ihr neu erstelltes Ziel zu aktivieren.

In diesem Tutorial wird für alle Beispiele das [!DNL Amazon Kinesis] verwendet, die Schritte sind jedoch für [!DNL Azure Event Hubs] identisch.

![Übersicht - Schritte zum Erstellen eines Streaming-Ziels und Aktivieren von Zielgruppen](../assets/api/streaming-destination/overview.png)

Wenn Sie die Benutzeroberfläche in Experience Platform bevorzugen, um eine Verbindung zu einem Ziel herzustellen und Daten zu aktivieren, finden Sie weitere Informationen in den Tutorials [Verbinden eines Ziels](../ui/connect-destination.md) und [Aktivieren von Zielgruppendaten für Streaming-Zielgruppenexportziele](../ui/activate-segment-streaming-destinations.md) .

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten ordnet.
* [[!DNL Catalog Service]](../../catalog/home.md): [!DNL Catalog] ist das „System of Record“ für den Speicherort und die Herkunft von Daten in Experience Platform.
* [Sandboxes](../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um Daten für Streaming-Ziele in Experience Platform zu aktivieren.

### Sammeln erforderlicher Anmeldedaten

Um die Schritte in diesem Tutorial abzuschließen, sollten Sie über die folgenden Anmeldeinformationen verfügen, je nachdem, mit welchem Zieltyp Sie Zielgruppen verbinden und aktivieren.

* Für [!DNL Amazon Kinesis] Verbindungen: `accessKeyId`, `secretKey`, `region` oder `connectionUrl`
* Für [!DNL Azure Event Hubs] Verbindungen: `sasKeyName`, `sasKey`, `namespace`

### Lesen von Beispiel-API-Aufrufen {#reading-sample-api-calls}

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für Experience Platform.

### Werte für erforderliche und optionale Kopfzeilen sammeln {#gather-values}

Um Experience Platform-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abschließen. Im Rahmen des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform-API-Aufrufen bereitgestellt, wie unten dargestellt:

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Ressourcen in Experience Platform lassen sich in spezifischen virtuellen Sandboxes isolieren. Bei Anfragen an Experience Platform-APIs können Sie den Namen und die ID der Sandbox angeben, in der der Vorgang ausgeführt werden soll. Dies sind optionale Parameter.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxes in Experience Platform finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

* Content-Type: `application/json`

### Swagger-Dokumentation {#swagger-docs}

Eine zugehörige Referenzdokumentation für alle API-Aufrufe finden Sie in dieser Anleitung in Swagger. Siehe die [Flow Service-API-Dokumentation auf Adobe I/O](https://www.adobe.io/experience-platform-apis/references/flow-service/). Es wird empfohlen, diese Anleitung sowie die Seite mit der Swagger-Dokumentation parallel zu verwenden.

## Abrufen der Liste der verfügbaren Streaming-Ziele {#get-the-list-of-available-streaming-destinations}

![Übersicht über die Zielschritte – Schritt 1](../assets/api/streaming-destination/step1.png)

Als ersten Schritt sollten Sie entscheiden, für welches Streaming-Ziel Daten aktiviert werden sollen. Führen Sie zunächst einen Aufruf durch, um eine Liste der verfügbaren Ziele anzufordern, mit denen Sie Zielgruppen verbinden und aktivieren können. Führen Sie die folgende GET-Anfrage an den `connectionSpecs`-Endpunkt aus, um eine Liste der verfügbaren Ziele zu erhalten:

**API-Format**

```http
GET /connectionSpecs
```

**Anfrage**

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
--header 'accept: application/json' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```


**Antwort**

Eine erfolgreiche Antwort enthält eine Liste der verfügbaren Ziele und ihre eindeutigen Kennungen (`id`). Notieren Sie sich den Wert des Ziels, das Sie verwenden möchten, da Sie ihn in weiteren Schritten benötigen werden. Wenn Sie beispielsweise Zielgruppen mit [!DNL Amazon Kinesis] oder [!DNL Azure Event Hubs] verbinden und bereitstellen möchten, suchen Sie in der Antwort nach folgendem Code-Ausschnitt:

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

![Übersicht über die Zielschritte – Schritt 2](../assets/api/streaming-destination/step2.png)

Als Nächstes müssen Sie eine Verbindung zu Ihren Experience Platform-Daten herstellen, um Profildaten exportieren und in Ihrem bevorzugten Ziel aktivieren zu können. Das umfasst zwei Unterschritte, die nachfolgend beschrieben werden.

1. Sie müssen zunächst einen Aufruf ausführen, um den Zugriff auf Ihre Daten in Experience Platform zu autorisieren, indem Sie eine Basisverbindung einrichten.
2. Anschließend führen Sie mit der Kennung der Basisverbindung einen weiteren Aufruf aus, mit dem Sie eine Quellverbindung einrichten, die die Verbindung zu Ihren Experience Platform-Daten herstellt.


### Zugriff auf Ihre Daten in Experience Platform genehmigen

**API-Format**

```http
POST /connections
```

**Anfrage**

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
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


* `{CONNECTION_SPEC_ID}`: Verwenden Sie die Verbindungsspezifikations-ID für Profile Service - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**Antwort**

Eine erfolgreiche Antwort enthält die eindeutige Kennung der Basisverbindung (`id`). Notieren Sie sich diesen Wert, da Sie ihn im nächsten Schritt zum Erstellen der Quellverbindung benötigen werden.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Verbindung zu Ihren Experience Platform-Daten herstellen {#connect-to-platform-data}

**API-Format**

```http
POST /sourceConnections
```

**Anfrage**

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
            "name": "Connecting to Profile Service",
            "description": "Optional",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC_ID}",
                "version": "1.0"
            },
            "baseConnectionId": "{BASE_CONNECTION_ID}",
            "data": {
                "format": "json"
            },
            "params": {}
}'
```

* `{BASE_CONNECTION_ID}`: Verwenden Sie die Kennung, die Sie im vorherigen Schritt erhalten haben.
* `{CONNECTION_SPEC_ID}`: Verwenden Sie die Verbindungsspezifikations-ID für Profile Service - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**Antwort**

Bei einer erfolgreichen Antwort wird die eindeutige Kennung (`id`) für die neu erstellte Quellverbindung zum Profil-Service zurückgegeben. Dadurch wird bestätigt, dass Sie erfolgreich eine Verbindung zu Ihren Experience Platform-Daten hergestellt haben. Notieren Sie sich diesen Wert, da Sie ihn in einem späteren Schritt benötigen werden.

```json
{
    "id": "ed48ae9b-c774-4b6e-88ae-9bc7748b6e97"
}
```


## Mit Streaming-Ziel verbinden {#connect-to-streaming-destination}

![Übersicht über die Zielschritte – Schritt 3](../assets/api/streaming-destination/step3.png)

In diesem Schritt richten Sie eine Verbindung zu Ihrem gewünschten Streaming-Ziel ein. Dies umfasst zwei Unterschritte, die nachfolgend beschrieben werden.

1. Sie müssen zunächst einen Aufruf ausführen, um den Zugriff auf das Streaming-Ziel zu autorisieren, indem Sie eine Basisverbindung einrichten.
2. Mithilfe der Kennung der Basisverbindung führen Sie dann einen weiteren Aufruf aus, mit dem Sie eine Zielverbindung erstellen. In dem Aufruf sind der Ort in Ihrem Speicherkonto, an dem die exportierten Daten bereitgestellt werden, sowie das Format der zu exportierenden Daten angegeben.

### Autorisieren des Zugriffs auf das Streaming-Ziel

**API-Format**

```http
POST /connections
```

**Anfrage**

>[!IMPORTANT]
>
>Das folgende Beispiel enthält Code-Kommentare mit dem Präfix `//`. Diese Kommentare zeigen, wo für verschiedene Streaming-Ziele unterschiedliche Werte verwendet werden müssen. Bitte entfernen Sie die Kommentare, bevor Sie das Snippet verwenden.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connection for Amazon Kinesis/ Azure Event Hubs",
    "description": "summer advertising campaign",
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
* `{AUTHENTICATION_CREDENTIALS}`: Geben Sie den Namen Ihres Streaming-Ziels ein: `Aws Kinesis authentication credentials` oder `Azure EventHub authentication credentials`.
* `{ACCESS_ID}`: *Für [!DNL Amazon Kinesis].* Ihre Zugriffs-ID für Ihren Amazon Kinesis-Speicherort.
* `{SECRET_KEY}`: *Für [!DNL Amazon Kinesis].* Sie Ihren geheimen Schlüssel für Ihren Amazon Kinesis-Speicherort.
* `{REGION}`: *Für [!DNL Amazon Kinesis].* Die Region in Ihrem [!DNL Amazon Kinesis]-Konto, in der Experience Platform Ihre Daten streamt.
* `{SAS_KEY_NAME}`: *Für [!DNL Azure Event Hubs].* Geben Sie den Namen Ihres SAS-Schlüssels ein. Erfahren Sie mehr über die Authentifizierung bei [!DNL Azure Event Hubs] mit SAS-Schlüsseln in der [Dokumentation zu Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* `{SAS_KEY}`: *Für [!DNL Azure Event Hubs].* Geben Sie Ihren SAS-Schlüssel ein. Erfahren Sie mehr über die Authentifizierung bei [!DNL Azure Event Hubs] mit SAS-Schlüsseln in der [Dokumentation zu Microsoft](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* `{EVENT_HUB_NAMESPACE}`: *Für [!DNL Azure Event Hubs].* Füllen Sie den [!DNL Azure Event Hubs]-Namespace aus, in den Experience Platform Ihre Daten streamen soll. Weitere Informationen finden Sie unter [Erstellen eines Event Hubs-Namespace](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace) in der [!DNL Microsoft].

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

>[!IMPORTANT]
>
>Das folgende Beispiel enthält Code-Kommentare mit dem Präfix `//`. Diese Kommentare zeigen, wo für verschiedene Streaming-Ziele unterschiedliche Werte verwendet werden müssen. Bitte entfernen Sie die Kommentare, bevor Sie das Snippet verwenden.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Amazon Kinesis/ Azure Event Hubs target connection",
    "description": "Connection to Amazon Kinesis/ Azure Event Hubs",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "{CONNECTION_SPEC_ID}",
        "version": "1.0"
    },
    "data": {
        "format": "json"
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
* `{NAME_OF_DATA_STREAM}`: *Für [!DNL Amazon Kinesis].* Geben Sie den Namen Ihres vorhandenen Datenstroms in Ihrem [!DNL Amazon Kinesis]-Konto an. Experience Platform exportiert Daten in diesen Stream.
* `{REGION}`: *Für [!DNL Amazon Kinesis].* Die Region in Ihrem Amazon Kinesis-Konto, in der Experience Platform Ihre Daten streamt.
* `{EVENT_HUB_NAME}`: *Für [!DNL Azure Event Hubs].* Geben Sie den [!DNL Azure Event Hub] ein, in den Experience Platform Ihre Daten streamen soll. Weitere Informationen finden Sie unter [Erstellen eines Ereignis-Hub](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub) in der [!DNL Microsoft].

**Antwort**

Bei einer erfolgreichen Antwort wird die eindeutige Kennung (`id`) für die neu erstellte Zielverbindung zu Ihrem Streaming-Ziel zurückgegeben. Notieren Sie sich diesen Wert, da Sie ihn in späteren Schritten benötigen werden.

```json
{
    "id": "12ab90c7-519c-4291-bd20-d64186b62da8"
}
```

## Datenfluss erstellen

![Übersicht über die Zielschritte – Schritt 4](../assets/api/streaming-destination/step4.png)

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
-H 'x-gw-ims-org-id: {ORG_ID}' \
-H 'x-sandbox-name: {SANDBOX_NAME}' \
-H 'Content-Type: application/json' \
-d  '{
  "name": "Azure Event Hubs",
  "description": "Azure Event Hubs",
  "flowSpec": {
    "id": "{FLOW_SPEC_ID}",
    "version": "1.0"
  },
  "sourceConnectionIds": [
    "{SOURCE_CONNECTION_ID}"
  ],
  "targetConnectionIds": [
    "{TARGET_CONNECTION_ID}"
  ],
  "transformations": [
    {
      "name": "GeneralTransform",
      "params": {
        "profileSelectors": {
          "selectors": [
            
          ]
        },
        "segmentSelectors": {
          "selectors": [
            
          ]
        }
      }
    }
  ]
}
```

* `{FLOW_SPEC_ID}`: Die Flussspezifikations-ID für profilbasierte Ziele ist `71471eba-b620-49e4-90fd-23f1fa0174d8`. Verwenden Sie diesen Wert im -Aufruf.
* `{SOURCE_CONNECTION_ID}`: Verwenden Sie die Quellverbindungs-ID, die Sie im Schritt [Verbindung zu Ihren Experience Platform-Daten herstellen](#connect-to-your-experience-platform-data) erhalten haben.
* `{TARGET_CONNECTION_ID}`: Verwenden Sie die Zielverbindungs-ID, die Sie im Schritt &quot;[ mit Streaming-Ziel herstellen“ erhalten ](#connect-to-streaming-destination).

**Antwort**

Bei einer erfolgreichen Antwort werden die Kennung (`id`) des neu erstellten Datenflusses und ein `etag` zurückgegeben. Notieren Sie sich beide Werte. So wie Sie es im nächsten Schritt tun, um Zielgruppen zu aktivieren.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```


## Daten an Ihr neues Ziel aktivieren {#activate-data}

![Übersicht über die Zielschritte – Schritt 5](../assets/api/streaming-destination/step5.png)

Nachdem Sie alle Verbindungen und den Datenfluss erstellt haben, können Sie jetzt Ihre Profildaten für die Streaming-Plattform aktivieren. In diesem Schritt legen Sie fest, welche Zielgruppen und Profilattribute Sie an das Ziel senden, und Sie können Daten planen und an das Ziel senden.

Um Zielgruppen für Ihr neues Ziel zu aktivieren, müssen Sie einen JSON-PATCH-Vorgang ausführen, ähnlich dem folgenden Beispiel. Sie können mehrere Zielgruppen und Profilattribute in einem Aufruf aktivieren. Weiterführende Informationen zu JSON PATCH finden Sie in der [RFC-Spezifikation](https://tools.ietf.org/html/rfc6902).

**API-Format**

```http
PATCH /flows
```

**Anfrage**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
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
        "name": "Name of the audience that you are activating",
        "description": "Description of the audience that you are activating",
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

| Eigenschaft | Beschreibung |
| --------- | ----------- |
| `{DATAFLOW_ID}` | Verwenden Sie in der URL die ID des Datenflusses, den Sie im vorherigen Schritt erstellt haben. |
| `{ETAG}` | Rufen Sie die `{ETAG}` aus der Antwort im vorherigen Schritt ab [Erstellen eines Datenflusses](#create-dataflow). Das Antwortformat im vorherigen Schritt wurde in Anführungszeichen gesetzt. Sie müssen die Werte ohne Escape-Zeichen im Header der Anfrage verwenden. Siehe folgendes Beispiel: <br> <ul><li>Anwendungsbeispiel für eine Antwort: `"etag":""7400453a-0000-1a00-0000-62b1c7a90000""`</li><li>In Ihrer Anfrage zu verwendender Wert: `"etag": "7400453a-0000-1a00-0000-62b1c7a90000"`</li></ul> <br> Der eTag-Wert wird bei jeder erfolgreichen Aktualisierung eines Datenflusses aktualisiert. |
| `{SEGMENT_ID}` | Geben Sie die Zielgruppen-ID an, die Sie an dieses Ziel exportieren möchten. Informationen zum Abrufen von Zielgruppen-IDs für die Zielgruppen, die Sie aktivieren möchten, finden Sie unter [Abrufen einer Zielgruppendefinition](https://www.adobe.io/experience-platform-apis/references/segmentation/#operation/retrieveSegmentDefinitionById) in der Experience Platform-API-Referenz. |
| `{PROFILE_ATTRIBUTE}` | Beispiel: `"person.lastName"` |
| `op` | Der Operationsaufruf, der verwendet wird, um die Aktion zu definieren, die zur Aktualisierung des Datenflusses erforderlich ist. Operationen umfassen: `add`, `replace` und `remove`. Um eine Zielgruppe zu einem Datenfluss hinzuzufügen, verwenden Sie den Vorgang `add` . |
| `path` | Definiert den Teil des Flusses, der aktualisiert werden soll. Verwenden Sie beim Hinzufügen einer Zielgruppe zu einem Datenfluss den im Beispiel angegebenen Pfad. |
| `value` | Der neue Wert, mit dem Sie Ihren Parameter aktualisieren möchten. |
| `id` | Geben Sie die ID der Zielgruppe an, die Sie dem Ziel-Datenfluss hinzufügen. |
| `name` | *Optional*. Geben Sie den Namen der Zielgruppe an, die Sie dem Ziel-Datenfluss hinzufügen. Beachten Sie, dass dieses Feld nicht obligatorisch ist und Sie dem Ziel-Datenfluss erfolgreich eine Zielgruppe hinzufügen können, ohne ihren Namen anzugeben. |

**Antwort**

Suchen Sie nach einer „202 OK“-Antwort. Es wird kein Antworttext zurückgegeben. Um zu überprüfen, ob die Anfrage korrekt war, lesen Sie den nächsten Schritt „Datenfluss validieren“.

## Datenfluss validieren

![Übersicht über die Zielschritte – Schritt 6](../assets/api/streaming-destination/step6.png)

Als letzten Schritt im Tutorial sollten Sie überprüfen, ob die Zielgruppen und Profilattribute dem Datenfluss korrekt zugeordnet wurden.

Führen Sie zur Validierung die folgende GET-Anfrage aus:

**API-Format**

```http
GET /flows
```

**Anfrage**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--header 'x-sandbox-name: prod' \
--header 'If-Match: "{ETAG}"' 
```

* `{DATAFLOW_ID}`: Verwenden Sie den Datenfluss aus dem vorherigen Schritt.
* `{ETAG}`: Verwenden Sie das eTag aus dem vorherigen Schritt.

**Antwort**

Die zurückgegebene Antwort sollte im `transformations` die Zielgruppen und Profilattribute enthalten, die Sie im vorherigen Schritt gesendet haben. Ein Beispielparameter `transformations` in der Antwort könnte wie folgt aussehen:

```json
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
> Zusätzlich zu den Profilattributen und den Zielgruppen im Schritt [Aktivieren von Daten für Ihr neues Ziel](#activate-data) enthalten die exportierten Daten in [!DNL AWS Kinesis] und [!DNL Azure Event Hubs] auch Informationen zur Identitätszuordnung. Dies stellt die Identitäten der exportierten Profile dar (z. B. [ECID](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html), mobile ID, Google ID, E-Mail-Adresse usw.). Siehe Beispiel unten.

```json
{
  "person": {
    "email": "yourstruly@adobe.com"
  },
  "segmentMembership": {
    "ups": {
      "72ddd79b-6b0a-4e97-a8d2-112ccd81bd02": {
        "lastQualificationTime": "2020-03-03T21:24:39Z",
        "status": "exited"
      },
      "7841ba61-23c1-4bb3-a495-00d695fe1e93": {
        "lastQualificationTime": "2020-03-04T23:37:33Z",
        "status": "realized"
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

## Verwenden [!DNL Postman] Sammlungen zum Herstellen einer Verbindung zu Streaming-Zielen  {#collections}

Um eine schnellere Verbindung zu den in diesem Tutorial beschriebenen Streaming-Zielen herzustellen, können Sie [[!DNL Postman]](https://www.postman.com/) verwenden.

[!DNL Postman] ist ein Tool, mit dem Sie API-Aufrufe durchführen und Bibliotheken vordefinierter Aufrufe und Umgebungen verwalten können.

Für dieses spezifische Tutorial wurden die folgenden [!DNL Postman] angehängt:

* [!DNL AWS Kinesis] [!DNL Postman]
* [!DNL Azure Event Hubs] [!DNL Postman]

Klicken Sie [hier](../assets/api/streaming-destination/DestinationPostmanCollection.zip), um das Sammlungsarchiv herunterzuladen.

Jede Sammlung enthält die erforderlichen Anforderungen und Umgebungsvariablen für [!DNL AWS Kinesis] bzw. [!DNL Azure Event Hub].

### Verwendung der [!DNL Postman] Sammlungen {#how-to-use-postman-collections}

Gehen Sie wie folgt vor, um mithilfe der angehängten [!DNL Postman] eine Verbindung zu den Zielen herzustellen:

* Herunterladen und Installieren von [!DNL Postman]
* [Herunterladen](../assets/api/streaming-destination/DestinationPostmanCollection.zip) und Entpacken der angehängten Sammlungen
* Importieren Sie die Sammlungen aus den entsprechenden Ordnern in [!DNL Postman].
* Füllen Sie die Umgebungsvariablen gemäß den Anweisungen in diesem Artikel aus.
* Führen Sie die [!DNL API] Anfragen von [!DNL Postman] aus, basierend auf den Anweisungen in diesem Artikel.

## Umgang mit API-Fehlern {#api-error-handling}

Die API-Endpunkte in diesem Tutorial folgen den allgemeinen Grundsätzen von Experience Platform API-Fehlermeldungen. Weitere Informationen [ Interpretieren von Fehlerantworten finden Sie unter ](/help/landing/troubleshooting.md#api-status-codes)API-Status-Codes[ und ](/help/landing/troubleshooting.md#request-header-errors)Fehler in der Anfragekopfzeile im Handbuch zur Fehlerbehebung bei Experience Platform .

## Nächste Schritte {#next-steps}

In diesem Tutorial haben Sie Experience Platform erfolgreich mit einem Ihrer bevorzugten Streaming-Ziele verbunden und einen Datenfluss zum jeweiligen Ziel eingerichtet. Ausgehende Daten können jetzt im Ziel für Kundenanalysen oder andere Datenvorgänge verwendet werden, die Sie möglicherweise durchführen möchten. Weiterführende Informationen finden Sie auf den folgenden Seiten:

* [Ziele – Übersicht](../home.md)
* [Zielkatalog – Übersicht](../catalog/overview.md)
