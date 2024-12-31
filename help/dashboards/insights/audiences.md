---
title: Zielgruppen-Insights
description: Entdecken Sie den SQL-Code, der Ihren Zielgruppenerkenntnissen zugrunde liegt, und verwenden Sie diese Abfragen, um benutzerdefinierte Einblicke zu generieren, damit Sie Zielgruppendaten aus Adobe Experience Platform weiter untersuchen können.
exl-id: 99624234-c4e1-44bb-9567-505bc0c4723e
source-git-commit: cce576c00823a0c02e4b639f0888a466a5af6a0c
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 3%

---

# Zielgruppen-Insights

Die aus der Analyse Ihres Datenmodells gewonnenen Erkenntnisse machen Ihre Adobe Real-Time CDP-Daten zugänglicher, verständlicher und wirkungsvoller für die Entscheidungsfindung.

Verstehen Sie Ihre Zielgruppeneinblicke, indem Sie auf die SQL zugreifen, die sie unterstützt, und dann Ihre eigenen Einblicke generieren, um die Identitäten und Profile, aus denen Ihre Zielgruppen bestehen, weiter zu untersuchen. Wandeln Sie Ihre Rohdaten in neue umsetzbare Einblicke um, indem Sie das vorhandene Real-Time CDP-Datenmodell als SQL-Inspiration verwenden, um Abfragen für Ihre individuellen Geschäftsanforderungen zu erstellen.

In der [SQL-Dokumentation anzeigen](../view-sql.md) finden Sie weitere Informationen darüber, wie Sie die SQL Ihrer Insights direkt über die Platform-Benutzeroberfläche anpassen können.

