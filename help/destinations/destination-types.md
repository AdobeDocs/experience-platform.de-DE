---
keywords: Ziele; Ziel; Zieltypen
title: Zieltypen und Kategorien
seo-title: Destination types and categories
description: Erfahren Sie mehr über die verschiedenen Zieltypen und -kategorien in Adobe Experience Platform.
exl-id: 7826d1e2-bd6b-4f65-9da9-0a3b3e8bb93b
source-git-commit: 08c6c2716b88180b1eb290663117e6da2d8641f0
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 12%

---

# Zieltypen und Kategorien

Lesen Sie diese Seite, um die verschiedenen Typen und Kategorien von Adobe Experience Platform-Zielen zu verstehen.

## Zieltypen

In Adobe Experience Platform unterscheiden wir zwischen zwei Zieltypen: Verbindungen und Erweiterungen. Es gibt zwei Arten von Verbindungszielen: Profilexportziele und Segmentexportziele.

![Zieltypen](./assets/destination-types/types-of-destinations.png)

## Verbindungen {#connections}

**[!UICONTROL Profilexport]** und **[!UICONTROL Export von Streaming-Segmenten]** Ziele in Adobe Experience Platform erfassen Ereignisdaten, kombinieren sie mit anderen Datenquellen, um die [Echtzeit-Kundenprofil](../profile/home.md), wenden Sie die Segmentierung an und exportieren Sie Segmente und qualifizierte Profile in Ziele.

## Profilexportziele

Profilexportziele erhalten Rohdaten, oft mit der E-Mail-Adresse als Primärschlüssel. Experience Platform unterstützt derzeit zwei Typen von Profilexportzielen:

* [Export-Ziele für Streaming-Profile](#streaming-profile-export)
* [Batch-Ziele (dateibasiert)](#file-based)

### Export-Ziele für Streaming-Profile {#streaming-profile-export}

Streaming-Profil-Export-Ziele empfangen Segment- und Profildaten als Experience Platform-Datenströme. [Amazon Kinesis](catalog/cloud-storage/amazon-kinesis.md) und [Azure Event Hubs](catalog/cloud-storage/azure-event-hubs.md) sind Beispiele für solche Ziele.

### Batch-Ziele (dateibasiert) {#file-based}

Dateibasierte Ziele empfangen `.csv` Dateien, die Profile und/oder Attribute enthalten. [Amazon S3](catalog/cloud-storage/amazon-s3.md) ist ein Beispiel für ein Ziel, an dem Sie Dateien exportieren können, die Profilexporte enthalten.

## Export-Ziele für Streaming-Segmente {#streaming-destinations}

Segmentexportziele erhalten Daten zu Experience Platform-Segmenten. Diese Ziele verwenden Segment-IDs oder Benutzer-IDs. [[!DNL Google Display & Video 360]](catalog/advertising/google-dv360.md), [[!DNL Google Ads]](catalog/advertising/google-ads-destination.md)und sind Beispiele für solche Ziele.

## Export- und Segmentexportziele - Videoübersicht {#video}

Im folgenden Video werden Sie durch die Besonderheiten der beiden Zieltypen geführt:

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

## Erweiterungen {#extensions}

Platform nutzt die Leistungsfähigkeit und Flexibilität des Tag-Managements, sodass Sie Tag-Erweiterungen in der Datenerfassungs-Benutzeroberfläche konfigurieren können.

>[!TIP]
>
>Ausführliche Informationen zu Tag-Erweiterungen, einschließlich Anwendungsfällen und deren Auffindung in der -Benutzeroberfläche, finden Sie in der [Tag-Erweiterungen - Übersicht](./catalog/launch-extensions/overview.md).

Tag-Erweiterungen leiten Rohdaten von Ereignissen an verschiedene Zieltypen weiter. Stellen Sie sich Erweiterungen als eine Art Ziel für die **Ereignisweiterleitung** vor. Dabei handelt es sich um eine einfachere Art der Integration mit Zielplattformen, die nur Rohdaten für Ereignisse weiterleiten. Beispiele hierfür sind die [Gainsight-Personalisierungserweiterung](./catalog/personalization/gainsight.md) oder die [Confirmit-Erweiterung „Stimme des Kunden“](./catalog/voice/confirmit-digital-feedback.md).

![Tag-Erweiterungen im Vergleich zu anderen Zielen](./assets/common/launch-and-other-destinations.png)

## Verwendung von Verbindungen und Erweiterungen {#when-to-use}

Als Marketing-Experte können Sie eine Kombination aus Verbindungen und Erweiterungen verwenden, um Ihre Anwendungsfälle zu bearbeiten.

Verbindungen sind nützlich, wenn es erforderlich ist, ein vollständiges zentralisiertes Kundenprofil oder ein Kundensegment zur Aktivierung zu nutzen. Verwenden Sie beispielsweise Verbindungen, wenn Sie Verhaltensdaten aus einem Analysesystem mit hochgeladenen CRM-Daten verbinden, um einen Benutzer für ein bestimmtes Segment zu qualifizieren, bevor Sie ihm eine personalisierte Nachricht senden.

Erweiterungen sind hilfreich, wenn Ereignisdaten zum Trigger einer Aktion oder zur Segmentierung in einer externen Umgebung verwendet werden. Wenn beispielsweise Verhaltensdaten an ein externes System weitergeleitet werden müssen, ohne dass sie für einen bestimmten Benutzer an andere Datenquellen in der Datei angebunden werden.

## Zielkategorien {#categories}

Die Verbindungen und Erweiterungen in der [Zielkatalog](https://platform.adobe.com/destination/catalog) nach Zielkategorie (**Werbung**, **Cloud-Speicher**, **Umfrageplattformen**, **E-Mail-Marketing** usw.), je nach Marketing-Aktion, zu deren Erreichung sie beitragen. Weitere Informationen zu den einzelnen Kategorien sowie zu den in den einzelnen Kategorien enthaltenen Zielen finden Sie in der [Dokumentation zum Zielkatalog](./catalog/overview.md).

![Zielkategorien](./assets/destination-types/destination-categories-menu.png)
