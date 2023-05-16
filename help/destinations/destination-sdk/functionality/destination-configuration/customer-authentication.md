---
description: Erfahren Sie, wie Sie einen Authentifizierungsmechanismus für Ihr Ziel einrichten und Einblicke darüber erhalten, welche Benutzer je nach ausgewählter Authentifizierungsmethode auf der Benutzeroberfläche angezeigt werden.
title: Konfiguration der Kundenauthentifizierung
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '1094'
ht-degree: 35%

---


# Konfiguration der Kundenauthentifizierung

Experience Platform bietet eine große Flexibilität bei den Authentifizierungsprotokollen, die Partnern und Kunden zur Verfügung stehen. Sie können Ihr Ziel so konfigurieren, dass es alle Authentifizierungsmethoden unterstützt, die dem Branchenstandard entsprechen, z. B. [!DNL OAuth2], Authentifizierung von Trägertoken, Kennwortauthentifizierung und vieles mehr.

Auf dieser Seite wird beschrieben, wie Sie Ihr Ziel mithilfe Ihrer bevorzugten Authentifizierungsmethode einrichten. Basierend auf der Authentifizierungskonfiguration, die Sie beim Erstellen Ihres Ziels verwenden, werden Kunden beim Herstellen einer Verbindung zum Ziel in der Experience Platform-Benutzeroberfläche unterschiedliche Arten von Authentifizierungsseiten angezeigt.

Informationen dazu, wo diese Komponente in eine mit Destination SDK erstellte Integration passt, finden Sie im Diagramm im [Konfigurationsoptionen](../configuration-options.md) Dokumentation oder sehen Sie die folgenden Übersichtsseiten zur Zielkonfiguration:

