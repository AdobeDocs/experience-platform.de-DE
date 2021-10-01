---
keywords: Experience Platform; Homepage; beliebte Themen; Oracle-Objektspeicher; oracle-Objektspeicher
solution: Experience Platform
title: Erstellen einer Oracle-Objektspeicher-Basisverbindung mithilfe der Flow Service-API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie Adobe Experience Platform mithilfe der Flow Service-API mit dem Oracle-Objektspeicher verbinden.
exl-id: a85faa44-7d5a-42a2-9052-af01744e13c9
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 10%

---

# Erstellen einer [!DNL Oracle Object Storage]-Basisverbindung mithilfe der [!DNL Flow Service]-API

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL Oracle Object Storage] mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von Platform-Diensten zu strukturieren, zu beschriften und zu erweitern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Anwendungen für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der [!DNL Flow Service]-API erfolgreich eine Verbindung zu [!DNL Oracle Object Storage] herstellen zu können.

### Erforderliche Anmeldedaten sammeln

Damit [!DNL Flow Service] eine Verbindung zu [!DNL Oracle Object Storage] herstellen kann, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `serviceUrl` | Der für die Authentifizierung erforderliche [!DNL Oracle Object Storage]-Endpunkt. Das Endpunktformat lautet: `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | Die für die Authentifizierung erforderliche Zugriffsschlüssel-ID [!DNL Oracle Object Storage]. |
| `secretKey` | Das für die Authentifizierung erforderliche [!DNL Oracle Object Storage]-Kennwort. |
| `bucketName` | Der zulässige Behältername, der erforderlich ist, wenn der Benutzer eingeschränkten Zugriff hat. Der Behältername muss zwischen drei und 63 Zeichen lang sein. Er muss entweder mit einem Buchstaben oder einer Zahl beginnen und enden und darf nur Kleinbuchstaben, Zahlen oder Bindestriche (`-`) enthalten. Der Behältername kann nicht wie eine IP-Adresse formatiert werden. |
| `folderPath` | Der zulässige Ordnerpfad, der erforderlich ist, wenn der Benutzer eingeschränkten Zugriff hat. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL Oracle Object Storage] lautet: `c85f9425-fb21-426c-ad0b-405e9bd8a46c`. |

Weitere Informationen zum Abrufen dieser Werte finden Sie im [Handbuch zur Authentifizierung bei der Oracle-Objektspeicherung](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials).

### Verwenden von Platform-APIs

Informationen dazu, wie Sie erfolgreich Aufrufe an Platform-APIs durchführen können, finden Sie im Handbuch [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Basisverbindung erstellen

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basis-Verbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den Endpunkt `/connections` und geben Sie dabei Ihre [!DNL Oracle Object Storage]-Authentifizierungsdaten als Teil der Anfrageparameter an.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `auth.params.accessKey` | Die für die Authentifizierung erforderliche Zugriffsschlüssel-ID [!DNL Oracle Object Storage]. |
| `auth.params.secretKey` | Das für die Authentifizierung erforderliche [!DNL Oracle Object Storage]-Kennwort. |
| `auth.params.bucketName` | Der zulässige Behältername, der erforderlich ist, wenn der Benutzer eingeschränkten Zugriff hat. |
| `auth.params.folderPath` | Der zulässige Ordnerpfad, der erforderlich ist, wenn der Benutzer eingeschränkten Zugriff hat. |
| `connectionSpec.id` | Die [!DNL Oracle Object Storage] Verbindungsspezifikations-ID: `c85f9425-fb21-426c-ad0b-405e9bd8a46c`. |

**Antwort**

Eine erfolgreiche Antwort gibt die Verbindungs-ID der neu erstellten Verbindung zurück. Diese ID ist erforderlich, um Ihre Cloud-Speicherdaten im nächsten Tutorial zu untersuchen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL Oracle Object Storage]-Verbindung mit der [!DNL Flow Service]-API erstellt und die eindeutige Verbindungs-ID erhalten. Sie können diese Verbindungs-ID verwenden, um [Cloud-Speicher mithilfe der Flow Service-API](../../explore/cloud-storage.md) zu untersuchen.
