---
keywords: Tag-Erweiterungen; Tag-Erweiterung; Launch-Ziele; Platform-Tag-Erweiterungen;Plattform-Tag-Erweiterung;Platform Launch-Ziele
title: Tag-Erweiterungen in Adobe Experience Platform
description: Adobe Experience Platform verfügt über die nächste Generation von Tag-Management-Funktionen von Adobe. Experience Platform bietet eine einfache Möglichkeit, alle Analyse-, Marketing- und Werbe-Tags bereitzustellen und zu verwalten, die für relevante Kundenerlebnisse erforderlich sind.
exl-id: 54fca635-0e37-460e-abb3-5da294d4e0cf
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 56%

---

# Tag-Erweiterungen in Adobe Experience Platform

Adobe Experience Platform bietet die nächste Generation von Tag-Management-Funktionen von Adobe. Experience Platform bietet eine einfache Möglichkeit, alle Analyse-, Marketing- und Werbe-Tags bereitzustellen und zu verwalten, die für relevante Kundenerlebnisse erforderlich sind. Tags werden Adobe Experience Cloud-Kunden als integrierte Mehrwertfunktion angeboten.

Eine Einführung in Tags finden Sie in den folgenden Ressourcen:

- [Übersicht über Tags](../../../tags/home.md)
- [Schnellstartanleitung](../../../tags/quick-start/quick-start.md)

## So finden Sie Tag-Erweiterungen in der Benutzeroberfläche von Experience Platform {#how-to-find-extensions-in-interface}

Um die Erweiterungen in der Experience Platform-Benutzeroberfläche zu finden, navigieren Sie zu **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]** und wählen Sie **[!UICONTROL Erweiterungen]** im Filter **[!UICONTROL Types]** aus.

![Erweiterungsfilter in der Benutzeroberfläche](../../assets/catalog/launch-extensions/filter.png)

## Funktionsweise von Tag-Erweiterungen {#how-extensions-work}

Eine [Tag-Erweiterung](../../../tags/home.md#extensions) ist ein Code-Paket, das die Funktionalität einer Website oder Mobile App erweitert. Dazu kann gehören, dass Rohdaten von Ereignissen an ein Ziel wie [Google Analytics gesendet ](/help/destinations/catalog/analytics/google-universal-analytics.md), aber sie können auch andere Funktionen erfüllen.

Es ist wichtig, zwischen Tag- und Ereignisweiterleitungs-Erweiterungen zu unterscheiden. Die Erweiterungen, die in der Benutzeroberfläche Experience Platform-Ziele angezeigt werden, sind *Tag-Erweiterungen*. Weitere Informationen zu den Unterschieden zwischen Tags und [ Ereignisweiterleitung finden Sie in der Übersicht ](/help/tags/ui/event-forwarding/overview.md#differences-between-event-forwarding-and-tags) Ereignisweiterleitung .



<!--

Extensions forward raw event data to several types of destinations. Think of extensions as an **Event Forwarding** type of destination. This is a simpler type of integration with destination platforms, which only forwards raw event data. Examples of those are the [Gainsight personalization extension](../personalization/gainsight.md) or the [Confirmit Voice of the Customer extension](../voice/confirmit-digital-feedback.md).

**Profile/Segment Export** destinations in Adobe Experience Platform capture event data, combine it with other data sources, apply segmentation, and export audiences and qualified profiles to destinations. Examples of those are the [Amazon S3 cloud storage destination](../cloud-storage/amazon-s3.md) or the [Google Display & Video 360 advertising destination](../advertising/google-dv360.md).

![Tag extensions compared to other destinations](../../assets/common/launch-and-other-destinations.png)

-->

## Vorteile der Verwendung von Tag-Erweiterungen {#extensions-benefits}

Die Tag-Funktionen von Experience Platform sind für bestehende Experience Cloud-Kunden kostenlos. Das System vereinfacht die Tag-Bereitstellung auf Ihrer Website durch benutzerfreundliche Erweiterungen, die Sie installieren, konfigurieren, aktualisieren und löschen können. Tags haben einen geringen Platzbedarf auf Ihrer Website und ermöglicht das schnelle Laden Ihrer Seiten.

Sie können zwar keine Zielgruppen für Tag-Erweiterungen aktivieren, aber Sie können Regeln einrichten, um Ereignisdaten nur in bestimmten Situationen weiterzuleiten. Mit dieser leistungsstarken Funktion können Sie Ereignisdaten nur in bestimmten Situationen weiterleiten, anstatt Ereignisdaten bei jeder Interaktion zu senden. Weitere Informationen zu Regeln finden Sie in der [Tags-Dokumentation](../../../tags/ui/managing-resources/rules.md).

## Anwendungsbeispiele für Erweiterungen {#extensions-use-cases}

Erweiterungen können Sie für verschiedene Anwendungsfälle nutzen. Beispielhafte Anwendungsfälle für Erweiterungen:

- Sie können Website- oder native App-Daten über die Facebook Pixel-Erweiterung an Facebook senden. Facebook Pixel gibt an, zu welchen Teilen Ihrer Website oder App ein Besucher navigiert hat, leitet diese Informationen an Facebook weiter und Sie können Ihren Besucher über Facebook erneut ansprechen.
- Sie können Ereignisdaten von Ihren Websites und Apps an Google Analytics weiterleiten, um diese Daten zu analysieren und Entscheidungen zu treffen.
- Sie können eine Client-seitige Chatbox-App zum richtigen Zeitpunkt aktivieren, je nachdem, wie Ihre Benutzer mit Ihren Seiten interagieren. Dies entspricht den festgelegten Regeln.

## Erweiterungskategorien {#extension-categories}

Erweiterungen können in Experience Platform unter die folgenden Kategorien fallen:

- [Werbung](../advertising/overview.md)
- [Analysen](../analytics/overview.md)
- [Daten-Management-Plattform](../data-management/overview.md)
- [E-Mail-Marketing-Ziele ](../email-marketing/overview.md)
- [Personalisierung](../personalization/overview.md)
- [Umfragen](../survey/overview.md)
- [Stimme des Kunden](../voice/overview.md)
