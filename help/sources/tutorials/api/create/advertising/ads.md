---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Google Ads-Connectors mithilfe der Flow Service API
topic: overview
translation-type: tm+mt
source-git-commit: 950fa88ed6c9235bff98658763b662113bb76caa
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 1%

---


# Erstellen eines Google Ads-Connectors mithilfe der Flow Service API

Mit dem Flow-Dienst werden Kundendaten aus verschiedenen Quellen innerhalb der Adobe Experience Platform erfasst und zentralisiert. Der Dienst stellt eine Benutzeroberfläche und eine RESTful-API bereit, über die alle unterstützten Quellen verbunden werden können.

In diesem Lernprogramm wird die Flow Service API verwendet, um Sie durch die Schritte zur Verbindung von Experience Platform mit Google Ads zu führen.

## Erste Schritte

Dieses Handbuch erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

* [Quellen](../../../../home.md): Mit Experience Platform können Daten aus verschiedenen Quellen erfasst werden, während Sie gleichzeitig die Möglichkeit haben, eingehende Daten mithilfe von Plattformdiensten zu strukturieren, zu beschriften und zu verbessern.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Plattforminstanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der Flow Service API eine Verbindung zu Ad herzustellen.

### Erforderliche Berechtigungen erfassen

Damit der Flow-Dienst eine Verbindung mit Anzeigen herstellen kann, müssen Sie Werte für die folgenden Verbindungseigenschaften bereitstellen:

| **Berechtigung** | **Beschreibung** |
| -------------- | --------------- |
| Kunden-ID des Kunden | Die Kunden-ID des Ads-Kontos. |
| Entwickler-Token | Das mit dem Managerkonto verknüpfte Entwicklertoken. |
| Token aktualisieren | Das Aktualisierungstoken, das von Google für die Autorisierung des Zugriffs auf Anzeigen erhalten wurde. |
| Client-ID | Die Client-ID der Google-Anwendung, mit der das Aktualisierungstoken erfasst wurde. |
| Kundengeheimnis | Das Clientgeheimnis der Google-Anwendung, das zum Abrufen des Aktualisierungstokens verwendet wurde. |
| Verbindungs-ID | Die eindeutige Kennung, die zum Erstellen einer Verbindung erforderlich ist. Die Verbindungsspezifikations-ID für Google Ads lautet: `d771e9c1-4f26-40dc-8617-ce58c4b53702` |

Weitere Informationen zu diesen Werten finden Sie in diesem [Google Ads-Dokument](https://developers.google.com/adwords/api/docs/guides/authentication).

### Lesen von Beispiel-API-Aufrufen

In diesem Lernprogramm finden Sie Beispiele für API-Aufrufe, die zeigen, wie Sie Ihre Anforderungen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anforderungs-Nutzdaten. Beispiel-JSON, die in API-Antworten zurückgegeben wird, wird ebenfalls bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für Experience Platform.

### Werte für erforderliche Kopfzeilen sammeln

Um Aufrufe an Plattform-APIs durchführen zu können, müssen Sie zunächst das [Authentifizierungslehrgang](../../../../../tutorials/authentication.md)abschließen. Das Abschließen des Authentifizierungstreutorials stellt die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform API-Aufrufen bereit, wie unten dargestellt:

* Genehmigung: Träger `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in Experience Platform, einschließlich der Ressourcen des Flow-Dienstes, werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an Plattform-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird:

* x-sandbox-name: `{SANDBOX_NAME}`

Für alle Anforderungen, die eine Payload enthalten (POST, PUT, PATCH), ist ein zusätzlicher Medientyp-Header erforderlich:

* Content-Type: `application/json`

## Verbindung herstellen

Eine Verbindung gibt eine Quelle an und enthält Ihre Anmeldeinformationen für diese Quelle. Pro Google Ads-Konto ist nur eine Verbindung erforderlich, da sie zum Erstellen mehrerer Quell-Connectors verwendet werden kann, um verschiedene Daten einzubringen.

**API-Format**

```https
POST /connections
```

**Anfrage**

Um eine Google Ads-Verbindung zu erstellen, muss die eindeutige Verbindungs-ID als Teil der POST-Anforderung angegeben werden. Die Verbindungsspezifikations-ID für Google Ads lautet `221c7626-58f6-4eec-8ee2-042b0226f03b`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "google-ads connection",
        "description": "Connection for google-ads",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "clientCustomerID": "{CLIENT_CUSTOMER_ID}",
                "developerToken": "{DEVELOPER_TOKEN}",
                "authenticationType": "{AUTHENTICATION_TYPE}"
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "d771e9c1-4f26-40dc-8617-ce58c4b53702",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| --------- | ----------- |
| `auth.params.clientCustomerID` | Die Kunden-ID Ihres Anzeigenkontos. |
| `auth.params.developerToken` | Das Entwicklertoken Ihres Anzeigenkontos. |
| `auth.params.refreshToken` | Das Aktualisierungstoken Ihres Anzeigenkontos. |
| `auth.params.clientID` | Die Client-ID Ihres Anzeigenkontos. |
| `auth.params.clientSecret` | Das Kundengeheimnis Ihres Anzeigenkontos. |
| `connectionSpec.id` | Die Google Ads-Verbindungs-ID: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Verbindung zurück, einschließlich der eindeutigen Kennung (`id`). Diese ID ist erforderlich, um Ihre Daten im nächsten Lernprogramm zu untersuchen.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Nächste Schritte

In diesem Lernprogramm haben Sie eine Google Ads-Verbindung mit der Flow Service API erstellt und den eindeutigen ID-Wert der Verbindung erhalten. Sie können diese ID im nächsten Lernprogramm verwenden, um zu erfahren, wie Sie mithilfe der Flow Service API [Werbetechnologien](../../explore/advertising.md)untersuchen.
