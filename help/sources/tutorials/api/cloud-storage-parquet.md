---
keywords: Experience Platform;Home;beliebte Themen;Datenquellenverbindung
solution: Experience Platform
title: Daten aus einem Drittanbieter-Cloud-Datenspeicherung-System mithilfe der Flow-Dienst-API erfassen
topic: Übersicht
type: Tutorial
description: Dieses Lernprogramm verwendet die Flow Service API, um Sie durch die Schritte zum Erfassen von Apache Parquet-Daten von einem Drittanbieter-Cloud-Datenspeicherung-System zu führen.
exl-id: fb1b19d6-16bb-4a5f-9e81-f537bac95041
translation-type: tm+mt
source-git-commit: 610ce5c6dca5e7375b941e7d6f550382da10ca27
workflow-type: tm+mt
source-wordcount: '1103'
ht-degree: 19%

---

# Erfassen von Parquet-Daten aus einem Drittanbieter-Cloud-Datenspeicherung-System mithilfe der API[!DNL Flow Service]

[!DNL Flow Service] wird zur Erfassung und Zentralisierung von Kundendaten aus unterschiedlichen Quellen innerhalb von Adobe Experience Platform verwendet. Der Dienst stellt eine Benutzeroberfläche und eine RESTful-API bereit, über die alle unterstützten Quellen verbunden werden können.

