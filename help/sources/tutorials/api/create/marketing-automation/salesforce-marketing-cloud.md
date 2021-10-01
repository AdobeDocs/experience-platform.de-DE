---
keywords: Experience Platform; Homepage; beliebte Themen; Salesforce Marketing Cloud; Salesforce-Marketing Cloud
solution: Experience Platform
title: Erstellen einer Salesforce-Marketing Cloud-Basisverbindung mithilfe der Flow Service-API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Flow Service-API Adobe Experience Platform mit Salesforce Marketing Cloud verbinden.
exl-id: fbf68d3a-f8b1-4618-bd56-160cc6e3346d
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 11%

---

# Erstellen einer [!DNL Salesforce Marketing Cloud]-Basisverbindung mithilfe der [!DNL Flow Service]-API

>[!NOTE]
>
>Die Quelle [!DNL Salesforce Marketing Cloud] befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta-beschrifteten Quellen finden Sie unter [Quellenübersicht](../../../../home.md#terms-and-conditions) .

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL Salesforce Marketing Cloud] mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von  [!DNL Platform] Diensten zu strukturieren, zu beschriften und zu erweitern.
* [Sandboxes](../../../../../sandboxes/home.md)[!DNL Platform]: Experience bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Anwendungen für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Verwenden von Platform-APIs

Informationen dazu, wie Sie erfolgreich Aufrufe an Platform-APIs durchführen können, finden Sie im Handbuch [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

Im folgenden Abschnitt finden Sie weitere Informationen, die Sie benötigen, um mithilfe der [!DNL Flow Service]-API eine erfolgreiche Verbindung zu [!DNL Salesforce Marketing Cloud] herstellen zu können.

### Erforderliche Anmeldedaten sammeln

Damit [!DNL Flow Service] eine Verbindung mit [!DNL Salesforce Marketing Cloud] herstellen kann, müssen Sie die folgenden Verbindungseigenschaften angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `host` | Der Host-Server Ihrer Anwendung. Dies ist häufig Ihre Subdomäne. |
| `clientId` | Die Client-ID, die Ihrer [!DNL Salesforce Marketing Cloud]-Anwendung zugeordnet ist. |
| `clientSecret` | Das Client-Geheimnis, das Ihrer [!DNL Salesforce Marketing Cloud]-Anwendung zugeordnet ist. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL Salesforce Marketing Cloud] lautet: `cea1c2a08-b722-11eb-8529-0242ac130003`. |

Weitere Informationen zu den ersten Schritten finden Sie in diesem [[!DNL Salesforce Marketing Cloud] Dokument](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm).

## Basisverbindung erstellen

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basis-Verbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den Endpunkt `/connections` und geben Sie dabei Ihre [!DNL Salesforce Marketing Cloud]-Authentifizierungsdaten als Teil des Anfragetexts an.

**API-Format**

```https
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Salesforce Marketing Cloud]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Salesforce Marketing Cloud base connection",
        "description": "Salesforce Marketing Cloud base connection",
        "auth": {
            "specName": "Client-Id-Secret Based Authentication",
            "params": {
                "host": "{HOST}"
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}"
            }
        },
        "connectionSpec": {
            "id": "cea1c2a08-b722-11eb-8529-0242ac130003",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `auth.params.clientId` | Die Client-ID, die Ihrer [!DNL Salesforce Marketing Cloud]-Anwendung zugeordnet ist. |
| `auth.params.clientSecret` | Das Client-Geheimnis, das Ihrer [!DNL Salesforce Marketing Cloud]-Anwendung zugeordnet ist. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID [!DNL Salesforce Marketing Cloud]: `cea1c2a08-b722-11eb-8529-0242ac130003`. |

**Antwort**

Eine erfolgreiche Antwort gibt die neu erstellte Verbindung zurück, einschließlich der eindeutigen Verbindungskennung (`id`). Diese ID ist erforderlich, um Ihre Daten im nächsten Tutorial zu untersuchen.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

In diesem Tutorial haben Sie eine [!DNL Salesforce Marketing Cloud]-Verbindung mit der [!DNL Flow Service]-API erstellt und den eindeutigen ID-Wert der Verbindung erhalten. Sie können diese Verbindungs-ID im nächsten Tutorial verwenden, wenn Sie erfahren, wie Sie [Marketing-Automatisierungssysteme mithilfe der Flow Service-API](../../explore/marketing-automation.md) untersuchen.
