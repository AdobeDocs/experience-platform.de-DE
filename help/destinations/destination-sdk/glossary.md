---
solution: Experience Platform
title: Adobe Experience Platform Destination SDK Glossar
description: Wichtige Terminologie bei der Erstellung eines Ziels mit Experience Platform-Destination SDK verstehen.
exl-id: d65f390a-a980-49b8-9570-840f03534553
source-git-commit: a11f469cb54421e0ca30c7c5878128e216470f7f
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 3%

---

# Adobe Experience Platform Destination SDK Glossar

Definitionen der in der Destination SDK verwendeten Begriffe finden Sie in diesem Glossar . Weitere Adobe Experience Platform-Begriffe finden Sie im [Experience Platform-Glossar](/help/landing/glossary.md).

## A

**Aggregationsrichtlinie**: Bei der Konfiguration, wie Daten an Ihr Echtzeit-Streaming-Ziel exportiert werden sollen, können Sie definieren, wie Profildaten aggregiert werden, bevor sie an Ihre Zielplattform gesendet werden. Dies hilft bei der Optimierung der Datenbereitstellung, indem Datensätze anhand spezifischer Kriterien gruppiert, die Häufigkeit von API-Aufrufen reduziert und die Gesamteffizienz verbessert werden. Verschiedene Richtlinien können so konfiguriert werden, dass sie verschiedenen Zielanforderungen entsprechen, um sicherzustellen, dass Daten auf die effektivste Weise gepackt und bereitgestellt werden. [Weitere Informationen](/help/destinations/destination-sdk/functionality/destination-configuration/aggregation-policy.md).

