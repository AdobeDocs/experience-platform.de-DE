---
keywords: Experience Platform;Startseite;beliebte Themen;Abfrage-Service;Abfrage-Service;experienceEvent-Abfragen;experienceEvent-Abfrage;Erlebnisereignisabfrage;
title: Besuchende nach Anzahl der Seitenansichten auflisten
description: Erfahren Sie, wie Sie Abfragen schreiben, die Erlebnisereignisse verwenden, um eine Liste der Besucher abzurufen, die nach der Anzahl der Seitenansichten organisiert ist.
exl-id: 6e8eed0c-838e-4cd0-ae8c-453114fbf4ea
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 1%

---

# Besuchende nach Anzahl der Seitenansichten auflisten

Dieses Dokument enthält ein Beispiel für den SQL-Code, der zum Abrufen einer Besucherliste erforderlich ist, die nach der Anzahl der Seitenansichten organisiert ist. Mit Adobe Experience Platform Query Service können Sie Abfragen schreiben, die [!DNL Experience Events] verwenden, um eine Vielzahl von Anwendungsfällen zu erfassen. Erlebnisereignisse werden durch die ExperienceEvent-Klasse des Experience-Datenmodells (XDM) dargestellt, die einen unveränderlichen und nicht aggregierten Schnappschuss des Systems erfasst, wenn ein Benutzer mit einer Website oder einem Service interagiert. Erlebnisereignisse können sogar für die Zeitbereichsanalyse verwendet werden. Weitere Anwendungsfälle, bei [&#128279;](#next-steps) Besucherberichte erstellt werden [!DNL Experience Events], finden Sie  Abschnitt „Nächste Schritte“.

Weitere Informationen zu XDM und [!DNL Experience Events] finden Sie in der [[!DNL XDM System] Übersicht](../../xdm/home.md). Durch die Kombination von Abfrage-Service und [!DNL Experience Events] können Sie Verhaltenstrends bei Ihren Benutzenden effektiv verfolgen. Im folgenden Dokument finden Sie Beispiele für Abfragen mit [!DNL Experience Events].

## Ziel

Im folgenden Beispiel wird ein Bericht erstellt, der die 10 IDs der Benutzer auflistet, die die meisten Seiten angesehen haben.

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

Durch das Lesen dieses Dokuments erhalten Sie ein besseres Verständnis dafür, wie Sie Query Service mit [!DNL Experience Events] verwenden können, um Benutzer aufzulisten, die die meisten Seiten angesehen haben.

In den folgenden Anwendungsfällen erfahren Sie mehr über andere besucherbasierte Anwendungsfälle:

- [Auflisten der vorherigen Sitzungen eines Besuchers.](./list-visitor-sessions.md)
- [Anzeigen eines Datenaggregationsberichts eines Besuchers.](./roll-up-report-of-a-visitor.md)
- [Erstellen Sie einen Trend-Bericht mit Ereignissen nach Tag.](./trended-report-of-events.md)
