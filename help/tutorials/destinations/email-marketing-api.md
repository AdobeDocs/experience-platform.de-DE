---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: E-Mail-Marketingziele erstellen
topic: tutorial
translation-type: tm+mt
source-git-commit: ed9d6eadeb00db51278ea700f7698a1b5590632f
workflow-type: tm+mt
source-wordcount: '1670'
ht-degree: 1%

---


# Erstellen Sie E-Mail-Marketing-Ziele und aktivieren Sie Daten in der Adobe-Platform für Echtzeit-Kundendaten

In diesem Lernprogramm wird gezeigt, wie Sie mit API-Aufrufen eine Verbindung zu Ihren Adobe Experience Platformen herstellen, ein [E-Mail-Marketingziel](../../rtcdp/destinations/email-marketing-destinations.md)erstellen, einen Datenfluss zu Ihrem neu erstellten Ziel erstellen und Daten zu Ihrem neu erstellten Ziel aktivieren können.

In diesem Lernprogramm wird in allen Beispielen das Adobe Campaign-Ziel verwendet, aber die Schritte sind für alle E-Mail-Marketingziele identisch.

![Übersicht - Schritte zum Erstellen eines Ziels und Aktivieren von Segmenten](../images/destinations/flow-api-destinations-steps-overview.png)

Wenn Sie die Benutzeroberfläche in der Echtzeit-CDP von Adobe verwenden möchten, um ein Ziel zu verbinden und Daten zu aktivieren, finden Sie weitere Informationen unter [Verbinden eines Ziels](../../rtcdp/destinations/connect-destination.md) und [Aktivieren von Profilen und Segmenten mit einem Ziel](../../rtcdp/destinations/activate-destinations.md) -Lernprogramm.

## Erste Schritte

Dieses Handbuch erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

