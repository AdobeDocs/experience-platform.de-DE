---
keywords: Experience Platform; Startseite; beliebte Themen; Flussdienst; Konten aktualisieren
solution: Experience Platform
title: Aktualisieren von Konten mithilfe der Flow Service-API
topic-legacy: overview
type: Tutorial
description: In diesem Tutorial werden die Schritte zum Aktualisieren der Details und Anmeldeinformationen eines Kontos mithilfe der Flow Service-API beschrieben.
exl-id: a93385fd-ed36-457f-8882-41e37f6f209d
source-git-commit: 95f455bd03b7baefe0133a9818c9d048f36f9d38
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 15%

---

# Aktualisieren von Konten mithilfe der Flow Service-API

Unter bestimmten Umständen kann es erforderlich sein, die Details einer vorhandenen Quellverbindung zu aktualisieren. [!DNL Flow Service] bietet Ihnen die Möglichkeit, Details einer vorhandenen Batch- oder Streaming-Verbindung, einschließlich Name, Beschreibung und Anmeldeinformationen, hinzuzufügen, zu bearbeiten und zu löschen.

In diesem Tutorial werden die Schritte zum Aktualisieren der Details und Anmeldedaten einer Verbindung mit dem [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Für dieses Tutorial benötigen Sie eine vorhandene Verbindung und eine gültige Verbindungs-ID. Wenn Sie noch keine Verbindung haben, wählen Sie die gewünschte Quelle aus der [Quellen - Übersicht](../../home.md) und führen Sie die Schritte aus, die vor dem Versuch dieses Tutorials beschrieben wurden.

Für dieses Tutorial benötigen Sie außerdem ein Verständnis der folgenden Komponenten von Adobe Experience Platform:

* [Quellen](../../home.md): Experience Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von Platform-Diensten zu strukturieren, zu beschriften und zu erweitern.
* [Sandboxes](../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Anwendungen für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Verwenden von Platform-APIs

Informationen zum erfolgreichen Aufrufen von Platform-APIs finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../landing/api-guide.md).

## Verbindungsdetails nachschlagen

Der erste Schritt beim Aktualisieren Ihrer Verbindung besteht darin, ihre Details mithilfe Ihrer Verbindungs-ID abzurufen. Um die aktuellen Details Ihrer Verbindung abzurufen, stellen Sie eine GET-Anfrage an die [!DNL Flow Service] API bei Angabe der Verbindungs-ID der Verbindung, die Sie aktualisieren möchten.

**API-Format**

```http
GET /connections/{CONNECTION_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{CONNECTION_ID}` | Die eindeutige `id` für die Verbindung, die Sie abrufen möchten. |

**Anfrage**

Mit der folgenden Anfrage werden Informationen zu Ihrer Verbindung abgerufen.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die aktuellen Details Ihrer Verbindung zurück, einschließlich der Anmeldeinformationen, der eindeutigen Kennung (`id`) und -Version. Der Versionswert ist erforderlich, um Ihre Verbindung zu aktualisieren.

```json
{
    "items": [
        {
            "createdAt": 1597973312000,
            "updatedAt": 1597973312000,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxName": "{SANDBOX_NAME}",
            "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
            "name": "E2E_SF Base_Connection",
            "connectionSpec": {
                "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Basic Authentication",
                "params": {
                    "securityToken": "{SECURITY_TOKEN}",
                    "password": "{PASSWORD}",
                    "username": "my-salesforce-account",
                    "environmentUrl": "login.salesforce.com"
                }
            },
            "version": "\"1400dd53-0000-0200-0000-5f3f23450000\"",
            "etag": "\"1400dd53-0000-0200-0000-5f3f23450000\""
        }
    ]
}
```

## Verbindung aktualisieren

Um den Namen, die Beschreibung und die Anmeldeinformationen Ihrer Verbindung zu aktualisieren, führen Sie eine PATCH-Anfrage an die [!DNL Flow Service] API bei der Angabe Ihrer Verbindungs-ID, -Version und der neuen Informationen, die Sie verwenden möchten.

>[!IMPORTANT]
>
>Die `If-Match` -Kopfzeile ist bei einer PATCH-Anfrage erforderlich. Der Wert für diesen Header ist die eindeutige Version der Verbindung, die Sie aktualisieren möchten.

**API-Format**

```http
PATCH /connections/{CONNECTION_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{CONNECTION_ID}` | Die eindeutige `id` für die Verbindung, die Sie aktualisieren möchten. |

**Anfrage**

Die folgende Anfrage enthält einen neuen Namen und eine neue Beschreibung sowie einen neuen Satz von Anmeldeinformationen, mit denen Sie Ihre Verbindung aktualisieren können.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: 1400dd53-0000-0200-0000-5f3f23450000' \
    -d '[
        {
            "op": "replace",
            "path": "/auth/params",
            "value": {
                "username": "salesforce-connector-username",
                "password": "{NEW_PASSWORD}",
                "securityToken": "{NEW_SECURITY_TOKEN}"
            }
        },
        {
            "op": "replace",
            "path": "/name",
            "value": "Test salesforce connection"
        },
        {
            "op": "add",
            "path": "/description",
            "value": "A test salesforce connection"
        }
    ]'
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `op` | Der Operationsaufruf, der für die Definition der zum Aktualisieren der Verbindung erforderlichen Aktion verwendet wird. Operationen umfassen: `add`, `replace` und `remove`. |
| `path` | Der Pfad des zu aktualisierenden Parameters. |
| `value` | Der neue Wert, mit dem Sie Ihren Parameter aktualisieren möchten. |

**Antwort**

Bei einer erfolgreichen Antwort werden Ihre Verbindungs-ID und ein aktualisiertes eTag zurückgegeben. Sie können die Aktualisierung überprüfen, indem Sie eine GET-Anfrage an die [!DNL Flow Service] API bei gleichzeitiger Angabe Ihrer Verbindungs-ID.

```json
{
    "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
    "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie die Anmeldeinformationen und Informationen für Ihre Verbindung mit der [!DNL Flow Service] API. Weitere Informationen zur Verwendung von Quell-Connectoren finden Sie im Abschnitt [Quellen - Übersicht](../../home.md).
