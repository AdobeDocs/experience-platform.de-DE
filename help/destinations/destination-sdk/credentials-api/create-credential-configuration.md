---
description: Auf dieser Seite wird der API-Aufruf zum Erstellen einer Adobe Experience Platform Destination SDK zur Konfiguration von Anmeldedaten veranschaulicht.
title: Erstellen einer Berechtigungskonfiguration
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 49%

---


# Erstellen einer Berechtigungskonfiguration

>[!IMPORTANT]
>
>**API-Endpunkt**: `platform.adobe.io/data/core/activation/authoring/credentials`

Auf dieser Seite werden die API-Anfrage und die Payload erläutert, die Sie zum Erstellen einer Berechtigungskonfiguration mit der `/authoring/credentials` API-Endpunkt.

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

Bevor Sie fortfahren, lesen Sie den Abschnitt [Erste Schritte](../getting-started.md). Dort erhalten Sie wichtige Informationen darüber, wie Sie die API aufrufen und die erforderliche Authoring-Berechtigung für Ziele und die Kopfzeilen abrufen können.

## Erstellen einer Zugangsdaten-Konfiguration {#create}

Sie können eine neue Konfiguration der Anmeldedaten erstellen, indem Sie eine `POST` Anfrage an `/authoring/credentials` -Endpunkt.

**API-Format**

```http
POST /authoring/credentials
```

Die folgenden Anfragen erstellen neue Berechtigungskonfigurationen, die durch die in der Payload bereitgestellten Parameter definiert werden.

Wählen Sie die einzelnen Registerkarten unten aus, um die entsprechende Payload anzuzeigen.

>[!BEGINTABS]

>[!TAB Allgemein]

**Basisberechtigungskonfiguration erstellen**

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

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zur neu erstellten Zugangsdaten-Konfiguration zurück.

+++

>[!TAB Amazon S3]

**Erstellen Sie eine [!DNL Amazon S3] Berechtigungskonfiguration**

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
| `secretKey` | Zeichenfolge | [!DNL Amazon S3] geheimer Schlüssel |

{style="table-layout:auto"}

+++

+++Antwort

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zur neu erstellten Zugangsdaten-Konfiguration zurück.

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

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zur neu erstellten Zugangsdaten-Konfiguration zurück.

+++

>[!TAB Azure Data Lake Storage]

**Erstellen Sie eine [!DNL Azure Data Lake Storage] Berechtigungskonfiguration**

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

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zur neu erstellten Zugangsdaten-Konfiguration zurück.

+++

>[!TAB Azure-Blobspeicher]

**Erstellen Sie eine [!DNL Azure Blob Storage] Berechtigungskonfiguration**

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
| `connectionString` | Zeichenfolge | [!DNL Azure Blob Storage] Verbindungszeichenfolge |

{style="table-layout:auto"}

+++

+++Antwort

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zur neu erstellten Zugangsdaten-Konfiguration zurück.

+++

>[!ENDTABS]

## Umgang mit API-Fehlern {#error-handling}

Destination SDK-API-Endpunkte folgen den allgemeinen Grundsätzen von Experience Platform API-Fehlermeldungen. Siehe [API-Status-Codes](../../../landing/troubleshooting.md#api-status-codes) und [Fehler im Anfrage-Header](../../../landing/troubleshooting.md#request-header-errors) in der Anleitung zur Fehlerbehebung für Platform.

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wann der Anmeldeinformationen-Endpunkt verwendet und wie Sie eine Konfiguration mit Anmeldeinformationen mithilfe des `/authoring/credentials` API-Endpunkt lesen [Verwendung von Destination SDK zum Konfigurieren Ihres Ziels](../guides/configure-destination-instructions.md) um zu verstehen, wo dieser Schritt in den Prozess der Konfiguration Ihres Ziels passt.
