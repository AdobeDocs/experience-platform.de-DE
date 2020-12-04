---
keywords: Experience Platform;home;popular topics;Phoenix;phoenix
solution: Experience Platform
title: Erstellen eines Phoenix-Connectors mit der Flow Service API
topic: overview
type: Tutorial
description: In diesem Lernprogramm wird die Flow Service API verwendet, um Sie durch die Schritte zu führen, mit denen Sie eine Phoenix-Datenbank mit der Experience Platform verbinden.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 24%

---


# Erstellen eines [!DNL Phoenix] Connectors mit der [!DNL Flow Service] API

>[!NOTE]
>
>Der [!DNL Phoenix] Anschluss befindet sich in der Betaphase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie in der Übersicht [zu den](../../../../home.md#terms-and-conditions) Quellen.

[!DNL Flow Service] wird zur Erfassung und Zentralisierung von Kundendaten aus unterschiedlichen Quellen innerhalb von Adobe Experience Platform verwendet. Der Dienst stellt eine Benutzeroberfläche und eine RESTful-API bereit, über die alle unterstützten Quellen verbunden werden können.

Dieses Lernprogramm verwendet die [!DNL Flow Service] API, um Sie durch die Schritte zu führen, mit denen Sie eine [!DNL Phoenix] Datenbank mit einer [!DNL Experience Platform]verbinden.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von [!DNL Platform] Diensten zu strukturieren, zu beschriften und zu verbessern.
* [Sandboxen](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

The following sections provide additional information that you will need to know in order to successfully connect to [!DNL Phoenix] using the [!DNL Flow Service] API.

### Erforderliche Anmeldedaten sammeln

Damit eine Verbindung [!DNL Flow Service] zu [!DNL Phoenix]hergestellt werden kann, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `host` | Die IP-Adresse oder der Hostname des [!DNL Phoenix] Servers. |
| `username` | Der Benutzername, mit dem Sie auf [!DNL Phoenix] Server zugreifen. |
| `password` | Das dem Benutzer entsprechende Kennwort. |
| `port` | Der TCP-Anschluss, den der [!DNL Phoenix] Server verwendet, um auf Clientverbindungen zu warten. Wenn Sie eine Verbindung zu [!DNL Azure] HDInsights herstellen, geben Sie den Anschluss als 443 an. |
| `httpPath` | Die Teil-URL, die dem [!DNL Phoenix] Server entspricht. Geben Sie /hbasephoenix0 an, wenn Sie einen [!DNL Azure] HDInsights-Cluster verwenden. |
| `enableSsl` | Ein boolescher Wert. Gibt an, ob die Verbindungen zum Server mit SSL verschlüsselt werden. |
| `connectionSpec.id` | Die eindeutige Kennung, die zum Erstellen einer Verbindung erforderlich ist. Die Verbindungs-Spezifikations-ID für [!DNL Phoenix] lautet: `102706fb-a5cd-42ee-afe0-bc42f017ff43` |

Weitere Informationen zum Einstieg finden Sie in [diesem Phoenix-Dokument](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

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

Eine Verbindung gibt eine Quelle an und enthält Ihre Anmeldeinformationen für diese Quelle. Pro [!DNL Phoenix] Konto ist nur eine Verbindung erforderlich, da sie zum Erstellen mehrerer Quell-Connectors verwendet werden kann, um verschiedene Daten einzubringen.

**API-Format**

```http
POST /connections
```

**Anfrage**

Zur Erstellung einer [!DNL Phoenix] Verbindung muss die eindeutige Verbindungs-ID als Teil der POST angegeben werden. Die Verbindungs-ID für [!DNL Phoenix] lautet `102706fb-a5cd-42ee-afe0-bc42f017ff43`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Phoenix test connection",
        "description": "Phoenix test connection",
        "auth": {
            "specName": "Basic Authentication",
        "params": {
            "host" :  "{HOST}",
            "username" : "{USERNAME}",
            "password" :"{PASSWORD}",
            "port" : {PORT},
            "httpPath" : "{PATH}",
            "enableSsl" : {SSL}
            }
        },
        "connectionSpec": {
            "id": "102706fb-a5cd-42ee-afe0-bc42f017ff43",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| --------- | ----------- |
| `auth.params.host` | The host of the [!DNL Phoenix] server. |
| `auth.params.username` | Der mit Ihrer [!DNL Phoenix] Verbindung verknüpfte Benutzername. |
| `auth.params.password` | Das mit Ihrer [!DNL Phoenix] Verbindung verknüpfte Kennwort. |
| `auth.params.port` | Der TCP-Anschluss für Ihre [!DNL Phoenix] Verbindung. |
| `auth.params.httpPath` | Der teilweise HTTP-Pfad für Ihre [!DNL Phoenix] Verbindung. |
| `auth.params.enableSsl` | Der boolesche Wert, der angibt, ob die Verbindungen zum Server mit SSL verschlüsselt werden. |
| `connectionSpec.id` | Die [!DNL Phoenix] Verbindungs-ID: `102706fb-a5cd-42ee-afe0-bc42f017ff43`. |

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Verbindung zurück, einschließlich der eindeutigen Kennung (`id`). Diese ID ist erforderlich, um Ihre Daten im nächsten Lernprogramm zu untersuchen.

```json
{
    "id": "0d982fff-c443-403e-982f-ffc443f03e37",
    "etag": "\"830082dc-0000-0200-0000-5e84ee560000\""
}
```

## Nächste Schritte

In diesem Lernprogramm haben Sie eine [!DNL Phoenix] Verbindung mit der [!DNL Flow Service] API erstellt und den eindeutigen ID-Wert der Verbindung erhalten. Sie können diese ID im nächsten Lernprogramm verwenden, um zu erfahren, wie Sie Datenbanken mithilfe der Flow Service API [untersuchen](../../explore/database-nosql.md).