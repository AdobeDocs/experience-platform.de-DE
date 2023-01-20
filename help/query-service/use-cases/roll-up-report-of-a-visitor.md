---
keywords: Experience Platform; Startseite; beliebte Themen; Abfragedienst; Query Service; Erlebnisereignisabfragen; Erlebnisereignisabfrage; Erlebnisereignisabfrage;
title: Anzeigen eines Rollup-Berichts für einen bestimmten Besucher
description: Das folgende Dokument enthält Beispiele für Abfragen, die Erlebnisereignisse in Adobe Experience Platform Query Service beinhalten.
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 1%

---

# Anzeigen eines Rollup-Berichts für einen bestimmten Besucher

Dieses Dokument bietet ein SQL-Beispiel zum Aggregieren von Daten aus mehreren Analytics-Eigenschaften für einen bestimmten Benutzer und zum Anzeigen dieser Daten in einem Bericht. Mit Adobe Experience Platform Query Service können Sie Abfragen schreiben, die [!DNL Experience Events] , um eine Vielzahl von Anwendungsfällen zu erfassen. Erlebnisereignisse werden durch die Experience-Datenmodell (XDM)-ExperienceEvent-Klasse repräsentiert, die einen unveränderlichen und nicht aggregierten Schnappschuss des Systems erfasst, wenn ein Benutzer mit einer Website oder einem Dienst interagiert. Erlebnisereignisse können sogar für die Zeitbereichsanalyse verwendet werden. Siehe [Abschnitt mit den nächsten Schritten](#next-steps) für weitere Anwendungsfälle, bei denen [!DNL Experience Events] , um Besucherberichte zu generieren.

Weitere Informationen zu XDM und [!DNL Experience Events] finden Sie im Abschnitt [[!DNL XDM System] Übersicht](../../xdm/home.md). Durch Kombination von Query Service mit [!DNL Experience Events]können Sie Verhaltenstrends unter Ihren Benutzern effektiv verfolgen. Das folgende Dokument enthält Beispiele für Abfragen, die Folgendes beinhalten: [!DNL Experience Events].

## Ziel

Das folgende SQL-Beispiel zeigt, wie ein aggregierter Bericht mit verschiedenen Analysewerten für einen bestimmten Benutzer angezeigt wird.

```sql
SELECT 
endUserIds._experience.aaid.id, 
SUM(web.webPageDetails.pageviews.value) as pageViews, 
SUM(_experience.analytics.event1to100.event1.value) as A, 
SUM(_experience.analytics.event1to100.event2.value) as B, 
SUM(_experience.analytics.event1to100.event3.value) as C,
SUM(
    CASE 
    WHEN _experience.analytics.customDimensions.evars.evar1 = 'parkas' 
    THEN 1 
    ELSE 0 
    END) as viewedParkas
FROM your_analytics_table 
WHERE endUserIds._experience.aaid.id = '457C3510571E5930-69AA721C4CBF9339' 
GROUP BY endUserIds._experience.aaid.id
ORDER BY pageViews DESC;
```

Die Abfrageergebnisse werden in der folgenden Tabelle angezeigt.

```console
               id                 | pageViews |   A   |   B   |   C   | viewedParkas
----------------------------------+-----------+-------+-------+-------+--------------
457C3510571E5930-69AA721C4CBF9339 |     706.0 | 83.0  |  7.0  | 38.0  |          22
```

## Nächste Schritte {#next-steps}

Durch Lesen dieses Dokuments erhalten Sie ein besseres Verständnis dafür, wie Sie Query Service mit [!DNL Experience Events] , um einen aggregierten Bericht mit Analysewerten für einen bestimmten Benutzer anzuzeigen.

In den folgenden Anwendungsfällen erfahren Sie mehr über andere besucherbasierte Anwendungsfälle:

- [Rufen Sie eine Liste von Besuchern ab, die nach der Anzahl der Seitenansichten organisiert sind.](./visitors-by-number-of-page-views.md)
- [Auflisten der vorherigen Sitzungen eines Besuchers.](./list-visitor-sessions.md)
- [Erstellen Sie einen Trendbericht mit Ereignissen nach Tag.](./trended-report-of-events.md)
