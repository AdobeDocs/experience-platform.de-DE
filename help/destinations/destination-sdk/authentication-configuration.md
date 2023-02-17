---
description: Verwenden Sie die unterstützten Authentifizierungskonfigurationen im Adobe Experience Platform Destination SDK, um Benutzer zu authentifizieren und Daten für Ihren Zielendpunkt zu aktivieren.
title: Authentifizierungskonfiguration
exl-id: 33eaab24-f867-4744-b424-4ba71727373c
source-git-commit: 59ac7749d788d8527da3578ec140248f7acf8e98
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 83%

---

# Authentifizierungskonfiguration {#credentials}

## Unterstützte Authentifizierungstypen {#supported-authentication-types}

Die von Ihnen gewählte Authentifizierungskonfiguration bestimmt, wie sich Experience Platform in der Platform-Benutzeroberfläche gegenüber Ihrem Ziel authentifiziert.

Adobe Experience Platform Destination SDK unterstützt mehrere Authentifizierungstypen:

* [Bearer-Authentifizierung](#bearer)
* [Einfache Authentifizierung](#basic)
* [[!DNL Amazon S3]-Authentifizierung](#s3)
* [[!DNL Azure Blob] Speicher](#blob)
* [[!DNL Azure Data Lake Storage]](#adls)
* [[!DNL Google Cloud Storage]](#gcs)
* [SFTP mit SSH-Schlüssel](#sftp-ssh)
* [SFTP mit Kennwort](#sftp-password)
* [OAuth 2 mit Autorisierungs-Code](#oauth2)
* [OAUth 2 mit Passwortgewährung](#oauth2)
* [OAuth 2 mit Gewährung von Client-Anmeldeinformationen](#oauth2)

Sie können die Authentifizierungsinformationen für Ihr Ziel über die `customerAuthenticationConfigurations`-Parameter des `/destinations`-Endpunkts konfigurieren.

In den folgenden Abschnitten finden Sie Details zur Authentifizierungskonfiguration für jeden Zieltyp:

* [Authentifizierungskonfigurationen für Streaming-Ziele](destination-configuration.md#customer-authentication-configurations)
* [Authentifizierungskonfigurationen für dateibasierte Ziele](file-based-destination-configuration.md#customer-authentication-configurations)

## Einfache Authentifizierung {#basic}

Die grundlegende Authentifizierung wird für Streaming-Ziele in Experience Platform unterstützt.

Wenn Sie den grundlegenden Authentifizierungstyp konfigurieren, müssen Benutzer einen Benutzernamen und ein Kennwort eingeben, um eine Verbindung zu Ihrem Ziel herzustellen.

Um eine einfache Authentifizierung für Ihr Ziel einzurichten, konfigurieren Sie die `customerAuthenticationConfigurations` über die `/destinations` Endpunkt wie unten gezeigt:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"BASIC"
   }
]
```

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

## [!DNL Amazon S3]-Authentifizierung {#s3}

Die [!DNL Amazon S3]-Authentifizierung wird für dateibasierte Ziele in Experience Platform unterstützt.

Um die [!DNL Amazon S3]-Authentifizierung für Ihr Ziel einzurichten, konfigurieren Sie den `customerAuthenticationConfigurations`-Parameter im `/destinations`-Endpunkt wie unten angezeigt:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"S3"
   }
]
```

## [!DNL Azure Blob Storage] {#blob}

Die [!DNL Azure Blob Storage]-Authentifizierung wird für dateibasierte Ziele in Experience Platform unterstützt.

Um die [!DNL Azure Blob]-Authentifizierung für Ihr Ziel einzurichten, konfigurieren Sie den `customerAuthenticationConfigurations`-Parameter im `/destinations`-Endpunkt wie unten angezeigt:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_CONNECTION_STRING"
   }
]
```

## [!DNL Azure Data Lake Storage] {#adls}

Die [!DNL Azure Data Lake Storage]-Authentifizierung wird für dateibasierte Ziele in Experience Platform unterstützt.

Um die [!DNL Azure Data Lake Storage] (ADLS)-Authentifizierung für Ihr Ziel einzurichten, konfigurieren Sie den `customerAuthenticationConfigurations`-Parameter im `/destinations`-Endpunkt, wie unten angezeigt:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_SERVICE_PRINCIPAL"
   }
]
```

## [!DNL Google Cloud Storage] {#gcs}

Die [!DNL Google Cloud Storage]-Authentifizierung wird für dateibasierte Ziele in Experience Platform unterstützt.

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"GOOGLE_CLOUD_STORAGE"
   }
]
```


## [!DNL SFTP] Authentifizierung mit [!DNL SSH] key {#sftp-ssh}

Die [!DNL SFTP]-Authentifizierung mit dem [!DNL SSH]-Schlüssel wird für dateibasierte Ziele in Experience Platform unterstützt.

Um die SFTP-Authentifizierung mit dem SSH-Schlüssel für Ihr Ziel einzurichten, konfigurieren Sie den `customerAuthenticationConfigurations`-Parameter im `/destinations`-Endpunkt, wie unten angezeigt:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_SSH_KEY"
   }
]
```

## [!DNL SFTP] Authentifizierung mit Kennwort {#sftp-password}

Die [!DNL SFTP]-Authentifizierung mit Passwort wird für dateibasierte Ziele in Experience Platform unterstützt.

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

Informationen zum Einrichten der verschiedenen unterstützten [!DNL OAuth 2] sowie für benutzerdefinierte [!DNL OAuth 2] Support, lesen Sie die Dokumentation zur Destination SDK unter [[!DNL OAuth 2] Authentifizierung](./oauth2-authentication.md).


## Verwendung des API-Endpunkts `/credentials` {#when-to-use}

>[!IMPORTANT]
>
>In den meisten Fällen ist es *nicht* erforderlich, den API-Endpunkt `/credentials` zu verwenden. Stattdessen können Sie die Authentifizierungsinformationen für Ihr Ziel über den `customerAuthenticationConfigurations`-Parameter des `/destinations`-Endpunkts konfigurieren.

Der API-Endpunkt `/credentials` wird den Entwicklern von Zielen für den Fall bereitgestellt, dass ein globales Authentifizierungssystem zwischen Adobe und Ihrem Ziel besteht und [!DNL Platform]-Kunden keine Anmeldedaten zur Authentifizierung angeben müssen, um sich mit Ihrem Ziel zu verbinden.

In diesem Fall müssen Sie mithilfe des API-Endpunkts `/credentials` ein Anmeldedatenobjekt erstellen. Sie müssen auch `PLATFORM_AUTHENTICATION` in der [Zielkonfiguration](./destination-configuration.md#destination-delivery) auswählen. Unter [Vorgänge bei Anmeldedaten-API-Endpunkten](./credentials-configuration-api.md) finden Sie eine vollständige Liste der Vorgänge, die Sie auf den Endpunkt `/credentials` anwenden können.
