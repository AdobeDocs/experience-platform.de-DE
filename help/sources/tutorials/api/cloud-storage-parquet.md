---
keywords: Experience Platform;Startseite;beliebte Themen;Datenquellenverbindung
solution: Experience Platform
title: Aufnehmen von Parquet-Daten aus einem Cloud-Speichersystem eines Drittanbieters mithilfe der Flow Service-API
type: Tutorial
description: In diesem Tutorial wird die Flow Service-API verwendet, um Sie durch die Schritte zur Aufnahme von Apache Parquet-Daten aus einem Cloud-Speichersystem eines Drittanbieters zu führen.
exl-id: fb1b19d6-16bb-4a5f-9e81-f537bac95041
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 44%

---

# Aufnehmen von Parquet-Daten aus einem Cloud-Speichersystem eines Drittanbieters mithilfe der [!DNL Flow Service]-API

[!DNL Flow Service] wird verwendet, um Kundendaten aus verschiedenen Quellen innerhalb von Adobe Experience Platform zu sammeln und zu zentralisieren. Der Dienst stellt eine Benutzeroberfläche und eine RESTful-API bereit, über die alle unterstützten Quellen verbunden werden können.

In diesem Tutorial wird die [!DNL Flow Service]-API verwendet, um Sie durch die Schritte zur Aufnahme von Parquet-Daten aus einem Cloud-Speichersystem eines Drittanbieters zu führen.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [Quellen](../../home.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Experience Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
- [Sandboxes](../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Experience Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um Parquet-Daten aus einem Cloud-Speicher eines Drittanbieters mithilfe der [!DNL Flow Service]-API erfolgreich aufnehmen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Experience Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Alle Ressourcen in [!DNL Experience Platform], einschließlich der Ressourcen, die zu [!DNL Flow Service] gehören, werden in bestimmten virtuellen Sandboxes isoliert. Bei allen Anfragen an [!DNL Experience Platform]-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

- `x-sandbox-name: {SANDBOX_NAME}`

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

- `Content-Type: application/json`

## Verbindung erstellen

Um Parquet-Daten mithilfe von [!DNL Experience Platform]-APIs aufzunehmen, müssen Sie über eine gültige Verbindung für die Cloud-Speicherquelle eines Drittanbieters verfügen, auf die Sie zugreifen. Wenn Sie noch keine Verbindung für den Speicher haben, mit dem Sie arbeiten möchten, können Sie eine Verbindung mithilfe der folgenden Tutorials erstellen:

- [Amazon S3](./create/cloud-storage/s3.md)
- [Azure Blob](./create/cloud-storage/blob.md)
- [Azure Data Lake Storage Gen2](./create/cloud-storage/adls-gen2.md)
- [Google Cloud Store](./create/cloud-storage/google.md)
- [SFTP](./create/cloud-storage/sftp.md)

Rufen Sie die eindeutige Kennung (`$id`) der Verbindung ab und speichern Sie sie. Fahren Sie dann mit dem nächsten Schritt dieses Tutorials fort.

## Erstellen eines Zielschemas

Damit die Quelldaten in [!DNL Experience Platform] verwendet werden können, muss auch ein Zielschema erstellt werden, das die Quelldaten entsprechend Ihren Anforderungen strukturiert. Das Zielschema wird dann verwendet, um einen [!DNL Experience Platform] Datensatz zu erstellen, in dem die Quelldaten enthalten sind.

Wenn Sie die Benutzeroberfläche lieber in [!DNL Experience Platform] verwenden möchten, finden Sie im Tutorial [Schema-](../../../xdm/tutorials/create-schema-ui.md)) schrittweise Anweisungen zum Ausführen ähnlicher Aktionen im Schema-Editor.

**API-Format**

```http
POST /schemaregistry/tenant/schemas
```

**Anfrage**

Die folgende Beispielanfrage erstellt ein XDM-Schema, das die XDM-[!DNL Individual Profile] erweitert.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
    "type": "object",
    "title": "Sample Demo Profile XDM {{$guid}}",
    "description": "",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-work-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-subscriptions"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/identitymap"
        }
    ],
    "meta:containerId": "tenant",
    "meta:resourceType": "schemas",
    "meta:xdmType": "object",
    "meta:class": "https://ns.adobe.com/xdm/context/profile"
}'
```

**Antwort**

Eine erfolgreiche Antwort gibt Details zum neu erstellten Schema zurück, einschließlich der eindeutigen Kennung (`$id`). Diese ID ist im nächsten Schritt erforderlich, um eine Quellverbindung zu erstellen.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80",
    "meta:altId": "_{TENANT_ID}.schemas.e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Sample Demo Profile XDM 8d96a964-aad8-43c5-a73a-c8b9b1ccbfb1",
    "type": "object",
    "description": "",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-work-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-subscriptions",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/identitymap",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/context/profile-subscriptions",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/context/profile-work-details"
    ],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/context/profile-subscriptions",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/context/profile-work-details"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1584673864341,
        "repo:lastModifiedDate": 1584673864341,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{MODIFIED_USER_ID}",
        "eTag": "fa704f80da907c8f0f66f453ffcac3e52958687edbf55d71231dc5e1522193c4"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Erstellen einer Quellverbindung {#source}

Nachdem ein Ziel-XDM-Schema erstellt wurde, kann jetzt eine Quellverbindung mithilfe einer POST-Anfrage an die [!DNL Flow Service]-API erstellt werden. Eine Quellverbindung besteht aus einer Verbindung für die API, einem Quelldatenformat und einem Verweis auf das im vorherigen Schritt abgerufene XDM-Zielschema.

**API-Format**

```http
POST /sourceConnections
```

**Anfrage**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Source Connection S3 {{$guid}}",
        "baseConnectionId": "5831c52c-c261-4945-b1c5-2cc261d945b2",
        "connectionSpec": {
            "id": "ecadc60c-7455-4d87-84dc-2a0e293d997b",
            "version": 1
        },
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80",
                "id": "",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "path": "partners-demo/samples",
            "recursive": "true"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `baseConnectionId` | Die Verbindung für die API, die Ihren Cloud-Speicher darstellt. |
| `data.schema.id` | Das (`$id`) des Ziel-XDM-Schemas, das im vorherigen Schritt abgerufen wurde. |
| `params.path` | Der Pfad der Quelldatei. |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung (`id`) der neu erstellten Quellverbindung zurück. Speichern Sie diesen Wert, da er in späteren Schritten zum Erstellen einer Zielverbindung erforderlich ist.

```json
{
    "id": "73bc8911-505a-4e46-bc89-11505a6e466f",
    "etag": "\"c4004435-0000-0200-0000-5e7437d90000\""
}
```

## Erstellen einer Datensatz-Basisverbindung

Um externe Daten in [!DNL Experience Platform] aufzunehmen, muss zunächst eine [!DNL Experience Platform] Datensatz-Basisverbindung abgerufen werden.

Um eine Datensatzbasisverbindung zu erstellen, führen Sie die Schritte aus, die im Abschnitt [Tutorial zur Datensatzbasisverbindung](./create-dataset-base-connection.md) beschrieben sind.

Fahren Sie mit den im Entwicklerhandbuch beschriebenen Schritten fort, bis Sie eine Datensatz-Basisverbindung erstellt haben. Rufen Sie die eindeutige Kennung (`$id`) ab, speichern Sie sie und verwenden Sie sie im nächsten Schritt, um eine Zielverbindung zu erstellen, als Basisverbindungs-ID.

## Erstellen eines Zieldatensatzes

Ein Zieldatensatz kann erstellt werden, indem eine POST-Anfrage an die [Catalog Service API](https://www.adobe.io/experience-platform-apis/references/catalog/) durchgeführt wird, wodurch die ID des Zielschemas in der Payload angegeben wird.

**API-Format**

```http
POST /catalog/dataSets
```

**Anfrage**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Leads Dataset {{$guid}}",
        "schemaRef": {
            "id": ""https://ns.adobe.com/{TENANT_ID}/schemas/e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80"",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `schemaRef.id` | Die ID Ihres XDM-Zielschemas. |

**Antwort**

Eine erfolgreiche Antwort gibt ein -Array zurück, das die ID des neu erstellten Datensatzes im `"@/datasets/{DATASET_ID}"` Format enthält. Die Datensatz-ID ist eine schreibgeschützte, systemgenerierte Zeichenfolge, die verwendet wird, um in API-Aufrufen auf den Datensatz zu verweisen. Speichern Sie die Zieldatensatz-ID, da sie in späteren Schritten zum Erstellen einer Zielverbindung und eines Datenflusses erforderlich ist.

```json
[
    "@/dataSets/5e7439b1ad55a618ad4c5102"
]
```

## Erstellen einer Zielverbindung {#target}

Sie verfügen jetzt über die eindeutigen Kennungen für eine Datensatz-Basisverbindung, ein Zielschema und einen Zieldatensatz. Anhand dieser Kennungen können Sie mit der [!DNL Flow Service]-API eine Zielverbindung erstellen, um den Datensatz anzugeben, der die eingehenden Quelldaten enthalten wird.

**API-Format**

```http
POST /targetConnections
```

**Anfrage**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "baseConnectionId": "291257e3-c560-4e07-9257-e3c5606e07d1",
        "connectionSpec": {
            "id":"c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        },
        "name": "Target Connection {{$guid}}",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": ""https://ns.adobe.com/{TENANT_ID}/schemas/e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80"",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "dataSetId": "5e7439b1ad55a618ad4c5102"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `baseConnectionId` | Die ID Ihrer Datensatz-Basisverbindung. |
| `data.schema.id` | Die `$id` des XDM-Zielschemas. |
| `params.dataSetId` | Die Kennung des Zieldatensatzes. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID für Ihren Cloud-Speicher. |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung der neuen Zielverbindung an (`id`). Notieren Sie sich diesen Wert, da Sie ihn in späteren Schritten benötigen werden.

```json
{
    "id": "9b3abc95-f2e9-47c1-babc-95f2e927c1ec",
    "etag": "\"7501936b-0000-0200-0000-5e743bcc0000\""
}
```

## Erstellen eines Datenflusses

Der letzte Schritt bei der Aufnahme von Parquet-Daten aus einem Cloud-Speicher eines Drittanbieters besteht darin, einen Datenfluss zu erstellen. Bislang haben Sie die folgenden erforderlichen Werte vorbereitet:

- [Quellverbindungs-ID](#source)
- [Zielverbindungs-ID](#target)

Ein Datenfluss ist für die Planung und Erfassung von Daten aus einer Quelle verantwortlich. Sie können einen Datenfluss erstellen, indem Sie eine POST-Anfrage ausführen und dabei die oben genannten Werte in der Payload angeben.

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
        "name": "Demo Parquet Ingestion Flow {{$guid}}",
        "flowSpec": {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "73bc8911-505a-4e46-bc89-11505a6e466f"
        ],
        "targetConnectionIds": [
            "9b3abc95-f2e9-47c1-babc-95f2e927c1ec"
        ],
        "scheduleParams": {
            "startTime": {{$timestamp}},
            "frequency": "minute",
            "interval": 1000,
            "backfill": true
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `sourceConnectionIds` | Die in einem früheren Schritt abgerufene Quellverbindungs-ID . |
| `targetConnectionIds` | Die Zielverbindungs-ID , die in einem früheren Schritt abgerufen wurde. |

**Antwort**

Bei einer erfolgreichen Antwort wird die ID (`id`) des neu erstellten Datenflusses angegeben.

```json
{
    "id": "89ff50ef-b082-426e-bf50-efb082d26e78",
    "etag": "\"890070b8-0000-0200-0000-5e743c040000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie einen Quell-Connector erstellt, um Parquet-Daten aus Ihrem Cloud-Speichersystem eines Drittanbieters nach einem bestimmten Zeitplan zu erfassen. Eingehende Daten können jetzt von nachgelagerten [!DNL Experience Platform]-Services verwendet werden, wie [!DNL Real-Time Customer Profile] und [!DNL Data Science Workspace]. Weiterführende Informationen finden Sie in folgenden Dokumenten:

- [Übersicht zum Echtzeit-Kundenprofil](../../../profile/home.md)
- [Übersicht über Data Science Workspace](../../../data-science-workspace/home.md)
