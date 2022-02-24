---
description: Verwenden Sie die unterstützten Authentifizierungskonfigurationen in Adobe Experience Platform Destination SDK, um Benutzer zu authentifizieren und Daten für Ihren Ziel-Endpunkt zu aktivieren.
title: Authentifizierungskonfiguration
exl-id: 33eaab24-f867-4744-b424-4ba71727373c
source-git-commit: 92bca3600d854540fd2badd925e453fba41601a7
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 7%

---

# Authentifizierungskonfiguration {#credentials}

## Unterstützte Authentifizierungstypen {#supported-authentication-types}

Die Authentifizierungskonfiguration, die Sie auswählen, bestimmt, wie sich die Experience Platform in der Platform-Benutzeroberfläche für Ihr Ziel authentifiziert.

Adobe Experience Platform Destination SDK unterstützt mehrere Authentifizierungstypen:

* Bearer-Authentifizierung
* (Beta) Amazon S3-Authentifizierung
* (Beta) Azure-Verbindungszeichenfolge
* (Beta) Azure-Dienstprinzipal
* (Beta) SFTP mit SSH-Schlüssel
* (Beta) SFTP mit Kennwort
* OAuth 2 mit Autorisierungscode
* OAU 2 mit Passwortgewährung
* OAuth 2 mit Client-Anmeldeinformationen gewähren

Sie können die Authentifizierungsinformationen für Ihr Ziel über die `customerAuthenticationConfigurations` Parameter der `/destinations` -Endpunkt.

In den folgenden Abschnitten finden Sie Details zur Authentifizierungskonfiguration für jeden Zieltyp:

