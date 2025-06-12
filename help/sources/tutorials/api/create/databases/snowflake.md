---
title: Verbinden von Snowflake mit Experience Platform mithilfe der Flow Service-API
description: Erfahren Sie, wie Sie Adobe Experience Platform mithilfe der Flow Service-API mit Snowflake verbinden.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 0ef34d30-7b4c-43f5-8e2e-cde05da05aa5
source-git-commit: d8d9303e358c66c4cd891d6bf59a801c09a95f8e
workflow-type: tm+mt
source-wordcount: '1251'
ht-degree: 15%

---

# Verbinden von [!DNL Snowflake] mit Experience Platform mithilfe der [!DNL Flow Service]-API

>[!IMPORTANT]
>
>Die [!DNL Snowflake] ist im Quellkatalog für Benutzende verfügbar, die Real-Time Customer Data Platform Ultimate erworben haben.

Lesen Sie dieses Handbuch, um zu erfahren, wie Sie Ihr [!DNL Snowflake]-Quellkonto mithilfe der [[!DNL Flow Service] API) mit Adobe Experience Platform ](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Experience Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Experience Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Verwenden von Experience Platform-APIs

Informationen zum erfolgreichen Aufrufen von Experience Platform-APIs finden Sie im Handbuch unter [ mit Experience Platform-APIs](../../../../../landing/api-guide.md).

Der folgende Abschnitt enthält zusätzliche Informationen, die Sie benötigen, um sich mithilfe der [!DNL Flow Service]-API erfolgreich mit [!DNL Snowflake] verbinden zu können.

## Verbinden von [!DNL Snowflake] mit Experience Platform auf Azure {#azure}

Lesen Sie die folgenden Schritte, um Informationen zum Verbinden Ihrer [!DNL Snowflake] mit Experience Platform auf Azure zu erhalten.

### Sammeln erforderlicher Anmeldedaten

>[!WARNING]
>
>Die Standardauthentifizierung (oder Kontoschlüsselauthentifizierung) für die [!DNL Snowflake] wird ab November 2025 eingestellt. Sie müssen zur schlüsselpaarbasierten Authentifizierung wechseln, um weiterhin die -Quelle verwenden und Daten aus Ihrer -Datenbank in Experience Platform aufnehmen zu können. Weitere Informationen zur Einstellung finden Sie im [[!DNL Snowflake] Handbuch mit Best Practices zum Minimieren der Risiken durch das Kompromittieren von Anmeldeinformationen](https://www.snowflake.com/en/resources/white-paper/best-practices-to-mitigate-the-risk-of-credential-compromise/).

Sie müssen Werte für die folgenden Anmeldeinformationen angeben, um Ihre [!DNL Snowflake] zu authentifizieren.

>[!BEGINTABS]

>[!TAB Authentifizierung mit Kontoschlüssel]

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| `account` | Ein Kontoname identifiziert ein Konto innerhalb Ihrer Organisation eindeutig. In diesem Fall müssen Sie ein Konto über verschiedene [!DNL Snowflake] hinweg eindeutig identifizieren. Dazu müssen Sie dem Kontonamen den Namen Ihres Unternehmens voranstellen. Beispiel: `orgname-account_name`. Weitere Anleitungen finden Sie im Handbuch [Abrufen  [!DNL Snowflake]  Kontokennung](../../../../connectors/databases/snowflake.md#retrieve-your-account-identifier) . Weiterführende Informationen dazu finden Sie im [[!DNL Snowflake] entsprechenden Handbuch](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `warehouse` | Das [!DNL Snowflake] Warehouse verwaltet den Abfrageausführungsprozess für das Programm. Jedes [!DNL Snowflake] Warehouse ist unabhängig voneinander und muss beim Übermitteln von Daten an Experience Platform einzeln aufgerufen werden. |
| `database` | Die [!DNL Snowflake]-Datenbank enthält die Daten, die Sie mit der Experience Platform verknüpfen möchten. |
| `username` | Der Benutzername für das [!DNL Snowflake]. |
| `password` | Das Kennwort für das [!DNL Snowflake] Benutzerkonto. |
| `role` | Die in der [!DNL Snowflake]-Sitzung zu verwendende standardmäßige Zugriffssteuerungsrolle. Die Rolle sollte eine vorhandene sein, die dem angegebenen Benutzer bereits zugewiesen wurde. Die Standardrolle ist `PUBLIC`. |
| `connectionString` | Die Verbindungszeichenfolge, die für die Verbindung mit Ihrer [!DNL Snowflake]-Instanz verwendet wird. Das Verbindungszeichenfolgenmuster für [!DNL Snowflake] ist `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

>[!TAB Schlüsselpaar-Authentifizierung]

Um die Schlüsselpaar-Authentifizierung zu verwenden, müssen Sie ein 2048-Bit-RSA-Schlüsselpaar generieren und dann die folgenden Werte angeben, wenn Sie ein Konto für Ihre [!DNL Snowflake] erstellen.

| Anmeldedaten | Beschreibung |
| --- | --- |
| `account` | Ein Kontoname identifiziert ein Konto innerhalb Ihrer Organisation eindeutig. In diesem Fall müssen Sie ein Konto über verschiedene [!DNL Snowflake] hinweg eindeutig identifizieren. Dazu müssen Sie dem Kontonamen den Namen Ihres Unternehmens voranstellen. Beispiel: `orgname-account_name`. Weitere Anleitungen finden Sie im Handbuch [Abrufen  [!DNL Snowflake]  Kontokennung](../../../../connectors/databases/snowflake.md#retrieve-your-account-identifier) . Weiterführende Informationen dazu finden Sie im [[!DNL Snowflake] entsprechenden Handbuch](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `username` | Der Benutzername Ihres [!DNL Snowflake]. |
| `privateKey` | Der [!DNL Base64-]kodierte private Schlüssel Ihres [!DNL Snowflake]. Sie können entweder verschlüsselte oder unverschlüsselte private Schlüssel generieren. Wenn Sie einen verschlüsselten privaten Schlüssel verwenden, müssen Sie auch eine Passphrase für den privaten Schlüssel angeben, wenn Sie sich bei Experience Platform authentifizieren. Weitere Informationen finden Sie im Handbuch unter [Abrufen  [!DNL Snowflake]  privaten ](../../../../connectors/databases/snowflake.md)Schlüssels). |
| `privateKeyPassphrase` | Die Passphrase für den privaten Schlüssel ist eine zusätzliche Sicherheitsebene, die Sie bei der Authentifizierung mit einem verschlüsselten privaten Schlüssel verwenden müssen. Sie müssen die Passphrase nicht angeben, wenn Sie einen unverschlüsselten privaten Schlüssel verwenden. |
| `database` | Die [!DNL Snowflake], die die Daten enthält, die in Experience Platform aufgenommen werden sollen. |
| `warehouse` | Das [!DNL Snowflake] Warehouse verwaltet den Abfrageausführungsprozess für das Programm. Jedes [!DNL Snowflake] Warehouse ist unabhängig voneinander und muss beim Übermitteln von Daten an Experience Platform einzeln aufgerufen werden. |

Weitere Informationen zu diesen Werten finden Sie im [[!DNL Snowflake] Handbuch zur Schlüsselpaar-Authentifizierung](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

>[!NOTE]
>
>Sie müssen das `PREVENT_UNLOAD_TO_INLINE_URL`-Flag auf `FALSE` setzen, um das Entladen von Daten aus Ihrer [!DNL Snowflake] in Experience Platform zu ermöglichen.

### Erstellen einer Basisverbindung für [!DNL Snowflake] auf Experience Platform auf Azure {#azure-base}

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Experience Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen ID der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basisverbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den `/connections`-Endpunkt und geben Sie dabei Ihre [!DNL Snowflake] Authentifizierungsdaten als Teil des Anfragetexts an.

**API-Format**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB connectionString]

+++Anfrage

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Snowflake]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection",
      "description": "Snowflake base connection",
      "auth": {
          "specName": "ConnectionString",
          "params": {
              "connectionString": "jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}"
          }
      },
      "connectionSpec": {
          "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
          "version": "1.0"
      }
  }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `auth.params.connectionString` | Die Verbindungszeichenfolge, die für die Verbindung mit Ihrer [!DNL Snowflake]-Instanz verwendet wird. Das Verbindungszeichenfolgenmuster für [!DNL Snowflake] ist `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`. |
| `connectionSpec.id` | Die Spezifikations-ID der [!DNL Snowflake]-Verbindung: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

+++

+++Antwort

Eine erfolgreiche Antwort gibt die neu erstellte Verbindung zurück, einschließlich ihrer eindeutigen Verbindungskennung (`id`). Diese ID ist erforderlich, um Ihre Daten im nächsten Tutorial zu untersuchen.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++


>[!TAB Schlüsselpaar-Authentifizierung mit verschlüsseltem privaten Schlüssel]

+++Anfrage

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection with encrypted private key",
      "description": "Snowflake base connection with encrypted private key",
      "auth": {
        "specName": "KeyPair Authentication",
        "params": {
            "account": "acme-snowflake123",
            "username": "acme-cj123",
            "database": "ACME_DB",
            "privateKey": "{BASE_64_ENCODED_PRIVATE_KEY}",
            "privateKeyPassphrase": "abcd1234",
            "warehouse": "COMPUTE_WH"
        }
    },
    "connectionSpec": {
        "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
        "version": "1.0"
    }
  }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `auth.params.account` | Der Name Ihres [!DNL Snowflake]. |
| `auth.params.username` | Der Benutzername, der Ihrem [!DNL Snowflake]-Konto zugeordnet ist. |
| `auth.params.database` | Die [!DNL Snowflake] Datenbank, aus der die Daten abgerufen werden. |
| `auth.params.privateKey` | Der [!DNL Base64-]verschlüsselte private Schlüssel Ihres [!DNL Snowflake]. |
| `auth.params.privateKeyPassphrase` | Die Passphrase, die Ihrem privaten Schlüssel entspricht. |
| `auth.params.warehouse` | Das [!DNL Snowflake] Warehouse, das Sie verwenden. |
| `connectionSpec.id` | Die Spezifikations-ID der [!DNL Snowflake]-Verbindung: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

+++

+++Antwort

Eine erfolgreiche Antwort gibt die neu erstellte Verbindung zurück, einschließlich ihrer eindeutigen Verbindungskennung (`id`). Diese ID ist erforderlich, um Ihre Daten im nächsten Tutorial zu untersuchen.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++

>[!TAB Schlüsselpaar-Authentifizierung mit unverschlüsseltem privaten Schlüssel]

+++Anfrage

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection with encrypted private key",
      "description": "Snowflake base connection with encrypted private key",
      "auth": {
        "specName": "KeyPair Authentication",
        "params": {
            "account": "acme-snowflake123",
            "username": "acme-cj123",
            "database": "ACME_DB",
            "privateKey": "{BASE_64_ENCODED_PRIVATE_KEY}",
            "warehouse": "COMPUTE_WH"
        }
    },
    "connectionSpec": {
        "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
        "version": "1.0"
    }
  }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `auth.params.account` | Der Name Ihres [!DNL Snowflake]. |
| `auth.params.username` | Der Benutzername, der Ihrem [!DNL Snowflake]-Konto zugeordnet ist. |
| `auth.params.database` | Die [!DNL Snowflake] Datenbank, aus der die Daten abgerufen werden. |
| `auth.params.privateKey` | Der [!DNL Base64-] unverschlüsselte private Schlüssel Ihres [!DNL Snowflake]. |
| `auth.params.warehouse` | Das [!DNL Snowflake] Warehouse, das Sie verwenden. |
| `connectionSpec.id` | Die Spezifikations-ID der [!DNL Snowflake]-Verbindung: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

+++

+++Antwort

Eine erfolgreiche Antwort gibt die neu erstellte Verbindung zurück, einschließlich ihrer eindeutigen Verbindungskennung (`id`). Diese ID ist erforderlich, um Ihre Daten im nächsten Tutorial zu untersuchen.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++

>[!ENDTABS]

## Verbinden von [!DNL Snowflake] mit Experience Platform auf Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Dieser Abschnitt gilt für Implementierungen von Experience Platform, die auf Amazon Web Services (AWS) ausgeführt werden. Experience Platform, das auf AWS ausgeführt wird, steht derzeit einer begrenzten Anzahl von Kunden zur Verfügung. Weitere Informationen zur unterstützten Experience Platform-Infrastruktur finden Sie in der Übersicht zur [Experience Platform Multi-Cloud](../../../../../landing/multi-cloud.md).

Lesen Sie die folgenden Schritte, um Informationen zum Verbinden Ihrer [!DNL Snowflake] mit Experience Platform auf AWS zu erhalten.

### Erstellen einer Basisverbindung für [!DNL Snowflake] auf Experience Platform in AWS {#aws-base}

**API-Format**

```http
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Snowflake], um das Datum in Experience Platform auf AWS aufzunehmen:

+++Beispiel auswählen, um es anzuzeigen

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection for Experience Platform on AWS",
      "description": "Snowflake base connection for Experience Platform on AWS",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "acme.snowflakecomputing.com",
              "port": "443",
              "username": "acme-cj123",
              "password": "{PASSWORD}",
              "database": "ACME_DB",
              "warehouse": "COMPUTE_WH",
              "schema": "{SCHEMA}"
          }
      },
      "connectionSpec": {
          "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
          "version": "1.0"
      }
  }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `auth.params.host` | Die Host-URL, mit der sich Ihr [!DNL Snowflake]-Konto verbindet. |
