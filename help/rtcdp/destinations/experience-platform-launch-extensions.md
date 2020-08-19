---
keywords: launch extensions;launch extension;launch destinations
title: Experience Platform Launch-Erweiterungen
seo-title: Experience Platform Launch-Erweiterungen
description: Launch ist mit Adobe-Tag-Management-Funktionen der nächsten Generation ausgestattet. Mit Launch können Kunden alle Analyse-, Marketing- und Werbe-Tags bereitstellen und verwalten, die für relevante Kundenerlebnisse erforderlich sind.
seo-description: Launch ist mit Adobe-Tag-Management-Funktionen der nächsten Generation ausgestattet. Mit Launch können Kunden alle Analyse-, Marketing- und Werbe-Tags bereitstellen und verwalten, die für relevante Kundenerlebnisse erforderlich sind.
translation-type: tm+mt
source-git-commit: 15323134f0c626cad2c4e90b3e1c0662cf7e57dd
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 96%

---


# Experience Platform Launch-Erweiterungen {#experience-platform-launch-extensions}

Experience Platform Launch bietet die nächste Generation der Tag-Management-Funktionen von Adobe.
Mit Launch können Kunden alle Analyse-, Marketing- und Werbe-Tags bereitstellen und verwalten, die für relevante Kundenerlebnisse erforderlich sind. Launch ist für Adobe Experience Cloud-Kunden als zusätzliche, Mehrwert bietende Funktion verfügbar.

Eine Einführung in die Funktionen von Experience Platform Launch finden Sie in den folgenden Ressourcen:
* Experience Platform Launch – [Dokumentation](https://docs.adobe.com/content/help/de-DE/launch/using/overview.html)
* Experience Platform Launch – [Kurzanleitungsvideos](https://docs.adobe.com/content/help/de-DE/launch/using/intro/get-started/videos.html). Beginnen Sie mit [Einführung in Experience Platform Launch](https://www.youtube.com/embed/rwqqkG1SERU) und [Publishing-Prozess – Übersicht](https://helpx.adobe.com/de/analytics/how-to/adobe-launch-publishing-process.html) und gehen Sie dann zu den nächsten Konzepten über.

## So finden Sie die Launch-Erweiterungen in der Benutzeroberfläche der Echtzeit-Kundendatenplattform von Adobe {#how-to-find-extensions-in-interface}

To find the Launch extensions in the Adobe Real-time CDP interface, browse to **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** and select **[!UICONTROL Extensions]** in the **[!UICONTROL Types]** filter.

![Erweiterungsfilter in der Benutzeroberfläche](/help/rtcdp/destinations/assets/extensions-filter.png)

## Funktionsweise von Launch-Erweiterungen {#how-extensions-work}

Launch-Erweiterungen leiten Rohdaten für Ereignisse an verschiedene Typen von Zielen weiter. Stellen Sie sich Erweiterungen als eine Art Ziel für die **Ereignisweiterleitung** vor. Dabei handelt es sich um eine einfachere Art der Integration mit Zielplattformen, die nur Rohdaten für Ereignisse weiterleiten. Beispiele hierfür sind die [Gainsight-Personalisierungserweiterung](/help/rtcdp/destinations/gainsight-extension.md) oder die [Confirmit-Erweiterung „Stimme des Kunden“](/help/rtcdp/destinations/confirmit-digital-feedback-extension.md).

**Profil-/Segmentexport-Ziele** in der Echtzeit-Kundendatenplattform von Adobe erfassen Ereignisdaten, kombinieren sie mit anderen Datenquellen, wenden Segmentierung an und exportieren Segmente und qualifizierte Profile in Ziele. Beispiele hierfür sind das [Amazon S3 Cloud-Speicher-Ziel](/help/rtcdp/destinations/amazon-s3-destination.md) oder das [Google Display &amp; Video 360-Werbeziel](/help/rtcdp/destinations/google-dv360-destination.md).

![Experience Platform Launch-Erweiterungen im Vergleich zu anderen Zielen](/help/rtcdp/destinations/assets/launch-and-other-destinations.png)

## Vorteile der Verwendung von Launch-Erweiterungen {#extensions-benefits}

Experience Platform Launch ist für bestehende Experience Cloud-Kunden kostenlos. Launch vereinfacht die Tag-Implementierung auf Ihrer Website durch benutzerfreundliche Erweiterungen, die Sie installieren, konfigurieren, aktualisieren und löschen können. Launch hat einen geringen Platzbedarf auf Ihrer Website und ermöglicht es Ihnen, Ihre Seiten schnell zu laden.

>[!IMPORTANT]
>
>Sie können zwar keine Segmente für Launch-Erweiterungen aktivieren, aber Sie können Regeln aufstellen, um Ereignisdaten nur in bestimmten Situationen weiterzuleiten. Weitere Informationen finden Sie unten.

Sie können *Regeln* erstellen, die bestimmen, wann Ereignisdaten an Erweiterungen weitergeleitet werden. Mit dieser leistungsstarken Funktion können Sie Ereignisdaten nur in bestimmten Situationen weiterleiten, anstatt Ereignisdaten bei jeder Interaktion zu senden. Weitere Informationen zu Regeln finden Sie in der [Launch-Dokumentation](https://docs.adobe.com/help/de-DE/launch/using/reference/manage-resources/rules.html).

## Anwendungsbeispiele für Launch-Erweiterungen {#extensions-use-cases}

Mit den Launch-Erweiterungen können Sie verschiedene Anwendungsfälle der Kunden erfüllen. Beispielhafte Anwendungsfälle für Launch-Erweiterungen:

* Sie können Website- oder native App-Daten über die Facebook Pixel-Erweiterung an Facebook senden. Facebook Pixel gibt an, zu welchen Teilen Ihrer Website oder App ein Besucher navigiert hat, leitet diese Informationen an Facebook weiter und Sie können Ihren Besucher über Facebook erneut ansprechen.
* Sie können Ereignisdaten von Ihren Websites und Apps an Google Analytics weiterleiten, um diese Daten zu analysieren und Entscheidungen zu treffen.
* Sie können eine Client-seitige Chatbox-App zum richtigen Zeitpunkt aktivieren, je nachdem, wie Ihre Benutzer mit Ihren Seiten interagieren. Dies entspricht den in Launch festgelegten Regeln.


## Erweiterungskategorien {#extension-categories}

Launch-Erweiterungen können in der Echtzeit-Kundendatenplattform von Adobe unter die folgenden Kategorien fallen:

* [Werbung](/help/rtcdp/destinations/advertising-destinations.md)
* [Analytics](/help/rtcdp/destinations/analytics-destinations.md)
* [Daten-Management-Plattform](/help/rtcdp/destinations/dmp-destinations.md)
* [E-Mail-Marketing-Ziele](/help/rtcdp/destinations/email-marketing-destinations.md)
* [Personalisierung](/help/rtcdp/destinations/personalization-destinations.md)
* [Umfragen](/help/rtcdp/destinations/survey-destinations.md)
* [Stimme des Kunden](/help/rtcdp/destinations/voice-of-customer-destinations.md)
