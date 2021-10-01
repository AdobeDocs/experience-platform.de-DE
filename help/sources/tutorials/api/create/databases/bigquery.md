---
keywords: Experience Platform; home; beliebte Themen; bigquery; Google; Google; Google BigQuery
solution: Experience Platform
title: Erstellen einer Google BigQuery-Basisverbindung mit der Flow Service-API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie Adobe Experience Platform mithilfe der Flow Service-API mit Google BigQuery verbinden.
exl-id: 51f90366-7a0e-49f1-bd57-b540fa1d15af
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 10%

---

# Erstellen einer [!DNL Google BigQuery]-Basisverbindung mithilfe der [!DNL Flow Service]-API

>[!NOTE]
>
>Der Connector [!DNL Google BigQuery] befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectoren finden Sie unter [Quellen - Übersicht](../../../../home.md#terms-and-conditions) .

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL Google BigQuery] (nachfolgend &quot;a1/>&quot;genannt) mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).[!DNL BigQuery]

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md):  [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von  [!DNL Platform] Diensten zu strukturieren, zu beschriften und zu erweitern.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der [!DNL Flow Service]-API erfolgreich eine Verbindung zu [!DNL BigQuery] herstellen zu können.

### Erforderliche Anmeldedaten sammeln

Damit [!DNL Flow Service] [!DNL BigQuery] eine Verbindung zu Platform herstellen kann, müssen Sie die folgenden OAuth 2.0-Authentifizierungswerte angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `project` | Die Projekt-ID des standardmäßigen [!DNL BigQuery]-Projekts, mit dem abgefragt werden soll. |
| `clientID` | Der ID-Wert, der zum Generieren des Aktualisierungstokens verwendet wird. |
| `clientSecret` | Der geheime Wert, der zum Generieren des Aktualisierungstokens verwendet wird. |
| `refreshToken` | Das Aktualisierungstoken, das von [!DNL Google] abgerufen wurde und zum Autorisieren des Zugriffs auf [!DNL BigQuery] verwendet wird. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL BigQuery] lautet: `3c9b37f8-13a6-43d8-bad3-b863b941fedd`. |

Weitere Informationen zu diesen Werten finden Sie in diesem [[!DNL BigQuery] Dokument](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing).

### Verwenden von Platform-APIs

Informationen dazu, wie Sie erfolgreich Aufrufe an Platform-APIs durchführen können, finden Sie im Handbuch [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Basisverbindung erstellen

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basis-Verbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den Endpunkt `/connections` und geben Sie dabei Ihre [!DNL BigQuery]-Authentifizierungsdaten als Teil der Anfrageparameter an.

**API-Format**

```https
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL BigQuery]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google BigQuery connection",
        "description": "Google BigQuery connection",
        "auth": {
            "specName": "Basic Authentication",
            "type": "OAuth2.0",
            "params": {
                    "project": "{PROJECT}",
                    "clientId": "{CLIENT_ID},
                    "clientSecret": "{CLIENT_SECRET}",
                    "refreshToken": "{REFRESH_TOKEN}"
                }
        },
        "connectionSpec": {
            "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| --------- | ----------- |
| `auth.params.project` | Die Projekt-ID des standardmäßigen [!DNL BigQuery]-Projekts, das abgefragt werden soll. gegen. |
| `auth.params.clientId` | Der ID-Wert, der zum Generieren des Aktualisierungstokens verwendet wird. |
| `auth.params.clientSecret` | Der Client-Wert, der zum Generieren des Aktualisierungstokens verwendet wird. |
| `auth.params.refreshToken` | Das Aktualisierungstoken, das von [!DNL Google] abgerufen wurde und zum Autorisieren des Zugriffs auf [!DNL BigQuery] verwendet wird. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID [!DNL Google BigQuery]: `3c9b37f8-13a6-43d8-bad3-b863b941fedd`. |

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Verbindung zurück, einschließlich der eindeutigen Kennung (`id`). Diese ID ist erforderlich, um Ihre Daten im nächsten Tutorial zu untersuchen.

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL BigQuery]-Verbindung mit der [!DNL Flow Service]-API erstellt und den eindeutigen ID-Wert der Verbindung erhalten. Sie können diese Verbindungs-ID im nächsten Tutorial verwenden, wenn Sie erfahren, wie Sie mit der Flow Service-API](../../explore/database-nosql.md)Datenbanken oder NoSQL-Systeme analysieren können.[
