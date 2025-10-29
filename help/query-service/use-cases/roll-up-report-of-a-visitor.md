---
keywords: Experience Platform;Startseite;beliebte Themen;Abfrage-Service;Abfrage-Service;experienceEvent-Abfragen;experienceEvent-Abfrage;Erlebnisereignisabfrage;
title: Anzeigen eines Datenaggregationsberichts für eine bestimmte Besucherin oder einen bestimmten Besucher
description: Das folgende Dokument enthält Beispiele für Abfragen zu Erlebnisereignissen in Adobe Experience Platform Query Service.
exl-id: 1348503f-65c1-41f9-b111-1284a49449a1
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 1%

---

# Anzeigen eines Datenaggregationsberichts für eine bestimmte Besucherin oder einen bestimmten Besucher

Dieses Dokument enthält ein SQL-Beispiel zum Aggregieren von Daten aus mehreren Analytics-Eigenschaften für einen bestimmten Benutzer und zum Anzeigen dieser Daten in einem Bericht. Mit Adobe Experience Platform Query Service können Sie Abfragen schreiben, die [!DNL Experience Events] verwenden, um eine Vielzahl von Anwendungsfällen zu erfassen. Erlebnisereignisse werden durch die ExperienceEvent-Klasse des Experience-Datenmodells (XDM) dargestellt, die einen unveränderlichen und nicht aggregierten Schnappschuss des Systems erfasst, wenn ein Benutzer mit einer Website oder einem Service interagiert. Erlebnisereignisse können sogar für die Zeitbereichsanalyse verwendet werden. Weitere Anwendungsfälle, bei [ Besucherberichte erstellt werden ](#next-steps), finden Sie [!DNL Experience Events] Abschnitt „Nächste Schritte“.

Weitere Informationen zu XDM und [!DNL Experience Events] finden Sie in der [[!DNL XDM System] Übersicht](../../xdm/home.md). Durch die Kombination von Abfrage-Service und [!DNL Experience Events] können Sie Verhaltenstrends bei Ihren Benutzenden effektiv verfolgen. Im folgenden Dokument finden Sie Beispiele für Abfragen mit [!DNL Experience Events].

## Zielvorgabe

Das folgende SQL-Beispiel zeigt, wie ein Aggregatbericht mit verschiedenen Analysewerten für einen bestimmten Benutzer angezeigt wird.

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
|----------------------------------+-----------+-------+-------+-------+--------------
457C3510571E5930-69AA721C4CBF9339 |     706.0 | 83.0  |  7.0  | 38.0  |          22
```

## Nächste Schritte {#next-steps}

Durch dieses Dokument erhalten Sie ein besseres Verständnis dafür, wie Sie den Abfrage-Service mit [!DNL Experience Events] verwenden, um einen aggregierten Bericht mit Analysewerten für einen bestimmten Benutzer anzuzeigen.

In den folgenden Anwendungsfällen erfahren Sie mehr über andere besucherbasierte Anwendungsfälle:

- [Abrufen einer Liste von Besuchern, sortiert nach der Anzahl der Seitenansichten.](./visitors-by-number-of-page-views.md)
- [Auflisten der vorherigen Sitzungen eines Besuchers.](./list-visitor-sessions.md)
- [Erstellen Sie einen Trend-Bericht mit Ereignissen nach Tag.](./trended-report-of-events.md)
