---
keywords: Ziele;Ziel;Zieltypen
title: Zieltypen und Kategorien
description: Erfahren Sie mehr über die verschiedenen Zieltypen und -kategorien in Adobe Experience Platform.
exl-id: 7826d1e2-bd6b-4f65-9da9-0a3b3e8bb93b
source-git-commit: d57af88cc9507e0164b044a7203c66fe9fd9240e
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 51%

---

# Zieltypen und Kategorien

Lesen Sie diese Seite, um die verschiedenen Typen und Kategorien von Adobe Experience Platform-Zielen zu verstehen.

## Zieltypen {#destination-types}

In Adobe Experience Platform unterscheiden wir zwischen verschiedenen Zieltypen - Verbindungen, Datensatzexporten und Erweiterungen. Es gibt mehrere Arten von Verbindungszielen, mit denen Sie Daten an API-basierte Ziele, Social-Media-Ziele, CRM-Plattformen und viele mehr exportieren können.

Schließlich können Verbindungen auch zwischen öffentlichen Zielen, die über alle Organisationen im Zielkatalog verfügbar sind, und privaten Zielen unterschieden werden, die Kundinnen und Kunden von Real-Time CDP Ultimate erstellen können, um ihre spezifischen Exportanwendungsfälle zu erfüllen.

>[!BEGINSHADEBOX]

![Abbildung mit den Zieltypen](./assets/destination-types/types-of-destinations-no-highlight.png "Abbildung mit den Zieltypen."){zoomable="yes"}

>[!ENDSHADEBOX]

## Verbindungen {#connections}

**[!UICONTROL Profile Export]**, **[!UICONTROL Streaming Audience Export]** und **[!DNL Edge Personalization]** Ziele in Adobe Experience Platform erfassen Ereignisdaten, kombinieren sie mit anderen Datenquellen, um das [Echtzeit-Kundenprofil](../profile/home.md) zu bilden, wenden die Segmentierung an und exportieren Zielgruppen und qualifizierte Profile zu Zielen.

## Profilexportziele {#profile-export}

Ziele von Profilexporten erhalten Rohdaten, wobei die E-Mail-Adresse oft als Primärschlüssel dient. Experience Platform unterstützt derzeit zwei Typen von Zielen von Profilexporten:

