---
solution: Experience Platform
title: Media Edge-APIs
description: Übersicht über Media Edge-APIs
source-git-commit: ff4bc64843e3d05277f56ab67b60400fb9e65c4f
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 5%

---


# Übersicht über die Media Edge API

Media Edge-APIs basieren auf der Adobe Experience Platform, um Medienereignis-Tracking-Daten im Rahmen von [XDM-Schemata](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=en#:~:text=Experience%20Data%20Model%20(XDM)%2C,the%20power%20of%20digital%20experiences). Kunden von Media Analytics erhalten dadurch die folgenden Funktionen:

* Mit [Adobe Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=de), können Kunden nahezu detaillierte Details zur Dauer, zu Start und Stopp in Echtzeit abrufen, um sie für Medienmetriken zu bewerten und zu kombinieren. Für Kunden, die aus Adobe Analytics migrieren, sind alle Berichtsmetriken in Adobe Customer Journey Analytics verfügbar.

* Mit [Adobe Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html?lang=de), können Kunden ihre Echtzeitprofile mit Daten zur Medienkonsum anreichern.

* Mit [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=en), können Kunden Omnichannel-Kampagnen optimieren und Journey mit Medienkonsumsignalen automatisieren.


## Optimieren von Medien-Tracking-Datenflüssen

Beide [Mediensammlungs-APIs](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-overview.html?lang=en&amp;media-tracking-data-flows) und Media Edge-APIs stellen Medien-Tracking-Daten als RESTful-Dienste bereit. Die Verwendung des Media Edge-Dienstes hat jedoch die folgenden Vorteile:

* Dies ist die einfachste Möglichkeit, XDM-Schemas in Ihren Datenfluss zu integrieren.

* Aufrufe werden von einem Medienplayer direkt an die [Experience Edge Platform-Netzwerk](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=en).

* Sie verfolgt Medienereignisse effizient mit einem Minimum an Server-übergreifenden Aufrufen.

Die folgende Tabelle zeigt einen möglichen Adobe-API-Dienst für verschiedene Medienanalysefälle:

| Anwendungsfall | API-Dienst |
| -------- | ----------- |
| Adobe Experience Platform-Lösung | Medien-Edge |
| Echtzeit-Kundendatenplattform und -Customer Journey Analytics | Medien-Edge |
| Adobe Analytics- und Adobe Experience Platform-Lösung | Medien-Edge |
| Nur Adobe Analytics (bereits Tracking) | Mediensammlung |

>[!NOTE]
>
> Der Mediensammlungs-API-Dienst für Analytics empfängt weiterhin XDM-Daten, ist jedoch nicht so weit optimiert, wie der Media Edge-Dienst dies ist. Je nach den vom Media Player gesendeten Daten können einige Nur-Analytics-Daten auch über den Media Edge API-Dienst weitergeleitet werden.

Die folgende Abbildung zeigt die Datenflüsse für die beiden API-Dienste:

![Datenflüsse für Medienanalysen](../assets/edge-api-dataflow.png)

## Nächste Schritte

* Weitere Informationen zur Verwendung von Media Edge-APIs finden Sie im Abschnitt [Erste Schritte - Dokumentation](getting-started.md).

* Weitere Informationen zum Arbeiten mit Platform Edge finden Sie unter [Installieren von Media Analytics mit Experience Platform Edge](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/implementation-edge.html?lang=en).




