---
title: Verbinden von Azure Blob Storage mit Experience Platform mithilfe der Flow Service-API
description: Erfahren Sie, wie Sie Adobe Experience Platform mithilfe der Flow Service-API mit Azure Blob verbinden.
exl-id: 4ab8033f-697a-49b6-8d9c-1aadfef04a04
source-git-commit: 8e932a25026bef2b785cfddfb8b668b1dd47eb0d
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 9%

---

# Verbinden von [!DNL Azure Blob Storage] mit Experience Platform mithilfe der API

Lesen Sie dieses Handbuch, um zu erfahren, wie Sie Ihr [!DNL Azure Blobg Storage]-Konto mithilfe der [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/) mit Adobe Experience Platform verbinden.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

### Verwenden von Experience Platform-APIs

Informationen zum erfolgreichen Aufrufen von Experience Platform-APIs finden Sie im Handbuch unter [&#x200B; mit Experience Platform-APIs](../../../../../landing/api-guide.md).

### Sammeln erforderlicher Anmeldedaten

Informationen zur Authentifizierung [[!DNL Azure Blob Storage]  Sie in &#x200B;](../../../../connectors/cloud-storage/blob.md#authentication)Übersicht“.

## Verbinden Ihres [!DNL Azure Blob Storage] mit Experience Platform {#connect}

Lesen Sie die folgenden Schritte, um Informationen zum Verbinden Ihres [!DNL Azure Blob Storage]-Kontos mit Experience Platform zu erhalten.

### Erstellen einer Basisverbindung

>[!NOTE]
>
>Nach der Erstellung können Sie den Authentifizierungstyp einer [!DNL Azure Blob Storage] Basisverbindung nicht mehr ändern. Um den Authentifizierungstyp zu ändern, müssen Sie eine neue Basisverbindung erstellen.

Eine Basisverbindung verknüpft Ihre Quelle mit Experience Platform und speichert Authentifizierungsdetails, Verbindungsstatus und eine eindeutige ID. Verwenden Sie diese ID, um Quelldateien zu durchsuchen und bestimmte aufzunehmende Elemente zu identifizieren, einschließlich ihrer Datentypen und Formate.

Sie können Ihr [!DNL Azure Blob Storage]-Konto mit Experience Platform verbinden, indem Sie die folgenden Authentifizierungstypen verwenden:

* **Kontoschlüsselauthentifizierung**: Verwendet den Zugriffsschlüssel des Speicherkontos zur Authentifizierung und Verbindung mit Ihrem [!DNL Azure Blob Storage].
* **Shared Access Signature (SAS)**: Verwendet einen SAS-URI, um delegierten, zeitlich begrenzten Zugriff auf Ressourcen in Ihrem [!DNL Azure Blob Storage]-Konto bereitzustellen.
* **Service-Prinzipal-basierte Authentifizierung**: Verwendet einen Azure Active Directory (AAD)-Service-Prinzipal (Client-ID und Geheimnis) zur sicheren Authentifizierung bei Ihrem Azure Blob Storage-Konto.

**API-Format**

```https
POST /connections
```

Um eine Basisverbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den `/connections`-Endpunkt und geben Sie Ihre Authentifizierungsberechtigungsdaten als Teil der Anfrageparameter an.

>[!BEGINTABS]

>[!TAB Authentifizierung mit Kontoschlüssel]

Um die Authentifizierung mit dem Kontoschlüssel zu verwenden, geben Sie Werte für Ihre `connectionString`, `container` und `folderPath` an.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Azure Blob Storage connection using connectingString",
    "description": "Azure Blob Storage connection using connectionString",
    "auth": {
      "specName": "ConnectionString",
      "params": {
        "connectionString": "DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}",
        "container": "acme-blob-container",
        "folderPath": "/acme/customers/salesData"
      }
    },
    "connectionSpec": {
      "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
      "version": "1.0"
    }
  }'
```

| Parameter | Beschreibung |
| --- | --- |
| `connectionString` | Die Verbindungszeichenfolge für Ihr [!DNL Azure Blob Storage]. Das Muster der Verbindungszeichenfolge ist: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY};EndpointSuffix=core.windows.net`. |
| `container` | Der Name des [!DNL Azure Blob Storage]-Containers, in dem Ihre Datendateien gespeichert werden. |
| `folderPath` | Der Pfad innerhalb des angegebenen Containers, in dem sich Ihre Dateien befinden. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID der [!DNL Azure Blob Storage]. Diese ID lautet: `4c10e202-c428-4796-9208-5f1f5732b1cf`. |

>[!TAB Shared Access Signature]

Um die Shared Access-Signatur zu verwenden, geben Sie Werte für Ihre `sasUri`, `container` und `folderPath` an.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Azure Blob Storage source connection using SAS URI",
    "description": "Azure Blob Storage source connection using SAS URI",
    "auth": {
      "specName": "SAS URI Authentication",
      "params": {
        "sasUri": "https://{ACCOUNT_NAME}.blob.core.windows.net/?sv={STORAGE_VERSION}&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>",
        "container": "acme-blob-container",
        "folderPath": "/acme/customers/salesData"
      }
    },
    "connectionSpec": {
      "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
      "version": "1.0"
    }
  }'
