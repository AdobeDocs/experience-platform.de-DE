---
description: Auf dieser Seite wird der API-Aufruf veranschaulicht, mit dem eine vorhandene Berechtigungskonfiguration über Adobe Experience Platform Destination SDK aktualisiert wird.
title: Aktualisieren einer Berechtigungskonfiguration
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: ht
source-wordcount: '583'
ht-degree: 100%

---


# Aktualisieren einer Berechtigungskonfiguration

>[!IMPORTANT]
>
>**API-Endpunkt**: `platform.adobe.io/data/core/activation/authoring/credentials`

Auf dieser Seite werden die API-Anfrage und die Payload erläutert, die Sie verwenden können, um eine vorhandene Berechtigungskonfiguration mithilfe des API-Endpunkts `/authoring/credentials` zu aktualisieren.

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

## Aktualisieren einer Berechtigungskonfiguration {#update}

Sie können eine [vorhandene](create-credential-configuration.md) Berechtigungskonfiguration durch eine `PUT`-Anfrage an den Endpunkt `/authoring/credentials` mit der aktualisierten Payload aktualisieren.

Wie Sie eine vorhandene Berechtigungskonfiguration und die entsprechende `{INSTANCE_ID}` abrufen, erfahren Sie im Artikel zum [Abrufen einer Berechtigungskonfiguration](retrieve-credential-configuration.md).

**API-Format**

```http
PUT /authoring/credentials/{INSTANCE_ID}
```

| Parameter | Beschreibung |
| -------- | ----------- |
| `{INSTANCE_ID}` | Die Kennung der Berechtigungskonfiguration, die Sie aktualisieren möchten. Wie Sie eine vorhandene Berechtigungskonfiguration und die entsprechende `{INSTANCE_ID}` abrufen, erfahren Sie unter [Abrufen einer Berechtigungskonfiguration](retrieve-credential-configuration.md). |

Mit den folgenden Anfragen werden bestehende Berechtigungskonfigurationen aktualisiert, die durch die in der Payload angegebenen Parameter definiert werden.

Wählen Sie die einzelnen Registerkarten unten aus, um die entsprechende Payload anzuzeigen.

>[!BEGINTABS]

>[!TAB Allgemein]

**Aktualisieren einer allgemeinen Berechtigungskonfiguration**

+++Anfrage

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
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

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit den Details Ihrer aktualisierten Berechtigungskonfiguration zurückgegeben.

+++

>[!TAB Amazon S3]

**Aktualisieren einer [!DNL Amazon S3]-Berechtigungskonfiguration**

+++Anfrage

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
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

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit den Details Ihrer aktualisierten Berechtigungskonfiguration zurückgegeben.

+++

>[!TAB SSH]

**Aktualisieren einer [!DNL SSH]-Berechtigungskonfiguration**

+++Anfrage

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
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
| `sshKey` | Zeichenfolge | [!DNL SSH]-Schlüssel für [!DNL SFTP] mit [!DNL SSH]-Authentifizierung |

{style="table-layout:auto"}

+++

+++Antwort

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit den Details Ihrer aktualisierten Berechtigungskonfiguration zurückgegeben.

+++

>[!TAB Azure Data Lake Storage]

**Aktualisieren einer [!DNL Azure Data Lake Storage]-Berechtigungskonfiguration**

+++Anfrage

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
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
| `servicePrincipalId` | Zeichenfolge | [!DNL Azure Service Principal]-ID für [!DNL Azure Data Lake Storage] |
| `servicePrincipalKey` | Zeichenfolge | [!DNL Azure Service Principal Key] for [!DNL Azure Data Lake Storage] |

{style="table-layout:auto"}

+++

+++Antwort

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit den Details Ihrer aktualisierten Berechtigungskonfiguration zurückgegeben.

+++

>[!TAB Azure-Blobspeicher]

**Aktualisieren einer [!DNL Azure Blob]-Berechtigungskonfiguration**

+++Anfrage

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
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

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit den Details Ihrer aktualisierten Berechtigungskonfiguration zurückgegeben.

+++

>[!ENDTABS]

## Umgang mit API-Fehlern {#error-handling}

Destination SDK-API-Endpunkte folgen den allgemeinen Grundsätzen von Experience Platform API-Fehlermeldungen. Siehe [API-Status-Codes](../../../landing/troubleshooting.md#api-status-codes) und [Fehler im Anfrage-Header](../../../landing/troubleshooting.md#request-header-errors) in der Anleitung zur Fehlerbehebung für Platform.

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie eine Berechtigungskonfiguration mithilfe des API-Endpunkts `/authoring/credentials` aktualisieren können. Lesen Sie [Verwenden des Destination SDK zum Konfigurieren Ihres Ziels](../guides/configure-destination-instructions.md), um zu verstehen, wo dieser Schritt in den Prozess der Konfiguration Ihres Ziels passt.
