---
keywords: Experience Platform; Startseite; beliebte Themen; oracle; eloqua; oracle eloqua
solution: Experience Platform
title: Erstellen einer Oracle Eloqua-Basisverbindung mit der Flow Service-API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie Adobe Experience Platform mithilfe der Flow Service-API mit Oracle Eloqua verbinden.
source-git-commit: 423f0efc3c0d9fb38cb8d1b16b885e1eddc23e72
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 5%

---

# Erstellen Sie eine [!DNL Oracle Eloqua] Basisverbindung mit [!DNL Flow Service] API

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL Oracle Eloqua] mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Platform voraus:

* [Quellen](../../../../home.md): Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten zu strukturieren, zu beschriften und zu erweitern, indem [!DNL Platform] Dienste.
* [Sandboxes](../../../../../sandboxes/home.md): Platform stellt virtuelle Sandboxes bereit, die eine einzelne [!DNL Platform] in separate virtuelle Umgebungen zu integrieren, um die Entwicklung und Weiterentwicklung von Programmen für digitale Erlebnisse zu unterstützen.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um eine erfolgreiche Verbindung zu [!DNL Oracle Eloqua] mithilfe der [!DNL Flow Service] API.

### Erforderliche Anmeldedaten sammeln

Zur [!DNL Flow Service] zur Verbindung mit [!DNL Oracle Eloqua]müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Berechtigung | Beschreibung |
| --- | --- |
| `endpoint` | Der Endpunkt Ihrer [!DNL Oracle Eloqua]. |
| `username` | Der Benutzername Ihres [!DNL Oracle Eloqua] -Konto. Der Benutzername muss als `siteName + \\ + username`, wobei `siteName` ist der Unternehmensname, mit dem Sie sich bei [!DNL Oracle Eloqua] und `username` ist Ihr Benutzername. Der Benutzername für die Anmeldung kann beispielsweise wie folgt lauten: `adobe\\emily`. |
| `password` | Das Passwort, das Ihrem [!DNL Oracle Eloqua] Benutzername. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Der Wert für die Verbindungsspezifikations-ID der [!DNL Oracle Eloqua] -Quelle wie folgt fest: `35d6c4d8-c9a9-11eb-b8bc-0242ac130003`. |

Weitere Informationen zu Authentifizierungsberechtigungen für [!DNL Oracle Eloqua], siehe [[!DNL Oracle Eloqua] Authentifizierungshandbuch](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html).

### Verwenden von Platform-APIs

Informationen zum erfolgreichen Aufrufen von Platform-APIs finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Basisverbindung erstellen

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basis-Verbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an die `/connections` Endpunkt beim Bereitstellen [!DNL Oracle Eloqua] Authentifizierungsberechtigungen als Teil der Anfrageparameter.

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
| `name` | Der Name Ihres [!DNL Oracle Eloqua] Basisverbindung. Es wird empfohlen, einen beschreibenden Namen anzugeben, da Sie diesen Wert zum Nachschlagen Ihrer Basisverbindung verwenden können. |
| `description` | (Optional) Eine Eigenschaft, die Sie einbeziehen können, um zusätzliche Informationen zu Ihrer Basisverbindung bereitzustellen. |
| `auth.specName` | Der Authentifizierungstyp, der für die Verbindung verwendet wird. |
| `auth.params.endpoint` | Der Endpunkt Ihrer [!DNL Oracle Eloqua] Server. |
| `auth.params.username` | Die verkettete Berechtigung, die den Site-Namen und Benutzernamen enthält, der Ihrer [!DNL Oracle Eloqua] -Konto. |
| `auth.params.password` | Das Kennwort, das Ihrem [!DNL Oracle Eloqua] -Konto. |
| `connectionSpec.id` | Der Wert für die Verbindungsspezifikations-ID der [!DNL Oracle Eloqua] -Quelle wie folgt fest: `35d6c4d8-c9a9-11eb-b8bc-0242ac130003`. |

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Basisverbindung zurück, einschließlich der eindeutigen Kennung (`id`). Diese ID ist im nächsten Schritt erforderlich, um eine Quellverbindung zu erstellen.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL Oracle Eloqua] Basisverbindung mit [!DNL Flow Service] API. Sie können diese Basis-Verbindungs-ID in den folgenden Tutorials verwenden:

* [Struktur und Inhalt einer Marketing-Automatisierungsquelle mithilfe des [!DNL Flow Service] API](../../explore/marketing-automation.md)
* [Erstellen Sie einen Datenfluss, um Daten zur Marketing-Automatisierung mit der [!DNL Flow Service] API](../../collect/marketing-automation.md)


