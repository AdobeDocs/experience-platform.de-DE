---
title: Aktivitätsanalyse mit Adobe Target
description: In diesem Dokument wird erläutert, wie Sie mit Query Service praktische Einblicke aus Datensätzen erstellen können, die mit Ihren Adobe Target-Daten erstellt wurden.
source-git-commit: 870626f25b1aabdcb5739bbb1ab85bdad44df195
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 12%

---

# Aktivitätsanalyse mit Adobe Target

Mit Adobe Experience Platform können Sie Daten aus Adobe Target mithilfe von XDM-Feldern (Experience-Datenmodell) erfassen, um Datensätze zu erstellen, die mit Query Service verwendet werden können. Da Adobe Target darauf ausgelegt ist, Inhalte anzupassen und Benutzererlebnisse zu personalisieren, ermöglichen Abfragen, die auf diesen Datensätzen ausgeführt werden, durch die Analyse der Benutzeraktivität über SQL hochgradig personalisierte und zielgerichtete Einblicke.

Dieses Dokument bietet eine Vielzahl von SQL-Beispielabfragen, die gängige Anwendungsfälle basierend auf dem Verhalten und den Merkmalen des Kunden demonstrieren.

## Erste Schritte

Für jeden der folgenden Anwendungsfälle wird ein parametrisiertes SQL-Abfragebeispiel als Vorlage bereitgestellt, die Sie anpassen können. Stellen Sie Parameter überall dort bereit, wo Sie sie sehen `{ }` in den SQL-Beispielen, die Sie bewerten möchten.

## Partielle XDM-Feldzuordnung auf hoher Ebene

In der folgenden Tabelle sind allgemeine Target-Felder und die entsprechenden XDM-Felder aufgeführt, denen sie zugeordnet sind.

>[!NOTE]
>
>Die Verwendung von `[ ]` innerhalb des XDM-Felds ein Array darstellt.

| Zielfeldname | XDM-Feldname | Anmerkungen |
|---|---|---|
| `mboxName` | `_experience.target.mboxname` | K. A. |
| Aktivitäts-ID | `_experience.target.activities.activityID` | K. A. |
| Erlebnis-ID | `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.experienceID` | K. A. |
| Segment-ID | `_experience.target.activities[].activityEvents[].segmentEvents[].segmentID._id` | K. A. |
| Ereignisumfang | `_experience.target.activities[].activityEvents[].eventScope` | In diesem Feld werden neue Besucher und Besuche verfolgt. |
| Schritt-ID | `_experience.target.activities[].activityEvents[]._experience.target.activity.activityevent.context.stepID` | Dieses Feld ist eine benutzerdefinierte Schritt-ID für Adobe Campaign. |
| Gesamtpreis | commerce.order.priceTotal | K. A. |

>[!IMPORTANT]
>
>Der Name eines Datensatzes, der automatisch mit Target-Daten erstellt wird, lautet &quot;Adobe Target-Erlebnisereignisse&quot;. Verwenden Sie bei Verwendung dieses Datensatzes mit Abfragen den Namen `adobe_target_experience_events`.

## Ziele

Durch Analyse von Benutzeraktivitäten können Sie Inhalte für eine bestimmte Zielgruppe personalisieren und verschiedene Versionen des Inhalts für eine einzelne Entität testen. Darüber hinaus lässt sich die Leistung jeder einzelnen Aktivität durch die Analyse einer bestimmten Aktivität über einen bestimmten Zeitraum oder für einzelne Benutzer besser nachvollziehen. Die Ergebnisse dieser kombinierten Analyse können genutzt werden, um die Leistung jeder einzelnen Aktivität zu verstehen.

Die folgenden Anwendungsfälle für die Personalisierung werden mithilfe von Adobe Target-Daten erstellt und konzentrieren sich auf Benutzeraktivitäten, um wertvolle Einblicke in das Kundenverhalten im Vergleich zu Geschäftsanwendungen zu erhalten.

In diesem Handbuch werden die folgenden Schlüsselkonzepte anhand der Anwendungsfallbeispiele erläutert:

* Um die Leistung einer Aktivitäts-ID für einen bestimmten Tag zu verstehen, z. B. Anzahl, Details und zugehörige Erlebnis-IDs.
* So bestimmen Sie den Besucher- und Ereignisbereich für eine Aktivität.
* Um die Anzahl der Besucher, Besuche und Impressionsinformationen für Erlebnis-ID, Segment-ID und Aktivitäts-ID zu erfassen.

### Stündliche Aktivitätsanzahl für einen bestimmten Tag generieren

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

### Generieren stündlicher Details für eine bestimmte

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

### Bestimmen der Liste der Erlebnis-IDs für eine bestimmte Aktivität an einem bestimmten Tag

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

### Bestimmen Sie die Anzahl der Besucher, Besuche und Impressionen pro Aktivität für einen bestimmten Tag.

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

### Bestimmen von Besuchern, Besuchen und Impressionen für Erlebnis-ID, Segment-ID und EventScope für einen bestimmten Tag

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
