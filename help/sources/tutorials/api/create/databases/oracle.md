---
title: Verbinden von Oracle DB mit Experience Platform mithilfe der Flow Service-API
description: Erfahren Sie, wie Sie Oracle DB mithilfe von APIs mit Experience Platform verbinden.
exl-id: b1cea714-93ff-425f-8e12-6061da97d094
source-git-commit: aa5496be968ee6f117649a6fff2c9e83a4ed7681
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 5%

---

# Verbinden von [!DNL Oracle DB] mit Experience Platform mithilfe der [!DNL Flow Service]-API

Lesen Sie dieses Handbuch, um zu erfahren, wie Sie Ihr [!DNL Oracle DB]-Konto mithilfe der [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/) mit Adobe Experience Platform verbinden.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der [!DNL Oracle]-API eine Verbindung zu [!DNL Flow Service] herstellen zu können.

### Verwenden von Experience Platform-APIs

Informationen zum erfolgreichen Aufrufen von Experience Platform-APIs finden Sie im Handbuch unter [ mit Experience Platform-APIs](../../../../../landing/api-guide.md).

### Sammeln erforderlicher Anmeldedaten

Informationen zur Authentifizierung [[!DNL Oracle DB]  Sie in ](../../../../connectors/databases/oracle.md#prerequisites)Übersicht“.

## Verbinden von [!DNL Oracle DB] mit Experience Platform auf Azure {#azure}

Lesen Sie die folgenden Schritte, um Informationen zum Verbinden Ihres [!DNL Oracle DB]-Kontos mit Experience Platform auf Azure zu erhalten.

### Erstellen einer Basisverbindung für [!DNL Oracle DB] auf Experience Platform auf Azure {#azure-base}

Eine Basisverbindung verknüpft Ihre Quelle mit Experience Platform und speichert Authentifizierungsdetails, Verbindungsstatus und eine eindeutige ID. Verwenden Sie diese ID, um Quelldateien zu durchsuchen und bestimmte aufzunehmende Elemente zu identifizieren, einschließlich ihrer Datentypen und Formate.

**API-Format**

```https
POST /connections
```

Um eine Basisverbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den `/connections`-Endpunkt und geben Sie Ihre [!DNL Oracle DB] Authentifizierungsdaten als Teil der Anfrageparameter an.

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Oracle DB] unter Verwendung der Authentifizierung über eine Verbindungszeichenfolge.

+++Anfrage anzeigen


```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Oracle DB base connection",
    "description": "A base connection to connect Oracle DB to Experience Platform on Azure",
    "auth": {
      "specName": "ConnectionString",
      "params": {
        "connectionString": "Host={HOST};Port={PORT};Sid={SID};UserId={USERNAME};Password={PASSWORD}"
      }
    },
    "connectionSpec": {
      "id": "d6b52d86-f0f8-475f-89d4-ce54c8527328",
      "version": "1.0"
    }
  }'
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `auth.params.connectionString` | Die Verbindungszeichenfolge, die zum Herstellen einer Verbindung mit [!DNL Oracle DB] verwendet wird. Das [!DNL Oracle DB]-Verbindungszeichenfolgenmuster ist: `Host={HOST};Port={PORT};Sid={SID};User Id={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | Die Spezifikations-ID der [!DNL Oracle]-Verbindung: `d6b52d86-f0f8-475f-89d4-ce54c8527328`. |

+++

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Basisverbindung zurück, einschließlich ihrer eindeutigen Kennung (`id`).

+++Antwort anzeigen

```json
{
    "id": "f088e4f2-2464-480c-88e4-f22464b80c90",
    "etag": "\"43011faa-0000-0200-0000-5ea740cd0000\""
}
```

+++

## Verbinden von [!DNL Oracle DB] mit Experience Platform auf Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Dieser Abschnitt gilt für Implementierungen von Experience Platform, die auf Amazon Web Services (AWS) ausgeführt werden. Experience Platform, das auf AWS ausgeführt wird, steht derzeit einer begrenzten Anzahl von Kunden zur Verfügung. Weitere Informationen zur unterstützten Experience Platform-Infrastruktur finden Sie in der Übersicht zur [Experience Platform Multi-Cloud](../../../../../landing/multi-cloud.md).

Lesen Sie die folgenden Schritte, um Informationen zum Verbinden Ihres [!DNL Oracle DB]-Kontos mit Experience Platform auf AWS zu erhalten.

### Erstellen einer Basisverbindung für [!DNL Oracle DB] auf Experience Platform auf AWS {#aws-base}

**API-Format**

```https
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Oracle DB], um eine Verbindung zu Experience Platform auf AWS herzustellen.

+++Anfrage anzeigen

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Oracle DB on Experience Platform AWS",
      "description": "Oracle DB on Experience Platform AWS",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "diy.us-dawkins-1.oraclecloud.com",
              "port": "1521",
              "database": "mcmg_profits_diy.oraclecloud.com",
              "username": "Admin",
              "password": "xxxx",
              "schema": "ADMIN",
              "sslMode": "true"
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
| `auth.params.server` | Die IP-Adresse oder der Hostname Ihres [!DNL Oracle DB]. |
| `auth.params.port` | Die Port-Nummer Ihres [!DNL Oracle DB]. |
| `auth.params.database` | Der Name der [!DNL Oracle DB]-Instanz, mit der Sie eine Verbindung herstellen. |
| `auth.params.username` | Das mit Ihrer [!DNL Oracle DB] verknüpfte Benutzerkonto. |
| `auth.prams.password` | Das Passwort, das Ihrem [!DNL Oracle DB]-Benutzerkonto entspricht. |
| `auth.params.schema` | Das Schema, das Ihre Datenbankobjekte enthält. |
| `auth.params.sslMode` | Ein boolescher Wert, der angibt, ob SSL-Maßnahmen erzwungen werden oder nicht. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID, die der [!DNL Oracle DB] entspricht. Dieser ID-Wert ist wie folgt festgelegt: `d6b52d86-f0f8-475f-89d4-ce54c8527328.` |

+++

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Basisverbindung zurück, einschließlich ihrer eindeutigen Kennung (`id`) und der entsprechenden. Sie können die ID verwenden, um [Quellverbindung zu erstellen](../../collect/database-nosql.md#create-a-source-connection) und den `etag`, um [Ihr Konto zu aktualisieren](../../update.md).

+++Antwort anzeigen

```json
{
    "id": "f847950c-1c12-4568-a550-d5312b16fdb8",
    "etag": "\"0c0099f4-0000-0200-0000-67da91710000\""
}
```

+++


## Erstellen eines Datenflusses für [!DNL Oracle DB] Daten

Nachdem Sie Ihr [!DNL Oracle DB]-Konto erfolgreich verbunden haben, können Sie jetzt [einen Datenfluss erstellen und Daten aus Ihrer Datenbank in Experience Platform aufnehmen](../../collect/database-nosql.md).