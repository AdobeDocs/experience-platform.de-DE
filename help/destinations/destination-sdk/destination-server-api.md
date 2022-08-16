---
description: Auf dieser Seite werden alle API-Vorgänge aufgelistet und beschrieben, die Sie mit dem API-Endpunkt „/authoring/destination-servers“ ausführen können. Die Server- und Vorlagenspezifikationen für Ihr Ziel können im Adobe Experience Platform Destination SDK über den allgemeinen Endpunkt „/authoring/destination-servers“ konfiguriert werden.
title: API-Vorgänge für Ziel-Server-Endpunkte
exl-id: a144b0fb-d34f-42d1-912b-8576296e59d2
source-git-commit: a43bb18182ac6e591e011b585719da955ee681b7
workflow-type: tm+mt
source-wordcount: '1382'
ht-degree: 95%

---

# API-Vorgänge für Ziel-Server-Endpunkte

>[!IMPORTANT]
>
>**API-Endpunkt**: `platform.adobe.io/data/core/activation/authoring/destination-servers`

Auf dieser Seite werden alle API-Vorgänge aufgelistet und beschrieben, die Sie mit dem API-Endpunkt `/authoring/destination-servers` ausführen können. Die Server- und Vorlagenspezifikationen für Ihr Ziel können im Adobe Experience Platform Destination SDK über den allgemeinen Endpunkt `/authoring/destination-servers` konfiguriert werden. Eine Beschreibung der von diesem Endpunkt bereitgestellten Funktionalität finden Sie unter [Server- und Vorlagenspezifikationen](./server-and-template-configuration.md).

## Erste Schritte mit API-Vorgängen für Ziel-Server {#get-started}

Bevor Sie fortfahren, lesen Sie [Erste Schritte](./getting-started.md) für wichtige Informationen, die Sie benötigen, um die API erfolgreich aufrufen zu können, einschließlich Informationen zum Abrufen der erforderlichen Authoring-Berechtigung für Ziele und der erforderlichen Kopfzeilen.

## Erstellen einer Konfiguration für einen Streaming-Ziel-Server {#create}

Sie können eine neue Ziel-Server-Konfiguration für ein Streaming-Ziel erstellen, indem Sie eine POST-Anfrage an den Endpunkt `/authoring/destination-servers` senden.

**API-Format**

```http
POST /authoring/destination-servers
```

**Anfrage**

