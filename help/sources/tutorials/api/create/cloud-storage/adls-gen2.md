---
keywords: Experience Platform; home; beliebte Themen; Azure Data Lake Storage Gen2; Azure Data Lake Storage; Azure
solution: Experience Platform
title: Erstellen einer Azure Data Lake Storage Gen2-Basisverbindung mithilfe der Flow Service-API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie Adobe Experience Platform mit Azure Data Lake Storage Gen2 über die Flow Service-API verbinden.
exl-id: cad5e2a0-e27c-4130-9ad8-888352c92f04
source-git-commit: 59a8e2aa86508e53f181ac796f7c03f9fcd76158
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 7%

---

# Erstellen einer [!DNL Azure Data Lake Storage Gen2]-Basisverbindung mithilfe der [!DNL Flow Service]-API

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL Azure Data Lake Storage Gen2] (im Folgenden &quot;ADLS Gen2&quot; genannt) mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md):  [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von  [!DNL Platform] Diensten zu strukturieren, zu beschriften und zu erweitern.
* [Sandboxes](../../../../../sandboxes/home.md):  [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen aufteilen, um die Entwicklung und Weiterentwicklung von Programmen für digitale Erlebnisse zu erleichtern.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um eine ADLS Gen2-Quellverbindung mit der [!DNL Flow Service]-API erfolgreich erstellen zu können.

### Erforderliche Anmeldedaten sammeln

Damit [!DNL Flow Service] eine Verbindung zu ADLS Gen2 herstellen kann, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `url` | Der Endpunkt für ADLS Gen2. Das Endpunktmuster lautet: `https://<accountname>.dfs.core.windows.net`. |
| `servicePrincipalId` | Die Client-ID der Anwendung. |
| `servicePrincipalKey` | Der Schlüssel der Anwendung. |
| `tenant` | Die Mandanteninformationen, die Ihre Anwendung enthalten. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für ADLS Gen2 lautet: `0ed90a81-07f4-4586-8190-b40eccef1c5a`. |

Weitere Informationen zu diesen Werten finden Sie in [diesem ADLS Gen2-Dokument](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage).

### Verwenden von Platform-APIs

Informationen dazu, wie Sie erfolgreich Aufrufe an Platform-APIs durchführen können, finden Sie im Handbuch [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Basisverbindung erstellen

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basis-Verbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den Endpunkt `/connections` und geben Sie dabei Ihre ADLS Gen2-Authentifizierungsdaten als Teil der Anfrageparameter an.

**API-Format**

```http
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für ADLS Gen2:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "adls-gen2",
        "description": "Connection for adls-gen2",
        "auth": {
            "specName": "Basic Authentication for adls-gen2",
            "params": {
                "url": "{URL}",
                "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}",
                "tenant": "{TENANT}"
            }
        },
        "connectionSpec": {
            "id": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `auth.params.url` | Der URL-Endpunkt für Ihr ADLS Gen2-Konto. |
| `auth.params.servicePrincipalId` | Die Dienstprinzipal-ID Ihres ADLS Gen2-Kontos. |
| `auth.params.servicePrincipalKey` | Der Service-Prinzipallschlüssel Ihres ADLS Gen2-Kontos. |
| `auth.params.tenant` | Die Mandanteninformationen Ihres ADLS Gen2-Kontos. |
| `connectionSpec.id` | Die ADLS Gen2-Verbindungsspezifikations-ID: `0ed90a81-07f4-4586-8190-b40eccef1c5a1`. |

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Basisverbindung zurück, einschließlich der eindeutigen Kennung (`id`). Diese ID ist im nächsten Schritt erforderlich, um eine Quellverbindung zu erstellen.

```json
{
    "id": "7497ad71-6d32-4973-97ad-716d32797304",
    "etag": "\"23005f80-0000-0200-0000-5e1d00a20000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie mithilfe von APIs eine ADLS Gen2-Verbindung erstellt und als Teil des Antworttexts wurde eine eindeutige ID abgerufen. Sie können diese Verbindungs-ID verwenden, um [Cloud-Speicher mithilfe der Flow Service-API](../../explore/cloud-storage.md) oder [Ermitteln von Parquet-Daten mithilfe der Flow Service-API](../../cloud-storage-parquet.md) zu untersuchen.
