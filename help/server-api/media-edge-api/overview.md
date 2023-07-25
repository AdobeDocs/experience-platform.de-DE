---
solution: Experience Platform
title: Media Edge-APIs
description: Media Edge-APIs – Übersicht
source-git-commit: ff4bc64843e3d05277f56ab67b60400fb9e65c4f
workflow-type: ht
source-wordcount: '393'
ht-degree: 100%

---


# Media Edge-APIs – Übersicht

Media Edge-APIs basieren auf Adobe Experience Platform, um Medienereignis-Tracking-Daten im Rahmen von [XDM-Schemata](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=de#:~:text=Experience%20Data%20Model%20(XDM)%2C,the%20power%20of%20digital%20experiences) bereitzustellen. Media Analytics-Kundinnen und -Kunden erhalten dadurch die folgenden Funktionen:

* Mit [Adobe Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=de) können Kundinnen und Kunden detaillierte Details zu Dauer, Start und Stopp nahezu in Echtzeit abrufen, um diese Informationen für Medienmetriken auszuwerten und zu kombinieren. Kundinnen und Kunden, die von Adobe Analytics migrieren, stehen alle Berichtsmetriken in Adobe Customer Journey Analytics zur Verfügung.

* Mit [Adobe Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html?lang=de) können Kundinnen und Kunden ihre Echtzeitprofile mit Daten zum Medienkonsum anreichern.

* Mit [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=de) können Kundinnen und Kunden Omni-Channel-Kampagnen optimieren und Journeys mithilfe von Indikatoren zum Medienkonsum automatisieren.


## Optimieren von Medien-Tracking-Datenflüssen

Sowohl [Mediensammlungs-APIs](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-overview.html?lang=de&amp;media-tracking-data-flows) als auch Media Edge-APIs stellen Medien-Tracking-Daten als RESTful-Services bereit. Die Nutzung des Media Edge-Service bietet jedoch die folgenden Vorteile:

* Dies ist die einfachste Möglichkeit, um XDM-Schemata in Ihren Datenfluss zu integrieren.

* Aufrufe werden von einem Media Player direkt an das [Experience Edge Platform-Netzwerk](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=de) umgeleitet.

* Medienereignisse werden effizient mit einem Minimum an Server-übergreifenden Aufrufen nachverfolgt.

Die folgende Tabelle zeigt einen möglichen Adobe-API-Service für verschiedene Media Analytics-Fälle:

| Anwendungsfall | API-Service |
| -------- | ----------- |
| Adobe Experience Platform-Lösung | Media Edge |
| Real-Time CDP + Customer Journey Analytics | Media Edge |
| Adobe Analytics + Adobe Experience Platform-Lösung | Media Edge |
| Nur Adobe Analytics (bereits mit Tracking) | Mediensammlung |

>[!NOTE]
>
> Der Mediensammlungs-API-Service für Analytics empfängt weiterhin XDM-Daten, ist dafür jedoch nicht im selben Umfang wie der Media Edge-Service optimiert. Je nach den vom Media Player gesendeten Daten können einige reine Analytics-Daten auch über den Media Edge-API-Service weitergeleitet werden.

Die folgende Abbildung zeigt die Datenflüsse für die beiden API-Services:

![Media Analytics-Datenflüsse](../assets/edge-api-dataflow.png)

## Nächste Schritte

* Weitere Informationen zum Verwenden von Media Edge-APIs finden Sie in der [Dokumentation „Erste Schritte“](getting-started.md).

* Weitere Informationen zum Arbeiten mit Platform Edge finden Sie unter [Installieren von Media Analytics mit Experience Platform Edge](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/implementation-edge.html?lang=de).




