---
description: Der Ziel-Service in Adobe Experience Platform verwendet Konfigurationsendpunkte für verschiedene Komponenten, die die Zielfunktion aufbauen. Erfahren Sie, wie diese Komponenten zusammen es Experience Platform ermöglichen, eine Verbindung zu Zielpartnern herzustellen, benutzerdefinierte Nachrichten zu senden und Profildaten im gesamten digitalen Ökosystem zu aktivieren.
title: Konfigurationsoptionen in Destination SDK
source-git-commit: 3f31a54c0cf329d374808dacce3fac597a72aa11
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 95%

---


# Konfigurationsoptionen in Destination SDK

Der Ziel-Service in Adobe Experience Platform verwendet Konfigurationsendpunkte für verschiedene Komponenten, die die Zielfunktion aufbauen.

Gemeinsam ermöglichen diese Komponenten es Experience Platform, eine Verbindung zu Zielplattformen herzustellen, benutzerdefinierte Nachrichten zu senden, benutzerdefinierte Dateien zu exportieren und Profildaten im gesamten digitalen Ökosystem zu aktivieren.

Das folgende Diagramm zeigt einen allgemeinen Überblick über die Komponenten, die Sie über Destination SDK konfigurieren können, um Ihr eigenes Ziel zu erstellen. Diese Komponenten werden weiter unten beschrieben.

![Diagramm mit den Destination SDK-Komponenten, den Konfigurations-Endpunkten und den von ihnen unterstützten Vorgängen.](../assets/functionality/destination-sdk-components-diagram.png)

## Server-Konfiguration {#server-configuration}

Die Ziel-Server-Konfiguration verknüpft Informationen zu Ihren Server-Spezifikationen und der von Adobe verwendeten Vorlage zum Bereitstellen von Payloads an Ihr Ziel.

Hier geben Sie beispielsweise die API-Endpunkte auf Ihrer Seite an, mit denen sich Experience Platform verbinden muss, sowie die Kopfzeilen und das Format der von Platform durchgeführten API-Aufrufe.

Bei dateibasierten Zielen enthält diese Konfiguration auch die unterstützten Dateiformatierungs- und Komprimierungsformate für Ihr Ziel. Sie können die im Folgenden beschriebenen Funktionen über den [Endpunkt destination-servers](../authoring-api/destination-server/create-destination-server.md)konfigurieren.

* [Server-Spezifikationen](destination-server/server-specs.md): Eine Konfigurationsvorlage, die Informationen zum Speicherort oder HTTP-Endpunkt enthält, an den Daten gesendet werden.
* [Vorlagenspezifikationen](destination-server/templating-specs.md): In dieser Vorlage können Sie definieren, wie die HTTP-API-Anfrage an Ihren Endpunkt strukturiert werden soll, einschließlich der Transformation von Profilattributfeldern zwischen dem XDM-Schema und dem Format, das Ihre Plattform unterstützt. Verwenden Sie diese Informationen zusammen mit der Dokumentation zum [Nachrichtenformat](destination-server/message-format.md).
* [Nachrichtenformat](destination-server/message-format.md): In diesem Abschnitt werden ausführliche Informationen zu unterstützten Vorlagensprachen, Nachrichtenformaten und den Informationen behandelt, die Adobe für die Einrichtung der Integration mit Ihrer Plattform benötigt. Verwenden Sie diese Informationen zusammen mit der Dokumentation zu [Vorlagenspezifikationen](destination-server/templating-specs.md).
* [Dateispezifikationen](destination-server/file-formatting.md): Eine Konfigurationsvorlage mit den Dateiformatierungs- und Komprimierungsoptionen für Ihr Batch-Ziel.

## Zielkonfiguration {#destination-configuration}

Dieser Konfigurationsendpunkt enthält grundlegende und erweiterte Informationen zu Ihrem Ziel. Hier geben Sie beispielsweise die Identitätstypen an, die Ihr Ziel unterstützen kann, das gewünschte Format der exportierten Dateien (für dateibasierte Ziele) und verschiedene Benutzeroberflächenattribute für Ihre Zielkarte in der Adobe Experience Platform-Benutzeroberfläche an.

Weitere Informationen zu den einzelnen Zielkonfigurationskomponenten finden Sie in der folgenden Dokumentation. Sie können die im Folgenden beschriebenen Funktionen über den [Endpunkt „destinations“](../authoring-api/destination-configuration/create-destination-configuration.md)konfigurieren.

