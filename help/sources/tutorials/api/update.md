---
keywords: Experience Platform;Home;beliebte Themen;Flussdienst;Updateverbindungen
solution: Experience Platform
title: Verbindungen mithilfe der Flow Service API aktualisieren
topic: Übersicht
type: Tutorial
description: In diesem Lernprogramm werden die Schritte zum Aktualisieren der Details und Anmeldeinformationen einer Verbindung mithilfe der Flow Service API beschrieben.
translation-type: tm+mt
source-git-commit: 5187647dfcf82a476bc776bf2b606db228ca70a4
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 31%

---


# Aktualisieren von Verbindungen mithilfe der Flow Service API

Unter bestimmten Umständen kann es erforderlich sein, die Details einer bestehenden Quellverbindung zu aktualisieren. [!DNL Flow Service] bietet Ihnen die Möglichkeit, Details zu einer vorhandenen Stapel- oder Streaming-Verbindung, einschließlich Name, Beschreibung und Anmeldeinformationen, hinzuzufügen, zu bearbeiten und zu löschen.

Dieses Lernprogramm beschreibt die Schritte zum Aktualisieren der Details und Anmeldedaten einer Verbindung mit der [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Erste Schritte

Für dieses Lernprogramm müssen Sie über eine bestehende Verbindung und eine gültige Verbindungs-ID verfügen. Wenn Sie über keine bestehende Verbindung verfügen, wählen Sie die gewünschte Quelle aus dem [Sources-Überblick](../../home.md) und befolgen Sie die Schritte, die Sie vor dem Versuch dieses Lernprogramms beschrieben haben.

Für dieses Lernprogramm müssen Sie außerdem die folgenden Komponenten von Adobe Experience Platform kennen:

* [Quellen](../../home.md): Experience Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von Plattformdiensten zu strukturieren, zu kennzeichnen und zu verbessern.
* [Sandboxes](../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Anwendungen für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um eine Verbindung mit der [!DNL Flow Service]-API erfolgreich zu aktualisieren.

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für Experience Platform.

### Sammeln von Werten für erforderliche Kopfzeilen

Um Platform-APIs aufrufen zu können, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://www.adobe.com/go/platform-api-authentication-en) abschließen. Im Rahmen des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alle Ressourcen in Experience Platform, einschließlich der Ressourcen von [!DNL Flow Service], werden zu bestimmten virtuellen Sandboxen isoliert. Bei allen Anfragen an Platform-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

* `x-sandbox-name: {SANDBOX_NAME}`

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

* `Content-Type: application/json`

## Verbindungsdetails suchen

Der erste Schritt beim Aktualisieren der Verbindung besteht darin, ihre Details mit Ihrer Verbindungs-ID abzurufen. Um die aktuellen Verbindungsdetails abzurufen, fordern Sie eine GET an die [!DNL Flow Service]-API an, während Sie die Verbindungs-ID für die zu aktualisierende Verbindung angeben.

**API-Format**

```http
GET /connections/{CONNECTION_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{CONNECTION_ID}` | Der eindeutige Wert `id` für die Verbindung, die Sie abrufen möchten. |

**Anfrage**

Die folgende Anforderung ruft Informationen zu Ihrer Verbindung ab.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die aktuellen Details Ihrer Verbindung zurück, einschließlich der Anmeldeinformationen, der eindeutigen Kennung (`id`) und der Version. Der Versionswert ist erforderlich, um Ihre Verbindung zu aktualisieren.

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

Um den Namen, die Beschreibung und die Anmeldeinformationen Ihrer Verbindung zu aktualisieren, führen Sie eine PATCH-Anforderung an die [!DNL Flow Service]-API durch und geben Sie dabei Ihre Verbindungs-ID, Ihre Version und die neuen Informationen ein, die Sie verwenden möchten.

>[!IMPORTANT]
>
>Die `If-Match`-Kopfzeile ist bei einer PATCH-Anforderung erforderlich. Der Wert für diesen Header ist die eindeutige Version der Verbindung, die Sie aktualisieren möchten.

**API-Format**

```http
PATCH /connections/{CONNECTION_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{CONNECTION_ID}` | Der eindeutige Wert `id` für die Verbindung, die Sie aktualisieren möchten. |

**Anfrage**

Die folgende Anforderung enthält einen neuen Namen und eine neue Beschreibung sowie einen neuen Satz Anmeldeinformationen, mit denen Sie Ihre Verbindung aktualisieren können.

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

Bei einer erfolgreichen Antwort werden Ihre Verbindungs-ID und ein aktualisierter Tag zurückgegeben. Sie können die Aktualisierung überprüfen, indem Sie eine GET an die [!DNL Flow Service]-API anfordern und dabei Ihre Verbindungs-ID angeben.

```json
{
    "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
    "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
}
```

## Nächste Schritte

In diesem Lernprogramm haben Sie die mit Ihrer Verbindung verknüpften Anmeldeinformationen und Informationen mit der API [!DNL Flow Service] aktualisiert. Weitere Informationen zur Verwendung von Quellschnittstellen finden Sie unter [Quellübersicht](../../home.md).
