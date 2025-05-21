---
title: Verbinden von PostgreSQL mit Experience Platform mithilfe der Flow Service-API
description: Erfahren Sie, wie Sie Ihre [!DNL PostgreSQL] Datenbank mithilfe von APIs mit Experience Platform verbinden.
exl-id: 5225368a-08c1-421d-aec2-d50ad09ae454
source-git-commit: f4200ca71479126e585ac76dd399af4092fdf683
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 18%

---

# Verbinden von [!DNL PostgreSQL] mit Experience Platform mithilfe der [!DNL Flow Service]-API

Lesen Sie dieses Handbuch, um zu erfahren, wie Sie Ihre [!DNL PostgreSQL]-Datenbank mithilfe der [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/) mit Adobe Experience Platform verbinden.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der [!DNL Flow Service]-API eine Verbindung zu [!DNL PostgreSQL] herstellen zu können.

### Verwenden von Experience Platform-APIs

Lesen Sie das Handbuch [Erste Schritte mit Experience Platform-APIs](../../../../../landing/api-guide.md) um Informationen darüber zu erhalten, wie Sie Experience Platform-APIs erfolgreich aufrufen können.

### Sammeln erforderlicher Anmeldedaten

Weitere Informationen zur Authentifizierung [[!DNL PostgreSQL]  Sie ](../../../../connectors/databases/postgres.md) „Übersicht“.

### Aktivieren der SSL-Verschlüsselung für die Verbindungszeichenfolge

Sie können die SSL-Verschlüsselung für Ihre [!DNL PostgreSQL] Verbindungszeichenfolge aktivieren, indem Sie Ihre Verbindungszeichenfolge mit den folgenden Eigenschaften anhängen:

| Eigenschaft | Beschreibung | Beispiel |
| --- | --- | --- |
| `EncryptionMethod` | Ermöglicht die Aktivierung der SSL-Verschlüsselung Ihrer [!DNL PostgreSQL]. | <uL><li>`EncryptionMethod=0`(deaktiviert)</li><li>`EncryptionMethod=1`(aktiviert)</li><li>`EncryptionMethod=6`(RequestSSL)</li></ul> |
| `ValidateServerCertificate` | Validiert das Zertifikat, das bei der Anwendung von `EncryptionMethod` von Ihrer [!DNL PostgreSQL]-Datenbank gesendet wird. | <uL><li>`ValidationServerCertificate=0`(deaktiviert)</li><li>`ValidationServerCertificate=1`(aktiviert)</li></ul> |

Im Folgenden finden Sie ein Beispiel für eine [!DNL PostgreSQL] Verbindungszeichenfolge, die mit SSL-Verschlüsselung angehängt wird: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD};EncryptionMethod=1;ValidateServerCertificate=1`.

## Verbinden von [!DNL PostgreSQL] mit Experience Platform auf Azure {#azure}

Gehen Sie wie folgt vor, um zu erfahren, wie Sie Ihr [!DNL PostgreSQL]-Konto mit Experience Platform auf Azure verbinden.

### Erstellen einer Basisverbindung {#azure-base}

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Experience Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen ID der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basisverbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den Endpunkt `/connections` und geben Sie dabei Ihre [!DNL PostgreSQL]-Authentifizierungs-Anmeldedaten als Teil der Anfrageparameter an.

**API-Format**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB Schlüsselbasierte Authentifizierung für das Konto]

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL PostgreSQL] mit Authentifizierung über einen Kontoschlüssel:

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
      "name": "PostgreSQL base connection",
      "description": "PostgreSQL base connection via connection string",
      "auth": {
          "specName": "Connection String Based Authentication",
          "params": {
              "connectionString": "Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "74a1c565-4e59-48d7-9d67-7c03b8a13137",
          "version": "1.0"
      }
  }'
```

| Eigenschaft | Beschreibung |
| ------------- | --------------- |
| `auth.params.connectionString` | Die mit Ihrem [!DNL PostgreSQL]-Konto verknüpfte Verbindungszeichenfolge. Das [!DNL PostgreSQL]-Verbindungszeichenfolgenmuster ist: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | Die Spezifikations-IDs der [!DNL PostgreSQL]-Verbindung: `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

+++

**Antwort**

Bei einer erfolgreichen Antwort wird die eindeutige Kennung (`id`) der neu erstellten Basisverbindung zurückgegeben.

+++Beispiel für eine Antwort anzeigen

```json
{
    "id": "056dd1b4-da33-42f9-add1-b4da3392f94e",
    "etag": "\"1700e582-0000-0200-0000-5e3c85180000\""
}
```

+++

>[!TAB Einfache Authentifizierung]

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL PostgreSQL] mit einfacher Authentifizierung:

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
      "name": "PostgreSQL base connection",
      "description": "PostgreSQL base connection via basic authentication",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "localhost",
              "port": "3306",
              "database": "postgresql-acme",
              "username": "acme",
              "password": "xxxx",
              "sslMode": "Allow"
          }
      },
      "connectionSpec": {
          "id": "74a1c565-4e59-48d7-9d67-7c03b8a13137",
          "version": "1.0"
      }
  }'
```

