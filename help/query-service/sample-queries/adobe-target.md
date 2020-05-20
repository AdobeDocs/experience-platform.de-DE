---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Sample queries
topic: queries
translation-type: tm+mt
source-git-commit: 33282b1c8ab1129344bd4d7054e86fed75e7b899
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 2%

---


# Beispieldaten für Abfragen zur Adobe-Zielgruppe

Daten aus Adobe Zielgruppe werden in Experience Ereignis XDM-Schema umgewandelt und als Datensätze in Experience Platform integriert. There are many use cases for Query Service with this data, and the following sample queries should work with your Adobe Target datasets.

>[!NOTE]
>In den folgenden Beispielen müssen Sie SQL bearbeiten, um die erwarteten Parameter für Ihre Abfragen basierend auf dem Datensatz, den Variablen oder dem Zeitrahmen, den Sie bewerten möchten, auszufüllen. Geben Sie Parameter an, wo immer Sie `{ }` in SQL sehen.

## Standarddataset-Name für die Zielgruppe der Datenquelle auf der Plattform:

Adobe Zielgruppe Experience Ereignisses (Anzeigename) <br>`adobe_target_experience_events` (in der Abfrage zu verwendender Name)

## Partielle XDM-Feldzuordnung auf hoher Ebene

Die Verwendung `[ ]` eines Arrays

| Name | XDM-Feld | Anmerkungen |
| ---- | --------- | ----- |
| mboxName | `_experience.target.mboxname` |  |
| Activity ID | `_experience.target.activities.activityID` |  |
| Erlebnis-ID | `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.experienceID` |  |
| Segment-ID | `_experience.target.activities[].activityEvents[].segmentEvents[].segmentID._id` |  |
| Ereignis | `_experience.target.activities[].activityEvents[].eventScope` | Verfolgt neue Besucher und Besuche |
| Schritt-ID | `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.stepID` | Benutzerdefinierte Schritt-ID für die Kampagne |
| Preis gesamt | `commerce.order.priceTotal` |  |

## Die stündliche Aktivität zählt für einen bestimmten Tag

```sql
SELECT
  Hour,
  ActivityID,
  COUNT(ActivityID) AS Instances
FROM
(
  SELECT
    date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd HH') AS Hour,
    EXPLODE(_experience.target.activities.activityID) AS ActivityID
  FROM adobe_target_experience_events
  WHERE
    _ACP_YEAR = {target_year} AND 
    _ACP_MONTH = {target_month} AND 
    _ACP_DAY = {target_day} AND 
    _experience.target.activities IS NOT NULL
)
GROUP BY Hour, ActivityID
ORDER BY Hour DESC, Instances DESC
LIMIT 24
```

## Stündliche Details für eine bestimmte Aktivität an einem bestimmten Tag

```sql
SELECT
  date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd HH') AS Hour,
  _experience.target.activities.activityID AS ActivityID,
  COUNT(ActivityID) AS Instances
FROM adobe_target_experience_events
WHERE
  array_contains( _experience.target.activities.activityID, {Activity ID} ) AND 
  _ACP_YEAR = {target_year} AND 
  _ACP_MONTH = {target_month} AND 
  _ACP_DAY = {target_day} AND 
  _experience.target.activities IS NOT NULL
GROUP BY Hour, ActivityID
ORDER BY Hour DESC
LIMIT 24
```

## Erlebnis-IDs für eine bestimmte Aktivität für einen bestimmten Tag

```sql
SELECT
  Day,
  Activities.activityID,
  ExperienceID,
  COUNT(ExperienceID) AS Instances
FROM
(
  SELECT
    Day,
    Activities,
    EXPLODE(Activities.activityEvents._experience.target.activity.activityevent.context.experienceID) AS ExperienceID
  FROM
  (
    SELECT
      date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd') AS Day,
      EXPLODE(_experience.target.activities) AS Activities
    FROM adobe_target_experience_events
    WHERE 
      _ACP_YEAR = {target_year} AND 
      _ACP_MONTH = {target_month} AND 
      _ACP_DAY = {target_day} AND 
      _experience.target.activities IS NOT NULL
  )
  WHERE Activities.activityID = {activity_id}
)
GROUP BY Day, Activities.activityID, ExperienceID
ORDER BY Day DESC, Instances DESC
LIMIT 20
```

