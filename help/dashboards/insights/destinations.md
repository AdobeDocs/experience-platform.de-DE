---
title: Ziele - Einblicke
description: Entdecken Sie den SQL-Code, der Ihre Zieleinblicke ermöglicht, und verwenden Sie diese Abfragen, um benutzerdefinierte Einblicke zu generieren, um die Aktivierung von Daten aus Adobe Experience Platform weiter zu untersuchen.
exl-id: 762a9960-e7a5-4796-80c7-ef745157cc04
source-git-commit: e4ee4accdb28dafda7e37625eb84062bb6e53644
workflow-type: tm+mt
source-wordcount: '1137'
ht-degree: 3%

---

# Ziele - Einblicke

Die aus der Analyse Ihres Datenmodells gewonnenen Erkenntnisse machen Ihre Adobe Real-Time CDP-Daten zugänglicher, verständlicher und wirkungsvoller für die Entscheidungsfindung.

Verstehen Sie Ihre Zieleinblicke, indem Sie auf die SQL zugreifen, die sie unterstützt, und dann Ihre eigenen Einblicke generieren, um die Aktivierung von Daten aus Adobe Experience Platform auf Ihren Zielplattformen weiter zu untersuchen. Wandeln Sie Ihre Rohdaten in neue umsetzbare Einblicke um, indem Sie das vorhandene Real-Time CDP-Datenmodell als SQL-Inspiration verwenden, um Abfragen für Ihre individuellen Geschäftsanforderungen zu erstellen.

In der [SQL-Dokumentation anzeigen](../view-sql.md) finden Sie weitere Informationen darüber, wie Sie die SQL Ihrer Insights direkt über die Platform-Benutzeroberfläche anpassen können.

