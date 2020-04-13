---
title: Erlebnisplattform-Starterweiterungen
seo-title: Erlebnisplattform-Starterweiterungen
description: Launch ist mit Adobe-Tag-Management-Funktionen der nächsten Generation ausgestattet.  Launch bietet Kunden eine einfache Möglichkeit zum Bereitstellen und Verwalten aller Analyse-, Marketing- und Werbe-Tags, die für relevante Kundenerlebnisse benötigt werden.
seo-description: Launch ist mit Adobe-Tag-Management-Funktionen der nächsten Generation ausgestattet.  Launch bietet Kunden eine einfache Möglichkeit zum Bereitstellen und Verwalten aller Analyse-, Marketing- und Werbe-Tags, die für relevante Kundenerlebnisse benötigt werden.
translation-type: tm+mt
source-git-commit: 2a082dc46b50eba1a38eb9d6946e17f851b2fd3f

---


# Experience Platform Launch extensions {#experience-platform-launch-extensions}

Experience Platform Launch ist die nächste Generation der Tag-Management-Funktionen von Adobe. 
Launch bietet Kunden eine einfache Möglichkeit zum Bereitstellen und Verwalten aller Analyse-, Marketing- und Werbe-Tags, die für relevante Kundenerlebnisse benötigt werden. Der Start wird Adobe Experience Cloud-Kunden als zusätzliche, nützliche Funktion angeboten.

Eine Einführung in die Funktionen zum Starten von Experience Platform finden Sie in den nachfolgend aufgeführten Ressourcen:
* Experience Platform Launch [documentation](https://docs.adobe.com/content/help/de-DE/launch/using/overview.html)
* Experience Platform - [Schnellvideos](https://docs.adobe.com/content/help/en/launch/using/intro/get-started/videos.html)zum Starten von Beginn Beginn mit [Einführung in Experience Platform - Einführung](https://www.youtube.com/embed/rwqqkG1SERU) und [Veröffentlichungsprozess - Übersicht](https://helpx.adobe.com/de/analytics/how-to/adobe-launch-publishing-process.html)und dann zu den nächsten Konzepten.

## Finden der Starterweiterungen in der CDP-Benutzeroberfläche von Adobe in Echtzeit

Um die Starterweiterungen in der Adobe Echtzeit-CDP-Oberfläche zu finden, suchen Sie den Filter **[!UICONTROL Destinations > Catalog]** und wählen Sie **[!UICONTROL Extensions]** ihn aus **[!UICONTROL Types]** .

![Erweiterungsfilter in der Oberfläche](/help/rtcdp/destinations/assets/extensions-filter.png)

## Funktionsweise von Starterweiterungen

Starten Sie Erweiterungen, um Rohdaten an verschiedene Zieltypen weiterzuleiten. Stellen Sie sich Erweiterungen als **Ereignis Forwarding** -Zieltyp vor. Dies ist eine einfachere Art der Integration mit Zielplattformen, die nur Rohdaten für Ereignisse weiterleiten. Beispiele hierfür sind die [Gainsight-Personalisierungserweiterung](/help/rtcdp/destinations/gainsight-extension.md) oder die [Bestätigungsstimme der Kundenerweiterung](/help/rtcdp/destinations/confirmit-digital-feedback-extension.md).

**Profil-/Segmentexport** -Ziele in Adobe Echtzeit-Kundendatenplattform erfassen Ereignis-Daten, kombinieren sie mit anderen Datenquellen, wenden Sie Segmentierung an und exportieren Sie Segmente und qualifizierte Profil in Ziele. Beispiele hierfür sind das Ziel [der](/help/rtcdp/destinations/amazon-s3-destination.md) Amazon S3 Cloud-Datenspeicherung oder das Werbeziel [](/help/rtcdp/destinations/google-dv360-destination.md)Google Display &amp; Video 360.

![Erlebnis-Plattform-Starterweiterungen im Vergleich zu anderen Zielen](/help/rtcdp/destinations/assets/launch-and-other-destinations.png)

## Vorteile der Verwendung von Launch-Erweiterungen

Experience Platform Launch ist für bestehende Experience Cloud-Kunden kostenlos. Starten vereinfacht die Tag-Bereitstellung auf Ihrer Website mithilfe benutzerfreundlicher Erweiterungen, die Sie installieren, konfigurieren, aktualisieren und löschen können. Launch hat einen kleinen Fußabdruck auf Ihrer Website und ermöglicht Ihnen, Ihre Seiten schnell zu laden.

>[!IMPORTANT]
>
>Sie können zwar keine Segmente aktivieren, um Erweiterungen zu starten, aber Sie können Regeln festlegen, die nur in bestimmten Situationen Ereignis-Daten weiterleiten. Lesen Sie weiter unten.

Sie können *Regeln* erstellen, die bestimmen, wann Ereignis-Daten an Erweiterungen weitergeleitet werden. Diese leistungsstarke Funktion ermöglicht es Ihnen, Ereignis-Daten nur in bestimmten Situationen weiterzuleiten, anstatt Ereignis-Daten bei jeder Interaktion zu senden. For more information, read about rules in the [Launch documentation](https://docs.adobe.com/help/de-DE/launch/using/reference/manage-resources/rules.html).

## Anwendungsbeispiele für Starterweiterungen

Mit den Starterweiterungen können Sie verschiedene Anwendungsfälle des Kunden befriedigen. Beispiele für Anwendungsfälle für die Verwendung von Starterweiterungen:

* Sie können Website- oder native App-Daten über die Facebook-Pixelerweiterung an Facebook senden. Facebook-Pixel zeigen an, zu welchen Teilen Ihrer Site oder App ein Besucher navigiert hat, leiten diese Informationen an Facebook weiter und Sie können Ihr Besucher über Facebook erneut ansprechen.
* Sie können Ereignis-Daten von Ihren Websites und Apps an Google Analytics weiterleiten, um auf diesen Daten basierende Entscheidungen zu treffen.
* Sie können eine clientseitige Chat-App zur richtigen Zeit aktivieren, je nachdem, wie Ihre Benutzer mit Ihren Seiten interagieren, entsprechend den Regeln, die Sie in Start festgelegt haben.


## Extension-Kategorien

Starterweiterungen können in Adobe Echtzeit-CDP unter die folgenden Kategorien fallen:

* [Werbung](/help/rtcdp/destinations/advertising-destinations.md)
* [Analytics](/help/rtcdp/destinations/analytics-destinations.md)
* [Data Management-Plattform](/help/rtcdp/destinations/dmp-destinations.md)
* [E-Mail-Marketing-Ziele ](/help/rtcdp/destinations/email-marketing-destinations.md)
* [Personalisierung ](/help/rtcdp/destinations/personalization-destinations.md)
* [Umfragen](/help/rtcdp/destinations/survey-destinations.md)
* [Stimme des Kunden](/help/rtcdp/destinations/voice-of-customer-destinations.md)
