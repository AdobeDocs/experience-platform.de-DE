---
keywords: Experience Platform; Startseite; beliebte Themen; Vertica; Vertika
solution: Experience Platform
title: Erstellen einer HP Vertica Source Connection mithilfe der Flow Service-API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie mit der Flow Service-API eine Verbindung zwischen HP Vertica und Adobe Experience Platform herstellen.
exl-id: 37f831c1-7c82-462a-8338-a0bcaaf08cd1
source-git-commit: c3d66e50f647c2203fcdd5ad36ad86ed223733e3
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 32%

---

# Erstellen Sie eine HP [!DNL Vertica]-Quellverbindung mithilfe der [!DNL Flow Service]-API.

>[!NOTE]
>
>Der HP [!DNL Vertica]-Connector befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectoren finden Sie unter [Quellen - Übersicht](../../../../home.md#terms-and-conditions) .

[!DNL Flow Service] wird verwendet, um Kundendaten aus verschiedenen Quellen innerhalb von Adobe Experience Platform zu sammeln und zu zentralisieren. Der Dienst bietet eine Benutzeroberfläche und eine RESTful-API, über die alle unterstützten Quellen verbunden werden können.

In diesem Tutorial wird die [!DNL Flow Service]-API verwendet, um Sie durch die Schritte zum Verbinden von HP [!DNL Vertica] mit [!DNL Experience Platform] zu führen.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](https://experienceleague.adobe.com/docs/experience-platform/source-connectors/home.html):  [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von  [!DNL Platform] Diensten zu strukturieren, zuzuordnen und zu erweitern.
* [Sandboxes](https://experienceleague.adobe.com/docs/experience-platform/sandbox/home.html): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mit der [!DNL Flow Service]-API erfolgreich eine Verbindung zu HP [!DNL Vertica] herstellen zu können.

### Erforderliche Anmeldedaten sammeln

Damit [!DNL Flow Service] eine Verbindung mit HP [!DNL Vertica] herstellen kann, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `connectionString` | Die Verbindungszeichenfolge, die für die Verbindung mit Ihrer HP [!DNL Vertica]-Instanz verwendet wird. Das Verbindungszeichenfolgenmuster für HP [!DNL Vertica] ist `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` |
| `connectionSpec.id` | Die zum Erstellen einer Verbindung erforderliche Kennung. Die feste Verbindungsspezifikations-ID für HP [!DNL Vertica] lautet: `a8b6a1a4-5735-42b4-952c-85dce0ac38b5` |

Weitere Informationen zum Erwerb einer Verbindungszeichenfolge finden Sie in [diesem HP Vertica-Dokument](https://www.vertica.com/docs/9.2.x/HTML/Content/Authoring/ConnectingToVertica/ClientJDBC/CreatingAndConfiguringAConnection.htm).

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de#platform-apis) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alle Ressourcen in [!DNL Experience Platform], einschließlich der Ressourcen, die zu [!DNL Flow Service] gehören, werden auf bestimmte virtuelle Sandboxes beschränkt. Bei allen Anfragen an [!DNL Platform]-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

* `x-sandbox-name: {SANDBOX_NAME}`

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

* `Content-Type: application/json`

## Verbindung erstellen

Eine Verbindung gibt eine Quelle an und enthält Ihre Anmeldeinformationen für diese Quelle. Pro HP [!DNL Vertica]-Konto ist nur eine Verbindung erforderlich, da sie zur Erstellung mehrerer Quell-Connectoren verwendet werden kann, um verschiedene Daten einzubringen.

**API-Format**

```http
POST /connections
```

**Anfrage**

Um eine HP [!DNL Vertica]-Verbindung zu erstellen, muss die eindeutige Verbindungsspezifikations-ID im Rahmen der POST-Anfrage angegeben werden. Die Verbindungsspezifikations-ID für HP [!DNL Vertica] lautet `a8b6a1a4-5735-42b4-952c-85dce0ac38b5`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Connection for HP Vertica",
        "description": "Connection for HP Vertica",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "a8b6a1a4-5735-42b4-952c-85dce0ac38b5",
            "version": "1.0"
        }
    }'
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `auth.params.connectionString` | Die Verbindungszeichenfolge, die Ihrem HP [!DNL Vertica]-Konto zugeordnet ist. Das Verbindungszeichenfolgenmuster für HP [!DNL Vertica] lautet: `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | Die HP [!DNL Vertica]-Verbindungsspezifikations-ID: `a8b6a1a4-5735-42b4-952c-85dce0ac38b5`. |

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Verbindung zurück, einschließlich der eindeutigen Kennung (`id`). Diese ID ist erforderlich, um Ihre Daten im nächsten Tutorial zu untersuchen.

```json
{
    "id": "6bc13a3b-3546-455f-813a-3b3546a55fb1",
    "etag": "\"3500866c-0000-0200-0000-5e83afa30000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine HP [!DNL Vertica]-Verbindung mit der [!DNL Flow Service]-API erstellt und den eindeutigen ID-Wert der Verbindung erhalten. Sie können diese ID im nächsten Tutorial verwenden, während Sie lernen, wie Sie [Datenbanken mithilfe der Flow Service-API](../../explore/database-nosql.md) analysieren können.
