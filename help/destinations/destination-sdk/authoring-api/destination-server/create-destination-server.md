---
description: Auf dieser Seite wird der API-Aufruf zum Erstellen eines Ziel-Servers über Adobe Experience Platform Destination SDK erläutert.
title: Erstellen einer Ziel-Server-Konfiguration
source-git-commit: cadffd60093eef9fb2dcf4562b1fd7611e61da94
workflow-type: tm+mt
source-wordcount: '2039'
ht-degree: 89%

---


# Erstellen einer Ziel-Server-Konfiguration

Das Erstellen eines Ziel-Servers ist der erste Schritt beim Erstellen eines eigenen Ziels mit Destination SDK. Der Ziel-Server enthält Konfigurationsoptionen für die Spezifikationen von [Server](../../functionality/destination-server/server-specs.md) und [Vorlagen](../../functionality/destination-server/templating-specs.md) sowie die Optionen für das [Nachrichtenformat](../../functionality/destination-server/message-format.md)und die [Dateiformatierung](../../functionality/destination-server/file-formatting.md) (für dateibasierte Ziele).

Auf dieser Seite werden die API-Anfrage und die Payload erläutert, die Sie verwenden können, um mithilfe des API-Endpunkts `/authoring/destination-servers` Ihren eigenen Ziel-Server zu erstellen.

Eine ausführliche Beschreibung der Funktionen, die Sie über diesen Endpunkt konfigurieren können, finden Sie in den folgenden Artikeln:

* [Server-Spezifikationen für Ziele, die mit Destination SDK erstellt wurden](../../../destination-sdk/functionality/destination-server/server-specs.md)
* [Vorlagenspezifikationen für Ziele, die mit Destination SDK erstellt wurden](../../../destination-sdk/functionality/destination-server/templating-specs.md)
* [Nachrichtenformat](../../../destination-sdk/functionality/destination-server/message-format.md)
* [Konfiguration der Dateiformatierung](../../../destination-sdk/functionality/destination-server/file-formatting.md)

>[!IMPORTANT]
>
>Bei allen von Destination SDK unterstützten Parameternamen und Werten wird **nach Groß-/Kleinschreibung unterschieden**. Um Fehler bei der Groß-/Kleinschreibung zu vermeiden, verwenden Sie bitte die Parameternamen und -werte genau wie in der Dokumentation dargestellt.

## Erste Schritte mit API-Vorgängen für Ziel-Server {#get-started}

Bevor Sie fortfahren, lesen Sie [Erste Schritte](../../getting-started.md) für wichtige Informationen, die Sie benötigen, um die API erfolgreich aufrufen zu können, einschließlich Informationen zum Abrufen der erforderlichen Authoring-Berechtigung für Ziele und der erforderlichen Kopfzeilen.

## Erstellen einer Ziel-Server-Konfiguration {#create}

Sie können eine neue Ziel-Server-Konfiguration erstellen, indem Sie eine `POST`-Anfrage an den Endpunkt `/authoring/destination-servers` stellen.

>[!TIP]
>
>**API-Endpunkt**: `platform.adobe.io/data/core/activation/authoring/destination-servers`

**API-Format**

```http
POST /authoring/destination-servers
```

Je nach dem von Ihnen erstellten Zieltyp müssen Sie einen etwas anderen Ziel-Server-Typ konfigurieren.

### Erstellen von Ziel-Servern für statische Schemata {#static-destination-servers}

