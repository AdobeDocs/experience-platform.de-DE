---
keywords: Experience Platform;Home;beliebte Themen;Azurblüte;Blob;Blob;Blob
solution: Experience Platform
title: Erstellen einer Blase-Quellverbindung mit der Flow-Dienst-API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie Adobe Experience Platform mit der Flow Service API mit Azurblase verbinden.
exl-id: 4ab8033f-697a-49b6-8d9c-1aadfef04a04
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 26%

---

# Erstellen einer [!DNL Azure Blob]-Quellverbindung mit der [!DNL Flow Service]-API

Dieses Lernprogramm verwendet die [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml), um Sie durch die Schritte zur Verbindung von [!DNL Azure Blob] (nachfolgend &quot;Blob&quot; genannt) mit Adobe Experience Platform zu führen.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von Plattformdiensten zu strukturieren, zu kennzeichnen und zu verbessern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Anwendungen für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mit der [!DNL Flow Service]-API eine [!DNL Blob]-Quellverbindung erfolgreich zu erstellen.

### Erforderliche Anmeldedaten sammeln

Damit [!DNL Flow Service] eine Verbindung zu Ihrer [!DNL Blob]-Datenspeicherung herstellen kann, müssen Sie Werte für die folgende Verbindungseigenschaft angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `connectionString` | Eine Zeichenfolge, die die Autorisierungsinformationen enthält, die zum Authentifizieren von [!DNL Blob] für die Experience Platform erforderlich sind. Das Verbindungszeichenfolgen-Muster [!DNL Blob] lautet: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Weitere Informationen zu Verbindungszeichenfolgen finden Sie in diesem [!DNL Blob]-Dokument unter [Konfigurieren von Verbindungszeichenfolgen](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |
| `sasUri` | Der URI für die Unterschrift für den gemeinsamen Zugriff, den Sie als alternativen Authentifizierungstyp verwenden können, um Ihr [!DNL Blob]-Konto zu verbinden. Das SAS-URI-Muster ist: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Weitere Informationen finden Sie in diesem [!DNL Blob] Dokument unter [URIs für freigegebene Zugriffssignaturen](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication).[!DNL Blob] |
| `connectionSpec.id` | Die eindeutige Kennung, die zum Erstellen einer Verbindung erforderlich ist. Die Verbindungs-Spezifikations-ID für [!DNL Blob] lautet: `4c10e202-c428-4796-9208-5f1f5732b1cf` |

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für Experience Platform.

### Sammeln von Werten für erforderliche Kopfzeilen

Um Platform-APIs aufrufen zu können, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://www.adobe.com/go/platform-api-authentication-en) abschließen. Im Rahmen des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alle Ressourcen in Experience Platform, einschließlich der Ressourcen von [!DNL Flow Service], werden zu bestimmten virtuellen Sandboxen isoliert. Bei allen Anfragen an Platform-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

* `x-sandbox-name: {SANDBOX_NAME}`

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

* `Content-Type: application/json`

## Verbindung erstellen

Eine Verbindung gibt eine Quelle an und enthält Ihre Anmeldeinformationen für diese Quelle. Pro [!DNL Blob]-Konto ist nur eine Verbindung erforderlich, da sie zum Erstellen mehrerer Datenflüsse verwendet werden kann, um verschiedene Daten einzubringen.

### Eine [!DNL Blob]-Verbindung mit einer auf einer Verbindungszeichenfolge basierenden Authentifizierung erstellen

Um eine [!DNL Blob]-Verbindung mit einer auf einer Verbindungszeichenfolge basierenden Authentifizierung zu erstellen, fordern Sie eine POST an die [!DNL Flow Service]-API an, während Sie [!DNL Blob] `connectionString` angeben.

**API-Format**

```http
POST /connections
```

**Anfrage**

Um eine [!DNL Blob]-POST zu erstellen, muss die eindeutige Verbindungs-ID als Teil der Verbindungsanforderung angegeben werden. Die Verbindungs-Spezifikations-ID für [!DNL Blob] ist `4c10e202-c428-4796-9208-5f1f5732b1cf`.

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
| `auth.params.connectionString` | Die Verbindungszeichenfolge, die für den Zugriff auf Daten in Ihrer Blob-Datenspeicherung erforderlich ist. Das Muster für die Zeichenfolge der Blob-Verbindung lautet: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |
| `connectionSpec.id` | Die Verbindungs-ID der Blob-Datenspeicherung lautet: `4c10e202-c428-4796-9208-5f1f5732b1cf` |

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Verbindung zurück, einschließlich der eindeutigen Kennung (`id`). Diese ID ist erforderlich, um Ihre Datenspeicherung im nächsten Lernprogramm zu untersuchen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

### Eine [!DNL Blob]-Verbindung mit einer URI für eine freigegebene Zugriffssignatur erstellen

Eine SAS-URI (shared access signature) ermöglicht eine sichere delegierte Autorisierung für Ihr [!DNL Blob]-Konto. Sie können SAS verwenden, um Authentifizierungsberechtigungen mit unterschiedlichem Zugriffsgrad zu erstellen, da eine SAS-basierte Authentifizierung Ihnen das Festlegen von Berechtigungen, Beginns- und Ablaufdaten sowie von Bestimmungen für bestimmte Ressourcen ermöglicht.

Um eine [!DNL Blob]-Verbindung mit dem URI für die freigegebene Zugriffssignatur zu erstellen, fordern Sie eine POST an die [!DNL Flow Service]-API an, während Sie Werte für [!DNL Blob] `sasUri` angeben.

**API-Format**

```http
POST /connections
```

**Anfrage**

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
| `auth.params.connectionString` | Der SAS-URI, der für den Zugriff auf Daten in Ihrer [!DNL Blob]-Datenspeicherung erforderlich ist. Das SAS-URI-Muster ist: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>`.[!DNL Blob] |
| `connectionSpec.id` | Die Verbindungs-ID der Datenspeicherung [!DNL Blob] lautet: `4c10e202-c428-4796-9208-5f1f5732b1cf` |

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Verbindung zurück, einschließlich der eindeutigen Kennung (`id`). Diese ID ist erforderlich, um Ihre Datenspeicherung im nächsten Lernprogramm zu untersuchen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

## Nächste Schritte

In diesem Lernprogramm haben Sie eine [!DNL Blob]-Verbindung mit APIs erstellt und eine eindeutige ID als Teil des Antwortkörpers erhalten. Sie können diese Verbindungs-ID verwenden, um Cloud-Datenspeicherung mithilfe der Flow Service API](../../explore/cloud-storage.md) oder [zu erfassen. Verwenden Sie dazu die Flussdienst-API](../../cloud-storage-parquet.md).[
