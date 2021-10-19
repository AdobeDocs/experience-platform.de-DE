---
keywords: Experience Platform;home;beliebte Themen;Azure Data Lake Datenspeicherung Gen2;azure data lake Datenspeicherung;Azure Data
solution: Experience Platform
title: Erstellen einer Azure Data Lake Datenspeicherung Gen2 Base Connection mithilfe der Flow Service API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie Adobe Experience Platform mit Azure Data Lake Datenspeicherung Gen2 über die Flow Service API verbinden.
exl-id: cad5e2a0-e27c-4130-9ad8-888352c92f04
source-git-commit: 13bd1254dfe89004465174a7532b4f6aaef54c09
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 6%

---

# Erstellen Sie eine [!DNL Azure Data Lake Storage Gen2] Basisverbindung mit [!DNL Flow Service] API

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL Azure Data Lake Storage Gen2] (nachstehend &quot;ADLS Gen2&quot; genannt) unter Verwendung der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten zu strukturieren, zu kennzeichnen und zu verbessern, indem Sie [!DNL Platform] Dienstleistungen.
* [Sandboxen](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxen, die eine einzelne Plattforminstanz in separate virtuelle Umgebung aufteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

In den folgenden Abschnitten finden Sie weitere Informationen, die Sie benötigen, um eine ADLS Gen2-Quellverbindung erfolgreich zu erstellen, indem Sie die [!DNL Flow Service] API.

### Erforderliche Anmeldedaten sammeln

In der Reihenfolge [!DNL Flow Service] Um eine Verbindung zu ADLS Gen2 herzustellen, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| `url` | Der Endpunkt für ADLS Gen2. Das Endpunktmuster ist: `https://<accountname>.dfs.core.windows.net`. |
| `servicePrincipalId` | Die Client-ID der Anwendung. |
| `servicePrincipalKey` | Der Schlüssel der Anwendung. |
| `tenant` | Die Mandanteninformationen, die Ihre Anwendung enthalten. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Verbindungseigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für das Erstellen der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für ADLS Gen2 lautet: `0ed90a81-07f4-4586-8190-b40eccef1c5a`. |

Weitere Informationen zu diesen Werten finden Sie unter [dieses ADLS Gen2-Dokument](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage).

### Verwenden von Plattform-APIs

Informationen dazu, wie Sie erfolgreich Aufrufe von Plattform-APIs durchführen, finden Sie im Handbuch zu [Erste Schritte mit Plattform-APIs](../../../../../landing/api-guide.md).

## Basisverbindung erstellen

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Plattform gespeichert, einschließlich der Authentifizierungsinformationen Ihrer Quelle, des aktuellen Zustands der Verbindung und Ihrer eindeutigen Basis-Verbindungs-ID. Die Basis-Verbindungs-ID ermöglicht es Ihnen, Dateien von der Quelle aus zu erkunden und zu navigieren und die spezifischen Elemente zu identifizieren, die Sie aufnehmen möchten, einschließlich Informationen zu den Datentypen und Formaten.

Um eine Basis-Verbindungs-ID zu erstellen, stellen Sie eine POST an `/connections` endpoint bei der Angabe Ihrer ADLS Gen2-Authentifizierungsdaten als Teil der Anforderungsparameter.

**API-Format**

```http
POST /connections
```

**Anfrage**

Mit der folgenden Anforderung wird eine Basisverbindung für ADLS Gen2 erstellt:

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
| `auth.params.servicePrincipalId` | Die Service-Prinzipal-ID Ihres ADLS Gen2-Kontos. |
| `auth.params.servicePrincipalKey` | Der Hauptschlüssel Ihres ADLS Gen2-Kontos. |
| `auth.params.tenant` | Die Mietinformationen Ihres ADLS Gen2-Kontos. |
| `connectionSpec.id` | Die ADLS Gen2-Verbindungsspezifikations-ID: `0ed90a81-07f4-4586-8190-b40eccef1c5a1`. |

**Antwort**

Eine erfolgreiche Antwort gibt Details der neu erstellten Basisverbindung einschließlich ihrer eindeutigen Kennung (`id`). Diese ID ist im nächsten Schritt zum Erstellen einer Quellverbindung erforderlich.

```json
{
    "id": "7497ad71-6d32-4973-97ad-716d32797304",
    "etag": "\"23005f80-0000-0200-0000-5e1d00a20000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine ADLS Gen2-Verbindung mithilfe von APIs erstellt und eine eindeutige ID als Teil des Antwortkörpers erhalten. Sie können diese Verbindungs-ID verwenden, um [Cloud-Datenspeicherung mithilfe der Flow Service API erkunden](../../explore/cloud-storage.md).
