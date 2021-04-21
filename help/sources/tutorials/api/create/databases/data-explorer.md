---
keywords: Experience Platform;Home;beliebte Themen;Azurblauer Data Explorer;Datenforscher;Data Explorer
solution: Experience Platform
title: Erstellen einer Azurblauer Data Explorer-Quellverbindung mit der Flow-Dienst-API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie mit der Flow-Dienst-API den Azurblauen Data Explorer mit Adobe Experience Platform verbinden.
exl-id: 1b17bbb0-1f7b-4d89-a158-ad269e6edf30
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 23%

---

# Erstellen einer [!DNL Azure Data Explorer]-Quellverbindung mit der [!DNL Flow Service]-API

>[!NOTE]
>
>Der [!DNL Azure Data Explorer]-Anschluss befindet sich in der Betaversion. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie unter [Sources overview](../../../../home.md#terms-and-conditions).

[!DNL Flow Service] wird zur Erfassung und Zentralisierung von Kundendaten aus unterschiedlichen Quellen innerhalb von Adobe Experience Platform verwendet. Der Dienst stellt eine Benutzeroberfläche und eine RESTful-API bereit, über die alle unterstützten Quellen verbunden werden können.

In diesem Lernprogramm wird die API [!DNL Flow Service] verwendet, um Sie durch die Schritte zur Verbindung von [!DNL Azure Data Explorer] (im Folgenden &quot;Data Explorer&quot; genannt) mit [!DNL Experience Platform] zu führen.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md):  [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von  [!DNL Platform] Diensten zu strukturieren, zu beschriften und zu verbessern.
* [Sandboxen](../../../../../sandboxes/home.md):  [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne  [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie kennen müssen, um eine Verbindung mit [!DNL Data Explorer] mithilfe der [!DNL Flow Service]-API herstellen zu können.

### Erforderliche Anmeldedaten sammeln

Damit [!DNL Flow Service] eine Verbindung mit [!DNL Data Explorer] herstellen kann, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `endpoint` | Der Endpunkt des [!DNL Data Explorer]-Servers. |
| `database` | Der Name der [!DNL Data Explorer]-Datenbank. |
| `tenant` | Die eindeutige Mandanten-ID, mit der eine Verbindung zur [!DNL Data Explorer]-Datenbank hergestellt wird. |
| `servicePrincipalId` | Die Prinzipal-ID des Unique Service, mit der eine Verbindung zur [!DNL Data Explorer]-Datenbank hergestellt wird. |
| `servicePrincipalKey` | Der Hauptschlüssel für den eindeutigen Dienst, mit dem eine Verbindung zur [!DNL Data Explorer]-Datenbank hergestellt wird. |
| `connectionSpec.id` | Die eindeutige Kennung, die zum Erstellen einer Verbindung erforderlich ist. Die Verbindungs-Spezifikations-ID für [!DNL Data Explorer] ist `0479cc14-7651-4354-b233-7480606c2ac3`. |

Weitere Informationen zum Einstieg finden Sie in [diesem Data Explorer Dokument](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad).

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

Eine Verbindung gibt eine Quelle an und enthält Ihre Anmeldeinformationen für diese Quelle. Pro [!DNL Data Explorer]-Konto ist nur ein Connector erforderlich, da er zum Erstellen mehrerer Quellschnittstellen verwendet werden kann, um verschiedene Daten einzubringen.

**API-Format**

```http
POST /connections
```

**Anfrage**

Um eine [!DNL Data Explorer]-POST zu erstellen, muss die eindeutige Verbindungs-ID als Teil der Verbindungsanforderung angegeben werden. Die Verbindungs-Spezifikations-ID für [!DNL Data Explorer] ist `0479cc14-7651-4354-b233-7480606c2ac3`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Data Explorer connection",
        "description": "A connection for Azure Data Explorer",
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
| `auth.params.endpoint` | Der Endpunkt des [!DNL Data Explorer]-Servers. |
| `auth.params.database` | Der Name der [!DNL Data Explorer]-Datenbank. |
| `auth.params.tenant` | Die eindeutige Mandanten-ID, mit der eine Verbindung zur [!DNL Data Explorer]-Datenbank hergestellt wird. |
| `auth.params.servicePrincipalId` | Die Prinzipal-ID des Unique Service, mit der eine Verbindung zur [!DNL Data Explorer]-Datenbank hergestellt wird. |
| `auth.params.servicePrincipalKey` | Der Hauptschlüssel für den eindeutigen Dienst, mit dem eine Verbindung zur [!DNL Data Explorer]-Datenbank hergestellt wird. |
| `connectionSpec.id` | Die [!DNL Data Explorer]-Verbindungs-Spec-ID: `0479cc14-7651-4354-b233-7480606c2ac3`. |

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Verbindung zurück, einschließlich der eindeutigen Kennung (`id`). Diese ID ist erforderlich, um Ihre Daten im nächsten Lernprogramm zu untersuchen.

```json
{
    "id": "f088e4f2-2464-480c-88e4-f22464b80c90",
    "etag": "\"43011faa-0000-0200-0000-5ea740cd0000\""
}
```

## Nächste Schritte

In diesem Lernprogramm haben Sie eine [!DNL Data Explorer]-Verbindung mit der [!DNL Flow Service]-API erstellt und den eindeutigen ID-Wert der Verbindung erhalten. Sie können diese ID im nächsten Lernprogramm verwenden, um zu erfahren, wie Sie Datenbanken mithilfe der Flow Service API](../../explore/database-nosql.md) untersuchen.[