In den folgenden Registerkarten finden Sie Beispiele von Ziel-Servern für Ziele, die [statische Schemata](../../functionality/destination-configuration/schema-configuration.md#attributes-schema) verwenden.

Die folgenden Beispiel-Payloads enthalten alle Parameter, die von den einzelnen Ziel-Server-Typen unterstützt werden. Sie müssen nicht alle Parameter in Ihre Anfrage einbeziehen. Die Payload kann entsprechend Ihren Anforderungen angepasst werden.

Wählen Sie die einzelnen Registerkarten unten aus, um die entsprechenden API-Anfragen anzuzeigen.

>[!BEGINTABS]

>[!TAB Echtzeit (Streaming)]

**Erstellen eines Echtzeit-Ziel-Servers (Streaming)**

Sie müssen einen Echtzeit-Ziel-Server (Streaming) erstellen, der dem unten gezeigten ähnelt, wenn Sie eine Echtzeit-API-basierte Integration (Streaming) konfigurieren.

+++Anfrage

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
| `name` | Zeichenfolge | *Erforderlich.* Stellt einen Anzeigenamen Ihres Servers dar, der nur für Adobe sichtbar ist. Dieser Name ist weder für Partner noch für Kundinnen und Kunden sichtbar. Beispiel `Moviestar destination server`. |
| `destinationServerType` | Zeichenfolge | *Erforderlich.* Legen Sie dies für Echtzeit-Ziele (Streaming) auf `URL_BASED` fest. |
| `urlBasedDestination.url.templatingStrategy` | Zeichenfolge | *Erforderlich.* <ul><li>Verwenden Sie `PEBBLE_V1`, wenn Adobe die URL im nachstehenden Feld `value` umwandeln muss. Verwenden Sie diese Option, wenn Sie einen Endpunkt wie `https://api.moviestar.com/data/{{customerData.region}}/items` haben, wobei der Teil `region` je nach Kundschaft unterschiedlich sein kann. In diesem Fall müssen Sie in der [Zielkonfiguration ] auch `region` als [Kundendatenfeld](../../functionality/destination-configuration/customer-data-fields.md) konfigurieren. (../destination-configuration/create-destination-configuration.md. </li><li> Verwenden Sie `NONE`, wenn von Adobe keine Umwandlung erforderlich ist, z. B. wenn Sie folgenden Endpunkt haben: `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | Zeichenfolge | *Erforderlich.* Geben Sie die Adresse des API-Endpunkts ein, mit dem sich Experience Platform verbinden soll. |
| `httpTemplate.httpMethod` | Zeichenfolge | *Erforderlich.* Die Methode, die Adobe bei Aufrufen an Ihren Server verwendet. Es gibt die Optionen `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `httpTemplate.requestBody.templatingStrategy` | Zeichenfolge | *Erforderlich.* Verwenden Sie `PEBBLE_V1`. |
| `httpTemplate.requestBody.value` | Zeichenfolge | *Erforderlich.* Diese Zeichenfolge ist die Version mit Escape-Zeichen, die die Daten von Platform-Kundinnen und -Kunden in das Format umwandelt, das Ihr Service erwartet. <br> <ul><li> Informationen zum Schreiben der Vorlage finden Sie im Abschnitt [Verwenden von Vorlagen](../../functionality/destination-server/message-format.md#using-templating). </li><li> Weitere Informationen zu Escape-Zeichen finden Sie unter [RFC JSON-Standard, Abschnitt 7](https://tools.ietf.org/html/rfc8259#section-7). </li><li> Ein Beispiel für eine einfache Umwandlung finden Sie im unter [Umwandlung von Profilattributen](../../functionality/destination-server/message-format.md#attributes). </li></ul> |
| `httpTemplate.contentType` | Zeichenfolge | *Erforderlich.* Der Content-Typ, den Ihr Server akzeptiert. Dieser Wert ist höchstwahrscheinlich `application/json`. |

{style="table-layout:auto"}

+++

+++Antwort

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zu Ihrer neu erstellten Ziel-Server-Konfiguration zurück.

+++

>[!TAB Amazon S3]

**Erstellen eines Amazon S3-Ziel-Servers**

Sie müssen beim Konfigurieren eines dateibasierten [!DNL Amazon S3]-Ziels einen [!DNL Amazon S3]-Ziel-Server ähnlich dem unten gezeigten erstellen.

+++Anfrage

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

| Parameter | Typ | Beschreibung |
|---|---|---|
| `name` | Zeichenfolge | Der Name Ihrer Zielverbindung. |
| `destinationServerType` | Zeichenfolge | Legen Sie diesen Wert entsprechend Ihrer Zielplattform fest. Wählen Sie für [!DNL Amazon S3] den Wert `FILE_BASED_S3`. |
| `fileBasedS3Destination.bucket.templatingStrategy` | Zeichenfolge | *Erforderlich.* Verwenden Sie `PEBBLE_V1`. |
| `fileBasedS3Destination.bucket.value` | Zeichenfolge | Der Name des [!DNL Amazon S3]-Buckets, der von diesem Ziel verwendet werden soll. |
| `fileBasedS3Destination.path.templatingStrategy` | Zeichenfolge | *Erforderlich.* Verwenden Sie `PEBBLE_V1`. |
| `fileBasedS3Destination.path.value` | Zeichenfolge | Der Pfad zum Zielordner, in dem die exportierten Dateien gespeichert werden. |
| `fileConfigurations` | K. A. | Siehe [Dateiformatierungskonfiguration](../../functionality/destination-server/file-formatting.md) für detaillierte Informationen zur Konfiguration dieser Einstellungen. |

{style="table-layout:auto"}

+++

+++Antwort

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zu Ihrer neu erstellten Ziel-Server-Konfiguration zurück.

+++

>[!TAB SFTP]

**Erstellen eines [!DNL SFTP] Ziel-Servers**

Sie müssen beim Konfigurieren eines dateibasierten [!DNL SFTP]-Ziels einen [!DNL SFTP]-Ziel-Server ähnlich dem unten gezeigten erstellen.

+++Anfrage

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
   "fileBasedSFTPDestination":{
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

| Parameter | Typ | Beschreibung |
|---|---|---|
| `name` | Zeichenfolge | Der Name Ihrer Zielverbindung. |
| `destinationServerType` | Zeichenfolge | Legen Sie diesen Wert entsprechend Ihrer Zielplattform fest. Wählen Sie für [!DNL SFTP]-Ziele `FILE_BASED_SFTP`. |
| `fileBasedSFTPDestination.rootDirectory.templatingStrategy` | Zeichenfolge | *Erforderlich.* Verwenden Sie `PEBBLE_V1`. |
| `fileBasedSFTPDestination.rootDirectory.value` | Zeichenfolge | Das Stammverzeichnis des Zielspeichers. |
| `fileBasedSFTPDestination.hostName.templatingStrategy` | Zeichenfolge | *Erforderlich.* Verwenden Sie `PEBBLE_V1`. |
| `fileBasedSFTPDestination.hostName.value` | Zeichenfolge | Der Host-Name des Zielspeichers. |
| `port` | Ganzzahl | Der SFTP-Datei-Server-Port. |
| `encryptionMode` | Zeichenfolge | Gibt an, ob eine Dateiverschlüsselung verwendet werden soll. Unterstützte Werte: <ul><li>PGP</li><li>Keine</li></ul> |
| `fileConfigurations` | K. A. | Siehe [Dateiformatierungskonfiguration](../../functionality/destination-server/file-formatting.md) für detaillierte Informationen zur Konfiguration dieser Einstellungen. |

{style="table-layout:auto"}

+++

+++Antwort

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zu Ihrer neu erstellten Ziel-Server-Konfiguration zurück.

+++

>[!TAB Azure Data Lake Storage]

**Erstellen eines [!DNL Azure Data Lake Storage] Ziel-Servers**

Sie müssen beim Konfigurieren eines dateibasierten [!DNL Azure Data Lake Storage]-Ziels einen [!DNL Azure Data Lake Storage]-Ziel-Server ähnlich dem unten gezeigten erstellen.

+++Anfrage

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

| Parameter | Typ | Beschreibung |
|---|---|---|
| `name` | Zeichenfolge | Der Name Ihrer Zielverbindung. |
| `destinationServerType` | Zeichenfolge | Legen Sie diesen Wert entsprechend Ihrer Zielplattform fest. Wählen Sie für [!DNL Azure Data Lake Storage]-Ziele `FILE_BASED_ADLS_GEN2`. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | Zeichenfolge | *Erforderlich.* Verwenden Sie `PEBBLE_V1`. |
| `fileBasedAdlsGen2Destination.path.value` | Zeichenfolge | Der Pfad zum Zielordner, in dem die exportierten Dateien gespeichert werden. |
| `fileConfigurations` | K. A. | Siehe [Dateiformatierungskonfiguration](../../functionality/destination-server/file-formatting.md) für detaillierte Informationen zur Konfiguration dieser Einstellungen. |

{style="table-layout:auto"}

+++

+++Antwort

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zu Ihrer neu erstellten Ziel-Server-Konfiguration zurück.

+++

>[!TAB Azure-Blobspeicher]

**Erstellen eines [!DNL Azure Blob Storage] Ziel-Servers**

Sie müssen beim Konfigurieren eines dateibasierten [!DNL Azure Blob Storage]-Ziels einen [!DNL Azure Blob Storage]-Ziel-Server ähnlich dem unten gezeigten erstellen.

+++Anfrage

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

| Parameter | Typ | Beschreibung |
|---|---|---|
| `name` | Zeichenfolge | Der Name Ihrer Zielverbindung. |
| `destinationServerType` | Zeichenfolge | Legen Sie diesen Wert entsprechend Ihrer Zielplattform fest. Wählen Sie für [!DNL Azure Blob Storage]-Ziele `FILE_BASED_AZURE_BLOB`. |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | Zeichenfolge | *Erforderlich.* Verwenden Sie `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.path.value` | Zeichenfolge | Der Pfad zum Zielordner, in dem die exportierten Dateien gespeichert werden. |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | Zeichenfolge | *Erforderlich.* Verwenden Sie `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.container.value` | Zeichenfolge | Der Name des [!DNL Azure Blob Storage]-Containers, der von diesem Ziel verwendet werden soll. |
| `fileConfigurations` | K. A. | Siehe [Dateiformatierungskonfiguration](../../functionality/destination-server/file-formatting.md) für detaillierte Informationen zur Konfiguration dieser Einstellungen. |

{style="table-layout:auto"}

+++

+++Antwort

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zu Ihrer neu erstellten Ziel-Server-Konfiguration zurück.

+++

>[!TAB Data Landing Zone (DLZ)]

**Erstellen eines [!DNL Data Landing Zone (DLZ)]-Ziel-Servers**

Sie müssen beim Konfigurieren eines dateibasierten [!DNL Data Landing Zone (DLZ)]-Ziels einen [!DNL Data Landing Zone (DLZ)]-Ziel-Server ähnlich dem unten gezeigten erstellen.

+++Anfrage

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

| Parameter | Typ | Beschreibung |
|---|---|---|
| `name` | Zeichenfolge | Der Name Ihrer Zielverbindung. |
| `destinationServerType` | Zeichenfolge | Legen Sie diesen Wert entsprechend Ihrer Zielplattform fest. Wählen Sie für [!DNL Data Landing Zone]-Ziele `FILE_BASED_DLZ`. |
| `fileBasedDlzDestination.path.templatingStrategy` | Zeichenfolge | *Erforderlich.*  Verwenden Sie `PEBBLE_V1`. |
| `fileBasedDlzDestination.path.value` | Zeichenfolge | Der Pfad zum Zielordner, in dem die exportierten Dateien gespeichert werden. |
| `fileConfigurations` | K. A. | Siehe [Dateiformatierungskonfiguration](../../functionality/destination-server/file-formatting.md) für detaillierte Informationen zur Konfiguration dieser Einstellungen. |

{style="table-layout:auto"}

+++

+++Antwort

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zu Ihrer neu erstellten Ziel-Server-Konfiguration zurück.

+++

>[!TAB Google Cloud Storage]

**Erstellen eines [!DNL Google Cloud Storage]-Ziel-Servers**

Sie müssen beim Konfigurieren eines dateibasierten [!DNL Google Cloud Storage]-Ziels einen [!DNL Google Cloud Storage]-Ziel-Server ähnlich dem unten gezeigten erstellen.

+++Anfrage

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Google Cloud Storage Server",
   "destinationServerType":"FILE_BASED_GOOGLE_CLOUD",
   "fileBasedGoogleCloudStorageDestination":{
      "bucket":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.bucket}}"
      },
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

| Parameter | Typ | Beschreibung |
|---|---|---|
| `name` | Zeichenfolge | Der Name Ihrer Zielverbindung. |
| `destinationServerType` | Zeichenfolge | Legen Sie diesen Wert entsprechend Ihrer Zielplattform fest. Wählen Sie für [!DNL Google Cloud Storage]-Ziele `FILE_BASED_GOOGLE_CLOUD`. |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | Zeichenfolge | *Erforderlich.*  Verwenden Sie `PEBBLE_V1`. |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | Zeichenfolge | Der Name des [!DNL Google Cloud Storage]-Buckets, der von diesem Ziel verwendet werden soll. |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | Zeichenfolge | *Erforderlich.* Verwenden Sie `PEBBLE_V1`. |
| `fileBasedGoogleCloudStorageDestination.path.value` | Zeichenfolge | Der Pfad zum Zielordner, in dem die exportierten Dateien gespeichert werden. |
| `fileConfigurations` | K. A. | Siehe [Dateiformatierungskonfiguration](../../functionality/destination-server/file-formatting.md) für detaillierte Informationen zur Konfiguration dieser Einstellungen. |

{style="table-layout:auto"}

+++

+++Antwort

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zu Ihrer neu erstellten Ziel-Server-Konfiguration zurück.

+++

>[!ENDTABS]

### Erstellen von dynamischen Schema-Ziel-Servern {#dynamic-schema-servers}

Mit dynamischen Schemata können Sie die unterstützten Zielattribute dynamisch abrufen und Schemata basierend auf Ihrer eigenen API generieren. Sie müssen einen Ziel-Server für dynamische Schemata konfigurieren, bevor Sie das Schema konfigurieren können.

Auf der Registerkarte unten finden Sie ein Beispiel für einen Ziel-Server für Ziele, die [dynamische Schemata](../../functionality/destination-configuration/schema-configuration.md#dynamic-schema-configuration) verwenden.

Die nachstehende Beispiel-Payload enthält alle Parameter, die für einen dynamischen Schema-Server erforderlich sind.

>[!BEGINTABS]

>[!TAB Dynamischer Schema-Server]

**Erstellen eines dynamischen Schema-Servers**

Sie müssen einen dynamischen Schema-Server ähnlich dem folgenden erstellen, wenn Sie ein Ziel konfigurieren, das sein Profilschema aus Ihrem eigenen API-Endpunkt abruft. Im Gegensatz zu statischen Schemata verwendet ein dynamisches Schema kein Array `profileFields`. Stattdessen verwenden dynamische Schemata einen dynamischen Schema-Server, der eine Verbindung zu Ihrer eigenen API herstellt, von der aus die Schemakonfiguration abgerufen wird.

+++Anfrage

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Dynamic Schema Server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://YOUR_API_ENDPOINT/"
      }
   },
   "httpTemplate":{
      "httpMethod":"GET"
   },
   "responseFields":[
      {
         "templatingStrategy":"PEBBLE_V1",
         "value":"{\n    \"type\":\"object\",\n    \"title\": \"Contact Schema\",\n    \"properties\": {\n        {% for setDefinition in response.body.items %}\n            \"{{setDefinition.key}}\": {\n                \"title\" : \"{{setDefinition.name.value}}\",\n                \"type\" : \"object\",\n                \"properties\": {\n                    {% for attribute in setDefinition.attributes %}\n                        \"{{attribute.key}}\": {\n                            \"title\" : \"{{attribute.name.value}}\",\n                            \"type\" : \"string\"\n                        }\n                        {% if not loop.last %},{%endif%}\n                    {% endfor %}\n                }\n            }\n            {% if not loop.last %},{%endif%}\n        {% endfor %}\n    }\n}",
         "name":"schema"
      }
   ]
}
```

| Parameter | Typ | Beschreibung |
| -------- | ----------- | ----------- |
| `name` | Zeichenfolge | *Erforderlich.* Stellt einen Anzeigenamen Ihres dynamischen Schema-Servers dar, der nur für Adobe sichtbar ist. |
| `destinationServerType` | Zeichenfolge | *Erforderlich.* Setzen Sie dies für dynamische Schema-Server auf `URL_BASED`. |
| `urlBasedDestination.url.templatingStrategy` | Zeichenfolge | *Erforderlich.* <ul><li>Verwenden Sie `PEBBLE_V1`, wenn Adobe die URL im nachstehenden Feld `value` umwandeln muss. Verwenden Sie diese Option, wenn Sie folgenden Endpunkt haben: `https://api.moviestar.com/data/{{customerData.region}}/items`. </li><li> Verwenden Sie `NONE`, wenn von Adobe keine Umwandlung erforderlich ist, z. B. wenn Sie folgenden Endpunkt haben: `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | Zeichenfolge | *Erforderlich.* Füllen Sie im Zuordnungs-Schritt des Aktivierungs-Workflows die Adresse des API-Endpunkts aus, mit dem sich Experience Platform verbinden soll, und rufen Sie die Schemafelder ab, die als Zielfelder ausgefüllt werden sollen. |
| `httpTemplate.httpMethod` | Zeichenfolge | *Erforderlich.* Die Methode, die Adobe bei Aufrufen an Ihren Server verwendet. Verwenden Sie für dynamische Schema-Server `GET`. |
| `responseFields.templatingStrategy` | Zeichenfolge | *Erforderlich.* Verwenden Sie `PEBBLE_V1`. |
| `responseFields.value` | Zeichenfolge | *Erforderlich.* Diese Zeichenfolge ist die Umwandlungsvorlage mit Escape-Zeichen, die die von der Partner-API erhaltene Antwort in das Partnerschema umwandelt, das in der Platform-Benutzeroberfläche angezeigt wird. <br> <ul><li> Informationen zum Schreiben der Vorlage finden Sie im Abschnitt [Verwenden von Vorlagen](../../functionality/destination-server/message-format.md#using-templating). </li><li> Weitere Informationen zu Escape-Zeichen finden Sie unter [RFC JSON-Standard, Abschnitt 7](https://tools.ietf.org/html/rfc8259#section-7). </li><li> Ein Beispiel für eine einfache Umwandlung finden Sie im unter [Umwandlung von Profilattributen](../../functionality/destination-server/message-format.md#attributes). </li></ul> |

{style="table-layout:auto"}

+++

+++Antwort

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zu Ihrer neu erstellten Ziel-Server-Konfiguration zurück.

+++


>[!ENDTABS]


### Dynamische Dropdown-Zielserver erstellen {#dynamic-dropdown-servers}

Verwendung [dynamische Dropdown-Listen](../../functionality/destination-configuration/customer-data-fields.md#dynamic-dropdown-selectors) , um Dropdown-Kundendatenfelder dynamisch abzurufen und auszufüllen, basierend auf Ihrer eigenen API. Beispielsweise können Sie eine Liste vorhandener Benutzerkonten abrufen, die Sie für eine Zielverbindung verwenden möchten.

Sie müssen einen Zielserver für dynamische Dropdown-Listen konfigurieren, bevor Sie das Feld für dynamische Dropdown-Kundendaten konfigurieren können.

Auf der Registerkarte unten finden Sie ein Beispiel für einen Zielserver, der verwendet wird, um die Werte, die in einem Dropdown-Selektor angezeigt werden sollen, dynamisch über eine API abzurufen.

Die nachstehende Beispiel-Payload enthält alle Parameter, die für einen dynamischen Schema-Server erforderlich sind.

>[!BEGINTABS]

>[!TAB Dynamischer Dropdown-Server]

**Erstellen eines dynamischen Dropdown-Servers**

Sie müssen einen dynamischen Dropdown-Server erstellen, der dem unten gezeigten ähnelt, wenn Sie ein Ziel konfigurieren, das die Werte für ein Dropdown-Feld für Kundendaten von Ihrem eigenen API-Endpunkt abruft.

+++Anfrage

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Server for dynamic dropdown",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.users}}/items"
      }
   },
   "httpTemplate":{
      "httpMethod":"GET",
      "headers":[
         {
            "header":"Authorization",
            "value":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"My Bearer Token"
            }
         },
         {
            "header":"x-integration",
            "value":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.integrationId}}"
            }
         },
         {
            "header":"Accept",
            "value":{
               "templatingStrategy":"NONE",
               "value":"application/json"
            }
         }
      ]
   },
   "responseFields":[
      {
         "templatingStrategy":"PEBBLE_V1",
         "value":"{% set list = [] %} {% for record in response.body %} {% set list = list|merge([{'name' : record.name, 'value' : record.id }]) %} {% endfor %}{{ {'list': list} | toJson | raw }}",
         "name":"list"
      }
   ]
}
```

| Parameter | Typ | Beschreibung |
| -------- | ----------- | ----------- |
| `name` | Zeichenfolge | *Erforderlich.* Stellt einen Anzeigenamen Ihres dynamischen Dropdown-Servers dar, der nur für Adobe sichtbar ist. |
| `destinationServerType` | Zeichenfolge | *Erforderlich.* Legen Sie `URL_BASED` für dynamische Dropdown-Server. |
| `urlBasedDestination.url.templatingStrategy` | Zeichenfolge | *Erforderlich.* <ul><li>Verwenden Sie `PEBBLE_V1`, wenn Adobe die URL im nachstehenden Feld `value` umwandeln muss. Verwenden Sie diese Option, wenn Sie folgenden Endpunkt haben: `https://api.moviestar.com/data/{{customerData.region}}/items`. </li><li> Verwenden Sie `NONE`, wenn von Adobe keine Umwandlung erforderlich ist, z. B. wenn Sie folgenden Endpunkt haben: `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | Zeichenfolge | *Erforderlich.* Füllen Sie die Adresse des API-Endpunkts aus, mit dem sich Experience Platform verbinden und die Dropdown-Werte abrufen soll. |
| `httpTemplate.httpMethod` | Zeichenfolge | *Erforderlich.* Die Methode, die Adobe bei Aufrufen an Ihren Server verwendet. Verwenden Sie für dynamische Dropdown-Server `GET`. |
| `httpTemplate.headers` | Objekt | *Optional.l* Schließen Sie alle Header ein, die zum Herstellen einer Verbindung mit dem dynamischen Dropdown-Server erforderlich sind. |
| `responseFields.templatingStrategy` | Zeichenfolge | *Erforderlich.* Verwenden Sie `PEBBLE_V1`. |
| `responseFields.value` | Zeichenfolge | *Erforderlich.* Diese Zeichenfolge ist die Umwandlungsvorlage mit Zeichenfolgenzeichen, die die von Ihrer API erhaltene Antwort in die Werte umwandelt, die in der Platform-Benutzeroberfläche angezeigt werden. <br> <ul><li> Informationen zum Schreiben der Vorlage finden Sie im Abschnitt [Verwenden von Vorlagen](../../functionality/destination-server/message-format.md#using-templating). </li><li> Weitere Informationen zu Escape-Zeichen finden Sie unter [RFC JSON-Standard, Abschnitt 7](https://tools.ietf.org/html/rfc8259#section-7). |

{style="table-layout:auto"}

+++

+++Antwort

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zu Ihrer neu erstellten Ziel-Server-Konfiguration zurück.

+++

>[!ENDTABS]

## Umgang mit API-Fehlern {#error-handling}

Destination SDK-API-Endpunkte folgen den allgemeinen Grundsätzen von Experience Platform API-Fehlermeldungen. Siehe [API-Status-Codes](../../../../landing/troubleshooting.md#api-status-codes) und [Fehler im Anfrage-Header](../../../../landing/troubleshooting.md#request-header-errors) in der Anleitung zur Fehlerbehebung für Platform.

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie über den API-Endpunkt `/authoring/destination-servers` von Destination SDK einen neuen Ziel-Server erstellen.

Weitere Informationen dazu, was Sie mit diesem Endpunkt tun können, finden Sie in den folgenden Artikeln:

* [Abrufen einer Ziel-Server-Konfiguration](retrieve-destination-server.md)
* [Aktualisieren einer Ziel-Server-Konfiguration](update-destination-server.md)
* [Löschen einer Ziel-Server-Konfiguration](delete-destination-server.md)

Informationen dazu, wo dieser Endpunkt in den Prozess zur Zielbearbeitung passt, finden Sie in den folgenden Artikeln:

* [Verwenden des Destination SDK zum Konfigurieren eines Streaming-Ziels](../../guides/configure-destination-instructions.md#create-server-template-configuration)
* [Verwenden des Destination SDK zum Konfigurieren eines dateibasierten Ziels](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)