Die folgende Anfrage erstellt eine neue Ziel-Server-Konfiguration, die durch die in der Payload bereitgestellten Parameter konfiguriert wird. Die nachstehende Payload enthält alle Parameter, die vom Endpunkt `/authoring/destination-servers` akzeptiert werden. Beachten Sie, dass Sie nicht alle Parameter für den Aufruf hinzufügen müssen und dass die Vorlage entsprechend Ihren API-Anforderungen angepasst werden kann.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.region}}/items"
      }
   },
   "httpTemplate":{
      "httpMethod":"POST",
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{ \"attributes\": [ {% for ns in [\"external_id\", \"yourdestination_id\"] %} {% if input.profile.identityMap[ns] is not empty and first_namespace_encountered %} , {% endif %} {% set first_namespace_encountered = true %} {% for identity in input.profile.identityMap[ns]%} { \"{{ ns }}\": \"{{ identity.id }}\" {% if input.profile.segmentMembership.ups is not empty %} , \"AEPSegments\": { \"add\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"realized\" or segment.value.status == \"existing\" %} {% if added_segment_found %} , {% endif %} {% set added_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ], \"remove\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"exited\" %} {% if removed_segment_found %} , {% endif %} {% set removed_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ] } {% set removed_segment_found = false %} {% set added_segment_found = false %} {% endif %} {% if input.profile.attributes is not empty %} , {% endif %} {% for attribute in input.profile.attributes %} \"{{ attribute.key }}\": {% if attribute.value is empty %} null {% else %} \"{{ attribute.value.value }}\" {% endif %} {% if not loop.last%} , {% endif %} {% endfor %} } {% if not loop.last %} , {% endif %} {% endfor %} {% endfor %} ] }"
      },
      "contentType":"application/json"
   }
}
```

| Parameter | Typ | Beschreibung |
| -------- | ----------- | ----------- |
| `name` | Zeichenfolge | *Erforderlich.* Stellt einen Anzeigenamen Ihres Servers dar, der nur für Adobe sichtbar ist. Dieser Name ist für Partner oder Kunden nicht sichtbar. Beispiel `Moviestar destination server`. |
| `destinationServerType` | Zeichenfolge | *Erforderlich.* Festlegen auf `URL_BASED` für Streaming-Ziele. |
| `urlBasedDestination.url.templatingStrategy` | Zeichenfolge | *Erforderlich.* <ul><li>Verwenden Sie `PEBBLE_V1`, wenn Adobe die URL im nachstehenden Feld `value` umwandeln muss. Verwenden Sie diese Option, wenn Sie folgenden Endpunkt haben: `https://api.moviestar.com/data/{{customerData.region}}/items`. </li><li> Verwenden Sie `NONE`, wenn von Adobe keine Umwandlung erforderlich ist, z. B. wenn Sie folgenden Endpunkt haben: `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | Zeichenfolge | *Erforderlich.* Geben Sie die Adresse des API-Endpunkts ein, mit dem sich Experience Platform verbinden soll. |
| `httpTemplate.httpMethod` | Zeichenfolge | *Erforderlich.* Die Methode, die Adobe bei Aufrufen an Ihren Server verwendet. Es gibt die Optionen `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `httpTemplate.requestBody.templatingStrategy` | Zeichenfolge | *Erforderlich.* Verwenden Sie `PEBBLE_V1`. |
| `httpTemplate.requestBody.value` | Zeichenfolge | *Erforderlich.* Diese Zeichenfolge ist die Version mit Escape-Zeichen, die die Daten von Platform-Kunden in das Format umwandelt, das Ihr Service erwartet. <br> <ul><li> Informationen zum Schreiben der Vorlage finden Sie im Abschnitt [Verwenden von Vorlagen](./message-format.md#using-templating). </li><li> Weitere Informationen zu Escape-Zeichen finden Sie unter [RFC JSON-Standard, Abschnitt 7](https://tools.ietf.org/html/rfc8259#section-7). </li><li> Ein Beispiel für eine einfache Umwandlung finden Sie im unter [Umwandlung von Profilattributen](./message-format.md#attributes). </li></ul> |
| `httpTemplate.contentType` | Zeichenfolge | *Erforderlich.* Der Content-Typ, den Ihr Server akzeptiert. Dieser Wert ist höchstwahrscheinlich `application/json`. |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zu Ihrer neu erstellten Ziel-Server-Konfiguration zurück.

## Erstellen Sie eine Konfiguration für einen dateibasierten Ziel-Server {#create-file-based}

>[!IMPORTANT]
>
>Die Unterstützung für dateibasierte Ziele im Adobe Experience Platform Destination SDK ist derzeit als Beta-Version verfügbar. Dokumentation und Funktionalität können sich ändern.

### Beispielkonfiguration für den SFTP-Zielserver {#sftp-server-sample}

+++Beispiel für ein [!DNL SFTP] Zielserverkonfiguration

Sie können eine neue SFTP-Ziel-Server-Konfiguration erstellen, indem Sie eine POST-Anfrage an den Endpunkt `/authoring/destination-servers` senden.

**API-Format**

```http
POST /authoring/destination-servers
```

**Anfrage**

Die folgende Anfrage erstellt eine neue Ziel-Server-Konfiguration, die durch die in der Payload bereitgestellten Parameter konfiguriert wird. Die nachstehende Payload enthält alle Parameter, die vom Endpunkt `/authoring/destination-servers` akzeptiert werden. Beachten Sie, dass Sie nicht alle Parameter für den Aufruf hinzufügen müssen und dass die Vorlage entsprechend Ihren API-Anforderungen angepasst werden kann.


```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"File-based SFTP destination server",
   "destinationServerType":"FILE_BASED_SFTP",
   "fileBasedSftpDestination":{
      "rootDirectory":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.rootDirectory}}"
      }, 
      "port": 22,
      "encryptionMode" : "PGP"
   },
    "fileConfigurations": {
        "compression": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            }
        }
    }
}
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zu Ihrer neu erstellten Ziel-Server-Konfiguration zurück.
+++

