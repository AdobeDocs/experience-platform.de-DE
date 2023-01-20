---
keywords: Experience Platform; Startseite; beliebte Themen; Abfragedienst; Query Service; Erlebnisereignisabfragen; Erlebnisereignisabfrage; Erlebnisereignisabfrage;
title: Besucher nach Anzahl Seitenansichten auflisten
description: Erfahren Sie, wie Sie Abfragen schreiben, die Erlebnisereignisse verwenden, um eine Liste von Besuchern abzurufen, die nach der Anzahl der Seitenansichten organisiert ist.
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 1%

---

# Besucher nach Anzahl der Seitenansichten auflisten

Dieses Dokument enthält ein Beispiel für SQL, das zum Abrufen einer Liste von Besuchern erforderlich ist, die nach der Anzahl der Seitenansichten organisiert sind. Mit Adobe Experience Platform Query Service können Sie Abfragen schreiben, die [!DNL Experience Events] , um eine Vielzahl von Anwendungsfällen zu erfassen. Erlebnisereignisse werden durch die Experience-Datenmodell (XDM)-ExperienceEvent-Klasse repräsentiert, die einen unveränderlichen und nicht aggregierten Schnappschuss des Systems erfasst, wenn ein Benutzer mit einer Website oder einem Dienst interagiert. Erlebnisereignisse können sogar für die Zeitbereichsanalyse verwendet werden. Siehe [Abschnitt mit den nächsten Schritten](#next-steps) für weitere Anwendungsfälle, bei denen [!DNL Experience Events] , um Besucherberichte zu generieren.

Weitere Informationen zu XDM und [!DNL Experience Events] finden Sie im Abschnitt [[!DNL XDM System] Übersicht](../../xdm/home.md). Durch Kombination von Query Service mit [!DNL Experience Events]können Sie Verhaltenstrends unter Ihren Benutzern effektiv verfolgen. Das folgende Dokument enthält Beispiele für Abfragen, die Folgendes beinhalten: [!DNL Experience Events].

## Ziel

Im folgenden Beispiel wird ein Bericht erstellt, in dem die 10 IDs der Benutzer aufgelistet werden, die die meisten Seiten angezeigt haben.

```sql
SELECT 
endUserIds._experience.aaid.id, 
SUM(web.webPageDetails.pageviews.value) as pageViews 
FROM your_analytics_table
GROUP BY endUserIds._experience.aaid.id 
ORDER BY pageViews DESC
LIMIT 10;
```

Die Abfrageergebnisse werden in der folgenden Tabelle angezeigt.

```console
               id                  | pageViews
-----------------------------------+-----------
 457C3510571E5930-69AA721C4CBF9339 |     706.0
 776F85658792C017-6491FE6570382A01 |     700.0
 6BEC9C6AB52E779F-28F5B023113F2C85 |     654.0
 1C0CCFB2DC63611E-6E4A4D4142AEB613 |     642.0
 112EE9A6F3BE29D1-514A6C355A2C9EF6 |     629.0
 CCC75A0E6AC7F2FA-11D58515D370F626 |     624.0
 749F850A44153120-3710C53FA2162349 |     614.0
 2B668C6DDDAF0C505-92EDCC072F7CDDA |     587.0
 7EB7257335935320-101921AF45111FE6 |     586.0
 5F4759CA80DCA9C9-2C0DA93D80D9DBFA |     586.0
(10 rows)
```

## Nächste Schritte {#next-steps}

Durch Lesen dieses Dokuments erhalten Sie ein besseres Verständnis dafür, wie Sie Query Service mit [!DNL Experience Events] , um Benutzer aufzulisten, die die meisten Seiten angezeigt haben.

In den folgenden Anwendungsfällen erfahren Sie mehr über andere besucherbasierte Anwendungsfälle:

- [Auflisten der vorherigen Sitzungen eines Besuchers.](./list-visitor-sessions.md)
- [Zeigen Sie einen Rollup-Bericht eines Besuchers an.](./roll-up-report-of-a-visitor.md)
- [Erstellen Sie einen Trendbericht mit Ereignissen nach Tag.](./trended-report-of-events.md)
