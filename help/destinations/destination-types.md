---
keywords: Ziele; Ziel; Zieltypen
title: Zieltypen und Kategorien
seo-title: Destination types and categories
description: Erfahren Sie mehr über die verschiedenen Zieltypen und -kategorien in Adobe Experience Platform.
exl-id: 7826d1e2-bd6b-4f65-9da9-0a3b3e8bb93b
source-git-commit: 5a6f14ba65584a6bd61d62c4fb0b46e8f9e8e96d
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 12%

---

# Zieltypen und Kategorien

Lesen Sie diese Seite, um die verschiedenen Typen und Kategorien von Adobe Experience Platform-Zielen zu verstehen.

## Zieltypen

In Adobe Experience Platform unterscheiden wir zwischen zwei Zieltypen: Verbindungen und Erweiterungen. Es gibt zwei Arten von Verbindungszielen: Profilexportziele und Segmentexportziele.

![Zieltypen](./assets/destination-types/types-of-destinations.png)

## Verbindungen {#connections}

**[!UICONTROL Profile]** Exportieren und  **[!UICONTROL Streaming-Segmentexportziele in Adobe Experience Platform erfassen Ereignisdaten, kombinieren sie mit anderen Datenquellen, um das]** Echtzeit-Kundenprofil [ ](../profile/home.md) zu bilden, wenden Segmentierung an und exportieren Segmente und qualifizierte Profile in Ziele.

## Profilexportziele

Profilexportziele erhalten Rohdaten, oft mit der E-Mail-Adresse als Primärschlüssel. Experience Platform unterstützt derzeit zwei Typen von Profilexportzielen:

* [Export-Ziele für Streaming-Profile](#streaming-profile-export)
* [Dateibasierte Ziele](#file-based)

### Export-Ziele für Streaming-Profile {#streaming-profile-export}

Streaming-Profil-Export-Ziele empfangen Segment- und Profildaten als Experience Platform-Datenströme. [Beispiele für solche Ziele sind Amazon ](catalog/cloud-storage/amazon-kinesis.md) Kinesiens und  [Azure Event ](catalog/cloud-storage/azure-event-hubs.md) Hubs.

### Dateibasierte Ziele {#file-based}

Dateibasierte Ziele erhalten `.csv` Dateien mit Profilen und/oder Attributen. [Amazon S3](catalog/cloud-storage/amazon-s3.md) ist ein Beispiel für ein Ziel, an dem Sie Dateien mit Profilexporten hinterlegen können.

## Export-Ziele für Streaming-Segmente

Segmentexportziele erhalten Daten zu Experience Platform-Segmenten. Diese Ziele verwenden Segment-IDs oder Benutzer-IDs. [[!DNL Google Display & Video 360]](catalog/advertising/google-dv360.md) und  [[!DNL Google Ads]](catalog/advertising/google-ads-destination.md) sind Beispiele für solche Ziele.

## Export- und Segmentexportziele - Videoübersicht

Im folgenden Video werden Sie durch die Besonderheiten der beiden Zieltypen geführt:

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

## Erweiterungen {#extensions}

Platform nutzt die Leistungsfähigkeit und Flexibilität des Tag-Managements, sodass Sie Tag-Erweiterungen in der Datenerfassungs-Benutzeroberfläche konfigurieren können.

>[!TIP]
>
>Ausführliche Informationen zu Tag-Erweiterungen, einschließlich Anwendungsfällen und deren Auffindung in der Benutzeroberfläche, finden Sie in der [Übersicht über Tag-Erweiterungen](./catalog/launch-extensions/overview.md).

Tag-Erweiterungen leiten Rohdaten von Ereignissen an verschiedene Zieltypen weiter. Stellen Sie sich Erweiterungen als eine Art Ziel für die **Ereignisweiterleitung** vor. Dabei handelt es sich um eine einfachere Art der Integration mit Zielplattformen, die nur Rohdaten für Ereignisse weiterleiten. Beispiele hierfür sind die [Gainsight-Personalisierungserweiterung](./catalog/personalization/gainsight.md) oder die [Confirmit-Erweiterung „Stimme des Kunden“](./catalog/voice/confirmit-digital-feedback.md).

![Tag-Erweiterungen im Vergleich zu anderen Zielen](./assets/common/launch-and-other-destinations.png)

## Verwendung von Verbindungen und Erweiterungen

Als Marketing-Experte können Sie eine Kombination aus Verbindungen und Erweiterungen verwenden, um Ihre Anwendungsfälle zu bearbeiten.

Verbindungen sind nützlich, wenn es erforderlich ist, ein vollständiges zentralisiertes Kundenprofil oder ein Kundensegment zur Aktivierung zu nutzen. Verwenden Sie beispielsweise Verbindungen, wenn Sie Verhaltensdaten aus einem Analysesystem mit hochgeladenen CRM-Daten verbinden, um einen Benutzer für ein bestimmtes Segment zu qualifizieren, bevor Sie ihm eine personalisierte Nachricht senden.

Erweiterungen sind hilfreich, wenn Ereignisdaten zum Trigger einer Aktion oder zur Segmentierung in einer externen Umgebung verwendet werden. Wenn beispielsweise Verhaltensdaten an ein externes System weitergeleitet werden müssen, ohne dass sie für einen bestimmten Benutzer an andere Datenquellen in der Datei angebunden werden.

## Zielkategorien

Die Verbindungen und Erweiterungen im [Zielkatalog](https://platform.adobe.com/destination/catalog) sind nach Zielkategorie (**Werbung**, **Cloud-Speicher**, **Umfrageplattformen**, **E-Mail-Marketing** usw.) gruppiert, je nachdem, welche Marketing-Aktion Ihnen hilft. Weitere Informationen zu den einzelnen Kategorien sowie zu den in den einzelnen Kategorien enthaltenen Zielen finden Sie in der [Dokumentation zum Zielkatalog](./catalog/overview.md).

![Zielkategorien](./assets/destination-types/destination-categories-menu.png)
