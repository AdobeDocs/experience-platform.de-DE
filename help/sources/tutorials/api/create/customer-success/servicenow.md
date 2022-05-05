---
keywords: Experience Platform; home; beliebte Themen; service; serviceNow
solution: Experience Platform
title: Erstellen einer ServiceNow-Basisverbindung mit der Flow Service-API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie Adobe Experience Platform mithilfe der Flow Service-API mit einem ServiceNow-Server verbinden.
exl-id: 39d0e628-5c07-4371-a5af-ac06385db891
source-git-commit: 17055f76800deadacf435970a691cec79c9f1d17
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 57%

---

# Erstellen einer [!DNL ServiceNow]-Basisverbindung mithilfe der [!DNL Flow Service]-API

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL Google ServiceNow] mithilfe der [[!DNL Flow Service] -API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um eine erfolgreiche Verbindung zu einer [!DNL ServiceNow] Server, der [!DNL Flow Service] API.

### Sammeln erforderlicher Anmeldeinformationen

Um [!DNL Flow Service] mit [!DNL ServiceNow] zu verbinden, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| `endpoint` | Der Endpunkt der [!DNL ServiceNow] Server. |
| `username` | Der Benutzername, mit dem die Verbindung zum [!DNL ServiceNow] -Server zur Authentifizierung. |
| `password` | Das Kennwort, mit dem eine Verbindung hergestellt werden soll [!DNL ServiceNow] -Server zur Authentifizierung. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL ServiceNow] ist: `eb13cb25-47ab-407f-ba89-c0125281c563`. |

Weitere Informationen zu den ersten Schritten finden Sie unter [this ServiceNow document](https://developer.servicenow.com/app.do#!/rest_api_doc?v=newyork&amp;id=r_TableAPI-GET).

### Verwenden von Platform-APIs

Informationen zum Aufrufen von Platform-APIs finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Erstellen einer Basisverbindung

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basisverbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den Endpunkt `/connections` und geben Sie dabei Ihre [!DNL ServiceNow]-Authentifizierungsdaten als Teil der Anfrageparameter an.

**API-Format**

```http
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL ServiceNow]:

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Connection for service-now",
        "description": "Connection for service-now,
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "endpoint": "{ENDPOINT}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "eb13cb25-47ab-407f-ba89-c0125281c563",
            "version": "1.0"
        }
    }'
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `auth.params.server` | Der Endpunkt Ihrer [!DNL ServiceNow] Server. |
| `auth.params.username` | Der Benutzername, mit dem die Verbindung zum [!DNL ServiceNow] -Server zur Authentifizierung. |
| `auth.params.password` | Das Kennwort, mit dem eine Verbindung hergestellt werden soll [!DNL ServiceNow] -Server zur Authentifizierung. |
| `connectionSpec.id` | Die [!DNL ServiceNow] Verbindungsspezifikations-ID: `eb13cb25-47ab-407f-ba89-c0125281c563` |

**Antwort**

Bei einer erfolgreichen Antwort wird die neu erstellte Verbindung einschließlich der eindeutigen Kennung (`id`). Diese ID ist erforderlich, um Ihr CRM-System im nächsten Schritt zu untersuchen.

```json
{
    "id": "8a3ca3dd-6d00-4c95-bca3-dd6d00dc954b",
    "etag": "\"8e0052a2-0000-0200-0000-5e25fb330000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL ServiceNow] Basisverbindung mit [!DNL Flow Service] API. Sie können diese Basis-Verbindungs-ID in den folgenden Tutorials verwenden:

* [Struktur und Inhalt Ihrer Datentabellen mithilfe des [!DNL Flow Service] API](../../explore/tabular.md)
* [Erstellen Sie einen Datenfluss, um Kundenerfolgsdaten mithilfe der [!DNL Flow Service] API](../../collect/customer-success.md)