### [!DNL Amazon S3] Beispielkonfiguration für Zielserver {#s3-server-sample}

+++Beispiel für ein [!DNL Amazon S3] Zielserverkonfiguration

Sie können eine neue Amazon S3-Ziel-Server-Konfiguration erstellen, indem Sie eine POST-Anfrage an den `/authoring/destination-servers`-Endpunkt senden.

**API-Format**

```http
POST /authoring/destination-servers
```

**Anfrage**

Die folgende Anfrage erstellt eine neue Ziel-Server-Konfiguration, die durch die in der Payload bereitgestellten Parameter konfiguriert wird. Die nachstehende Payload enthält alle Parameter, die vom Endpunkt `/authoring/destination-servers` akzeptiert werden. Beachten Sie, dass Sie nicht alle Parameter für den Aufruf hinzufügen müssen und dass die Vorlage entsprechend Ihren API-Anforderungen angepasst werden kann.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "name": "S3 destination",
    "destinationServerType": "FILE_BASED_S3",
    "fileBasedS3Destination": {
        "bucket": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.bucket}}"
        },
        "path": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.path}}"
        }
    },
    "fileConfigurations": {
        "compression": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            }
        }
    }
}
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zu Ihrer neu erstellten Ziel-Server-Konfiguration zurück.
+++

### [!DNL Azure Blob] Beispielkonfiguration für Zielserver {#blob-server-sample}

+++Beispiel für ein [!DNL Azure Blob] Zielserverkonfiguration

Sie können eine neue Azure Blob-Ziel-Server-Konfiguration erstellen, indem Sie eine POST-Anfrage an den Endpunkt `/authoring/destination-servers` senden.

**API-Format**

```http
POST /authoring/destination-servers
```

**Anfrage**

Die folgende Anfrage erstellt eine neue Ziel-Server-Konfiguration, die durch die in der Payload bereitgestellten Parameter konfiguriert wird. Die nachstehende Payload enthält alle Parameter, die vom Endpunkt `/authoring/destination-servers` akzeptiert werden. Beachten Sie, dass Sie nicht alle Parameter für den Aufruf hinzufügen müssen und dass die Vorlage entsprechend Ihren API-Anforderungen angepasst werden kann.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Blob destination server",
   "destinationServerType":"FILE_BASED_AZURE_BLOB",
   "fileBasedAzureBlobDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "container":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.container}}"
      }
   },
  "fileConfigurations": {
        "compression": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            }
        }
    }
}
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zu Ihrer neu erstellten Ziel-Server-Konfiguration zurück.
+++

### [!DNL Azure Data Lake Storage] Beispielkonfiguration für Zielserver {#adls-server-sample}

+++Beispiel für ein [!DNL Azure Data Lake Storage (ADLS)] Zielserverkonfiguration

Sie können eine neue ADLS-Ziel-Server-Konfiguration erstellen, indem Sie eine POST-Anfrage an den Endpunkt `/authoring/destination-servers` senden.

**API-Format**

```http
POST /authoring/destination-servers
```

**Anfrage**

Die folgende Anfrage erstellt eine neue Ziel-Server-Konfiguration, die durch die in der Payload bereitgestellten Parameter konfiguriert wird. Die nachstehende Payload enthält alle Parameter, die vom Endpunkt `/authoring/destination-servers` akzeptiert werden. Beachten Sie, dass Sie nicht alle Parameter für den Aufruf hinzufügen müssen und dass die Vorlage entsprechend Ihren API-Anforderungen angepasst werden kann.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"ADLS destination server",
   "destinationServerType":"FILE_BASED_ADLS_GEN2",
   "fileBasedAdlsGen2Destination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   },
  "fileConfigurations": {
        "compression": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            }
        }
    }
}
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zu Ihrer neu erstellten Ziel-Server-Konfiguration zurück.
+++

