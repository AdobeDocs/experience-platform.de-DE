---
keywords: Experience Platform;Startseite;beliebte Themen;Microsoft Dynamics;Mikrosoft dynamics;dynamics;Dynamics
solution: Experience Platform
title: Erstellen einer Microsoft Dynamics-Basisverbindung mit der Flow Service-API
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Flow Service-API Platform mit einem Microsoft Dynamics-Konto verbinden.
exl-id: 423c6047-f183-4d92-8d2f-cc8cc26647ef
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 56%

---

# Erstellen einer [!DNL Microsoft Dynamics]-Basisverbindung mithilfe der [!DNL Flow Service]-API

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL Microsoft Dynamics] (nachstehend &quot;genannt)[!DNL Dynamics]&quot;) mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um Platform mithilfe des [!DNL Flow Service] API.

### Sammeln erforderlicher Anmeldeinformationen

Um [!DNL Flow Service] mit [!DNL Dynamics] zu verbinden, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| `serviceUri` | Die Dienst-URL Ihrer [!DNL Dynamics] -Instanz. |
| `username` | Der Benutzername für Ihre [!DNL Dynamics] Benutzerkonto. |
| `password` | Das Kennwort für Ihre [!DNL Dynamics] -Konto. |
| `servicePrincipalId` | Die Client-ID Ihrer [!DNL Dynamics] -Konto. Diese ID ist bei der Verwendung der Service-Prinzipal- und schlüsselbasierten Authentifizierung erforderlich. |
| `servicePrincipalKey` | Der Geheimschlüssel des Dienstprinzips. Diese Berechtigung ist bei der Verwendung von Dienstprinzipal und schlüsselbasierter Authentifizierung erforderlich. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL Dynamics] ist: `38ad80fe-8b06-4938-94f4-d4ee80266b07`. |

Weitere Informationen zu den ersten Schritten finden Sie unter [this [!DNL Dynamics] Dokument](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

### Verwenden von Platform-APIs

Informationen zum Aufrufen von Platform-APIs finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Erstellen einer Basisverbindung

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basisverbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den Endpunkt `/connections` und geben Sie dabei Ihre [!DNL Dynamics]-Authentifizierungsdaten als Teil der Anfrageparameter an.

### Erstellen einer [!DNL Dynamics]-Basisverbindung mit einfacher Authentifizierung

So erstellen Sie eine [!DNL Dynamics] Basisverbindung mit einfacher Authentifizierung, stellen Sie eine POST-Anfrage an die [!DNL Flow Service] API beim Bereitstellen von Werten für die `serviceUri`, `username`und `password`.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `auth.params.serviceUri` | Der Dienst-URI, der mit Ihrer [!DNL Dynamics] -Instanz. |
| `auth.params.username` | Der Benutzername, der mit Ihrer [!DNL Dynamics] -Konto. |
| `auth.params.password` | Das Kennwort, das mit Ihrem [!DNL Dynamics] -Konto. |
| `connectionSpec.id` | Die [!DNL Dynamics]-Verbindungsspezifikations-ID: `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

**Antwort**

Eine erfolgreiche Antwort gibt die neu erstellte Basisverbindung zurück, einschließlich ihrer eindeutigen Kennung (`id`). Diese ID ist erforderlich, um im nächsten Schritt Ihr CRM-System zu untersuchen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

### Erstellen Sie eine [!DNL Dynamics] Basisverbindung mithilfe der schlüsselbasierten Authentifizierung des Dienstprinzips

So erstellen Sie eine [!DNL Dynamics] Basisverbindung mithilfe der schlüsselbasierten Authentifizierung des Dienstprinzips, stellen Sie eine POST-Anfrage an die [!DNL Flow Service] API beim Bereitstellen von Werten für die `serviceUri`, `servicePrincipalId`und `servicePrincipalKey`.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `auth.params.serviceUri` | Der Dienst-URI, der mit Ihrer [!DNL Dynamics] -Instanz. |
| `auth.params.servicePrincipalId` | Die Client-ID Ihrer [!DNL Dynamics] -Konto. Diese ID ist bei der Verwendung der Service-Prinzipal- und schlüsselbasierten Authentifizierung erforderlich. |
| `auth.params.servicePrincipalKey` | Der Geheimschlüssel des Dienstprinzips. Diese Berechtigung ist bei der Verwendung von Dienstprinzipal und schlüsselbasierter Authentifizierung erforderlich. |
| `connectionSpec.id` | Die [!DNL Dynamics]-Verbindungsspezifikations-ID: `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

**Antwort**

Eine erfolgreiche Antwort gibt die neu erstellte Basisverbindung zurück, einschließlich ihrer eindeutigen Kennung (`id`). Diese ID ist erforderlich, um im nächsten Schritt Ihr CRM-System zu untersuchen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL Microsoft Dynamics]-Basisverbindung mithilfe der [!DNL Flow Service]-API erstellt. Sie können diese Basisverbindungs-ID in den folgenden Tutorials verwenden:

* [Erkunden von Struktur und Inhalten Ihrer Datentabellen mithilfe der  [!DNL Flow Service] -API](../../explore/tabular.md)
* [Erstellen Sie einen Datenfluss, um CRM-Daten mithilfe des [!DNL Flow Service] API](../../collect/crm.md)
