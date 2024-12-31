---
keywords: Experience Platform;Startseite;beliebte Themen;Microsoft Dynamics;Microsoft Dynamics;Dynamics;Dynamics
solution: Experience Platform
title: Erstellen einer Microsoft Dynamics-Basisverbindung mithilfe der Flow Service-API
type: Tutorial
description: Erfahren Sie, wie Sie Platform mithilfe der Flow Service-API mit einem Microsoft Dynamics-Konto verbinden.
exl-id: 423c6047-f183-4d92-8d2f-cc8cc26647ef
source-git-commit: d22c71fb77655c401f4a336e339aaf8b3125d1b6
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 55%

---

# Erstellen einer [!DNL Microsoft Dynamics]-Basisverbindung mithilfe der [!DNL Flow Service]-API

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL Microsoft Dynamics] (nachstehend &quot;[!DNL Dynamics]&quot; genannt) mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um Platform mithilfe der [!DNL Flow Service]-API erfolgreich mit einem Dynamics-Konto verbinden zu können.

### Sammeln erforderlicher Anmeldedaten

Um [!DNL Flow Service] mit [!DNL Dynamics] zu verbinden, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

>[!BEGINTABS]

>[!TAB Einfache Authentifizierung]

| Anmeldedaten | Beschreibung |
| --- | --- |
| `serviceUri` | Die Service-URL Ihrer [!DNL Dynamics]. |
| `username` | Der Benutzername für Ihr [!DNL Dynamics] Benutzerkonto. |
| `password` | Das Kennwort für Ihr [!DNL Dynamics]. |

>[!TAB Service-Prinzipal- und Schlüsselauthentifizierung]

| Anmeldedaten | Beschreibung |
| --- | --- |
| `servicePrincipalId` | Die Client-ID Ihres [!DNL Dynamics]. Diese ID ist erforderlich, wenn die Service-Prinzipal- und schlüsselbasierte Authentifizierung verwendet wird. |
| `servicePrincipalKey` | Der geheime Schlüssel des Service-Prinzipals. Diese Berechtigung ist erforderlich, wenn die Authentifizierung über einen Service-Prinzipal und einen Schlüssel verwendet wird. |

>[!ENDTABS]

Weitere Informationen zu den ersten Schritten finden Sie [diesem  [!DNL Dynamics] Dokument](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

### Verwenden von Platform-APIs

Informationen zum Aufrufen von Platform-APIs finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Erstellen einer Basisverbindung

>[!TIP]
>
>Nach der Erstellung können Sie den Authentifizierungstyp einer [!DNL Dynamics] Basisverbindung nicht mehr ändern. Um den Authentifizierungstyp zu ändern, müssen Sie eine neue Basisverbindung erstellen.

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungs-Anmeldedaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basisverbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den Endpunkt `/connections` und geben Sie dabei Ihre [!DNL Dynamics]-Authentifizierungs-Anmeldedaten als Teil der Anfrageparameter an.

### Erstellen einer [!DNL Dynamics] Basisverbindung

>[!TIP]
>
>Nach der Erstellung können Sie den Authentifizierungstyp einer [!DNL Dynamics] Basisverbindung nicht mehr ändern. Um den Authentifizierungstyp zu ändern, müssen Sie eine neue Basisverbindung erstellen.

Der erste Schritt beim Erstellen einer Quellverbindung besteht darin, Ihre [!DNL Dynamics]-Quelle zu authentifizieren und eine Basisverbindungs-ID zu generieren. Mittels einer Basisverbindungs-ID können Sie Dateien aus Ihrer Quelle durchsuchen, zwischen Dateien innerhalb der Quelle navigieren und bestimmte Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu Datentypen und Formaten.

Um eine Basisverbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den `/connections`-Endpunkt beim Bereitstellen der [!DNL Dynamics]-Authentifizierungs-Anmeldedaten als Teil der Anfrageparameter.

**API-Format**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB Einfache Authentifizierung]

Um eine [!DNL Dynamics] Basisverbindung mit einfacher Authentifizierung zu erstellen, stellen Sie eine Verbindungsanfrage an die [!DNL Flow Service]-API und geben dabei Werte für `serviceUri`, `username` und `password` Ihrer POST an.

+++Anfrage

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
| `auth.params.serviceUri` | Der Service-URI, der Ihrer [!DNL Dynamics]-Instanz zugeordnet ist. |
| `auth.params.username` | Der Benutzername, der Ihrem [!DNL Dynamics]-Konto zugeordnet ist. |
| `auth.params.password` | Das mit Ihrem [!DNL Dynamics]-Konto verknüpfte Kennwort. |
| `connectionSpec.id` | Die [!DNL Dynamics]-Verbindungsspezifikations-ID: `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

+++

+++Antwort

Eine erfolgreiche Antwort gibt die neu erstellte Basisverbindung zurück, einschließlich ihrer eindeutigen Kennung (`id`). Diese ID ist erforderlich, um im nächsten Schritt Ihr CRM-System zu untersuchen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

+++

>[!TAB Schlüsselbasierte Authentifizierung für Service-Prinzipal]

Um eine [!DNL Dynamics] Basisverbindung mithilfe der Authentifizierung über einen Schlüssel zu erstellen, stellen Sie eine Verbindungsanfrage an die [!DNL Flow Service]-API und geben dabei Werte für die `serviceUri`, `servicePrincipalId` und `servicePrincipalKey` Ihrer POST an.

+++Anfrage

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
| `auth.params.serviceUri` | Der Service-URI, der Ihrer [!DNL Dynamics]-Instanz zugeordnet ist. |
| `auth.params.servicePrincipalId` | Die Client-ID Ihres [!DNL Dynamics]. Diese ID ist erforderlich, wenn die Service-Prinzipal- und schlüsselbasierte Authentifizierung verwendet wird. |
| `auth.params.servicePrincipalKey` | Der geheime Schlüssel des Service-Prinzipals. Diese Berechtigung ist erforderlich, wenn die Authentifizierung über einen Service-Prinzipal und einen Schlüssel verwendet wird. |
| `connectionSpec.id` | Die [!DNL Dynamics]-Verbindungsspezifikations-ID: `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

+++

+++Antwort

Eine erfolgreiche Antwort gibt die neu erstellte Basisverbindung zurück, einschließlich ihrer eindeutigen Kennung (`id`). Diese ID ist erforderlich, um im nächsten Schritt Ihr CRM-System zu untersuchen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

+++

>[!ENDTABS]


## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL Microsoft Dynamics]-Basisverbindung mithilfe der [!DNL Flow Service]-API erstellt. Sie können diese Basisverbindungs-ID in den folgenden Tutorials verwenden:

* [Erkunden von Struktur und Inhalten Ihrer Datentabellen mithilfe der  [!DNL Flow Service] -API](../../explore/tabular.md)
* [Erstellen eines Datenflusses, um CRM-Daten mithilfe der API  [!DNL Flow Service]  Platform zu übertragen](../../collect/crm.md)
