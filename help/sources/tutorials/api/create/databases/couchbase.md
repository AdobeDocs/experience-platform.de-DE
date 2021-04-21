---
keywords: Experience Platform;Home;beliebte Themen;Couchbase;Couchbase
solution: Experience Platform
title: Erstellen einer Couchbase-Quellverbindung mit der Flow Service API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Flow Service API eine Verbindung zwischen Couchbase und Adobe Experience Platform herstellen.
exl-id: 625e3acf-fc27-44cf-b4e6-becf1d107ff2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 27%

---

# Erstellen einer [!DNL Couchbase]-Quellverbindung mit der [!DNL Flow Service]-API

>[!NOTE]
>
>Der [!DNL Couchbase]-Anschluss befindet sich in der Betaversion. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie unter [Sources overview](../../../../home.md#terms-and-conditions).

[!DNL Flow Service] wird zur Erfassung und Zentralisierung von Kundendaten aus verschiedenen Quellen verwendet, um sie in Adobe Experience Platform zu importieren. Der Dienst stellt eine Benutzeroberfläche und eine RESTful-API bereit, über die alle unterstützten Quellen verbunden werden können.

Erfahren Sie, wie [!DNL Couchbase] mit [!DNL Experience Platform] verbunden wird.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md):  [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von  [!DNL Platform] Diensten zu strukturieren, zu beschriften und zu verbessern.
* [Sandboxen](../../../../../sandboxes/home.md):  [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne  [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie kennen müssen, um eine Verbindung mit [!DNL Couchbase] mithilfe der [!DNL Flow Service]-API herstellen zu können.

### Erforderliche Anmeldedaten sammeln

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `connectionString` | Die Verbindungszeichenfolge, mit der eine Verbindung zu Ihrer [!DNL Couchbase]-Instanz hergestellt wird. Das Verbindungszeichenfolgen-Muster für [!DNL Couchbase] ist `Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];`. Weitere Informationen zum Abrufen einer Verbindungszeichenfolge finden Sie in [diesem Couchbase-Dokument](https://docs.Couchbase.com/c-sdk/2.10/client-settings.html#configuring-overview). |
| `connectionSpec.id` | Der zum Erstellen einer Verbindung erforderliche Bezeichner. Die feste Verbindungs-Spec-ID für [!DNL Couchbase] ist `1fe283f6-9bec-11ea-bb37-0242ac130002`. |

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Fehlerbehebungshandbuch für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://www.adobe.com/go/platform-api-authentication-en) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alle Ressourcen in [!DNL Experience Platform], einschließlich derjenigen, die zu [!DNL Flow Service] gehören, werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an [!DNL Platform]-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird in:

* `x-sandbox-name: {SANDBOX_NAME}`

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

* `Content-Type: application/json`

## Verbindung erstellen

Eine Verbindung gibt eine Quelle an und enthält Ihre Anmeldeinformationen für diese Quelle. Pro [!DNL Couchbase]-Konto ist nur ein Connector erforderlich, da er zum Erstellen mehrerer Quellschnittstellen verwendet werden kann, um verschiedene Daten einzubringen.

**API-Format**

```http
POST /connections
```

**Anfrage**

Die folgende Anforderung erstellt eine neue [!DNL Couchbase]-Verbindung, die von den in der Payload bereitgestellten Eigenschaften konfiguriert wird:.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Couchbase test connection",
        "description": "A test connection for a Couchbase source",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                    "connectionString": "Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];"
                }
        },
        "connectionSpec": {
            "id": "1fe283f6-9bec-11ea-bb37-0242ac130002",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| --------- | ----------- |
| `auth.params.connectionString` | Die Verbindungszeichenfolge, mit der eine Verbindung zu einem [!DNL Couchbase]-Konto hergestellt wird. Das Verbindungszeichenfolgen-Muster lautet: `Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];`. |
| `connectionSpec.id` | Die [!DNL Couchbase]-Verbindungs-Spec-ID: `1fe283f6-9bec-11ea-bb37-0242ac130002`. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details der neu erstellten Verbindung zurück, einschließlich der eindeutigen Kennung (`id`). Diese ID ist erforderlich, um Ihre Daten im nächsten Lernprogramm zu untersuchen.

```json
{
    "id": "54997109-07b5-40b7-9971-0907b5a0b75a",
    "etag": "\"280168f5-0000-0200-0000-5ed72b230000\""
}
```

## Nächste Schritte

In diesem Lernprogramm haben Sie eine [!DNL Couchbase]-Verbindung mit der [!DNL Flow Service]-API erstellt und den eindeutigen ID-Wert der Verbindung erhalten. Sie können diese ID im nächsten Lernprogramm verwenden, um zu erfahren, wie Sie Datenbanken mithilfe der Flow Service API](../../explore/database-nosql.md) untersuchen.[
