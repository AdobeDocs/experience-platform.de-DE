---
keywords: Experience Platform; Medien-Edge; beliebte Themen; Datumsbereich
solution: Experience Platform
title: Media Edge-APIs
description: Übersicht über Media Edge-APIs.
exl-id: null
source-git-commit: f040ba6d1403da4212fe279e32316bac995905b2
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 5%

---


# Übersicht über die Media Edge API

Media Edge-APIs basieren auf Adobe Experience Platform (AEP), um Medienereignis-Tracking-Daten im Rahmen von [XDM-Schemata](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=en#:~:text=Experience%20Data%20Model%20(XDM)%2C,the%20power%20of%20digital%20experiences). Kunden von Media Analytics erhalten dadurch die folgenden Funktionen:

* Mit [Customer Journey Analytics (CJA)](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=de), können Kunden nahezu detaillierte Details zur Dauer, zu Start und Stopp in Echtzeit abrufen, um sie für Medienmetriken zu bewerten und zu kombinieren. Für Kunden, die aus Adobe Analytics migrieren, stehen in Customer Journey Analytics alle Berichtsmetriken zur Verfügung.

* Mit [Adobe Real-time Customer Data Platform (CDP)](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html?lang=de), können Kunden ihre Echtzeitprofile mit Daten zur Medienkonsum anreichern.

* Mit [Adobe Journey Optimizer (AJO)](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=en), können Kunden Omnichannel-Kampagnen optimieren und Journey mit Medienkonsumsignalen automatisieren.


## Optimieren von Medien-Tracking-Datenflüssen

Beide [Mediensammlung](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-overview.html?lang=en&amp;media-tracking-data-flows) APIs und Media Edge-APIs stellen Medien-Tracking-Daten als RESTful-Dienste bereit. Die Verwendung des Media Edge-Dienstes hat jedoch die folgenden Vorteile:

* Dies ist die einfachste Möglichkeit, XDM-Schemas in Ihren Datenfluss zu integrieren.

* Aufrufe werden von einem Medienplayer direkt an die [Experience Edge Platform-Netzwerk](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=en).

* Medienereignisse werden am effizientesten verfolgt.

In der folgenden Tabelle finden Sie den besten Adobe-API-Dienst für verschiedene Medienanalysefälle:

| Anwendungsfall | Plattform | API-Dienst |
| -------- | ------ | ---------- |
| CJA | AEP | Medien-Edge |
| CDP + CJA | AEP | Medien-Edge |
| Analytics + CJA | AEP | Medien-Edge |
| Legacy Analytics | K. A. | Mediensammlung |

>[!NOTE]
>
> Der Mediensammlungs-API-Dienst für Analytics empfängt weiterhin XDM-Daten, ist jedoch nicht so weit optimiert, wie der Media Edge-Dienst dies ist. Je nach den vom Media Player gesendeten Daten können einige Nur-Analytics-Daten auch über den Media Edge API-Dienst weitergeleitet werden.

Die folgende Abbildung zeigt die Datenflüsse für die beiden API-Dienste:


![Datenflüsse für Medienanalysen](../assets/edge-api-dataflow.png)


Weitere Informationen zur Verwendung von Media Edge-APIs finden Sie in der Dokumentation zu den ersten Schritten .

Weitere Informationen zum Arbeiten mit Platform Edge finden Sie unter [Installieren von Media Analytics mit Experience Platform Edge](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/implementation-edge.html?lang=en).




