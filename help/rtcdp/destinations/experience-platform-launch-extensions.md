---
keywords: launch extensions;launch extension;launch destinations; platform launch extensions;platform launch extension;platform launch destinations
title: Experience Platform Launch-Erweiterungen
seo-title: Experience Platform Launch-Erweiterungen
description: Launch ist mit Adobe-Tag-Management-Funktionen der nächsten Generation ausgestattet. Mit Launch können Kunden alle Analyse-, Marketing- und Werbe-Tags bereitstellen und verwalten, die für relevante Kundenerlebnisse erforderlich sind.
seo-description: Launch ist mit Adobe-Tag-Management-Funktionen der nächsten Generation ausgestattet. Mit Launch können Kunden alle Analyse-, Marketing- und Werbe-Tags bereitstellen und verwalten, die für relevante Kundenerlebnisse erforderlich sind.
translation-type: tm+mt
source-git-commit: 0232acdc64019b9d93888e8137ef9bc8e114779b
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 60%

---


# Adobe Experience Platform Launch-Erweiterungen {#experience-platform-launch-extensions}

Adobe Experience Platform Launch ist die nächste Generation von Tag-Management-Funktionen aus der Adobe. Platform
Launch bietet Kunden eine einfache Möglichkeit zum Bereitstellen und Verwalten aller Analyse-, Marketing- und Werbe-Tags, die für relevante Kundenerlebnisse benötigt werden.  Platform Launch ist für Adobe Experience Cloud-Kunden als integrierte, Mehrwert bietende Funktion verfügbar.

Eine Einführung in die Funktionen von Experience Platform Launch finden Sie in den folgenden Ressourcen:
* Adobe Experience Platform Launch [documentation](https://docs.adobe.com/content/help/de-DE/launch/using/overview.html)
* Adobe Experience Platform Launch [quick start videos](https://docs.adobe.com/content/help/de-DE/launch/using/intro/get-started/videos.html). Start with [Introduction to Adobe Experience Platform Launch](https://www.youtube.com/embed/rwqqkG1SERU) and [Publishing process overview](https://helpx.adobe.com/de/analytics/how-to/adobe-launch-publishing-process.html), then move on to the next concepts.

## How to find the Platform Launch extensions in the Adobe Real-time CDP interface {#how-to-find-extensions-in-interface}

To find the Platform Launch extensions in the Adobe Real-time CDP interface, browse to **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** and select **[!UICONTROL Extensions]** in the **[!UICONTROL Types]** filter.

![Erweiterungsfilter in der Benutzeroberfläche](/help/rtcdp/destinations/assets/extensions-filter.png)

## Funktionsweise von Plattformstarterweiterungen {#how-extensions-work}

Plattformstarterweiterungen leiten Rohdaten an verschiedene Ereignis weiter. Stellen Sie sich Erweiterungen als eine Art Ziel für die **Ereignisweiterleitung** vor. Dabei handelt es sich um eine einfachere Art der Integration mit Zielplattformen, die nur Rohdaten für Ereignisse weiterleiten. Beispiele hierfür sind die [Gainsight-Personalisierungserweiterung](/help/rtcdp/destinations/gainsight-extension.md) oder die [Confirmit-Erweiterung „Stimme des Kunden“](/help/rtcdp/destinations/confirmit-digital-feedback-extension.md).

**Profil-/Segmentexport-Ziele** in der Echtzeit-Kundendatenplattform von erfassen Ereignisdaten, kombinieren sie mit anderen Datenquellen, wenden Segmentierung an und exportieren Segmente und qualifizierte Profile in Ziele. Beispiele hierfür sind das [Amazon S3 Cloud-Speicher-Ziel](/help/rtcdp/destinations/amazon-s3-destination.md) oder das [Google Display &amp; Video 360-Werbeziel](/help/rtcdp/destinations/google-dv360-destination.md).

![Experience Platform Launch-Erweiterungen im Vergleich zu anderen Zielen](/help/rtcdp/destinations/assets/launch-and-other-destinations.png)

## Benefits of using Platform Launch extensions {#extensions-benefits}

Adobe Experience Platform Launch ist für bestehende Experience Cloud-Kunden kostenlos. Plattformstart vereinfacht die Tag-Bereitstellung auf Ihrer Website mithilfe benutzerfreundlicher Erweiterungen, die Sie installieren, konfigurieren, aktualisieren und löschen können. Plattformstart hat einen kleinen Platzbedarf auf Ihrer Website und ermöglicht Ihnen, Ihre Seiten schnell zu laden.

>[!IMPORTANT]
>
>Sie können zwar keine Segmente für Plattformstarterweiterungen aktivieren, aber Sie können Regeln festlegen, die nur in bestimmten Ereignissen weiterleiten. Weitere Informationen finden Sie unten.

Sie können *Regeln* erstellen, die bestimmen, wann Ereignisdaten an Erweiterungen weitergeleitet werden. Mit dieser leistungsstarken Funktion können Sie Ereignisdaten nur in bestimmten Situationen weiterleiten, anstatt Ereignisdaten bei jeder Interaktion zu senden. For more information, read about rules in the [Adobe Experience Platform Launch documentation](https://docs.adobe.com/help/de-DE/launch/using/reference/manage-resources/rules.html).

## Example use cases for Platform Launch extensions {#extensions-use-cases}

Plattformstarterweiterungen ermöglichen es Ihnen, verschiedene Anwendungsfälle des Kunden zu befriedigen. Beispiele für Anwendungsfälle für die Verwendung von Plattformstarterweiterungen:

* Sie können Website- oder native App-Daten über die Facebook Pixel-Erweiterung an Facebook senden. Facebook Pixel gibt an, zu welchen Teilen Ihrer Website oder App ein Besucher navigiert hat, leitet diese Informationen an Facebook weiter und Sie können Ihren Besucher über Facebook erneut ansprechen.
* Sie können Ereignisdaten von Ihren Websites und Apps an Google Analytics weiterleiten, um diese Daten zu analysieren und Entscheidungen zu treffen.
* Sie können eine clientseitige Chat-App zur richtigen Zeit aktivieren, je nachdem, wie Ihre Benutzer mit Ihren Seiten interagieren, entsprechend den Regeln, die Sie in Plattformstart festgelegt haben.


## Erweiterungskategorien {#extension-categories}

Plattformstarterweiterungen können unter die folgenden Kategorien in der Adobe CDP in Echtzeit fallen:

* [Werbung](/help/rtcdp/destinations/advertising-destinations.md)
* [Analytics](/help/rtcdp/destinations/analytics-destinations.md)
* [Daten-Management-Plattform](/help/rtcdp/destinations/dmp-destinations.md)
* [E-Mail-Marketing-Ziele](/help/rtcdp/destinations/email-marketing-destinations.md)
* [Personalisierung](/help/rtcdp/destinations/personalization-destinations.md)
* [Umfragen](/help/rtcdp/destinations/survey-destinations.md)
* [Stimme des Kunden](/help/rtcdp/destinations/voice-of-customer-destinations.md)
