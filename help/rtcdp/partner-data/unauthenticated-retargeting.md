---
title: Offsite-Retargeting nicht authentifizierter Besucher
description: Erfahren Sie, wie Sie nicht authentifizierte Benutzer mithilfe von ECIDs erneut ansprechen können
feature: Use Cases, Customer Acquisition
source-git-commit: 672b15b0c36efbf3b7d62ec616f254fffe3dbb81
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 0%

---

# Nicht authentifiziertes Retargeting {#unauthenticated-retargeting}

Da Drittanbieter-Cookies an Effektivität verlieren, wechseln Unternehmen zu Cookie-losen Lösungen für personalisierte Interaktion und Retargeting. Offsite-Retargeting ermöglicht es Unternehmen, anspruchsvolle Anwender basierend auf ihren vorherigen Interaktionen zu erreichen, ohne auf Client-seitige JavaScript angewiesen zu sein.

## Gründe für das erneute Targeting nicht authentifizierter Besucher {#why-use-case}

Durch die Integration von Adobe Experience Platform Web SDK und Server-seitiger Ereignisweiterleitung können Sie Ereignis-Streaming und Datenweiterleitung optimieren. Dies ermöglicht das nahtlose Retargeting nicht authentifizierter Benutzender mithilfe von ECIDs (Experience Cloud IDs), wodurch eine konsistente plattformübergreifende Interaktion sichergestellt wird. Mit dieser Lösung können Sie die Konversionsmöglichkeiten erhöhen, indem Sie nicht authentifizierte Benutzer basierend auf ihren früheren Interaktionen effektiv erneut ansprechen.

## Voraussetzungen und Planung {#prerequisites-and-planning}

Bevor Sie mit der Bereitstellung der Web-SDK und der Ereignisweiterleitungskonfiguration fortfahren, stellen Sie Folgendes sicher:

1. **Adobe mit Web SDK-Setup**: Die Adobe Web SDK muss implementiert werden, um die Ereigniserfassung und Datenweiterleitung zu erleichtern.

2. **Adobe Experience Platform Edge Network-Konfiguration**: Stellen Sie sicher, dass der Edge Network so konfiguriert ist, dass er die Echtzeit-Ereignisweiterleitung für das Offsite-Retargeting unterstützt.

3. **ECID-Synchronisierung**: Stellen Sie sicher, dass ECIDs plattformübergreifend synchronisiert sind, um den nahtlosen Zielgruppen-Abgleich zu ermöglichen.

## So erreichen Sie das Offsite-Retargeting {#achieve-offsite-retargeting}

1. **Web SDK bereitstellen**: Implementieren Sie Adobe Web SDK auf Ihrer Website, um Echtzeit-Ereignisdaten zu erfassen, einschließlich Benutzerinteraktionen wie Seitenansichten, Klicks und anderen Verhaltensweisen.

2. **Ereignisweiterleitung aktivieren**: Konfigurieren Sie die Ereignisweiterleitung in Platform, um erfasste Benutzerdaten zu senden und so eine effiziente Datenübertragung für die Zielgruppenaktivierung sicherzustellen.

3. **Konfigurieren der Server-seitigen Aktivierung**: Verwenden Sie die Server-seitigen Funktionen von Adobe, um das Retargeting von Zielgruppen basierend auf ECIDs zu aktivieren und so eine plattformübergreifende, präzise Zielgruppenbestimmung sicherzustellen.

4. **Erstellen zielgerichteter Zielgruppen**: Verwenden Sie die Zielgruppensegmentierungs-Tools von Platform, um fokussierte Zielgruppen basierend auf dem Benutzerverhalten, wie Ansichten, Interaktionen oder Transaktionsabbrüche, zu definieren.

5. **Zielgruppen aktivieren**: Nachdem Ihre Zielgruppen für die erneute Zielgruppenbestimmung erstellt wurden, aktivieren Sie sie, um personalisierte Inhalte bereitzustellen, und stellen Sie sicher, dass die Benutzer basierend auf ihren vorherigen Interaktionen mit Ihrer Site erneut interagieren.