* [Konfiguration der Kundenauthentifizierung](destination-configuration/customer-authentication.md): Wählen Sie den Authentifizierungsmechanismus aus, den Experience Platform für die Verbindung mit Ihrem Ziel verwenden sollte. Diese Konfiguration erzeugt die Seite [Neues Ziel konfigurieren](../../ui/connect-destination.md) in der Benutzeroberfläche von Experience Platform, auf der Benutzerinnen und Benutzer Experience Platform mit ihren Konten und mit Ihrem Ziel verbinden.
* [OAuth2-Authentifizierung](destination-configuration/oauth2-authentication.md): Erfahren Sie mehr über alle [!DNL OAuth2] von Destination SDK unterstützten Authentifizierungsabläufe und erhalten Sie Anweisungen zum Einrichten der [!DNL OAuth2] -Authentifizierung für Ihr Ziel.
* [Kundendatenfelder](destination-configuration/customer-data-fields.md): Erfahren Sie, wie Sie Eingabefelder in der Experience Platform-Benutzeroberfläche erstellen, mit denen Ihre Benutzerinnen und Benutzer verschiedene Informationen angeben können, die für die Verbindung und den Export von Daten zu Ihrem Ziel relevant sind.
* [Benutzeroberflächenattribute](destination-configuration/ui-attributes.md): Erfahren Sie, wie Sie die Attribute der Benutzeroberfläche, wie z. B. den Dokumentations-Link, die Kategorie der Zielkarte sowie den Verbindungstyp und die Häufigkeit der Zielverbindungen für Ziele konfigurieren, die mit Destination SDK erstellt wurden.
* [Schemakonfiguration](destination-configuration/schema-configuration.md): Erfahren Sie, wie Sie das Zielschema Ihres Ziels definieren, dem Benutzerinnen und Benutzer Profilattribute und Identitäten zuordnen können.
* [Konfiguration von Identity-Namespaces](destination-configuration/identity-namespace-configuration.md): Erfahren Sie, wie Sie die von Ihrem Ziel unterstützten Identitäten konfigurieren. Durch diese Konfiguration werden auch die Zielidentitäten im [Zuordnungsschritt](../../ui/activate-segment-streaming-destinations.md#mapping) der Experience Platform-Benutzeroberfläche ausgefüllt, in dem Benutzerinnen und Benutzer Identitäten und Attribute aus ihren XDM-Schemata dem Schema in Ihrem Ziel zuordnen.
* [Zielversand](destination-configuration/destination-delivery.md): Erfahren Sie, wie Sie konfigurieren können, wohin genau die exportierten Daten gehen und welche Authentifizierungsregel an dem Ort verwendet wird, an dem die Daten landen.
* [Konfiguration von Zielgruppen-Metadaten](destination-configuration/audience-metadata-configuration.md): Erfahren Sie, wie Zielgruppen-Metadaten wie Zielgruppennamen oder IDs von Experience Platform und Ihrem Ziel gemeinsam genutzt werden sollten.
* [Aggregationsrichtlinie](destination-configuration/aggregation-policy.md): Erfahren Sie, wie Sie eine Aggregationsrichtlinie einrichten, um zu bestimmen, wie HTTP-Anfragen an Ihr Ziel gruppiert und in Batches eingesetzt werden sollen.
* [Batch-Konfiguration](destination-configuration/batch-configuration.md): Richten Sie verschiedene Einstellungen für die Dateibenennung und Exportplanung ein, die Benutzerinnen und Benutzern beim Herstellen einer Verbindung zu Ihrem Ziel in der Benutzeroberfläche von Experience Platform zur Verfügung stehen.
* [Historische Profilqualifikationen](destination-configuration/historical-profile-qualifications.md): Erfahren Sie mehr über die historischen Profilqualifikationen, die von mit Destination SDK erstellten Zielen unterstützt werden.

## Konfiguration von Zielgruppen-Metadaten {#audience-metadata-configuration}

Mit dieser Komponente können Sie konfigurieren, wie Zielgruppen programmgesteuert in Ihrem Ziel erstellt, aktualisiert oder gelöscht werden. Bei dateibasierten Zielen können Sie eine Benachrichtigung einrichten, sobald Dateien erfolgreich an Ihr Ziel gesendet wurden. Sie können diese Funktion über den [Endpunkt „audience-templates“](../metadata-api/create-audience-template.md) konfigurieren.

## Nächste Schritte {#next-steps}

Durch das Lesen dieses Artikels haben Sie jetzt einen allgemeinen Überblick über die Funktionen, die von Destination SDK bereitgestellt werden, und darüber, welche Seiten Sie lesen können, um weitere Informationen zu bestimmten Konfigurationen zu erhalten. Als Nächstes können Sie die Handbücher lesen, die alle Schritte zum [Konfigurieren eines Streaming-Ziels](../guides/configure-destination-instructions.md) oder eines [dateibasierten Ziels](../guides/configure-file-based-destination-instructions.md) durch Verwendung von Destination SDK enthalten.
