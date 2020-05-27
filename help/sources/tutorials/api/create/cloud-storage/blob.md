---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Azurblauch-Connectors mit der Flow Service API
topic: overview
translation-type: tm+mt
source-git-commit: 0a2247a9267d4da481b3f3a5dfddf45d49016e61
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 1%

---


# Erstellen eines Azurblauch-Connectors mit der Flow Service API

Mit dem Flow-Dienst werden Kundendaten aus verschiedenen Quellen innerhalb der Adobe Experience Platform erfasst und zentralisiert. Der Dienst stellt eine Benutzeroberfläche und eine RESTful-API bereit, über die alle unterstützten Quellen verbunden werden können.

In diesem Lernprogramm wird die Flow Service API verwendet, um Sie durch die Schritte zu führen, die notwendig sind, um Experience Platform mit einer Azurblase-Datenspeicherung (im Folgenden &quot;Blob&quot; genannt) zu verbinden.

Wenn Sie lieber die Benutzeroberfläche in Experience Platform verwenden möchten, finden Sie im [Amazon S3-Quellschnittstellen-Lernprogramm](../../../ui/create/cloud-storage/blob-s3.md) schrittweise Anleitungen zum Ausführen ähnlicher Aktionen.

## Erste Schritte

Dieses Handbuch erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

* [Quellen](../../../../home.md): Mit Experience Platform können Daten aus verschiedenen Quellen erfasst werden, während Sie gleichzeitig die Möglichkeit haben, eingehende Daten mithilfe von Plattformdiensten zu strukturieren, zu beschriften und zu verbessern.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Plattforminstanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der Flow Service API eine Verbindung zu einer Blob-Datenspeicherung herstellen zu können.

### Erforderliche Berechtigungen erfassen

Damit der Flow-Dienst eine Verbindung zu Ihrer Blob-Datenspeicherung herstellen kann, müssen Sie Werte für die folgende Verbindungseigenschaft angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `connectionString` | Die Verbindungszeichenfolge, die für den Zugriff auf Daten in Ihrer Blob-Datenspeicherung erforderlich ist. Das Muster für die Zeichenfolge der Blob-Verbindung lautet: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |
| `connectionSpec.id` | Die eindeutige Kennung, die zum Erstellen einer Verbindung erforderlich ist. Die Verbindungs-Spezifikations-ID für Blob lautet: `4c10e202-c428-4796-9208-5f1f5732b1cf` |

Weitere Informationen zum Abrufen einer Verbindungszeichenfolge finden Sie im [folgenden Dokument](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string):

### Lesen von Beispiel-API-Aufrufen

In diesem Lernprogramm finden Sie Beispiele für API-Aufrufe, die zeigen, wie Sie Ihre Anforderungen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anforderungs-Nutzdaten. Beispiel-JSON, die in API-Antworten zurückgegeben wird, wird ebenfalls bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für Experience Platform.

### Werte für erforderliche Kopfzeilen sammeln

Um Aufrufe an Plattform-APIs durchzuführen, müssen Sie zunächst das [Authentifizierungstraining](../../../../../tutorials/authentication.md)abschließen. Das Abschließen des Authentifizierungstreutorials stellt die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform API-Aufrufen bereit, wie unten dargestellt:

* Genehmigung: Träger `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in Experience Platform, einschließlich der Ressourcen des Flow-Dienstes, werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an Plattform-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird:

* x-sandbox-name: `{SANDBOX_NAME}`

Für alle Anforderungen, die eine Payload enthalten (POST, PUT, PATCH), ist ein zusätzlicher Medientyp-Header erforderlich:

* Content-Type: `application/json`

## Verbindung herstellen

Eine Verbindung gibt eine Quelle an und enthält Ihre Anmeldeinformationen für diese Quelle. Pro Blob-Konto ist nur eine Verbindung erforderlich, da sie zum Erstellen mehrerer Quell-Connectors verwendet werden kann, um verschiedene Daten einzubringen.

**API-Format**

```http
POST /connections
```

**Anfrage**

Um eine Blob-Verbindung zu erstellen, muss die eindeutige Verbindungs-ID als Teil der POST-Anforderung angegeben werden. Die Verbindungsspezifikations-ID für Blob ist `4c10e202-c428-4796-9208-5f1f5732b1cf`.

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Blob Connection",
        "description": "Cnnection for an Azure Blob account",
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

## Nächste Schritte

In diesem Lernprogramm haben Sie eine Blob-Verbindung mit APIs erstellt und eine eindeutige ID als Teil des Antwortkörpers erhalten. Sie können diese Verbindungs-ID verwenden, um Cloud-Datenspeicherung mithilfe der Flow Service API [zu](../../explore/cloud-storage.md) untersuchen oder Parkettdaten mithilfe der Flow Service API [zu erfassen](../../cloud-storage-parquet.md).