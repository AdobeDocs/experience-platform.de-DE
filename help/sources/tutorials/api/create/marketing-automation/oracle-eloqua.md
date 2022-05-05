---
keywords: Experience Platform;home;popular topics;oracle;eloqua;oracle eloqua
solution: Experience Platform
title: Erstellen einer Oracle Eloqua-Basisverbindung mit der Flow Service-API
topic-legacy: overview
type: Tutorial
description: Learn how to connect Adobe Experience Platform to Oracle Eloqua using the Flow Service API.
exl-id: 866e408f-6e0b-4e81-9ad8-9d74c485c89a
source-git-commit: 1f2ae53e5503618b7ac12628923b30c457fd17e2
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 58%

---

# Erstellen Sie eine [!DNL Oracle Eloqua] Basisverbindung mit [!DNL Flow Service] API

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL Oracle Eloqua] mithilfe der [[!DNL Flow Service] -API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Platform voraus:

* [Quellen](../../../../home.md): Platform ermöglicht das Aufnehmen von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, eingehende Daten mithilfe von [!DNL Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md)[!DNL Platform]:  bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie für eine erfolgreiche Verbindung mit [!DNL Oracle Eloqua] unter Verwendung der [!DNL Flow Service]-API benötigen.

### Sammeln erforderlicher Anmeldeinformationen

Damit [!DNL Flow Service] eine Verbindung mit [!DNL Oracle Eloqua] herstellen kann, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Anmeldedaten | Beschreibung |
| --- | --- |
| `endpoint` | Der Endpunkt Ihrer [!DNL Oracle Eloqua]. |
| `username` | Der Benutzername Ihres [!DNL Oracle Eloqua] -Konto. Der Benutzername muss als `siteName + \\ + username`, wobei `siteName` ist der Unternehmensname, mit dem Sie sich bei [!DNL Oracle Eloqua] und `username` ist Ihr Benutzername. Der Benutzername für die Anmeldung kann beispielsweise wie folgt lauten: `adobe\\emily`. |
| `password` | Das Passwort, das Ihrem [!DNL Oracle Eloqua] Benutzername. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. The value for the connection specification ID of the [!DNL Oracle Eloqua] source is fixed as: `35d6c4d8-c9a9-11eb-b8bc-0242ac130003`. |

Weitere Informationen zu Authentifizierungsberechtigungen für [!DNL Oracle Eloqua], siehe [[!DNL Oracle Eloqua] Authentifizierungshandbuch](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html).

### Verwenden von Platform-APIs

Informationen zum Aufrufen von Platform-APIs finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Erstellen einer Basisverbindung

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basisverbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den Endpunkt `/connections` und geben Sie dabei Ihre [!DNL Oracle Eloqua]-Authentifizierungsdaten als Teil der Anfrageparameter an.

**API-Format**

```https
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Oracle Eloqua]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "name": "Oracle Eloqua Base Connection",
      "description": "Base Connection for Oracle Eloqua",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "endpoint": "{ENDPOINT}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "35d6c4d8-c9a9-11eb-b8bc-0242ac130003",
          "version": "1.0"
      }
  }'
```

| Parameter | Beschreibung |
| --- | --- |
| `name` | Der Name Ihrer [!DNL Oracle Eloqua]-Basisverbindung. Es wird empfohlen, einen beschreibenden Namen anzugeben, da Sie diesen Wert zum Nachschlagen Ihrer Basisverbindung verwenden können. |
| `description` | (Optional) Eine Eigenschaft, die Sie einbeziehen können, um zusätzliche Informationen zu Ihrer Basisverbindung bereitzustellen. |
| `auth.specName` | Der Authentifizierungstyp, der für die Verbindung verwendet wird. |
| `auth.params.endpoint` | The endpoint of your [!DNL Oracle Eloqua] server. |
| `auth.params.username` | Die verkettete Berechtigung, die den Site-Namen und Benutzernamen enthält, der Ihrer [!DNL Oracle Eloqua] -Konto. |
| `auth.params.password` | Das Passwort, das Ihrem [!DNL Oracle Eloqua]-Konto entspricht. |
| `connectionSpec.id` | Der Wert für die Verbindungsspezifikations-ID der [!DNL Oracle Eloqua] -Quelle wie folgt fest: `35d6c4d8-c9a9-11eb-b8bc-0242ac130003`. |

**Antwort**

Bei einer erfolgreichen Antwort werden Details zu der neu erstellten Basisverbindung zurückgegeben, einschließlich ihrer eindeutigen Kennung (`id`). Diese ID ist im nächsten Schritt erforderlich, um eine Quellverbindung zu erstellen.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Nächste Schritte

By following this tutorial, you have created an [!DNL Oracle Eloqua] base connection using the [!DNL Flow Service] API. Sie können diese Basis-Verbindungs-ID in den folgenden Tutorials verwenden:

* [Explore the structure and contents of your data tables using the [!DNL Flow Service] API](../../explore/tabular.md)
* [Erstellen Sie einen Datenfluss, um Daten zur Marketing-Automatisierung mit der [!DNL Flow Service] API](../../collect/marketing-automation.md)