| `auth.params.port` | Die Port-Nummer, die von [!DNL Snowflake] verwendet wird, wenn eine Verbindung zu einem Server über das Internet hergestellt wird. |
| `auth.params.username` | Der Benutzername, der Ihrem [!DNL Snowflake]-Konto zugeordnet ist. |
| `auth.params.database` | Die [!DNL Snowflake] Datenbank, aus der die Daten abgerufen werden. |
| `auth.params.password` | Das mit Ihrem [!DNL Snowflake]-Konto verknüpfte Kennwort. |
| `auth.params.warehouse` | Das [!DNL Snowflake] Warehouse, das Sie verwenden. |
| `auth.params.schema` | Der Name des Schemas, das Ihrer [!DNL Snowflake]-Datenbank zugeordnet ist. Sie müssen sicherstellen, dass der Benutzer, dem Sie Datenbankzugriff gewähren möchten, auch Zugriff auf dieses Schema hat. |

+++

**Antwort**

Eine erfolgreiche Antwort gibt Details der neu erstellten Verbindung zurück, einschließlich ihrer eindeutigen Kennung (`id`). Diese ID ist erforderlich, um Ihren -Speicher im nächsten Tutorial zu untersuchen.

+++Beispiel auswählen, um es anzuzeigen

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700d77b-0000-0200-0000-5e3b41a10000\""
}
```

+++

In diesem Tutorial haben Sie eine [!DNL Snowflake]-Basisverbindung mithilfe der [!DNL Flow Service]-API erstellt. Sie können diese Basisverbindungs-ID in den folgenden Tutorials verwenden:

* [Erkunden von Struktur und Inhalten Ihrer Datentabellen mithilfe der  [!DNL Flow Service] -API](../../explore/tabular.md)
* [Erstellen eines Datenflusses, um Datenbankdaten mithilfe der API  [!DNL Flow Service]  Experience Platform zu übertragen](../../collect/database-nosql.md)