* [Verwenden des Destination SDK zum Konfigurieren eines Streaming-Ziels](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Verwenden des Destination SDK zum Konfigurieren eines dateibasierten Ziels](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

Bevor Kunden Daten aus Platform in Ihr Ziel exportieren können, müssen sie eine neue Verbindung zwischen Experience Platform und Ihrem Ziel herstellen, indem sie die im Abschnitt [Zielverbindung](../../../ui/connect-destination.md) Tutorial.

Wann [Erstellen eines Ziels](../../authoring-api/destination-configuration/create-destination-configuration.md) durch Destination SDK, `customerAuthenticationConfigurations` definiert, was Kunden sehen im [Authentifizierungsbildschirm](../../../ui/connect-destination.md#authenticate). Abhängig vom Zielauthentifizierungstyp müssen Kunden verschiedene Authentifizierungsdetails angeben, z. B.:

* Für Ziele, die [einfache Authentifizierung](#basic)müssen Benutzer einen Benutzernamen und ein Kennwort direkt auf der Authentifizierungsseite der Experience Platform-Benutzeroberfläche angeben.
* Für Ziele, die [Bearer-Authentifizierung](#bearer), müssen Benutzer ein Bearer-Token bereitstellen.
* Für Ziele, die [OAuth2-Authentifizierung](#oauth2), werden Benutzer zur Anmeldeseite Ihres Ziels weitergeleitet, wo sie sich mit ihren Anmeldeinformationen anmelden können.
* Für [Amazon S3](#s3) Ziele, müssen Benutzer ihre [!DNL Amazon S3] Zugriffsschlüssel und geheimer Schlüssel.
* Für [Azure Blob](#blob) Ziele, müssen Benutzer ihre [!DNL Azure Blob] Verbindungszeichenfolge.

Sie können Details zur Kundenauthentifizierung über die `/authoring/destinations` -Endpunkt. Detaillierte Beispiele für API-Aufrufe, in denen Sie die auf dieser Seite angezeigten Komponenten konfigurieren können, finden Sie auf den folgenden API-Referenzseiten.

* [Erstellen einer Zielkonfiguration](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Zielkonfiguration aktualisieren](../../authoring-api/destination-configuration/update-destination-configuration.md)

In diesem Artikel werden alle unterstützten Konfigurationen für die Kundenauthentifizierung beschrieben, die Sie für Ihr Ziel verwenden können, und es wird gezeigt, welche Experience Platformen in der Benutzeroberfläche angezeigt werden, basierend auf der Authentifizierungsmethode, die Sie für Ihr Ziel eingerichtet haben.

>[!IMPORTANT]
>
>Für die Konfiguration der Kundenauthentifizierung müssen Sie keine Parameter konfigurieren. Sie können die auf dieser Seite angezeigten Snippets kopieren und in Ihre API-Aufrufe einfügen, wenn Sie [erstellen](../../authoring-api/destination-configuration/create-destination-configuration.md) oder [Aktualisieren](../../authoring-api/destination-configuration/update-destination-configuration.md) eine Zielkonfiguration erstellen und Ihren Benutzern wird der entsprechende Authentifizierungsbildschirm in der Platform-Benutzeroberfläche angezeigt.

>[!IMPORTANT]
>
>Alle von Destination SDK unterstützten Parameternamen und Werte sind **Groß-/Kleinschreibung**. Um Fehler bei der Groß-/Kleinschreibung zu vermeiden, verwenden Sie bitte die Parameternamen und -werte genau wie in der Dokumentation dargestellt.

## Unterstützte Integrationstypen {#supported-integration-types}

Die nachstehende Tabelle beschreibt ausführlich, welche Integrationstypen die auf dieser Seite beschriebenen Funktionen unterstützen.

| Integrationstyp | Unterstützt Funktionen |
|---|---|
| Echtzeit-Integrationen (Streaming) | Ja |
| Dateibasierte (Batch-)Integrationen | Ja |

## Konfiguration der Authentifizierungsregel {#authentication-rule}

Wenn Sie eine der auf dieser Seite beschriebenen Kundenauthentifizierungskonfigurationen verwenden, legen Sie immer die `authenticationRule` Parameter in [Zielversand](destination-delivery.md) nach `"CUSTOMER_AUTHENTICATION"`, wie unten dargestellt.

```json {line-numbers="true" highlight="4"
{
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ]
}
```

## Einfache Authentifizierung {#basic}

Die grundlegende Authentifizierung wird bei Echtzeit-Integrationen (Streaming) in Experience Platform unterstützt.

Wenn Sie den grundlegenden Authentifizierungstyp konfigurieren, müssen Benutzer einen Benutzernamen und ein Kennwort eingeben, um eine Verbindung zu Ihrem Ziel herzustellen.

![UI-Rendering mit einfacher Authentifizierung](../../assets/functionality/destination-configuration/basic-authentication-ui.png)

Um eine einfache Authentifizierung für Ihr Ziel einzurichten, konfigurieren Sie die `customerAuthenticationConfigurations` über die `/destinations` Endpunkt wie unten gezeigt:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"BASIC"
   }
]
```

## Bearer-Authentifizierung {#bearer}

Wenn Sie den Bearer-Authentifizierungstyp konfigurieren, müssen Benutzer das Bearer-Token eingeben, das sie von Ihrem Ziel erhalten.

![UI-Rendering mit Bearer-Authentifizierung](../../assets/functionality/destination-configuration/bearer-authentication-ui.png)

Um die Authentifizierung des Trägertyps für Ihr Ziel einzurichten, konfigurieren Sie die `customerAuthenticationConfigurations` über die `/destinations` Endpunkt wie unten gezeigt:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"BEARER"
   }
]
```

## OAuth 2-Authentifizierung {#oauth2}

Benutzer wählen **[!UICONTROL Mit Ziel verbinden]** aus, um den OAuth 2-Authentifizierungsfluss für Ihr Ziel auszulösen (siehe folgendes Beispiel für das Ziel „Twitter Custom Audiences“). Detaillierte Informationen zum Konfigurieren der OAuth 2-Authentifizierung für Ihren Ziel-Endpunkt finden Sie in der entsprechenden [Authentifizierungsseite für Destination SDK OAuth 2](oauth2-authentication.md).

![UI-Rendering mit OAuth 2-Authentifizierung](../../assets/functionality/destination-configuration/oauth2-authentication-ui.png)

So richten Sie [!DNL OAuth2] Authentifizierung für Ihr Ziel konfigurieren Sie die `customerAuthenticationConfigurations` über die `/destinations` Endpunkt wie unten gezeigt:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"OAUTH2"
   }
]
```

## Amazon S3-Authentifizierung {#s3}

Die [!DNL Amazon S3]-Authentifizierung wird für dateibasierte Ziele in Experience Platform unterstützt.

Wenn Sie den Authentifizierungstyp Amazon S3 konfigurieren, müssen Benutzer ihre S3-Anmeldeinformationen eingeben.

![Darstellung der Benutzeroberfläche mit S3-Authentifizierung](../../assets/functionality/destination-configuration/s3-authentication-ui.png)

So richten Sie [!DNL Amazon S3] Authentifizierung für Ihr Ziel konfigurieren Sie die `customerAuthenticationConfigurations` über die `/destinations` Endpunkt wie unten gezeigt:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"S3"
   }
]
```

## Azure Blob-Authentifizierung  {#blob}

Die [!DNL Azure Blob Storage]-Authentifizierung wird für dateibasierte Ziele in Experience Platform unterstützt.

Wenn Sie den Authentifizierungstyp Azure Blob konfigurieren, müssen Benutzer die Verbindungszeichenfolge eingeben.

![Darstellung der Benutzeroberfläche mit Blob-Authentifizierung](../../assets/functionality/destination-configuration/blob-authentication-ui.png)

Um die [!DNL Azure Blob]-Authentifizierung für Ihr Ziel einzurichten, konfigurieren Sie den `customerAuthenticationConfigurations`-Parameter im `/destinations`-Endpunkt wie unten angezeigt:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_CONNECTION_STRING"
   }
]
```

## [!DNL Azure Data Lake Storage]-Authentifizierung {#adls}

Die [!DNL Azure Data Lake Storage]-Authentifizierung wird für dateibasierte Ziele in Experience Platform unterstützt.

Wenn Sie die [!DNL Azure Data Lake Storage] Authentifizierungstyp, müssen Benutzer die Prinzipalanmeldeinformationen von Azure Service und ihre Mandanteninformationen eingeben.

![Benutzeroberflächen-Rendering mit [!DNL Azure Data Lake Storage] Authentifizierung](../../assets/functionality/destination-configuration/adls-authentication-ui.png)

Um die [!DNL Azure Data Lake Storage] (ADLS)-Authentifizierung für Ihr Ziel einzurichten, konfigurieren Sie den `customerAuthenticationConfigurations`-Parameter im `/destinations`-Endpunkt, wie unten angezeigt:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_SERVICE_PRINCIPAL"
   }
]
```

## SFTP mit Passwortauthentifizierung

Die [!DNL SFTP]-Authentifizierung mit Passwort wird für dateibasierte Ziele in Experience Platform unterstützt.

Wenn Sie den SFTP-Authentifizierungstyp mit Passwort konfigurieren, müssen Benutzer den SFTP-Benutzernamen und das Passwort sowie die SFTP-Domain und den Port eingeben (der standardmäßige Port ist 22).

![Darstellung der Benutzeroberfläche mit SFTP mit Passwortauthentifizierung](../../assets/functionality/destination-configuration/sftp-password-authentication-ui.png)

Um die SFTP-Authentifizierung mit einem Kennwort für Ihr Ziel einzurichten, konfigurieren Sie den `customerAuthenticationConfigurations`-Parameter im `/destinations`-Endpunkt, wie unten angezeigt:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_PASSWORD"
   }
]
```

## SFTP mit SSH-Schlüsselauthentifizierung

Die [!DNL SFTP]-Authentifizierung mit dem [!DNL SSH]-Schlüssel wird für dateibasierte Ziele in Experience Platform unterstützt.

Wenn Sie den Authentifizierungstyp SFTP mit SSH-Schlüssel konfigurieren, müssen Benutzer den SFTP-Benutzernamen und SSH-Schlüssel sowie die SFTP-Domain und den Port eingeben (der standardmäßige Port ist 22).

![Darstellung der Benutzeroberfläche mit SFTP mit SSH-Schlüsselauthentifizierung](../../assets/functionality/destination-configuration/sftp-key-authentication-ui.png)

Um die SFTP-Authentifizierung mit dem SSH-Schlüssel für Ihr Ziel einzurichten, konfigurieren Sie den `customerAuthenticationConfigurations`-Parameter im `/destinations`-Endpunkt, wie unten angezeigt:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_SSH_KEY"
   }
]
```

