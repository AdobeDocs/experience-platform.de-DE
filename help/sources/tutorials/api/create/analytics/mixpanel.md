---
keywords: Experience Platform;Startseite;beliebte Themen;Quellen;Connectoren;Quell-Connectoren;Quellen-SDK;SDK
title: (Beta) Erstellen einer Quellverbindung und eines Datenflusses für Mixpanel mithilfe der Flow Service-API
description: Erfahren Sie, wie Sie mit der Flow Service-API Adobe Experience Platform mit Mixpanel verbinden.
exl-id: 804b876d-6fd5-4a28-b33c-4ecab1ba3333
source-git-commit: 23a6f8ee23fb67290a5bcba2673a87ce74c9e1d3
workflow-type: tm+mt
source-wordcount: '2050'
ht-degree: 63%

---

# (Beta) Erstellen Sie eine Quellverbindung und einen Datenfluss für [!DNL Mixpanel] mithilfe der [!DNL Flow Service] API

>[!NOTE]
>
>Die [!DNL Mixpanel] -Quelle befindet sich in der Beta-Phase. Siehe [Quellen - Übersicht](../../../../home.md#terms-and-conditions) für weitere Informationen zur Verwendung von Beta-beschrifteten Quellen.

Das folgende Tutorial führt Sie durch die Schritte zum Erstellen einer Quellverbindung und eines Datenflusses, um [!DNL Mixpanel] Daten an Adobe Experience Platform mithilfe der [Flussdienst-API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um eine erfolgreiche Verbindung zu [!DNL Mixpanel] mithilfe der [!DNL Flow Service] API.

### Sammeln erforderlicher Anmeldeinformationen

Um eine Verbindung zwischen [!DNL Mixpanel] und Platform herzustellen, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Anmeldedaten | Beschreibung | Beispiel |
| --- | --- | --- |
| `username` | Der Benutzername des Dienstkontos, der Ihrer [!DNL Mixpanel] -Konto. Siehe [[!DNL Mixpanel] Dokumentation zu Dienstkonten](https://developer.mixpanel.com/reference/service-accounts#authenticating-with-a-service-account) für weitere Informationen. | `Test8.6d4ee7.mp-service-account` |
| `password` | Das Dienstkontokennwort, das Ihrer [!DNL Mixpanel] -Konto. | `dLlidiKHpCZtJhQDyN2RECKudMeTItX1` |
| `projectId` | Ihre [!DNL Mixpanel] Projekt-ID. Diese ID ist erforderlich, um eine Quellverbindung zu erstellen. Siehe [[!DNL Mixpanel] Dokumentation zu den Projekteinstellungen](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings) und [[!DNL Mixpanel] Handbuch zum Erstellen und Verwalten von Projekten](https://help.mixpanel.com/hc/en-us/articles/115004505106-Create-and-Manage-Projects) für weitere Informationen. | `2384945` |
| `timezone` | Die Zeitzone, die Ihrer [!DNL Mixpanel] Projekt. Zum Erstellen einer Quellverbindung ist eine Zeitzone erforderlich. Siehe [Dokumentation zu den Projekteinstellungen in Mixpanel](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings) für weitere Informationen. | `Pacific Standard Time` |

Weitere Informationen zum Authentifizieren Ihrer [!DNL Mixpanel] -Quelle, siehe [[!DNL Mixpanel] Quellübersicht](../../../../connectors/analytics/mixpanel.md).

## Erstellen einer Basisverbindung {#base-connection}

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basis-Verbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an die `/connections` Endpunkt beim Bereitstellen [!DNL Mixpanel] Authentifizierungsberechtigungen als Teil des Anfragetexts.

**API-Format**

```https
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Mixpanel]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Mixpanel base connection",
      "description": "Mixpanel base connection to authenticate to Platform",
      "connectionSpec": {
          "id": "fd2c8ff3-1de0-4f6b-8fa8-4264784870eb",
          "version": "1.0"
      },
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      }
  }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der Name Ihrer Basisverbindung. Stellen Sie sicher, dass der Name Ihrer Basisverbindung beschreibend ist, da Sie damit Informationen zu Ihrer Basisverbindung nachschlagen können. |
| `description` | Ein optionaler Wert, den Sie angeben können, um weitere Informationen zu Ihrer Basisverbindung bereitzustellen. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID Ihrer Quelle. Diese ID kann abgerufen werden, nachdem Ihre Quelle registriert und über die [!DNL Flow Service]-API genehmigt wurde. |
| `auth.specName` | Der Authentifizierungstyp, mit dem Sie Ihre Quelle für Platform authentifizieren. |
| `auth.params.` | Enthält die Anmeldeinformationen, die zum Authentifizieren Ihrer Quelle erforderlich sind. |
| `auth.params.username` | Der Benutzername, der Ihrem [!DNL Mixpanel]-Konto entspricht. |
| `auth.params.password` | Das Passwort, das Ihrem [!DNL Mixpanel]-Konto entspricht. |

**Antwort**

Eine erfolgreiche Antwort gibt die neu erstellte Basisverbindung zurück, einschließlich ihrer eindeutigen Verbindungskennung (`id`). Diese ID ist erforderlich, um die Dateistruktur und Inhalte Ihrer Quelle im nächsten Schritt zu untersuchen.

```json
{
     "id": "70383d02-2777-4be7-a309-9dd6eea1b46d",
     "etag": "\"d64c8298-add4-4667-9a49-28195b2e2a84\""
}
```

## Durchsuchen der Quelle {#explore}

Mithilfe der im vorherigen Schritt generierten Basisverbindungs-ID können Sie Dateien und Ordner durch Ausführen von GET-Anfragen untersuchen.
Verwenden Sie die folgenden Aufrufe, um den Pfad der Datei zu finden, die in Experience Platform integriert werden soll:

**API-Format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

Bei der Durchführung von GET-Anfragen zur Analyse der Dateistruktur und des Inhalts Ihrer Quelle müssen Sie die in der folgenden Tabelle aufgeführten Abfrageparameter einbeziehen:


| Parameter | Beschreibung |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | Die im vorherigen Schritt generierte Basisverbindungs-ID. |
| `objectType=rest` | Der Typ des Objekts, das Sie untersuchen möchten. Derzeit ist dieser Wert immer auf `rest`. |
| `{OBJECT}` | Dieser Parameter ist nur beim Anzeigen eines bestimmten Ordners erforderlich. Der Wert stellt den Pfad des Ordners dar, den Sie untersuchen möchten. Für diese Quelle würde der Wert `json`. |
| `fileType=json` | Der Dateityp der Datei, die Sie in Platform laden möchten. Zurzeit `json` ist der einzige unterstützte Dateityp. |
| `{PREVIEW}` | Ein boolescher Wert, der definiert, ob der Inhalt der Verbindung die Vorschau unterstützt. |
| `{SOURCE_PARAMS}` | Definiert Parameter für die Quelldatei, die Sie in Platform laden möchten. Um den akzeptierten Formattyp für `{SOURCE_PARAMS}` abzurufen, müssen Sie die gesamte Zeichenfolge `{"projectId":"2671127","timezone":"Pacific Standard Time"}` in base64 kodieren. **Hinweis**: Im folgenden Beispiel: `"{"projectId":"2671127","timezone":"Pacific Standard Time"}"` kodiert in base64 entspricht `eyJwcm9qZWN0SWQiOiIyNjcxMTI3IiwidGltZXpvbmUiOiJQYWNpZmljIFN0YW5kYXJkIFRpbWUifQ==`. |


**Anfrage**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/70383d02-2777-4be7-a309-9dd6eea1b46d/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJsaXN0SWQiOiIxMGMwOTdjYTcxIn0=' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Struktur der abgefragten Datei zurück.

```json
{
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "event": {
                "type": "string"
            },
            "properties": {
                "type": "object",
                "properties": {
                    "$mp_api_endpoint": {
                        "type": "string"
                    },
                    "$insert_id": {
                        "type": "string"
                    },
                    "item_id": {
                        "type": "string"
                    },
                    "distinct_id": {
                        "type": "string"
                    },
                    "$mp_api_timestamp_ms": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "item_price": {
                        "type": "string"
                    },
                    "$import": {
                        "type": "boolean"
                    },
                    "item_name": {
                        "type": "string"
                    },
                    "time": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "mp_processing_time_ms": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    }
                }
            }
        }
    },
    "data": [
        {
            "event": "Items purchased",
            "properties": {
                "time": 1652825148,
                "distinct_id": "test@test.com",
                "$insert_id": "935d87b1-00cd-41b7-be34-b9d98dd08b70",
                "$mp_api_endpoint": "api.mixpanel.com",
                "$mp_api_timestamp_ms": 1652850348643,
                "item_id": "29066",
                "item_name": "charger",
                "item_price": "800.00",
                "mp_processing_time_ms": 1652850348702
            }
        },
        {
            "event": "Items sold",
            "properties": {
                "time": 1652423938,
                "distinct_id": "test@test.com",
                "$insert_id": "935d87b1-00cd-41b7-be34-b9d98dd08b70",
                "$mp_api_endpoint": "api.mixpanel.com",
                "$mp_api_timestamp_ms": 1652449138115,
                "item_id": "29036",
                "item_name": "chair",
                "item_price": "5000.00",
                "mp_processing_time_ms": 1652449138173
            }
        },
        {
            "event": "Items sold",
            "properties": {
                "time": 1652854256,
                "distinct_id": "test@test.com",
                "$insert_id": "935d87b1-00cd-41b7-be34-b9d98dd08b70",
                "$mp_api_endpoint": "api.mixpanel.com",
                "$mp_api_timestamp_ms": 1652879456538,
                "item_id": "29066",
                "item_name": "mobile",
                "item_price": "7000.00",
                "mp_processing_time_ms": 1652879456604
            }
        },
        {
            "event": "Sign off",
            "properties": {
                "time": 1648140611,
                "distinct_id": "test@test.com",
                "$insert_id": "935d87b1-00cd-41b7-be34-b9d98dd08b75",
                "$mp_api_endpoint": "api.mixpanel.com",
                "$mp_api_timestamp_ms": 1648555709515,
                "item_id": "29073",
                "item_name": "Watch",
                "item_price": "50000.00",
                "mp_processing_time_ms": 1648555710375
            }
        },
        {
            "event": "Items sold",
            "properties": {
                "time": 1648140612,
                "distinct_id": "test@test.com",
                "$insert_id": "935d87b1-00cd-41b7-be34-b9d98dd08b75",
                "$mp_api_endpoint": "api.mixpanel.com",
                "$mp_api_timestamp_ms": 1648556481708,
                "item_id": "29073",
                "item_name": "Pen",
                "item_price": "1000.00",
                "mp_processing_time_ms": 1648556481880
            }
        },
        {
            "event": "Sign in",
            "properties": {
                "time": 1648140614,
                "distinct_id": "test1@test.com",
                "$import": true,
                "$insert_id": "935d87b1-00cd-41b7-be34-b9d98dd08b75",
                "$mp_api_endpoint": "api.mixpanel.com",
                "$mp_api_timestamp_ms": 1648556032401,
                "item_id": "29073",
                "item_name": "Watch",
                "item_price": "50000.00",
                "mp_processing_time_ms": 1648556032462
            }
        },
        {
            "event": "Item Purchased",
            "properties": {
                "time": 1648165814,
                "distinct_id": "test1@test.com",
                "$insert_id": "935d87b1-00cd-41b7-be34-b9d98dd08b74",
                "$mp_api_endpoint": "api.mixpanel.com",
                "$mp_api_timestamp_ms": 1648480684785,
                "item_id": "29073",
                "item_name": "Watch",
                "item_price": "50000.00",
                "mp_processing_time_ms": 1648480685058
            }
        },
        {
            "event": "Item Purchased",
            "properties": {
                "time": 1648165814,
                "distinct_id": "test1@test.com",
                "$insert_id": "935d87b1-00cd-41b7-be34-b9d98dd08b75",
                "$mp_api_endpoint": "api.mixpanel.com",
                "$mp_api_timestamp_ms": 1648551687866,
                "item_id": "29073",
                "item_name": "Watch",
                "item_price": "50000.00",
                "mp_processing_time_ms": 1648551687922
            }
        },
        {
            "event": "Sign off",
            "properties": {
                "time": 1648530419,
                "distinct_id": "test1@test.com",
                "$insert_id": "935d87b1-00cd-41b7-be34-b9d98dd08b75",
                "$mp_api_endpoint": "api.mixpanel.com",
                "$mp_api_timestamp_ms": 1648555619274,
                "item_id": "29073",
                "item_name": "Watch",
                "item_price": "50000.00",
                "mp_processing_time_ms": 1648555619326
            }
        },
        {
            "event": "Items sold",
            "properties": {
                "time": 1648566534,
                "distinct_id": "test1@test.com",
                "$import": true,
                "$insert_id": "935d87b1-00cd-41b7-be34-b9d98dd08b75",
                "$mp_api_endpoint": "api.mixpanel.com",
                "$mp_api_timestamp_ms": 1648635830114,
                "item_id": "29073",
                "item_name": "Pen",
                "item_price": "1000.00",
                "mp_processing_time_ms": 1648635831010
            }
        }
    ]
}
```

## Erstellen einer Quellverbindung {#source-connection}

Sie können eine Quellverbindung herstellen, indem Sie eine POST-Anfrage an die [!DNL Flow Service]-API senden. Eine Quellverbindung besteht aus einer Verbindungs-ID, einem Pfad zur Quelldatendatei und einer Verbindungsspezifikations-ID.

**API-Format**

```https
POST /sourceConnections
```

**Anfrage**

Die folgende Anfrage erstellt eine Quellverbindung für [!DNL Mixpanel]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Mixpanel source connection",
      "description": "Mixpanel source connection",
      "baseConnectionId": "70383d02-2777-4be7-a309-9dd6eea1b46d",
      "connectionSpec": {
          "id": "fd2c8ff3-1de0-4f6b-8fa8-4264784870eb",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
          "projectId": "{PROJECT_ID}",
          "timezone": "{TIMEZONE}"
      }
  }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der Name Ihrer Quellverbindung. Stellen Sie sicher, dass der Name Ihrer Quellverbindung beschreibend ist, da Sie damit Informationen zu Ihrer Quellverbindung nachschlagen können. |
| `description` | Ein optionaler Wert, den Sie angeben können, um weitere Informationen über Ihre Quellverbindung bereitzustellen. |
| `baseConnectionId` | Die Basisverbindungs-ID von [!DNL Mixpanel]. Diese ID wurde in einem früheren Schritt generiert. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID, die Ihrer Quelle entspricht. |
| `data.format` | Das Format der [!DNL Mixpanel]-Daten, die Sie aufnehmen möchten. Derzeit wird nur das Datenformat `json` unterstützt. |
| `params.projectId` | Ihre [!DNL Mixpanel] Projekt-ID. |
| `params.timezone` | Die Zeitzone Ihrer [!DNL Mixpanel] Projekt. |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung (`id`) der neu erstellten Quellverbindung zurück. Diese ID ist in einem späteren Schritt erforderlich, um einen Datenfluss zu erstellen.

```json
{
     "id": "246d052c-da4a-494a-937f-a0d17b1c6cf5",
     "etag": "\"712a8c08-fda7-41c2-984b-187f823293d8\""
}
```

## Erstellen eines XDM-Zielschemas {#target-schema}

Damit die Quelldaten in Platform verwendet werden können, muss ein Zielschema erstellt werden, das die Quelldaten entsprechend Ihren Anforderungen strukturiert. Das Zielschema wird dann verwendet, um einen Platform-Datensatz zu erstellen, in dem die Quelldaten enthalten sind.

Ein Ziel-XDM-Schema kann erstellt werden, indem eine POST-Anfrage an die [Schema-Registrierungs-API](https://www.adobe.io/experience-platform-apis/references/schema-registry/) durchgeführt wird.

Ausführliche Schritte zum Erstellen eines XDM-Zielschemas finden Sie im Tutorial zum [Erstellen eines Schemas mithilfe der API](../../../../../xdm/api/schemas.md).

## Erstellen eines Zieldatensatzes {#target-dataset}

Ein Zieldatensatz kann erstellt werden, indem eine POST-Anfrage an die [Catalog Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) durchgeführt wird, wodurch die ID des Zielschemas in der Payload angegeben wird.

Ausführliche Anweisungen zum Erstellen eines Zieldatensatzes finden Sie im Tutorial zu [Erstellen eines Datensatzes mithilfe der API](../../../../../catalog/api/create-dataset.md).

## Erstellen einer Zielverbindung {#target-connection}

Eine Zielverbindung stellt die Verbindung zum Ziel dar, an dem die aufgenommenen Daten gespeichert werden sollen. Um eine Zielverbindung zu erstellen, müssen Sie die ID der Festnetzverbindungsspezifikation angeben, die dem Data Lake entspricht. Diese ID lautet: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Sie verfügen jetzt über die eindeutigen Kennungen eines Zielschemas, eines Zieldatensatzes und der Verbindungsspezifikations-ID zum Data Lake. Anhand dieser Kennungen können Sie mit der [!DNL Flow Service]-API eine Zielverbindung erstellen, um den Datensatz anzugeben, der die eingehenden Quelldaten enthalten wird.

**API-Format**

```https
POST /targetConnections
```

**Anfrage**

Die folgende Anfrage erstellt eine Zielverbindung für [!DNL Mixpanel]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "{Mixpanel} Target Connection",
        "description": "{Mixpanel} Target Connection",
        "connectionSpec": {
            "id": "fd2c8ff3-1de0-4f6b-8fa8-4264784870eb",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "dataSetId": "5ef4551c52e054191a61a99f"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `name` | Der Name Ihrer Zielverbindung. Stellen Sie sicher, dass der Name Ihrer Zielverbindung beschreibend ist, da Sie damit Informationen zu Ihrer Zielverbindung nachschlagen können. |
| `description` | Ein optionaler Wert, den Sie für weitere Informationen zu Ihrer Zielverbindung angeben können. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID, die dem Data Lake entspricht. Diese feste ID lautet: `fd2c8ff3-1de0-4f6b-8fa8-4264784870eb`. |
| `data.format` | Das Format der [!DNL Mixpanel]-Daten, die Sie an Platform übermitteln möchten. |
| `params.dataSetId` | Die Zieldatensatz-ID, die in einem vorherigen Schritt abgerufen wurde. |


**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung der neuen Zielverbindung an (`id`). Diese ID ist in späteren Schritten erforderlich.

```json
{
     "id": "7c96c827-3ffd-460c-a573-e9558f72f263",
     "etag": "\"a196f685-f5e8-4c4c-bfbd-136141bb0c6d\""
}
```

## Erstellen einer Zuordnung {#mapping}

Damit die Quelldaten in einen Zieldatensatz aufgenommen werden können, müssen sie zunächst dem Zielschema zugeordnet werden, zu dem der Zieldatensatz gehört. Dies wird erreicht, indem eine POST-Anfrage an [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) mit Datenzuordnungen, die in der Anfrage-Payload definiert sind.

**API-Format**

```http
POST /conversion/mappingSets
```

**Anfrage**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "version": 0,
      "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
      "xdmVersion": "1.0",
      "id": null,
      "mappings": [
          {
              "sourceType": "ATTRIBUTE",
              "source": "data.distinct_id",
              "destination": "_extconndev.distinct_id",
              "name": "distinct_id",
              "description": "Mixpanel"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "data.event_name",
              "destination": "_extconndev.event_name"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "data.import",
              "destination": "_extconndev.import"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "data.insert_id",
              "destination": "_extconndev.insert_id"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "data.item_id",
              "destination": "_extconndev.item_id"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "data.item_name",
              "destination": "_extconndev.item_name"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "data.item_price",
              "destination": "_extconndev.item_price"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "data.mp_api_endpoint",
              "destination": "_extconndev.mp_api_endpoint"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "data.mp_api_timestamp_ms",
              "destination": "_extconndev.mp_api_timestamp_ms"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "data.mp_processing_time_ms",
              "destination": "_extconndev.mp_processing_time_ms"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "data.time",
              "destination": "_extconndev.time"
          }
      ]
  }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `xdmSchema` | Die ID des [Ziel-XDM-Schema](#target-schema), die in einem früheren Schritt generiert wurde. |
| `mappings.destinationXdmPath` | Der Ziel-XDM-Pfad, dem das Quellattribut zugeordnet wird. |
| `mappings.sourceAttribute` | Das Quellattribut, das einem Ziel-XDM-Pfad zugeordnet werden muss. |
| `mappings.identity` | Ein boolescher Wert, der angibt, ob der Zuordnungssatz für [!DNL Identity Service] markiert wird. |

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Zuordnung an, einschließlich der eindeutigen Kennung (`id`). Dieser Wert ist in einem späteren Schritt zum Erstellen eines Datenflusses erforderlich.

```json
{
    "id": "bf5286a9c1ad4266baca76ba3adc9366",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## Erstellen eines Flusses {#flow}

Der letzte Schritt zur Datenübermittlung von [!DNL Mixpanel] in Platform einen Datenfluss erstellen. Bislang haben Sie die folgenden erforderlichen Werte vorbereitet:

* [Quellverbindungs-ID](#source-connection)
* [Zielverbindungs-ID](#target-connection)
* [Zuordnungs-ID](#mapping)

Ein Datenfluss ist für die Planung und Erfassung von Daten aus einer Quelle verantwortlich. Sie können einen Datenfluss erstellen, indem Sie eine POST-Anfrage ausführen und dabei die oben genannten Werte in der Payload angeben.

Um eine Aufnahme zu planen, legen Sie zunächst den Startzeitwert auf die Epochenzeit in Sekunden fest. Anschließend müssen Sie den Frequenzwert auf eine der fünf Optionen festlegen: `once`, `minute`, `hour`, `day` oder `week`. Der Intervallwert gibt den Zeitraum zwischen zwei aufeinander folgenden Erfassungsschritten an. Für die Erstellung einer einmaligen Erfassung ist jedoch kein Intervall erforderlich. Für alle anderen Frequenzen muss der Intervallwert auf gleich oder größer als `15` festgelegt werden.


**API-Format**

```http
POST /flows
```

**Anfrage**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "{Mixpanel} dataflow",
      "description": "{Mixpanel} dataflow",
      "flowSpec": {
          "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "246d052c-da4a-494a-937f-a0d17b1c6cf5"
      ],
      "targetConnectionIds": [
          "7c96c827-3ffd-460c-a573-e9558f72f263"
      ],
      "transformations": [
          {
              "name": "Mapping",
              "params": {
                  "mappingId": "bf5286a9c1ad4266baca76ba3adc9366",
                  "mappingVersion": "0"
              }
          }
      ],
      "scheduleParams": {
          "startTime": "1625040887",
          "frequency": "minute",
          "interval": 15
      }
  }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der Name Ihres Datenflusses. Stellen Sie sicher, dass der Name Ihres Datenflusses beschreibend ist, da Sie damit Informationen zu Ihrem Datenfluss suchen können. |
| `description` | Ein optionaler Wert, den Sie hinzufügen können, um weitere Informationen zu Ihrem Datenfluss bereitzustellen. |
| `flowSpec.id` | Die Flussspezifikations-ID, die zum Erstellen eines Datenflusses erforderlich ist. Diese feste ID lautet: `6499120c-0b15-42dc-936e-847ea3c24d72`. |
| `flowSpec.version` | Die entsprechende Version der Flussspezifikations-ID. Dieser Wert ist standardmäßig auf `1.0` festgelegt. |
| `sourceConnectionIds` | Die [Quellverbindungs-ID](#source-connection), die in einem früheren Schritt generiert wurde. |
| `targetConnectionIds` | Die [Zielverbindungs-ID](#target-connection), die in einem früheren Schritt generiert wurde. |
| `transformations` | Diese Eigenschaft enthält die verschiedenen Umwandlungen, die auf Ihre Daten angewendet werden müssen. Diese Eigenschaft ist erforderlich, wenn nicht-XDM-konforme Daten an Platform übermittelt werden. |
| `transformations.name` | Der Name, der der Transformation zugewiesen wurde. |
| `transformations.params.mappingId` | Die [Zuordnungs-ID](#mapping), die in einem früheren Schritt generiert wurde. |
| `transformations.params.mappingVersion` | Die entsprechende Version der Zuordnungs-ID. Dieser Wert ist standardmäßig auf `0` festgelegt. |
| `scheduleParams.startTime` | Diese Eigenschaft enthält Informationen zur Erfassungszeitplanung des Datenflusses. |
| `scheduleParams.frequency` | Die Häufigkeit, mit der der Datenfluss Daten erfasst. Zulässige Werte sind: `once`, `minute`, `hour`, `day` oder `week`. |
| `scheduleParams.interval` | Das Intervall bezeichnet den Zeitraum zwischen zwei aufeinanderfolgenden Datenflussausführungen. Der Wert des Intervalls sollte eine Ganzzahl ungleich null sein. Das Intervall ist nicht erforderlich, wenn die Häufigkeit auf `once` festgelegt ist, und sollte größer oder gleich `15` für andere Frequenzwerte sein. |

**Antwort**

Bei einer erfolgreichen Antwort wird die ID (`id`) des neu erstellten Datenflusses angegeben. Mit dieser ID können Sie Ihren Datenfluss überwachen, aktualisieren oder löschen.

```json
{
     "id": "993f908f-3342-4d9c-9f3c-5aa9a189ca1a",
     "etag": "\"510bb1d4-8453-4034-b991-ab942e11dd8a\""
}
```

## Anhang

Im folgenden Abschnitt finden Sie Informationen zu den Schritten, mit denen Sie Ihren Datenfluss überwachen, aktualisieren und löschen können.

### Überwachen Ihres Datenflusses

Nachdem Ihr Datenfluss erstellt wurde, können Sie die Datenaufnahme überwachen, um Informationen über die Datenflussausführungen, den Abschlussstatus und Fehler anzuzeigen. Die vollständigen API-Beispiele finden Sie im Handbuch unter [Überwachen der Datenflüsse Ihrer Quellen mithilfe der API](../../monitor.md).

### Aktualisieren des Datenflusses

Aktualisieren Sie die Details Ihres Datenflusses, z. B. seinen Namen und seine Beschreibung, sowie den Ausführungszeitplan und die zugehörigen Zuordnungssätze, indem Sie eine PATCH-Anfrage an die `/flows` Endpunkt von [!DNL Flow Service] API verwenden, während Sie die Kennung Ihres Datenflusses angeben. Bei einer PATCH-Anfrage müssen Sie die eindeutige `etag` im `If-Match` -Kopfzeile. Die vollständigen API-Beispiele finden Sie im Handbuch unter [Aktualisieren von Datenflüssen für Quellen mithilfe der API](../../update-dataflows.md).

### Konto aktualisieren

Aktualisieren Sie den Namen, die Beschreibung und die Anmeldeinformationen Ihres Quellkontos, indem Sie eine PATCH-Anfrage an die [!DNL Flow Service] API bei der Bereitstellung Ihrer Basis-Verbindungs-ID als Abfrageparameter. Bei einer PATCH-Anfrage müssen Sie die eindeutige `etag` im `If-Match` -Kopfzeile. Die vollständigen API-Beispiele finden Sie im Handbuch unter [Quellkonto mithilfe der API aktualisieren](../../update.md).

### Löschen des Datenflusses

Löschen Sie Ihren Datenfluss, indem Sie eine DELETE-Anfrage an die [!DNL Flow Service] API bei Angabe der Kennung des Datenflusses, den Sie als Teil des Abfrageparameters löschen möchten. Die vollständigen API-Beispiele finden Sie im Handbuch unter [Löschen Ihrer Datenflüsse mithilfe der API](../../delete-dataflows.md).

### Konto löschen

Löschen Sie Ihr Konto, indem Sie eine DELETE-Anfrage an die [!DNL Flow Service] API bei Angabe der grundlegenden Verbindungs-ID des Kontos, das Sie löschen möchten. Die vollständigen API-Beispiele finden Sie im Handbuch unter [Löschen Ihres Quellkontos mithilfe der API](../../delete.md).