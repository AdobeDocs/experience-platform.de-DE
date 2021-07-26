---
keywords: Experience Platform; home; beliebte Themen; redshift; Redshift; Amazon Redshift; amazon redshift
solution: Experience Platform
title: Erstellen einer Amazon Redshift-Basisverbindung mit der Flow Service-API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie mit der Flow Service-API Adobe Experience Platform mit Amazon Redshift verbinden.
exl-id: 2728ce08-05c9-4dca-af1d-d2d1b266c5d9
source-git-commit: 600b216932a7d19440534c4b190fb2f3766c8785
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 12%

---

# Erstellen einer [!DNL Amazon Redshift]-Basisverbindung mithilfe der [!DNL Flow Service]-API

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL Amazon Redshift] mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md):  [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von  [!DNL Platform] Diensten zu strukturieren, zu beschriften und zu erweitern.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der [!DNL Flow Service]-API erfolgreich eine Verbindung zu [!DNL Amazon Redshift] herstellen zu können.

### Erforderliche Anmeldedaten sammeln

Damit [!DNL Flow Service] eine Verbindung mit [!DNL Amazon Redshift] herstellen kann, müssen Sie die folgenden Verbindungseigenschaften angeben:

| **Berechtigung** | **Beschreibung** |
| -------------- | --------------- |
| `server` | Der mit Ihrem [!DNL Amazon Redshift]-Konto verknüpfte Server. |
| `username` | Der Benutzername, der Ihrem [!DNL Amazon Redshift]-Konto zugeordnet ist. |
| `password` | Das Ihrem [!DNL Amazon Redshift]-Konto zugeordnete Kennwort. |
| `database` | Die [!DNL Amazon Redshift]-Datenbank, auf die Sie zugreifen. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL Amazon Redshift] ist `3416976c-a9ca-4bba-901a-1f08f66978ff`. |

Weitere Informationen zu den ersten Schritten finden Sie in diesem [[!DNL Amazon Redshift] Dokument](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

### Verwenden von Platform-APIs

Informationen dazu, wie Sie erfolgreich Aufrufe an Platform-APIs durchführen können, finden Sie im Handbuch [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Basisverbindung erstellen

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basis-Verbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den Endpunkt `/connections` und geben Sie dabei Ihre [!DNL Amazon Redshift]-Authentifizierungsdaten als Teil der Anfrageparameter an.

**API-Format**

```https
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Amazon Redshift]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "amazon-redshift base connection",
        "description": "base connection for amazon-redshift,
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "server": "{SERVER}",
                "database": "{DATABASE}",
                "password": "{PASSWORD}",
                "username": "{USERNAME}"
            }
        },
        "connectionSpec": {
            "id": "3416976c-a9ca-4bba-901a-1f08f66978ff",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| ------------- | --------------- |
| `auth.params.server` | Ihr [!DNL Amazon Redshift]-Server. |
| `auth.params.database` | Die mit Ihrem [!DNL Amazon Redshift]-Konto verknüpfte Datenbank. |
| `auth.params.password` | Das Ihrem [!DNL Amazon Redshift]-Konto zugeordnete Kennwort. |
| `auth.params.username` | Der Benutzername, der Ihrem [!DNL Amazon Redshift]-Konto zugeordnet ist. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID [!DNL Amazon Redshift]: `3416976c-a9ca-4bba-901a-1f08f66978ff` |

**Antwort**

Eine erfolgreiche Antwort gibt die neu erstellte Verbindung zurück, einschließlich der eindeutigen Kennung (`id`). Diese ID ist erforderlich, um Ihre Daten im nächsten Tutorial zu untersuchen.

```json
{
    "id": "373e88fc-43da-4e3c-be88-fc43da3e3c0f",
    "etag": "\"1700ce7b-0000-0200-0000-5e3b405e0000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL Amazon Redshift]-Verbindung mit der [!DNL Flow Service]-API erstellt und den eindeutigen ID-Wert der Verbindung erhalten. Sie können diese Verbindungs-ID im nächsten Tutorial verwenden, wenn Sie erfahren, wie Sie mit der Flow Service-API](../../explore/database-nosql.md)Datenbanken oder NoSQL-Systeme analysieren können.[