### [!DNL Data Landing Zone] (DLZ) Beispiel-Konfiguration des Zielservers {#dlz-server-sample}

+++Beispiel für ein [!DNL Data Landing Zone (DLZ)] Zielserverkonfiguration

[!DNL Data Landing Zone] ([!DNL DLZ]) ist eine von Adobe Experience Platform bereitgestellte [!DNL Azure Blob]-Speicherschnittstelle, die Ihnen Zugriff auf eine sichere, Cloud-basierte Dateispeichereinrichtung gewährt, um Dateien in Platform zu laden.

Sie können eine neue DLZ-Ziel-Server-Konfiguration erstellen, indem Sie eine POST-Anfrage an den Endpunkt `/authoring/destination-servers` senden.

**API-Format**

```http
POST /authoring/destination-servers
```

**Anfrage**

Die folgende Anfrage erstellt eine neue Ziel-Server-Konfiguration, die durch die in der Payload bereitgestellten Parameter konfiguriert wird. Die nachstehende Payload enthält alle Parameter, die vom Endpunkt `/authoring/destination-servers` akzeptiert werden. Beachten Sie, dass Sie nicht alle Parameter für den Aufruf hinzufügen müssen und dass die Vorlage entsprechend Ihren API-Anforderungen angepasst werden kann.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"DLZ destination server",
   "destinationServerType":"FILE_BASED_DLZ",
   "fileBasedDlzDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "useCase": "Your use case"
   },
   "fileConfigurations": {
        "compression": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            }
        }
    }
}
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zu Ihrer neu erstellten Ziel-Server-Konfiguration zurück.
+++

## Auflisten von Ziel-Server-Konfigurationen {#retrieve-list}

Sie können eine Liste aller Ziel-Server-Konfigurationen für Ihre IMS-Organisation abrufen, indem Sie eine GET-Anfrage an den Endpunkt `/authoring/destination-servers` senden.

**API-Format**

```http
GET /authoring/destination-servers
```

**Anfrage**

Mit der folgenden Anfrage wird die Liste der Ziel-Server-Konfigurationen abgerufen, auf die Sie Zugriff haben, basierend auf der IMS-Organisation und der Sandbox-Konfiguration.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Die folgende Antwort gibt den HTTP-Status 200 mit einer Liste der Ziel-Server-Konfigurationen zurück, auf die Sie Zugriff haben, basierend auf der von Ihnen verwendeten IMS-Organisations-ID und dem Sandbox-Namen. Eine `instanceId` entspricht der Vorlage für einen Ziel-Server. Die Antwort wird verkürzt angegeben.

