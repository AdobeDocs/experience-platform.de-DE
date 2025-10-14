---
title: Verbinden von MariaDB mit Experience Platform mithilfe der Flow Service-API
description: Erfahren Sie, wie Sie Ihr MariaDB-Konto mithilfe von APIs mit Experience Platform verbinden.
exl-id: 9b7ff394-ca55-4ab4-99ef-85c80b04a6df
source-git-commit: bca4f40d452f0a5e70a388872a65640d1fd58533
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 22%

---

# Verbinden von [!DNL MariaDB] mit Experience Platform mithilfe der [!DNL Flow Service]-API

Lesen Sie dieses Handbuch, um zu erfahren, wie Sie Ihr [!DNL MariaDB]-Konto mithilfe der [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/) mit Adobe Experience Platform verbinden.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der [!DNL Flow Service]-API eine Verbindung zu [!DNL MariaDB] herstellen zu können.

### Sammeln erforderlicher Anmeldedaten

Informationen zur Authentifizierung [[!DNL MariaDB]  Sie in &#x200B;](../../../../connectors/databases/mariadb.md#prerequisites)Übersicht“.

### Verwenden von Experience Platform-APIs

Lesen Sie das Handbuch [Erste Schritte mit Experience Platform-APIs](../../../../../landing/api-guide.md) um Informationen darüber zu erhalten, wie Sie Experience Platform-APIs erfolgreich aufrufen können.

## Verbinden von [!DNL MariaDB] mit Experience Platform

Lesen Sie die folgenden Schritte, um Informationen zum Verbinden Ihres [!DNL MariaDB]-Kontos mit Experience Platform zu erhalten.

### Erstellen einer Basisverbindung für [!DNL MariaDB]

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Experience Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen ID der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

**API-Format**

```https
POST /connections
```

Um eine Basisverbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den `/connections`-Endpunkt und geben Sie die entsprechenden Authentifizierungsdaten für Ihr [!DNL MariaDB]-Konto an.

>[!BEGINTABS]

>[!TAB Auf Verbindungszeichenfolgen basierende Authentifizierung]

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für eine [!DNL MariaDB] mithilfe der Authentifizierung über eine Verbindungszeichenfolge.

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
    "name": "MariaDB connection",
    "description": "MariaDB connection",
    "auth": {
        "specName": "Connection String Based Authentication",
        "params": {
            "connectionString": "Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}"
        }
    },
    "connectionSpec": {
        "id": "3000eb99-cd47-43f3-827c-43caf170f015",
        "version": "1.0"
    }
}'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `auth.params.connectionString` | Die mit Ihrer [!DNL MariaDB] verknüpfte Verbindungszeichenfolge. Das [!DNL MariaDB]-Verbindungszeichenfolgenmuster ist: `Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | Die Spezifikations-ID der [!DNL MariaDB]-Verbindung lautet: `3000eb99-cd47-43f3-827c-43caf170f015`. |

+++

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Basisverbindung zurück, einschließlich ihrer eindeutigen Kennung (`id`).

+++Beispiel für eine Antwort anzeigen

```json
{
    "id": "be3a2d71-1fb6-4fea-ba2d-711fb61fea50",
    "etag": "\"02002624-0000-0200-0000-5e41f7040000\""
}
```

+++

>[!TAB Einfache Authentifizierung]

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für eine [!DNL MariaDB] mit einfacher Authentifizierung.

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
      "name": "MariaDB on Experience Platform using basic auth",
      "description": "MariaDB on Experience Platform using basic auth",
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
          "id": "3000eb99-cd47-43f3-827c-43caf170f015",
          "version": "1.0"
      }
  }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `auth.params.server` | Der Name oder die IP der [!DNL MariaDB]. |
| `auth.params.database` | Der Name Ihrer Datenbank. |
| `auth.params.username` | Der Benutzername, der Ihrer Datenbank entspricht. |
| `auth.params.password` | Das Passwort, das Ihrer Datenbank entspricht. |
| `auth.params.sslMode` | Die Methode, mit der Daten während der Datenübertragung verschlüsselt werden. |
| `connectionSpec.id` | Die Spezifikations-ID der [!DNL MariaDB]-Verbindung lautet: `3000eb99-cd47-43f3-827c-43caf170f015`. |

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

>[!ENDTABS]


## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL MariaDB]-Basisverbindung mithilfe der [!DNL Flow Service]-API erstellt. Sie können diese Basisverbindungs-ID in den folgenden Tutorials verwenden:

* [Erkunden von Struktur und Inhalten Ihrer Datentabellen mithilfe der  [!DNL Flow Service] -API](../../explore/tabular.md)
* [Erstellen eines Datenflusses, um Datenbankdaten mithilfe der API  [!DNL Flow Service]  Experience Platform zu übertragen](../../collect/database-nosql.md)