* [Erlebnis-Datenmodell (XDM)-System](../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
* [Katalogdienst](../../catalog/home.md): Catalog ist das Datensatzsystem für die Datenposition und -linie innerhalb der Experience Platform.
* [Sandboxen](../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxen, die eine Instanz einer Platform in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie zur Aktivierung von Daten für E-Mail-Marketing-Ziele in Adobe Echtzeit-CDP kennen müssen.

### Erforderliche Berechtigungen erfassen

Um die Schritte in diesem Lernprogramm abzuschließen, sollten Sie die folgenden Anmeldeinformationen entsprechend der Art der Ziele, mit denen Sie Segmente verbinden und aktivieren, bereitstellen.

* Für Amazon S3-Verbindungen zu E-Mail-Marketingplattformen: `accessId`, `secretKey`
* Für SFTP-Verbindungen zu E-Mail-Marketingplattformen: `domain`, `port`, `username``password` oder `ssh key` (je nach Verbindungsmethode zum FTP-Speicherort)

### Lesen von Beispiel-API-Aufrufen

In diesem Lernprogramm finden Sie Beispiele für API-Aufrufe, die zeigen, wie Sie Ihre Anforderungen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anforderungs-Nutzdaten. Beispiel-JSON, die in API-Antworten zurückgegeben wird, wird ebenfalls bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt [zum Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung bei Experience Platformen.

### Werte für erforderliche und optionale Überschriften sammeln

Um Platformen-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungslehrgang](../authentication.md)abschließen. Das Abschließen des Authentifizierungtutorials stellt die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform API-Aufrufen bereit, wie unten dargestellt:

* Genehmigung: Träger `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Ressourcen in Experience Platform können zu bestimmten virtuellen Sandboxen isoliert werden. Bei Anforderungen an Platformen-APIs können Sie den Namen und die ID der Sandbox angeben, in der der Vorgang ausgeführt wird. Dies sind optionale Parameter.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NHinweis]
>Weitere Informationen zu Sandboxen in der Experience Platform finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Für alle Anforderungen, die eine Payload enthalten (POST, PUT, PATCH), ist ein zusätzlicher Medientyp-Header erforderlich:

* Content-Type: `application/json`

<!--

### Definitions

Before starting this tutorial, familiarize yourself with the following terms which we'll use throughout the tutorial:

**Flow**: 

**Base Connection**: 

**Target Connection**: 

**Source Connection**: 

-->

### Swagger-Dokumentation

Die zugehörige Referenzdokumentation für alle API-Aufrufe finden Sie in diesem Tutorial in Swagger. Weitere Informationen finden Sie in der Dokumentation zur [Flow Service API unter Adobe.io](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml). Es wird empfohlen, dieses Tutorial und die Seite Swagger-Dokumentation parallel zu verwenden.

## Liste der verfügbaren Ziele {#get-the-list-of-available-destinations}

![Übersichtsschritt zu den Zielschritten 1](../images/destinations/flow-api-destinations-step1.png)

Als ersten Schritt sollten Sie entscheiden, in welchem E-Mail-Marketingziel Daten aktiviert werden sollen. Zunächst führen Sie einen Aufruf durch, um eine Liste der verfügbaren Ziele anzufordern, mit denen Sie eine Verbindung herstellen und Segmente aktivieren können. Führen Sie die folgende GET-Anforderung an den `connectionSpecs` Endpunkt aus, um eine Liste der verfügbaren Ziele zurückzugeben:

**API-Format**

```http
GET /connectionSpecs
```

**Anfrage**

<!--

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-sandbox-id: {SANDBOX_ID}' \    
    -H 'Content-Type: application/json' \
```

-->

```
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
--header 'accept: application/json' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```


**Antwort**

Eine erfolgreiche Antwort enthält eine Liste der verfügbaren Ziele und ihrer eindeutigen Bezeichner (`id`). Speichern Sie den Wert des Ziels, das Sie verwenden möchten, wie in weiteren Schritten erforderlich. Wenn Sie z. B. Segmente mit Adobe Campaign verbinden und bereitstellen möchten, suchen Sie in der Antwort nach folgendem Codefragment:

```json
{
    "id": "0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
  "name": "Adobe Campaign",
  ...
  ...
}
```

## Herstellen einer Verbindung zu Ihren Experience Platformen {#connect-to-your-experience-platform-data}

![Übersichtsschritt zu den Zielschritten 2](../images/destinations/flow-api-destinations-step2.png)

Als Nächstes müssen Sie eine Verbindung zu den Daten Ihrer Experience Platform herstellen, damit Sie die Profil-Daten exportieren und in Ihrem bevorzugten Ziel aktivieren können. Diese besteht aus zwei Unterteilen, die nachfolgend beschrieben werden.

1. Zunächst müssen Sie einen Aufruf ausführen, um den Zugriff auf Ihre Daten in Experience Platform zu autorisieren, indem Sie eine Basisverbindung einrichten.
2. Anschließend führen Sie mit der Basis-Verbindungs-ID einen weiteren Aufruf durch, bei dem Sie eine Quellverbindung erstellen, die die Verbindung zu den Daten Ihrer Experience Platform herstellt.


### Zugriff auf Ihre Daten in der Experience Platform genehmigen

**API-Format**

```http
POST /connections
```

**Anfrage**

<!--

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-sandbox-id: {SANDBOX_ID}' \ 
    -H 'Content-Type: application/json' \
    -d  '{
            
            "name": "Base connection to Experience Platform",
            "description": "This call establishes the connection to Experience Platform data",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC}",
                "version": "1.0"
            }
           }'
```

-->

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

### Herstellen einer Verbindung zu Ihren Experience Platformen

**API-Format**

```http
POST /sourceConnections
```

**Anfrage**

<!--

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-id: {SANDBOX_ID}' \ 
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d  '{
  "name": "Connecting to Unified Profile Service",
  "description": "Optional",
  "baseConnectionId": "{BASE_CONNECTION_ID}",
  "connectionSpec": {
    "id": "{CONNECTION_SPEC}",
    "version": "1.0"
  },
  "data": {
    "format": "CSV",
    "schema": null
  }
  }
```

