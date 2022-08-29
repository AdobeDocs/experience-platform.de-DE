---
keywords: Experience Platform;Startseite;beliebte Themen;Quellen;Connectoren;Quell-Connectoren;Quellen-SDK;SDK
solution: Experience Platform
title: Erstellen eines Datenflusses für Zendesk mithilfe der Flow Service-API
topic-legacy: tutorial
description: Erfahren Sie, wie Sie Adobe Experience Platform mithilfe der Flow Service-API mit Zendesk verbinden.
exl-id: 3e00e375-c6f8-407c-bded-7357ccf3482e
source-git-commit: 23a6f8ee23fb67290a5bcba2673a87ce74c9e1d3
workflow-type: tm+mt
source-wordcount: '1977'
ht-degree: 65%

---

# (Beta) Erstellen Sie einen Datenfluss für [!DNL Zendesk] mithilfe der [!DNL Flow Service] API

>[!NOTE]
>
>Die [!DNL Zendesk] -Quelle befindet sich in der Beta-Phase. Siehe [Quellen - Übersicht](../../../../home.md#terms-and-conditions) für weitere Informationen zur Verwendung von Beta-beschrifteten Quellen.

Das folgende Tutorial führt Sie durch die Schritte zum Erstellen einer Quellverbindung und eines Datenflusses, um [!DNL Zendesk]-Daten mithilfe der [[!DNL Flow Service] -API](https://www.adobe.io/experience-platform-apis/references/flow-service/) an Platform zu übermitteln.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Experience Platform voraus:

* [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen aufteilen, um die Entwicklung und Weiterentwicklung von Programmen für digitale Erlebnisse zu erleichtern.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um eine erfolgreiche Verbindung zu [!DNL Zendesk] mithilfe der [!DNL Flow Service] API.

### Sammeln erforderlicher Anmeldeinformationen

Um auf Ihre [!DNL Zendesk] -Konto in Platform angeben, müssen Sie Werte für die folgenden Anmeldedaten angeben:

| Anmeldedaten | Beschreibung | Beispiel |
| --- | --- | --- |
| `accessToken` | Zendesk-API-Token. | `0lZnClEvkJSTQ7olGLl7PMhVq99gu26GTbJtf` |

Weitere Informationen zum Authentifizieren Ihrer [!DNL Zendesk] -Quelle, siehe [[!DNL Zendesk] Quellübersicht](../../../../connectors/customer-success/zendesk.md).

## Verbinden [!DNL Zendesk] zur Plattform mithilfe der [!DNL Flow Service] API

Das folgende Tutorial führt Sie durch die Schritte zum Erstellen einer [!DNL Zendesk] Quellverbindung und Erstellen eines Datenflusses zum [!DNL Zendesk] Daten an Platform mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

### Erstellen einer Basisverbindung {#base-connection}

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basis-Verbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an die `/connections` Endpunkt beim Bereitstellen [!DNL Zendesk] Authentifizierungsberechtigungen als Teil des Anfragetexts.

**API-Format**

```https
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Zendesk]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Zendesk base connection",
        "description": "Zendesk base connection to authenticate to Platform",
        "connectionSpec": {
            "id": "0a27232b-2c6e-4396-b8c6-c9fc24e37ba4",
            "version": "1.0"
        },
        "auth": {
            "specName": "OAuth2 Refresh Code",
            "params": {
                "accessToken": "{ACCESS_TOKEN}"
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
| `auth.params.accessToken` | Das entsprechende Zugriffs-Token, das zum Authentifizieren Ihrer Quelle verwendet wird. Dies ist für die OAuth-basierte Authentifizierung erforderlich. |

**Antwort**

Eine erfolgreiche Antwort gibt die neu erstellte Basisverbindung zurück, einschließlich ihrer eindeutigen Verbindungskennung (`id`). Diese ID ist erforderlich, um die Dateistruktur und Inhalte Ihrer Quelle im nächsten Schritt zu untersuchen.

```json
{
     "id": "70383d02-2777-4be7-a309-9dd6eea1b46d",
     "etag": "\"d64c8298-add4-4667-9a49-28195b2e2a84\""
}
```

### Durchsuchen der Quelle {#explore}

Mithilfe der im vorherigen Schritt generierten Basisverbindungs-ID können Sie Dateien und Ordner durch Ausführen von GET-Anfragen untersuchen.
Verwenden Sie die folgenden Aufrufe, um den Pfad der Datei zu finden, die in integriert werden soll [!DNL Platform]:

**API-Format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

Bei der Durchführung von GET-Anfragen zur Analyse der Dateistruktur und des Inhalts Ihrer Quelle müssen Sie die in der folgenden Tabelle aufgeführten Abfrageparameter einbeziehen:


| Parameter | Beschreibung |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | Die im vorherigen Schritt generierte Basisverbindungs-ID. |
| `objectType=rest` | Der Typ des Objekts, das Sie untersuchen möchten. Derzeit ist dieser Wert immer auf `rest`. |
| `{OBJECT}` | Dieser Parameter ist nur beim Anzeigen eines bestimmten Ordners erforderlich. Der Wert stellt den Pfad des Ordners dar, den Sie untersuchen möchten. |
| `fileType=json` | Der Dateityp der Datei, die Sie in Platform laden möchten. Zurzeit `json` ist der einzige unterstützte Dateityp. |
| `{PREVIEW}` | Ein boolescher Wert, der definiert, ob der Inhalt der Verbindung die Vorschau unterstützt. |
| `{SOURCE_PARAMS}` | Definiert Parameter für die Quelldatei, die Sie in Platform laden möchten. Um den akzeptierten Formattyp für `{SOURCE_PARAMS}` abzurufen, müssen Sie die gesamte Zeichenfolge `parameter` in base64 kodieren. Im folgenden Beispiel: `"{}"` kodiert in base64 entspricht `e30`. |


**Anfrage**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/70383d02-2777-4be7-a309-9dd6eea1b46d/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=e30' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Struktur der abgefragten Datei zurück. Im folgenden Beispiel innerhalb der ``data[]`` Nutzlast wird nur ein einzelner Datensatz angezeigt, es können jedoch mehrere Datensätze vorhanden sein.

```json
{
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "result": {
                "type": "object",
                "properties": {
                    "organization_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "external_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "role_type": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "custom_role_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "default_group_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "phone": {
                        "type": "string"
                    },
                    "shared_phone_number": {
                        "type": "boolean"
                    },
                    "alias": {
                        "type": "string"
                    },
                    "last_login_at": {
                        "type": "string"
                    },
                    "signature": {
                        "type": "string"
                    },
                    "details": {
                        "type": "string"
                    },
                    "notes": {
                        "type": "string"
                    },
                    "photo": {
                        "type": "string",
                        "media": {
                            "binaryEncoding": "base64",
                            "type": "image/png"
                        }
                    },
                    "active": {
                        "type": "boolean"
                    },
                    "created_at": {
                        "type": "string"
                    },
                    "email": {
                        "type": "string"
                    },
                    "iana_time_zone": {
                        "type": "string"
                    },
                    "id": {
                        "type": "integer"
                    },
                    "locale": {
                        "type": "string"
                    },
                    "locale_id": {
                        "type": "integer"
                    },
                    "moderator": {
                        "type": "boolean"
                    },
                    "name": {
                        "type": "string"
                    },
                    "only_private_comments": {
                        "type": "boolean"
                    },
                    "report_csv": {
                        "type": "boolean"
                    },
                    "restricted_agent": {
                        "type": "boolean"
                    },
                    "result_type": {
                        "type": "string"
                    },
                    "role": {
                        "type": "integer"
                    },
                    "shared": {
                        "type": "boolean"
                    },
                    "shared_agent": {
                        "type": "boolean"
                    },
                    "suspended": {
                        "type": "boolean"
                    },
                    "ticket_restriction": {
                        "type": "string"
                    },
                    "time_zone": {
                        "type": "string"
                    },
                    "two_factor_auth_enabled": {
                        "type": "boolean"
                    },
                    "updated_at": {
                        "type": "string"
                    },
                    "url": {
                        "type": "string"
                    },
                    "verified": {
                        "type": "boolean"
                    },
                    "tags": {
                        "type": "array",
                        "items": {
                            "type": "string"
                        }
                    }
                }
            }
        }
    },
    "data": [
        {
            "result": {
                "id": 6106699702801,
                "url": "https://{YOURSUBDOMAIN}.zendesk.com/api/v2/users/6106699702801.json",
                "name": "test",
                "email": "test@org.com",
                "created_at": "2022-05-13T08:04:22Z",
                "updated_at": "2022-05-13T08:04:22Z",
                "time_zone": "Asia/Kolkata",
                "iana_time_zone": "Asia/Kolkata",
                "locale_id": 1,
                "locale": "en-US",
                "role": "end-user",
                "verified": false,
                "active": true,
                "shared": false,
                "shared_agent": false,
                "two_factor_auth_enabled": false,
                "moderator": false,
                "ticket_restriction": "requested",
                "only_private_comments": false,
                "restricted_agent": true,
                "suspended": false,
                "report_csv": false,
                "result_type": "user"
            }
        }
    ]
}
```

### Erstellen einer Quellverbindung {#source-connection}

Sie können eine Quellverbindung herstellen, indem Sie eine POST-Anfrage an die [!DNL Flow Service]-API senden. Eine Quellverbindung besteht aus einer Verbindungs-ID, einem Pfad zur Quelldatendatei und einer Verbindungsspezifikations-ID.

**API-Format**

```https
POST /sourceConnections
```

**Anfrage**

Die folgende Anfrage erstellt eine Quellverbindung für [!DNL Zendesk]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Zendesk Source Connection",
        "description": "Zendesk Source Connection",
        "baseConnectionId": "70383d02-2777-4be7-a309-9dd6eea1b46d",
        "connectionSpec": {
            "id": "0a27232b-2c6e-4396-b8c6-c9fc24e37ba4",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {}
    }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der Name Ihrer Quellverbindung. Stellen Sie sicher, dass der Name Ihrer Quellverbindung beschreibend ist, da Sie damit Informationen zu Ihrer Quellverbindung nachschlagen können. |
| `description` | Ein optionaler Wert, den Sie angeben können, um weitere Informationen über Ihre Quellverbindung bereitzustellen. |
| `baseConnectionId` | Die Basisverbindungs-ID von [!DNL Zendesk]. Diese ID wurde in einem früheren Schritt generiert. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID, die Ihrer Quelle entspricht. |
| `data.format` | Das Format der [!DNL Zendesk]-Daten, die Sie aufnehmen möchten. Derzeit wird nur das Datenformat `json` unterstützt. |

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

### Erstellen eines Zieldatensatzes {#target-dataset}

Ein Zieldatensatz kann erstellt werden, indem eine POST-Anfrage an die [Catalog Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) durchgeführt wird, wodurch die ID des Zielschemas in der Payload angegeben wird.

Ausführliche Anweisungen zum Erstellen eines Zieldatensatzes finden Sie im Tutorial zu [Erstellen eines Datensatzes mithilfe der API](../../../../../catalog/api/create-dataset.md).

### Erstellen einer Zielverbindung {#target-connection}

Eine Zielverbindung stellt die Verbindung zum Ziel dar, an dem die aufgenommenen Daten gespeichert werden sollen. Um eine Zielverbindung zu erstellen, müssen Sie die ID der Festnetzverbindungsspezifikation angeben, die dem Data Lake entspricht. Diese ID lautet: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Sie verfügen jetzt über die eindeutigen Kennungen eines Zielschemas, eines Zieldatensatzes und der Verbindungsspezifikations-ID zum Data Lake. Anhand dieser Kennungen können Sie mit der [!DNL Flow Service]-API eine Zielverbindung erstellen, um den Datensatz anzugeben, der die eingehenden Quelldaten enthalten wird.

**API-Format**

```https
POST /targetConnections
```

**Anfrage**

Die folgende Anfrage erstellt eine Zielverbindung für Zendesk:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Zendesk Target Connection",
        "description": "Zendesk Target Connection",
        "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "dataSetId": "624bf42e16519d19496e3f67"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `name` | Der Name Ihrer Zielverbindung. Stellen Sie sicher, dass der Name Ihrer Zielverbindung beschreibend ist, da Sie damit Informationen zu Ihrer Zielverbindung nachschlagen können. |
| `description` | Ein optionaler Wert, den Sie für weitere Informationen zu Ihrer Zielverbindung angeben können. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID, die dem Data Lake entspricht. Diese feste ID lautet: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | Das Format der [!DNL Zendesk]-Daten, die Sie an Platform übermitteln möchten. |
| `params.dataSetId` | Die Zieldatensatz-ID, die in einem vorherigen Schritt abgerufen wurde. |


**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung der neuen Zielverbindung an (`id`). Diese ID ist in späteren Schritten erforderlich.

```json
{
     "id": "7c96c827-3ffd-460c-a573-e9558f72f263",
     "etag": "\"a196f685-f5e8-4c4c-bfbd-136141bb0c6d\""
}
```

### Erstellen einer Zuordnung {#mapping}

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "version": 0,
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
        "xdmVersion": "1.0",
        "mappings": [
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.id",
                "destination": "_extconndev.id",
                "name": "id",
                "description": "Zendesk"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.external_id",
                "destination": "_extconndev.external_id"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.role_type",
                "destination": "_extconndev.role_type"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.custom_role_id",
                "destination": "_extconndev.custom_role_id"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.default_group_id",
                "destination": "_extconndev.default_group_id"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.phone",
                "destination": "_extconndev.phone"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.shared_phone_number",
                "destination": "_extconndev.shared_phone_number"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.verified",
                "destination": "_extconndev.verified"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.alias",
                "destination": "_extconndev.alias"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.last_login_at",
                "destination": "_extconndev.last_login_at"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.signature",
                "destination": "_extconndev.signature"
            },        {
                "sourceType": "ATTRIBUTE",
                "source": "result.details",
                "destination": "_extconndev.details"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.notes",
                "destination": "_extconndev.notes"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.active",
                "destination": "_extconndev.active"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.created_at",
                "destination": "_extconndev.created_at"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.email",
                "destination": "_extconndev.email"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.iana_time_zone",
                "destination": "_extconndev.iana_time_zone"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.organization_id",
                "destination": "_extconndev.organization_id"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.locale",
                "destination": "_extconndev.locale"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.locale_id",
                "destination": "_extconndev.locale_id"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.moderator",
                "destination": "_extconndev.moderator"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.name",
                "destination": "_extconndev.name"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.only_private_comments",
                "destination": "_extconndev.only_private_comments"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.report_csv",
                "destination": "_extconndev.report_csv"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.restricted_agent",
                "destination": "_extconndev.restricted_agent"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.result_type",
                "destination": "_extconndev.result_type"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.role",
                "destination": "_extconndev.role"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.shared",
                "destination": "_extconndev.shared"
            },        {
                "sourceType": "ATTRIBUTE",
                "source": "result.shared_agent",
                "destination": "_extconndev.shared_agent"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.time_zone",
                "destination": "_extconndev.time_zone"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.two_factor_auth_enabled",
                "destination": "_extconndev.two_factor_auth_enabled"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.suspended",
                "destination": "_extconndev.suspended"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.updated_at",
                "destination": "_extconndev.updated_at"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.url",
                "destination": "_extconndev.url"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.verified",
                "destination": "_extconndev.verified"
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

### Erstellen eines Flusses {#flow}

Der letzte Schritt zur Übermittlung von Daten aus Zendesk an Platform besteht darin, einen Datenfluss zu erstellen. Bislang haben Sie die folgenden erforderlichen Werte vorbereitet:

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Zendesk dataflow",
        "description": "Zendesk dataflow",
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