**Zielgruppen-Metadatenkonfiguration**: Eine Zielgruppen-Metadatenkonfiguration bezieht sich auf die in Adobe Experience Platform definierten strukturierten Konfigurationen und Parameter, die die programmgesteuerte Erstellung, Aktualisierung und Löschung von Zielgruppensegmenten in einem bestimmten Ziel ermöglichen. Bei dieser Konfiguration werden Vorlagen für Zielgruppen-Metadaten verwendet, um sie an die Spezifikationen der Marketing-API der Zielplattform anzupassen. Lesen Sie mehr über die [Zielgruppen-Metadatenkonfiguration](/help/destinations/destination-sdk/functionality/audience-metadata-management.md) und [verfügbaren Makros](/help/destinations/destination-sdk/functionality/audience-metadata-management.md#macros).

## D

**Zielkonfigurations-Endpunkt**: Ein Zielkonfigurations-Endpunkt in Adobe Experience Platform, insbesondere der `/authoring/destinations` API-Endpunkt, wird zum Erstellen, Abrufen, Aktualisieren und Löschen von Konfigurationen für Ziele verwendet. Diese Konfigurationen definieren, wie Daten aus Adobe Experience Platform an verschiedene externe Systeme oder Ziele wie Marketing-Plattformen, Cloud-Speicher-Services oder andere Datenverarbeitungsendpunkte bereitgestellt werden. Lesen Sie mehr über [verfügbaren Konfigurationsoptionen](/help/destinations/destination-sdk/functionality/configuration-options.md#destination-configuration) und lesen Sie die [Referenzdokumentation](/help/destinations/destination-sdk/authoring-api/destination-configuration/create-destination-configuration.md).

**Zielinstanz**: Eine bestimmte Einrichtung einer Zielkonfiguration in Adobe Experience Platform, die über die Experience Platform-Benutzeroberfläche erstellt und verwaltet wird. Sie enthält alle erforderlichen Parameter und Anmeldeinformationen für das Verbinden und Senden von Daten an das Ziel. Nachdem Sie die Verbindung zu Ihrem Ziel hergestellt haben, können Sie die ID der Zielinstanz abrufen, wenn [eine Verbindung mit Ihrem Ziel durchsuchen](/help/destinations/ui/destination-details-page.md).

![UI-Bild, wie Sie die Ziel-Instanz-ID abrufen](/help/destinations/destination-sdk/assets/testing-api/get-destination-instance-id.png)

## P

**[!DNL Pebble]-Vorlage**: Eine [!DNL Pebble]-Vorlage wird verwendet, um aus Adobe Experience Platform exportierte Daten in das für die Zielplattform erforderliche Format umzuwandeln. Dabei wird die [!DNL Pebble] Vorlagensprache verwendet, die eine dynamische Datenumwandlung durch Funktionen wie `filter`, `for`, `if` und `set` ermöglicht. Adobe Experience Platform enthält zusätzliche benutzerdefinierte Funktionen wie `addedSegments` und `removedSegments`. Mithilfe dieser Vorlagen können Datenelemente wie Zeitstempel und Zielgruppenzugehörigkeiten so formatiert werden, dass sie den Spezifikationen des Ziels entsprechen. Weitere Informationen [hier](/help/destinations/destination-sdk/functionality/destination-server/message-format.md) und [hier](/help/destinations/destination-sdk/functionality/destination-server/templating-specs.md).

**Privates Ziel**: Benutzerdefinierte Integrationen, die von einzelnen Adobe Experience Platform-Kundinnen und -Kunden erstellt wurden. Diese sind auf spezifische Geschäftsanforderungen zugeschnitten und nur innerhalb des Unternehmens des Kunden zugänglich, was eine Flexibilität bei der Konfiguration von Datenexporten bietet. Private Ziele sind nur für Kundinnen und Kunden von Real-Time CDP Ultimate verfügbar. [Weitere Informationen](/help/destinations/destination-sdk/overview.md#productized-custom-integrations).

**Öffentliches Ziel**: Eine öffentlich verfügbare Integration im Adobe Experience Platform-Katalog. Diese Ziele sind standardisiert und mit Markenbezeichnungen versehen. Durch die Bereitstellung vorkonfigurierter Parameter wird die Einrichtung für Kunden vereinfacht. Sie stehen allen Kundinnen und Kunden zur Verfügung, die Adobe Experience Platform verwenden. [Weitere Informationen](/help/destinations/destination-sdk/overview.md#productized-custom-integrations).

## S

**Self-Service-Dokumentationsvorlage**: Die Self-Service-Dokumentationsvorlage bietet ein strukturiertes Format, das Sie zum Dokumentieren Ihres Ziels verwenden können. Sie enthält Abschnitte mit einer Übersicht, Anwendungsfällen, Voraussetzungen, unterstützten Identitäten, Zielgruppen, Exporttypen und -häufigkeit sowie Schritte zum Herstellen einer Verbindung mit dem Ziel, Aktivieren von Zielgruppen und Zuordnungsattributen. Verwenden Sie diese Vorlage, um eine umfassende und konsistente Dokumentation sicherzustellen, sodass Kundinnen und Kunden schnell mit Ihrem Ziel beginnen und die bereitgestellten Anwendungsfälle verstehen können. Lesen Sie mehr über [Dokumentieren Ihres Ziels](/help/destinations/destination-sdk/docs-framework/documentation-instructions.md), [Herunterladen der neuesten Self-Service-Dokumentationsvorlage](/help/destinations/destination-sdk/assets/docs-framework/yourdestination-template.zip) und [Anzeigen, wie sie gerendert wird](/help/destinations/destination-sdk/docs-framework/self-service-template.md).

## T

**Vorlagenspezifikationen und Vorlagenstrategien**: Vorlagenspezifikationen sind Konfigurationen zum Formatieren von HTTP-Anfragen, die von Adobe Experience Platform an ein Ziel gesendet werden. Sie transformieren Profilattributfelder aus dem XDM-Schema in ein von der Zielplattform unterstütztes Format. Mithilfe einer Vorlagensprache, die [!DNL Jinja] ähnelt, ermöglichen diese Spezifikationen dynamische Datenumwandlungen auf der Grundlage spezifischer Regeln und Eingabedaten. [Weitere Informationen](/help/destinations/destination-sdk/functionality/destination-server/templating-specs.md).

**Test-API**: Mit der Test-API können Sie Ihre Zielkonfigurationen validieren, bevor Sie eine Veröffentlichungsanfrage senden. Es bietet Tools zum Generieren von Beispielprofilen und zum Testen des Datenflusses, um sicherzustellen, dass die Konfiguration den Anforderungen des Ziels entspricht. Die -API unterstützt sowohl Streaming- als auch dateibasierte (Batch-)Ziele und bietet eine Möglichkeit, Daten zu simulieren und potenzielle Probleme im Einrichtungsprozess zu beheben. Erfahren Sie mehr über die Test[API für &#x200B;](/help/destinations/destination-sdk/testing-api/streaming-destinations/streaming-destination-testing-overview.md)Streaming“ und [dateibasierte Ziele](/help/destinations/destination-sdk/testing-api/batch-destinations/file-based-destination-testing-overview.md).

**Umwandlungsvorlage**: Eine Umwandlungsvorlage passt das Datenformat vom Adobe-XDM-Schema an das erwartete Format des Ziels an. [Weitere Informationen](/help/destinations/destination-sdk/functionality/destination-server/message-format.md).
