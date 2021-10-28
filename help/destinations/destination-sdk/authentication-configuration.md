---
description: Verwenden Sie die unterstützten Authentifizierungskonfigurationen im Adobe Experience Platform Destination SDK, um Benutzer zu authentifizieren und Daten für Ihren Ziel-Endpunkt zu aktivieren.
title: Authentifizierungskonfiguration
exl-id: 33eaab24-f867-4744-b424-4ba71727373c
source-git-commit: e6d922800c17312df8529061c56d8a2deac46662
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# Authentifizierungskonfiguration {#credentials}

## Unterstützte Authentifizierungstypen {#supported-authentication-types}

Das Adobe Experience Platform Destination SDK unterstützt mehrere Authentifizierungstypen:

* Bearer-Authentifizierung
* OAuth 2 mit Autorisierungscode
* OAU 2 mit Passwortgewährung
* OAuth 2 mit Client-Anmeldeinformationen gewähren

Sie können die Authentifizierungsinformationen für Ihr Ziel über die `customerAuthenticationConfigurations` Parameter der `/destinations` -Endpunkt. Siehe Abschnitt [Abschnitt &quot;Kundenauthentifizierungskonfigurationen&quot;](./destination-configuration.md#customer-authentication-configurations) im Artikel zur Zielkonfiguration und in den folgenden Abschnitten finden Sie Details zu den Konfigurationen für jeden Authentifizierungstyp.

## Bearer-Authentifizierung {#bearer}

Um die Authentifizierung des Trägertyps für Ihre Ziele einzurichten, müssen Sie nur die `customerAuthenticationConfigurations` -Parameter in der `/destinations` Endpunkt wie unten gezeigt:

```json
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ]
```

## OAuth 2-Authentifizierung {#oauth2}

Informationen zum Einrichten der verschiedenen unterstützten OAuth 2-Flüsse sowie zur benutzerdefinierten OAuth 2-Unterstützung finden Sie in der Dokumentation zum Ziel-SDK unter [OAuth 2-Authentifizierung](./oauth2-authentication.md).


## Verwendung der `/credentials` API-Endpunkt {#when-to-use}

>[!IMPORTANT]
>
>In den meisten Fällen *nicht* die `/credentials` API-Endpunkt. Stattdessen können Sie die Authentifizierungsinformationen für Ihr Ziel über die `customerAuthenticationConfigurations` Parameter der `/destinations` -Endpunkt.

Die `/credentials` Der API-Endpunkt wird den Zielentwicklern für die Fälle bereitgestellt, in denen ein globales Authentifizierungssystem zwischen Adobe und Ihrem Ziel und [!DNL Platform] -Kunden müssen keine Authentifizierungsberechtigungen bereitstellen, um eine Verbindung zu Ihrem Ziel herzustellen.

In diesem Fall müssen Sie mithilfe der `/credentials` API-Endpunkt. Sie müssen auch `PLATFORM_AUTHENTICATION` im [Zielkonfiguration](./destination-configuration.md#destination-delivery). Lesen [Vorgänge bei Anmeldedaten-API-Endpunkten](./credentials-configuration-api.md) für eine vollständige Liste der Vorgänge, die Sie für die `/credentials` -Endpunkt.
