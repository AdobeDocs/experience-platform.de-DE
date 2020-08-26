---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines HubSpot-Connectors mit der Flow Service API
topic: overview
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 19%

---


# Erstellen eines [!DNL HubSpot] Connectors mit der [!DNL Flow Service] API

>[!NOTE]
>
>Der [!DNL HubSpot] Anschluss befindet sich in der Betaphase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie in der Übersicht [zu den](../../../../home.md#terms-and-conditions) Quellen.

[!DNL Flow Service] wird zur Erfassung und Zentralisierung von Kundendaten aus unterschiedlichen Quellen innerhalb von Adobe Experience Platform verwendet. Der Dienst stellt eine Benutzeroberfläche und eine RESTful-API bereit, über die alle unterstützten Quellen verbunden werden können.

Dieses Lernprogramm verwendet die [!DNL Flow Service] API, um Sie durch die Schritte zu führen, mit denen Sie eine Verbindung herstellen [!DNL Experience Platform] können [!DNL HubSpot].

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von [!DNL Platform] Diensten zu strukturieren, zu beschriften und zu verbessern.
* [Sandboxen](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

The following sections provide additional information that you will need to know in order to successfully connect to [!DNL HubSpot] using the [!DNL Flow Service] API.

### Erforderliche Anmeldedaten sammeln

Damit eine Verbindung [!DNL Flow Service] mit [!DNL HubSpot]hergestellt werden kann, müssen Sie die folgenden Verbindungseigenschaften angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| Client-ID | Die mit Ihrer [!DNL HubSpot] Anwendung verknüpfte Client-ID. |
| geheimer Clientschlüssel | Das mit Ihrer [!DNL HubSpot] Anwendung verknüpfte Clientgeheimnis. |
| Zugriffstoken | Das Zugriffstoken, das beim erstmaligen Authentifizieren der OAuth-Integration erhalten wurde. |
| Token aktualisieren | Das Aktualisierungstoken, das beim erstmaligen Authentifizieren der OAuth-Integration erhalten wurde. |
| Verbindungs-ID | Die eindeutige Kennung, die zum Erstellen einer Verbindung erforderlich ist. Die Verbindungs-Spezifikations-ID für [!DNL HubSpot] lautet: `cc6a4487-9e91-433e-a3a3-9cf6626c1806` |

Weitere Informationen zum Einstieg finden Sie in diesem [HubSpot-Dokument](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview).

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

In order to make calls to [!DNL Platform] APIs, you must first complete the [authentication tutorial](../../../../../tutorials/authentication.md). Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform], including those belonging to the [!DNL Flow Service], are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

* x-sandbox-name: `{SANDBOX_NAME}`

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

* Content-Type: `application/json`

## Verbindung erstellen

Eine Verbindung gibt eine Quelle an und enthält Ihre Anmeldeinformationen für diese Quelle. Pro [!DNL HubSpot] Konto ist nur eine Verbindung erforderlich, da sie zum Erstellen mehrerer Quell-Connectors verwendet werden kann, um verschiedene Daten einzubringen.

**API-Format**

```https
POST /connections
```

**Anfrage**

Zur Erstellung einer [!DNL HubSpot] Verbindung muss die eindeutige Verbindungs-ID als Teil der POST angegeben werden. Die Verbindungs-ID für [!DNL HubSpot] lautet `cc6a4487-9e91-433e-a3a3-9cf6626c1806`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "connection for hubspot",
        "description": "connection for hubspot",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "accessToken": "{ACCESS_TOKEN}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
            "version": "1.0"
        }
    }
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `auth.params.clientId` | Die mit Ihrer [!DNL HubSpot] Anwendung verknüpfte Client-ID. |
| `auth.params.clientSecret` | Das mit Ihrer [!DNL HubSpot] Anwendung verknüpfte Clientgeheimnis. |
| `auth.params.accessToken` | Das Zugriffstoken, das beim erstmaligen Authentifizieren der OAuth-Integration erhalten wurde. |
| `auth.params.refreshToken` | Das Aktualisierungstoken, das beim erstmaligen Authentifizieren der OAuth-Integration erhalten wurde. |

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Verbindung für die API zurück, einschließlich der eindeutigen Kennung (`id`). Diese ID ist erforderlich, um Ihre Daten im nächsten Lernprogramm zu untersuchen.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

In diesem Lernprogramm haben Sie eine [!DNL HubSpot] Verbindung mit der [!DNL Flow Service] API erstellt und den eindeutigen ID-Wert der Verbindung erhalten. Sie können diese Verbindungs-ID im nächsten Lernprogramm verwenden, um zu erfahren, wie Sie Marketingautomatisierungssysteme mithilfe der Flow Service API [untersuchen](../../explore/marketing-automation.md).