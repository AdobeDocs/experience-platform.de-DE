---
title: Destinations Insights
description: Entdecken Sie die SQL-Datenbank, die Ihre Zieleinblicke nutzt, um benutzerdefinierte Einblicke zu generieren und die Aktivierung von Daten aus Adobe Experience Platform weiter zu untersuchen.
source-git-commit: 3d5dd6300952409e2dddb32eb11547fb43a5feac
workflow-type: tm+mt
source-wordcount: '1097'
ht-degree: 2%

---

# Zieleinblicke

Die aus der Analyse Ihres Datenmodells gewonnenen Erkenntnisse machen Ihre Adobe Real-time Customer Data Platform-Daten leichter zugänglich, verständlich und für die Entscheidungsfindung wirkungsvoll.

Machen Sie sich mit Ihren Zieleinblicken vertraut, indem Sie auf die SQL-Datenbank zugreifen, über die diese Benutzer verfügen, und generieren Sie dann Ihre eigenen Einblicke, um die Aktivierung von Daten von Adobe Experience Platform zu Ihren Zielplattformen weiter zu untersuchen. Transformieren Sie Ihre Rohdaten in neue umsetzbare Einblicke, indem Sie die vorhandene SQL des Real-Time CDP-Datenmodells als Anregung verwenden, um Abfragen für Ihre individuellen Geschäftsanforderungen zu erstellen.

<!-- This link will go in during the January release.
See the [View SQL documentation]() for more information on how to adapt your insights' SQL directly through the PLatform UI.  -->

