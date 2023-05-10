---
description: Der Zieldienst in Adobe Experience Platform verwendet Konfigurationsendpunkte für verschiedene Komponenten, die die Zielfunktion aufbauen. Gemeinsam ermöglichen diese Komponenten der Experience Platform, eine Verbindung zu Zielpartnern herzustellen, benutzerdefinierte Nachrichten zu senden und Profildaten im gesamten digitalen Ökosystem zu aktivieren.
title: Konfigurationsoptionen in Destination SDK
exl-id: 8890c70a-cdb9-4b9d-aa81-affe72b1fdc5
source-git-commit: 9b4c7da5aa02ae27608c2841b1d825445ac3015e
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 7%

---

# Konfigurationsoptionen in Destination SDK

## Übersicht {#overview}

Der Zieldienst in Adobe Experience Platform verwendet Konfigurationsendpunkte für verschiedene Komponenten, die die Zielfunktion aufbauen. Gemeinsam ermöglichen diese Komponenten die Experience Platform, eine Verbindung zu Zielplattformen herzustellen, benutzerdefinierte Nachrichten zu senden, benutzerdefinierte Dateien zu exportieren und Profildaten im gesamten digitalen Ökosystem zu aktivieren. Die in Adobe Experience Platform Destination SDK verwendeten Konfigurationen sind:

* **Zielkonfiguration**: Enthält grundlegende Informationen über Ihr Ziel. Diese Konfiguration umfasst die Identitätstypen, die Ihr Ziel unterstützen kann, das gewünschte Format der exportierten Dateien (für dateibasierte Ziele) und verschiedene Benutzeroberflächenattribute für Ihre Zielkarte in der Adobe Experience Platform-Benutzeroberfläche.
* **Server-, Datei- und Vorlagenspezifikationen**: Verbindet Informationen zu Ihren Serverspezifikationen und der von Adobe verwendeten Vorlage zum Übermitteln von Payloads an Ihr Ziel. Bei dateibasierten Zielen enthält diese Konfiguration auch die unterstützten Dateiformatierungs- und Komprimierungsformate für Ihr Ziel.
   * **Serverspezifikationen**: Eine Konfigurationsvorlage, die Informationen zum Speicherort oder HTTP-Endpunkt enthält, an den Daten gesendet werden.&quot;
   * **Dateispezifikationen**: Eine Konfigurationsvorlage mit den Dateiformatierungs- und Komprimierungsoptionen für Ihr Batch-Ziel.
   * **Vorlagenspezifikationen**: In dieser Vorlage können Sie definieren, wie Sie Profilattributfelder zwischen dem XDM-Schema und dem Format umwandeln können, das Ihre Plattform unterstützt. Detaillierte Informationen zu unterstützten Vorlagensprachen, Nachrichtenformaten und den Informationen, die die Adobe für die Einrichtung der Integration mit Ihrer Plattform benötigt, finden Sie unter [Nachrichtenformat](./message-format.md).
* **Authentifizierungskonfiguration**: Diese Einstellungen definieren, wie Adobe Experience Platform-Benutzer eine Verbindung zu Ihrem Ziel herstellen.
* **Konfiguration von Zielgruppen-Metadaten**: Mit diesem Konfigurations-Endpunkt können Sie konfigurieren, wie Zielgruppen/Segmente programmgesteuert in Ihrem Ziel erstellt, aktualisiert oder gelöscht werden. Bei Batch-Zielen können Sie eine Benachrichtigung einrichten, sobald Dateien erfolgreich an Ihr Ziel gesendet wurden.

![Diagramm, das die Endpunkte der Destination SDK-Konfiguration und deren gemeinsame Verwendung anzeigt.](./assets/self-service-configuration.png)

## Siehe auch: {#related-links}

Auf den folgenden Seiten finden Sie weitere Details zu den in Destination SDK verfügbaren Funktionen und Konfigurationsoptionen sowie zu den entsprechenden API-Vorgängen, die Sie ausführen können.

| Beschreibung der Funktionen (Streaming-Ziele) | Funktionsbeschreibung (Batch-Ziele) | API-Referenz |
|--- |--- |--- |
| [Konfigurationsoptionen für Ziele](./destination-configuration.md) | [Dateibasierte Zielkonfigurationsoptionen](/help/destinations/destination-sdk/file-based-destination-configuration.md) | [API-Endpunktvorgänge für Ziele](./destination-configuration-api.md) |
| [Server- und Vorlagenspezifikationen](./server-and-template-configuration.md) | [Server- und Dateikonfigurationsspezifikationen](/help/destinations/destination-sdk/server-and-file-configuration.md) | [API-Endpunktvorgänge für Zielserver](./destination-server-api.md) |
| [Authentifizierungskonfiguration](./authentication-configuration.md) | Entspricht Streaming-Zielen. | Sie können die Authentifizierungsinformationen für Ihr Ziel über die `customerAuthenticationConfigurations`-Parameter des `/destinations`-Endpunkts konfigurieren. Weitere Informationen unter [Streaming](/help/destinations/destination-sdk/destination-configuration.md#customer-authentication-configurations) und [Batch](/help/destinations/destination-sdk/file-based-destination-configuration.md#customer-authentication-configurations) Ziele. |
| [Verwaltung von Zielgruppen-Metadaten](./audience-metadata-management.md) | Wie beim Streaming. Siehe [dateibasiertes Beispiel](/help/destinations/destination-sdk/audience-metadata-management.md#example-file-based) , um zu verstehen, wie Zielgruppen-Metadaten in einem Batch-Zielkontext verwendet werden können. | [API-Vorgänge für Zielgruppen-Metadaten-Endpunkte](./audience-metadata-api.md) |
| [OAuth 2-Konfiguration](./oauth2-authentication.md) | Dasselbe wie für Streaming-Ziele | Konfigurieren Sie mithilfe des `customerAuthenticationConfigurations` -Parameter in der [/destinations-API-Endpunkt](./destination-configuration-api.md). |
| [Nachrichtenformat](./message-format.md) | – | – |
| [Testwerkzeuge für Streaming-Ziele](./test-destination.md) | [Testwerkzeuge für dateibasierte Ziele](/help/destinations/destination-sdk/file-based-destination-testing-overview.md) | [API-Vorgänge für Zieltests](./destination-testing-api.md) |
| [Zielveröffentlichung](./configure-destination-instructions.md#publish-destination) | Dasselbe wie für Streaming-Ziele | [API-Vorgänge für die Zielveröffentlichung](./destination-publish-api.md) |

{style="table-layout:auto"}

## Nächste Schritte {#next-steps}

Durch Lesen dieses Artikels erhalten Sie jetzt einen allgemeinen Überblick über die Funktionen, die von Destination SDK bereitgestellt werden, und darüber, welche Seiten Sie lesen können, um weitere Informationen zu bestimmten Konfigurationen zu erhalten. Als Nächstes können Sie die Handbücher lesen, die alle Schritte zum [Streaming konfigurieren](/help/destinations/destination-sdk/configure-destination-instructions.md) oder [dateibasiertes Ziel](/help/destinations/destination-sdk/configure-file-based-destination-instructions.md) durch Verwendung von Destination SDK.
