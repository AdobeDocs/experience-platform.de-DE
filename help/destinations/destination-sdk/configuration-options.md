---
description: Der Zieldienst in Adobe Experience Platform verwendet Konfigurationsvorlagen für verschiedene Komponenten, die die Funktion "Ziele"aufbauen. Gemeinsam ermöglichen diese Komponenten der Experience Platform, eine Verbindung zu Zielpartnern herzustellen, benutzerdefinierte Nachrichten zu senden und Profildaten im gesamten digitalen Ökosystem zu aktivieren.
seo-description: The destinations service in Adobe Experience Platform uses configuration templates for several components that build up the destinations functionality. Combined, these components allow Experience Platform to connect to destination partners, send custom messages, and activate profile data across the digital ecosystem.
seo-title: Configuration options in Destination SDK
title: Konfigurationsoptionen im Ziel-SDK
exl-id: 8890c70a-cdb9-4b9d-aa81-affe72b1fdc5
source-git-commit: 0bd57e226155ee68758466146b5d873dc4fdca29
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 2%

---

# Konfigurationsoptionen im Ziel-SDK

## Übersicht {#overview}

Der Zieldienst in Adobe Experience Platform verwendet Konfigurationsvorlagen für verschiedene Komponenten, die die Funktion &quot;Ziele&quot;aufbauen. Gemeinsam ermöglichen diese Komponenten der Experience Platform, eine Verbindung zu Zielpartnern herzustellen, benutzerdefinierte Nachrichten zu senden und Profildaten im gesamten digitalen Ökosystem zu aktivieren. Die in Adobe Experience Platform verwendeten Vorlagen sind:

* **Zielkonfiguration**: Enthält grundlegende Informationen über Ihr Ziel. Diese Konfiguration umfasst die Identitätstypen, die Ihr Ziel unterstützen kann, und verschiedene Benutzeroberflächenattribute für Ihre Zielkarte in der Adobe Experience Platform-Benutzeroberfläche.
* **Server- und Vorlagenspezifikationen**: Verbindet Informationen zu Ihren Serverspezifikationen und der von Adobe verwendeten Vorlage zum Übermitteln von Payloads an Ihr Ziel.
   * **Serverspezifikationen**: Eine Vorlage, in der Ihre Endpunktdetails gespeichert werden.
   * **Vorlagenspezifikationen**: In dieser Vorlage können Sie definieren, wie Sie Profilattributfelder zwischen dem XDM-Schema und dem Format umwandeln können, das Ihre Plattform unterstützt. Detaillierte Informationen zu unterstützten Vorlagensprachen, Nachrichtenformaten und den Informationen, die die Adobe für die Einrichtung der Integration mit Ihrer Plattform benötigt, finden Sie unter [Nachrichtenformat](./message-format.md).
* **Authentifizierungskonfiguration**: Diese Einstellungen definieren, wie Adobe Experience Platform-Benutzer eine Verbindung zu Ihrem Ziel herstellen.
* **Konfiguration von Zielgruppen-Metadaten**: Mit dieser Vorlage können Sie konfigurieren, wie Zielgruppen/Segmente programmgesteuert in Ihrem Ziel erstellt, aktualisiert oder gelöscht werden.

![Ziel-SDK-Vorlagen und -Konfigurationen](./assets/self-service-configuration.png)

## Verwandte Links {#related-links}

Auf den folgenden Seiten finden Sie weitere Details zu den im Destination SDK verfügbaren Funktionen und Konfigurationsoptionen sowie zu den entsprechenden API-Vorgängen, die Sie ausführen können.

| Beschreibung der Funktionen | API-Referenz |
|--- |--- |
| [Zielkonfiguration](./destination-configuration.md) | [API-Endpunktvorgänge für Ziele](./destination-configuration-api.md) |
| [Server- und Vorlagenspezifikationen](./server-and-template-configuration.md) | [API-Endpunktvorgänge für Zielserver](./destination-server-api.md) |
| [Authentifizierungskonfiguration](./authentication-configuration.md) | [API-Vorgänge für Anmeldeendpunkte](./credentials-configuration-api.md) |
| [Zielgruppen-Metadatenverwaltung](./audience-metadata-management.md) | [API-Vorgänge für Zielgruppen-Metadaten-Endpunkte](./audience-metadata-api.md) |
| [OAuth 2-Konfiguration](./oauth2-authentication.md) | Konfigurieren Sie mithilfe des `customerAuthenticationConfigurations` -Parameter in der [/destinations-API-Endpunkt](./destination-configuration-api.md). |
| [Nachrichtenformat](./message-format.md) | – |
| [Zieltests](./test-destination.md) | [API-Vorgänge für Zieltests](./destination-testing-api.md) |
| [Zielveröffentlichung](./configure-destination-instructions.md#publish-destination) | [API-Vorgänge für die Zielveröffentlichung](./destination-publish-api.md) |

{style=&quot;table-layout:auto&quot;}
