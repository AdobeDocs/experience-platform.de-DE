---
title: Erstellen einer Azure Blob-Basisverbindung mit der Flow Service-API
description: Erfahren Sie, wie Sie mit der Flow Service-API eine Verbindung zwischen Adobe Experience Platform und Azure Blob herstellen.
exl-id: 4ab8033f-697a-49b6-8d9c-1aadfef04a04
source-git-commit: d22c71fb77655c401f4a336e339aaf8b3125d1b6
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 43%

---

# Erstellen einer [!DNL Azure Blob]-Basisverbindung mithilfe der [!DNL Flow Service]-API

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

In diesem Tutorial werden Schritte zum Erstellen einer Basisverbindung für [!DNL Azure Blob] (nachstehend &quot;genannt)[!DNL Blob]&quot;) mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um erfolgreich eine [!DNL Blob] Quellverbindung mithilfe der [!DNL Flow Service] API.

### Sammeln erforderlicher Anmeldeinformationen

Zur [!DNL Flow Service] , um eine Verbindung mit Ihrer [!DNL Blob] Speicher, müssen Sie Werte für die folgende Verbindungseigenschaft angeben:

>[!BEGINTABS]

>[!TAB Authentifizierung von Verbindungszeichenfolgen]

| Anmeldedaten | Beschreibung |
| --- | --- |
| `connectionString` | Eine Zeichenfolge, die die für die Authentifizierung erforderlichen Autorisierungsinformationen enthält [!DNL Blob] auf Experience Platform. Die [!DNL Blob] Verbindungszeichenfolgenmuster ist: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Weitere Informationen zu Verbindungszeichenfolgen finden Sie in diesem [!DNL Blob] Dokument auf [Konfigurieren von Verbindungszeichenfolgen](https://docs.microsoft.com/de-de/azure/storage/common/storage-configure-connection-string). |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL Blob] ist: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

>[!TAB SAS-URI-Authentifizierung]

| Anmeldedaten | Beschreibung |
| --- | --- |
| `sasUri` | Der URI für die gemeinsame Zugriffssignatur, den Sie als alternativen Authentifizierungstyp verwenden können, um Ihre [!DNL Blob] -Konto. Die [!DNL Blob] Das SAS-URI-Muster lautet: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Weitere Informationen finden Sie in diesem [!DNL Blob] Dokument auf [URIs für freigegebene Zugriffssignatur](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |
| `container` | Der Name des Containers, für den Sie Zugriff festlegen möchten. Beim Erstellen eines neuen Kontos mit dem [!DNL Blob] -Quelle können Sie einen Containernamen bereitstellen, um den Benutzerzugriff auf den Unterordner Ihrer Wahl anzugeben. |
| `folderPath` | Der Pfad zu dem Ordner, auf den Sie Zugriff gewähren möchten. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL Blob] ist: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

>[!ENDTABS]

### Verwenden von Platform-APIs

Informationen zum Aufrufen von Platform-APIs finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Erstellen einer Basisverbindung

>[!TIP]
>
>Nach der Erstellung können Sie den Authentifizierungstyp eines [!DNL Blob] Basisverbindung. Um den Authentifizierungstyp zu ändern, müssen Sie eine neue Basisverbindung erstellen.

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Die [!DNL Blob] -Quelle unterstützt sowohl die Authentifizierung für Verbindungszeichenfolgen als auch für freigegebene Zugriffssignaturen (SAS). Eine SAS-URI (Shared Access Signature) ermöglicht die sichere delegierte Autorisierung Ihrer [!DNL Blob] -Konto. Sie können SAS verwenden, um Authentifizierungsberechtigungen mit unterschiedlichem Zugriffsgrad zu erstellen, da eine SAS-basierte Authentifizierung es Ihnen ermöglicht, Berechtigungen, Start- und Ablaufdaten sowie Bestimmungen für bestimmte Ressourcen festzulegen.

In diesem Schritt können Sie auch die Unterordner angeben, auf die Ihr Konto Zugriff haben soll, indem Sie den Namen des Containers und den Pfad zum Unterordner definieren.

Um eine Basisverbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den `/connections`-Endpunkt beim Bereitstellen der [!DNL Blob]-Authentifizierungsberechtigungsdaten als Teil der Anfrageparameter.

**API-Format**

```http
POST /connections
```

**Anfrage**

>[!BEGINTABS]

>[!TAB Verbindungszeichenfolge]

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Blob] Verwenden der auf einer Verbindungszeichenfolge basierenden Authentifizierung:

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
      "name": "Azure Blob connection using connectionString",
      "description": "Azure Blob connection using connectionString",
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

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `auth.params.connectionString` | Die Verbindungszeichenfolge, die für den Zugriff auf Daten in Ihrem Blob-Speicher erforderlich ist. Das Muster der Blob-Verbindungszeichenfolge lautet: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |
| `connectionSpec.id` | Die Blob Storage-Verbindungsspezifikations-ID lautet: `4c10e202-c428-4796-9208-5f1f5732b1cf` |

+++

+++Antwort

Bei einer erfolgreichen Antwort werden Details zu der neu erstellten Basisverbindung zurückgegeben, einschließlich ihrer eindeutigen Kennung (`id`). Diese ID ist im nächsten Schritt erforderlich, um eine Quellverbindung zu erstellen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

+++

>[!TAB SAS-URI-Authentifizierung]

So erstellen Sie eine [!DNL Blob] Verbindung mithilfe des URI für die freigegebene Zugriffssignatur erstellen, eine POST-Anfrage an die [!DNL Flow Service] API bei der Bereitstellung von Werten für Ihre [!DNL Blob] `sasUri`.

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
      "name": "Azure Blob source connection using SAS URI",
      "description": "Azure Blob source connection using SAS URI",
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

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `auth.params.connectionString` | Der SAS-URI, der für den Zugriff auf Daten in Ihrer [!DNL Blob] Speicher. Die [!DNL Blob] Das SAS-URI-Muster lautet: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>`. |
| `connectionSpec.id` | Die [!DNL Blob] Speicherverbindungsspezifikations-ID lautet: `4c10e202-c428-4796-9208-5f1f5732b1cf` |

+++

+++Antwort

Bei einer erfolgreichen Antwort werden Details zu der neu erstellten Basisverbindung zurückgegeben, einschließlich ihrer eindeutigen Kennung (`id`). Diese ID ist im nächsten Schritt erforderlich, um eine Quellverbindung zu erstellen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

+++

>[!ENDTABS]

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL Blob] Verbindung mithilfe von APIs und eine eindeutige ID als Teil des Antworttexts erhalten. Sie können diese Verbindungs-ID verwenden, um [Erkunden von Cloud-Speichern mithilfe der Flow Service-API](../../explore/cloud-storage.md).
