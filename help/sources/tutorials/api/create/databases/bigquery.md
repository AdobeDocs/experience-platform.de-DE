---
keywords: Experience Platform; Startseite; beliebte Themen; bigquery; Google; Google; Google BigQuery
solution: Experience Platform
title: Erstellen einer Google BigQuery-Basisverbindung mit der Flow Service-API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie mit der Flow Service-API Adobe Experience Platform mit Google BigQuery verbinden.
exl-id: 51f90366-7a0e-49f1-bd57-b540fa1d15af
source-git-commit: 0ca900b77275851076a13dcc4b8b4a9995ddd0be
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 49%

---

# Erstellen einer [!DNL Google BigQuery]-Basisverbindung mithilfe der [!DNL Flow Service]-API

>[!NOTE]
>
>Die [!DNL Google BigQuery] -Connector befindet sich in der Beta-Phase. Siehe [Quellen - Übersicht](../../../../home.md#terms-and-conditions) Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectoren.

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL Google BigQuery] (nachstehend &quot;genannt)[!DNL BigQuery]&quot;) mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um eine erfolgreiche Verbindung zu [!DNL BigQuery] mithilfe der [!DNL Flow Service] API.

### Sammeln erforderlicher Anmeldeinformationen

Zur [!DNL Flow Service] Verbindung herstellen [!DNL BigQuery] müssen Sie die folgenden OAuth 2.0-Authentifizierungswerte für Platform angeben:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| `project` | Die Projekt-ID der Standardeinstellung [!DNL BigQuery] -Projekt, für das abgefragt werden soll. |
| `clientID` | Der ID-Wert, der zum Generieren des Aktualisierungstokens verwendet wird. |
| `clientSecret` | Der geheime Wert, der zum Generieren des Aktualisierungstokens verwendet wird. |
| `refreshToken` | Das Aktualisierungstoken, das von [!DNL Google] verwendet, um den Zugriff auf [!DNL BigQuery]. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL BigQuery] ist: `3c9b37f8-13a6-43d8-bad3-b863b941fedd`. |

Weiterführende Informationen zu diesen Werten finden Sie in diesem Abschnitt [[!DNL BigQuery] Dokument](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing).

### Verwenden von Platform-APIs

Informationen zum Aufrufen von Platform-APIs finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Erstellen einer Basisverbindung

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basisverbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den Endpunkt `/connections` und geben Sie dabei Ihre [!DNL BigQuery]-Authentifizierungsdaten als Teil der Anfrageparameter an.

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
| `auth.params.project` | Die Projekt-ID der Standardeinstellung [!DNL BigQuery] -Projekt abfragen. gegen. |
| `auth.params.clientId` | Der ID-Wert, der zum Generieren des Aktualisierungstokens verwendet wird. |
| `auth.params.clientSecret` | Der Client-Wert, der zum Generieren des Aktualisierungstokens verwendet wird. |
| `auth.params.refreshToken` | Das Aktualisierungstoken, das von [!DNL Google] verwendet, um den Zugriff auf [!DNL BigQuery]. |
| `connectionSpec.id` | Die [!DNL Google BigQuery] Verbindungsspezifikations-ID: `3c9b37f8-13a6-43d8-bad3-b863b941fedd`. |

**Antwort**

Eine erfolgreiche Antwort gibt Details der neu erstellten Verbindung zurück, einschließlich ihrer eindeutigen Kennung (`id`). Diese ID ist erforderlich, um Ihre Daten im nächsten Tutorial zu untersuchen.

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL Google BigQuery] Basisverbindung mit [!DNL Flow Service] API. Sie können diese Basis-Verbindungs-ID in den folgenden Tutorials verwenden:

* [Struktur und Inhalt Ihrer Datentabellen mithilfe des [!DNL Flow Service] API](../../explore/tabular.md)
* [Erstellen Sie einen Datenfluss, um Datenbankdaten mit der [!DNL Flow Service] API](../../collect/database-nosql.md)
