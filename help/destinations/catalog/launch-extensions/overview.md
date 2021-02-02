---
keywords: Start-Erweiterungen;Start-Erweiterung;Start-Ziele; Plattformstarterweiterungen;Plattformstarterweiterung;Plattformstartziele
title: Experience Platform Launch-Erweiterungen
seo-title: Experience Platform Launch-Erweiterungen
description: Launch ist mit Adobe-Tag-Management-Funktionen der nächsten Generation ausgestattet. Mit Launch können Kunden alle Analyse-, Marketing- und Werbe-Tags bereitstellen und verwalten, die für relevante Kundenerlebnisse erforderlich sind.
seo-description: Launch ist mit Adobe-Tag-Management-Funktionen der nächsten Generation ausgestattet. Mit Launch können Kunden alle Analyse-, Marketing- und Werbe-Tags bereitstellen und verwalten, die für relevante Kundenerlebnisse erforderlich sind.
translation-type: tm+mt
source-git-commit: 7aadb4b7e7c36b659490d155ad4cfa7ef0a24306
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 52%

---


# Adobe Experience Platform Launch-Erweiterungen {#overview.md}

Adobe Experience Platform Launch ist die nächste Generation von Tag-Management-Funktionen aus der Adobe. Platform
Launch bietet Kunden eine einfache Möglichkeit zum Bereitstellen und Verwalten aller Analyse-, Marketing- und Werbe-Tags, die für relevante Kundenerlebnisse benötigt werden.  Platform Launch ist für Adobe Experience Cloud-Kunden als integrierte, Mehrwert bietende Funktion verfügbar.

Eine Einführung in die Funktionen von Experience Platform Launch finden Sie in den folgenden Ressourcen:
- Adobe Experience Platform Launch [Dokumentation](https://docs.adobe.com/content/help/de-DE/experience-cloud/user-guides/home.translate.html)
- Adobe Experience Platform Launch [Schnellvideos](https://experienceleague.adobe.com/docs/launch/using/intro/get-started/videos.html?) für Beginn. Beginn mit [Einführung in Adobe Experience Platform Launch](https://www.youtube.com/embed/rwqqkG1SERU) und [Übersicht über den Veröffentlichungsprozess](https://helpx.adobe.com/de/analytics/how-to/adobe-launch-publishing-process.html) und fahren Sie dann mit den nächsten Konzepten fort.

## Suchen der Plattformstarterweiterungen in der Plattform-Oberfläche {#how-to-find-extensions-in-interface}

Um die Plattformstarterweiterungen in der Plattform-Oberfläche zu finden, navigieren Sie zu **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]** und wählen Sie **[!UICONTROL Erweiterungen]** im Filter **[!UICONTROL Typen]** aus.

![Erweiterungsfilter in der Benutzeroberfläche](../../assets/catalog/launch-extensions/filter.png)

## Funktionsweise von Plattformstarterweiterungen {#how-extensions-work}

Plattformstarterweiterungen leiten Rohdaten an verschiedene Ereignis weiter. Stellen Sie sich Erweiterungen als eine Art Ziel für die **Ereignisweiterleitung** vor. Dabei handelt es sich um eine einfachere Art der Integration mit Zielplattformen, die nur Rohdaten für Ereignisse weiterleiten. Beispiele hierfür sind die [Gainsight-Personalisierungserweiterung](../personalization/gainsight.md) oder die [Confirmit-Erweiterung „Stimme des Kunden“](../voice/confirmit-digital-feedback.md).

**Profil-/Segmentexport-** Ziele in Adobe Experience Platform erfassen Ereignis-Daten, kombinieren diese mit anderen Datenquellen, wenden Segmentierung an und exportieren Segmente und qualifizierte Profil in Ziele. Beispiele hierfür sind das [Amazon S3 Cloud-Speicher-Ziel](../cloud-storage/amazon-s3.md) oder das [Google Display &amp; Video 360-Werbeziel](../advertising/google-dv360.md).

![Experience Platform Launch-Erweiterungen im Vergleich zu anderen Zielen](../../assets/common/launch-and-other-destinations.png)

## Vorteile der Verwendung von Plattformstarterweiterungen {#extensions-benefits}

Adobe Experience Platform Launch ist für bestehende Experience Cloud-Kunden kostenlos. Plattformstart vereinfacht die Tag-Bereitstellung auf Ihrer Website mithilfe benutzerfreundlicher Erweiterungen, die Sie installieren, konfigurieren, aktualisieren und löschen können. Plattformstart hat einen kleinen Platzbedarf auf Ihrer Website und ermöglicht Ihnen, Ihre Seiten schnell zu laden.

>[!IMPORTANT]
>
>Sie können zwar keine Segmente für Plattformstarterweiterungen aktivieren, aber Sie können Regeln festlegen, die nur in bestimmten Ereignissen weiterleiten. Weitere Informationen finden Sie unten.

Sie können *Regeln* erstellen, die bestimmen, wann Ereignisdaten an Erweiterungen weitergeleitet werden. Mit dieser leistungsstarken Funktion können Sie Ereignisdaten nur in bestimmten Situationen weiterleiten, anstatt Ereignisdaten bei jeder Interaktion zu senden. Weitere Informationen finden Sie unter Regeln in der [Adobe Experience Platform Launch-Dokumentation](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html).

## Anwendungsbeispiele für Plattformstarterweiterungen {#extensions-use-cases}

Plattformstarterweiterungen ermöglichen es Ihnen, verschiedene Anwendungsfälle des Kunden zu befriedigen. Beispiele für Anwendungsfälle für die Verwendung von Plattformstarterweiterungen:

- Sie können Website- oder native App-Daten über die Facebook Pixel-Erweiterung an Facebook senden. Facebook Pixel gibt an, zu welchen Teilen Ihrer Website oder App ein Besucher navigiert hat, leitet diese Informationen an Facebook weiter und Sie können Ihren Besucher über Facebook erneut ansprechen.
- Sie können Ereignisdaten von Ihren Websites und Apps an Google Analytics weiterleiten, um diese Daten zu analysieren und Entscheidungen zu treffen.
- Sie können eine clientseitige Chat-App zur richtigen Zeit aktivieren, je nachdem, wie Ihre Benutzer mit Ihren Seiten interagieren, entsprechend den Regeln, die Sie in Plattformstart festgelegt haben.

## Erweiterungskategorien {#extension-categories}

Plattformstarterweiterungen können unter die folgenden Kategorien in Plattform fallen:

- [Werbung](../advertising/overview.md)
- [Analytics](../analytics/overview.md)
- [Daten-Management-Plattform](../data-management/overview.md)
- [E-Mail-Marketing-Ziele](../email-marketing/overview.md)
- [Personalisierung](../personalization/overview.md)
- [Umfragen](../survey/overview.md)
- [Stimme des Kunden](../voice/overview.md)
