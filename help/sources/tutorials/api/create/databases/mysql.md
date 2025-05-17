---
title: Verbinden von MySQL mit Experience Platform mithilfe der Flow Service-API
description: Erfahren Sie, wie Sie Ihre MySQL-Datenbank mithilfe von APIs mit Experience Platform verbinden.
exl-id: 273da568-84ed-4a3d-bfea-0f5b33f1551a
source-git-commit: 659af23c6d05f184b745e13ab8545941f3892e7e
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 7%

---

# Verbinden von [!DNL MySQL] mit Experience Platform mithilfe der [!DNL Flow Service]-API

Lesen Sie dieses Handbuch, um zu erfahren, wie Sie Ihr [!DNL MySQL]-Konto mithilfe der [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/) mit Adobe Experience Platform verbinden.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der [!DNL Flow Service]-API eine Verbindung zu [!DNL MySQL] herstellen zu können.

### Sammeln erforderlicher Anmeldedaten

Informationen zur Authentifizierung [[!DNL MySQL]  Sie in ](../../../../connectors/databases/mysql.md#prerequisites)Übersicht“.

### Verwenden von Experience Platform-APIs

Lesen Sie das Handbuch [Erste Schritte mit Experience Platform-APIs](../../../../../landing/api-guide.md) um Informationen darüber zu erhalten, wie Sie Experience Platform-APIs erfolgreich aufrufen können.

## Verbinden von [!DNL MySQL] mit Experience Platform auf Azure {#azure}

Lesen Sie die folgenden Schritte, um Informationen zum Verbinden Ihres [!DNL MySQL]-Kontos mit Experience Platform auf Azure zu erhalten.

### Erstellen einer Basisverbindung für [!DNL MySQL] auf Experience Platform auf Azure {#azure-base}

Eine Basisverbindung verknüpft Ihre Quelle mit Experience Platform und speichert Authentifizierungsdetails, Verbindungsstatus und eine eindeutige ID. Verwenden Sie diese ID, um Quelldateien zu durchsuchen und bestimmte aufzunehmende Elemente zu identifizieren, einschließlich ihrer Datentypen und Formate.

**API-Format**

```https
POST /connections
```

Um eine Basisverbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den `/connections`-Endpunkt und geben Sie Ihre [!DNL MySQL] Authentifizierungsdaten als Teil der Anfrageparameter an.

>[!BEGINTABS]

>[!TAB Auf Verbindungszeichenfolgen basierende Authentifizierung]

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL MySQL] unter Verwendung der Authentifizierung über eine Verbindungszeichenfolge.

+++Beispiel für eine Anfrage anzeigen

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "MySQL Base Connection to Experience Platform",
      "description": "Via Connection String,
      "auth": {
          "specName": "Connection String Based Authentication",
          "params": {
              "connectionString": "Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "26d738e0-8963-47ea-aadf-c60de735468a",
          "version": "1.0"
      }
  }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `auth.params.connectionString` | Die Ihrem Konto zugeordnete [!DNL MySQL]-Verbindungszeichenfolge. Das [!DNL MySQL]-Verbindungszeichenfolgenmuster ist: `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | Die Spezifikations-ID der [!DNL MySQL]-Verbindung: `26d738e0-8963-47ea-aadf-c60de735468a`. |

+++

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Basisverbindung zurück, einschließlich ihrer eindeutigen Kennung (`id`).

+++Beispiel für eine Antwort anzeigen

```json
{
    "id": "1a444165-3439-4c16-8441-653439dc166a",
    "etag": "\"5b04c219-0000-0200-0000-5e179c8f0000\""
}
```

+++

>[!TAB Einfache Authentifizierung]

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für eine [!DNL MySQL] mit einfacher Authentifizierung.

+++Beispiel für eine Anfrage anzeigen

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "MySQL Base Connection to Experience Platform",
      "description": "Via Basic Authentication",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "database": "{DATABASE}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "sslMode": "{SSLMODE}"
          }
      },
      "connectionSpec": {
          "id": "26d738e0-8963-47ea-aadf-c60de735468a",
          "version": "1.0"
      }
  }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `auth.params.server` | Der Name oder die IP der [!DNL MySQL]. |
| `auth.params.database` | Der Name Ihrer Datenbank. |
| `auth.params.username` | Der Benutzername, der Ihrer Datenbank entspricht. |
| `auth.params.password` | Das Passwort, das Ihrer Datenbank entspricht. |
| `auth.params.sslMode` | Die Methode, mit der Daten während der Datenübertragung verschlüsselt werden. |
| `connectionSpec.id` | Die Spezifikations-ID der [!DNL MySQL]-Verbindung lautet: `26d738e0-8963-47ea-aadf-c60de735468a`. |

+++

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Basisverbindung zurück, einschließlich ihrer eindeutigen Kennung (`id`).

+++Beispiel für eine Antwort anzeigen

```json
{
    "id": "025d4158-4113-403b-b551-e81724d3880c",
    "etag": "\"ae004437-0000-0200-0000-67ee107e0000\""
}
```

+++

>[!ENDTABS]

## Verbinden von [!DNL MySQL] mit Experience Platform auf Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Dieser Abschnitt gilt für Implementierungen von Experience Platform, die auf Amazon Web Services (AWS) ausgeführt werden. Experience Platform, das auf AWS ausgeführt wird, steht derzeit einer begrenzten Anzahl von Kunden zur Verfügung. Weitere Informationen zur unterstützten Experience Platform-Infrastruktur finden Sie in der Übersicht zur [Experience Platform Multi-Cloud](../../../../../landing/multi-cloud.md).

Lesen Sie die folgenden Schritte, um Informationen zum Verbinden Ihres [!DNL MySQL]-Kontos mit Experience Platform auf AWS zu erhalten.

### Erstellen einer Basisverbindung für [!DNL MySQL] auf Experience Platform auf AWS {#aws-base}

**API-Format**

```https
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL MySQL], um eine Verbindung zu Experience Platform auf AWS herzustellen.

+++Beispiel für eine Anfrage anzeigen

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "MySQL on Experience Platform AWS",
      "description": "MySQL on Experience Platform AWS",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "database": "{DATABASE}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "sslMode": "{SSLMODE}"
          }
      },
      "connectionSpec": {
          "id": "26d738e0-8963-47ea-aadf-c60de735468a",
          "version": "1.0"
      }
  }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `auth.params.server` | Der Name oder die IP der [!DNL MySQL]. |
| `auth.params.database` | Der Name Ihrer Datenbank. |
| `auth.params.username` | Der Benutzername, der Ihrer Datenbank entspricht. |
| `auth.params.password` | Das Passwort, das Ihrer Datenbank entspricht. |
| `auth.params.sslMode` | Die Methode, mit der Daten während der Datenübertragung verschlüsselt werden. |
| `connectionSpec.id` | Die Spezifikations-ID der [!DNL MySQL]-Verbindung lautet: `26d738e0-8963-47ea-aadf-c60de735468a`. |

+++

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Basisverbindung zurück, einschließlich ihrer eindeutigen Kennung (`id`).

+++Beispiel für eine Antwort anzeigen

```json
{
    "id": "f847950c-1c12-4568-a550-d5312b16fdb8",
    "etag": "\"0c0099f4-0000-0200-0000-67da91710000\""
}
```

+++

## Erstellen eines Datenflusses für [!DNL MySQL] Daten

Nachdem Sie Ihre [!DNL MySQL] erfolgreich verbunden haben, können Sie jetzt [einen Datenfluss erstellen und Daten aus Ihrer Datenbank in Experience Platform aufnehmen](../../collect/database-nosql.md).