Die folgenden Einblicke stehen Ihnen als Teil des [Ziele-Dashboards](../guides/destinations.md) oder eines benutzerdefinierten [benutzerdefinierten Dashboards](../standard-dashboards.md) zur Verfügung. Anleitungen zum Anpassen Ihres Dashboards oder zum [Erstellen und Bearbeiten neuer Widgets](../customize/overview.md) in der Widget-Bibliothek und im benutzerdefinierten Dashboard finden [&#x200B; &#x200B;](../customize/custom-widgets.md) in der [Anpassungsübersicht](../standard-dashboards.md#create-widget).

## Aktivierte Zielgruppen {#activated-audiences}

Fragen, die von diesem insight beantwortet werden:

- Wie viele aktivierte Zielgruppen wurden insgesamt nach einem bestimmten Ziel gefiltert?
- Was ist die aktivierte Zielgruppengröße für jedes Ziel?

+++Auswählen, um die SQL anzuzeigen, die diese insight generiert

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

Weitere Informationen über [&#x200B; Erscheinungsbild und die Funktionen &#x200B;](../guides/destinations.md#activated-audiences) insight finden Sie in der Dokumentation zum Widget „Aktivierte Zielgruppen“ .

## Aktivierte Zielgruppen für alle Ziele {#activated-audiences-across-all-destinations}

Fragen, die von diesem insight beantwortet werden:

- Wie viele Zielgruppen werden für alle Ziele aktiviert?
- Wie viele aktivierte Zielgruppen gibt es insgesamt?

+++Auswählen, um die SQL anzuzeigen, die diese insight generiert

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

Weitere Informationen [&#x200B; Erscheinungsbild und Funktionalität dieser insight finden Sie in der &#x200B;](../guides/destinations.md#activated-audiences-across-all-destinations) zum Widget „Aktivierte Zielgruppen für alle Ziele“ .

## Aktive Ziele nach Zielplattform {#active-destinations-by-destination-platform}

Fragen, die von diesem insight beantwortet werden:

- Wie viele Ziele sind aktiv?
- Wie ist die Aufschlüsselung der aktiven Ziele nach Zielplattform?
- Wie viele aktive Ziele sind nach Zielplattform aufgeschlüsselt?

+++Auswählen, um die SQL anzuzeigen, die diese insight generiert

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

Weitere Informationen [&#x200B; Erscheinungsbild und Funktionalität dieser insight finden Sie &#x200B;](../guides/destinations.md#active-destinations-by-destination-platform) der Widget-Dokumentation „Aktive Ziele Zielplattform“ .

## Trend der Zielgruppen-Größe {#audience-size-trend}

Fragen, die von diesem insight beantwortet werden:

- Wie hat sich die Zielgruppengröße im Laufe der Zeit geändert, einschließlich Anomalien für eine Zielgruppe, die einem Ziel zugeordnet ist?
- Wie finde ich den allgemeinen Trend der Zielgruppengröße nach Ziel über die angegebenen Zeiträume von 30 Tagen, 90 Tagen und 12 Monaten?
- Welche Hauptmerkmale trägt die Zielgruppe zur Größe bei, z. B. Spitzen bei E-Mail-Marketing-Kampagnen?

+++Auswählen, um die SQL anzuzeigen, die diese insight generiert

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

Weitere Informationen [&#x200B; Erscheinungsbild und Funktionalität dieser insight finden Sie in &#x200B;](../guides/destinations.md#audience-size-trend) Dokumentation zu Widgets für die Entwicklung der Zielgruppengröße .

## Häufige Zielgruppen {#common-audiences}

Fragen, die von diesem insight beantwortet werden:

- Welche Zielgruppen gibt es für zwei verschiedene Ziele?
- Wie viele Profile hat jede der gemeinsamen Zielgruppen zwischen zwei verschiedenen Zielen?
- Welcher Zielgruppe sind die größten Ziele zugeordnet?

+++Auswählen, um die SQL anzuzeigen, die diese insight generiert

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

Weitere Informationen über [&#x200B; Erscheinungsbild und die Funktionen &#x200B;](../guides/destinations.md#common-audiences) insight finden Sie in der Dokumentation zum Widget „Allgemeine Zielgruppen“ .

## Zielstatus {#destination-status}

Fragen, die von diesem insight beantwortet werden:

- Wie viele Ziele sind insgesamt für die Verwendung aktiviert?
- Wie viele Ziele sind insgesamt deaktiviert?
- Wie sieht die prozentuale Aufteilung zwischen aktivierten und deaktivierten Zielen aus?

+++Auswählen, um die SQL anzuzeigen, die diese insight generiert

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

Weitere Informationen [&#x200B; Erscheinungsbild und Funktionalität dieser insight finden &#x200B;](../guides/destinations.md#destination-status) in der Dokumentation zum Zielstatus-Widget .

## Anzahl der Ziele {#destinations-count}

Fragen, die von diesem insight beantwortet werden:

- Wie viele Ziele sind derzeit konfiguriert?
- Wie hat sich die Gesamtzahl der Ziele im Laufe der Zeit verändert?

+++Auswählen, um die SQL anzuzeigen, die diese insight generiert

```sql
SELECT count(destination_id) AS total_number_of_destinations
  FROM qsaccel.profile_agg.adwh_dim_destination;
```

+++

Weitere Informationen [&#x200B; Erscheinungsbild und Funktionalität dieser insight finden &#x200B;](../guides/destinations.md#destinations-count) in der Dokumentation zum Widget Anzahl der Ziele“.

## Zustand der zugeordneten Zielgruppe {#mapped-audience-health}

Fragen, die von diesem insight beantwortet werden:

- Welche Zielgruppen, die einem Ziel zugeordnet sind, haben in den letzten 30 Tagen signifikante Variationen?
- Wie groß ist eine zugeordnete Zielgruppe zuletzt und ob sich diese im Laufe des letzten Monats geändert hat?
- Wie kann ich alle einem Ziel zugeordneten Zielgruppen basierend auf dem Schweregrad der Größenänderungen im letzten Monat auflisten?

+++Auswählen, um die SQL anzuzeigen, die diese insight generiert

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

Weitere Informationen über [&#x200B; Erscheinungsbild und die Funktionen dieser insight finden &#x200B;](../guides/destinations.md#mapped-audience-health) in der Dokumentation zum Widget „Zustand der zugeordneten Zielgruppe .

## Zugeordnete Zielgruppen {#mapped-audiences}

Fragen, die von diesem insight beantwortet werden:

- Wie viele Zielgruppen werden einem bestimmten Ziel zugeordnet?
- Wie hat sich die Anzahl der zugeordneten Zielgruppen im Laufe der Zeit verändert?
- Wo kann ich zwei Ziele vergleichen, um die Zielgruppenüberschneidung zu sehen, die jedem Ziel zugeordnet ist?

+++Auswählen, um die SQL anzuzeigen, die diese insight generiert

```sql
SELECT COUNT(segment_id) AS mapped_audiences_count
FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations
WHERE destination_id = 1458738325;
```

+++

Weitere Informationen über [&#x200B; Erscheinungsbild und die Funktionen &#x200B;](../guides/destinations.md#mapped-audiences) insight finden Sie in der Dokumentation zum Widget „Zugeordnete Zielgruppen“ .

<!-- 
Commented out until the Jan release as the SQL IS MISSING:
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

Fragen, die von diesem insight beantwortet werden:

- Was sind die am häufigsten verwendeten Ziele?
- Wie viele Zielgruppen werden jedem Ziel zugeordnet, sortiert nach den meisten bis zu den wenigsten?
- Wie ändert sich die Zuordnung von Zielgruppen zu Zielen von einer Momentaufnahme zur anderen?

+++Auswählen, um die SQL anzuzeigen, die diese insight generiert

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

Weitere Informationen [&#x200B; Erscheinungsbild und Funktionalität dieser insight finden Sie in &#x200B;](../guides/destinations.md#most-used-destinations) Dokumentation zum Widget „Am häufigsten verwendete Ziele“ .

## Zuletzt aktivierte Zielgruppen {#recently-activated-audiences}

Fragen, die von diesem insight beantwortet werden:

- Für welches Ziel wurde eine Zielgruppe zuletzt aktiviert?
- Wie finde ich eine Liste aller Ziele, sortiert nach dem Datum der letzten Aktualisierung?
- Wie kann ich zwei Ziele basierend auf den letzten Aktivierungen vergleichen?

+++Auswählen, um die SQL anzuzeigen, die diese insight generiert

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

Weitere Informationen über [&#x200B; Erscheinungsbild und die Funktionen dieser insight finden &#x200B;](../guides/destinations.md#recently-activated-audiences) in der Dokumentation zum Widget „Kürzlich aktivierte Zielgruppen“ .

## Zuletzt aktivierte Zielgruppen nach Ziel {#recently-activated-audiences-by-destination}

Fragen, die von diesem insight beantwortet werden:

- Welche Zielgruppen sind für ein bestimmtes Ziel aktiviert?
- Wie finde ich eine Liste von Zielgruppen, die von einer bestimmten Zielgruppe aktiviert wurden, von der letzten bis zur letzten?
- Wie finde ich eine Liste von Zielgruppen bis zu dem Datum, an dem sie für ein bestimmtes Ziel aktiviert wurde?

+++Auswählen, um die SQL anzuzeigen, die diese insight generiert

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

In der [Widget-Dokumentation Kürzlich aktivierte Zielgruppen nach Ziel](../guides/destinations.md#recently-activated-audiences-by-destination) finden Sie Informationen über das Erscheinungsbild und die Funktionen dieser insight.

## Kürzlich erstellte Ziele {#recently-created-destinations}

Fragen, die von diesem insight beantwortet werden:

- Welche sind die zuletzt erstellten Ziele?
- Wie finde ich eine Liste von Zielen mit dem Datum, an dem sie erstellt wurden?
- Welches neue Ziel wurde kürzlich erstellt?

+++Auswählen, um die SQL anzuzeigen, die diese insight generiert

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

Weitere Informationen [&#x200B; Erscheinungsbild und Funktionalität dieser insight finden Sie &#x200B;](../guides/destinations.md#recently-created-destinations) der Dokumentation zum Widget „Kürzlich erstellte Ziele .

<!-- 
Commented out until the Jan release as SQL MISSING FROM WIKI:

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

Durch das Lesen dieses Dokuments wissen Sie jetzt, welche SQL-Daten Dashboard-Einblicke generieren und welche häufigen Fragen diese Analyse löst. Sie können diese SQL-Abfragen jetzt bearbeiten und iterieren, um eigene Einblicke zu generieren.

In der [SQL-Dokumentation anzeigen](../view-sql.md) finden Sie weitere Informationen darüber, wie Sie die SQL Ihrer Insights direkt über die Platform-Benutzeroberfläche anpassen können.

Sie können auch den SQL-Code lesen und verstehen, der Einblicke für die Dashboards [Profile](./profiles.md), [Kontoprofile](./account-profiles.md) und [Zielgruppen](./audiences.md) generiert.