-->

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
                "format": "CSV",
                "schema": null
            },
            "params" : {}
}'
```

* `{BASE_CONNECTION_ID}`: Verwenden Sie die ID, die Sie im vorherigen Schritt erhalten haben.
* `{CONNECTION_SPEC_ID}`: Verwenden Sie die Verbindungsspezifikations-ID für Unified Profil Service - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung (`id`) für die neu erstellte Quellverbindung zum Unified Profil Service zurück. Dadurch wird bestätigt, dass Sie erfolgreich eine Verbindung zu Ihren Experience Platformen hergestellt haben. Speichern Sie diesen Wert so, wie er in einem späteren Schritt erforderlich ist.

```json
{
    "id": "ed48ae9b-c774-4b6e-88ae-9bc7748b6e97"
}
```


## Verbindung zum E-Mail-Marketingziel herstellen {#connect-to-email-marketing-destination}

![Übersichtsschritt zu den Zielschritten 3](../images/destinations/flow-api-destinations-step3.png)

In diesem Schritt richten Sie eine Verbindung zu Ihrem gewünschten E-Mail-Marketingziel ein. Diese besteht aus zwei Unterteilen, die nachfolgend beschrieben werden.

1. Zunächst müssen Sie einen Aufruf ausführen, um den Zugriff auf den E-Mail-Dienstleister zu autorisieren, indem Sie eine Basisverbindung einrichten.
2. Mithilfe der Basis-Verbindungs-ID führen Sie dann einen weiteren Aufruf durch, bei dem Sie eine Zielgruppe erstellen, die den Speicherort in Ihrem Datenspeicherung-Konto, an dem die exportierten Daten bereitgestellt werden, sowie das Format der zu exportierenden Daten angibt.

### Autorisieren des Zugriffs auf das E-Mail-Marketingziel

**API-Format**

```http
POST /connections
```

**Anfrage**

<!--

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-sandbox-id: {SANDBOX_ID}' \ 
    -H 'Content-Type: application/json' \
    -d  '{
            
            "name": "S3 Connection for Adobe Campaign",
            "description": "ACME company holiday campaign",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC}",
                "version": "1.0"
            },
            "auth": {
                "specName": "{S3 or SFTP}",
                "params": {
                    "accessId": "{ACCESS_ID}",
                    "secretKey": "{SECRET_KEY}"
                }
            }
           }'
```

-->

```
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "S3 Connection for Adobe Campaign",
    "description": "your company's holiday campaign",
    "connectionSpec": {
        "id": "{_CONNECTION_SPEC_ID}",
        "version": "1.0"
    },
    "auth": {
        "specName": "{S3 or SFTP}",
        "params": {
            "accessId": "{ACCESS_ID}",
            "secretKey": "{SECRET_KEY}"
        }
    }
}'
```

* `{CONNECTION_SPEC_ID}`: Verwenden Sie die Verbindungsspezifikations-ID, die Sie im Schritt [Liste der verfügbaren Ziele](#get-the-list-of-available-destinations)erhalten haben.
* `{S3 or SFTP}`: den gewünschten Verbindungstyp für dieses Ziel eingeben. Blättern Sie im [Zielkatalog](../../rtcdp/destinations/destinations-catalog.md)zu Ihrem bevorzugten Ziel, um zu sehen, ob S3- und/oder SFTP-Verbindungstypen unterstützt werden.
* `{ACCESS_ID}`: Ihre Zugriffs-ID für Ihren Amazon S3-Datenspeicherung-Standort.
* `{SECRET_KEY}`: Ihr geheimer Schlüssel für Ihre Amazon S3-Datenspeicherung.

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

<!--

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \    
    -H 'x-sandbox-id: {SANDBOX_ID}' \ 
    -H 'Content-Type: application/json' \
    -d  '{
   "baseConnectionId": "{BASE_CONNECTION_ID}",
   "name": "TargetConnection for Adobe Campaign",
   "data": {
       "format": "CSV",
       "schema": {
           "id": "1.0",
           "version": "1.0"
       },
    "connectionSpec": {
    "id": "{CONNECTION_SPEC_ID}",
    "version": "1.0"
   },
   "params": {
       "mode": "S3",
       "bucketName": "{BUCKETNAME}",
       "path": "{FILEPATH}"
    }
    }
```

-->

```
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for Adobe Campaign",
    "description": "Connection to Adobe Campaign",
    "baseConnection": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "{CONNECTION_SPEC_ID}",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "S3",
        "bucketName": "{BUCKETNAME}",
        "path": "{FILEPATH}",
        "format": "CSV"
    }
}'
```

* `{BASE_CONNECTION_ID}`: Verwenden Sie die Basis-Verbindungs-ID, die Sie im obigen Schritt erhalten haben.
* `{CONNECTION_SPEC_ID}`: Verwenden Sie die Verbindungsspezifikation, die Sie im Schritt erhalten haben [Sie die Liste der verfügbaren Ziele](#get-the-list-of-available-destinations).
* `{BUCKETNAME}`: Ihr Amazon S3-Behälter, in dem CDP den Datenexport in Echtzeit einlagert.
* `{FILEPATH}`: Der Pfad in Ihrem Amazon S3-Bucket-Ordner, in dem die Echtzeit-CDP den Datenexport hinterlegt.

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung (`id`) für die neu erstellte Zielgruppe-Verbindung mit Ihrem E-Mail-Marketingziel zurück. Speichern Sie diesen Wert so, wie er in späteren Schritten erforderlich ist.

```json
{
    "id": "12ab90c7-519c-4291-bd20-d64186b62da8"
}
```

## Erstellen eines Datenflusses

![Übersichtsschritt zu den Zielschritten 4](../images/destinations/flow-api-destinations-step4.png)

Mithilfe der IDs, die Sie in den vorherigen Schritten erhalten haben, können Sie jetzt einen Datendurchlauf zwischen den Daten Ihrer Experience Platform und dem Ziel erstellen, an das Sie Daten aktivieren möchten. Stellen Sie sich diesen Schritt als eine Konstruktion der Pipeline vor, durch die Daten später zwischen der Experience Platform und dem gewünschten Ziel fließen.

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
   
        "name": "Activate segments to Adobe Campaign",
        "description": "This operation creates a dataflow which we will later use to activate segments to Adobe Campaign",
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
                    "segmentSelectors": {
                        "selectors": []
                    },
                    "profileSelectors": {
                        "selectors": []
                    }
                }
            }
        ]
    }
```