Dieses Lernprogramm verwendet die API [!DNL Flow Service], um Sie durch die Schritte zum Erfassen von Parquet-Daten aus einem Drittanbieter-Cloud-Datenspeicherung-System zu führen.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [Quellen](../../home.md):  [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von  [!DNL Platform] Diensten zu strukturieren, zu beschriften und zu verbessern.
- [Sandboxen](../../../sandboxes/home.md):  [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne  [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um Parquet-Daten von einer Drittanbieter-Cloud-Datenspeicherung mit der API [!DNL Flow Service] erfolgreich zu erfassen.

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Fehlerbehebungshandbuch für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://www.adobe.com/go/platform-api-authentication-en) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

Alle Ressourcen in [!DNL Experience Platform], einschließlich derjenigen, die zu [!DNL Flow Service] gehören, werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an [!DNL Platform]-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird in:

- `x-sandbox-name: `{SANDBOX_NAME}&quot;

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

- `Content-Type: application/json`

## Verbindung erstellen

Um Parquet-Daten mithilfe von [!DNL Platform]-APIs zu erfassen, müssen Sie über eine gültige Verbindung für die Cloud-Datenspeicherung eines Drittanbieters verfügen, auf die Sie zugreifen. Wenn Sie noch keine Verbindung zu der Datenspeicherung haben, mit der Sie arbeiten möchten, können Sie eine dieser Übungen erstellen:

- [Amazon S3](./create/cloud-storage/s3.md)
- [Azure Blob](./create/cloud-storage/blob.md)
- [Azurblase Data Lake Datenspeicherung Gen2](./create/cloud-storage/adls-gen2.md)
- [Google Cloud Store](./create/cloud-storage/google.md)
- [SFTP](./create/cloud-storage/sftp.md)

Rufen Sie die eindeutige Kennung (`$id`) der Verbindung ab und speichern Sie sie und fahren Sie dann mit dem nächsten Schritt dieses Lernprogramms fort.

## Erstellen eines Zielgruppe-Schemas

Damit die Quelldaten in [!DNL Platform] verwendet werden können, muss auch ein Zielgruppe-Schema erstellt werden, um die Quelldaten entsprechend Ihren Anforderungen zu strukturieren. Mit dem Schema Zielgruppe wird dann ein [!DNL Platform]-Datensatz erstellt, in dem die Quelldaten enthalten sind.

Wenn Sie lieber die Benutzeroberfläche in [!DNL Experience Platform] verwenden möchten, enthält das [Schema-Editor-Tutorial](../../../xdm/tutorials/create-schema-ui.md) eine schrittweise Anleitung zum Durchführen ähnlicher Aktionen im Schema-Editor.

**API-Format**

```http
POST /schemaregistry/tenant/schemas
```

**Anfrage**

Die folgende Beispielanforderung erstellt ein XDM-Schema, das die XDM [!DNL Individual Profile]-Klasse erweitert.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Eine erfolgreiche Antwort gibt Details zum neu erstellten Schema einschließlich seiner eindeutigen Kennung (`$id`) zurück. Diese ID ist im nächsten Schritt erforderlich, um eine Quellverbindung zu erstellen.

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
    "imsOrg": "{IMS_ORG}",
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

Nachdem ein XDM-Schema der Zielgruppe erstellt wurde, kann jetzt eine Quellverbindung mit einer POST-Anfrage an die [!DNL Flow Service]-API erstellt werden. Eine Quellverbindung besteht aus einer Verbindung für die API, einem Quelldatenformat und einem Verweis auf das im vorherigen Schritt abgerufene XDM-Schema der Zielgruppe.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `baseConnectionId` | Die Verbindung für die API, die Ihre Cloud-Datenspeicherung darstellt. |
| `data.schema.id` | Das Schema (`$id`), wenn die Zielgruppe xdm im vorherigen Schritt abgerufen wurde. |
| `params.path` | Der Pfad der Quelldatei. |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung (`id`) der neu erstellten Quellverbindung zurück. Speichern Sie diesen Wert so, wie er in späteren Schritten zum Erstellen einer Zielgruppe-Verbindung erforderlich ist.

```json
{
    "id": "73bc8911-505a-4e46-bc89-11505a6e466f",
    "etag": "\"c4004435-0000-0200-0000-5e7437d90000\""
}
```

## Erstellen einer Datenbank-Basisverbindung

Um externe Daten in [!DNL Platform] zu erfassen, muss zunächst eine [!DNL Experience Platform]-Datenbank-Verbindung aufgebaut werden.

Gehen Sie zum Erstellen einer Datenbank-Basisverbindung wie im Lernprogramm [Datenbank-Basisverbindung](./create-dataset-base-connection.md) beschrieben vor.

Führen Sie die im Entwicklerhandbuch beschriebenen Schritte aus, bis Sie eine Datenbank-Basisverbindung erstellt haben. Besorgen Sie sich den eindeutigen Bezeichner (`$id`) und speichern Sie ihn im nächsten Schritt als Basis-Verbindungs-ID, um eine Zielgruppe-Verbindung zu erstellen.

## Zielgruppen-Dataset erstellen

Ein Zielgruppen-Datensatz kann erstellt werden, indem eine POST an die [Katalogdienst-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) angefordert wird und die ID des Zielgruppe-Schemas innerhalb der Nutzlast angegeben wird.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Leads Dataset {{$guid}}",
        "schemaRef": {
            "id": ""https://ns.adobe.com/{TENANT_ID}/schemas/e15530faf88aeb52d9ca5c5671a059f44f1a42ea7f5fdb80"",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        },
        "fileDescription": {
            "format": "parquet"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `schemaRef.id` | Die ID Ihres Zielgruppe XDM-Schemas. |

**Antwort**

Eine erfolgreiche Antwort gibt ein Array zurück, das die ID des neu erstellten Datensatzes im Format `"@/datasets/{DATASET_ID}"` enthält. Die Datensatz-ID ist eine schreibgeschützte, vom System generierte Zeichenfolge, mit der in API-Aufrufen auf den Datensatz verwiesen wird. Speichern Sie die Zielgruppe-Dataset-ID wie in den späteren Schritten zum Erstellen einer Zielgruppe- und eines Datenflusses erforderlich.

```json
[
    "@/dataSets/5e7439b1ad55a618ad4c5102"
]
```

## Erstellen einer Zielgruppe-Verbindung {#target}

Sie haben jetzt die eindeutigen Bezeichner für eine Datenbankverbindung, ein Schema für die Zielgruppe und einen Datensatz für die Zielgruppe. Mithilfe dieser Bezeichner können Sie eine Zielgruppe-Verbindung mit der API [!DNL Flow Service] erstellen, um den Datensatz anzugeben, der die eingehenden Quelldaten enthalten soll.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `baseConnectionId` | Die ID der Datenbankverbindung Ihres Datensatzes. |
| `data.schema.id` | Die `$id` des Zielgruppe XDM-Schemas. |
| `params.dataSetId` | Die ID des Zielgruppe-Datensatzes. |
| `connectionSpec.id` | Die Verbindungs-Spezifikations-ID für Ihre Cloud-Datenspeicherung. |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung der neuen Zielgruppe-Verbindung (`id`) zurück. Notieren Sie sich diesen Wert, da Sie ihn in späteren Schritten benötigen werden.

```json
{
    "id": "9b3abc95-f2e9-47c1-babc-95f2e927c1ec",
    "etag": "\"7501936b-0000-0200-0000-5e743bcc0000\""
}
```

## Datenfluss erstellen

Der letzte Schritt zur Erfassung von Parquet-Daten aus einer Cloud-Datenspeicherung eines Drittanbieters besteht in der Erstellung eines Datenflusses. Jetzt haben Sie die folgenden erforderlichen Werte vorbereitet:

- [Quell-Verbindungs-ID](#source)
- [Zielgruppen-Verbindungs-ID](#target)

Ein Datenaflow ist für die Planung und Erfassung von Daten aus einer Quelle zuständig. Sie können einen Datenflug erstellen, indem Sie eine POST anfordern und dabei die zuvor genannten Werte in der Nutzlast angeben.

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
| `sourceConnectionIds` | Die Quell-Verbindungs-ID, die in einem früheren Schritt abgerufen wurde. |
| `targetConnectionIds` | Die Zielgruppe-Verbindungs-ID, die in einem früheren Schritt abgerufen wurde. |

**Antwort**

Eine erfolgreiche Antwort gibt die ID (`id`) des neu erstellten Datenflusses zurück.

```json
{
    "id": "89ff50ef-b082-426e-bf50-efb082d26e78",
    "etag": "\"890070b8-0000-0200-0000-5e743c040000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie einen Quell-Connector zur planmäßigen Erfassung von Parquet-Daten aus Ihrem Drittanbieter-Cloud-Datenspeicherung-System erstellt. Eingangsdaten können nun von nachgeschalteten [!DNL Platform]-Diensten wie [!DNL Real-time Customer Profile] und [!DNL Data Science Workspace] verwendet werden. Weitere Informationen finden Sie in den folgenden Dokumenten:

- [Übersicht über das Echtzeit-Kundenprofil](../../../profile/home.md)
- [Übersicht über den Data Science Workspace](../../../data-science-workspace/home.md)
