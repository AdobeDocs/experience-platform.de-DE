---
description: Auf dieser Seite wird der API-Aufruf zum Abrufen einer Berechtigungskonfiguration über Adobe Experience Platform Destination SDK veranschaulicht.
title: Abrufen einer Berechtigungskonfiguration
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 28%

---


# Abrufen einer Berechtigungskonfiguration

>[!IMPORTANT]
>
>**API-Endpunkt**: `platform.adobe.io/data/core/activation/authoring/credentials`

Auf dieser Seite werden die API-Anfrage und die Payload erläutert, die Sie verwenden können, um eine Berechtigungskonfiguration mithilfe der `/authoring/credentials` API-Endpunkt.

## Verwendung des API-Endpunkts `/credentials` {#when-to-use}

>[!IMPORTANT]
>
>In den meisten Fällen ist es ***nicht*** erforderlich, den API-Endpunkt `/credentials` zu verwenden. Stattdessen können Sie die Authentifizierungsinformationen für Ihr Ziel über den `customerAuthenticationConfigurations`-Parameter des `/destinations`-Endpunkts konfigurieren.
> 
>Lesen [Konfiguration der Kundenauthentifizierung](../functionality/destination-configuration/customer-authentication.md) für detaillierte Informationen zu den unterstützten Authentifizierungstypen.

Verwenden Sie diesen API-Endpunkt, um eine Berechtigungskonfiguration nur dann zu erstellen, wenn ein globales Authentifizierungssystem zwischen Adobe und Ihrer Zielplattform vorhanden ist und die [!DNL Platform] Der Kunde muss keine Authentifizierungsberechtigungen bereitstellen, um eine Verbindung zu Ihrem Ziel herzustellen. In diesem Fall müssen Sie mithilfe der `/credentials` API-Endpunkt.

Bei der Verwendung eines globalen Authentifizierungssystems müssen Sie `"authenticationRule":"PLATFORM_AUTHENTICATION"` im [Zielversand](../functionality/destination-configuration/destination-delivery.md) Konfiguration, wenn [Erstellen einer neuen Zielkonfiguration](../authoring-api/destination-configuration/create-destination-configuration.md).

>[!IMPORTANT]
>
>Alle von Destination SDK unterstützten Parameternamen und Werte sind **Groß-/Kleinschreibung**. Um Fehler bei der Groß-/Kleinschreibung zu vermeiden, verwenden Sie bitte die Parameternamen und -werte genau wie in der Dokumentation dargestellt.

## Erste Schritte mit API-Vorgängen für Anmeldedaten {#get-started}

Bevor Sie fortfahren, lesen Sie [Erste Schritte](../getting-started.md). Dort finden Sie die nötigen Informationen für den erfolgreichen Aufruf der API, einschließlich Details für den Abruf der erforderlichen Authoring-Berechtigung für Ziele und zu den erforderlichen Kopfzeilen.

## Abrufen einer Berechtigungskonfiguration {#retrieve}

Sie können eine [vorhandene](create-credential-configuration.md) Berechtigungskonfiguration durch `GET` Anfrage an `/authoring/credentials` -Endpunkt.

**API-Format**

Verwenden Sie das folgende API-Format, um alle Berechtigungskonfigurationen für Ihr Konto abzurufen.

```http
GET /authoring/credentials
```

Verwenden Sie das folgende API-Format, um eine bestimmte Berechtigungskonfiguration abzurufen, die von der `{INSTANCE_ID}` Parameter.

```http
GET /authoring/credentials/{INSTANCE_ID}
```

Die folgenden beiden Anfragen rufen alle Anmeldekonfigurationen für Ihre IMS-Organisation oder eine bestimmte Berechtigungskonfiguration ab, je nachdem, ob Sie die `INSTANCE_ID` -Parameter in der -Anfrage.

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

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit einer Liste von Berechtigungskonfigurationen zurück, auf die Sie basierend auf der [!DNL IMS Org ID] und des von Ihnen verwendeten Sandbox-Namens. One `instanceId` entspricht einer Berechtigungskonfiguration.

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

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit den Details der Konfiguration der Anmeldedaten zurück, die der `instanceId` auf der Anfrage bereitgestellt werden.

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

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie Details zu Ihren Berechtigungskonfigurationen mithilfe der `/authoring/credentials` API-Endpunkt. Lesen Sie [Verwenden des Destination SDK zum Konfigurieren Ihres Ziels](../guides/configure-destination-instructions.md), um zu verstehen, wo dieser Schritt in den Prozess der Konfiguration Ihres Ziels passt.
