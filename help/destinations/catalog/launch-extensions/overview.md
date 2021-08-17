---
keywords: Tag-Erweiterungen; Tag-Erweiterung; Launch-Ziele; Platform-Tag-Erweiterungen;Plattform-Tag-Erweiterung;platform launch-Ziele
title: Tag-Erweiterungen in Adobe Experience Platform
description: Adobe Experience Platform bietet die nächste Generation von Tag-Management-Funktionen von Adobe. Platform bietet Ihnen eine einfache Möglichkeit, alle Analyse-, Marketing- und Werbe-Tags bereitzustellen und zu verwalten, die für relevante Kundenerlebnisse erforderlich sind.
exl-id: 54fca635-0e37-460e-abb3-5da294d4e0cf
source-git-commit: 272cf2906b44ccfeca041d9620ac0780e24ad1ae
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 32%

---

# Tag-Erweiterungen in Adobe Experience Platform

Adobe Experience Platform bietet die nächste Generation von Tag-Management-Funktionen von Adobe. Platform bietet Ihnen eine einfache Möglichkeit, alle Analyse-, Marketing- und Werbe-Tags bereitzustellen und zu verwalten, die für relevante Kundenerlebnisse erforderlich sind. Tags werden Adobe Experience Cloud-Kunden als zusätzliche, Mehrwert bietende Funktion angeboten.

Eine Einführung in Tags finden Sie in den folgenden Ressourcen:

- [Übersicht über Tags](../../../tags/home.md)
- [Schnellstartanleitung](../../../tags/quick-start/quick-start.md)

## Suchen von Tag-Erweiterungen in der Platform-Oberfläche {#how-to-find-extensions-in-interface}

Um die Erweiterungen in der Platform-Oberfläche zu finden, navigieren Sie zu **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]** und wählen Sie **[!UICONTROL Erweiterungen]** im Filter **[!UICONTROL Typen]** aus.

![Erweiterungsfilter in der Benutzeroberfläche](../../assets/catalog/launch-extensions/filter.png)

## Funktionsweise von Tag-Erweiterungen {#how-extensions-work}

Erweiterungen leiten Rohdaten von Ereignissen an verschiedene Zieltypen weiter. Stellen Sie sich Erweiterungen als eine Art Ziel für die **Ereignisweiterleitung** vor. Dabei handelt es sich um eine einfachere Art der Integration mit Zielplattformen, die nur Rohdaten für Ereignisse weiterleiten. Beispiele hierfür sind die [Gainsight-Personalisierungserweiterung](../personalization/gainsight.md) oder die [Confirmit-Erweiterung „Stimme des Kunden“](../voice/confirmit-digital-feedback.md).

**Profil-/Segmentexportziele in Adobe Experience Platform erfassen** Ereignisdaten, kombinieren sie mit anderen Datenquellen, wenden die Segmentierung an und exportieren Segmente und qualifizierte Profile in Ziele. Beispiele hierfür sind das [Amazon S3 Cloud-Speicher-Ziel](../cloud-storage/amazon-s3.md) oder das [Google Display &amp; Video 360-Werbeziel](../advertising/google-dv360.md).

![Tag-Erweiterungen im Vergleich zu anderen Zielen](../../assets/common/launch-and-other-destinations.png)

## Vorteile der Verwendung von Tag-Erweiterungen {#extensions-benefits}

Die Tag-Funktionen von Platform sind für Bestandskunden von Experience Cloud kostenlos. Das System vereinfacht die Tag-Implementierung auf Ihrer Website mithilfe benutzerfreundlicher Erweiterungen, die Sie installieren, konfigurieren, aktualisieren und löschen können. Tags hinterlassen einen geringen Platzbedarf auf Ihrer Website und ermöglichen es Ihnen, Ihre Seiten schnell zu laden.

Sie können zwar keine Segmente für Tag-Erweiterungen aktivieren, aber Sie können Regeln einrichten, um Ereignisdaten nur in bestimmten Situationen weiterzuleiten. Mit dieser leistungsstarken Funktion können Sie Ereignisdaten nur in bestimmten Situationen weiterleiten, anstatt Ereignisdaten bei jeder Interaktion zu senden. Weitere Informationen finden Sie in der [Tag-Dokumentation](../../../tags/ui/managing-resources/rules.md) unter Regeln.

## Anwendungsbeispiele für Erweiterungen {#extensions-use-cases}

Erweiterungen ermöglichen es Ihnen, verschiedene Anwendungsfälle von Kunden zu erfüllen. Beispiele für Anwendungsfälle für die Verwendung von Erweiterungen:

- Sie können Website- oder native App-Daten über die Facebook Pixel-Erweiterung an Facebook senden. Facebook Pixel gibt an, zu welchen Teilen Ihrer Website oder App ein Besucher navigiert hat, leitet diese Informationen an Facebook weiter und Sie können Ihren Besucher über Facebook erneut ansprechen.
- Sie können Ereignisdaten von Ihren Websites und Apps an Google Analytics weiterleiten, um diese Daten zu analysieren und Entscheidungen zu treffen.
- Sie können eine Client-seitige Chatbox-App zum richtigen Zeitpunkt aktivieren, je nachdem, wie Ihre Benutzer mit Ihren Seiten interagieren, gemäß den von Ihnen festgelegten Regeln.

## Erweiterungskategorien {#extension-categories}

Erweiterungen können in Platform unter die folgenden Kategorien fallen:

- [Werbung](../advertising/overview.md)
- [Analytics](../analytics/overview.md)
- [Daten-Management-Plattform](../data-management/overview.md)
- [E-Mail-Marketing-Ziele ](../email-marketing/overview.md)
- [Personalisierung](../personalization/overview.md)
- [Umfragen](../survey/overview.md)
- [Stimme des Kunden](../voice/overview.md)
