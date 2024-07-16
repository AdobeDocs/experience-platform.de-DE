---
solution: Experience Platform
title: Glossar zu Adobe Experience Platform Destinationen SDK
description: Verstehen Sie wichtige Terminologie bei der Erstellung eines Ziels mithilfe der Experience Platform-Destination SDK.
exl-id: d65f390a-a980-49b8-9570-840f03534553
source-git-commit: a11f469cb54421e0ca30c7c5878128e216470f7f
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 3%

---

# Glossar zu Adobe Experience Platform Destinationen SDK

In diesem Glossar werden die in der Destination SDK verwendeten Begriffe beschrieben. Weitere Adobe Experience Platform-Begriffe finden Sie im [Experience Platform-Glossar](/help/landing/glossary.md).

## A

**Aggregationsrichtlinie**: Wenn Sie konfigurieren, wie Daten an Ihr Echtzeit-Streaming-Ziel exportiert werden sollen, können Sie definieren, wie Profildaten aggregiert werden, bevor sie an Ihre Zielplattform gesendet werden. Dies hilft bei der Optimierung der Datenbereitstellung, indem Datensätze nach bestimmten Kriterien gruppiert, die Häufigkeit von API-Aufrufen reduziert und die Gesamteffizienz verbessert werden. Verschiedene Richtlinien können so konfiguriert werden, dass sie verschiedenen Zielanforderungen entsprechen und sicherstellen, dass Daten möglichst effektiv gepackt und bereitgestellt werden. [Weitere Informationen](/help/destinations/destination-sdk/functionality/destination-configuration/aggregation-policy.md).

