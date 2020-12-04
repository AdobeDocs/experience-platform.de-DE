---
keywords: Experience Platform;home;popular topics;PostgreSQL;postgresql;PSQL;psql
solution: Experience Platform
title: Erstellen eines PostgreSQL-Connectors mit der Flow Service API
topic: overview
type: Tutorial
description: Dieses Lernprogramm verwendet die Flow Service API, um Sie durch die Schritte zu führen, die zur Verbindung der Experience Platform mit PostgreSQL (im Folgenden "PSQL" genannt) durchgeführt werden.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 26%

---


# Erstellen eines [!DNL PostgreSQL] Connectors mit der [!DNL Flow Service] API

>[!NOTE]
>
>Der [!DNL PostgreSQL] Anschluss befindet sich in der Betaphase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie in der Übersicht [zu den](../../../../home.md#terms-and-conditions) Quellen.

[!DNL Flow Service] wird zur Erfassung und Zentralisierung von Kundendaten aus unterschiedlichen Quellen innerhalb von Adobe Experience Platform verwendet. Der Dienst stellt eine Benutzeroberfläche und eine RESTful-API bereit, über die alle unterstützten Quellen verbunden werden können.

Dieses Lernprogramm verwendet die [!DNL Flow Service] API, um Sie durch die Schritte zur Verbindung [!DNL Experience Platform] mit [!DNL PostgreSQL] (nachfolgend &quot;PSQL&quot; genannt) zu führen.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von [!DNL Platform] Diensten zu strukturieren, zu beschriften und zu verbessern.
* [Sandboxen](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

The following sections provide additional information that you will need to know in order to successfully connect to PSQL using the [!DNL Flow Service] API.

### Erforderliche Anmeldedaten sammeln

Damit eine Verbindung mit PSQL hergestellt [!DNL Flow Service] werden kann, müssen Sie die folgende Verbindungseigenschaft angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `connectionString` | Die mit Ihrem PSQL-Konto verknüpfte Verbindungszeichenfolge. Das Muster der PSQL-Verbindungszeichenfolge lautet: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | Die ID, mit der eine Verbindung generiert wird. Die spezifizierte ID für feste Verbindungen für PSQL lautet `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

Weitere Informationen zum Abrufen einer Verbindungszeichenfolge finden Sie in [diesem PSQL-Dokument](https://www.postgresql.org/docs/9.2/app-psql.html).

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

Eine Verbindung gibt eine Quelle an und enthält Ihre Anmeldeinformationen für diese Quelle. Pro PSQL-Konto ist nur eine Verbindung erforderlich, da sie zum Erstellen mehrerer Quell-Connectors verwendet werden kann, um verschiedene Daten einzubringen.

**API-Format**

```http
POST /connections
```

**Anfrage**

Um eine PSQL-Verbindung zu erstellen, muss die eindeutige Verbindungsspezifikations-ID als Teil der POST-Anfrage angegeben werden. Die Verbindungsspezifikations-ID für PSQL ist `74a1c565-4e59-48d7-9d67-7c03b8a13137`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Test connection for PostgreSQL",
        "description": "Test connection for PostgreSQL",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "74a1c565-4e59-48d7-9d67-7c03b8a13137",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| ------------- | --------------- |
| `auth.params.connectionString` | Die mit Ihrem PSQL-Konto verknüpfte Verbindungszeichenfolge. Das Muster der PSQL-Verbindungszeichenfolge lautet: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID für PSQL lautet: `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung (`id`) der neu erstellten Basisverbindung zurück. Diese ID ist erforderlich, um Ihre PSQL-Datenbank im nächsten Lernprogramm zu untersuchen.

```json
{
    "id": "056dd1b4-da33-42f9-add1-b4da3392f94e",
    "etag": "\"1700e582-0000-0200-0000-5e3c85180000\""
}
```

## Nächste Schritte

In diesem Lernprogramm haben Sie eine PSQL-Verbindung mit der [!DNL Flow Service] API erstellt und den eindeutigen ID-Wert der Verbindung erhalten. Sie können diese Verbindungs-ID im nächsten Lernprogramm verwenden, um zu erfahren, wie Sie Datenbanken oder NoSQL-Systeme mit der Flow Service API [erkunden können](../../explore/database-nosql.md).
