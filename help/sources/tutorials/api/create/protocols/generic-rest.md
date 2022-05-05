---
keywords: Experience Platform; Startseite; beliebte Themen; generische REST; generische Ruhezeit
solution: Experience Platform
title: Erstellen einer generischen REST-API-Basisverbindung mit der Flow Service-API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Flow Service-API eine Verbindung der generischen REST-API mit Adobe Experience Platform herstellen.
exl-id: 6b414868-503e-49d5-8f4a-5b2fc003dab0
source-git-commit: 1f2ae53e5503618b7ac12628923b30c457fd17e2
workflow-type: tm+mt
source-wordcount: '945'
ht-degree: 54%

---

# Erstellen Sie eine generische REST-API-Basisverbindung mit dem [!DNL Flow Service] API

>[!NOTE]
>
>Die [!DNL Generic REST API] -Quelle befindet sich in der Beta-Phase. Siehe [Quellen - Übersicht](../../../../home.md#terms-and-conditions) Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectoren.

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL Generic REST API] mithilfe der [[!DNL Flow Service] -API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Informationen darüber, wie Sie Platform-APIs erfolgreich aufrufen können, finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

### Sammeln erforderlicher Anmeldeinformationen

Zur [!DNL Flow Service] zur Verbindung mit [!DNL Generic REST API]müssen Sie gültige Anmeldeinformationen für den Authentifizierungstyp Ihrer Wahl angeben. [!DNL Generic REST API] unterstützt sowohl OAuth 2-Aktualisierungscode als auch einfache Authentifizierung. In den folgenden Tabellen finden Sie Informationen zu den Anmeldeinformationen für die beiden unterstützten Authentifizierungstypen.

#### OAuth 2-Aktualisierungscode

| Anmeldedaten | Beschreibung |
| --- | --- |
| `host` | Die Host-URL der Quelle, an die Sie Ihre Anfrage richten. Dieser Wert ist erforderlich und kann nicht mithilfe von `requestParameterOverride`. |
| `authorizationTestUrl` | (Optional) Die URL für den Autorisierungstest wird verwendet, um Anmeldeinformationen beim Erstellen einer Basisverbindung zu überprüfen. Wenn die Anmeldeinformationen nicht angegeben sind, werden sie stattdessen während des Erstellungsschritts der Quellverbindung automatisch überprüft. |
| `clientId` | (Optional) Die mit Ihrem Benutzerkonto verknüpfte Client-ID. |
| `clientSecret` | (Optional) Das mit Ihrem Benutzerkonto verknüpfte Client-Geheimnis. |
| `accessToken` | Die primäre Authentifizierungsberechtigung für den Zugriff auf Ihre Anwendung. Das Zugriffstoken stellt die Autorisierung Ihrer Anwendung dar, um auf bestimmte Aspekte der Daten eines Benutzers zuzugreifen. Dieser Wert ist erforderlich und kann nicht mithilfe von `requestParameterOverride`. |
| `refreshToken` | (Optional) Ein Token, mit dem ein neues Zugriffstoken generiert wird, wenn das Zugriffstoken abgelaufen ist. |
| `expirationDate` | (Optional) Ein ausgeblendeter Wert, der das Ablaufdatum Ihres Zugriffstokens definiert. |
| `accessTokenUrl` | (Optional) Der URL-Endpunkt, der zum Abrufen Ihres Zugriffstokens verwendet wird. |
| `requestParameterOverride` | (Optional) Eine Eigenschaft, mit der Sie angeben können, welche Berechtigungsparameter überschrieben werden sollen. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL Generic REST API] ist: `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |

#### Einfache Authentifizierung

| Anmeldedaten | Beschreibung |
| --- | --- |
| `host` | Die Host-URL der Quelle, an die Sie Ihre Anfrage richten. |
| `username` | Der Benutzername, der Ihrem Benutzerkonto entspricht. |
| `password` | Das Kennwort, das Ihrem Benutzerkonto entspricht. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL Generic REST API] ist: `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |

## Erstellen einer Basisverbindung

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

[!DNL Generic REST API] unterstützt sowohl einfache Authentifizierung als auch OAuth 2-Aktualisierungs-Code. In den folgenden Beispielen finden Sie Anleitungen zum Authentifizieren mit beiden Authentifizierungstypen.

### Erstellen einer [!DNL Generic REST API]-Basisverbindung mit OAuth 2-Aktualisierungs-Code

Um eine Basis-Verbindungs-ID mit dem OAuth 2-Aktualisierungscode zu erstellen, stellen Sie eine POST-Anfrage an die `/connections` -Endpunkt bei der Bereitstellung Ihrer OAuth 2-Anmeldeinformationen.

