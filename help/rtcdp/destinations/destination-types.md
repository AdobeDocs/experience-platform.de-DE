---
keywords: destinations;destination;destination types
title: Zieltypen und Kategorien
seo-title: Zieltypen und Kategorien
description: 'In der Echtzeit-Kundendatenplattform erfassen Profil-/Segmentexportziele Ereignis-Daten, kombinieren diese mit anderen Datenquellen, wenden Segmentierung an und exportieren Segmente und qualifizierte Profil in Ziele. Experience Platform Launch Extensions leiten Rohdaten aus Ereignissen an verschiedene Zieltypen weiter. '
seo-description: In der Echtzeit-Kundendatenplattform erfassen Profil-/Segmentexportziele Ereignis-Daten, kombinieren diese mit anderen Datenquellen, wenden Segmentierung an und exportieren Segmente und qualifizierte Profil in Ziele. Experience Platform Launch Extensions leiten Rohdaten aus Ereignissen an verschiedene Zieltypen weiter.
translation-type: tm+mt
source-git-commit: 0232acdc64019b9d93888e8137ef9bc8e114779b
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 16%

---


# Zieltypen und Kategorien

Lesen Sie diese Seite, um die verschiedenen Typen und Kategorien von Zielen der Echtzeit-Kundendatenplattform zu verstehen.

## Zieltypen

In der Echtzeit-Kundendatenplattform wird zwischen zwei Zieltypen unterschieden: Verbindungen und Erweiterungen. Es gibt zwei Arten von Verbindungszielen: Profil Export-Ziele und Segmentexport-Ziele.

![Zieltypen](/help/rtcdp/destinations/assets/types-of-destinations.png)

<br> 

### Verbindungen {#connections}

**[!UICONTROL Profil-Export]** - und **[!UICONTROL Segmentexport]** -Ziele in Echtzeit-Daten zur Kundendatenplattform erfassen Ereignis-Daten, kombinieren Sie diese mit anderen Datenquellen, um das [Echtzeit-Kundendaten-Profil](/help/profile/home.md)zu bilden, Segmentierung anzuwenden und Segmente und qualifizierte Profil an Ziele zu exportieren.

<br> 

#### Profilexportziele

Profilexportziele generieren eine Datei, die Profile und/oder Attribute enthält. Diese Ziele nutzen Rohdaten, oft mit der E-Mail-Adresse als Primärschlüssel. Das Ziel [der](/help/rtcdp/destinations/amazon-s3-destination.md) Amazon S3 Cloud-Datenspeicherung ist ein Beispiel dafür, wo Sie Dateien mit Profil-Exporten ablegen können.

#### Segmentexportziele

Segmentexportziele senden die Profil und Segmente, für die sie qualifiziert sind, an Zielplattformen. Diese Ziele nutzen Segmentkennungen oder Anwenderkennungen. Werbeziele wie [[!DNL Google Display & Video 360]](/help/rtcdp/destinations/google-dv360-destination.md) oder [[!DNL Google Ads]](/help/rtcdp/destinations/google-ads-destination.md) sind Beispiele für diese Zieltypen.

#### Export- und Segmentziele - Videoübersicht

Das folgende Video führt Sie durch die Besonderheiten der beiden Zieltypen:

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

<br> 

### Erweiterungen {#extensions}

Adobe Echtzeit-CDP nutzt die Leistungsfähigkeit und Flexibilität von Adobe Experience Platform Launch, um Plattformstarterweiterungen in die CDP-Benutzeroberfläche der Adobe in Echtzeit einzubinden.

>[!TIP]
>
>Detaillierte Informationen zu Adobe Experience Platform Launch-Erweiterungen, einschließlich Anwendungsfällen und Informationen dazu, wie Sie sie in der Benutzeroberfläche finden, finden Sie in der Übersicht über die [Adobe Experience Platform Launch-Erweiterungen](/help/rtcdp/destinations/experience-platform-launch-extensions.md).

Plattformstarterweiterungen leiten Rohdaten an verschiedene Ereignis weiter. Stellen Sie sich Erweiterungen als eine Art Ziel für die **Ereignisweiterleitung** vor. Dabei handelt es sich um eine einfachere Art der Integration mit Zielplattformen, die nur Rohdaten für Ereignisse weiterleiten. Beispiele hierfür sind die [Gainsight-Personalisierungserweiterung](/help/rtcdp/destinations/gainsight-extension.md) oder die [Confirmit-Erweiterung „Stimme des Kunden“](/help/rtcdp/destinations/confirmit-digital-feedback-extension.md).

![Experience Platform Launch-Erweiterungen im Vergleich zu anderen Zielen](/help/rtcdp/destinations/assets/launch-and-other-destinations.png)

<br> 

### Verwenden von Verbindungen und Erweiterungen

Als Vermarkter können Sie eine Kombination aus Verbindungen und Erweiterungen verwenden, um Ihre Anwendungsfälle zu bearbeiten.

Verbindungen sind nützlich, wenn es erforderlich ist, ein vollständig zentralisiertes Kundensegment oder ein Kundensegment zur Aktivierung zu nutzen. Verwenden Sie z. B. Verbindungen, wenn Sie Verhaltensdaten aus einem Analysesystem mit hochgeladenen CRM-Daten verbinden, um einen Benutzer für ein bestimmtes Segment zu qualifizieren, bevor Sie ihm eine personalisierte Nachricht übermitteln.

Erweiterungen sind hilfreich, wenn Ereignis-Daten verwendet werden, um eine Aktion auszulösen oder eine Segmentierung in einer externen Umgebung durchzuführen. Wenn beispielsweise Verhaltensdaten an ein externes System weitergeleitet werden müssen, ohne für einen bestimmten Benutzer an andere Datenquellen in der Datei angeschlossen zu werden.

<br> 

## Zielkategorien

Die Verbindungen und Erweiterungen im [Zielkatalog](https://platform.adobe.com/destination/catalog) werden je nach Zielplattform (**Werbung**, **Cloud-Datenspeicherung**, **Umfrage-Plattformen**, **E-Mail-Marketing** usw.) gruppiert, je nachdem, welchen Marketing-Anwendungsfall sie Ihnen dabei helfen. Weitere Informationen zu den einzelnen Kategorien sowie zu den in den einzelnen Kategorien enthaltenen Zielen finden Sie in der [Zielkatalogdokumentation](/help/rtcdp/destinations/destinations-catalog.md).

![Zielkategorien](/help/rtcdp/destinations/assets/destination-categories-menu.png)

