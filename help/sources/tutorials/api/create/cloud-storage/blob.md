---
keywords: Experience Platform;Startseite;beliebte Themen;Azure;Azure Blob;Blob;Blob
solution: Experience Platform
title: Erstellen einer Azure Blob-Basisverbindung mit der Flow Service-API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie mit der Flow Service-API eine Verbindung zwischen Adobe Experience Platform und Azure Blob herstellen.
exl-id: 4ab8033f-697a-49b6-8d9c-1aadfef04a04
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 8%

---

# Erstellen einer [!DNL Azure Blob]-Basisverbindung mithilfe der [!DNL Flow Service]-API

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL Azure Blob] (nachfolgend &quot;a1/>&quot;genannt) mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).[!DNL Blob]

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von Platform-Diensten zu strukturieren, zu beschriften und zu erweitern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Anwendungen für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der [!DNL Flow Service]-API erfolgreich eine [!DNL Blob]-Quellverbindung erstellen zu können.

### Erforderliche Anmeldedaten sammeln

Damit [!DNL Flow Service] eine Verbindung zu Ihrem [!DNL Blob]-Speicher herstellen kann, müssen Sie Werte für die folgende Verbindungseigenschaft angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `connectionString` | Eine Zeichenfolge, die die Autorisierungsinformationen enthält, die zum Authentifizieren von [!DNL Blob] für die Experience Platform erforderlich sind. Das Verbindungszeichenfolgenmuster [!DNL Blob] lautet: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Weitere Informationen zu Verbindungszeichenfolgen finden Sie in diesem [!DNL Blob] Dokument zu [Konfigurieren von Verbindungszeichenfolgen](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |
| `sasUri` | Der URI für die gemeinsame Zugriffssignatur, den Sie als alternativen Authentifizierungstyp verwenden können, um Ihr [!DNL Blob]-Konto zu verbinden. Das SAS-URI-Muster [!DNL Blob] lautet: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Weitere Informationen finden Sie in diesem [!DNL Blob] Dokument unter [URIs für freigegebene Zugriffssignaturen](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL Blob] lautet: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

### Verwenden von Platform-APIs

Informationen dazu, wie Sie erfolgreich Aufrufe an Platform-APIs durchführen können, finden Sie im Handbuch [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Basisverbindung erstellen

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basis-Verbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den Endpunkt `/connections` und geben Sie dabei Ihre [!DNL Blob]-Authentifizierungsdaten als Teil der Anfrageparameter an.

### Erstellen Sie eine Basisverbindung [!DNL Blob] mithilfe der auf einer Verbindungszeichenfolge basierenden Authentifizierung.

Um eine Basisverbindung [!DNL Blob] mit einer auf einer Verbindungszeichenfolge basierenden Authentifizierung zu erstellen, stellen Sie eine POST-Anfrage an die [!DNL Flow Service]-API und geben Sie dabei Ihre [!DNL Blob] `connectionString` an.

**API-Format**

```http
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Blob] mithilfe der Verbindungszeichenfolgen-basierten Authentifizierung:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Blob connection using connectionString",
        "description": "Azure Blob connection using connectionString",
        "auth": {
            "specName": "ConnectionString",
            "params": {
                "connectionString": "DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}"
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

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Basisverbindung zurück, einschließlich der eindeutigen Kennung (`id`). Diese ID ist im nächsten Schritt erforderlich, um eine Quellverbindung zu erstellen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

### Erstellen einer Basisverbindung [!DNL Blob] mithilfe des URI für die gemeinsame Zugriffssignatur

Eine freigegebene Zugriffssignatur (SAS)-URI ermöglicht eine sichere delegierte Autorisierung für Ihr [!DNL Blob]-Konto. Sie können SAS verwenden, um Authentifizierungsberechtigungen mit unterschiedlichem Zugriffsgrad zu erstellen, da eine SAS-basierte Authentifizierung es Ihnen ermöglicht, Berechtigungen, Start- und Ablaufdaten sowie Bestimmungen für bestimmte Ressourcen festzulegen.

Um eine Blob-Verbindung mit dem Namen [!DNL Blob] mithilfe des URI für die gemeinsame Zugriffssignatur zu erstellen, stellen Sie eine POST-Anfrage an die [!DNL Flow Service]-API und geben Sie dabei Werte für [!DNL Blob] `sasUri` an.

**API-Format**

```http
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Blob] mithilfe des URI für die Freigegebene Zugriffssignatur:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Blob source connection using SAS URI",
        "description": "Azure Blob source connection using SAS URI",
        "auth": {
            "specName": "SasURIAuthentication",
            "params": {
                "sasUri": "https://{ACCOUNT_NAME}.blob.core.windows.net/?sv={STORAGE_VERSION}&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>"
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
| `auth.params.connectionString` | Der SAS-URI, der für den Zugriff auf Daten in Ihrem [!DNL Blob]-Speicher erforderlich ist. Das SAS-URI-Muster [!DNL Blob] lautet: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>`. |
| `connectionSpec.id` | Die Kennung der Speicherverbindungsspezifikation [!DNL Blob] lautet: `4c10e202-c428-4796-9208-5f1f5732b1cf` |

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Basisverbindung zurück, einschließlich der eindeutigen Kennung (`id`). Diese ID ist im nächsten Schritt erforderlich, um eine Quellverbindung zu erstellen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL Blob]-Verbindung mit APIs erstellt und eine eindeutige ID als Teil des Antworttextes erhalten. Sie können diese Verbindungs-ID verwenden, um [Cloud-Speicher mithilfe der Flow Service-API](../../explore/cloud-storage.md) oder [Ermitteln von Parquet-Daten mithilfe der Flow Service-API](../../cloud-storage-parquet.md) zu untersuchen.
