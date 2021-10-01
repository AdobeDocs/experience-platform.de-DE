---
keywords: Experience Platform; Startseite; beliebte Themen; Google Cloud-Speicher; Google Cloud-Speicher; Google; Google
solution: Experience Platform
title: Erstellen einer Google Cloud Storage-Basisverbindung mit der Flow Service-API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Flow Service-API Adobe Experience Platform mit einem Google Cloud Storage-Konto verbinden.
exl-id: 321d15eb-82c0-45a7-b257-1096c6db6b18
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 11%

---

# Erstellen einer [!DNL Google Cloud Storage]-Basisverbindung mithilfe der [!DNL Flow Service]-API

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL Google Cloud Storage] mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md):  [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von  [!DNL Platform] Diensten zu strukturieren, zu beschriften und zu erweitern.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der [!DNL Flow Service]-API erfolgreich eine Verbindung zu einem Google Cloud Storage-Konto herstellen zu können.

### Erforderliche Anmeldedaten sammeln

Damit [!DNL Flow Service] eine Verbindung zu Ihrem [!DNL Google Cloud Storage]-Konto herstellen kann, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `accessKeyId` | Eine alphanumerische Zeichenfolge mit 61 Zeichen, die zur Authentifizierung Ihres [!DNL Google Cloud Storage]-Kontos bei Platform verwendet wird. |
| `secretAccessKey` | Eine base-64-kodierte Zeichenfolge mit 40 Zeichen, die zur Authentifizierung Ihres [!DNL Google Cloud Storage]-Kontos bei Platform verwendet wird. |

Weitere Informationen zu diesen Werten finden Sie im Handbuch [Google Cloud Storage HMAC-Schlüssel](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) . Anweisungen zum Generieren Ihrer eigenen Zugriffsschlüssel-ID und des geheimen Zugriffsschlüssels finden Sie in der [[!DNL Google Cloud Storage] Übersicht](../../../../connectors/cloud-storage/google-cloud-storage.md).

### Verwenden von Platform-APIs

Informationen dazu, wie Sie erfolgreich Aufrufe an Platform-APIs durchführen können, finden Sie im Handbuch [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Basisverbindung erstellen

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basis-Verbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den Endpunkt `/connections` und geben Sie dabei Ihre [!DNL Google Cloud Storage]-Authentifizierungsdaten als Teil der Anfrageparameter an.

**API-Format**

```http
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Google Cloud Storage]:

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
| `auth.params.accessKeyId` | Die Zugriffsschlüssel-ID, die Ihrem [!DNL Google Cloud Storage]-Konto zugeordnet ist. |
| `auth.params.secretAccessKey` | Der geheime Zugriffsschlüssel, der Ihrem [!DNL Google Cloud Storage]-Konto zugeordnet ist. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID [!DNL Google Cloud Storage]: `32e8f412-cdf7-464c-9885-78184cb113fd` |

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Verbindung zurück, einschließlich der eindeutigen Kennung (`id`). Diese ID ist erforderlich, um Ihre Cloud-Speicherdaten im nächsten Tutorial zu untersuchen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL Google Cloud Storage]-Verbindung mit APIs erstellt und eine eindeutige ID als Teil des Antworttextes erhalten. Sie können diese Verbindungs-ID verwenden, um [Cloud-Speicher mithilfe der Flow Service-API](../../explore/cloud-storage.md) oder [Ermitteln von Parquet-Daten mithilfe der Flow Service-API](../../cloud-storage-parquet.md) zu untersuchen.