* [Batch-Ziele (dateibasiert)](#file-based)
* [Erweiterte Unternehmensziele (Exportziele von Streaming-Profilen)](#advanced-enterprise-destinations)

### Erweiterte Unternehmensziele (Exportziele von Streaming-Profilen) {#advanced-enterprise-destinations}

>[!IMPORTANT]
>
>Erweiterte Unternehmensziele oder Exportziele von Streaming-Profilen sind nur für [Adobe Real-Time Customer Data Platform Ultimate](https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform.html)-Kunden verfügbar.

Verwenden Sie die erweiterten Data Connectors für Unternehmensziele, um Adobe Real-Time Customer Data Platform-Profile nahezu in Echtzeit für interne Systeme oder andere Drittanbietersysteme zur Datensynchronisierung, Analyse und weiteren Anwendungsfällen der Profilanreicherung bereitzustellen.

Diese Ziele empfangen Zielgruppen- und Profildaten als Experience Platform-Datenströme.

Zu den erweiterten Unternehmenszielen gehören:

* [HTTP-API-Ziel](catalog/streaming/http-destination.md)
* [Amazon Kinesis](catalog/cloud-storage/amazon-kinesis.md)
* [Azure Event Hubs](catalog/cloud-storage/azure-event-hubs.md)
* [Snowflake-Streaming](catalog/warehouses/snowflake.md)
* [Snowflake Batch](catalog/warehouses/snowflake-batch.md)

>[!NOTE]
>
>Die Snowflake-Ziele sind derzeit nur für US-Kunden verfügbar. Wenn Sie Zugriff außerhalb der USA benötigen, wenden Sie sich bitte an Ihr Adobe Account Team.

### Batch-Ziele (dateibasiert) {#file-based}

Dateibasierte Ziele empfangen `.csv`-Dateien, die Profile und/oder Attribute enthalten. [Amazon S3](catalog/cloud-storage/amazon-s3.md) ist ein Beispiel für ein Ziel, zu dem Sie Dateien mit Profilexporten exportieren können.

## Exportziele für Streaming-Zielgruppen {#streaming-destinations}

Ziele von Zielgruppenexporten erhalten Experience Platform-Zielgruppendaten. Diese Ziele verwenden Zielgruppen-IDs oder Benutzer-IDs. Werbung und Social-Media-Ziele wie [[!DNL Google Display & Video 360]](catalog/advertising/google-dv360.md), [[!DNL Google Ads]](catalog/advertising/google-ads-destination.md) oder [Facebook](catalog/social/facebook.md) sind Beispiele für solche Ziele.

## Edge-Personalisierungsziele {#edge-personalization-destinations}

Zu den Edge-Personalisierungszielen in Experience Platform gehören [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) und das [benutzerdefinierte Personalisierungsziel](/help/destinations/catalog/personalization/custom-personalization.md). Mithilfe dieser Ziele können Sie Anwendungsfälle für die Personalisierung von der gleichen Seite und der nächsten Seite für Ihre Kunden aktivieren.

Erfahren Sie mehr darüber, wie Sie [Personalisierungsziele für die Personalisierung der gleichen Seite und der nächsten Seite konfigurieren](/help/destinations/ui/activate-edge-personalization-destinations.md).

## Ziele für Profil- und Zielgruppenexport - Videoübersicht {#video}

Im folgenden Video werden Sie durch die Besonderheiten der beiden Zieltypen geführt:

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

## Typen von exportierten Zielgruppen {#exported-audiences-types}

Sie können drei Arten von Zielgruppen aus Experience Platform in verschiedene Ziele exportieren:

* Personen und Zielgruppen
* Kontozielgruppen
* Potenzielle Zielgruppen

Erfahren Sie mehr über [verschiedene Zielgruppentypen](/help/segmentation/types/account-audiences.md#terminology).

Ein Symbol auf der Zielkarte zeigt an, welche Zielgruppentypen Sie für jedes Ziel exportieren können.

![Beispiel einer Zielkarte mit Symbolen, die zeigen, welche Zielgruppentypen exportiert werden können.](/help/destinations/assets/destination-types/types-of-audiences.png "Beispiel einer Zielkarte mit Symbolen, die zeigen, welche Zielgruppentypen exportiert werden können."){zoomable="yes"}


## Ziele für Datensatzexporte {#dataset-export-destinations}

Einige Cloud-Speicherziele im Zielkatalog unterstützen Datensatzexporte. Verwenden Sie diese Ziele, um Rohdatensätze an Cloud-Speicherorte zu exportieren.

Weitere Informationen zum [Exportieren von Datensätzen](/help/destinations/ui/export-datasets.md).

## Erweiterungen {#extensions}

Experience Platform nutzt die Leistungsfähigkeit und Flexibilität des Tag-Managements, sodass Sie Tag-Erweiterungen in der Benutzeroberfläche konfigurieren können.

>[!TIP]
>
>Ausführliche Informationen zu Tag-Erweiterungen, einschließlich Anwendungsfällen und wie sie in der Benutzeroberfläche zu finden sind, finden Sie in der [Übersicht über Tag-Erweiterungen](./catalog/launch-extensions/overview.md).

Tag-Erweiterungen leiten Rohdaten von Ereignissen an verschiedene Typen von Zielen weiter. Stellen Sie sich Erweiterungen als eine Art Ziel für die **Ereignisweiterleitung** vor. Dabei handelt es sich um eine einfachere Art der Integration mit Zielplattformen, die nur Rohdaten für Ereignisse weiterleiten. Beispiele hierfür sind die [Gainsight-Personalisierungserweiterung](./catalog/personalization/gainsight.md) oder die [Confirmit-Erweiterung „Stimme des Kunden“](./catalog/voice/confirmit-digital-feedback.md).

![Tag-Erweiterungen im Vergleich zu anderen Zielen](./assets/common/launch-and-other-destinations.png)

## Verwendung von Verbindungen und Erweiterungen {#when-to-use}

Als Marketing-Experte können Sie eine Kombination aus Verbindungen und Erweiterungen verwenden, um Ihre Anwendungsfälle zu bearbeiten.

Verbindungen sind nützlich, wenn es erforderlich ist, ein vollständiges zentralisiertes Kundenprofil oder eine Kundenzielgruppe zur Aktivierung zu nutzen. Verwenden Sie beispielsweise Verbindungen, wenn Sie Verhaltensdaten aus einem Analysesystem mit hochgeladenen CRM-Daten verbinden, um einen Benutzer für eine bestimmte Zielgruppe zu qualifizieren, bevor Sie ihm eine personalisierte Nachricht senden.

Erweiterungen sind hilfreich, wenn Ereignisdaten zum Auslösen einer Aktion oder zur Segmentierung in einer externen Umgebung verwendet werden. Wenn beispielsweise Verhaltensdaten an ein externes System weitergeleitet werden müssen, ohne dass sie für einen bestimmten Benutzer an andere Datenquellen in der Datei angebunden werden.

## Zielkategorien {#categories}

Die Verbindungen und Erweiterungen im [Zielkatalog](https://platform.adobe.com/destination/catalog) sind nach Zielkategorie (**Werbung**, **Cloud-Speicher**, **Umfrageplattformen**, **E-Mail-Marketing** usw.) gruppiert, je nach Marketing-Aktion, zu deren Erreichung sie beitragen. Weitere Informationen zu den einzelnen Kategorien sowie zu den in den einzelnen Kategorien enthaltenen Zielen finden Sie in der [Dokumentation zum Zielkatalog](./catalog/overview.md).

![Zielkategorien, die auf der Katalogseite hervorgehoben sind.](./assets/destination-types/destination-categories-menu.png "Zielkategorien, die auf der Katalogseite hervorgehoben sind."){zoomable="yes"}