```json
{
   "items":[
      {
         "instanceId":"2307ec2b-4798-45a4-9239-5d0a2fb0ed67",
         "createdDate":"2020-11-17T06:49:24.331012Z",
         "lastModifiedDate":"2020-11-17T06:49:24.331012Z",
         "name":"Moviestar Destination Server",
         "destinationServerType":"URL_BASED",
         "urlBasedDestination":{
            "url":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"https://go.{% if destination.config.domain == \"US\" %}moviestar.com{% else %}moviestar.eu{% endif%}/api/named_users/tags"
            }
         },
         "httpTemplate":{
            "requestBody":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{ \"audience\": { \"named_user_id\": [ {% for named_user in input.profile.identityMap.named_user_id %} \"{{ named_user.id }}\"{% if not loop.last %},{% endif %} {% endfor %} ] }, {% if addedSegments(input.profile.segmentMembership.ups) is not empty %} \"add\": { \"adobe-segments\": [ {% for added_segment in addedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[added_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} {% if addedSegments(input.profile.segmentMembership.ups) is not empty and removedSegments(input.profile.segmentMembership.ups) is not empty %} , {% endif %} {% if removedSegments(input.profile.segmentMembership.ups) is not empty %} \"remove\": { \"adobe-segments\": [ {% for removed_segment in removedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[removed_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} }"
            },
            "httpMethod":"POST",
            "contentType":"application/json",
            "headers":[
               {
                  "header":"Accept",
                  "value":{
                     "templatingStrategy":"NONE",
                     "value":"application/vnd.moviestar+json; version=3;"
                  }
               }
            ]
         },
         "qos":{
            "name":"freeform"
         }
      },
      {
         "instanceId":"d88de647-a352-4824-8b46-354afc7acbff",
         "createdDate":"2020-11-17T16:50:59.635228Z",
         "lastModifiedDate":"2020-11-17T16:50:59.635228Z",
         "name":"Test11 Destination Server",
         "destinationServerType":"URL_BASED",
         "urlBasedDestination":{
            "url":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"https://go.{% if destination.config.domain == \"US\" %}moviestar.com{% else %}moviestar.eu{% endif%}/api/named_users/tags"
            }
         },
         "httpTemplate":{
            "requestBody":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{ \"audience\": { \"named_user_id\": [ {% for named_user in input.profile.identityMap.named_user_id %} \"{{ named_user.id }}\"{% if not loop.last %},{% endif %} {% endfor %} ] }, {% if addedSegments(input.profile.segmentMembership.ups) is not empty %} \"add\": { \"adobe-segments\": [ {% for added_segment in addedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[added_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} {% if addedSegments(input.profile.segmentMembership.ups) is not empty and removedSegments(input.profile.segmentMembership.ups) is not empty %} , {% endif %} {% if removedSegments(input.profile.segmentMembership.ups) is not empty %} \"remove\": { \"adobe-segments\": [ {% for removed_segment in removedSegments(input.profile.segmentMembership.ups) %} \"{{ destination.segmentNames[removed_segment.key] }}\"{% if not loop.last %},{% endif %} {% endfor %} ] } {% endif %} }"
            },
            "httpMethod":"POST",
            "contentType":"application/json",
            "headers":[
               {
                  "header":"Accept",
                  "value":{
                     "templatingStrategy":"NONE",
                     "value":"application/vnd.moviestar+json; version=3;"
                  }
               }
            ]
         },
         "qos":{
            "name":"freeform"
         }
      }
   ]
}
    
```

## Aktualisieren einer vorhandenen Ziel-Server-Konfiguration {#update}

Sie können eine vorhandene Ziel-Server-Konfiguration aktualisieren, indem Sie eine PUT-Anfrage an den Endpunkt `/authoring/destination-servers` senden und die Instanz-ID der Ziel-Server-Konfiguration angeben, die Sie aktualisieren möchten. Geben Sie im Hauptteil des Aufrufs die aktualisierte Ziel-Server-Konfiguration an.

**API-Format**

```http
PUT /authoring/destination-servers/{INSTANCE_ID}
```

| Parameter | Beschreibung |
| -------- | ----------- |
| `{INSTANCE_ID}` | Die ID des Ziel-Servers, den Sie aktualisieren möchten. |

**Anfrage**