## [!DNL Google Cloud Storage]-Authentifizierung {#gcs}

Die [!DNL Google Cloud Storage]-Authentifizierung wird für dateibasierte Ziele in Experience Platform unterstützt.

Wenn Sie die [!DNL Google Cloud Storage] Authentifizierungstyp: Benutzer müssen ihre [!DNL Google Cloud Storage] [!UICONTROL Zugriffsschlüssel-ID] und [!UICONTROL geheimer Zugriffsschlüssel].

![Benutzeroberflächen-Rendering mit Google Cloud Storage-Authentifizierung](../../assets/functionality/destination-configuration/google-cloud-storage-ui.png)

Um die [!DNL Google Cloud Storage]-Authentifizierung für Ihr Ziel einzurichten, konfigurieren Sie den `customerAuthenticationConfigurations`-Parameter im `/destinations`-Endpunkt wie unten angezeigt:

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"GOOGLE_CLOUD_STORAGE"
   }
]
```

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Artikels sollten Sie besser verstehen, wie Sie die Benutzerauthentifizierung für Ihre Zielplattform konfigurieren können.

Weitere Informationen zu den anderen Zielkomponenten finden Sie in den folgenden Artikeln:

* [OAuth 2-Authentifizierung](oauth2-authentication.md)
* [Benutzerdefinierte Datenfelder](customer-data-fields.md)
* [Benutzeroberflächenattribute](ui-attributes.md)
* [Schemakonfiguration](schema-configuration.md)
* [Identitäts-Namespace-Konfiguration](identity-namespace-configuration.md)
* [Unterstützte Zuordnungskonfigurationen](supported-mapping-configurations.md)
* [Zielbereitstellung](destination-delivery.md)
* [Konfiguration von Zielgruppen-Metadaten](audience-metadata-configuration.md)
* [Aggregationsrichtlinie](aggregation-policy.md)
* [Batch-Konfiguration](batch-configuration.md)
* [Historische Profilqualifikationen](historical-profile-qualifications.md)