**API-Format**

```http
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Generic REST API]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Generic REST API base connection with OAuth 2 refresh code",
      "description": "Generic REST API base connection with OAuth 2 refresh code",
      "connectionSpec": {
          "id": "4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62",
          "version": "1.0"
      },
      "auth": {
          "specName": "oAuth2RefreshCode",
          "params": {
              "host": "{HOST}",
              "accessToken": "{ACCESS_TOKEN}"
          }
      }
  }'
```

| Eigenschaft | Beschreibung |
| --------- | ----------- |
| `name` | Der Name Ihrer Basisverbindung. Stellen Sie sicher, dass der Name Ihrer Basisverbindung beschreibend ist, da Sie damit Informationen zu Ihrer Basisverbindung nachschlagen können. |
| `description` | (Optional) Eine Eigenschaft, die Sie einbeziehen können, um weitere Informationen zu Ihrer Basisverbindung bereitzustellen. |
| `connectionSpec.id` | Die mit [!DNL Generic REST API]. Diese feste ID lautet: `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |
| `auth.specName` | Der Authentifizierungstyp, mit dem Sie Ihre Quelle für Platform authentifizieren. |
| `auth.params.host` | Die Stamm-URL, die für die Verbindung mit Ihrer [!DNL Generic REST API] -Quelle. |
| `auth.params.accessToken` | Das entsprechende Zugriffs-Token, das zum Authentifizieren Ihrer Quelle verwendet wird. Dies ist für die OAuth-basierte Authentifizierung erforderlich. |

**Antwort**

Eine erfolgreiche Antwort gibt die neu erstellte Verbindung zurück, einschließlich der eindeutigen Verbindungskennung (`id`). Diese ID ist erforderlich, um Ihre Daten im nächsten Tutorial zu untersuchen.

```json
{
  "id": "a5c6b647-e784-4b58-86b6-47e784ab580b",
  "etag": "\"7b01056a-0000-0200-0000-5e8a4f5b0000\""
}
```

### Erstellen einer [!DNL Generic REST API]-Basisverbindung mit einfacher Authentifizierung

So erstellen Sie eine [!DNL Generic REST API] Basisverbindung mit einfacher Authentifizierung, stellen Sie eine POST-Anfrage an die `/connections` Endpunkt von [!DNL Flow Service] API bei der Bereitstellung Ihrer grundlegenden Authentifizierungsberechtigungen.

**API-Format**

```https
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Generic REST API]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "Generic REST API base connection with basic authentication",
      "description": "Generic REST API base connection with basic authentication",
      "connectionSpec": {
          "id": "4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62",
          "version": "1.0"
      },
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "{HOST}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      }
  }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der Name Ihrer Basisverbindung. Stellen Sie sicher, dass der Name Ihrer Basisverbindung beschreibend ist, da Sie damit Informationen zu Ihrer Basisverbindung nachschlagen können. |
| `description` | (Optional) Eine Eigenschaft, die Sie einbeziehen können, um weitere Informationen zu Ihrer Basisverbindung bereitzustellen. |
| `connectionSpec.id` | Die mit [!DNL Generic REST API]. Diese feste ID lautet: `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |
| `auth.specName` | Der Authentifizierungstyp, mit dem Sie Ihre Quelle mit Platform verbinden. |
| `auth.params.host` | Die Stamm-URL, die für die Verbindung mit Ihrer [!DNL Generic REST API] -Quelle. |
| `auth.params.username` | Der Benutzername, der Ihrer [!DNL Generic REST API] -Quelle. Dies ist für die einfache Authentifizierung erforderlich. |
| `auth.params.password` | Das Kennwort, das Ihrem [!DNL Generic REST API] -Quelle. Dies ist für die einfache Authentifizierung erforderlich. |

**Antwort**

Eine erfolgreiche Antwort gibt die neu erstellte Basisverbindung zurück, einschließlich ihrer eindeutigen Verbindungskennung (`id`). Diese ID ist erforderlich, um die Dateistruktur und Inhalte Ihrer Quelle im nächsten Schritt zu untersuchen.

```json
{
    "id": "9601747c-6874-4c02-bb00-5732a8c43086",
    "etag": "\"3702dabc-0000-0200-0000-615b5b5a0000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL Generic REST API] Basisverbindung mit [!DNL Flow Service] API. Sie können diese Basis-Verbindungs-ID in den folgenden Tutorials verwenden:

* [Struktur und Inhalt Ihrer Datentabellen mithilfe des [!DNL Flow Service] API](../../explore/tabular.md)
* [Erstellen Sie einen Datenfluss, um Protokolldaten mit der [!DNL Flow Service] API](../../collect/protocols.md)
