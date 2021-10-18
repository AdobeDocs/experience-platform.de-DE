---
keywords: Experience Platform;Startseite;beliebte Themen;Microsoft Dynamics;Mikrosoft dynamics;dynamics;Dynamics
solution: Experience Platform
title: Erstellen einer Microsoft Dynamics-Basisverbindung mit der Flow Service-API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Flow Service-API Platform mit einem Microsoft Dynamics-Konto verbinden.
exl-id: 423c6047-f183-4d92-8d2f-cc8cc26647ef
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 9%

---

# Erstellen einer [!DNL Microsoft Dynamics]-Basisverbindung mithilfe der [!DNL Flow Service]-API

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL Microsoft Dynamics] (nachfolgend &quot;a1/>&quot;genannt) mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).[!DNL Dynamics]

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von Platform-Diensten zu strukturieren, zu beschriften und zu erweitern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Anwendungen für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um Platform mithilfe der [!DNL Flow Service]-API erfolgreich mit einem Dynamics-Konto verbinden zu können.

### Erforderliche Anmeldedaten sammeln

Damit [!DNL Flow Service] eine Verbindung zu [!DNL Dynamics] herstellen kann, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `serviceUri` | Die Dienst-URL Ihrer [!DNL Dynamics]-Instanz. |
| `username` | Der Benutzername für Ihr [!DNL Dynamics]-Benutzerkonto. |
| `password` | Das Kennwort für Ihr [!DNL Dynamics]-Konto. |
| `servicePrincipalId` | Die Client-ID Ihres [!DNL Dynamics]-Kontos. Diese ID ist bei der Verwendung der Service-Prinzipal- und schlüsselbasierten Authentifizierung erforderlich. |
| `servicePrincipalKey` | Der Geheimschlüssel des Dienstprinzips. Diese Berechtigung ist bei der Verwendung von Dienstprinzipal und schlüsselbasierter Authentifizierung erforderlich. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL Dynamics] lautet: `38ad80fe-8b06-4938-94f4-d4ee80266b07`. |

Weitere Informationen zu den ersten Schritten finden Sie unter [this [!DNL Dynamics] document](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

### Verwenden von Platform-APIs

Informationen dazu, wie Sie erfolgreich Aufrufe an Platform-APIs durchführen können, finden Sie im Handbuch [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Basisverbindung erstellen

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basis-Verbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den Endpunkt `/connections` und geben Sie dabei Ihre [!DNL Dynamics]-Authentifizierungsdaten als Teil der Anfrageparameter an.

### Basisverbindung [!DNL Dynamics] mit einfacher Authentifizierung erstellen

Um eine [!DNL Dynamics]-Basisverbindung mit einfacher Authentifizierung zu erstellen, stellen Sie eine POST-Anfrage an die [!DNL Flow Service]-API und geben Sie dabei Werte für `serviceUri`, `username` und `password` an.

**API-Format**

```http
POST /connections
```

**Anfrage**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Dynamics connection",
        "description": "Dynamics connection using basic auth",
        "auth": {
            "specName": "Basic Authentication for Dynamics-Online",
            "params": {
                "serviceUri": "{SERVICE_URI}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `auth.params.serviceUri` | Der Dienst-URI, der Ihrer [!DNL Dynamics]-Instanz zugeordnet ist. |
| `auth.params.username` | Der Benutzername, der Ihrem [!DNL Dynamics]-Konto zugeordnet ist. |
| `auth.params.password` | Das Ihrem [!DNL Dynamics]-Konto zugeordnete Kennwort. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID [!DNL Dynamics]: `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

**Antwort**

Eine erfolgreiche Antwort gibt die neu erstellte Verbindung zurück, einschließlich der eindeutigen Kennung (`id`). Diese ID ist erforderlich, um Ihr CRM-System im nächsten Schritt zu untersuchen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

### Erstellen Sie eine [!DNL Dynamics]-Basisverbindung mithilfe der schlüsselbasierten Authentifizierung des Dienstprinzipals.

Um eine [!DNL Dynamics]-Basisverbindung mithilfe der schlüsselbasierten Authentifizierung des Dienstprinzipals zu erstellen, stellen Sie eine POST-Anfrage an die [!DNL Flow Service]-API und geben Sie dabei Werte für `serviceUri`, `servicePrincipalId` und `servicePrincipalKey` an.

**API-Format**

```http
POST /connections
```

**Anfrage**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Dynamics connection",
        "description": "Dynamics connection using key-based authentication",
        "auth": {
            "specName": "Service Principal Key Based Authentication",
            "params": {
                "serviceUri": "{SERVICE_URI}",
                "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}"
            }
        },
        "connectionSpec": {
            "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `auth.params.serviceUri` | Der Dienst-URI, der Ihrer [!DNL Dynamics]-Instanz zugeordnet ist. |
| `auth.params.servicePrincipalId` | Die Client-ID Ihres [!DNL Dynamics]-Kontos. Diese ID ist bei der Verwendung der Service-Prinzipal- und schlüsselbasierten Authentifizierung erforderlich. |
| `auth.params.servicePrincipalKey` | Der Geheimschlüssel des Dienstprinzips. Diese Berechtigung ist bei der Verwendung von Dienstprinzipal und schlüsselbasierter Authentifizierung erforderlich. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID [!DNL Dynamics]: `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

**Antwort**

Eine erfolgreiche Antwort gibt die neu erstellte Verbindung zurück, einschließlich der eindeutigen Kennung (`id`). Diese ID ist erforderlich, um Ihr CRM-System im nächsten Schritt zu untersuchen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL Dynamics]-Verbindung mit der [!DNL Flow Service]-API erstellt und den eindeutigen ID-Wert der Verbindung erhalten. Sie können diese ID im nächsten Tutorial verwenden, wenn Sie erfahren, wie Sie [CRM-Systeme mithilfe der Flow Service-API](../../explore/crm.md) untersuchen.
