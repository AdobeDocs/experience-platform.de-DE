---
description: Verwenden Sie die unterstützten Authentifizierungskonfigurationen im Adobe Experience Platform Destination SDK, um Benutzer zu authentifizieren und Daten für Ihren Zielendpunkt zu aktivieren.
title: Authentifizierungskonfiguration
exl-id: 33eaab24-f867-4744-b424-4ba71727373c
source-git-commit: 92bca3600d854540fd2badd925e453fba41601a7
workflow-type: ht
source-wordcount: '564'
ht-degree: 100%

---

# Authentifizierungskonfiguration {#credentials}

## Unterstützte Authentifizierungstypen {#supported-authentication-types}

Die von Ihnen gewählte Authentifizierungskonfiguration bestimmt, wie sich Experience Platform in der Platform-Benutzeroberfläche gegenüber Ihrem Ziel authentifiziert.

Adobe Experience Platform Destination SDK unterstützt mehrere Authentifizierungstypen:

* Bearer-Authentifizierung
* (Beta) Amazon S3-Authentifizierung
* (Beta) Azure-Verbindungszeichenfolge
* (Beta) Azure-Service-Prinzipal
* (Beta) SFTP mit SSH-Schlüssel
* (Beta) SFTP mit Passwort
* OAuth 2 mit Autorisierungs-Code
* OAUth 2 mit Passwortgewährung
* OAuth 2 mit Gewährung von Client-Anmeldeinformationen

Sie können die Authentifizierungsinformationen für Ihr Ziel über die `customerAuthenticationConfigurations`-Parameter des `/destinations`-Endpunkts konfigurieren.

In den folgenden Abschnitten finden Sie Details zur Authentifizierungskonfiguration für jeden Zieltyp:

