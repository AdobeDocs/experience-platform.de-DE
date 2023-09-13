---
description: Auf dieser Seite wird der API-Aufruf veranschaulicht, mit dem eine vorhandene Ziel-Server-Konfiguration über Adobe Experience Platform Destination SDK aktualisiert wird.
title: Aktualisieren einer Ziel-Server-Konfiguration
source-git-commit: 03ec0e919304c9d46ef88d606eed9e12d1824856
workflow-type: tm+mt
source-wordcount: '1098'
ht-degree: 100%

---


# Aktualisieren einer Ziel-Server-Konfiguration

Auf dieser Seite werden die API-Anfrage und die Payload erläutert, die Sie verwenden können, um eine vorhandene Ziel-Server-Konfiguration mithilfe des API-Endpunkts `/authoring/destination-servers` aktualisieren können.

>[!TIP]
>
>Jeder Aktualisierungsvorgang für produktbezogene/öffentliche Ziele ist erst sichtbar, nachdem Sie die [Publishing-API](../../publishing-api/create-publishing-request.md) verwendet und die Aktualisierung zur Überprüfung durch Adobe eingereicht haben.

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

## Aktualisieren einer Ziel-Server-Konfiguration {#update}

Sie können eine [vorhandene](create-destination-server.md) Ziel-Server-Konfiguration aktualisieren, indem Sie eine `PUT`-Anfrage an den Endpunkt `/authoring/destination-servers` mit der aktualisierten Payload stellen.

>[!TIP]
>
>**API-Endpunkt**: `platform.adobe.io/data/core/activation/authoring/destination-servers`

Um eine vorhandene Ziel-Server-Konfiguration und die zugehörige `{INSTANCE_ID}` abzurufen, lesen Sie den Artikel über das [Abrufen einer Ziel-Server-Konfiguration](retrieve-destination-server.md).

**API-Format**

```http
PUT /authoring/destination-servers/{INSTANCE_ID}
```

| Parameter | Beschreibung |
| -------- | ----------- |
| `{INSTANCE_ID}` | Die ID des Ziel-Servers, den Sie aktualisieren möchten. Um eine vorhandene Ziel-Server-Konfiguration und die zugehörige `{INSTANCE_ID}` abzurufen, lesen Sie den Artikel über das [Abrufen einer Ziel-Server-Konfiguration](retrieve-destination-server.md). |

Die folgenden Anfragen aktualisieren eine vorhandene Ziel-Server-Konfiguration, die durch die in der Payload bereitgestellten Parameter konfiguriert wird.

Wählen Sie die einzelnen Registerkarten unten aus, um die entsprechende Payload anzuzeigen.

>[!BEGINTABS]

>[!TAB Echtzeit (Streaming)]

+++Anfrage

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers\{INSTANCE_ID} \
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
      "httpMethod":"PUT",
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
| `urlBasedDestination.url.templatingStrategy` | Zeichenfolge | *Erforderlich.* <ul><li>Verwenden Sie `PEBBLE_V1`, wenn Adobe die URL im nachstehenden Feld `value` umwandeln muss. Verwenden Sie diese Option, wenn Sie folgenden Endpunkt haben: `https://api.moviestar.com/data/{{customerData.region}}/items`. </li><li> Verwenden Sie `NONE`, wenn von Adobe keine Umwandlung erforderlich ist, z. B. wenn Sie folgenden Endpunkt haben: `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | Zeichenfolge | *Erforderlich.* Geben Sie die Adresse des API-Endpunkts ein, mit dem sich Experience Platform verbinden soll. |
| `httpTemplate.httpMethod` | Zeichenfolge | *Erforderlich.* Die Methode, die Adobe bei Aufrufen an Ihren Server verwendet. Es gibt die Optionen `GET`, `PUT`, `PUT`, `DELETE`, `PATCH`. |
| `httpTemplate.requestBody.templatingStrategy` | Zeichenfolge | *Erforderlich.* Verwenden Sie `PEBBLE_V1`. |
| `httpTemplate.requestBody.value` | Zeichenfolge | *Erforderlich.* Diese Zeichenfolge ist die Version mit Escape-Zeichen, die die Daten von Platform-Kundinnen und -Kunden in das Format umwandelt, das Ihr Service erwartet. <br> <ul><li> Informationen zum Schreiben der Vorlage finden Sie im Abschnitt [Verwenden von Vorlagen](../../functionality/destination-server/message-format.md#using-templating). </li><li> Weitere Informationen zu Escape-Zeichen finden Sie unter [RFC JSON-Standard, Abschnitt 7](https://tools.ietf.org/html/rfc8259#section-7). </li><li> Ein Beispiel für eine einfache Umwandlung finden Sie im unter [Umwandlung von Profilattributen](../../functionality/destination-server/message-format.md#attributes). </li></ul> |
| `httpTemplate.contentType` | Zeichenfolge | *Erforderlich.* Der Content-Typ, den Ihr Server akzeptiert. Dieser Wert ist höchstwahrscheinlich `application/json`. |

{style="table-layout:auto"}

+++

+++Antwort

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit den Details der neu erstellten Ziel-Server-Konfiguration zurückgegeben.

+++

>[!TAB Amazon S3]

+++Anfrage

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers\{INSTANCE_ID} \
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

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit den Details der neu erstellten Ziel-Server-Konfiguration zurückgegeben.

+++

>[!TAB SFTP]

+++Anfrage

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
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

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit den Details der neu erstellten Ziel-Server-Konfiguration zurückgegeben.

+++

>[!TAB Azure Data Lake Storage]

+++Anfrage

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
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

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit den Details der neu erstellten Ziel-Server-Konfiguration zurückgegeben.

+++

>[!TAB Azure-Blobspeicher]

+++Anfrage

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_D} \
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

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit den Details der neu erstellten Ziel-Server-Konfiguration zurückgegeben.

+++

>[!TAB Data Landing Zone (DLZ)]

+++Anfrage

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
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

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit den Details der neu erstellten Ziel-Server-Konfiguration zurückgegeben.

+++

>[!TAB Google Cloud Storage]

+++Anfrage

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
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

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit den Details der neu erstellten Ziel-Server-Konfiguration zurückgegeben.

+++

>[!ENDTABS]

## Umgang mit API-Fehlern {#error-handling}

Destination SDK-API-Endpunkte folgen den allgemeinen Grundsätzen von Experience Platform API-Fehlermeldungen. Siehe [API-Status-Codes](../../../../landing/troubleshooting.md#api-status-codes) und [Fehler im Anfrage-Header](../../../../landing/troubleshooting.md#request-header-errors) in der Anleitung zur Fehlerbehebung für Platform.

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie eine Ziel-Server-Konfiguration über den API-Endpunkt `/authoring/destination-servers` von Destination SDK aktualisieren können.

Weitere Informationen dazu, was Sie mit diesem Endpunkt tun können, finden Sie in den folgenden Artikeln:

* [Erstellen einer Ziel-Server-Konfiguration](create-destination-server.md)
* [Abrufen einer Ziel-Server-Konfiguration](retrieve-destination-server.md)
* [Aktualisieren einer Ziel-Server-Konfiguration](update-destination-server.md)