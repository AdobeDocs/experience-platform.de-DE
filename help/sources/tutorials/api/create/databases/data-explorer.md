---
keywords: Experience Platform; Startseite; beliebte Themen; Azure Azure Data Explorer; Azure Data Explorer; Azure Data Explorer
solution: Experience Platform
title: Erstellen einer Azure Azure Data Explorer-Basisverbindung mit der Flow Service-API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie mit der Flow Service-API Azure Data Explorer mit Adobe Experience Platform verbinden.
exl-id: 1b17bbb0-1f7b-4d89-a158-ad269e6edf30
source-git-commit: 5fb5f0ce8bd03ba037c6901305ba17f8939eb9ce
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 10%

---

# Erstellen einer [!DNL Azure Azure Data Explorer]-Basisverbindung mithilfe der [!DNL Flow Service]-API

>[!NOTE]
>
>Der Connector [!DNL Azure Azure Data Explorer] befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectoren finden Sie unter [Quellen - Übersicht](../../../../home.md#terms-and-conditions) .

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL Azure Data Explore] mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).


## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md):  [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von  [!DNL Platform] Diensten zu strukturieren, zu beschriften und zu erweitern.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der [!DNL Flow Service]-API erfolgreich eine Verbindung zu [!DNL Azure Data Explorer] herstellen zu können.

### Erforderliche Anmeldedaten sammeln

Damit [!DNL Flow Service] eine Verbindung mit [!DNL Azure Data Explorer] herstellen kann, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `endpoint` | Der Endpunkt des [!DNL Azure Data Explorer]-Servers. |
| `database` | Der Name der [!DNL Azure Data Explorer]-Datenbank. |
| `tenant` | Die eindeutige Mandantenkennung, die für die Verbindung mit der [!DNL Azure Data Explorer]-Datenbank verwendet wird. |
| `servicePrincipalId` | Die eindeutige Dienstprinzipal-ID, die für die Verbindung mit der [!DNL Azure Data Explorer]-Datenbank verwendet wird. |
| `servicePrincipalKey` | Der eindeutige Dienstprinzipalschlüssel, der für die Verbindung mit der [!DNL Azure Data Explorer]-Datenbank verwendet wird. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL Azure Data Explorer] ist `0479cc14-7651-4354-b233-7480606c2ac3`. |

Weitere Informationen zu den ersten Schritten finden Sie in diesem [[!DNL Azure Data Explorer] Dokument](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad).

### Verwenden von Platform-APIs

Informationen dazu, wie Sie erfolgreich Aufrufe an Platform-APIs durchführen können, finden Sie im Handbuch [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Basisverbindung erstellen

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basis-Verbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den Endpunkt `/connections` und geben Sie dabei Ihre [!DNL Azure Data Explorer]-Authentifizierungsdaten als Teil der Anfrageparameter an.

**API-Format**

```https
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Azure Data Explorer]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Azure Data Explorer connection",
        "description": "A connection for Azure Azure Data Explorer",
        "auth": {
            "specName": "Service Principal Based Authentication",
            "params": {
                    "endpoint": "{ENDPOINT}",
                    "database": "{DATABASE}",
                    "tenant": "{TENANT}",
                    "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                    "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}"
                }
        },
        "connectionSpec": {
            "id": "0479cc14-7651-4354-b233-7480606c2ac3",
            "version": "1.0"
        }
    }'
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `auth.params.endpoint` | Der Endpunkt des [!DNL Azure Data Explorer]-Servers. |
| `auth.params.database` | Der Name der [!DNL Azure Data Explorer]-Datenbank. |
| `auth.params.tenant` | Die eindeutige Mandantenkennung, die für die Verbindung mit der [!DNL Azure Data Explorer]-Datenbank verwendet wird. |
| `auth.params.servicePrincipalId` | Die eindeutige Dienstprinzipal-ID, die für die Verbindung mit der [!DNL Azure Data Explorer]-Datenbank verwendet wird. |
| `auth.params.servicePrincipalKey` | Der eindeutige Dienstprinzipalschlüssel, der für die Verbindung mit der [!DNL Azure Data Explorer]-Datenbank verwendet wird. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID [!DNL Azure Data Explorer]: `0479cc14-7651-4354-b233-7480606c2ac3`. |

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Verbindung zurück, einschließlich der eindeutigen Kennung (`id`). Diese ID ist erforderlich, um Ihre Daten im nächsten Tutorial zu untersuchen.

```json
{
    "id": "f088e4f2-2464-480c-88e4-f22464b80c90",
    "etag": "\"43011faa-0000-0200-0000-5ea740cd0000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL Azure Data Explorer]-Verbindung mit der [!DNL Flow Service]-API erstellt und den eindeutigen ID-Wert der Verbindung erhalten. Sie können diese ID im nächsten Tutorial verwenden, während Sie lernen, wie Sie [Datenbanken mithilfe der Flow Service-API](../../explore/database-nosql.md) analysieren können.
