---
keywords: Experience Platform; Startseite; beliebte Themen; Azure Azure Data Explorer; Azure Data Explorer; Azure Data Explorer
solution: Experience Platform
title: Erstellen einer Azure Azure Data Explorer-Basisverbindung mit der Flow Service-API
type: Tutorial
description: Erfahren Sie, wie Sie mit der Flow Service-API Azure Data Explorer mit Adobe Experience Platform verbinden.
exl-id: 1b17bbb0-1f7b-4d89-a158-ad269e6edf30
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 64%

---

# Erstellen einer [!DNL Azure Azure Data Explorer]-Basisverbindung mithilfe der [!DNL Flow Service]-API

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL Azure Data Explorer] mithilfe der [[!DNL Flow Service] -API](https://www.adobe.io/experience-platform-apis/references/flow-service/).


## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um eine erfolgreiche Verbindung zu [!DNL Azure Data Explorer] mithilfe der [!DNL Flow Service] API.

### Sammeln erforderlicher Anmeldeinformationen

Damit [!DNL Flow Service] eine Verbindung mit [!DNL Azure Data Explorer] herstellen kann, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| `endpoint` | Der Endpunkt des [!DNL Azure Data Explorer]-Servers. |
| `database` | Der Name der [!DNL Azure Data Explorer] Datenbank. |
| `tenant` | Die eindeutige Mandantenkennung, die für die Verbindung mit der [!DNL Azure Data Explorer] Datenbank. |
| `servicePrincipalId` | Die eindeutige Dienstprinzipal-ID, die für die Verbindung mit dem [!DNL Azure Data Explorer] Datenbank. |
| `servicePrincipalKey` | Der Hauptschlüssel des eindeutigen Dienstes, der für die Verbindung mit dem [!DNL Azure Data Explorer] Datenbank. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL Azure Data Explorer] ist `0479cc14-7651-4354-b233-7480606c2ac3`. |

Weitere Informationen zu den ersten Schritten finden Sie in diesem [[!DNL Azure Data Explorer] Dokument](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad).

### Verwenden von Platform-APIs

Informationen zum Aufrufen von Platform-APIs finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Erstellen einer Basisverbindung

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basisverbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den Endpunkt `/connections` und geben Sie dabei Ihre [!DNL Azure Data Explorer]-Authentifizierungsdaten als Teil der Anfrageparameter an.

**API-Format**

```https
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Azure Data Explorer]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Azure Data Explorer connection",
        "description": "A connection for Azure Azure Data Explorer",
        "auth": {
            "specName": "Service Principal Based Authentication",
            "params": {
                    "endpoint": "{ENDPOINT}",
                    "database": "{DATABASE}",
                    "tenant": "{TENANT}",
                    "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                    "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}"
                }
        },
        "connectionSpec": {
            "id": "0479cc14-7651-4354-b233-7480606c2ac3",
            "version": "1.0"
        }
    }'
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `auth.params.endpoint` | Der Endpunkt des [!DNL Azure Data Explorer]-Servers. |
| `auth.params.database` | Der Name der [!DNL Azure Data Explorer] Datenbank. |
| `auth.params.tenant` | Die eindeutige Mandantenkennung, die für die Verbindung mit der [!DNL Azure Data Explorer] Datenbank. |
| `auth.params.servicePrincipalId` | Die eindeutige Dienstprinzipal-ID, die für die Verbindung mit dem [!DNL Azure Data Explorer] Datenbank. |
| `auth.params.servicePrincipalKey` | Der Hauptschlüssel des eindeutigen Dienstes, der für die Verbindung mit dem [!DNL Azure Data Explorer] Datenbank. |
| `connectionSpec.id` | Die [!DNL Azure Data Explorer]-Verbindungsspezifikations-ID: `0479cc14-7651-4354-b233-7480606c2ac3`. |

**Antwort**

Eine erfolgreiche Antwort gibt Details der neu erstellten Verbindung zurück, einschließlich ihrer eindeutigen Kennung (`id`). Diese ID ist erforderlich, um Ihre Daten im nächsten Tutorial zu untersuchen.

```json
{
    "id": "f088e4f2-2464-480c-88e4-f22464b80c90",
    "etag": "\"43011faa-0000-0200-0000-5ea740cd0000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL Azure Data Explorer]-Basisverbindung mithilfe der [!DNL Flow Service]-API erstellt. Sie können diese Basisverbindungs-ID in den folgenden Tutorials verwenden:

* [Erkunden von Struktur und Inhalten Ihrer Datentabellen mithilfe der  [!DNL Flow Service] -API](../../explore/tabular.md)
* [Erstellen Sie einen Datenfluss, um Datenbankdaten mit der [!DNL Flow Service] API](../../collect/database-nosql.md)