Die folgenden Einblicke stehen Ihnen alle als Teil des [Zielgruppen-Dashboards](../guides/audiences.md) oder eines benutzerdefinierten [benutzerdefinierten Dashboards](../standard-dashboards.md) zur Verfügung. Anleitungen zum Anpassen Ihres Dashboards oder zum [Erstellen und Bearbeiten neuer Widgets](../customize/custom-widgets.md) in der Widget-Bibliothek und im benutzerdefinierten Dashboard finden [ ](../customize/overview.md) in der [Anpassungsübersicht](../standard-dashboards.md#create-widget).

Die folgenden Einblicke stehen Ihnen alle als Teil des (Zielgruppen[Dashboards ](../guides/audiences.md) benutzerdefinierten Dashboards zur Verfügung.

## Bericht zur Zielgruppenüberschneidung {#audience-overlap-report}

Diese Einsicht beantwortet Fragen:

- Welche sind die 50 sich überschneidenden Zielgruppen einer bestimmten gefilterten Zielgruppe?
- Welche sind die 50 Zielgruppen mit der geringsten Überschneidung einer bestimmten gefilterten Zielgruppe?
- Wie ändert sich das Überschneidungsmuster für eine andere gefilterte Zielgruppe?

+++Auswählen, um die SQL anzuzeigen, die diese Einsicht generiert

```sql
SELECT source_segment_name,
        source_segment_id,
        overlap_segment_name,
        overlap_segment_id,
        max(source_segment_audience_count) source_segment_audience_count,
        max(overlap_segment_audience_count) overlap_segment_audience_count,
        max(overlap_audience_count) overlap_audience_count,
        CASE
            WHEN (max(source_segment_audience_count) + max(overlap_segment_audience_count) - max(overlap_audience_count)) > 0 THEN (cast(max(overlap_audience_count) AS DECIMAL(18, 2)) / cast((max(source_segment_audience_count) + max(overlap_segment_audience_count) - max(overlap_audience_count)) AS DECIMAL(18, 2))) * 100::DECIMAL(9, 2)
            ELSE 100.00
        END overlapping_percentage
  FROM
    (SELECT adwh_fact_profile_overlap_of_segments.Segment1 source_segment_id,
            adwh_fact_profile_overlap_of_segments.Segment2 overlap_segment_id,
            Sum(count_of_overlap) overlap_audience_count
    FROM qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments
    WHERE qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.date_key = '2024-01-10'
    GROUP BY qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.Segment2 ,
              qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.Segment1) a
  INNER JOIN
    (SELECT sum(count_of_profiles) source_segment_audience_count,
            adwh_dim_segments.segment_name source_segment_name,
            adwh_fact_profile_by_segment_trendlines.merge_policy_id,
            adwh_fact_profile_by_segment_trendlines.segment_Id segment1
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
    JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_dim_segments.segment_id = qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_Id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
    GROUP BY qsaccel.profile_agg.adwh_dim_segments.segment_name,
              qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id,
              qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_id) b ON a.source_segment_id = b.segment1
  INNER JOIN
    (SELECT sum(count_of_profiles) overlap_segment_audience_count,
            adwh_dim_segments.segment_name overlap_segment_name,
            adwh_fact_profile_by_segment_trendlines.merge_policy_id,
            adwh_fact_profile_by_segment_trendlines.segment_Id segment2
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
    JOIN qsaccel.profile_agg.adwh_dim_segments ON adwh_dim_segments.segment_id = adwh_fact_profile_by_segment_trendlines.segment_Id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
    GROUP BY qsaccel.profile_agg.adwh_dim_segments.segment_name,
              qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id,
              qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_id) c ON a.overlap_segment_id = c.segment2
  GROUP BY source_segment_name,
          source_segment_id,
          overlap_segment_name,
          overlap_segment_id
  ORDER BY overlapping_percentage DESC
  LIMIT 5;
```

+++

Weitere Informationen [ Erscheinungsbild und Funktionalität dieser Einsicht finden Sie in ](../guides/audiences.md#audience-overlap-report) Widget-Dokumentation zum Bericht zur Zielgruppenüberschneidung .

## Zielgruppenüberschneidung {#audience-overlap}

Diese Einsicht beantwortet Fragen:

- Welche Profile sind für beide Zielgruppen gleich?
- Wie wirkt sich die Überschneidung auf Interaktions- oder Konversionsraten aus?
- Wie können Marketing-Strategien auf das sich überschneidende Segment zugeschnitten werden?

+++Auswählen, um die SQL anzuzeigen, die diese Einsicht generiert

```sql
SELECT Sum(overlap_col1) overlap_col1,
        Sum(overlap_col2) overlap_col2,
        Sum(overlap_count) Overlap_count
  FROM
    (SELECT 0 overlap_col1,
            0 overlap_col2,
            sum(count_of_overlap)Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments
    WHERE qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.merge_policy_id = 1133248113
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.date_key = '2024-01-10'
      AND ((qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment1=1870062812
            AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment2=2080256533)
            OR (qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment1=2080256533
                AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment2=1870062812))
    UNION ALL SELECT sum(count_of_profiles) overlap_col1,
                      0 overlap_col2,
                      0 overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
    LEFT JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_Id = qsaccel.profile_agg.adwh_dim_segments.segment_Id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 1133248113
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_dim_segments.segment_Id = 1870062812
    UNION ALL SELECT 0 overlap_col1,
                      sum(count_of_profiles) overlap_col2,
                      0 Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
    JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_Id = qsaccel.profile_agg.adwh_dim_segments.segment_Id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 1133248113
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_dim_segments.segment_Id = 2080256533 ) a;
```

+++

Weitere Informationen [ Erscheinungsbild und Funktionalität dieser Einsicht finden Sie in ](../guides/audiences.md#audience-overlap) Dokumentation zu Zielgruppenüberschneidungen .

## Entwicklung der Zielgruppengröße {#audience-size-change-trend}

Diese Einsicht beantwortet Fragen:

- Gibt es signifikante Spitzen oder Rückgänge in der Zielgruppengröße innerhalb der letzten 30 Tage, 90 Tage oder 12 Monate?
- Wie ändert sich die Zielgruppengröße an bestimmten Tagen?
- Gab es in den letzten 12 Monaten Anomalien oder sich wiederholende Muster von Spitzen oder Tiefpunkten?

+++Auswählen, um die SQL anzuzeigen, die diese Einsicht generiert

```sql
SELECT date_key,
      Profiles_added
  FROM
    (SELECT rn_num,
            date_key,
            (count_of_profiles-lag(count_of_profiles, 1, 0) over(
                                                                ORDER BY date_key))Profiles_added
    FROM
      (SELECT date_key,
              sum(x.count_of_profiles)count_of_profiles,
              row_number() OVER (
                                  ORDER BY date_key) rn_num
        FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines x
        INNER JOIN
          (SELECT MAX(process_date) last_process_date,
                  merge_policy_id
          FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
          WHERE process_name = 'FACT_TABLES_PROCESSING'
            AND process_status = 'SUCCESSFUL'
          GROUP BY merge_policy_id) y ON x.merge_policy_id = y.merge_policy_id
        WHERE segment_id = 1333234510
          AND x.date_key >= dateadd(DAY, -30 -1, y.last_process_date)
        GROUP BY x.date_key) a)b
  WHERE rn_num > 1;
```

+++

Weitere Informationen [ Aussehen und Funktionalität dieser Einsicht finden Sie in ](../guides/audiences.md#audience-size-change-trend) Dokumentation zum Widget „Entwicklung der“.

## Entwicklung der Zielgruppengröße nach Identität {#audience-size-trend-by-identity}

Diese Einsicht beantwortet Fragen:

- Wachst, stabilisiert oder erlebt meine Zielgruppe ständig Schwankungen?
- Gibt es eine bestimmte Identität, die im Laufe der Zeit Spitzen oder Rückgänge beim Zielgruppenwachstum aufweist?
- Gibt es Anomalien in meinem Identitätswachstum im Laufe der Zeit?

+++Auswählen, um die SQL anzuzeigen, die diese Einsicht generiert

```sql
SELECT sum(count_of_profiles) AS identities,
        date_key
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines x
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
    FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
    GROUP BY merge_policy_id) y ON x.merge_policy_id = y.merge_policy_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_namespaces z ON x.namespace_id = z.namespace_id
  AND x.merge_policy_id = z.merge_policy_id
  WHERE x.date_key >= dateadd(DAY, -30, y.last_process_date)
    AND x.segment_id = 1333234510
    AND z.namespace_description = 'crmid'
  GROUP BY date_key;
```

+++

Informationen [ Erscheinungsbild und Funktionalität dieser Einsicht finden Sie in ](../guides/audiences.md#audience-size-trend-by-identity) Dokumentation zu Widgets für die Entwicklung der Zielgruppengröße nach Identität.

## Trend der Zielgruppen-Größe {#audience-size-trend}

Diese Einsicht beantwortet Fragen:

- Wie hat sich die Zielgruppengröße im Laufe der Zeit verändert, einschließlich aller Anomalien?
- Wie finde ich den allgemeinen Trend der Zielgruppengröße über die Zeiträume: 30 Tage, 90 Tage und 12 Monate?
- Was sind die wichtigsten Merkmale der Zielgruppe, die zu ihrer Größe beitragen? Beispielsweise Spitzen aufgrund von E-Mail-Marketing-Kampagnen.

+++Auswählen, um die SQL anzuzeigen, die diese Einsicht generiert

```sql
SELECT date_key,
        sum(count_of_profiles) AS audience_size
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines x
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
    FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
    GROUP BY merge_policy_id) y ON x.merge_policy_id = y.merge_policy_id
  WHERE date_key >= dateadd(DAY, -30, y.last_process_date)
    AND x.segment_id = 1333234510
  GROUP BY date_key,
          segment_id;
```

+++

Weitere Informationen [ Erscheinungsbild und Funktionalität dieser Einsicht finden Sie in ](../guides/audiences.md#audience-size-trend) Dokumentation zu Widgets für die Entwicklung der Zielgruppengröße .

## Zielgruppengröße {#audience-size}

Diese Einsicht beantwortet Fragen:

- Wie groß ist die aktuelle Zielgruppe insgesamt?
- Wie sieht die aktuelle Zielgruppengröße im Vergleich zu früheren Zeiträumen oder bestimmten Zielgruppen aus?
- Wie wirken sich die letzten Marketing-Kampagnen auf die Zielgruppengröße aus?

+++Auswählen, um die SQL anzuzeigen, die diese Einsicht generiert

```sql
SELECT
  sum(
    qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.count_of_profiles
  ) count_of_profiles
FROM
  qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_id = qsaccel.profile_agg.adwh_dim_segments.segment_id
WHERE
  qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_id = -1323307941
  AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 1914917902
  AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-12';
```

+++

Weitere Informationen [ Erscheinungsbild und Funktionalität dieser Einsicht finden Sie in ](../guides/audiences.md#audience-size) Dokumentation zu Widgets für Zielgruppengrößen .

## Kunden-KI – Verteilung der Scores {#customer-ai-distribution-of-scores}

Diese Einsicht beantwortet Fragen:

- Wie sieht die Scoring-Verteilung für jeden Bereich meines Kunden-KI-Modells aus, gefiltert nach einer ausgewählten Zielgruppe?
- Was ist die Scoring-Verteilung von hoch, mittel und niedrig für eine bestimmte Zielgruppe?
- Wie ist die Verteilung der Punktzahl nach Zielgruppen aufgeschlüsselt?

+++Auswählen, um die SQL anzuzeigen, die diese Einsicht generiert

```sql
SELECT b.model_name,
      b.model_type,
      c.segment_name,
      c.segment_id,
      CASE
        WHEN score >= 0
          AND score < 25 THEN 'LOW'
        WHEN score >= 25
          AND score < 75 THEN 'MEDIUM'
        WHEN score >= 75
          AND score <= 100 THEN 'HIGH'
        END bucket_name,
      CASE
        WHEN score >= 0
          AND score < 5 THEN '02.50'
        WHEN score >= 5
          AND score < 10 THEN '07.50'
        WHEN score >= 10
          AND score < 15 THEN '12.50'
        WHEN score >= 15
          AND score < 20 THEN '17.50'
        WHEN score >= 20
          AND score < 25 THEN '22.50'
        WHEN score >= 25
          AND score < 30 THEN '27.50'
        WHEN score >= 30
          AND score < 35 THEN '32.50'
        WHEN score >= 35
          AND score < 40 THEN '37.50'
        WHEN score >= 40
          AND score < 45 THEN '42.50'
        WHEN score >= 45
          AND score < 50 THEN '47.50'
        WHEN score >= 50
          AND score < 55 THEN '52.50'
        WHEN score >= 55
          AND score < 60 THEN '57.50'
        WHEN score >= 60
          AND score < 65 THEN '62.50'
        WHEN score >= 65
          AND score < 70 THEN '67.50'
        WHEN score >= 70
          AND score < 75 THEN '72.50'
        WHEN score >= 75
          AND score < 80 THEN '77.50'
        WHEN score >= 80
          AND score < 85 THEN '82.50'
        WHEN score >= 85
          AND score < 90 THEN '87.50'
        WHEN score >= 90
          AND score < 95 THEN '92.50'
        WHEN score >= 95
          AND score <= 100 THEN '97.50'
        END score_bins,
      Sum(CASE
            WHEN score >= 0
              AND score < 25 THEN count_of_profiles
            WHEN score >= 25
              AND score < 75 THEN count_of_profiles
            WHEN score >= 75
              AND score <= 100 THEN count_of_profiles
        END) count_of_profiles
   FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_ai_models a
          JOIN qsaccel.profile_agg.adwh_dim_ai_models b ON a.merge_policy_id = b.merge_policy_id
     AND a.model_id = b.model_id
          JOIN qsaccel.profile_agg.adwh_dim_segments c ON a.segment_id = c.segment_id
   WHERE a.merge_policy_id = 1133248113
     AND a.model_id = 1829081696
     AND a.segment_id = 1870062812
     AND score_date =
         (SELECT MAX(score_date)
          FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_ai_models d
          WHERE d.model_id = a.model_id) GROUP  BY b.model_name,
             b.model_type,
             c.segment_name,
             c.segment_id,
             CASE
               WHEN score >= 0
                 AND score < 25 THEN 'LOW'
               WHEN score >= 25
                 AND score < 75 THEN 'MEDIUM'
               WHEN score >= 75
                 AND score <= 100 THEN 'HIGH'
               END,
             CASE
               WHEN score >= 0
                 AND score < 5 THEN '02.50'
               WHEN score >= 5
                 AND score < 10 THEN '07.50'
               WHEN score >= 10
                 AND score < 15 THEN '12.50'
               WHEN score >= 15
                 AND score < 20 THEN '17.50'
               WHEN score >= 20
                 AND score < 25 THEN '22.50'
               WHEN score >= 25
                 AND score < 30 THEN '27.50'
               WHEN score >= 30
                 AND score < 35 THEN '32.50'
               WHEN score >= 35
                 AND score < 40 THEN '37.50'
               WHEN score >= 40
                 AND score < 45 THEN '42.50'
               WHEN score >= 45
                 AND score < 50 THEN '47.50'
               WHEN score >= 50
                 AND score < 55 THEN '52.50'
               WHEN score >= 55
                 AND score < 60 THEN '57.50'
               WHEN score >= 60
                 AND score < 65 THEN '62.50'
               WHEN score >= 65
                 AND score < 70 THEN '67.50'
               WHEN score >= 70
                 AND score < 75 THEN '72.50'
               WHEN score >= 75
                 AND score < 80 THEN '77.50'
               WHEN score >= 80
                 AND score < 85 THEN '82.50'
               WHEN score >= 85
                 AND score < 90 THEN '87.50'
               WHEN score >= 90
                 AND score < 95 THEN '92.50'
               WHEN score >= 95
                 AND score <= 100 THEN '97.50'
               END;
```

+++

Weitere Informationen [ Erscheinungsbild und Funktionalität dieser Einsicht finden Sie in der Widget](../guides/audiences.md#customer-ai-distribution-of-scores)Dokumentation zur Kunden-KI-Verteilung der Bewertungen ).

## Zusammenfassung der KI-Kundenbewertung {#customer-ai-scoring-summary}

Diese Einsicht beantwortet Fragen:

- Wie lautet die Scoring-Zusammenfassung für jedes meiner Kunden-KI-Modelle für eine bestimmte Zielgruppe?
- Wie ändern sich die Tendenzwerte meiner Kunden-KI für verschiedene Zielgruppen?
- Wie lässt sich meine Scoring-Zusammenfassung mit den anderen KPIs in der Zielgruppenübersicht vergleichen?

+++Auswählen, um die SQL anzuzeigen, die diese Einsicht generiert

```sql
SELECT model_name,
         model_type,
         segment_name,
         CASE
             WHEN score BETWEEN 0 AND 24 THEN 'LOW'
             WHEN score BETWEEN 25 AND 74 THEN 'MEDIUM'
             WHEN score BETWEEN 75 AND 100 THEN 'HIGH'
         END score_buckets,
         sum(count_of_profiles) count_of_profiles
  FROM QSAccel.profile_agg.adwh_fact_profile_by_segment_ai_models a
  JOIN QSAccel.profile_agg.adwh_dim_ai_models b ON a.merge_policy_id=b.merge_policy_id
  AND a.model_id=b.model_id
  JOIN QSAccel.profile_agg.adwh_dim_segments c ON a.segment_id=c.segment_id
  WHERE a.merge_policy_id=1133248113
    AND a.model_id =1829081696
    AND a.segment_id=1870062812
    AND score_date=
      (SELECT max(score_date)
       FROM QSAccel.profile_agg.adwh_fact_profile_by_segment_ai_models d
       WHERE d.model_id=a.model_id)
  GROUP BY model_name,
           model_type,
           segment_name,
           CASE
               WHEN score BETWEEN 0 AND 24 THEN 'LOW'
               WHEN score BETWEEN 25 AND 74 THEN 'MEDIUM'
               WHEN score BETWEEN 75 AND 100 THEN 'HIGH'
           END;
```

+++

Weitere Informationen [ Erscheinungsbild und Funktionalität dieser Einsicht finden Sie in ](../guides/audiences.md#customer-ai-scoring-summary) Dokumentation zum Kunden-KI-Scoring-.

## Identitätsüberschneidung {#identity-overlap}

Diese Einsicht beantwortet Fragen:

- Wie überschneiden sich [!UICONTROL Identitätstyp A] und [!UICONTROL Identitätstyp B] bei einer gefilterten Zielgruppe?
- Wie verfeinere ich Zielgruppen basierend auf der Überschneidung bestimmter Identitätstypen, um die zielgerichteten Marketing-Strategien zu verbessern?
- Welche Einblicke kann man aus der Evaluierung der Kampagnenleistung in den sich überschneidenden Bereichen gewinnen?
- Wie lassen sich zukünftige Marketing-Maßnahmen auf der Grundlage dieser Erkenntnisse optimieren?

+++Auswählen, um die SQL anzuzeigen, die diese Einsicht generiert

```sql
SELECT Sum(overlap_col1) overlap_col1,
        Sum(overlap_col2) overlap_col2,
        Sum(overlap_count) Overlap_count
  FROM
    (SELECT 0 overlap_col1,
            0 overlap_col2,
            Sum(count_of_profiles) Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace_by_segment
    WHERE qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace_by_segment.segment_id = 1333234510
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace_by_segment.merge_policy_id = 1709997014
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace_by_segment.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace_by_segment.overlap_id IN
        (SELECT a.overlap_id
          FROM
            (SELECT qsaccel.profile_agg.adwh_dim_overlap_namespaces.overlap_id overlap_id,
                    count(*) cnt_num
            FROM qsaccel.profile_agg.adwh_dim_overlap_namespaces
            WHERE qsaccel.profile_agg.adwh_dim_overlap_namespaces.merge_policy_id = 1709997014
              AND qsaccel.profile_agg.adwh_dim_overlap_namespaces.overlap_namespaces in ('crmid',
                                                                                          'email')
            GROUP BY qsaccel.profile_agg.adwh_dim_overlap_namespaces.overlap_id)a
          WHERE a.cnt_num>1 )
    UNION ALL SELECT count_of_profiles overlap_col1,
                      0 overlap_col2,
                      0 Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines
    LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
    AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
    WHERE qsaccel.profile_agg.adwh_dim_namespaces.namespace_description = 'crmid'
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.segment_id = 1333234510
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.merge_policy_id = 1709997014
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.date_key = '2024-01-10'
    UNION ALL SELECT 0 overlap_col1,
                      count_of_profiles overlap_col2,
                      0 Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines
    LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
    AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
    WHERE qsaccel.profile_agg.adwh_dim_namespaces.namespace_description = 'email'
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.segment_id = 1333234510
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.merge_policy_id = 1709997014
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.date_key = '2024-01-10' ) a;
```

+++

Informationen [ Erscheinungsbild und Funktionalität dieser Einsicht finden Sie in ](../guides/audiences.md#identity-overlap) Dokumentation zum Widget „Identitätsüberschneidung“ .

## Profile nach Identität {#profiles-by-identity}

Diese Einsicht beantwortet Fragen:

- Welcher Identitätstyp hat den höchsten Anteil in der Gesamtzahl der Profile für eine ausgewählte Zielgruppe?
- Gibt es bei den Identitätstypen für eine ausgewählte Zielgruppe signifikante Unterschiede?
- Wie ist die Gesamtverteilung der Identitätstypen nach Zielgruppe?
- Gibt es signifikante Unterschiede oder Anomalien bei der Anzahl von Identitäten für verschiedene Zielgruppen?

+++Auswählen, um die SQL anzuzeigen, die diese Einsicht generiert

```sql
SELECT qsaccel.profile_agg.adwh_dim_namespaces.namespace_description,
        sum(qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.count_of_profiles) count_of_profiles
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
  AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.segment_id = 1333234510
    AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.merge_policy_id = 1709997014
    AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.date_key = '2024-01-10'
  GROUP BY qsaccel.profile_agg.adwh_dim_namespaces.namespace_description
  ORDER BY count_of_profiles DESC;
```

+++

Informationen [ Erscheinungsbild und Funktionalität dieser Einsicht finden Sie in ](../guides/audiences.md#profiles-by-identity) Dokumentation zum Widget „Profile nach Identität .

## Geplante Aktivierungen {#scheduled-activations}

Diese Einsicht beantwortet Fragen:

- Welches Start- und Enddatum haben die leistungsstärksten Aktivierungen für eine bestimmte Zielgruppe auf einer bestimmten Plattform?
- Welche Plattformen wurden am häufigsten für geplante Aktivierungen einer bestimmten Zielgruppe verwendet?
- Gibt es Muster in der Platform-Nutzung, die bei Entscheidungen über die Priorisierung oder Diversifizierung von Aktivierungsstrategien für eine bestimmte Zielgruppe hilfreich sein könnten?

+++Auswählen, um die SQL anzuzeigen, die diese Einsicht generiert

```sql
SELECT p.destination_platform ,
       p.destination_platform_name AS platform ,
       d.destination_name ,
       d.destination ,
       br.start_date ,
       CASE
           WHEN br.end_date = '9999-12-31' THEN 'Ongoing'
           ELSE br.end_date
       END AS end_date
  FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations br
  JOIN qsaccel.profile_agg.adwh_dim_destination d ON br.destination_id = d.destination_id
  JOIN qsaccel.profile_agg.adwh_dim_destination_platform p ON d.destination_platform_id = p.destination_platform_id
  JOIN
    (SELECT MAX(process_date) AS last_process_date
     FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
     WHERE process_name = 'FACT_TABLES_PROCESSING'
       AND process_status = 'SUCCESSFUL' ) lpd ON lpd.last_process_date BETWEEN br.start_date AND br.end_date
  AND br.segment_id = 1333234510;
```

+++

Weitere Informationen [ Erscheinungsbild und Funktionalität dieser Einblicke finden ](../guides/audiences.md#scheduled-activations) in der Dokumentation zum Widget „Geplante Aktivierungen“.

## Nächste Schritte

Durch das Lesen dieses Dokuments wissen Sie jetzt, welche SQL-Daten Dashboard-Einblicke generieren und welche häufigen Fragen diese Analyse löst. Sie können jetzt SQL bearbeiten und iterieren, um eigene Einblicke zu generieren.

In der [SQL-Dokumentation anzeigen](../view-sql.md) finden Sie weitere Informationen darüber, wie Sie die SQL Ihrer Insights direkt über die Platform-Benutzeroberfläche anpassen können.

Sie können auch den SQL-Code lesen und verstehen, der Einblicke für die Dashboards [Profile](./profiles.md), [Kontoprofile](./account-profiles.md) und [Ziele](./destinations.md) generiert.