## Erstellen einer Zielgruppe mit dem berechneten Attribut {#create-audience}

Um Benutzer mit hohen Absichten effektiv erneut anzusprechen, erstellen Sie Zielgruppen basierend auf ihren früheren Interaktionen mit Ihrer Website. Verwenden Sie Platform, um Benutzer mithilfe berechneter Attribute zu segmentieren.

1. **Identifizieren wichtiger**: Wählen Sie zu verfolgende Benutzeraktionen aus, z. B. Seitenansichten oder Klicks.

2. **Zielgruppen erstellen**: Verwenden Sie Tools zur Zielgruppensegmentierung, um Benutzer basierend auf Verhaltensweisen zu gruppieren.

3. **ECID synchronisieren**: Stellen Sie sicher, dass ECIDs plattformübergreifend synchronisiert werden, um einen genauen Zielgruppenabgleich zu ermöglichen.

## Zielgruppe aktivieren {#activate-audience}

Nachdem Sie Ihre Zielgruppe erstellt haben, aktivieren Sie sie plattformübergreifend, um Benutzer einzubinden.

1. **Zielgruppen überprüfen**: Stellen Sie sicher, dass die Zielgruppensegmente die richtigen Verhaltensweisen widerspiegeln.

2. **Aktivierungsregeln erstellen**: Legen Sie Bedingungen fest, wann und wie Benutzende basierend auf Aktionen interagieren.

3. **Push an Platform**: Aktivieren Sie die Zielgruppe.

4. **Leistung überwachen**: Verfolgen Sie die Leistung der Zielgruppe und nehmen Sie bei Bedarf Anpassungen vor.

## Konfigurieren der Offsite-Retargeting-Erweiterung {#configure-extension}

### Bereitstellen der Web-SDK

Stellen Sie sicher, dass Adobe Web SDK ordnungsgemäß in Ihre Website integriert ist. Diese SDK ermöglicht die Erfassung von Echtzeit-Ereignisdaten, die für ein effizientes Retargeting von entscheidender Bedeutung sind.

### Aktivieren der Ereignisweiterleitung

Richten Sie eine Ereignisweiterleitung in Platform ein, um erfasste Benutzerverhaltensdaten an Retargeting-Plattformen zu senden. Die Ereignisweiterleitung stellt sicher, dass Daten effizient übertragen werden, sodass Unternehmen anspruchsvolle Benutzer ansprechen können, ohne auf Cookies angewiesen zu sein.

### An Retargeting-Regel anhängen

Stellen Sie sicher, dass die Offsite-Retargeting-Erweiterung an eine gültige Ereignisregel in der Datenerfassung von Adobe Experience Platform angehängt ist. Normalerweise sollte eine globale Regel erstellt werden, die für wichtige Aktionen wie `page load` oder bestimmte Benutzerinteraktionen ausgelöst wird.

Weitere Informationen zum Konfigurieren der Erweiterung finden Sie in der Dokumentation [Ereignisweiterleitung](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/getting-started) .

## Andere Anwendungsfälle {#other-use-cases}

Dieses Dokument bietet einen Überblick über die wichtigsten Anwendungsfälle und technischen Überlegungen für die erfolgreiche Entwicklung und Verwendung der Einrichtung von Web SDK und Ereignisweiterleitung. Wenn Sie die beschriebenen Verfahren befolgen und sicherstellen, dass die erforderlichen Voraussetzungen erfüllt sind, können Sie die Datenverfolgungs- und Analysefunktionen erheblich verbessern.

Sie können weitere Anwendungsfälle erkunden, die über die Partnerdatenunterstützung in Real-Time CDP aktiviert wurden:

- [Gewinnen und gewinnen Sie neue Kunden](./prospecting.md) mithilfe von Partnerdaten.
- [Personalisieren von Onsite](./offsite-retargeting.md)Erlebnissen mit Partnerunterstützung der Besuchererkennung.
- [Erstanbieterprofile ergänzen](./supplement-first-party-profiles.md) durch von Partnern bereitgestellte Attribute.