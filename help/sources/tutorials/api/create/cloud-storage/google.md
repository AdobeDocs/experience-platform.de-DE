---
keywords: Experience Platform;Home;beliebte Themen;Google Cloud-Datenspeicherung;Google Cloud-Datenspeicherung;Google;Google
solution: Experience Platform
title: Google Cloud-Datenspeicherung-Basisverbindung mithilfe der Flow Service-API erstellen
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie Adobe Experience Platform mit einem Google Cloud-Datenspeicherung-Konto über die Flow Service-API verbinden.
exl-id: 321d15eb-82c0-45a7-b257-1096c6db6b18
source-git-commit: 13bd1254dfe89004465174a7532b4f6aaef54c09
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 11%

---

# Erstellen Sie eine [!DNL Google Cloud Storage] Basisverbindung mit [!DNL Flow Service] API

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL Google Cloud Storage] mit [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten zu strukturieren, zu kennzeichnen und zu verbessern, indem Sie [!DNL Platform] Dienstleistungen.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um eine Verbindung mit einem Google Cloud-Datenspeicherung-Konto über die [!DNL Flow Service] API.

### Erforderliche Anmeldedaten sammeln

In der Reihenfolge [!DNL Flow Service] zur Verbindung mit [!DNL Google Cloud Storage] -Konto, müssen Sie Werte für die folgenden Verbindungseigenschaften bereitstellen:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| `accessKeyId` | Eine alphanumerische Zeichenfolge aus 61 Zeichen, die zur Authentifizierung Ihrer [!DNL Google Cloud Storage] Konto auf Plattform. |
| `secretAccessKey` | Eine 40-stellige, Base-64-kodierte Zeichenfolge, die zur Authentifizierung Ihrer [!DNL Google Cloud Storage] Konto auf Plattform. |

Weitere Informationen zu diesen Werten finden Sie im [HMAC-Schlüssel für Google Cloud-Datenspeicherung](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) Leitfaden. Weitere Informationen zum Generieren einer eigenen Zugriffsschlüssel-ID und eines geheimen Zugriffsschlüssels finden Sie in der [[!DNL Google Cloud Storage] Überblick](../../../../connectors/cloud-storage/google-cloud-storage.md).

### Verwenden von Plattform-APIs

Informationen dazu, wie Sie erfolgreich Aufrufe von Plattform-APIs durchführen, finden Sie im Handbuch zu [Erste Schritte mit Plattform-APIs](../../../../../landing/api-guide.md).

## Basisverbindung erstellen

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Plattform gespeichert, einschließlich der Authentifizierungsinformationen Ihrer Quelle, des aktuellen Zustands der Verbindung und Ihrer eindeutigen Basis-Verbindungs-ID. Die Basis-Verbindungs-ID ermöglicht es Ihnen, Dateien von der Quelle aus zu erkunden und zu navigieren und die spezifischen Elemente zu identifizieren, die Sie aufnehmen möchten, einschließlich Informationen zu den Datentypen und Formaten.

Um eine Basis-Verbindungs-ID zu erstellen, stellen Sie eine POST an `/connections` Endpunkt beim Bereitstellen von [!DNL Google Cloud Storage] Authentifizierungsdaten als Teil der Anforderungsparameter.

**API-Format**

```http
POST /connections
```

**Anfrage**

Die folgende Anforderung erstellt eine Basisverbindung für [!DNL Google Cloud Storage]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google Cloud Storage connection",
        "description": "Connector for Google Cloud Storage",
        "auth": {
            "specName": "Basic Authentication for google-cloud",
            "params": {
                "accessKeyId": "accessKeyId",
                "secretAccessKey": "secretAccessKey"
            }
        },
        "connectionSpec": {
            "id": "32e8f412-cdf7-464c-9885-78184cb113fd",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `auth.params.accessKeyId` | Die Ihrer [!DNL Google Cloud Storage] Konto. |
| `auth.params.secretAccessKey` | Der geheime Zugriffsschlüssel, der Ihrem [!DNL Google Cloud Storage] Konto. |
| `connectionSpec.id` | Die [!DNL Google Cloud Storage] Verbindungsspezifikations-ID: `32e8f412-cdf7-464c-9885-78184cb113fd` |

**Antwort**

Eine erfolgreiche Antwort gibt Details der neu erstellten Verbindung zurück, einschließlich ihrer eindeutigen Kennung (`id`). Diese ID ist erforderlich, um Ihre Cloud-Datenspeicherung-Daten im nächsten Tutorial zu untersuchen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Nächste Schritte

Durch Befolgen dieses Tutorials haben Sie eine [!DNL Google Cloud Storage] Verbindung mit APIs und eine eindeutige ID wurde als Teil des Antwortkörpers ermittelt. Sie können diese Verbindungs-ID verwenden, um [Cloud-Datenspeicherung mithilfe der Flow Service API erkunden](../../explore/cloud-storage.md).
