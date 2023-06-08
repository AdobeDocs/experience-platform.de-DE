---
title: Entwicklung von Audience Manager zu Real-Time CDP
description: Machen Sie sich mit den Überlegungen vertraut, bevor Sie die Migration von Audience Manager zu Real-Time CDP planen.
source-git-commit: 147e95cce203933d591fc807d9d20bcbc06e68e3
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---


# Entwicklung von Audience Manager zu Real-Time CDP

Wenn sich Ihr Unternehmen weiterentwickelt, um Adobe Real-Time CDP zu verwenden, sollten Sie diese Überlegungen aufzeigen, um Ihre Daten vorzubereiten und sich der entscheidenden Unterschiede zwischen den beiden Technologien bewusst zu werden. Dieser Artikel richtet sich an eine Fachpublikum.

![Audience Manager zum Real-Time CDP-Evolutionsdiagramm](/help/rtcdp/assets/aam-to-rtcdp-evolution.png)

## 1. Betrachten Sie die Datenarchitektur in Audience Manager

Wenn Sie die Entwicklung von Audience Manager zu Real-Time CDP betrachten, ist jetzt ein kritischer Zeitpunkt für die Analyse Ihrer [Audience Manager-Segmente](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segments-purpose.html?lang=en) und bestimmen, was die [Signale](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-explorer/data-explorer-understanding-signals.html?lang=en), [Eigenschaften](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/trait-details-page.html?lang=en)und [Regeln](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/segments/segment-builder.html?lang=en#segment-builder-section) sind, aus denen sich diese Segmente zusammensetzen.

Denken Sie außerdem an die Datenquellen, die Sie derzeit in Audience Manager verwenden.

Adobe empfiehlt, Ihre Segmente wie folgt zu kategorisieren:

* Segmente, die über die [[!UICONTROL Audience Manager Source Connector]](/help/sources/connectors/adobe-applications/audience-manager.md), da sie keine Datenabhängigkeiten, keine Ziel- oder Aktivierungsprobleme haben und ihre Segmentierungsregeln über die Echtzeit-Kundendatenplattform erstellt werden können [Segment Builder](/help/segmentation/ui/segment-builder.md) später.
* Segmente mit Regeln, die unterstützt werden können, aber möglicherweise Daten enthalten, die in Real-Time CDP nicht verfügbar sind.
* Segmente, die nicht in der Echtzeit-Kundendatenplattform erstellt werden können und Funktionen fehlen.

>[!TIP]
>
>Adobe Real-Time CDP-Angebote [drei Arten der Segmentauswertung](/help/segmentation/home.md#evaluate-segments): [!UICONTROL Batch], [!UICONTROL Streaming]und [!UICONTROL Edge]. Kunden, die Echtzeit-Segmente in Audience Manager verwenden, können durch die aktuelle Beschränkung von 500 Streaming-Segmenten in Real-Time CDP eingeschränkt sein. Mehr dazu [Limits bei der Segmentierung](/help/profile/guardrails.md).

## 2. Welche Segmente müssen unbedingt über gesendet werden [!UICONTROL Audience Manager Source Connector]?

Basierend auf ihren Bewertungskriterien können Segmente ohne Datenabhängigkeiten, keine Ziel- oder Aktivierungsprobleme und ihre Segmentierungsregeln über die Real-Time CDP-Datenerfassung erstellt werden, z. B. [Adobe Experience Platform Web SDK](/help/edge/web-sdk-faq.md) zu einem späteren Zeitpunkt über den Audience Manager Source Connector gesendet werden.

## 3. Verwenden Sie die [!UICONTROL Experience Cloud Audiences] Ziel, um Daten an den Audience Manager zurückzubringen?

Segmente mit Regeln, die in Real-Time CDP unterstützt werden können, aber Aktivierungsabhängigkeiten zum Audience Manager haben, können über die [Experience Cloud Audiences](/help/destinations/catalog/adobe/experience-cloud-audiences.md) Zielkarte.

## 4. Welche Ziele haben Sie heute in Audience Manager eingerichtet, um mit dem Umzug nach Real-Time CDP zu beginnen?

Adobe empfiehlt dringend, dass Segmente in Audience Manager aktiviert werden, um [Benutzerbasierte Ziele](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=en) werden über die [!UICONTROL Audience Manager Source Connector], um dann über Real-Time CDP zu aktivieren.

Alle benutzerbezogenen Ziele, die in Audience Manager verfügbar sind: [Facebook](/help/destinations/catalog/social/facebook.md), [[!UICONTROL Google-Kundenabgleich]](/help/destinations/catalog/advertising/google-customer-match.md), [linkedIn](/help/destinations/catalog/social/linkedin.md) - sind auch in Real-Time CDP verfügbar.

Zusätzliche Erstanbieter-Daten- und Medienstrategiepartner wie [Pinterest](/help/destinations/catalog/advertising/pinterest.md), [Snapchat](/help/destinations/catalog/advertising/snap-inc.md), [TikTok](/help/destinations/catalog/social/tiktok.md), [Amazon Ads](/help/destinations/catalog/advertising/amazon-ads.md)und [[!UICONTROL Handelsabteilung]](/help/destinations/catalog/advertising/tradedesk.md) verfügbar sind.

Real-Time CDP unterstützt derzeit über 60 Ziele nativ im [Katalog](/help/destinations/catalog/overview.md), darunter mehr als 20 Werbeziele oder soziale Ziele, die die Zuordnung von Erstanbieterzielgruppen unterstützen.

## Nächste Schritte

Nachdem Sie diese Seite gelesen haben, müssen Sie jetzt eine Reihe von Überlegungen anstellen, die Sie beim Start Ihrer Evolution von Audience Manager nach Real-Time CDP berücksichtigen müssen.