Die folgenden Einblicke stehen Ihnen als Teil der [Dashboard &quot;Ziele&quot;](../guides/destinations.md) oder benutzerdefiniert [Benutzerdefiniertes Dashboard](../user-defined-dashboards.md). Siehe [Anpassungsübersicht](../customize/overview.md) Anweisungen zum Anpassen Ihres Dashboards erhalten Sie oder [Erstellen und Bearbeiten neuer Widgets](../customize/custom-widgets.md) in der Widget-Bibliothek und [Benutzerdefiniertes Dashboard](../user-defined-dashboards.md#create-widget).

## Aktivierte Zielgruppen {#activated-audiences}

Fragen, die durch diesen Einblick beantwortet werden:

- Wie hoch ist die Gesamtzahl der aktivierten Zielgruppen, die nach einem bestimmten Ziel gefiltert wurden?
- Wie hoch ist die aktivierte Zielgruppenanzahl für jedes Ziel?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

```sql
SELECT
  COUNT(segment_id) AS Activated_Audiences_Count
FROM
  qsaccel.profile_agg.adwh_dim_br_segment_destinations
WHERE
  (
    SELECT
      MAX(process_date)
    FROM
      qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE
      process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
  ) BETWEEN start_date AND end_date
  AND destination_id = 1458738325;
```

+++

Siehe [Dokumentation zum Widget &quot;Aktivierte Zielgruppen&quot;](../guides/destinations.md#activated-audiences) für Informationen über das Erscheinungsbild und die Funktionalität dieses Einblicks.

## Aktivierte Zielgruppen für alle Ziele {#activated-audiences-across-all-destinations}

Fragen, die durch diesen Einblick beantwortet werden:

- Wie viele Zielgruppen werden für alle Ziele aktiviert?
- Wie hoch ist die Gesamtzahl der aktivierten Zielgruppen?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

```sql
SELECT count(segment_id) AS Activated_Audiences_Count
FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations
WHERE
    (SELECT MAX(process_date)
     FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
     WHERE process_name = 'FACT_TABLES_PROCESSING'
       AND process_status = 'SUCCESSFUL' ) BETWEEN start_date AND end_date;
```

+++

Siehe [Dokumentation zu aktivierten Zielgruppen für alle Ziele](../guides/destinations.md#activated-audiences-across-all-destinations) für Informationen über das Erscheinungsbild und die Funktionalität dieses Einblicks.

## Aktive Ziele nach Zielplattform {#active-destinations-by-destination-platform}

Fragen, die durch diesen Einblick beantwortet werden:

- Wie viele Ziele sind aktiv?
- Wie werden aktive Ziele nach Zielplattform aufgeschlüsselt?
- Wie viele aktive Ziele gibt es für jede Zielplattform?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

```sql
SELECT destination_platform_name AS Destination_Platform_Name,
       COUNT(destination_id) AS Active_Destinations_Count
  FROM qsaccel.profile_agg.adwh_dim_destination a
  INNER JOIN qsaccel.profile_agg.adwh_dim_destination_platform b ON a.destination_platform_id = b.destination_platform_id
  WHERE destination_status='enabled'
  GROUP BY destination_platform_name
  ORDER BY Active_Destinations_Count DESC
  LIMIT 20;
```

+++

Siehe [Dokumentation zu aktiven Zielen nach Zielplattform-Widgets](../guides/destinations.md#active-destinations-by-destination-platform) für Informationen über das Erscheinungsbild und die Funktionalität dieses Einblicks.

## Trend der Zielgruppen-Größe {#audience-size-trend}

Fragen, die durch diesen Einblick beantwortet werden:

- Wie hat sich die Zielgruppengröße im Laufe der Zeit verändert, einschließlich Anomalien für eine einem Ziel zugeordnete Zielgruppe?
- Wie finde ich den Gesamttrend der Zielgruppengröße nach Zielgruppe über die angegebenen Zeiträume von 30 Tagen, 90 Tagen und 12 Monaten?
- Welche Hauptmerkmale hat die Zielgruppe, die zur Größe beiträgt, z. B. Spitzen bei E-Mail-Marketing-Kampagnen?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

```sql
SELECT d.destination_name,
        d.destination,
        d.destination_id,
        b.segment_name,
        b.segment,
        c.segment_id,
        a.date_key,
        sum(a.count_of_profiles) AS profile_count
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines a
  INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON a.segment_id = b.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_br_segment_destinations c ON a.segment_id = c.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_destination d ON c.destination_id = d.destination_id
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
    FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
    GROUP BY merge_policy_id) f ON a.merge_policy_id = f.merge_policy_id
  WHERE a.date_key >= dateadd(DAY, -30-1, f.last_process_date)
    AND d.destination_id = -1275507046
    AND c.segment_id = -1452100519
  GROUP BY d.destination_name,
          d.destination,
          d.destination_id,
          b.segment_name,
          b.segment,
          c.segment_id,
          a.date_key;
```

+++

Siehe [Dokumentation zum Widget zum Trend der Zielgruppengröße](../guides/destinations.md#audience-size-trend) für Informationen über das Erscheinungsbild und die Funktionalität dieses Einblicks.

## Häufige Zielgruppen {#common-audiences}

Fragen, die durch diesen Einblick beantwortet werden:

- Welche Zielgruppen gibt es zwischen zwei verschiedenen Zielen?
- Wie viele Profile haben die einzelnen gemeinsamen Zielgruppen zwischen zwei verschiedenen Zielen?
- Welche Zielgruppe ist die größte, der zwei Ziele zugeordnet sind?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

```sql
SELECT k.destination_name1,
       k.destination_1,
       k.destination_id1,
       k.destination_name2,
       k.destination_2,
       k.destination_id2,
       b.segment_name,
       b.segment,
       b.segment_id,
       sum(a.count_of_profiles) AS profile_count
  FROM
    (SELECT i.destination_name AS destination_name1,
            i.destination AS destination_1,
            i.destination_id AS destination_id1,
            j.destination_name AS destination_name2,
            j.destination AS destination_2,
            j.destination_id AS destination_id2,
            i.segment_id
     FROM
       (SELECT b.destination_name,
               b.destination,
               b.destination_id,
               a.segment_id
        FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations a
        INNER JOIN qsaccel.profile_agg.adwh_dim_destination b ON a.destination_id=b.destination_id
        WHERE b.destination_id=1458738325) AS i
     INNER JOIN
       (SELECT b.destination_name,
               b.destination,
               b.destination_id,
               a.segment_id
        FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations a
        INNER JOIN qsaccel.profile_agg.adwh_dim_destination b ON a.destination_id=b.destination_id
        WHERE b.destination_id=-635802802) AS j ON i.segment_id=j.segment_id) AS k
  INNER JOIN qsaccel.profile_agg.adwh_fact_profile_by_segment a ON a.segment_id = k.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON b.segment_id = k.segment_id
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
     FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
     WHERE process_name = 'FACT_TABLES_PROCESSING'
       AND process_status = 'SUCCESSFUL'
     GROUP BY merge_policy_id) c ON a.merge_policy_id = c.merge_policy_id
  WHERE a.date_key = c.last_process_date
  GROUP BY k.destination_name1,
           k.destination_1,
           k.destination_id1,
           k.destination_name2,
           k.destination_2,
           k.destination_id2,
           b.segment_name,
           b.segment,
           b.segment_id
  ORDER BY profile_count DESC
  LIMIT 20;
```

+++

Siehe [Dokumentation zum Widget &quot;Allgemeine Zielgruppen&quot;](../guides/destinations.md#common-audiences) für Informationen über das Erscheinungsbild und die Funktionalität dieses Einblicks.

## Zielstatus {#destination-status}

Fragen, die durch diesen Einblick beantwortet werden:

- Wie viele Ziele sind insgesamt für die Verwendung aktiviert?
- Wie viele Ziele sind insgesamt deaktiviert?
- Wie hoch ist die prozentuale Aufteilung zwischen aktivierten und deaktivierten Zielen?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

```sql
SELECT COUNT(CASE
                 WHEN destination_status='enabled' THEN 1
             END) AS count_of_active_destinations,
       COUNT(CASE
                 WHEN destination_status='disabled' THEN 1
             END) AS count_of_inactive_destinations
FROM qsaccel.profile_agg.adwh_dim_destination;
```

+++

Siehe [Dokumentation zum Zielstatus-Widget](../guides/destinations.md#destination-status) für Informationen über das Erscheinungsbild und die Funktionalität dieses Einblicks.

## Anzahl der Ziele {#destinations-count}

Fragen, die durch diesen Einblick beantwortet werden:

- Wie viele Ziele sind derzeit konfiguriert?
- Wie hat sich die Gesamtzahl der Ziele im Laufe der Zeit verändert?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

```sql
SELECT count(destination_id) AS total_number_of_destinations
  FROM qsaccel.profile_agg.adwh_dim_destination;
```

+++

Siehe [Dokumentation zum Widget &quot;Ziele zählen&quot;](../guides/destinations.md#destinations-count) für Informationen über das Erscheinungsbild und die Funktionalität dieses Einblicks.

## Zustand der zugeordneten Zielgruppe {#mapped-audience-health}

Fragen, die durch diesen Einblick beantwortet werden:

- Welche Zielgruppen sind in den letzten 30 Tagen einem Ziel zugeordnet?
- Wie groß ist die aktuelle Zielgruppe und hat sich im letzten Monat verändert?
- Wie werden alle Zielgruppen aufgelistet, die einem Ziel zugeordnet sind, basierend auf der Schwere der im letzten Monat vorgenommenen Größenänderungen?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

```sql
SELECT destination_name,
        SEGMENT,
        segment_id,
        segment_name,
        avg_profile_count,
        latest_profile_count,
        stddev_profile_count,
        profile_count_z_factor
  FROM
    (SELECT b.destination_name,
            f.segment_id,
            c.segment_name,
            c.segment,
            f.avg_profile_count,
            f.latest_profile_count,
            f.stddev_profile_count,
            CASE
                WHEN stddev_profile_count = 0 THEN 0 ELSE(f.latest_profile_count - f.avg_profile_count)/f.stddev_profile_count
            END AS profile_count_z_factor
    FROM
      (SELECT segment_id,
              avg(profile_count) AS avg_profile_count,
              sum(CASE
                      WHEN last_process_date = date_key THEN profile_count
                      ELSE 0
                  END) AS latest_profile_count,
              stdevp(profile_count) AS stddev_profile_count
        FROM
          (SELECT x.date_key,
                  x.segment_id,
                  d.last_process_date,
                  sum(x.count_of_profiles) AS profile_count
          FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines x
          INNER JOIN
            (SELECT MAX(process_date) last_process_date,
                    merge_policy_id
              FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
              WHERE process_name = 'FACT_TABLES_PROCESSING'
                AND process_status = 'SUCCESSFUL'
              GROUP BY merge_policy_id) d ON x.merge_policy_id = d.merge_policy_id
          WHERE x.date_key >= dateadd (DAY, -30, d.last_process_date)
          GROUP BY x.date_key,
                    x.segment_id,
                    d.last_process_date) AS t
        GROUP BY segment_id) AS f
    INNER JOIN qsaccel.profile_agg.adwh_dim_segments c ON f.segment_id = c.segment_id
    INNER JOIN qsaccel.profile_agg.adwh_dim_br_segment_destinations a ON a.segment_id = c.segment_id
    INNER JOIN qsaccel.profile_agg.adwh_dim_destination b ON a.destination_id = b.destination_id
    WHERE b.destination_id = 1458738325) AS m
  WHERE abs(m.profile_count_z_factor) >= 1
  ORDER BY m.latest_profile_count DESC
  LIMIT 20;
```

+++

Siehe [Dokumentation zum zugeordneten Zielgruppen-Health-Widget](../guides/destinations.md#mapped-audience-health) für Informationen über das Erscheinungsbild und die Funktionalität dieses Einblicks.

## Zugeordnete Zielgruppen {#mapped-audiences}

Fragen, die durch diesen Einblick beantwortet werden:

- Wie viele Zielgruppen sind einem bestimmten Ziel zugeordnet?
- Wie hat sich die Anzahl der zugeordneten Zielgruppen im Laufe der Zeit verändert?
- Wo kann ich zwei Ziele vergleichen, um die Zielgruppenüberschneidung zu sehen, die den einzelnen Zielen zugeordnet ist?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

```sql
SELECT COUNT(segment_id) AS mapped_audiences_count
FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations
WHERE destination_id = 1458738325;
```

+++

Siehe [Dokumentation zum Widget &quot;Zugeordnete Zielgruppen&quot;](../guides/destinations.md#mapped-audiences) für Informationen über das Erscheinungsbild und die Funktionalität dieses Einblicks.

<!-- Commented out until the Jan release as the SQL IS MISSING:
## Mapped audiences by identity {#mapped-audiences-by-identity}

Questions answered by this insight:

- How do I find a list of audiences that are mapped to a destination?
- What is the count of identities for audiences mapped to a destination?
- Which audiences have the highest count of identities mapped to a particular destination?

+++Select to reveal the SQL that generates this insight

```sql
```

+++

See the [Mapped audiences by identity widget documentation](../guides/destinations.md#mapped-audiences-by-identity) for information on the appearance and functionality of this insight.
-->

## Am häufigsten verwendete Ziele {#most-used-destinations}

Fragen, die durch diesen Einblick beantwortet werden:

- Welche Ziele werden am häufigsten verwendet?
- Wie viele Zielgruppen werden den einzelnen Zielen zugeordnet, die am wenigsten nach ihnen sortiert sind?
- Wie ändert sich die Zuordnung von Zielgruppen zu Zielen von einem Schnappschuss zum anderen?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

```sql
SELECT qsaccel.profile_agg.adwh_dim_destination.destination_name,
       qsaccel.profile_agg.adwh_dim_destination.destination_id,
       qsaccel.profile_agg.adwh_dim_destination.destination,
       count(DISTINCT qsaccel.profile_agg.adwh_dim_br_segment_destinations.segment_id) segment_count
  FROM qsaccel.profile_agg.adwh_dim_destination
  JOIN qsaccel.profile_agg.adwh_dim_br_segment_destinations ON qsaccel.profile_agg.adwh_dim_destination.destination_id = qsaccel.profile_agg.adwh_dim_br_segment_destinations.destination_id
  WHERE qsaccel.profile_agg.adwh_dim_destination.destination_name IS NOT NULL
  GROUP BY qsaccel.profile_agg.adwh_dim_destination.destination_name,
           qsaccel.profile_agg.adwh_dim_destination.destination,
           qsaccel.profile_agg.adwh_dim_destination.destination_id
  ORDER BY segment_count DESC
  LIMIT 20;
```

+++

Siehe [Dokumentation zum am häufigsten verwendeten Ziel-Widget](../guides/destinations.md#most-used-destinations) für Informationen über das Erscheinungsbild und die Funktionalität dieses Einblicks.

## Zuletzt aktivierte Zielgruppen {#recently-activated-audiences}

Fragen, die durch diesen Einblick beantwortet werden:

- Für welches Ziel wurde zuletzt eine Zielgruppe aktiviert?
- Wie finde ich eine Liste aller Ziele sortiert nach dem letzten aktualisierten Datum?
- Wie kann ich zwei Ziele anhand der letzten Aktivierungen vergleichen?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

```sql
SELECT
  segment_name,
  segment,
  destination_name,
  a.create_time create_time
FROM
  qsaccel.profile_agg.adwh_dim_br_segment_destinations a
  INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON a.segment_id = b.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_destination c ON a.destination_id = c.destination_id
ORDER BY
  create_time DESC,
  segment
LIMIT
  20;
```

+++

Siehe [Dokumentation zum kürzlich aktivierten Zielgruppen-Widget](../guides/destinations.md#recently-activated-audiences) für Informationen über das Erscheinungsbild und die Funktionalität dieses Einblicks.

## Zuletzt aktivierte Zielgruppen nach Ziel {#recently-activated-audiences-by-destination}

Fragen, die durch diesen Einblick beantwortet werden:

- Welche Zielgruppen sind für ein bestimmtes Ziel aktiviert?
- Wie finde ich eine Liste von Zielgruppen, die von einer bestimmten Zielgruppe aktiviert wurden, von der letzten bis zur letzten?
- Wie finde ich eine Liste von Zielgruppen nach dem Datum, an dem sie für ein bestimmtes Ziel aktiviert wurde?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

```sql
SELECT c.destination_name,
       c.destination,
       c.destination_id,
       b.segment_name,
       b.segment,
       b.segment_id,
       a.create_time activated
  FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations a
  INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON a.segment_id=b.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_destination c ON a.destination_id=c.destination_id
  WHERE c.destination_id=-1275507046
  ORDER BY a.create_time DESC,
           a.segment_id
  LIMIT 20;
```

+++

Siehe [Kürzlich aktivierte Zielgruppen nach Ziel-Widget-Dokumentation](../guides/destinations.md#recently-activated-audiences-by-destination) für Informationen über das Erscheinungsbild und die Funktionalität dieses Einblicks.

## Kürzlich erstellte Ziele {#recently-created-destinations}

Fragen, die durch diesen Einblick beantwortet werden:

- Welche Ziele wurden zuletzt erstellt?
- Wie finde ich eine Liste von Zielen mit dem Datum, an dem sie erstellt wurden?
- Welches neue Ziel wurde kürzlich erstellt?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

```sql
SELECT DISTINCT
  destination,
  destination_name,
  create_time
FROM
  qsaccel.profile_agg.adwh_dim_destination
WHERE
  destination_status = 'enabled'
ORDER BY
  create_time DESC
LIMIT
  20;
```

+++

Siehe [Dokumentation zum kürzlich erstellten Ziel-Widget](../guides/destinations.md#recently-created-destinations) für Informationen über das Erscheinungsbild und die Funktionalität dieses Einblicks.

<!-- Commented out until the Jan release as SQL MISSING FROM WIKI:

## Unmapped audiences by identity {#unmapped-audiences-by-identity}

Questions answered by this insight:

- How do I find a list of audiences that are not mapped to a destination?
- What is the count of identities for audiences that are not mapped to a destination?
- Which audiences have the highest count of identities not mapped to a particular destination?

+++Select to reveal the SQL that generates this insight

```sql
```

+++

See the [Unmapped audiences by identity widget documentation](../guides/destinations.md#unmapped-audiences-by-identity) for information on the appearance and functionality of this insight.

-->

## Nächste Schritte {#next-steps}

Durch Lesen dieses Dokuments verstehen Sie jetzt die SQL-Datenbank, die Dashboard-Einblicke generiert, und welche häufig gestellten Fragen diese Analyse löst. Sie können diese SQL-Abfragen jetzt bearbeiten und iterieren, um eigene Einblicke zu erhalten.

<!-- This link will go in during the January release.
See the [View SQL documentation]() for more information on how to adapt your insights' SQL directly through the PLatform UI. -->

Sie können auch die SQL lesen und verstehen, die Einblicke für die [Profile](./profiles.md) und [Zielgruppen](./audiences.md) Dashboards.

<!-- 
SQL MISSING FROM WIKI:
Unmapped audiences by identity
Mapped audiences by identity 
-->
