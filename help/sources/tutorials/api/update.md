---
keywords: Experience Platform;Startseite;beliebte Themen;Flow Service;Konten aktualisieren
solution: Experience Platform
title: Aktualisieren von Konten mithilfe der Flow Service-API
topic-legacy: overview
type: Tutorial
description: In diesem Tutorial werden die Schritte zum Aktualisieren der Details und Anmeldeinformationen eines Kontos mithilfe der Flow Service-API beschrieben.
exl-id: a93385fd-ed36-457f-8882-41e37f6f209d
source-git-commit: 95f455bd03b7baefe0133a9818c9d048f36f9d38
workflow-type: ht
source-wordcount: '523'
ht-degree: 100%

---

# Aktualisieren von Konten mithilfe der Flow Service-API

Unter bestimmten Umständen kann es erforderlich sein, die Details einer vorhandenen Quellverbindung zu aktualisieren. [!DNL Flow Service] bietet Ihnen die Möglichkeit, Details einer vorhandenen Batch- oder Streaming-Verbindung, einschließlich Name, Beschreibung und Anmeldeinformationen, hinzuzufügen, zu bearbeiten und zu löschen.

In diesem Tutorial werden die Schritte zum Aktualisieren der Details und Anmeldeinformationen einer Verbindung mithilfe der [[!DNL Flow Service] -API](https://www.adobe.io/experience-platform-apis/references/flow-service/) beschrieben.

## Erste Schritte

Für dieses Tutorial benötigen Sie eine vorhandene Verbindung und eine gültige Verbindungs-ID. Wenn Sie noch keine Verbindung haben, wählen Sie die gewünschte Quelle aus der [Übersicht über Quellen](../../home.md) und führen Sie vor diesem Tutorial die beschriebenen Schritte aus.

Dieses Tutorial setzt außerdem ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Verwenden von Platform-APIs

Informationen zum erfolgreichen Aufrufen von Platform-APIs finden Sie im Handbuch zu den [Ersten Schritten mit Platform-APIs](../../../landing/api-guide.md).

## Nachschlagen von Verbindungsdetails

Der erste Schritt beim Aktualisieren Ihrer Verbindung besteht darin, ihre Details mithilfe Ihrer Verbindungs-ID abzurufen. Um die aktuellen Details Ihrer Verbindung abzurufen,stellen Sie eine GET-Anfrage an die [!DNL Flow Service]-API und geben Sie dabei die Verbindungs-ID der Verbindung an, die Sie aktualisieren möchten.

**API-Format**

```http
GET /connections/{CONNECTION_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{CONNECTION_ID}` | Der eindeutige `id`-Wert für die Verbindung, die Sie abrufen möchten. |

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

Bei einer erfolgreichen Antwort werden die aktuellen Details Ihrer Verbindung zurückgegeben, einschließlich der Anmeldedaten, der eindeutigen Kennung (`id`) und der Version. Der Versionswert ist erforderlich, um Ihre Verbindung zu aktualisieren.

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

## Aktualisieren der Verbindung

Um den Namen, die Beschreibung und die Anmeldeinformationen Ihrer Verbindung zu aktualisieren, führen Sie eine PATCH-Anfrage an die [!DNL Flow Service]-API durch und geben Sie dabei Ihre Verbindungs-ID, die Version und die neuen Informationen an, die Sie verwenden möchten.

>[!IMPORTANT]
>
>Die `If-Match`-Kopfzeile ist bei einer PATCH-Anfrage erforderlich. Der Wert für diese Kopfzeile ist die eindeutige Version der Verbindung, die Sie aktualisieren möchten.

**API-Format**

```http
PATCH /connections/{CONNECTION_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{CONNECTION_ID}` | Der eindeutige `id`-Wert für die Verbindung, die Sie aktualisieren möchten. |

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

Bei einer erfolgreichen Antwort werden Ihre Verbindungs-ID und ein aktualisiertes eTag zurückgegeben. Sie können die Aktualisierung überprüfen, indem Sie eine GET-Anfrage an die [!DNL Flow Service]-API stellen und dabei Ihre Verbindungs-ID angeben.

```json
{
    "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
    "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie mithilfe der [!DNL Flow Service]-API die Anmeldeinformationen und Informationen für Ihre Verbindung aktualisiert. Weitere Informationen zur Verwendung von Quell-Connectoren finden Sie im Abschnitt [Quellen – Übersicht](../../home.md).
