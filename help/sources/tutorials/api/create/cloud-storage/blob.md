---
keywords: Experience Platform;home;beliebte Themen;Azure;azure blob;Blob;Blob
solution: Experience Platform
title: Erstellen einer Azure Blob Base Connection mithilfe der Flow Service API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie Adobe Experience Platform mithilfe der Flow Service API mit Azure Blob verbinden.
exl-id: 4ab8033f-697a-49b6-8d9c-1aadfef04a04
source-git-commit: 13bd1254dfe89004465174a7532b4f6aaef54c09
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 9%

---

# Erstellen Sie eine [!DNL Azure Blob] Basisverbindung mit [!DNL Flow Service] API

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL Azure Blob] (nachstehend &quot;nachstehend &quot;nachstehend&quot; genannt[!DNL Blob]&quot;) unter Verwendung der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von Plattformdiensten zu strukturieren, zu kennzeichnen und zu verbessern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Anwendungen für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um erfolgreich eine [!DNL Blob] Quellverbindung mit [!DNL Flow Service] API.

### Erforderliche Anmeldedaten sammeln

In der Reihenfolge [!DNL Flow Service] zur Verbindung mit [!DNL Blob] Datenspeicherung, müssen Sie Werte für die folgende Verbindungseigenschaft angeben:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| `connectionString` | Eine Zeichenfolge, die die für die Authentifizierung erforderlichen Autorisierungsinformationen enthält [!DNL Blob] in die Experience Platform. Die [!DNL Blob] Verbindungszeichenfolgemuster ist: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Weitere Informationen zu Verbindungszeichenfolgen finden Sie in diesem [!DNL Blob] Dokument ein [Verbindungszeichenfolgen konfigurieren](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |
| `sasUri` | Der URI für die Unterschrift für den gemeinsamen Zugriff, den Sie als alternativen Authentifizierungstyp verwenden können, um Ihre [!DNL Blob] Konto. Die [!DNL Blob] SAS-URI-Muster ist: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Weitere Informationen finden Sie in diesem [!DNL Blob] Dokument ein [Freigabesignatur-URIs](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Verbindungseigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für das Erstellen der Basis- und Quellverbindungen. Verbindungsspezifikations-ID für [!DNL Blob] ist: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

### Verwenden von Plattform-APIs

Informationen dazu, wie Sie erfolgreich Aufrufe von Plattform-APIs durchführen, finden Sie im Handbuch zu [Erste Schritte mit Plattform-APIs](../../../../../landing/api-guide.md).

## Basisverbindung erstellen

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Plattform gespeichert, einschließlich der Authentifizierungsinformationen Ihrer Quelle, des aktuellen Zustands der Verbindung und Ihrer eindeutigen Basis-Verbindungs-ID. Die Basis-Verbindungs-ID ermöglicht es Ihnen, Dateien von der Quelle aus zu erkunden und zu navigieren und die spezifischen Elemente zu identifizieren, die Sie aufnehmen möchten, einschließlich Informationen zu den Datentypen und Formaten.

Um eine Basis-Verbindungs-ID zu erstellen, stellen Sie eine POST an `/connections` Endpunkt beim Bereitstellen von [!DNL Blob] Authentifizierungsdaten als Teil der Anforderungsparameter.

### Erstellen Sie eine [!DNL Blob] Basisverbindung mit einer verbindungszeichenbasierten Authentifizierung

So erstellen Sie [!DNL Blob] Basisverbindung mit einer auf Verbindungszeichenfolgen basierenden Authentifizierung erstellen Sie eine POST an die [!DNL Flow Service] API während der Bereitstellung [!DNL Blob] `connectionString`.

**API-Format**

```http
POST /connections
```

**Anfrage**

Die folgende Anforderung erstellt eine Basisverbindung für [!DNL Blob] mit einer auf Verbindungszeichenfolgen basierenden Authentifizierung:

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
| `auth.params.connectionString` | Die Verbindungszeichenfolge, die für den Zugriff auf Daten in der Blob-Datenspeicherung erforderlich ist. Das Muster der Blob-Verbindungszeichenfolge lautet: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |
| `connectionSpec.id` | Die Verbindungs-ID der Blob Datenspeicherung lautet: `4c10e202-c428-4796-9208-5f1f5732b1cf` |

**Antwort**

Eine erfolgreiche Antwort gibt Details der neu erstellten Basisverbindung einschließlich ihrer eindeutigen Kennung (`id`). Diese ID ist im nächsten Schritt zum Erstellen einer Quellverbindung erforderlich.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

### Erstellen Sie eine [!DNL Blob] Basisverbindung mit freigegebener Zugriffssignatur-URI

Eine SAS-URI (Shared Access Signature) ermöglicht eine sichere delegierte Autorisierung für Ihre [!DNL Blob] Konto. Sie können SAS verwenden, um Authentifizierungsdaten mit unterschiedlichem Zugriffsgrad zu erstellen, da eine SAS-basierte Authentifizierung Ihnen die Möglichkeit bietet, Berechtigungen, Beginns- und Ablaufdaten sowie Bestimmungen für bestimmte Ressourcen festzulegen.

So erstellen Sie [!DNL Blob] BLOB-Verbindung mit einer freigegebenen Zugriffssignatur-URI, stellen Sie eine POST an [!DNL Flow Service] API bei Angabe von Werten für [!DNL Blob] `sasUri`.

**API-Format**

```http
POST /connections
```

**Anfrage**

Die folgende Anforderung erstellt eine Basisverbindung für [!DNL Blob] Verwenden der URI für freigegebene Zugriffssignatur:

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
| `auth.params.connectionString` | Der SAS-URI, der für den Zugriff auf Daten in Ihrer [!DNL Blob] Datenspeicherung. Die [!DNL Blob] SAS-URI-Muster ist: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>`. |
| `connectionSpec.id` | Die [!DNL Blob] Spezifikations-ID der Datenspeicherung: `4c10e202-c428-4796-9208-5f1f5732b1cf` |

**Antwort**

Eine erfolgreiche Antwort gibt Details der neu erstellten Basisverbindung einschließlich ihrer eindeutigen Kennung (`id`). Diese ID ist im nächsten Schritt zum Erstellen einer Quellverbindung erforderlich.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

## Nächste Schritte

Durch Befolgen dieses Tutorials haben Sie eine [!DNL Blob] Verbindung mit APIs und eine eindeutige ID wurde als Teil des Antwortkörpers ermittelt. Sie können diese Verbindungs-ID verwenden, um [Cloud-Datenspeicherung mithilfe der Flow Service API erkunden](../../explore/cloud-storage.md).
