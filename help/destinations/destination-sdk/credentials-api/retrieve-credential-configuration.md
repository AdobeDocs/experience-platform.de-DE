---
description: Auf dieser Seite wird der API-Aufruf zum Abrufen einer Berechtigungskonfiguration über Adobe Experience Platform Destination SDK veranschaulicht.
title: Abrufen einer Berechtigungskonfiguration
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: ht
source-wordcount: '475'
ht-degree: 100%

---


# Abrufen einer Berechtigungskonfiguration

>[!IMPORTANT]
>
>**API-Endpunkt**: `platform.adobe.io/data/core/activation/authoring/credentials`

Auf dieser Seite werden die API-Anfrage und die Payload erläutert, die Sie verwenden können, um eine Berechtigungskonfiguration mithilfe des API-Endpunkts `/authoring/credentials` abzurufen.

## Verwendung des API-Endpunkts `/credentials` {#when-to-use}

>[!IMPORTANT]
>
>In den meisten Fällen ist es ***nicht*** erforderlich, den API-Endpunkt `/credentials` zu verwenden. Stattdessen können Sie die Authentifizierungsinformationen für Ihr Ziel über den Parameter `customerAuthenticationConfigurations` des Endpunkts `/destinations` konfigurieren.
> 
>Lesen Sie [Konfiguration der Kundenauthentifizierung](../functionality/destination-configuration/customer-authentication.md) für detaillierte Informationen zu den unterstützten Authentifizierungstypen.

Verwenden Sie diesen API-Endpunkt nur dann zum Erstellen einer Berechtigungskonfiguration, wenn ein globales Authentifizierungssystem zwischen Adobe und Ihrer Zielplattform besteht und die [!DNL Platform]-Kundinnen und -Kunden keine Authentifizierungsdaten bereitstellen müssen, um eine Verbindung zu Ihrem Ziel herzustellen. In diesem Fall müssen Sie mithilfe des API-Endpunkts `/credentials` eine Berechtigungskonfiguration erstellen.

Bei der Verwendung eines globalen Authentifizierungssystems müssen Sie `"authenticationRule":"PLATFORM_AUTHENTICATION"` in der Konfiguration des [Zielversands](../functionality/destination-configuration/destination-delivery.md) festlegen, wenn Sie [eine neue Zielkonfiguration erstellen](../authoring-api/destination-configuration/create-destination-configuration.md).

>[!IMPORTANT]
>
>Bei allen von Destination SDK unterstützten Parameternamen und Werten wird **nach Groß-/Kleinschreibung unterschieden**. Um Fehler bei der Groß-/Kleinschreibung zu vermeiden, verwenden Sie bitte die Parameternamen und -werte genau wie in der Dokumentation dargestellt.

## Erste Schritte mit Berechtigungs-API-Vorgängen {#get-started}

Bevor Sie fortfahren, lesen Sie [Erste Schritte](../getting-started.md). Dort finden Sie die nötigen Informationen für den erfolgreichen Aufruf der API, einschließlich Details für den Abruf der erforderlichen Authoring-Berechtigung für Ziele und zu den erforderlichen Kopfzeilen.

## Abrufen einer Berechtigungskonfiguration {#retrieve}

Sie können eine [vorhandene](create-credential-configuration.md) Berechtigungskonfiguration abrufen, indem Sie eine `GET`-Anfrage an den Endpunkt `/authoring/credentials` stellen.

**API-Format**

Verwenden Sie das folgende API-Format, um alle Berechtigungskonfigurationen für Ihr Konto abzurufen.

```http
GET /authoring/credentials
```

Verwenden Sie das folgende API-Format, um eine bestimmte Berechtigungskonfiguration abzurufen, die durch den Parameter `{INSTANCE_ID}` bestimmt wird.

```http
GET /authoring/credentials/{INSTANCE_ID}
```

Die folgenden beiden Anfragen rufen alle Berechtigungskonfigurationen für Ihre IMS-Organisation oder eine bestimmte Berechtigungskonfiguration ab, je nachdem, ob Sie den Parameter `INSTANCE_ID` in der Anfrage übergeben.

Wählen Sie die einzelnen Registerkarten unten aus, um die entsprechende Payload anzuzeigen.

>[!BEGINTABS]

>[!TAB Alle Berechtigungskonfigurationen abrufen]

+++Anfrage

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Antwort

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit einer Liste der Berechtigungskonfigurationen zurückgegeben, auf die Sie Zugriff haben, basierend auf der von Ihnen verwendeten [!DNL IMS Org ID] und dem Sandbox-Namen. Eine `instanceId` entspricht einer Berechtigungskonfiguration.

```json
{
   "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
   "createdDate":"2021-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
   "type":"s3Authentication",
   "name":"yourdestination",
   "s3Authentication":{
      "accessId":"string",
      "secretKey":"string"
   }
},
{
   "instanceId":"a25bffa0-3127-4030-895d-1d1236bb3680",
   "createdDate":"2022-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2022-08-07T06:41:48.641943Z",
   "type":"basic",
   "name":"yourdestination",
   "s3Authentication":{
      "url":"string",
      "username":"string",
      "password":"string"
   }
}
```

+++

>[!TAB Abrufen einer bestimmten Berechtigungskonfiguration]

+++Anfrage

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| Parameter | Beschreibung |
| -------- | ----------- |
| `{INSTANCE_ID}` | Die ID der Berechtigungskonfiguration, die Sie abrufen möchten. |

+++

+++Antwort

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit den Details der Berechtigungskonfiguration zurückgegeben, die der `instanceId` in der Anfrage entspricht.

```json
{
   "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
   "createdDate":"2021-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
   "type":"s3Authentication",
   "name":"yourdestination",
   "s3Authentication":{
      "accessId":"string",
      "secretKey":"string"
   }
}
```

+++

>[!ENDTABS]

## Umgang mit API-Fehlern {#error-handling}

Destination SDK-API-Endpunkte folgen den allgemeinen Grundsätzen von Experience Platform API-Fehlermeldungen. Siehe [API-Status-Codes](../../../landing/troubleshooting.md#api-status-codes) und [Fehler im Anfrage-Header](../../../landing/troubleshooting.md#request-header-errors) in der Anleitung zur Fehlerbehebung für Platform.

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie Details zu Ihren Berechtigungskonfigurationen mithilfe des API-Endpunkts `/authoring/credentials` abrufen. Lesen Sie [Verwenden des Destination SDK zum Konfigurieren Ihres Ziels](../guides/configure-destination-instructions.md), um zu verstehen, wo dieser Schritt in den Prozess der Konfiguration Ihres Ziels passt.
