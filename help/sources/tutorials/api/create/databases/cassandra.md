---
keywords: Experience Platform;Startseite;beliebte Themen;Apache Cassandra;Apache Cassandra;Cassandra;cassandra
solution: Experience Platform
title: Erstellen einer Apache Cassandra Source-Verbindung mithilfe der Flow Service-API
type: Tutorial
description: Erfahren Sie, wie Sie Apache Cassandra mithilfe der Flow Service-API mit Adobe Experience Platform verbinden.
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 47%

---


# Erstellen einer [!DNL Apache Cassandra]-Quellverbindung mithilfe der [!DNL Flow Service]-API

[!DNL Flow Service] wird verwendet, um Kundendaten aus verschiedenen Quellen innerhalb von Adobe Experience Platform zu sammeln und zu zentralisieren. Der Dienst stellt eine Benutzeroberfläche und eine RESTful-API bereit, über die alle unterstützten Quellen verbunden werden können.

In diesem Tutorial wird die [!DNL Flow Service]-API verwendet, um Sie durch die Schritte zum Verbinden von [!DNL Apache Cassandra] (im Folgenden als „Kassandra“ bezeichnet) mit [!DNL Experience Platform] zu führen.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Experience Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Experience Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um sich mithilfe der [!DNL Flow Service]-API erfolgreich mit Cassandra verbinden zu können.

### Sammeln erforderlicher Anmeldedaten

Damit [!DNL Flow Service] eine Verbindung mit [!DNL Cassandra] herstellen kann, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| `host` | Die IP-Adresse oder der Hostname des [!DNL Cassandra]. |
| `port` | Der TCP-Port, den der [!DNL Cassandra]-Server verwendet, um auf Client-Verbindungen zu warten. Der Standard-Port ist `9042`. |
| `username` | Der Benutzername, mit dem eine Verbindung zum [!DNL Cassandra]-Server zwecks Authentifizierung hergestellt wird. |
| `password` | Das Kennwort, mit dem eine Verbindung zum [!DNL Cassandra]-Server zwecks Authentifizierung hergestellt wird. |
| `connectionSpec.id` | Die zum Erstellen einer Verbindung erforderliche eindeutige Kennung. Die Verbindungsspezifikations-ID für [!DNL Cassandra] ist `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

Weitere Informationen zu den ersten Schritten finden Sie in [diesem Cassandra-Dokument](https://cassandra.apache.org/doc/latest/operating/security.html#authentication).

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Experience Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Alle Ressourcen in [!DNL Experience Platform], einschließlich der Ressourcen, die zum [!DNL Flow Service] gehören, sind in bestimmten virtuellen Sandboxes isoliert. Bei allen Anfragen an [!DNL Experience Platform]-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

* x-sandbox-name: `{SANDBOX_NAME}`

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

* Content-Type: `application/json`

## Verbindung erstellen

Eine Verbindung gibt eine Quelle an und enthält Ihre Anmeldeinformationen für diese Quelle. Pro [!DNL Cassandra]-Konto ist nur ein Connector erforderlich, da er zum Erstellen mehrerer Quell-Connectoren verwendet werden kann, um verschiedene Daten einzubringen.

**API-Format**

```http
POST /connections
```

**Anfrage**

Um eine [!DNL Cassandra] Verbindung zu erstellen, muss deren eindeutige Verbindungsspezifikations-ID als Teil der POST-Anfrage angegeben werden. Die Verbindungsspezifikations-ID für [!DNL Cassandra] ist `a8f4d393-1a6b-43f3-931f-91a16ed857f4`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Cassandra test connection",
        "description": "A test connection for Cassandra",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "host": "{HOST},
                    "port": "{PORT}",
                    "username": "{USERNAME}",
                    "password": "{PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "a8f4d393-1a6b-43f3-931f-91a16ed857f4",
            "version": "1.0"
        }
    }'
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `auth.params.host` | Die IP-Adresse oder der Hostname des [!DNL Cassandra]. |
| `auth.params.port` | Der TCP-Port, den der [!DNL Cassandra]-Server verwendet, um auf Client-Verbindungen zu warten. Der Standard-Port ist `9042`. |
| `auth.params.username` | Der Benutzername, mit dem eine Verbindung zum [!DNL Cassandra]-Server zwecks Authentifizierung hergestellt wird. |
| `auth.params.password` | Das Kennwort, mit dem eine Verbindung zum [!DNL Cassandra]-Server zwecks Authentifizierung hergestellt wird. |
| `connectionSpec.id` | Die [!DNL Cassandra]-Verbindungsspezifikations-ID: `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

**Antwort**

Eine erfolgreiche Antwort gibt Details der neu erstellten Verbindung zurück, einschließlich ihrer eindeutigen Kennung (`id`). Diese ID ist erforderlich, um Ihre Daten im nächsten Tutorial zu untersuchen.

```json
{
    "id": "ce69aa89-1baa-4054-a9aa-891baa605425",
    "etag": "\"5a026e19-0000-0200-0000-5eac76d00000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL Cassandra] mithilfe der [!DNL Flow Service]-API erstellt und den eindeutigen ID-Wert der Verbindung erhalten. Sie können diese ID im nächsten Tutorial verwenden, in dem Sie das Erkunden [ Datenbanken mithilfe der Flow Service-API ](../../explore/database-nosql.md).