* `{FLOW_SPEC_ID}`: Verwenden Sie den Fluss für das E-Mail-Marketingziel, mit dem Sie eine Verbindung herstellen möchten. Um die Flussspezifikation abzurufen, führen Sie einen GET-Vorgang am `flowspecs` Endpunkt durch. Weitere Informationen finden Sie in der Swagger-Dokumentation: https://platform.adobe.io/data/foundation/flowservice/swagger#/Flow%20Specs%20API/getFlowSpecs. Suchen `upsTo` und kopieren Sie in der Antwort die entsprechende ID des E-Mail-Marketingziels, mit dem Sie eine Verbindung herstellen möchten. Suchen Sie zum Adobe Campaign nach dem `upsToCampaign` Parameter `id` und kopieren Sie ihn.
* `{SOURCE_CONNECTION_ID}`: Verwenden Sie die Quell-Verbindungs-ID, die Sie im Schritt [Verbindung zu Ihrer Experience Platform](#connect-to-your-experience-platform-data)herstellen erhalten haben.
* `{TARGET_CONNECTION_ID}`: Verwenden Sie die Zielgruppe-Verbindungs-ID, die Sie im Schritt [Verbinden mit E-Mail-Marketingziel](#connect-to-email-marketing-destination)erhalten haben.

**Antwort**

Bei einer erfolgreichen Antwort werden die ID (`id`) des neu erstellten Datenflusses und eine `etag`zurückgegeben. Beachten Sie beide Werte. wie im nächsten Schritt beschrieben, um Segmente zu aktivieren.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```


## Aktivieren von Daten an Ihrem neuen Ziel

![Übersichtsschritt zu den Zielschritten 5](../images/destinations/flow-api-destinations-step5.png)

Nachdem Sie alle Verbindungen und den Datenfluss erstellt haben, können Sie jetzt Ihre Profil-Daten auf der E-Mail-Marketingplattform aktivieren. In diesem Schritt wählen Sie aus, welche Segmente und welche Profil-Attribute Sie an das Ziel senden, und Sie können Daten planen und an das Ziel senden.

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
* `{SEGMENT_ID}`: Geben Sie die Segment-ID an, die Sie an dieses Ziel exportieren möchten. Um Segment-IDs für die Segmente abzurufen, die Sie aktivieren möchten, gehen Sie zu https://www.adobe.io/apis/experienceplatform/home/api-reference.html#/ und suchen Sie nach dem `GET /segment/jobs` Vorgang.
* `{PROFILE_ATTRIBUTE}`: Beispiel, `"person.lastName"`

**Antwort**

Suchen Sie nach einer OK-Antwort für 202. Es wird kein Antwortkörper zurückgegeben. Um zu überprüfen, ob die Anforderung korrekt war, lesen Sie den nächsten Schritt Validieren des Datenflusses.

## Datenfluss überprüfen

![Übersichtsschritt zu den Zielschritten 6](../images/destinations/flow-api-destinations-step6.png)

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

In diesem Lernprogramm haben Sie CDP in Echtzeit erfolgreich mit einem Ihrer bevorzugten E-Mail-Marketingziele verbunden und einen Datenflug zum entsprechenden Ziel eingerichtet. Ausgehende Daten können jetzt im Zielort für E-Mail-Kampagnen, gezielte Werbung und viele andere Anwendungsfälle verwendet werden. Weitere Informationen finden Sie auf den folgenden Seiten:

* [Ziele – Übersicht](../../rtcdp/destinations/destinations-overview.md)
* [Zielkatalog - Übersicht](../../rtcdp/destinations/destinations-catalog.md)