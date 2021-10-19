---
keywords: Ziele;Ziel;Zieltypen
title: Zieltypen und Kategorien
seo-title: Destination types and categories
description: Erfahren Sie mehr über die verschiedenen Zieltypen und Kategorien in Adobe Experience Platform.
exl-id: 7826d1e2-bd6b-4f65-9da9-0a3b3e8bb93b
source-git-commit: a7c36f1a157b6020fede53e5c1074d966f26cf3d
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 12%

---

# Zieltypen und Kategorien

Lesen Sie diese Seite, um die verschiedenen Typen und Kategorien von Adobe Experience Platform-Zielen zu verstehen.

## Zieltypen

In Adobe Experience Platform unterscheiden wir zwischen zwei Zieltypen: Verbindungen und Erweiterungen. Es gibt zwei Arten von Verbindungszielen: Profil-Exportziele und Segment-Exportziele.

![Bestimmungsarten](./assets/destination-types/types-of-destinations.png)

## Verbindungen {#connections}

**[!UICONTROL Profil-Export]** und **[!UICONTROL Segmentexport streamen]** Ziele in Adobe Experience Platform erfassen Ereignis-Daten, kombinieren sie mit anderen Datenquellen, um [Echtzeit-Kundenerlebnis](../profile/home.md), wenden Sie Segmentierung an und exportieren Sie Segmente und qualifizierte Profil auf Ziele.

## Profilexportziele

Profil-Exportziele erhalten Rohdaten, oft mit E-Mail-Adresse als Primärschlüssel. Experience Platform unterstützt derzeit zwei Arten von Profil-Exportzielen:

* [Streaming-Profil-Exportziele](#streaming-profile-export)
* [Dateibasierte Ziele](#file-based)

### Streaming-Profil-Exportziele {#streaming-profile-export}

Streaming-Profil-Exportziele erhalten Segment- und Profil-Daten als Experience Platform-Datenströme. [Amazon Kinesis](catalog/cloud-storage/amazon-kinesis.md) und [Azure Ereignis Hubs](catalog/cloud-storage/azure-event-hubs.md) sind Beispiele für solche Ziele.

### Dateibasierte Ziele {#file-based}

Dateibasierte Ziele erhalten `.csv` Dateien mit Profilen und/oder Attributen. [Amazon S3](catalog/cloud-storage/amazon-s3.md) ist ein Beispiel für das Ziel, wo Sie Dateien mit Profil-Exporten hinterlegen können.

## Streaming-Segment-Exportziele {#streaming-destinations}

Segmentexportziele erhalten Experience Platformen-Segmentdaten. Diese Ziele verwenden Segment-IDs oder Benutzer-IDs. [[!DNL Google Display & Video 360]](catalog/advertising/google-dv360.md), [[!DNL Google Ads]](catalog/advertising/google-ads-destination.md)und sind Beispiele für solche Ziele.

## Export- und Segmentexportziele für Profile - Videoübersicht {#video}

Das folgende Video zeigt Ihnen die Besonderheiten der beiden Zieltypen:

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

## Erweiterungen {#extensions}

Die Plattform nutzt die Leistung und Flexibilität des Tag-Managements und ermöglicht die Konfiguration von Tag-Erweiterungen in der Data Collection-Benutzeroberfläche.

>[!TIP]
>
>Ausführliche Informationen zu Tag-Erweiterungen, einschließlich Verwendungsfällen und deren Auffinden in der Benutzeroberfläche finden Sie in der [Tag-Erweiterungen - Übersicht](./catalog/launch-extensions/overview.md).

Tag-Erweiterungen leiten Rohdaten an verschiedene Zieltypen weiter. Stellen Sie sich Erweiterungen als eine Art Ziel für die **Ereignisweiterleitung** vor. Dabei handelt es sich um eine einfachere Art der Integration mit Zielplattformen, die nur Rohdaten für Ereignisse weiterleiten. Beispiele hierfür sind die [Gainsight-Personalisierungserweiterung](./catalog/personalization/gainsight.md) oder die [Confirmit-Erweiterung „Stimme des Kunden“](./catalog/voice/confirmit-digital-feedback.md).

![Tag-Erweiterungen im Vergleich zu anderen Zielen](./assets/common/launch-and-other-destinations.png)

## Wann Verbindungen und Erweiterungen verwendet werden {#when-to-use}

Als Vermarkter können Sie eine Kombination aus Verbindungen und Erweiterungen verwenden, um Ihre Anwendungsfälle zu bearbeiten.

Verbindungen sind nützlich, wenn es notwendig ist, ein komplettes zentralisiertes Kundensegment oder ein Kundensegment für die Aktivierung zu nutzen. Verwenden Sie beispielsweise Verbindungen, wenn Sie Verhaltensdaten aus einem Analysesystem mit hochgeladenen CRM-Daten zusammenführen, um einen Benutzer für ein bestimmtes Segment zu qualifizieren, bevor Sie diesem Benutzer eine personalisierte Nachricht zukommen lassen.

Erweiterungen sind hilfreich, wenn Ereignis-Daten zum Trigger einer Aktion oder zur Durchführung der Segmentierung in einer externen Umgebung verwendet werden. Zum Beispiel, wenn Verhaltensdaten an ein externes System weitergeleitet werden müssen, ohne an andere Datenquellen in der Datei für einen bestimmten Benutzer angeschlossen zu werden.

## Zielkategorien {#categories}

Die Verbindungen und Erweiterungen im [Zielkatalog](https://platform.adobe.com/destination/catalog) sind nach Ziel-Kategorie gruppiert (**Werbung**, **Cloud-Datenspeicherung**, **Umfrage-Plattformen**, **E-Mail-Marketing**, usw.), je nach der Marketingaktion, die Ihnen hilft, dies zu erreichen. Weitere Informationen zu den einzelnen Kategorien sowie zu den in jeder Kategorie aufgeführten Bestimmungsorten finden Sie im [Dokumentation zum Zielkatalog](./catalog/overview.md).

![Zielkategorien](./assets/destination-types/destination-categories-menu.png)
