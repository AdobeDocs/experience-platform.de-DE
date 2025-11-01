---
title: Verbinden von Salesforce Marketing Cloud mit Experience Platform mithilfe der Flow Service-API
description: Erfahren Sie, wie Sie Ihr Salesforce Marketing Cloud-Konto mithilfe von APIs mit Experience Platform verbinden.
exl-id: fbf68d3a-f8b1-4618-bd56-160cc6e3346d
source-git-commit: 16cc811a545414021b8686ae303d6112bcf6cebb
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 6%

---

# Verbinden von [!DNL Salesforce Marketing Cloud] mit Experience Platform mithilfe der [!DNL Flow Service]-API

>[!WARNING]
>
>Die [!DNL Salesforce Marketing Cloud] wird im Januar 2026 eingestellt. Eine neue Quelle wird noch in diesem Jahr als Alternative veröffentlicht. Nach der Veröffentlichung der neuen Quelle müssen Sie die Migration zur neuen Quelle planen, indem Sie neue Kontoverbindungen und Datenflüsse vor Ende Januar 2026 erstellen.

Lesen Sie dieses Handbuch, um zu erfahren, wie Sie Ihr [!DNL Salesforce Marketing Cloud]-Konto mithilfe der [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/) mit Adobe Experience Platform verbinden.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der [!DNL Azure Synapse Analytics]-API eine Verbindung zu [!DNL Flow Service] herstellen zu können.


### Verwenden von Experience Platform-APIs

Informationen zum erfolgreichen Aufrufen von Experience Platform-APIs finden Sie im Handbuch unter [ mit Experience Platform-APIs](../../../../../landing/api-guide.md).

Der folgende Abschnitt enthält zusätzliche Informationen, die Sie benötigen, um sich mithilfe der [!DNL Salesforce Marketing Cloud]-API erfolgreich mit [!DNL Flow Service] verbinden zu können.

### Sammeln erforderlicher Anmeldedaten

Informationen zur Authentifizierung [[!DNL Salesforce Marketing Cloud]  Sie in ](../../../../connectors/marketing-automation/salesforce-marketing-cloud.md)Authentifizierungsübersicht“.

### Verwenden von Experience Platform-APIs

Lesen Sie das Handbuch [Erste Schritte mit Experience Platform-APIs](../../../../../landing/api-guide.md) um Informationen darüber zu erhalten, wie Sie Experience Platform-APIs erfolgreich aufrufen können.

## Verbinden von [!DNL Salesforce Marketing Cloud] mit Experience Platform auf [!DNL Azure]

Lesen Sie das Folgende, um zu erfahren, wie Sie eine Basisverbindung erstellen und Ihr [!DNL Salesforce Marketing Cloud]-Konto mit Experience Platform on [!DNL Azure] verbinden.

### Erstellen einer Basisverbindung {#azure-base}

>[!IMPORTANT]
>
>Die Aufnahme benutzerdefinierter Objekte wird von der [!DNL Salesforce Marketing Cloud] derzeit nicht unterstützt.

Eine **Basisverbindung** speichert wichtige Informationen, die Ihr Quellsystem mit Adobe Experience Platform verknüpfen. Dazu gehören:

* Authentifizierungsdaten Ihrer Quelle
* Der aktuelle Status der Verbindung
* Eine eindeutige **Basisverbindungs-ID**

Mit **Basisverbindungs-ID** können Sie Dateien aus Ihrer Quelle durchsuchen und untersuchen, um zu ermitteln, welche Elemente zusammen mit ihren Datentypen und Formaten aufgenommen werden sollen.

Um eine Basisverbindungs-ID zu erstellen, senden Sie eine POST-Anfrage an den `/connections`-Endpunkt, einschließlich Ihrer [!DNL Salesforce Marketing Cloud] Authentifizierungsdaten in den Anfrageparametern.

**API-Format**

```https
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Salesforce Marketing Cloud].

+++Beispielanfrage anzeigen

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Salesforce Marketing Cloud base connection for Azure",
    "description": "Salesforce Marketing Cloud base connection for Azure",
    "auth": {
      "specName": "Client-Id-Secret Based Authentication",
      "params": {
        "host": "acme-ab12c3d4e5fg6hijk7lmnop8qrst",
        "clientId": "acme-salesforce-marketing-cloud",
        "clientSecret": "xxxx"
      }
    },
    "connectionSpec": {
      "id": "ea1c2a08-b722-11eb-8529-0242ac130003",
      "version": "1.0"
    }
  }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `auth.params.host` |  |
| `auth.params.clientId` | Die mit Ihrem [!DNL Salesforce Marketing Cloud] Programm verknüpfte Client-ID. |
| `auth.params.clientSecret` | Das mit Ihrer [!DNL Salesforce Marketing Cloud]-Anwendung verknüpfte Client-Geheimnis. |
| `connectionSpec.id` | Die Spezifikations-ID der [!DNL Salesforce Marketing Cloud]-Verbindung: `ea1c2a08-b722-11eb-8529-0242ac130003`. |

+++

+++Beispielantwort anzeigen

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Basisverbindung zurück, einschließlich ihrer eindeutigen Kennung (`id`).

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++

## Verbinden von [!DNL Salesforce Marketing Cloud] mit Experience Platform auf Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Dieser Abschnitt gilt für Implementierungen von Experience Platform, die auf Amazon Web Services (AWS) ausgeführt werden. Experience Platform, das auf AWS ausgeführt wird, steht derzeit einer begrenzten Anzahl von Kunden zur Verfügung. Weitere Informationen zur unterstützten Experience Platform-Infrastruktur finden Sie in der Übersicht zur [Experience Platform Multi-Cloud](../../../../../landing/multi-cloud.md).

Lesen Sie die folgenden Schritte, um Informationen zum Verbinden Ihres [!DNL Salesforce Marketing Cloud]-Kontos mit Experience Platform auf AWS zu erhalten.

### Erstellen einer Basisverbindung {#aws-base}

**API-Format**

```https
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Salesforce Service Cloud], um eine Verbindung zu Experience Platform auf AWS herzustellen.

+++Beispiel für eine Anfrage anzeigen

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Salesforce Marketing Cloud base connection for AWS",
    "description": "Salesforce Marketing Cloud base connection for AWS",
    "auth": {
      "specName": "OAuth2 Client Credential",
      "params": {
        "subdomain": "mc563885gzs27c5t9-63k636ttgm",
        "clientId": "3a1b2c3d4e5f67890123456789abcdef",
        "clientSecret": "xxxx"
      }
    },
    "connectionSpec": {
      "id": "ea1c2a08-b722-11eb-8529-0242ac130003",
      "version": "1.0"
    }
  }'
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Basisverbindung zurück, einschließlich ihrer eindeutigen Kennung (`id`).

+++Beispiel für eine Anfrageantwort

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++


## Erstellen eines Datenflusses für [!DNL Salesforce Marketing Cloud] Daten

Nachdem Sie Ihr [!DNL Salesforce Marketing Cloud]-Konto erfolgreich verbunden haben, können Sie jetzt [einen Datenfluss erstellen und Daten von Ihrem Marketing-Automatisierungsanbieter in Experience Platform ](../../collect/marketing-automation.md).