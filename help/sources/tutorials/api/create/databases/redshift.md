---
keywords: Experience Platform;home;popular topics;redshift;Redshift;Amazon Redshift;amazon redshift
solution: Experience Platform
title: Erstellen einer Amazon Redshift-Basisverbindung mit der Flow Service-API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie mit der Flow Service-API Adobe Experience Platform mit Amazon Redshift verbinden.
exl-id: 2728ce08-05c9-4dca-af1d-d2d1b266c5d9
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 11%

---

# Create an [!DNL Amazon Redshift] base connection using the [!DNL Flow Service] API

A base connection represents the authenticated connection between a source and Adobe Experience Platform.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL Amazon Redshift] mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Sources](../../../../home.md): [!DNL Experience Platform] allows data to be ingested from various sources while providing you with the ability to structure, label, and enhance incoming data using [!DNL Platform] services.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der [!DNL Flow Service]-API erfolgreich eine Verbindung zu [!DNL Amazon Redshift] herstellen zu können.

### Erforderliche Anmeldedaten sammeln

Damit [!DNL Flow Service] eine Verbindung mit [!DNL Amazon Redshift] herstellen kann, müssen Sie die folgenden Verbindungseigenschaften angeben:

| **Berechtigung** | **Beschreibung** |
| -------------- | --------------- |
| `server` | The server associated with your [!DNL Amazon Redshift] account. |
| `username` | Der Benutzername, der Ihrem [!DNL Amazon Redshift]-Konto zugeordnet ist. |
| `password` | Das Ihrem [!DNL Amazon Redshift]-Konto zugeordnete Kennwort. |
| `database` | Die [!DNL Amazon Redshift]-Datenbank, auf die Sie zugreifen. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL Amazon Redshift] ist `3416976c-a9ca-4bba-901a-1f08f66978ff`. |

For more information about getting started, refer to this [[!DNL Amazon Redshift] document](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

### Verwenden von Platform-APIs

Informationen dazu, wie Sie erfolgreich Aufrufe an Platform-APIs durchführen können, finden Sie im Handbuch [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Basisverbindung erstellen

A base connection retains information between your source and Platform, including your source&#39;s authentication credentials, the current state of the connection, and your unique base connection ID. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

To create a base connection ID, make a POST request to the `/connections` endpoint while providing your [!DNL Amazon Redshift] authentication credentials as part of the request parameters.

**API-Format**

```https
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Amazon Redshift]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "amazon-redshift base connection",
        "description": "base connection for amazon-redshift,
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "server": "{SERVER}",
                "database": "{DATABASE}",
                "password": "{PASSWORD}",
                "username": "{USERNAME}"
            }
        },
        "connectionSpec": {
            "id": "3416976c-a9ca-4bba-901a-1f08f66978ff",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| ------------- | --------------- |
| `auth.params.server` | Your [!DNL Amazon Redshift] server. |
| `auth.params.database` | The database associated with your [!DNL Amazon Redshift] account. |
| `auth.params.password` | The password associated with your [!DNL Amazon Redshift] account. |
| `auth.params.username` | Der Benutzername, der Ihrem [!DNL Amazon Redshift]-Konto zugeordnet ist. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID [!DNL Amazon Redshift]: `3416976c-a9ca-4bba-901a-1f08f66978ff` |

**Antwort**

Eine erfolgreiche Antwort gibt die neu erstellte Verbindung zurück, einschließlich der eindeutigen Kennung (`id`). This ID is required to explore your data in the next tutorial.

```json
{
    "id": "373e88fc-43da-4e3c-be88-fc43da3e3c0f",
    "etag": "\"1700ce7b-0000-0200-0000-5e3b405e0000\""
}
```

## Nächste Schritte

By following this tutorial, you have created a [!DNL Amazon Redshift] connection using the [!DNL Flow Service] API, and have obtained the connection&#39;s unique ID value. Sie können diese Verbindungs-ID im nächsten Tutorial verwenden, wenn Sie erfahren, wie Sie mit der Flow Service-API](../../explore/database-nosql.md)Datenbanken oder NoSQL-Systeme analysieren können.[