* [Authentifizierungskonfigurationen für Streaming-Ziele](destination-configuration.md#customer-authentication-configurations)
* [Authentifizierungskonfigurationen für dateibasierte Ziele](file-based-destination-configuration.md#customer-authentication-configurations)

## Bearer-Authentifizierung {#bearer}

Die Trägerauthentifizierung wird für Streaming-Ziele in Experience Platform unterstützt.

Um die Authentifizierung des Trägertyps für Ihr Ziel einzurichten, konfigurieren Sie den `customerAuthenticationConfigurations`-Parameter im `/destinations`-Endpunkt, wie unten angezeigt:

```json
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ]
```

## (Beta) [!DNL Amazon S3]-Authentifizierung {#s3}

Die [!DNL Amazon S3]-Authentifizierung wird für dateibasierte Ziele in Experience Platform unterstützt.

>[!IMPORTANT]
>
>Die Unterstützung für dateibasierte Ziele im Adobe Experience Platform Destination SDK ist derzeit als Beta-Version verfügbar. Dokumentation und Funktionalität können sich ändern.

Um die Amazon S3-Authentifizierung für Ihr Ziel einzurichten, konfigurieren Sie den `customerAuthenticationConfigurations`-Parameter im `/destinations`-Endpunkt wie unten angezeigt:

```json
   "customerAuthenticationConfigurations":[
      {
         "authType":"S3"
      }
   ]
```

## (Beta) [!DNL Azure Blob Storage] {#blob}

Die [!DNL Azure Blob Storage]-Authentifizierung wird für dateibasierte Ziele in Experience Platform unterstützt.

>[!IMPORTANT]
>
>Die Unterstützung für dateibasierte Ziele im Adobe Experience Platform Destination SDK ist derzeit als Beta-Version verfügbar. Dokumentation und Funktionalität können sich ändern.

Um die [!DNL Azure Blob]-Authentifizierung für Ihr Ziel einzurichten, konfigurieren Sie den `customerAuthenticationConfigurations`-Parameter im `/destinations`-Endpunkt wie unten angezeigt:

```json
   "customerAuthenticationConfigurations":[
     {
        "authType":"AZURE_CONNECTION_STRING"
     }
  ]
```

## (Beta) [!DNL Azure Data Lake Storage] {#adls}

Die [!DNL Azure Data Lake Storage]-Authentifizierung wird für dateibasierte Ziele in Experience Platform unterstützt.

>[!IMPORTANT]
>
>Die Unterstützung für dateibasierte Ziele im Adobe Experience Platform Destination SDK ist derzeit als Beta-Version verfügbar. Dokumentation und Funktionalität können sich ändern.

Um die [!DNL Azure Data Lake Storage] (ADLS)-Authentifizierung für Ihr Ziel einzurichten, konfigurieren Sie den `customerAuthenticationConfigurations`-Parameter im `/destinations`-Endpunkt, wie unten angezeigt:

```json
   "customerAuthenticationConfigurations":[
     {
        "authType":"AZURE_SERVICE_PRINCIPAL"
     }
  ]
```

## (Beta) Die [!DNL SFTP]-Authentifizierung mit dem [!DNL SSH]-Schlüssel {#sftp-ssh}

Die [!DNL SFTP]-Authentifizierung mit dem [!DNL SSH]-Schlüssel wird für dateibasierte Ziele in Experience Platform unterstützt.

>[!IMPORTANT]
>
>Die Unterstützung für dateibasierte Ziele im Adobe Experience Platform Destination SDK ist derzeit als Beta-Version verfügbar. Dokumentation und Funktionalität können sich ändern.

Um die SFTP-Authentifizierung mit dem SSH-Schlüssel für Ihr Ziel einzurichten, konfigurieren Sie den `customerAuthenticationConfigurations`-Parameter im `/destinations`-Endpunkt, wie unten angezeigt:

```json
   "customerAuthenticationConfigurations":[
      {
         "authType":"SFTP_WITH_SSH_KEY"
      }
   ]
```

## (Beta) [!DNL SFTP]-Authentifizierung mit Passwort {#sftp-password}

Die [!DNL SFTP]-Authentifizierung mit Passwort wird für dateibasierte Ziele in Experience Platform unterstützt.

>[!IMPORTANT]
>
>Die Unterstützung für dateibasierte Ziele im Adobe Experience Platform Destination SDK ist derzeit als Beta-Version verfügbar. Dokumentation und Funktionalität können sich ändern.

Um die SFTP-Authentifizierung mit einem Kennwort für Ihr Ziel einzurichten, konfigurieren Sie den `customerAuthenticationConfigurations`-Parameter im `/destinations`-Endpunkt, wie unten angezeigt:

```json
   "customerAuthenticationConfigurations":[
      {
         "authType":"SFTP_WITH_PASSWORD"
      }
   ]
```

## [!DNL OAuth 2]-Authentifizierung {#oauth2}

Die [!DNL OAuth 2]-Authentifizierung wird für Streaming-Ziele in Experience Platform unterstützt.

Informationen zum Einrichten der verschiedenen unterstützten OAuth 2-Flüsse sowie zur benutzerdefinierten OAuth 2-Unterstützung finden Sie in der Dokumentation zu Destination SDK unter [OAuth 2-Authentifizierung](./oauth2-authentication.md).


## Verwendung des API-Endpunkts `/credentials` {#when-to-use}

>[!IMPORTANT]
>
>In den meisten Fällen ist es *nicht* erforderlich, den API-Endpunkt `/credentials` zu verwenden. Stattdessen können Sie die Authentifizierungsinformationen für Ihr Ziel über den `customerAuthenticationConfigurations`-Parameter des `/destinations`-Endpunkts konfigurieren.

Der API-Endpunkt `/credentials` wird den Entwicklern von Zielen für den Fall bereitgestellt, dass ein globales Authentifizierungssystem zwischen Adobe und Ihrem Ziel besteht und [!DNL Platform]-Kunden keine Anmeldedaten zur Authentifizierung angeben müssen, um sich mit Ihrem Ziel zu verbinden.

In diesem Fall müssen Sie mithilfe des API-Endpunkts `/credentials` ein Anmeldedatenobjekt erstellen. Sie müssen auch `PLATFORM_AUTHENTICATION` in der [Zielkonfiguration](./destination-configuration.md#destination-delivery) auswählen. Unter [Vorgänge bei Anmeldedaten-API-Endpunkten](./credentials-configuration-api.md) finden Sie eine vollständige Liste der Vorgänge, die Sie auf den Endpunkt `/credentials` anwenden können.
