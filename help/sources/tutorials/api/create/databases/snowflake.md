---
title: Erstellen einer Snowflake-Basisverbindung mit der Flow Service-API
description: Erfahren Sie, wie Sie mit der Flow Service-API eine Verbindung zwischen Adobe Experience Platform und Snowflake herstellen.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 0ef34d30-7b4c-43f5-8e2e-cde05da05aa5
source-git-commit: 4de2193a45fc2925af310b5e2475eabe26d13adc
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 25%

---

# Erstellen einer [!DNL Snowflake]-Basisverbindung mithilfe der [!DNL Flow Service]-API

>[!IMPORTANT]
>
>Die [!DNL Snowflake] -Quelle ist im Quellkatalog für Benutzer verfügbar, die Real-time Customer Data Platform Ultimate erworben haben.

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Verwenden Sie das folgende Tutorial, um zu erfahren, wie Sie eine Basisverbindung für [!DNL Snowflake] mithilfe der [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Verwenden von Platform-APIs

Informationen darüber, wie Sie Platform-APIs erfolgreich aufrufen können, finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

Im folgenden Abschnitt finden Sie weitere Informationen, die Sie benötigen, um eine erfolgreiche Verbindung zu [!DNL Snowflake] mithilfe der [!DNL Flow Service] API.

### Sammeln erforderlicher Anmeldeinformationen

Sie müssen Werte für die folgenden Berechtigungseigenschaften angeben, um Ihre [!DNL Snowflake] -Quelle.

>[!BEGINTABS]

>[!TAB Kontoschlüsselauthentifizierung]

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| `account` | Ein Kontoname identifiziert ein Konto in Ihrer Organisation eindeutig. In diesem Fall müssen Sie ein Konto eindeutig über verschiedene [!DNL Snowflake] Organisationen. Dazu müssen Sie dem Kontonamen den Namen Ihres Unternehmens voranstellen. Beispiel: `orgname-account_name`. Weitere Informationen zu den Kontonamen finden Sie im Abschnitt [!DNL Snowflake] Dokumentation zu [Kontokennung](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `warehouse` | Die [!DNL Snowflake] Warehouse verwaltet den Prozess der Ausführung der Abfrage für die Anwendung. Jeder [!DNL Snowflake] Warehouse ist unabhängig voneinander und muss einzeln aufgerufen werden, wenn Daten an Platform übermittelt werden. |
| `database` | Die [!DNL Snowflake] -Datenbank enthält die Daten, die Sie an Platform übermitteln möchten. |
| `username` | Der Benutzername für die [!DNL Snowflake] -Konto. |
| `password` | Das Kennwort für die [!DNL Snowflake] Benutzerkonto. |
| `role` | Die standardmäßige Zugriffssteuerungsrolle, die in der [!DNL Snowflake] Sitzung. Die Rolle sollte eine bestehende sein, die dem angegebenen Benutzer bereits zugewiesen wurde. Die Standardrolle lautet `PUBLIC`. |
| `connectionString` | Die Verbindungszeichenfolge, über die die Verbindung zu Ihrem [!DNL Snowflake] -Instanz. Das Verbindungszeichenfolgenmuster für [!DNL Snowflake] is `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |

>[!TAB Authentifizierung mit Schlüsselpaaren]

Um die Schlüsselpaar-Authentifizierung zu verwenden, müssen Sie ein 2048-Bit-RSA-Schlüsselpaar generieren und dann beim Erstellen eines Kontos für Ihre [!DNL Snowflake] -Quelle.

| Anmeldedaten | Beschreibung |
| --- | --- |
| `account` | Ein Kontoname identifiziert ein Konto in Ihrer Organisation eindeutig. In diesem Fall müssen Sie ein Konto eindeutig über verschiedene [!DNL Snowflake] Organisationen. Dazu müssen Sie dem Kontonamen den Namen Ihres Unternehmens voranstellen. Beispiel: `orgname-account_name`. Weitere Informationen zu den Kontonamen finden Sie im Abschnitt [!DNL Snowflake] Dokumentation zu [Kontokennung](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `username` | Der Benutzername Ihres [!DNL Snowflake] -Konto. |
| `privateKey` | Die [!DNL Base64-]kodierter privater Schlüssel Ihres [!DNL Snowflake] -Konto. Sie können entweder verschlüsselte oder unverschlüsselte private Schlüssel generieren. Wenn Sie einen verschlüsselten privaten Schlüssel verwenden, müssen Sie bei der Authentifizierung bei Experience Platform auch eine Passphrase für den privaten Schlüssel angeben. |
| `privateKeyPassphrase` | Die Passphrase des privaten Schlüssels ist eine zusätzliche Sicherheitsebene, die Sie bei der Authentifizierung mit einem verschlüsselten privaten Schlüssel verwenden müssen. Sie müssen die Passphrase nicht bereitstellen, wenn Sie einen unverschlüsselten privaten Schlüssel verwenden. |
| `database` | Die [!DNL Snowflake] -Datenbank, die die Daten enthält, die Sie auf Experience Platform erfassen möchten. |
| `warehouse` | Die [!DNL Snowflake] Warehouse verwaltet den Prozess der Ausführung der Abfrage für die Anwendung. Jeder [!DNL Snowflake] Warehouse ist unabhängig voneinander und muss einzeln aufgerufen werden, wenn Daten an Experience Platform übermittelt werden. |

Weitere Informationen zu diesen Werten finden Sie im Abschnitt [[!DNL Snowflake] Authentifizierungshandbuch für Schlüsselpaare](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

>[!NOTE]
>
>Sie müssen die `PREVENT_UNLOAD_TO_INLINE_URL` Markierung auf `FALSE` , um das Entladen von Daten aus Ihrem [!DNL Snowflake] Datenbank zu Experience Platform.

## Erstellen einer Basisverbindung

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basis-Verbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an die `/connections` Endpunkt beim Bereitstellen [!DNL Snowflake] Authentifizierungsberechtigungen als Teil des Anfragetexts.

**API-Format**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB ConnectionString]

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
| `auth.params.connectionString` | Die Verbindungszeichenfolge, über die die Verbindung zu Ihrem [!DNL Snowflake] -Instanz. Das Verbindungszeichenfolgenmuster für [!DNL Snowflake] is `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`. |
| `connectionSpec.id` | Die [!DNL Snowflake] Verbindungsspezifikations-ID: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

+++

+++Antwort

Eine erfolgreiche Antwort gibt die neu erstellte Verbindung zurück, einschließlich der eindeutigen Verbindungskennung (`id`). Diese ID ist erforderlich, um Ihre Daten im nächsten Tutorial zu untersuchen.

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
| `auth.params.account` | Der Name Ihres [!DNL Snowflake] -Konto. |
| `auth.params.username` | Der mit Ihrer [!DNL Snowflake] -Konto. |
| `auth.params.database` | Die [!DNL Snowflake] Datenbank, aus der die Daten abgerufen werden. |
| `auth.params.privateKey` | Die [!DNL Base64-]verschlüsselter privater Schlüssel Ihres [!DNL Snowflake] -Konto. |
| `auth.params.privateKeyPassphrase` | Die Passphrase, die Ihrem privaten Schlüssel entspricht. |
| `auth.params.warehouse` | Die [!DNL Snowflake] -Warehouse verwenden. |
| `connectionSpec.id` | Die [!DNL Snowflake] Verbindungsspezifikations-ID: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

+++

+++Antwort

Eine erfolgreiche Antwort gibt die neu erstellte Verbindung zurück, einschließlich der eindeutigen Verbindungskennung (`id`). Diese ID ist erforderlich, um Ihre Daten im nächsten Tutorial zu untersuchen.

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
| `auth.params.account` | Der Name Ihres [!DNL Snowflake] -Konto. |
| `auth.params.username` | Der mit Ihrer [!DNL Snowflake] -Konto. |
| `auth.params.database` | Die [!DNL Snowflake] Datenbank, aus der die Daten abgerufen werden. |
| `auth.params.privateKey` | Die [!DNL Base64-]verschlüsselter, unverschlüsselter privater Schlüssel Ihres [!DNL Snowflake] -Konto. |
| `auth.params.warehouse` | Die [!DNL Snowflake] -Warehouse verwenden. |
| `connectionSpec.id` | Die [!DNL Snowflake] Verbindungsspezifikations-ID: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

+++

+++Antwort

Eine erfolgreiche Antwort gibt die neu erstellte Verbindung zurück, einschließlich der eindeutigen Verbindungskennung (`id`). Diese ID ist erforderlich, um Ihre Daten im nächsten Tutorial zu untersuchen.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++

>[!ENDTABS]

In diesem Tutorial haben Sie eine [!DNL Snowflake]-Basisverbindung mithilfe der [!DNL Flow Service]-API erstellt. Sie können diese Basisverbindungs-ID in den folgenden Tutorials verwenden:

* [Erkunden von Struktur und Inhalten Ihrer Datentabellen mithilfe der  [!DNL Flow Service] -API](../../explore/tabular.md)
* [Erstellen Sie einen Datenfluss, um Datenbankdaten mit der [!DNL Flow Service] API](../../collect/database-nosql.md)
