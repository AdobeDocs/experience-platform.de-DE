---
title: Erstellen einer Amazon Redshift-Basisverbindung mit der Flow Service-API
description: Erfahren Sie, wie Sie mit der Flow Service-API Adobe Experience Platform mit Amazon Redshift verbinden.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 2728ce08-05c9-4dca-af1d-d2d1b266c5d9
source-git-commit: a7c2c5e4add5c80e0622d5aeb766cec950d79dbb
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 59%

---

# Erstellen einer [!DNL Amazon Redshift]-Basisverbindung mit der [!DNL Flow Service]-API

>[!IMPORTANT]
>
>Die Quelle &quot;[!DNL Amazon Redshift]&quot; steht Benutzern, die Real-time Customer Data Platform Ultimate erworben haben, im Quellkatalog zur Verfügung.

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL Amazon Redshift] mithilfe der [[!DNL Flow Service] -API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der [!DNL Flow Service] -API erfolgreich eine Verbindung zu [!DNL Amazon Redshift] herstellen zu können.

### Sammeln erforderlicher Anmeldeinformationen

Damit [!DNL Flow Service] eine Verbindung zu [!DNL Amazon Redshift] herstellen kann, müssen Sie die folgenden Verbindungseigenschaften angeben:

| **Credential** | **Beschreibung** |
| -------------- | --------------- |
| `server` | Der mit Ihrem [!DNL Amazon Redshift]-Konto verknüpfte Server. |
| `port` | Der TCP-Port, den ein [!DNL Amazon Redshift] -Server verwendet, um auf Clientverbindungen zu warten. |
| `username` | Der Benutzername, der Ihrem [!DNL Amazon Redshift] -Konto zugeordnet ist. |
| `password` | Das Ihrem [!DNL Amazon Redshift]-Konto zugeordnete Kennwort. |
| `database` | Die [!DNL Amazon Redshift]-Datenbank, auf die Sie zugreifen. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL Amazon Redshift] ist `3416976c-a9ca-4bba-901a-1f08f66978ff`. |

Weitere Informationen zu den ersten Schritten finden Sie in diesem [[!DNL Amazon Redshift] Dokument](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

### Verwenden von Platform-APIs

Informationen zum Aufrufen von Platform-APIs finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Erstellen einer Basisverbindung

>[!NOTE]
>
>Der Standard für die Kodierung von [!DNL Redshift] ist Unicode. Dies kann nicht geändert werden.

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basisverbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den Endpunkt `/connections` und geben Sie dabei Ihre [!DNL Amazon Redshift]-Authentifizierungsdaten als Teil der Anfrageparameter an.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "amazon-redshift base connection",
      "description": "base connection for amazon-redshift,
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "port": "{PORT},
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "database": "{DATABASE}"
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
| `auth.params.server` | Ihr [!DNL Amazon Redshift] -Server. |
| `auth.params.port` | Der TCP-Port, den der [!DNL Amazon Redshift] -Server verwendet, um auf Clientverbindungen zu warten. |
| `auth.params.database` | Die mit Ihrem [!DNL Amazon Redshift]-Konto verknüpfte Datenbank. |
| `auth.params.password` | Das Ihrem [!DNL Amazon Redshift]-Konto zugeordnete Kennwort. |
| `auth.params.username` | Der Benutzername, der Ihrem [!DNL Amazon Redshift] -Konto zugeordnet ist. |
| `connectionSpec.id` | Die [!DNL Amazon Redshift]-Verbindungsspezifikations-ID: `3416976c-a9ca-4bba-901a-1f08f66978ff` |

**Antwort**

Eine erfolgreiche Antwort gibt die neu erstellte Basisverbindung zurück, einschließlich ihrer eindeutigen Kennung (`id`). Diese ID ist erforderlich, um Ihre Daten im nächsten Tutorial zu untersuchen.

```json
{
    "id": "373e88fc-43da-4e3c-be88-fc43da3e3c0f",
    "etag": "\"1700ce7b-0000-0200-0000-5e3b405e0000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL Amazon Redshift]-Basisverbindung mithilfe der [!DNL Flow Service]-API erstellt. Sie können diese Basisverbindungs-ID in den folgenden Tutorials verwenden:

* [Erkunden von Struktur und Inhalten Ihrer Datentabellen mithilfe der  [!DNL Flow Service] -API](../../explore/tabular.md)
* [Erstellen Sie einen Datenfluss, um Datenbankdaten mithilfe der [!DNL Flow Service] API an Platform zu übertragen.](../../collect/database-nosql.md)
