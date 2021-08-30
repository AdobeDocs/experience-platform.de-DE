---
keywords: Experience Platform; Startseite; beliebte Themen; Flussdienst; Konten aktualisieren
solution: Experience Platform
title: Aktualisieren von Konten mithilfe der Flow Service-API
topic-legacy: overview
type: Tutorial
description: In diesem Tutorial werden die Schritte zum Aktualisieren der Details und Anmeldeinformationen eines Kontos mithilfe der Flow Service-API beschrieben.
exl-id: a93385fd-ed36-457f-8882-41e37f6f209d
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 32%

---

# Aktualisieren von Konten mithilfe der Flow Service-API

Unter bestimmten Umständen kann es erforderlich sein, die Details einer vorhandenen Quellverbindung zu aktualisieren. [!DNL Flow Service] bietet Ihnen die Möglichkeit, Details einer vorhandenen Batch- oder Streaming-Verbindung, einschließlich Name, Beschreibung und Anmeldeinformationen, hinzuzufügen, zu bearbeiten und zu löschen.

In diesem Tutorial werden die Schritte zum Aktualisieren der Details und Anmeldeinformationen einer Verbindung mit der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) beschrieben.

## Erste Schritte

Für dieses Tutorial benötigen Sie eine vorhandene Verbindung und eine gültige Verbindungs-ID. Wenn Sie noch keine Verbindung haben, wählen Sie Ihre gewünschte Quelle aus der [Quellen-Übersicht](../../home.md) aus und führen Sie die Schritte aus, die vor dem Versuch dieses Tutorials beschrieben werden.

Für dieses Tutorial benötigen Sie außerdem ein Verständnis der folgenden Komponenten von Adobe Experience Platform:

* [Quellen](../../home.md): Experience Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von Platform-Diensten zu strukturieren, zu beschriften und zu erweitern.
* [Sandboxes](../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Anwendungen für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um eine Verbindung mithilfe der [!DNL Flow Service]-API erfolgreich aktualisieren zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für Experience Platform.

### Sammeln von Werten für erforderliche Kopfzeilen

Um Platform-APIs aufrufen zu können, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de#platform-apis) abschließen. Im Rahmen des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alle Ressourcen in der Experience Platform, einschließlich der Ressourcen, die zu [!DNL Flow Service] gehören, werden auf bestimmte virtuelle Sandboxes beschränkt. Bei allen Anfragen an Platform-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

* `x-sandbox-name: {SANDBOX_NAME}`

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

* `Content-Type: application/json`

## Verbindungsdetails nachschlagen

Der erste Schritt beim Aktualisieren Ihrer Verbindung besteht darin, ihre Details mithilfe Ihrer Verbindungs-ID abzurufen. Um die aktuellen Details Ihrer Verbindung abzurufen, stellen Sie eine GET-Anfrage an die [!DNL Flow Service]-API und geben Sie dabei die Verbindungs-ID der Verbindung an, die Sie aktualisieren möchten.

**API-Format**

```http
GET /connections/{CONNECTION_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{CONNECTION_ID}` | Der eindeutige `id` -Wert für die Verbindung, die Sie abrufen möchten. |

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

Um den Namen, die Beschreibung und die Anmeldeinformationen Ihrer Verbindung zu aktualisieren, führen Sie eine PATCH-Anfrage an die [!DNL Flow Service]-API durch und geben Sie dabei Ihre Verbindungs-ID, -Version und die neuen Informationen ein, die Sie verwenden möchten.

>[!IMPORTANT]
>
>Die Kopfzeile `If-Match` ist bei einer PATCH-Anfrage erforderlich. Der Wert für diesen Header ist die eindeutige Version der Verbindung, die Sie aktualisieren möchten.

**API-Format**

```http
PATCH /connections/{CONNECTION_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{CONNECTION_ID}` | Der eindeutige `id` -Wert für die Verbindung, die Sie aktualisieren möchten. |

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

Bei einer erfolgreichen Antwort werden Ihre Verbindungs-ID und ein aktualisiertes eTag zurückgegeben. Sie können die Aktualisierung überprüfen, indem Sie eine GET-Anfrage an die [!DNL Flow Service]-API richten und dabei Ihre Verbindungs-ID angeben.

```json
{
    "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
    "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie die Anmeldeinformationen und Informationen für Ihre Verbindung mithilfe der [!DNL Flow Service]-API aktualisiert. Weitere Informationen zur Verwendung von Quell-Connectoren finden Sie in der [Quellenübersicht](../../home.md).