| Eigenschaft | Beschreibung |
| ---| --- |
| `auth.params.server` | Der Name oder die IP-Adresse Ihrer [!DNL PostgreSQL]. |
| `auth.params.port` | Die Port-Nummer des Datenbank-Servers. |
| `auth.params.database` | Der Name Ihrer [!DNL PostgreSQL]. |
| `auth.params.username` | Der Benutzername, der Ihrer [!DNL PostgreSQL]-Datenbankauthentifizierung zugeordnet ist. |
| `auth.params.password` | Das Passwort, das mit Ihrer [!DNL PostgreSQL]-Datenbankauthentifizierung verknüpft ist. |
| `auth.params.sslMode` | Die Methode, mit der Daten während der Datenübertragung verschlüsselt werden. Zu den verfügbaren Werten gehören: `Disable`, `Allow`, `Prefer`, `Verify Ca` und `Verify Full`. |
| `connectionSpec.id` | Die Spezifikations-IDs der [!DNL PostgreSQL]-Verbindung: `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

+++

**Antwort**

Bei einer erfolgreichen Antwort wird die eindeutige Kennung (`id`) der neu erstellten Basisverbindung zurückgegeben.

+++Beispiel für eine Antwort anzeigen

```json
{
    "id": "2c15b1c5-73bf-47ab-9098-0467fcd854d9",
    "etag": "\"2600fc39-0000-0200-0000-67dd48f80000\""
}
```

+++

>[!ENDTABS]

## Verbinden von [!DNL PostgreSQL] mit Experience Platform auf Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Dieser Abschnitt gilt für Implementierungen von Experience Platform, die auf Amazon Web Services (AWS) ausgeführt werden. Experience Platform, das auf AWS ausgeführt wird, steht derzeit einer begrenzten Anzahl von Kunden zur Verfügung. Weitere Informationen zur unterstützten Experience Platform-Infrastruktur finden Sie in der Übersicht zur [Experience Platform Multi-Cloud](../../../../../landing/multi-cloud.md).

Lesen Sie die folgenden Schritte, um Informationen zum Verbinden Ihrer [!DNL PostgreSQL]-Datenbank mit Experience Platform auf AWS zu erhalten.

### Erstellen einer Basisverbindung {#aws-base}

Um eine Basisverbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den `/connections`-Endpunkt beim Bereitstellen der [!DNL PostgreSQL]-Authentifizierungs-Anmeldedaten als Teil der Anfrageparameter.

**API-Format**

```https
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL PostgreSQL], um eine Verbindung zu Experience Platform auf AWS herzustellen.

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
      "name": "PostgreSQL base connection",
      "description": "PostgreSQL base connection via basic authentication",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "localhost",
              "port": "3306",
              "database": "postgresql-acme",
              "username": "acme",
              "password": "xxxx",
              "sslMode": "false"
          }
      },
      "connectionSpec": {
          "id": "74a1c565-4e59-48d7-9d67-7c03b8a13137",
          "version": "1.0"
      }
  }'
```

| Eigenschaft | Beschreibung |
| ---| --- |
| `auth.params.server` | Der Name oder die IP-Adresse Ihrer [!DNL PostgreSQL]. |
| `auth.params.port` | Die Port-Nummer des Datenbank-Servers. |
| `auth.params.database` | Der Name Ihrer [!DNL PostgreSQL]. |
| `auth.params.username` | Der Benutzername, der Ihrer [!DNL PostgreSQL]-Datenbankauthentifizierung zugeordnet ist. |
| `auth.params.password` | Das Passwort, das mit Ihrer [!DNL PostgreSQL]-Datenbankauthentifizierung verknüpft ist. |
| `sslMode` | Ein boolescher Wert, der steuert, ob SSL je nach Server-Unterstützung erzwungen wird oder nicht. Die Standardeinstellung für diese Konfiguration ist `false`. |
| `connectionSpec.id` | Die Spezifikations-IDs der [!DNL PostgreSQL]-Verbindung: `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

+++

**Antwort**

Bei einer erfolgreichen Antwort wird die eindeutige Kennung (`id`) der neu erstellten Basisverbindung zurückgegeben.

+++Beispiel für eine Antwort anzeigen

```json
{
    "id": "2c15b1c5-73bf-47ab-9098-0467fcd854d9",
    "etag": "\"2600fc39-0000-0200-0000-67dd48f80000\""
}
```

+++

## Nächste Schritte

Nachdem Sie eine Verbindung zwischen Ihrer [!DNL PostgreSQL]-Datenbank und Experience Platform erstellt haben, können Sie jetzt mit den nächsten Schritten fortfahren und Ihre [!DNL PostgreSQL]-Daten in Experience Platform übertragen. Weitere Informationen finden Sie in der folgenden Dokumentation:

* [Erkunden von Struktur und Inhalten Ihrer Datentabellen mithilfe der  [!DNL Flow Service] -API](../../explore/tabular.md)
* [Erstellen eines Datenflusses, um Datenbankdaten mithilfe der API  [!DNL Flow Service]  Experience Platform zu übertragen](../../collect/database-nosql.md)
