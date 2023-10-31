---
description: Auf dieser Seite wird der API-Aufruf zum Erstellen einer Berechtigungskonfiguration im Adobe Experience Platform Destination SDK veranschaulicht.
title: Erstellen einer Berechtigungskonfiguration
exl-id: 9844c9c5-d2dc-4d4b-ae93-759bf23b87fa
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 100%

---

# Erstellen einer Berechtigungskonfiguration

>[!IMPORTANT]
>
>**API-Endpunkt**: `platform.adobe.io/data/core/activation/authoring/credentials`

Auf dieser Seite werden die API-Anfrage und die Payload erläutert, die Sie zum Erstellen einer Berechtigungskonfiguration mit dem API-Endpunkt `/authoring/credentials` verwenden können.

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

## Erstellen einer Zugangsdaten-Konfiguration {#create}

Sie können eine neue Zugangsdaten-Konfiguration erstellen, indem Sie eine `POST`-Anfrage an den Endpunkt `/authoring/credentials` senden.

**API-Format**

```http
POST /authoring/credentials
```

Die folgenden Anfragen erstellen neue Berechtigungskonfigurationen, die durch die in der Payload bereitgestellten Parameter bestimmt werden.

Wählen Sie die einzelnen Registerkarten unten aus, um die entsprechende Payload anzuzeigen.

>[!BEGINTABS]

>[!TAB Allgemein]

**Erstellen einer Basisberechtigungskonfiguration**

+++Anfrage

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "basicAuthentication":{
      "url":"string",
      "username":"string",
      "password":"string"
   }
}
```

| Parameter | Typ | Beschreibung |
| -------- | ----------- | ----------- |
| `url` | Zeichenfolge | URL des Autorisierungsanbieters |
| `username` | Zeichenfolge | Benutzername für die Anmeldung zur Zugriffsdaten-Konfiguration |
| `password` | Zeichenfolge | Passwort für die Anmeldung zur Zugangsdaten-Konfiguration |

{style="table-layout:auto"}

+++

+++Antwort

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit Details zur neu erstellten Zugangsdaten-Konfiguration zurückgegeben.

+++

>[!TAB Amazon S3]

**Erstellen einer [!DNL Amazon S3]-Berechtigungskonfiguration**

+++**Anfrage**

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "s3Authentication":{
      "accessId":"string",
      "secretKey":"string"
   }
}
```

| Parameter | Typ | Beschreibung |
| -------- | ----------- | ----------- |
| `accessId` | Zeichenfolge | [!DNL Amazon S3] Zugriffs-ID |
| `secretKey` | Zeichenfolge | Geheimer [!DNL Amazon S3]-Schlüssel |

{style="table-layout:auto"}

+++

+++Antwort

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit Details zur neu erstellten Zugangsdaten-Konfiguration zurückgegeben.

+++

>[!TAB SSH]

**Erstellen einer SSH-Berechtigungskonfiguration**

+++Anfrage

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "sshAuthentication":{
      "username":"string",
      "sshKey":"string"
   }
}
```

| Parameter | Typ | Beschreibung |
| -------- | ----------- | ----------- |
| `username` | Zeichenfolge | Benutzername für die Anmeldung zur Zugriffsdaten-Konfiguration |
| `sshKey` | Zeichenfolge | SSH-Schlüssel für SFTP mit SSH-Authentifizierung |

{style="table-layout:auto"}

+++

+++Antwort

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit Details zur neu erstellten Zugangsdaten-Konfiguration zurückgegeben.

+++

>[!TAB Azure Data Lake Storage]

**Erstellen einer [!DNL Azure Data Lake Storage]-Berechtigungskonfiguration**

+++Anfrage

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "azureAuthentication":{
      "url":"string",
      "tenant":"string",
      "servicePrincipalId":"string",
      "servicePrincipalKey":"string"
   }
}
```

| Parameter | Typ | Beschreibung |
| -------- | ----------- | ----------- |
| `url` | Zeichenfolge | URL des Autorisierungsanbieters |
| `tenant` | Zeichenfolge | Azure Data Lake Storage-Mandant |
| `servicePrincipalId` | Zeichenfolge | Azure Service Principal ID für Azure Data Lake Storage |
| `servicePrincipalKey` | Zeichenfolge | Azure Service Principal Key für Azure Data Lake Storage |

{style="table-layout:auto"}

+++

+++Antwort

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit Details zur neu erstellten Zugangsdaten-Konfiguration zurückgegeben.

+++

>[!TAB Azure-Blobspeicher]

**Erstellen einer [!DNL Azure Blob Storage]-Berechtigungskonfiguration**

+++Anfrage

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "azureConnectionStringAuthentication":{
      "connectionString":"string"
   }
}
```

| Parameter | Typ | Beschreibung |
| -------- | ----------- | ----------- |
| `connectionString` | Zeichenfolge | [!DNL Azure Blob Storage]-Verbindungszeichenfolge |

{style="table-layout:auto"}

+++

+++Antwort

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit Details zur neu erstellten Zugangsdaten-Konfiguration zurückgegeben.

+++

>[!ENDTABS]

## Umgang mit API-Fehlern {#error-handling}

Destination SDK-API-Endpunkte folgen den allgemeinen Grundsätzen von Experience Platform API-Fehlermeldungen. Siehe [API-Status-Codes](../../../landing/troubleshooting.md#api-status-codes) und [Fehler im Anfrage-Header](../../../landing/troubleshooting.md#request-header-errors) in der Anleitung zur Fehlerbehebung für Platform.

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wann der Berechtigungs-Endpunkt verwendet wird und wie Sie eine Berechtigungskonfiguration mithilfe des API-Endpunkts `/authoring/credentials` einrichten. Lesen Sie [Verwenden von Destination SDK zum Konfigurieren Ihres Ziels](../guides/configure-destination-instructions.md), um zu verstehen, wo dieser Schritt in den Prozess der Konfiguration Ihres Ziels passt.
