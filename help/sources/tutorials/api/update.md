---
keywords: Experience Platform;home;popular topics; flow service; update connections
solution: Experience Platform
title: Aktualisieren von Verbindungsinformationen mithilfe der Flow Service API
topic: overview
type: Tutorial
description: Unter bestimmten Umständen kann es erforderlich sein, die Details einer bestehenden Quellverbindung zu aktualisieren. Die Flow Service API bietet Ihnen die Möglichkeit, Details zu einer vorhandenen Stapel- oder Streaming-Verbindung, einschließlich Name, Beschreibung und Anmeldeinformationen, hinzuzufügen, zu bearbeiten und zu löschen.
translation-type: tm+mt
source-git-commit: d1a9f7d0c83b8bb34e26b6e5a9825488e62b43de
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 25%

---


# Aktualisieren von Verbindungsinformationen mithilfe der Flow Service API

Unter bestimmten Umständen kann es erforderlich sein, die Details einer bestehenden Quellverbindung zu aktualisieren. [!DNL Flow Service] bietet Ihnen die Möglichkeit, Details zu einer vorhandenen Stapel- oder Streaming-Verbindung, einschließlich Name, Beschreibung und Anmeldeinformationen, hinzuzufügen, zu bearbeiten und zu löschen.

In diesem Lernprogramm werden die Schritte zum Aktualisieren der Details und Anmeldeinformationen einer bestehenden Verbindung mit dem [[!DNL Flow Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)Handbuch beschrieben.

## Erste Schritte

Für dieses Lernprogramm ist eine gültige Verbindungs-ID erforderlich. Wenn Sie keine gültige Verbindungs-ID haben, wählen Sie den gewünschten Connector aus der [Quellenübersicht](../../home.md) und führen Sie die Schritte aus, die Sie vor dem Versuch dieses Lernprogramms beschrieben haben.

Für dieses Lernprogramm müssen Sie außerdem die folgenden Komponenten von Adobe Experience Platform kennen:

* [Quellen](../../home.md): [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von [!DNL Platform] Diensten zu strukturieren, zu beschriften und zu verbessern.
* [Sandboxen](../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

The following sections provide additional information that you will need to know in order to successfully update your connection&#39;s information using the [!DNL Flow Service] API.

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](../../../tutorials/authentication.md) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

All resources in [!DNL Experience Platform], including those belonging to [!DNL Flow Service], are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

* `x-sandbox-name: {SANDBOX_NAME}`

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

* `Content-Type: application/json`

## Verbindungsdetails suchen

>[!NOTE]
>In diesem Lernprogramm wird der [Salesforce-Quellanschluss](../../connectors/crm/salesforce.md) als Beispiel verwendet, die beschriebenen Schritte gelten jedoch für alle [verfügbaren Quellschnittstellen](../../home.md).

Der erste Schritt beim Aktualisieren Ihrer Verbindungsinformationen besteht darin, Verbindungsdetails mit Ihrer Verbindungs-ID abzurufen.

**API-Format**

```http
GET /connections/{CONNECTION_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{CONNECTION_ID}` | Der eindeutige `id` Wert für die Verbindung, die Sie abrufen möchten. |

**Anfrage**

Im Folgenden werden Informationen zu Ihrer Verbindungs-ID abgerufen.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die aktuellen Details Ihrer Verbindung zurück, einschließlich der Anmeldeinformationen, der eindeutigen Kennung (`id`) und der Version.

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

Nachdem Sie über eine Verbindungs-ID verfügen, führen Sie eine PATCH-Anforderung an die [!DNL Flow Service] API durch.

>[!IMPORTANT]
>Eine PATCH-Anforderung erfordert die Verwendung des `If-Match` Headers. Der Wert für diesen Header ist die eindeutige Version Ihrer Verbindung.

**API-Format**

```http
PATCH /connections/{CONNECTION_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{CONNECTION_ID}` | Der eindeutige `id` Wert für die Verbindung, die Sie aktualisieren möchten. |

**Anfrage**

Die folgende Anforderung enthält neue Informationen, mit denen Sie Ihre Verbindung aktualisieren können.

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

Bei einer erfolgreichen Antwort werden Ihre Verbindungs-ID und ein aktualisierter Tag zurückgegeben.

```json
{
    "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
    "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
}
```

## Aktualisierte Verbindungsdetails nachschlagen

Sie können die gleiche Verbindungs-ID abrufen, die Sie aktualisiert haben, um die vorgenommenen Änderungen zu sehen, indem Sie eine GET an die [!DNL Flow Service] API anfordern.

**API-Format**

```http
GET /connections/{CONNECTION_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{CONNECTION_ID}` | Der eindeutige `id` Wert für die Verbindung, die Sie abrufen möchten. |

**Anfrage**

Die folgende Anforderung ruft aktualisierte Informationen zu Ihrer Verbindungs-ID ab.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die aktualisierten Details Ihrer Verbindungs-ID zurück, einschließlich des neuen Namens, der Beschreibung und der Version.

```json
{
    "items": [
        {
            "createdAt": 1597973312000,
            "updatedAt": 1598038319627,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxName": "{SANDBOX_NAME}",
            "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
            "name": "Test salesforce connection",
            "description": "A test salesforce connection",
            "connectionSpec": {
                "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Basic Authentication",
                "params": {
                    "securityToken": "{NEW_SECURITY_TOKEN}",
                    "password": "{PASSWORD}",
                    "username": "salesforce-connector-username"
                }
            },
            "version": "\"3600e378-0000-0200-0000-5f40212f0000\"",
            "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
        }
    ]
}
```

## Nächste Schritte

Durch Befolgen dieses Lernprogramms haben Sie die mit Ihrer Verbindung verknüpften Anmeldeinformationen und Informationen mit der [!DNL Flow Service] API aktualisiert. Weitere Informationen zur Verwendung von Quellschnittstellen finden Sie in der Übersicht über die [Quellen](../../home.md).
