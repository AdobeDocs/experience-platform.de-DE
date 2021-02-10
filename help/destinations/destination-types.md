---
keywords: Ziele;Ziel;Zieltypen;Zieltypen
title: Zieltypen und Kategorien
seo-title: Zieltypen und Kategorien
description: Erfahren Sie mehr über die verschiedenen Arten und Kategorien von Destinationen in Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: e13a19640208697665b0a7e0106def33fd1e456d
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 20%

---


# Zieltypen und Kategorien

Lesen Sie diese Seite, um die verschiedenen Typen und Kategorien von Adobe Experience Platform-Zielen zu verstehen.

## Zieltypen

In Adobe Experience Platform unterscheiden wir zwischen zwei Zieltypen - Verbindungen und Erweiterungen. Es gibt zwei Arten von Verbindungszielen: Profil Export-Ziele und Segmentexport-Ziele.

![Zieltypen](./assets/destination-types/types-of-destinations.png)

### Verbindungen {#connections}

**[!UICONTROL Profil]** Export- und  **[!UICONTROL Segmentexport-]** Ziele in Adobe Experience Platform erfassen Ereignis-Daten, kombinieren diese mit anderen Datenquellen, um das  [Echtzeit-Kundendienstmodell](../profile/home.md) zu bilden, wenden Segmentierung an und exportieren Segmente und qualifizierte Profil in Ziele.

#### Profilexportziele

Profilexportziele generieren eine Datei, die Profile und/oder Attribute enthält. Diese Ziele nutzen Rohdaten, oft mit der E-Mail-Adresse als Primärschlüssel. Das Ziel [Amazon S3 Cloud-Datenspeicherung-Ziel](./catalog/cloud-storage/amazon-s3.md) ist ein Beispiel dafür, wo Sie Dateien mit Profil-Exporten hinterlegen können.

#### Segmentexportziele

Segmentexportziele senden die Profil und Segmente, für die sie qualifiziert sind, an Zielplattformen. Diese Ziele nutzen Segmentkennungen oder Anwenderkennungen. Werbeziele wie [[!DNL Google Display & Video 360]](./catalog/advertising/google-dv360.md) oder [[!DNL Google Ads]](./catalog/advertising/google-ads-destination.md) sind Beispiele für diese Zieltypen.

#### Export- und Segmentziele - Videoübersicht

Das folgende Video führt Sie durch die Besonderheiten der beiden Zieltypen:

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

### Erweiterungen {#extensions}

Die Plattform nutzt die Leistungsfähigkeit und Flexibilität von Adobe Experience Platform Launch, um Plattformstarterweiterungen in die Plattform-Oberfläche aufzunehmen.

>[!TIP]
>
>Detaillierte Informationen zu Adobe Experience Platform Launch-Erweiterungen, einschließlich Anwendungsfällen und Informationen zum Auffinden in der Oberfläche, finden Sie unter [Übersicht über Adobe Experience Platform Launch-Erweiterungen](./catalog/launch-extensions/overview.md).

Plattformstarterweiterungen leiten Rohdaten an verschiedene Ereignis weiter. Stellen Sie sich Erweiterungen als eine Art Ziel für die **Ereignisweiterleitung** vor. Dabei handelt es sich um eine einfachere Art der Integration mit Zielplattformen, die nur Rohdaten für Ereignisse weiterleiten. Beispiele hierfür sind die [Gainsight-Personalisierungserweiterung](./catalog/personalization/gainsight.md) oder die [Confirmit-Erweiterung „Stimme des Kunden“](./catalog/voice/confirmit-digital-feedback.md).

![Experience Platform Launch-Erweiterungen im Vergleich zu anderen Zielen](./assets/common/launch-and-other-destinations.png)

### Verwenden von Verbindungen und Erweiterungen

Als Vermarkter können Sie eine Kombination aus Verbindungen und Erweiterungen verwenden, um Ihre Anwendungsfälle zu bearbeiten.

Verbindungen sind nützlich, wenn es erforderlich ist, ein vollständig zentralisiertes Kundensegment oder ein Kundensegment zur Aktivierung zu nutzen. Verwenden Sie z. B. Verbindungen, wenn Sie Verhaltensdaten aus einem Analysesystem mit hochgeladenen CRM-Daten verbinden, um einen Benutzer für ein bestimmtes Segment zu qualifizieren, bevor Sie ihm eine personalisierte Nachricht übermitteln.

Erweiterungen sind hilfreich, wenn Ereignis-Daten zum Trigger einer Aktion oder zur Durchführung der Segmentierung in einer externen Umgebung verwendet werden. Wenn beispielsweise Verhaltensdaten an ein externes System weitergeleitet werden müssen, ohne für einen bestimmten Benutzer an andere Datenquellen in der Datei angeschlossen zu werden.

## Zielkategorien

Die Verbindungen und Erweiterungen im [Zielkatalog](https://platform.adobe.com/destination/catalog) sind nach Zielplattformen (**Advertising**, **Cloud-Datenspeicherung**, **Umfragen-Plattformen**, **E-Mail-Marketing** usw.) gruppiert, je nach dem Marketinganwendungsfall, den sie Ihnen dabei helfen. Weitere Informationen zu den einzelnen Kategorien sowie zu den in den einzelnen Kategorien enthaltenen Zielen finden Sie in der [Katalogdokumentation zu Zielen](./catalog/overview.md).

![Zielkategorien](./assets/destination-types/destination-categories-menu.png)

