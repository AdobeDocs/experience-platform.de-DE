---
keywords: Experience Platform;home;popular topics;MariaDB;mariadb
solution: Experience Platform
title: Erstellen eines MariaDB-Connectors mit der Flow Service API
topic: overview
type: Tutorial
description: In diesem Lernprogramm wird die Flow Service API verwendet, um Sie durch die Schritte zur Verbindung von Experience Platform] mit MariaDB zu führen.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 27%

---


# Erstellen eines [!DNL MariaDB] Connectors mit der [!DNL Flow Service] API

>[!NOTE]
>
>Der [!DNL MariaDB] Anschluss befindet sich in der Betaphase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie in der Übersicht [zu den](../../../../home.md#terms-and-conditions) Quellen.

[!DNL Flow Service] wird zur Erfassung und Zentralisierung von Kundendaten aus unterschiedlichen Quellen innerhalb von Adobe Experience Platform verwendet. Der Dienst stellt eine Benutzeroberfläche und eine RESTful-API bereit, über die alle unterstützten Quellen verbunden werden können.

Dieses Lernprogramm verwendet die [!DNL Flow Service] API, um Sie durch die Schritte zu führen, mit denen eine Verbindung hergestellt [!DNL Experience Platform] werden soll [!DNL MariaDB].

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von [!DNL Platform] Diensten zu strukturieren, zu beschriften und zu verbessern.
* [Sandboxen](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

The following sections provide additional information that you will need to know in order to successfully connect to [!DNL MariaDB] using the [!DNL Flow Service] API.

### Erforderliche Anmeldedaten sammeln

Damit eine Verbindung [!DNL Flow Service] [!DNL MariaDB]mit hergestellt werden kann, müssen Sie die folgende Verbindungseigenschaft angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `connectionString` | Die mit Ihrer [!DNL MariaDB] Authentifizierung verknüpfte Verbindungszeichenfolge. Das Muster für die [!DNL MariaDB] Verbindungszeichenfolge lautet: `Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | Die ID, mit der eine Verbindung generiert wird. Die spezifizierte ID für feste Verbindungen [!DNL MariaDB] lautet `3000eb99-cd47-43f3-827c-43caf170f015`. |

Weitere Informationen zum Abrufen einer Verbindungszeichenfolge finden Sie in [diesem MariaDB-Dokument](https://mariadb.com/kb/en/about-mariadb-connector-odbc/).

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](../../../../../tutorials/authentication.md) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform], including those belonging to the [!DNL Flow Service], are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

* x-sandbox-name: `{SANDBOX_NAME}`

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

* Content-Type: `application/json`

## Verbindung erstellen

Eine Verbindung gibt eine Quelle an und enthält Ihre Anmeldeinformationen für diese Quelle. Pro [!DNL MariaDB] Konto ist nur eine Verbindung erforderlich, da sie zum Erstellen mehrerer Quell-Connectors verwendet werden kann, um verschiedene Daten einzubringen.

**API-Format**

```http
POST /connections
```

**Anfrage**

Um eine [!DNL MariaDB] Verbindung zu erstellen, muss ihre eindeutige Verbindungs-Spezifikations-ID als Teil der POST-Anfrage angegeben werden. Die Verbindungsspezifikations-ID für [!DNL MariaDB] ist `3000eb99-cd47-43f3-827c-43caf170f015`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Test connection for maria-db",
        "description": "Test connection for maria-db",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "3000eb99-cd47-43f3-827c-43caf170f015",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `auth.params.connectionString` | Die mit Ihrer [!DNL MariaDB] Authentifizierung verknüpfte Verbindungszeichenfolge. Das Muster für die [!DNL MariaDB] Verbindungszeichenfolge lautet: `Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | Die [!DNL MariaDB] Spezial-ID der Verbindung lautet: `3000eb99-cd47-43f3-827c-43caf170f015`. |

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Basisverbindung einschließlich ihrer eindeutigen Kennung (`id`) zurück. Diese ID ist erforderlich, um Ihre Datenbank im nächsten Schritt zu untersuchen.

```json
{
    "id": "be3a2d71-1fb6-4fea-ba2d-711fb61fea50",
    "etag": "\"02002624-0000-0200-0000-5e41f7040000\""
}
```

## Nächste Schritte

In diesem Lernprogramm haben Sie eine [!DNL MariaDB] Verbindung mit der [!DNL Flow Service] API erstellt und den eindeutigen ID-Wert der Verbindung erhalten. Sie können diese Verbindungs-ID im nächsten Lernprogramm verwenden, um zu erfahren, wie Sie Datenbanken oder NoSQL-Systeme mit der Flow Service API [erkunden können](../../explore/database-nosql.md).
