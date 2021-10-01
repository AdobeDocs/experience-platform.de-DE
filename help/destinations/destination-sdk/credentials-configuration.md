---
description: Diese Konfiguration bestimmt, wie Adobe Experience Platform-Benutzer sich bei Ihrem Ziel-Endpunkt authentifizieren, um Daten zu aktivieren.
title: Konfigurationsoptionen für Anmeldedaten im Destination SDK
exl-id: 33eaab24-f867-4744-b424-4ba71727373c
source-git-commit: 6ff5fd0e80f7ca1015969e91cc23c88251509b61
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---

# Authentifizierungskonfiguration {#credentials}

## Unterstützte Authentifizierungstypen {#supported-authentication-types}

Adobe Experience Platform unterstützt mehrere Authentifizierungstypen:

* Bearer-Authentifizierung
* OAuth 2 mit Autorisierungscode
* OAU 2 mit Passwortgewährung
* OAuth 2 mit Client-Anmeldeinformationen gewähren

Lesen Sie für die verschiedenen unterstützten OAuth 2-Flüsse sowie für benutzerdefinierte OAuth 2-Unterstützung die Dokumentation zum Ziel-SDK unter [OAuth 2-Authentifizierung](./oauth2-authentication.md).

Sie können die Authentifizierungsinformationen für Ihr Ziel über die Parameter `customerAuthenticationConfigurations` des Endpunkts `/destinations` konfigurieren. Weitere Informationen finden Sie im Abschnitt [Konfigurationen für die Kundenauthentifizierung](./destination-configuration.md#customer-authentication-configurations) im Artikel zur Zielkonfiguration.

## Verwendung des API-Endpunkts `/credentials` {#when-to-use}

>[!IMPORTANT]
>
>In den meisten Fällen müssen Sie *nicht* den API-Endpunkt `/credentials` verwenden. Stattdessen können Sie die Authentifizierungsinformationen für Ihr Ziel über die Parameter `customerAuthenticationConfigurations` des Endpunkts `/destinations` konfigurieren.

Verwenden Sie den API-Endpunkt `activation/authoring/credentials` und wählen Sie `PLATFORM_AUTHENTICATION` in der [Zielkonfiguration](./destination-configuration.md#destination-delivery) aus, wenn ein globales Authentifizierungssystem zwischen Adobe und Ihrem Ziel vorhanden ist und der [!DNL Platform]-Kunde keine Authentifizierungsdaten angeben muss, um eine Verbindung mit Ihrem Ziel herzustellen. In diesem Fall müssen Sie mithilfe des API-Endpunkts `/credentials` ein Anmeldedatenobjekt erstellen. Eine vollständige Liste der Vorgänge, die Sie am Endpunkt `/credentials` ausführen können, finden Sie unter [API-Endpunktoperationen für Anmeldedaten](./credentials-configuration-api.md) .