```

| Parameter | Beschreibung |
| --- | --- |
| `sasUri` | Der Signatur-URI für den gemeinsamen Zugriff, den Sie als alternativen Authentifizierungstyp zum Verbinden Ihres Kontos verwenden können. Das SAS-URI-Muster lautet: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv={STORAGE_VERSION}&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}`. |
| `container` | Der Name des [!DNL Azure Blob Storage]-Containers, in dem Ihre Datendateien gespeichert werden. |
| `folderPath` | Der Pfad innerhalb des angegebenen Containers, in dem sich Ihre Dateien befinden. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID der [!DNL Azure Blob Storage]. Diese ID lautet: `4c10e202-c428-4796-9208-5f1f5732b1cf`. |

>[!TAB Auf Service-Prinzipalen basierende Authentifizierung]

Um die Verbindung über eine auf Service-Prinzipalen basierende Authentifizierung herzustellen, geben Sie Werte für Folgendes an: `serviceEndpoint`, `servicePrincipalId`, `servicePrincipalKey`, `accountKind`, `tenant`, `container` und `folderPath`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Azure Blob Storage source connection using service principal based authentication",
    "description": "Azure Blob Storage source connection using service principal based authentication",
    "auth": {
      "specName": "Service Principal Based Authentication",
      "params": {
        "serviceEndpoint": "{SERVICE_ENDPOINT}",
        "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
        "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}",
        "accountKind": "{ACCOUNT_KIND}",
        "tenant": "{TENANT}",
        "container": "acme-blob-container",
        "folderPath": "/acme/customers/salesData"
      }
    },
    "connectionSpec": {
      "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
      "version": "1.0"
    }
  }'
```

| Parameter | Beschreibung |
| --- | --- |
| `serviceEndpoint` | Die Endpunkt-URL Ihres [!DNL Azure Blob Storage]. Normalerweise im Format: `https://{ACCOUNT_NAME}.blob.core.windows.net`. |
| `servicePrincipalId` | Die Client-/Anwendungs-ID des für die Authentifizierung verwendeten Azure Active Directory (AAD)-Service-Prinzipals. |
| `servicePrincipalKey` | Das mit dem Azure-Service-Prinzipal verknüpfte Client-Geheimnis oder Kennwort. |
| `accountKind` | Der Typ Ihres [!DNL Azure Blob Storage]. Häufige Werte sind `Storage` (Allgemeiner Zweck V1), `StorageV2` (Allgemeiner Zweck V2), `BlobStorage` und `BlockBlobStorage`. |
| `tenant` | Die Azure Active Directory (AAD)-Mandanten-ID, in der der Service-Prinzipal registriert ist. |
| `container` | Der Name des [!DNL Azure Blob Storage]-Containers, in dem Ihre Datendateien gespeichert werden. |
| `folderPath` | Der Pfad innerhalb des angegebenen Containers, in dem sich Ihre Dateien befinden. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID der [!DNL Azure Blob Storage]. Diese ID lautet: `4c10e202-c428-4796-9208-5f1f5732b1cf`. |

>[!ENDTABS]

Bei einer erfolgreichen Antwort werden Details zu der neu erstellten Basisverbindung zurückgegeben, einschließlich ihrer eindeutigen Kennung (`id`). Diese ID ist im nächsten Schritt erforderlich, um eine Quellverbindung zu erstellen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```



## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL Blob] mithilfe von APIs erstellt und eine eindeutige ID als Teil der Antwort erhalten. Sie können diese Verbindungs-ID verwenden, um [Cloud-Speicher mithilfe der Flow Service-API zu &#x200B;](../../explore/cloud-storage.md).
