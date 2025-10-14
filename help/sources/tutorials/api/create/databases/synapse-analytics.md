---
title: Verbinden von Azure Synapse Analytics mit Experience Platform mithilfe der Flow Service-API
description: Erfahren Sie, wie Sie Ihr Azure Synapse Analytics-Konto mithilfe von APIs mit Experience Platform verbinden.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 8944ac3f-366d-49c8-882f-11cd0ea766e4
source-git-commit: b8497ede7f90717ed23bcd10b7abe51de18e08a5
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 15%

---

# Verbinden von [!DNL Azure Synapse Analytics] mit Experience Platform mithilfe der [!DNL Flow Service]-API

>[!IMPORTANT]
>
>Die [!DNL Azure Synapse Analytics] ist im Quellkatalog für Benutzende verfügbar, die Real-Time Customer Data Platform Ultimate erworben haben.

Lesen Sie dieses Handbuch, um zu erfahren, wie Sie Ihr [!DNL Azure Synapse Analytics]-Konto mithilfe der [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/) mit Adobe Experience Platform verbinden.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der [!DNL Flow Service]-API eine Verbindung zu [!DNL Azure Synapse Analytics] herstellen zu können.

### Sammeln erforderlicher Anmeldedaten

Informationen zur Authentifizierung [[!DNL Azure Synapse Analytics]  Sie in &#x200B;](../../../../connectors/databases/synapse-analytics.md#prerequisites)Übersicht“.

### Verwenden von Experience Platform-APIs

Informationen zum erfolgreichen Aufrufen von Experience Platform-APIs finden Sie im Handbuch unter [&#x200B; mit Experience Platform-APIs](../../../../../landing/api-guide.md).

## Verbinden von [!DNL Azure Synapse Analytics] mit Experience Platform

Im Folgenden erfahren Sie, wie Sie eine Basisverbindung erstellen und Ihr [!DNL Azure Synapse Analytics]-Konto mit Experience Platform verbinden.

### Erstellen einer Basisverbindung

Eine **Basisverbindung** speichert wichtige Informationen, die Ihr Quellsystem mit Adobe Experience Platform verknüpfen. Dazu gehören:

* Authentifizierungsdaten Ihrer Quelle
* Der aktuelle Status der Verbindung
* Eine eindeutige **Basisverbindungs-ID**

Mit **Basisverbindungs-ID** können Sie Dateien aus Ihrer Quelle durchsuchen und untersuchen, um zu ermitteln, welche Elemente zusammen mit ihren Datentypen und Formaten aufgenommen werden sollen.

Um eine Basisverbindungs-ID zu erstellen, senden Sie eine POST-Anfrage an den `/connections`-Endpunkt, einschließlich Ihrer [!DNL Azure Synapse Analytics] Authentifizierungsdaten in den Anfrageparametern.

**API-Format**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB Auf Verbindungszeichenfolgen basierende Authentifizierung]

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Azure Synapse Analytics] unter Verwendung der Authentifizierung über eine Verbindungszeichenfolge.

+++Beispielanfrage anzeigen

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Connection for Azure Synapse Analytics",
      "description": "Connection for Azure Synapse Analytics",
      "auth": {
          "specName": "Connection String Based Authentication",
          "params": {
              "connectionString": "Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
          }
      },
      "connectionSpec": {
          "id": "a49bcc7d-8038-43af-b1e4-5a7a089a7d79",
          "version": "1.0"
      }
  }'
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `auth.params.connectionString` | Die Verbindungszeichenfolge, die zum Herstellen einer Verbindung mit [!DNL Azure Synapse Analytics] verwendet wird. Das [!DNL Azure Synapse Analytics]-Verbindungszeichenfolgenmuster ist `Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30`. |
| `connectionSpec.id` | Die Spezifikations-ID der [!DNL Azure Synapse Analytics]-Verbindung lautet: `a49bcc7d-8038-43af-b1e4-5a7a089a7d79`. |

+++

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Basisverbindung zurück, einschließlich ihrer eindeutigen Kennung (`id`).

+++Beispielantwort anzeigen

```json
{
    "id": "6bc13a3b-3546-455f-813a-3b3546a55fb1",
    "etag": "\"3500866c-0000-0200-0000-5e83afa30000\""
}
```

+++

>[!TAB Schlüsselbasierte Authentifizierung für Service-Prinzipal]

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Azure Synapse Analytics] mit einer Authentifizierung, die auf dem Service-Prinzipal-Schlüssel basiert.

**Anfrage**

+++Beispielanfrage anzeigen

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Connection for Azure Synapse Analytics",
    "description": "Connection for Azure Synapse Analytics",
    "auth": {
      "specName": "Service Principal Key Based Authentication",
      "params": {
        "server": "yourworkspace.sql.azuresynapse.net",
        "database": "SalesDW",
        "tenant": "72f988bf-86f1-41af-91ab-2d7cd011db47",
        "servicePrincipalId": "e7b8c1f2-1234-4c9a-9f3e-abcdef123456",
        "servicePrincipalKey": "~XyZ1234abcDEF5678..."
      }
    },
    "connectionSpec": {
      "id": "a49bcc7d-8038-43af-b1e4-5a7a089a7d79",
      "version": "1.0"
    }
  }'
```

| Anmeldedaten | Beschreibung |
| --- | --- |
| `auth.params.server` | Der vollständig qualifizierte Domain-Name Ihres [!DNL Azure Synapse Analytics] SQL-Endpunkts. |
| `auth.params.database` | Der Name der spezifischen Datenbank in Ihrem [!DNL Azure Synapse Analytics] Workspace. |
| `auth.params.tenant` | Die mit Ihrem [!DNL Azure]-Abonnement verknüpfte [!DNL Azure Active Directory]-Mandanten-ID. |
| `auth.params.servicePrincipalId` | Die Client-ID einer [!DNL Azure Active Directory]. |
| `auth.params.servicePrincipalKey` | Das mit dem Service-Prinzipal verknüpfte Client-Geheimnis oder Kennwort. |
| `connectSpec.id` | Die Verbindungsspezifikations-ID von [!DNL Azure Synapse Analytics]. |

+++

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Basisverbindung zurück, einschließlich ihrer eindeutigen Kennung (`id`).

+++Beispielantwort anzeigen

```json
{
    "id": "6bc13a3b-3546-455f-813a-3b3546a55fb1",
    "etag": "\"3500866c-0000-0200-0000-5e83afa30000\""
}
```

+++

>[!ENDTABS]

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL Azure Synapse Analytics]-Basisverbindung mithilfe der [!DNL Flow Service]-API erstellt. Sie können diese Basisverbindungs-ID in den folgenden Tutorials verwenden:

* [Erkunden von Struktur und Inhalten Ihrer Datentabellen mithilfe der  [!DNL Flow Service] -API](../../explore/tabular.md)
* [Erstellen eines Datenflusses, um Datenbankdaten mithilfe der API  [!DNL Flow Service]  Experience Platform zu übertragen](../../collect/database-nosql.md)
