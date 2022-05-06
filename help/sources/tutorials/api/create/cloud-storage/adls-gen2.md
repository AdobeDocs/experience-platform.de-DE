---
keywords: Experience Platform; home; beliebte Themen; Azure Data Lake Storage Gen2; Azure Data Lake Storage; Azure
solution: Experience Platform
title: Erstellen einer Azure Data Lake Storage Gen2-Basisverbindung mithilfe der Flow Service-API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie Adobe Experience Platform mit Azure Data Lake Storage Gen2 über die Flow Service-API verbinden.
exl-id: cad5e2a0-e27c-4130-9ad8-888352c92f04
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 40%

---

# Erstellen Sie eine [!DNL Azure Data Lake Storage Gen2] Basisverbindung mit [!DNL Flow Service] API

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL Azure Data Lake Storage Gen2] (nachstehend &quot;ADLS Gen2&quot; genannt) unter Verwendung der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen aufteilen, um die Entwicklung und Weiterentwicklung von Programmen für digitale Erlebnisse zu erleichtern.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um erfolgreich eine ADLS Gen2-Quellverbindung mit dem [!DNL Flow Service] API.

### Sammeln erforderlicher Anmeldeinformationen

Zur [!DNL Flow Service] Um eine Verbindung zu ADLS Gen2 herzustellen, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| `url` | Der Endpunkt für ADLS Gen2. Das Endpunktmuster lautet: `https://<accountname>.dfs.core.windows.net`. |
| `servicePrincipalId` | Die Client-ID der Anwendung. |
| `servicePrincipalKey` | Der Schlüssel der Anwendung. |
| `tenant` | Die Mandanteninformationen, die Ihre Anwendung enthalten. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für ADLS Gen2 lautet: `b3ba5556-48be-44b7-8b85-ff2b69b46dc4`. |

Weitere Informationen zu diesen Werten finden Sie unter [Dieses ADLS Gen2-Dokument](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage).

### Verwenden von Platform-APIs

Informationen zum Aufrufen von Platform-APIs finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Erstellen einer Basisverbindung

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basis-Verbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an die `/connections` -Endpunkt bei der Bereitstellung Ihrer ADLS Gen2-Authentifizierungsdaten als Teil der Anfrageparameter.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
            "id": "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
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
| `connectionSpec.id` | Die ADLS Gen2-Verbindungsspezifikations-ID: `b3ba5556-48be-44b7-8b85-ff2b69b46dc41`. |

**Antwort**

Bei einer erfolgreichen Antwort werden Details zu der neu erstellten Basisverbindung zurückgegeben, einschließlich ihrer eindeutigen Kennung (`id`). Diese ID ist im nächsten Schritt erforderlich, um eine Quellverbindung zu erstellen.

```json
{
    "id": "7497ad71-6d32-4973-97ad-716d32797304",
    "etag": "\"23005f80-0000-0200-0000-5e1d00a20000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie mithilfe von APIs eine ADLS Gen2-Verbindung erstellt und als Teil des Antworttexts wurde eine eindeutige ID abgerufen. Sie können diese Verbindungs-ID verwenden, um [Erkunden von Cloud-Speichern mithilfe der Flow Service-API](../../explore/cloud-storage.md).
