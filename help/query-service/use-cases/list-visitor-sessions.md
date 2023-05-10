---
keywords: Experience Platform; Startseite; beliebte Themen; Abfragedienst; Query Service; Erlebnisereignisabfragen; Erlebnisereignisabfrage; Erlebnisereignisabfrage;
title: Auflisten der Seitenansichten eines Benutzers
description: Erfahren Sie, wie Sie Abfragen schreiben, die Erlebnisereignisse verwenden, um eine Liste der letzten 100 Seiten zu erstellen, die ein bestimmter Benutzer verwendet hat.
exl-id: d831910d-d3a4-4a5a-b897-b09f0546dab0
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 8%

---

# Auflisten der Seitenansichten von Benutzenden

Dieses Dokument enthält ein Beispiel für die SQL, die erforderlich ist, um die Seitenansichten eines bestimmten Benutzers aufzulisten. Mit Adobe Experience Platform Query Service können Sie Abfragen schreiben, die [!DNL Experience Events] , um eine Vielzahl von Anwendungsfällen zu erfassen. Erlebnisereignisse werden durch die Experience-Datenmodell (XDM)-ExperienceEvent-Klasse repräsentiert, die einen unveränderlichen und nicht aggregierten Schnappschuss des Systems erfasst, wenn ein Benutzer mit einer Website oder einem Dienst interagiert. Erlebnisereignisse können sogar für die Zeitbereichsanalyse verwendet werden. Siehe [Abschnitt mit den nächsten Schritten](#next-steps) für weitere Anwendungsfälle, bei denen [!DNL Experience Events] , um Besucherberichte zu generieren.

Weitere Informationen zu XDM und [!DNL Experience Events] finden Sie im Abschnitt [[!DNL XDM System] Übersicht](../../xdm/home.md). Durch Kombination von Query Service mit [!DNL Experience Events]können Sie Verhaltenstrends unter Ihren Benutzern effektiv verfolgen. Das folgende Dokument enthält Beispiele für Abfragen, die Folgendes beinhalten: [!DNL Experience Events].

## Ziel

Im folgenden Beispiel werden die letzten 100 Seiten aufgelistet, die ein bestimmter Benutzer angezeigt hat.

```sql
SELECT 
timestamp, 
web.webReferrer.type as referrerType, 
web.webReferrer.URL as referrer, 
web.webPageDetails.name as pageName, 
_experience.analytics.event1to100.event1.value as A, 
_experience.analytics.event1to100.event2.value as B, 
_experience.analytics.event1to100.event3.value as C, 
web.webPageDetails.pageviews.value as pageViews
FROM your_analytics_table 
WHERE endUserIds._experience.aaid.id = '457C3510571E5930-69AA721C4CBF9339' 
ORDER BY timestamp 
LIMIT 100;
```

Die Ergebnisse dieser Abfrage sind unten dargestellt.

```console
      timestamp       |  referrerType  |                            referrer                                |                 pageName            |  A  |  B  |  C  | pageViews
----------------------+----------------+--------------------------------------------------------------------+-------------------------------------+-----+-----+-----+--------------
2019-11-08 17:15:28.0 | typed_bookmark |                                                                    |                                     |     |     |     |
2019-11-08 17:53:05.0 | social         | http://www.reddit.com                                              | Home                                |     |     |     |          1.0
2019-11-08 17:53:45.0 | typed_bookmark |                                                                    | Kids                                |     |     |     |          1.0
2019-11-08 19:22:34.0 | typed_bookmark |                                                                    |                                     |     |     |     |          
2019-11-08 20:01:12.0 | search_engine  | http://www.google.com/search?ie=UTF-8&q=laundry parkas&cid=sem:115 | Home                                |     |     |     |          1.0 
2019-11-08 20:01:57.0 | typed_bookmark |                                                                    | Kids                                |     |     |     |          1.0
2019-11-08 20:03:36.0 | typed_bookmark |                                                                    | Search Results                      | 1.0 |     |     |          1.0
2019-11-08 20:04:30.0 | typed_bookmark |                                                                    | Product Details: Pemmican Power Bar |     |     |     |          1.0
2019-11-08 20:05:27.0 | typed_bookmark |                                                                    | Shopping Cart: Cart Details         |     |     |     |          1.0
2019-11-08 20:06:07.0 | typed_bookmark |                                                                    | Shopping Cart: Shipping Information |     |     |     |          1.0
2019-11-08 20:07:02.0 | typed_bookmark |                                                                    | Shopping Cart: Billing Information  |     |     | 1.0 |          1.0
2019-11-08 20:07:52.0 | typed_bookmark |                                                                    | Shopping Cart: Order Review         |     |     |     |          1.0
2019-11-08 20:08:45.0 | typed_bookmark |                                                                    | Order Confirmation                  |     |     |     |          1.0
2019-11-08 20:09:24.0 | typed_bookmark |                                                                    | Home                                |     |     |     |          1.0
2019-11-08 20:10:03.0 | typed_bookmark |                                                                    | Editorial Page: Camping Essentials  |     |     |     |          1.0
2019-11-08 20:11:01.0 | typed_bookmark |                                                                    | Account Registration|Form           |     |     |     |          1.0
2019-11-08 20:11:38.0 | typed_bookmark |                                                                    | Seasonal Sale                       |     |     |     |          1.0
2019-11-08 20:12:10.0 | typed_bookmark |                                                                    | Blog: Iris Sagan                    |     |     |     |          1.0
2019-11-08 20:13:09.0 | typed_bookmark |                                                                    | Product Details: UltraTech Socks    |     |     |     |          1.0
2019-11-08 20:14:05.0 | typed_bookmark |                                                                    | Seasonal Sale                       |     |     |     |          1.0
```

## Nächste Schritte {#next-steps}

Durch Lesen dieses Dokuments erhalten Sie ein besseres Verständnis dafür, wie Sie Query Service mit [!DNL Experience Events] , um die Seitenansichten als angegebenen Benutzer aufzulisten.

In den folgenden Anwendungsfällen erfahren Sie mehr über andere besucherbasierte Anwendungsfälle:

- [Rufen Sie eine Liste von Besuchern ab, die nach der Anzahl der Seitenansichten organisiert sind.](./visitors-by-number-of-page-views.md)
- [Zeigen Sie einen Rollup-Bericht eines Besuchers an.](./roll-up-report-of-a-visitor.md)
- [Erstellen Sie einen Trendbericht mit Ereignissen nach Tag.](./trended-report-of-events.md)
