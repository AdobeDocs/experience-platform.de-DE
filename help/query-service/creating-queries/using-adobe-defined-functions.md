---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe-definierte Funktionen
topic: queries
translation-type: tm+mt
source-git-commit: cc101b1a439408861961c6fcd0899ca7c48bfa04
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 85%

---


# Verwenden von Adobe-definierten Funktionen

Einer der Hauptvorteile von Adobe besteht darin, dass Adobe Erlebnisdaten genau kennt und weiß, was Kunden mit diesen Daten machen wollen. So können Sie Hilfsfunktionen entwickeln, die Ihnen die Arbeit erleichtern.

Das vorliegende Dokument deckt Adobe-definierte Funktionen (ADFs) zur Unterstützung von drei wichtigen Analyseaktivitäten ab:
- [Sessionization](#sessionization)
- [Attribution](#attribution)
- [Pathing](#pathing)

## Sessionization

Der `SESS_TIMEOUT()` reproduziert die in Adobe Analytics gefundenen Besuchergruppen. Er führt eine ähnliche zeitbasierte Gruppierung durch, jedoch mit anpassbaren Parametern.

**Syntax:**

`SESS_TIMEOUT(timestamp, timeout_in_seconds) OVER ([partition] [order] [frame])`

**Rückgabe:**

Struktur mit Feldern `(timestamp_diff, num, is_new, depth)`

### `SESS_TIMEOUT()` auf der Zeilenebene und Ausgabe prüfen

```sql
SELECT analyticsVisitor,
      session.is_new,
      session.timestamp_diff,
      session.num,
      session.depth
FROM  (
        SELECT endUserIDs._experience.aaid.id as analyticsVisitor,
        SESS_TIMEOUT(timestamp, 60 * 30)
        OVER (PARTITION BY endUserIDs._experience.aaid.id
        ORDER BY timestamp
        ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
        AS session
        FROM your_analytics_table
        WHERE _ACP_YEAR = 2018
      )
LIMIT 100;
```

![Bild](../images/queries/adobe-functions/sess-timeout.png)

### Neuen Trendbericht mit Besuchern, Sitzungen und Seitenansichten erstellen

```sql
SELECT
      date_format( from_utc_timestamp(timestamp, 'EDT') , 'yyyy-MM-dd') as Day,
      COUNT(DISTINCT analyticsVisitor ) as Visitors,
      COUNT(DISTINCT analyticsVisitor || session.num ) as Sessions,
      SUM( PageViews ) as PageViews
FROM
    (
      SELECT
          timestamp,
          endUserIDs._experience.aaid.id as analyticsVisitor,
          SESS_TIMEOUT(timestamp, 60 * 30)
      OVER (PARTITION BY endUserIDs._experience.aaid.id
      ORDER BY timestamp
      ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS session,
          web.webPageDetails.pageviews.value as PageViews
      FROM your_analytics_table
      WHERE _ACP_YEAR = 2018
    )
GROUP BY Day 
ORDER BY Day DESC 
LIMIT 31;
```

![Bild](../images/queries/adobe-functions/trended-report.png)

## Attribution

Bei der Attribution werden Metriken oder Konversionen wie Umsätze, Bestellungen oder Anmeldungen Ihren Marketing-Bemühungen zugeordnet.

In Adobe Analytics werden Attributionseinstellungen mithilfe von Variablen wie eVars konfiguriert und bei der Erfassung von Daten generiert.

Die Attribution-ADFs, die in Query Service vorhanden sind, ermöglichen das Definieren und Generieren dieser Zuordnungen zur Abfragezeit.

In diesem Beispiel geht es um „Last Touch“-Attribution; Adobe unterstützt aber auch „First Touch“-Attribution.

>[!NOTE]
>
>Andere Optionen mit Timeouts und ereignisbasiertem Ablaufen werden in zukünftigen Versionen von Query Service zur Verfügung stehen.

**Syntax:**

`ATTRIBUTION_LAST_TOUCH(timestamp, [channel_name], column) OVER ([partition] [order] [frame])`

**Rückgabe:**

Struktur mit Feld `(value)`

### Attribution auf der Zeilenebene erkunden

```sql
SELECT
  endUserIds._experience.aaid.id,
  _experience.analytics.customDimensions.evars.evar10 as MemberLevel,
  ATTRIBUTION_LAST_TOUCH(timestamp, 'eVar10', _experience.analytics.customDimensions.evars.evar10)
      OVER(PARTITION BY endUserIds._experience.aaid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW).value
      AS LastMemberLevel,
  commerce.purchases.value as Orders
FROM your_analytics_table 
WHERE _ACP_YEAR=2018 AND _ACP_MONTH=4
LIMIT 50;
```

![Bild](../images/queries/adobe-functions/row-level-attribution.png)

### Aufschlüsselung von Bestellungen nach letzter Mitgliederebene erstellen (eVar10)

```sql
SELECT
  LastMemberLevel,
  SUM(Orders) as MemberLevelOrders
FROM 
(SELECT
  ATTRIBUTION_LAST_TOUCH(timestamp, 'eVar10', _experience.analytics.customDimensions.evars.evar10)
      OVER(PARTITION BY endUserIds._experience.aaid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW).value
      AS LastMemberLevel,
  commerce.purchases.value as Orders
FROM your_analytics_table 
WHERE _ACP_YEAR=2018 AND _ACP_MONTH=4
)
GROUP BY LastMemberLevel 
ORDER BY MemberLevelOrders DESC
LIMIT 25;
```

![Bild](../images/queries/adobe-functions/last-member-level.png)

## Pathing

Pathing hilft zu verstehen, wie Kunden durch Ihre Site navigieren. Die ADFs `NEXT()` und `PREVIOUS()` machen dies möglich.

**Syntax:**

```
NEXT(key, [shift, [ignoreNulls]]) OVER ([partition] [order] [frame])
PREVIOUS(key, [shift, [ignoreNulls]]) OVER ([partition] [order] [frame])
```

**Rückgabe:**

Struktur mit Feld `(value)`

### Aktuelle Seite und nächste Seite auswählen

```sql
SELECT 
      endUserIds._experience.aaid.id,
      timestamp,
      web.webPageDetails.name,
      NEXT(web.webPageDetails.name, 1, true)
          OVER(PARTITION BY endUserIds._experience.aaid.id
              ORDER BY timestamp
              ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING).value
          AS next_pagename
FROM your_analytics_table
WHERE _ACP_YEAR=2018 
LIMIT 10;
```

![Bild](../images/queries/adobe-functions/select-current-page.png)

### Detailbericht für die fünf häufigsten Seitennamen bei Anfang der Sitzung erstellen

```sql
  SELECT 
    PageName,
    PageName_2,
    PageName_3,
    PageName_4,
    PageName_5,
    SUM(PageViews) as PageViews
  FROM
    (SELECT
      PageName,
      NEXT(PageName, 1, true)
        OVER(PARTITION BY VisitorID, session.num
              ORDER BY timestamp
              ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING).value
        AS PageName_2,
      NEXT(PageName, 2, true)
        OVER(PARTITION BY VisitorID, session.num
              ORDER BY timestamp
              ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING).value
        AS PageName_3,
      NEXT(PageName, 3, true)
         OVER(PARTITION BY VisitorID, session.num
              ORDER BY timestamp
              ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING).value
        AS PageName_4,
      NEXT(PageName, 4, true)
         OVER(PARTITION BY VisitorID, session.num
              ORDER BY timestamp
              ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING).value
        AS PageName_5,
      PageViews,
      session.depth AS SessionPageDepth
    FROM
      (SELECT
        endUserIds._experience.aaid.id as VisitorID,
        timestamp,
        web.webPageDetails.pageviews.value AS PageViews,
        web.webPageDetails.name AS PageName,
        SESS_TIMEOUT(timestamp, 60 * 30) 
          OVER (PARTITION BY endUserIDs._experience.aaid.id 
                ORDER BY timestamp 
                ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
        AS session
      FROM your_analytics_table
      WHERE _ACP_YEAR=2018)
    )
  WHERE SessionPageDepth=1
  GROUP BY PageName, PageName_2, PageName_3, PageName_4, PageName_5
  ORDER BY PageViews DESC
  LIMIT 100;
```

![Bild](../images/queries/adobe-functions/create-breakdown-report.png)

## Zusätzliche Ressourcen

Das folgende Video zeigt, wie Abfragen in der Benutzeroberfläche der Adobe Experience Platform und in einem PSQL-Client ausgeführt werden. Darüber hinaus verwendet das Video Beispiele für einzelne Eigenschaften in einem XDM-Objekt, unter Verwendung von von Adobe definierten Funktionen und unter Verwendung von CREATE TABLE AS SELECT (CTAS).

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