* [Authentifizierungskonfigurationen für Streaming-Ziele](destination-configuration.md#customer-authentication-configurations)
* [Authentifizierungskonfigurationen für dateibasierte Ziele](file-based-destination-configuration.md#customer-authentication-configurations)

## Bearer-Authentifizierung {#bearer}

Die Trägerauthentifizierung wird für Streaming-Ziele in Experience Platform unterstützt.

Um die Authentifizierung des Trägertyps für Ihr Ziel einzurichten, konfigurieren Sie die `customerAuthenticationConfigurations` -Parameter in der `/destinations` Endpunkt wie unten gezeigt:

```json
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ]
```

## (Beta) [!DNL Amazon S3] Authentifizierung {#s3}

[!DNL Amazon S3] Die Authentifizierung wird für dateibasierte Ziele in Experience Platform unterstützt.

>[!IMPORTANT]
>
>Die dateibasierte Zielunterstützung in Adobe Experience Platform Destination SDK ist derzeit als Beta-Version verfügbar. Dokumentation und Funktionalität können sich ändern.

Um die Amazon S3-Authentifizierung für Ihr Ziel einzurichten, konfigurieren Sie die `customerAuthenticationConfigurations` -Parameter in der `/destinations` Endpunkt wie unten gezeigt:

```json
   "customerAuthenticationConfigurations":[
      {
         "authType":"S3"
      }
   ]
```

## (Betaversion) [!DNL Azure Blob Storage] {#blob}

[!DNL Azure Blob Storage] Die Authentifizierung wird für dateibasierte Ziele in Experience Platform unterstützt.

>[!IMPORTANT]
>
>Die dateibasierte Zielunterstützung in Adobe Experience Platform Destination SDK ist derzeit als Beta-Version verfügbar. Dokumentation und Funktionalität können sich ändern.

So richten Sie [!DNL Azure Blob] Authentifizierung für Ihr Ziel konfigurieren Sie die `customerAuthenticationConfigurations` -Parameter in der `/destinations` Endpunkt wie unten gezeigt:

```json
   "customerAuthenticationConfigurations":[
     {
        "authType":"AZURE_CONNECTION_STRING"
     }
  ]
```

## (Betaversion) [!DNL Azure Data Lake Storage] {#adls}

[!DNL Azure Data Lake Storage] Die Authentifizierung wird für dateibasierte Ziele in Experience Platform unterstützt.

>[!IMPORTANT]
>
>Die dateibasierte Zielunterstützung in Adobe Experience Platform Destination SDK ist derzeit als Beta-Version verfügbar. Dokumentation und Funktionalität können sich ändern.

So richten Sie [!DNL Azure Data Lake Storage] (ADLS)-Authentifizierung für Ihr Ziel konfigurieren Sie die `customerAuthenticationConfigurations` -Parameter in der `/destinations` Endpunkt wie unten gezeigt:

```json
   "customerAuthenticationConfigurations":[
     {
        "authType":"AZURE_SERVICE_PRINCIPAL"
     }
  ]
```

## (Beta) [!DNL SFTP] Authentifizierung mit [!DNL SSH] key {#sftp-ssh}

[!DNL SFTP] Authentifizierung mit [!DNL SSH] -Schlüssel wird für dateibasierte Ziele in Experience Platform unterstützt.

>[!IMPORTANT]
>
>Die dateibasierte Zielunterstützung in Adobe Experience Platform Destination SDK ist derzeit als Beta-Version verfügbar. Dokumentation und Funktionalität können sich ändern.

Um die SFTP-Authentifizierung mit dem SSH-Schlüssel für Ihr Ziel einzurichten, konfigurieren Sie die `customerAuthenticationConfigurations` -Parameter in der `/destinations` Endpunkt wie unten gezeigt:

```json
   "customerAuthenticationConfigurations":[
      {
         "authType":"SFTP_WITH_SSH_KEY"
      }
   ]
```

## (Beta) [!DNL SFTP] Authentifizierung mit Kennwort {#sftp-password}

[!DNL SFTP] Die Authentifizierung mit Kennwort wird für dateibasierte Ziele in Experience Platform unterstützt.

>[!IMPORTANT]
>
>Die dateibasierte Zielunterstützung in Adobe Experience Platform Destination SDK ist derzeit als Beta-Version verfügbar. Dokumentation und Funktionalität können sich ändern.

Um die SFTP-Authentifizierung mit einem Kennwort für Ihr Ziel einzurichten, konfigurieren Sie die `customerAuthenticationConfigurations` -Parameter in der `/destinations` Endpunkt wie unten gezeigt:

```json
   "customerAuthenticationConfigurations":[
      {
         "authType":"SFTP_WITH_PASSWORD"
      }
   ]
```

## [!DNL OAuth 2] Authentifizierung {#oauth2}

[!DNL OAuth 2] -Authentifizierung wird für Streaming-Ziele in Experience Platform unterstützt.

Informationen zum Einrichten der verschiedenen unterstützten OAuth 2-Flüsse sowie zur benutzerdefinierten OAuth 2-Unterstützung finden Sie in der Dokumentation zur Destination SDK unter [OAuth 2-Authentifizierung](./oauth2-authentication.md).


## Verwendung der `/credentials` API-Endpunkt {#when-to-use}

>[!IMPORTANT]
>
>In den meisten Fällen *nicht* die `/credentials` API-Endpunkt. Stattdessen können Sie die Authentifizierungsinformationen für Ihr Ziel über die `customerAuthenticationConfigurations` Parameter der `/destinations` -Endpunkt.

Die `/credentials` Der API-Endpunkt wird den Zielentwicklern für die Fälle bereitgestellt, in denen ein globales Authentifizierungssystem zwischen Adobe und Ihrem Ziel und [!DNL Platform] -Kunden müssen keine Authentifizierungsberechtigungen bereitstellen, um eine Verbindung zu Ihrem Ziel herzustellen.

In diesem Fall müssen Sie mithilfe der `/credentials` API-Endpunkt. Sie müssen auch `PLATFORM_AUTHENTICATION` im [Zielkonfiguration](./destination-configuration.md#destination-delivery). Lesen [Vorgänge bei Anmeldedaten-API-Endpunkten](./credentials-configuration-api.md) für eine vollständige Liste der Vorgänge, die Sie für die `/credentials` -Endpunkt.
