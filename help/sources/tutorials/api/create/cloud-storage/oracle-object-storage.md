---
keywords: Experience Platform;Startseite;beliebte Themen;Oracle Object Storage;Oracle Object Storage
solution: Experience Platform
title: Erstellen einer Oracle Object Storage Base-Verbindung mithilfe der Flow Service-API
type: Tutorial
description: Erfahren Sie, wie Sie Adobe Experience Platform mithilfe der Flow Service-API mit dem Oracle-Objektspeicher verbinden.
exl-id: a85faa44-7d5a-42a2-9052-af01744e13c9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 31%

---

# Erstellen einer [!DNL Oracle Object Storage]-Basisverbindung mithilfe der [!DNL Flow Service]-API

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL Oracle Object Storage] mithilfe der [[!DNL Flow Service] -API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der [!DNL Flow Service]-API eine Verbindung zu [!DNL Oracle Object Storage] herstellen zu können.

### Sammeln erforderlicher Anmeldedaten

Um [!DNL Flow Service] mit [!DNL Oracle Object Storage] zu verbinden, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| `serviceUrl` | Der für die Authentifizierung erforderliche [!DNL Oracle Object Storage]-Endpunkt. Das Endpunktformat ist: `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | Die [!DNL Oracle Object Storage] Zugriffsschlüssel-ID, die für die Authentifizierung erforderlich ist. |
| `secretKey` | Das [!DNL Oracle Object Storage] Kennwort, das für die Authentifizierung erforderlich ist. |
| `bucketName` | Der zulässige Behältername ist erforderlich, wenn der Benutzer eingeschränkten Zugriff hat. Der Behältername muss zwischen drei und 63 Zeichen lang sein. Er muss entweder mit einem Buchstaben oder einer Zahl beginnen und enden und darf nur Kleinbuchstaben, Zahlen oder Bindestriche (`-`) enthalten. Der Behältername kann nicht wie eine IP-Adresse formatiert werden. |
| `folderPath` | Der Pfad des zulässigen Ordners ist erforderlich, wenn der Benutzer eingeschränkten Zugriff hat. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL Oracle Object Storage] ist: `c85f9425-fb21-426c-ad0b-405e9bd8a46c`. |

Weitere Informationen zum Abrufen dieser Werte finden Sie im [Authentifizierungshandbuch für den Oracle-Objektspeicher](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials).

### Verwenden von Experience Platform-APIs

Informationen zum erfolgreichen Aufrufen von Experience Platform-APIs finden Sie im Handbuch unter [ mit Experience Platform-APIs](../../../../../landing/api-guide.md).

## Erstellen einer Basisverbindung

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Experience Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen ID der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basisverbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den Endpunkt `/connections` und geben Sie dabei Ihre [!DNL Oracle Object Storage]-Authentifizierungs-Anmeldedaten als Teil der Anfrageparameter an.

**API-Format**

```http
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Oracle Object Storage]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Oracle Object Storage connection",
        "description": "Oracle Object Storage connection",
        "auth": {
            "specName": "Access Key",
            "params": {
                "serviceUrl": "{SERVICE_URL}",
                "accessKey": "{ACCESS_KEY}",
                "secretKey": "{SECRET_KEY}",
                "bucketName": "{BUCKET_NAME}",
                "folderPath", "{FOLDER_PATH}"
            }
        },
        "connectionSpec": {
            "id": "c85f9425-fb21-426c-ad0b-405e9bd8a46c",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `auth.params.serviceUrl` | Der für die Authentifizierung erforderliche [!DNL Oracle Object Storage]-Endpunkt. |
| `auth.params.accessKey` | Die [!DNL Oracle Object Storage] Zugriffsschlüssel-ID, die für die Authentifizierung erforderlich ist. |
| `auth.params.secretKey` | Das [!DNL Oracle Object Storage] Kennwort, das für die Authentifizierung erforderlich ist. |
| `auth.params.bucketName` | Der zulässige Behältername ist erforderlich, wenn der Benutzer eingeschränkten Zugriff hat. |
| `auth.params.folderPath` | Der Pfad des zulässigen Ordners ist erforderlich, wenn der Benutzer eingeschränkten Zugriff hat. |
| `connectionSpec.id` | Die [!DNL Oracle Object Storage]-Verbindungsspezifikations-ID: `c85f9425-fb21-426c-ad0b-405e9bd8a46c`. |

**Antwort**

Bei einer erfolgreichen Antwort wird die Verbindungs-ID der neu erstellten Verbindung zurückgegeben. Diese ID ist erforderlich, um Ihre Cloud-Speicherdaten im nächsten Tutorial zu untersuchen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL Oracle Object Storage] mithilfe der [!DNL Flow Service]-API erstellt und ihre eindeutige Verbindungs-ID erhalten. Sie können diese Verbindungs-ID verwenden, um [Cloud-Speicher mithilfe der Flow Service-API zu ](../../explore/cloud-storage.md).