**Konfiguration der Zielgruppen-Metadaten**: Eine Konfiguration der Zielgruppen-Metadaten bezieht sich auf die in Adobe Experience Platform definierte strukturierte Einrichtung und Parameter, die die programmgesteuerte Erstellung, Aktualisierung und Löschung von Zielgruppensegmenten in einem angegebenen Ziel ermöglichen. Diese Konfiguration verwendet Vorlagen für Zielgruppen-Metadaten, um sie an die Spezifikationen der Marketing-API der Zielplattform anzupassen. Erfahren Sie mehr über die Konfiguration der [Audience-Metadaten](/help/destinations/destination-sdk/functionality/audience-metadata-management.md) und [verfügbaren Makros](/help/destinations/destination-sdk/functionality/audience-metadata-management.md#macros).

## D

**Endpunkt der Zielkonfiguration**: Ein Endpunkt der Zielkonfiguration in Adobe Experience Platform, insbesondere der API-Endpunkt `/authoring/destinations`, wird zum Erstellen, Abrufen, Aktualisieren und Löschen von Konfigurationen für Ziele verwendet. Diese Konfigurationen definieren, wie Daten aus Adobe Experience Platform an verschiedene externe Systeme oder Ziele wie Marketing-Plattformen, Cloud-Speicher-Services oder andere Datenverarbeitungs-Endpunkte bereitgestellt werden. Lesen Sie mehr über [verfügbare Konfigurationsoptionen](/help/destinations/destination-sdk/functionality/configuration-options.md#destination-configuration) und sehen Sie sich die [Referenzdokumentation](/help/destinations/destination-sdk/authoring-api/destination-configuration/create-destination-configuration.md) an.

**Ziel-Instanz**: Eine bestimmte Einrichtung einer Zielkonfiguration in Adobe Experience Platform, die über die Experience Platform-Benutzeroberfläche erstellt und verwaltet wird. Es enthält alle erforderlichen Parameter und Anmeldeinformationen zum Verbinden und Senden von Daten an das Ziel. Nachdem Sie die Verbindung zu Ihrem Ziel hergestellt haben, können Sie die Kennung der Zielinstanz abrufen, wenn [eine Verbindung zu Ihrem Ziel durchsuchen](/help/destinations/ui/destination-details-page.md).

![UI-Bild, wie Sie die Ziel-Instanz-ID abrufen](/help/destinations/destination-sdk/assets/testing-api/get-destination-instance-id.png)

## P

**[!DNL Pebble]template**: Mit einer [!DNL Pebble] -Vorlage können aus Adobe Experience Platform exportierte Daten in das für die Zielplattform erforderliche Format umgewandelt werden. Es verwendet die Vorlagensprache [!DNL Pebble], die eine dynamische Datenumwandlung durch Funktionen wie `filter`, `for`, `if` und `set` ermöglicht. Adobe Experience Platform enthält zusätzliche benutzerdefinierte Funktionen wie `addedSegments` und `removedSegments`. Diese Vorlagen helfen bei der Formatierung von Datenelementen wie Zeitstempeln und Zielgruppenmitgliedschaften, um die Spezifikationen des Ziels zu erfüllen. Weitere Informationen zu [hier](/help/destinations/destination-sdk/functionality/destination-server/message-format.md) und [hier](/help/destinations/destination-sdk/functionality/destination-server/templating-specs.md).

**Privates Ziel**: Benutzerdefinierte Integrationen, die von einzelnen Adobe Experience Platform-Kunden erstellt wurden. Diese sind auf spezifische Geschäftsanforderungen zugeschnitten und stehen nur innerhalb der Organisation des Kunden zur Verfügung und bieten Flexibilität bei der Datenexportkonfiguration. Private Ziele stehen nur Real-Time CDP Ultimate-Kunden zur Verfügung. [Weitere Informationen](/help/destinations/destination-sdk/overview.md#productized-custom-integrations).

**Öffentliches Ziel**: Eine öffentlich verfügbare Integration im Adobe Experience Platform-Katalog. Diese Ziele sind standardisiert, gebrandmarkt und vereinfachen die Kundeneinrichtung durch Bereitstellung vorkonfigurierter Parameter. Sie stehen allen Kunden zur Verfügung, die Adobe Experience Platform verwenden. [Weitere Informationen](/help/destinations/destination-sdk/overview.md#productized-custom-integrations).

## S

**Vorlage für die Self-Service-Dokumentation**: Die Vorlage für die Self-Service-Dokumentation bietet ein strukturiertes Format, mit dem Sie Ihr Ziel dokumentieren können. Es enthält Abschnitte für eine Übersicht, Anwendungsfälle, Voraussetzungen, unterstützte Identitäten, Zielgruppen, Exporttypen und Häufigkeit sowie Schritte zum Herstellen einer Verbindung zum Ziel, Aktivieren von Zielgruppen und Zuordnen von Attributen. Verwenden Sie diese Vorlage, um eine umfassende und konsistente Dokumentation sicherzustellen, sodass Kunden schnell mit der Verwendung Ihres Ziels beginnen und die bereitgestellten Anwendungsfälle verstehen können. Lesen Sie mehr über [wie Sie Ihr Ziel dokumentieren](/help/destinations/destination-sdk/docs-framework/documentation-instructions.md), [die neueste Self-Service-Dokumentationsvorlage herunterladen](/help/destinations/destination-sdk/assets/docs-framework/yourdestination-template.zip) und [wie es dargestellt wird](/help/destinations/destination-sdk/docs-framework/self-service-template.md).

## T

**Vorlagenspezifikationen und Vorlagenstrategien**: Vorlagenspezifikationen sind Konfigurationen, die zum Formatieren von HTTP-Anforderungen verwendet werden, die von Adobe Experience Platform an ein Ziel gesendet werden. Sie wandeln Profilattributfelder aus dem XDM-Schema in ein Format um, das von der Zielplattform unterstützt wird. Mithilfe einer Vorlagensprache, die [!DNL Jinja] ähnelt, ermöglichen diese Spezifikationen dynamische Datenumwandlungen basierend auf bestimmten Regeln und Eingabedaten. [Weitere Informationen](/help/destinations/destination-sdk/functionality/destination-server/templating-specs.md).

**Test-API**: Mit der Test-API können Sie Ihre Zielkonfigurationen überprüfen, bevor Sie eine Veröffentlichungsanforderung senden. Es bietet Tools zum Generieren von Beispielprofilen und zum Testen des Datenflusses, um sicherzustellen, dass die Konfiguration den Anforderungen des Ziels entspricht. Die API unterstützt sowohl Streaming- als auch dateibasierte (Batch-)Ziele und bietet eine Möglichkeit, Daten zu simulieren und potenzielle Probleme im Einrichtungsprozess zu beheben. Erfahren Sie mehr über die Test-API für [Streaming](/help/destinations/destination-sdk/testing-api/streaming-destinations/streaming-destination-testing-overview.md) und [dateibasierte Ziele](/help/destinations/destination-sdk/testing-api/batch-destinations/file-based-destination-testing-overview.md).

**Umwandlungsvorlage**: Eine Umwandlungsvorlage passt das Datenformat vom Adobe-XDM-Schema zum erwarteten Format des Ziels an. [Weitere Informationen](/help/destinations/destination-sdk/functionality/destination-server/message-format.md).
