---
keywords: Experience Platform; Startseite; beliebte Themen; Query Service; Query Service; Beispielabfragen; Beispielabfrage; Adobe Target
solution: Experience Platform
title: Beispielabfragen für Adobe Target-Daten
topic-legacy: queries
description: Daten von Adobe Target werden in XDM-Schema für Erlebnisereignisse umgewandelt und als Datensätze in Experience Platform integriert. Dieses Dokument enthält Beispielabfragen zur Verwendung von Query Service mit Ihren Adobe Target-Datensätzen.
exl-id: 0ab3cd6e-25ed-43dc-b8f0-a2b71621ae50
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 51%

---

# Beispielabfragen für Adobe Target-Daten

Daten aus Adobe Target werden in Erlebnisereignis-XDM-Schema umgewandelt und als Datensätze in Adobe Experience Platform aufgenommen. Es gibt viele Anwendungsfälle für Adobe Experience Platform Query Service mit diesen Daten. Die folgenden Beispielabfragen sollten mit Ihren Adobe Target-Datensätzen funktionieren.

In Experience Platform lautet der Name des automatisch erstellten Datensatzes &quot;Adobe Target-Erlebnisereignisse&quot;. Bei Verwendung dieses Datensatzes mit Abfragen sollten Sie den Namen `adobe_target_experience_events` verwenden.

## Partielle XDM-Feldzuordnung auf hoher Ebene

Die folgende Liste zeigt die Zielfelder, die ihren entsprechenden XDM-Feldern zugeordnet sind.

>[!NOTE]
>
> Die Verwendung von `[ ]` im XDM-Feld bedeutet ein Array.

- mboxName: `_experience.target.mboxname`
- Aktivitäts-ID: `_experience.target.activities.activityID`
- Erlebnis-ID: `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.experienceID`
- Segment-ID: `_experience.target.activities[].activityEvents[].segmentEvents[].segmentID._id`
- Ereignisumfang: `_experience.target.activities[].activityEvents[].eventScope`
   - In diesem Feld werden neue Besucher und Besuche verfolgt.
- Schritt-ID: `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.stepID`
   - Dieses Feld ist eine benutzerdefinierte Schritt-ID für Adobe Campaign.
- Gesamtpreis: `commerce.order.priceTotal`

## Beispielabfragen

Die folgenden Abfragen zeigen Beispiele für häufig verwendete Abfragen mit Adobe Target.

In den folgenden Beispielen müssen Sie die SQL bearbeiten, um die erwarteten Parameter für Ihre Abfragen basierend auf dem Datensatz, den Variablen oder dem Zeitraum, den Sie auswerten möchten, einzugeben. Geben Sie Parameter an, wo immer Sie `{ }` in der SQL sehen.

### Stündliche Aktivitätszahlen für einen bestimmten Tag

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
  WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND 
    _experience.target.activities IS NOT NULL
)
GROUP BY Hour, ActivityID
ORDER BY Hour DESC, Instances DESC
LIMIT 24
```

### Stündliche Details für eine bestimmte Aktivität für einen bestimmten Tag

```sql
SELECT
  date_format(from_utc_timestamp(timestamp, 'America/New_York'), 'yyyy-MM-dd HH') AS Hour,
  _experience.target.activities.activityID AS ActivityID,
  COUNT(ActivityID) AS Instances
FROM adobe_target_experience_events
WHERE
  array_contains( _experience.target.activities.activityID, {Activity ID} ) AND 
    TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND 
  _experience.target.activities IS NOT NULL
GROUP BY Hour, ActivityID
ORDER BY Hour DESC
LIMIT 24
```

### Erlebnis-IDs für eine bestimmte Aktivität für einen bestimmten Tag

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
      TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND 
      _experience.target.activities IS NOT NULL
  )
  WHERE Activities.activityID = {activity_id}
)
GROUP BY Day, Activities.activityID, ExperienceID
ORDER BY Day DESC, Instances DESC
LIMIT 20
```

### Rückgabe einer Liste von Ereignisumfängen (Besucher, Besuch, Impression) nach Instanzen pro Aktivitäten-ID für einen bestimmten Tag

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
      TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND 
      _experience.target.activities IS NOT NULL
  )
)
GROUP BY Day, Activities.activityID, EventScope
ORDER BY Day DESC, Instances DESC
LIMIT 30
```

### Anzahl wiederkehrender Besucher, Besuche, Impressionen pro Aktivität für einen bestimmten Tag

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
    TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND 
    _experience.target.activities IS NOT NULL
)
GROUP BY Hour, Activities.activityid
ORDER BY Hour DESC, Visitors DESC
LIMIT 30
```

### Wiederkehrende Besucher, Besuche, Impressionen für Erlebnis-ID, Segment-ID und Ereignisumfang für einen bestimmten Tag

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
        TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}') AND 
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

### Rückgabe der mbox-Namen und Anzahl der Einträge für einen bestimmten Tag

```sql
SELECT
  _experience.target.mboxname,
  COUNT(timestamp) AS records
FROM
  adobe_target_experience_events
WHERE
  TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
  GROUP BY _experience.target.mboxname ORDER BY records DESC
LIMIT 100
```