Die folgende Anfrage aktualisiert eine vorhandene Ziel-Server-Konfiguration, die durch die in der Payload bereitgestellten Parameter konfiguriert wird.

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.region}}/items"
      }
   },
   "httpTemplate":{
      "httpMethod":"POST",
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{ \"attributes\": [ {% for ns in [\"external_id\", \"yourdestination_id\"] %} {% if input.profile.identityMap[ns] is not empty and first_namespace_encountered %} , {% endif %} {% set first_namespace_encountered = true %} {% for identity in input.profile.identityMap[ns]%} { \"{{ ns }}\": \"{{ identity.id }}\" {% if input.profile.segmentMembership.ups is not empty %} , \"AEPSegments\": { \"add\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"realized\" or segment.value.status == \"existing\" %} {% if added_segment_found %} , {% endif %} {% set added_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ], \"remove\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"exited\" %} {% if removed_segment_found %} , {% endif %} {% set removed_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ] } {% set removed_segment_found = false %} {% set added_segment_found = false %} {% endif %} {% if input.profile.attributes is not empty %} , {% endif %} {% for attribute in input.profile.attributes %} \"{{ attribute.key }}\": {% if attribute.value is empty %} null {% else %} \"{{ attribute.value.value }}\" {% endif %} {% if not loop.last%} , {% endif %} {% endfor %} } {% if not loop.last %} , {% endif %} {% endfor %} {% endfor %} ] }"
      },
      "contentType":"application/json"
   }
}
```

## Abrufen einer bestimmten Ziel-Server-Konfiguration {#get}

Sie können detaillierte Informationen zu einer bestimmten Ziel-Server-Konfiguration abrufen, indem Sie eine GET-Anfrage an den Endpunkt `/authoring/destination-servers` senden und die Instanz-ID der Ziel-Server-Konfiguration angeben, die Sie aktualisieren möchten.

**API-Format**

```http
GET /authoring/destination-servers/{INSTANCE_ID}
```

| Parameter | Beschreibung |
| -------- | ----------- |
| `{INSTANCE_ID}` | Die ID der Ziel-Server-Konfiguration, die Sie abrufen möchten. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destination-servers/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort enthält den HTTP-Status 200 mit detaillierten Informationen zur angegebenen Ziel-Server-Konfiguration.

```json
{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.region}}/items"
      }
   },
   "httpTemplate":{
      "httpMethod":"POST",
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{ \"attributes\": [ {% for ns in [\"external_id\", \"yourdestination_id\"] %} {% if input.profile.identityMap[ns] is not empty and first_namespace_encountered %} , {% endif %} {% set first_namespace_encountered = true %} {% for identity in input.profile.identityMap[ns]%} { \"{{ ns }}\": \"{{ identity.id }}\" {% if input.profile.segmentMembership.ups is not empty %} , \"AEPSegments\": { \"add\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"realized\" or segment.value.status == \"existing\" %} {% if added_segment_found %} , {% endif %} {% set added_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ], \"remove\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"exited\" %} {% if removed_segment_found %} , {% endif %} {% set removed_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ] } {% set removed_segment_found = false %} {% set added_segment_found = false %} {% endif %} {% if input.profile.attributes is not empty %} , {% endif %} {% for attribute in input.profile.attributes %} \"{{ attribute.key }}\": {% if attribute.value is empty %} null {% else %} \"{{ attribute.value.value }}\" {% endif %} {% if not loop.last%} , {% endif %} {% endfor %} } {% if not loop.last %} , {% endif %} {% endfor %} {% endfor %} ] }"
      },
      "contentType":"application/json"
   }
}
```

## Löschen einer bestimmten Ziel-Server-Konfiguration {#delete}

Sie können die angegebene Ziel-Server-Konfiguration löschen, indem Sie eine DELETE-Anfrage an den Endpunkt `/authoring/destination-servers` senden und im Anfragepfad die ID der Ziel-Server-Konfiguration angeben, die Sie löschen möchten.

**API-Format**

```http
DELETE /authoring/destination-servers/{INSTANCE_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{INSTANCE_ID}` | Die `id` der Ziel-Server-Konfiguration, die Sie löschen möchten. |

**Anfrage**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destination-servers/bd4ec8f0-e98f-4b6a-8064-dd7adbfffec9 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 zusammen mit einer leeren HTTP-Antwort zurück.

## Umgang mit API-Fehlern

Destination SDK-API-Endpunkte folgen den allgemeinen Grundsätzen von Experience Platform API-Fehlermeldungen. Siehe [API-Status-Codes](../../landing/troubleshooting.md#api-status-codes) und [Fehler im Anfrage-Header](../../landing/troubleshooting.md#request-header-errors) in der Anleitung zur Fehlerbehebung für Platform.

## Nächste Schritte

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie Ihren Ziel-Server konfigurieren und Vorlagen mithilfe des API-Endpunkts `/authoring/destination-servers` erstellen. Lesen Sie [Verwendung des Destination SDK zum Konfigurieren Ihres Ziels](./configure-destination-instructions.md), um zu verstehen, wo dieser Schritt in den Prozess der Konfiguration Ihres Ziels passt.