## Gibt eine Liste von Ereignis-Scopes (Besucher, Besuch, Impression) nach Instanzen pro Aktivitäten-ID für einen bestimmten Tag zurück

```sql
SELECT
  Day,
  Activities.activityID,
  EventScope,
  COUNT(EventScope) AS Instances
FROM
(
  SELECT
    Day,
    Activities,
    EXPLODE(Activities.activityEvents.eventScope) AS EventScope
  FROM
  (
    SELECT
      date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd') AS Day,
      EXPLODE(_experience.target.activities) AS Activities
    FROM adobe_target_experience_events
    WHERE 
      _ACP_YEAR = {target_year} AND 
      _ACP_MONTH = {target_month} AND 
      _ACP_DAY = {target_day} AND 
      _experience.target.activities IS NOT NULL
  )
)
GROUP BY Day, Activities.activityID, EventScope
ORDER BY Day DESC, Instances DESC
LIMIT 30
```

## Rückkehranzahl von Besuchern, Besuchen, Impressionen pro Aktivität an einem bestimmten Tag

```sql
SELECT
  Hour,
  Activities.activityid,
  SUM(CASE WHEN array_contains( Activities.activityEvents.eventScope, 'visitor' ) THEN 1 END) as Visitors,
  SUM(CASE WHEN array_contains( Activities.activityEvents.eventScope, 'visit' ) THEN 1 END) as Visits,
  SUM(CASE WHEN array_contains( Activities.activityEvents.eventScope, 'impression' ) THEN 1 END) as Impressions
FROM
(
  SELECT
    date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd HH') AS Hour,
    EXPLODE(_experience.target.activities) AS Activities
  FROM adobe_target_experience_events
  WHERE
    _ACP_YEAR = {target_year} AND 
    _ACP_MONTH = {target_month} AND 
    _ACP_DAY = {target_day} AND 
    _experience.target.activities IS NOT NULL
)
GROUP BY Hour, Activities.activityid
ORDER BY Hour DESC, Visitors DESC
LIMIT 30
```

## Rückkehrende Besucher, Besuche, Impressionen für Erlebnis-ID, Segment-ID und EventScope für einen bestimmten Tag

```sql
SELECT
  Day,
  Activities.activityID,
  ExperienceID,
  SegmentID._id,
  SUM(CASE WHEN ActivityEvent.eventScope = 'visitor' THEN 1 END) as Visitors,
  SUM(CASE WHEN ActivityEvent.eventScope = 'visit' THEN 1 END) as Visits,
  SUM(CASE WHEN ActivityEvent.eventScope = 'impression' THEN 1 END) as Impressions
FROM
(
  SELECT
    Day,
    Activities,
    ActivityEvent,
    ActivityEvent._experience.target.activity.activityevent.context.experienceID AS ExperienceID,
    EXPLODE(ActivityEvent.segmentEvents.segmentID) AS SegmentID
  FROM
  (
    SELECT
      Day,
      Activities,
      EXPLODE(Activities.activityEvents) AS ActivityEvent
    FROM
    (
      SELECT
        date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd') AS Day,
        EXPLODE(_experience.target.activities) AS Activities
      FROM adobe_target_experience_events
      WHERE 
        _ACP_YEAR = {target_year} AND
        _ACP_MONTH = {target_month} AND 
        _ACP_DAY = {target_day} AND 
        _experience.target.activities IS NOT NULL
      LIMIT 1000000
    )
    LIMIT 1000000
  )
  LIMIT 1000000
)
GROUP BY Day, Activities.activityID, ExperienceID, SegmentID._id
ORDER BY Day DESC, Activities.activityID, ExperienceID ASC, SegmentID._id ASC, Visitors DESC
LIMIT 20
```

## Mbox-Namen und Anzahl der Datensätze für einen bestimmten Tag zurückgeben

```sql
SELECT
  _experience.target.mboxname,
  COUNT(timestamp) AS records
FROM
  adobe_target_experience_events
WHERE
  _ACP_YEAR= {target_year} AND 
  _ACP_MONTH= {target_month} AND 
  _ACP_DAY= {target_day}
  GROUP BY _experience.target.mboxname ORDER BY records DESC
LIMIT 100
```
