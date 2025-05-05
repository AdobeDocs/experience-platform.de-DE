---
title: Profil-Insights
description: Entdecken Sie die SQL, die Ihren Profileinblicken zugrunde liegt, und verwenden Sie diese Abfragen, um benutzerdefinierte Einblicke zu generieren, die Ihre Kunden und deren Kundenerlebnisse weiter untersuchen.
exl-id: f3792076-3e01-4e26-8788-32927202a2e5
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1660'
ht-degree: 3%

---

# Profileinblicke

Die aus der Analyse Ihres Datenmodells gewonnenen Erkenntnisse machen Ihre Adobe Real-Time CDP-Daten zugänglicher, verständlicher und wirkungsvoller für die Entscheidungsfindung.

Verstehen Sie Ihre Profileinblicke, indem Sie auf die SQL zugreifen, die sie unterstützt, und dann Ihre eigenen Einblicke generieren, um Ihre Kunden und deren Kundenerlebnisse, aus denen Ihre Profile bestehen, weiter zu untersuchen. Wandeln Sie Ihre Rohdaten in neue umsetzbare Einblicke um, indem Sie das vorhandene Real-Time CDP-Datenmodell als SQL-Inspiration verwenden, um Abfragen für Ihre individuellen Geschäftsanforderungen zu erstellen.

Weitere Informationen [ Anpassen der SQL-Insights ](../view-sql.md) Sie direkt über die Experience Platform-Benutzeroberfläche in der Dokumentation zu SQL anzeigen .

Die folgenden Einblicke stehen Ihnen als Teil des (Profile[Dashboards ](../guides/profiles.md) benutzerdefinierten (benutzerdefinierten) [ zur ](../standard-dashboards.md). Anleitungen zum Anpassen Ihres Dashboards oder zum [Erstellen und Bearbeiten neuer Widgets](../customize/custom-widgets.md) in der Widget-Bibliothek und im benutzerdefinierten Dashboard finden [&#128279;](../customize/overview.md) in der [Anpassungsübersicht](../standard-dashboards.md#create-widget).

## Zielgruppenüberschneidung durch Zusammenführungsrichtlinie {#audience-overlap-by-merge-policy}

Fragen, die von diesem insight beantwortet werden:

- Welche Profile sind für beide Zielgruppen gleich?
- Wie wirkt sich die Überschneidung auf Interaktions- oder Konversionsraten aus?
- Wie können Marketing-Strategien auf das sich überschneidende Segment zugeschnitten werden?

+++Auswählen, um die SQL anzuzeigen, die diese insight generiert

```sql
SELECT Sum(overlap_col1) overlap_col1,
        Sum(overlap_col2) overlap_col2,
        Sum(overlap_count) Overlap_count
  FROM
    (SELECT 0 overlap_col1,
            0 overlap_col2,
            sum(count_of_overlap)Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments
    WHERE qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.date_key = '2024-01-10'
      AND ((qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment1=1333234510
            AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment2=1559754729)
            OR (qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment1=1559754729
                AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment2=1333234510))
    UNION ALL SELECT sum(count_of_profiles) overlap_col1,
                      0 overlap_col2,
                      0 overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
    LEFT JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_Id = qsaccel.profile_agg.adwh_dim_segments.segment_Id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_dim_segments.segment_Id = 1333234510
    UNION ALL SELECT 0 overlap_col1,
                      sum(count_of_profiles) overlap_col2,
                      0 Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
    JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_Id = qsaccel.profile_agg.adwh_dim_segments.segment_Id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_dim_segments.segment_Id = 1559754729 ) a;
```

+++

Weitere Informationen [ Erscheinungsbild und Funktionalität dieser insight finden Sie ](../guides/profiles.md#audience-overlap-by-merge-policy) der Widget-Dokumentation „Zielgruppenüberschneidung nach Zusammenführungsrichtlinie“.

## Bericht zur Zielgruppenüberschneidung {#audience-overlap-report}

Fragen, die von diesem insight beantwortet werden:

- Welche 50 Zielgruppen überschneiden sich am meisten?
- Welche Zielgruppen überschneiden sich am wenigsten?
- Wie ändert sich das Überschneidungsmuster je nach Zusammenführungsrichtlinie?

+++Auswählen, um die SQL anzuzeigen, die diese insight generiert

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

Weitere Informationen [ Erscheinungsbild und Funktionalität dieser insight finden Sie ](../guides/profiles.md#audience-overlap-report) der Widget-Dokumentation „Bericht Zielgruppenüberschneidung“ .

## Zielgruppen (Anzahl) {#audiences}

Fragen, die von diesem insight beantwortet werden:

- Welche Zusammenführungsrichtlinie wird hauptsächlich für die Segmentierung verwendet?
- Wie ist die Verteilung von Zielgruppen über Zusammenführungsrichtlinien hinweg?
- Gibt es im Laufe der Zeit signifikante Änderungen bei den Zielgruppenzahlen für bestimmte Zusammenführungsrichtlinien?

+++Auswählen, um die SQL anzuzeigen, die diese insight generiert

```sql
SELECT count(DISTINCT a.segment_id) count_of_segments
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines a
  JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
    FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
    GROUP BY merge_policy_id) b ON a.merge_policy_id= b.merge_policy_id
  AND a.date_key = b.last_process_date
  WHERE a.merge_policy_id= 2027892989;
```

+++

Weitere Informationen [ Erscheinungsbild und Funktionalität dieser insight finden ](../guides/profiles.md#audiences) in der Dokumentation zum Zielgruppen-Widget .

## Zielgruppen, die dem Zielstatus zugeordnet sind {#audiences-mapped-to-destination-status}

Fragen, die von diesem insight beantwortet werden:

- Wie ist die Gesamtverteilung der Zielgruppen zwischen zugeordneten und nicht zugeordneten Zielen?
- Welche spezifischen Ziele haben die höchste Anzahl zugeordneter Zielgruppen?
- Welcher Anteil der gesamten Zielgruppen bleibt nicht zugeordnet?
- Gibt es bei diesen nicht zugeordneten Zielgruppen Muster oder verknüpfte Trends?

+++Auswählen, um die SQL anzuzeigen, die diese insight generiert

```sql
SELECT COUNT(DISTINCT (y.segment_id)) AS count_mapped_segments,
        COUNT(DISTINCT (x.segment_id)) - COUNT(DISTINCT (y.segment_id)) AS count_unmapped_segments,
        COUNT(DISTINCT (x.segment_id)) AS total_segments
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines x
  LEFT JOIN qsaccel.profile_agg.adwh_dim_br_segment_destinations y ON x.segment_id = y.segment_id
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
    FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
    GROUP BY merge_policy_id) z ON x.merge_policy_id = z.merge_policy_id
  AND x.date_key = z.last_process_date
  WHERE x.merge_policy_id = 2027892989;
```

+++

Weitere Informationen [ Erscheinungsbild und Funktionalität dieser insight finden Sie in ](../guides/profiles.md#audiences-mapped-to-destination-status) Widget-Dokumentation Zielgruppen, die dem Zielstatus zugeordnet sind .

## Zielgruppengröße {#audiences-size}

Fragen, die von diesem insight beantwortet werden:

- Welches Zielgruppensegment hat die größte Größe?
- Welches sind die fünf größten Zielgruppen?
- Wie ändert sich die Verteilung der Zielgruppengröße im Laufe der Zeit für die Top-Zielgruppe?

+++Auswählen, um die SQL anzuzeigen, die diese insight generiert

```sql
SELECT qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key,
        qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name,
        qsaccel.profile_agg.adwh_dim_segments.segment,
        qsaccel.profile_agg.adwh_dim_segments.segment_name,
        sum(qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.count_of_profiles)count_of_profiles
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_id = qsaccel.profile_agg.adwh_dim_segments.segment_id
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id=adwh_dim_merge_policies.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
    AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id= 2027892989
  GROUP BY qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key,
          qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name,
          qsaccel.profile_agg.adwh_dim_segments.segment,
          qsaccel.profile_agg.adwh_dim_segments.segment_name
  ORDER BY count_of_profiles DESC
  LIMIT 20;
```

+++

Weitere Informationen [ Erscheinungsbild und Funktionalität dieser insight finden Sie in ](../guides/profiles.md#audiences-size) Dokumentation zu Widgets für Zielgruppen .

## Kunden-KI – Verteilung der Scores {#customer-ai-distribution-of-scores}

Fragen, die von diesem insight beantwortet werden:

- Wie ist die Verteilung der Scores auf die einzelnen Buckets für jedes meiner Kunden-KI-Modelle?
- Wie sind die Werte nach hohen, mittleren und niedrigen Werten verteilt?
- Wie ist die Verteilung der Bewertungen nach Zusammenführungsrichtlinie aufgeteilt?

+++Auswählen, um die SQL anzuzeigen, die diese insight generiert

```sql
SELECT b.model_name,
     b.model_type,
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
  FROM qsaccel.profile_agg.adwh_fact_profile_ai_models a
  JOIN qsaccel.profile_agg.adwh_dim_ai_models b ON a.merge_policy_id = b.merge_policy_id
  AND a.model_id = b.model_id
  WHERE a.merge_policy_id = 2027892989
    AND a.model_id = 1829081696
    AND score_date =
      (SELECT Max(score_date)
       FROM qsaccel.profile_agg.adwh_fact_profile_ai_models d
       WHERE d.model_id = a.model_id) GROUP  BY b.model_name,
          model_type,
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

Weitere Informationen [ Erscheinungsbild und Funktionalität dieser insight finden Sie in der Widget](../guides/profiles.md#customer-ai-distribution-of-scores)Dokumentation zur Kunden-KI-Verteilung der Bewertungen ).

## Zusammenfassung der KI-Kundenbewertung {#customer-ai-scoring-summary}

Fragen, die von diesem insight beantwortet werden:

- Wie lautet die Scoring-Zusammenfassung für jedes meiner Kunden-KI-Modelle?
- Wie ändern sich die Tendenzwerte meiner Kunden-KI für verschiedene Zielgruppen?
- Wie ändert sich meine Scoring-Zusammenfassung im Vergleich zu anderen KPIs in der Profilübersicht?

+++Auswählen, um die SQL anzuzeigen, die diese insight generiert

```sql
SELECT model_name,
         model_type,
         CASE
             WHEN score BETWEEN 0 AND 24 THEN 'LOW'
             WHEN score BETWEEN 25 AND 74 THEN 'MEDIUM'
             WHEN score BETWEEN 75 AND 100 THEN 'HIGH'
         END score_buckets,
         sum(count_of_profiles) count_of_profiles
  FROM QSAccel.profile_agg.adwh_fact_profile_ai_models a
  JOIN QSAccel.profile_agg.adwh_dim_ai_models b ON a.merge_policy_id=b.merge_policy_id
  AND a.model_id=b.model_id
  WHERE a.merge_policy_id=2027892989
    AND a.model_id =1829081696
    AND score_date=
      (SELECT max(score_date)
       FROM QSAccel.profile_agg.adwh_fact_profile_ai_models d
       WHERE d.model_id=a.model_id)
  GROUP BY model_name,
           model_type,
           CASE
               WHEN score BETWEEN 0 AND 24 THEN 'LOW'
               WHEN score BETWEEN 25 AND 74 THEN 'MEDIUM'
               WHEN score BETWEEN 75 AND 100 THEN 'HIGH'
           END;
```

+++

Weitere Informationen [ Erscheinungsbild und die Funktionalität dieser insight finden Sie in ](../guides/profiles.md#customer-ai-scoring-summary) Dokumentation zum Kunden-KI-Scoring Zusammenfassung-Widget .

## Identitätsüberschneidung {#identity-overlap}

Fragen, die von diesem insight beantwortet werden:

- Wie überschneiden sich [!UICONTROL Identitätstyp A] und [!UICONTROL Identitätstyp B]?
- Wie kann ich Zielgruppen basierend auf der Überschneidung bestimmter Identitätstypen einschränken, um zielgerichtete Marketing-Strategien zu verbessern?
- Welche Einblicke kann man aus der Evaluierung der Kampagnenleistung in den sich überschneidenden Bereichen gewinnen?
- Wie können zukünftige Marketing-Maßnahmen mithilfe dieser Kampagnen-Performance-insight optimiert werden?

+++Auswählen, um die SQL anzuzeigen, die diese insight generiert

```sql
SELECT Sum(overlap_col1) overlap_col1,
        Sum(overlap_col2) overlap_col2,
        coalesce(Sum(overlap_count), 0) overlap_count
  FROM
    (SELECT 0 overlap_col1,
            0 overlap_col2,
            Sum(count_of_profiles) overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace
    WHERE qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace.overlap_id IN
        (SELECT a.overlap_id
          FROM
            (SELECT qsaccel.profile_agg.adwh_dim_overlap_namespaces.overlap_id overlap_id,
                    count(*) cnt_num
            FROM qsaccel.profile_agg.adwh_dim_overlap_namespaces
            WHERE qsaccel.profile_agg.adwh_dim_overlap_namespaces.merge_policy_id = 2027892989
              AND qsaccel.profile_agg.adwh_dim_overlap_namespaces.overlap_namespaces in ('avid',
                                                                                          'crmid')
            GROUP BY qsaccel.profile_agg.adwh_dim_overlap_namespaces.overlap_id)a
          WHERE a.cnt_num>1 )
    UNION ALL SELECT count_of_profiles overlap_col1,
                      0 overlap_col2,
                      0 overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines
    JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
    AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_dim_namespaces.namespace_description = 'avid'
    UNION ALL SELECT 0 overlap_col1,
                      count_of_profiles overlap_col2,
                      0 Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines
    JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
    AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_dim_namespaces.namespace_description = 'crmid' )a;
```

+++

Weitere Informationen [ Erscheinungsbild und Funktionalität dieser insight finden Sie in ](../guides/profiles.md#identity-overlap) Dokumentation zum Widget „Identitätsüberschneidung“ .

## Anzahl der Profile {#profile-count}

Fragen, die von diesem insight beantwortet werden:

- Wie hoch ist die Gesamtanzahl der Profile in der Adobe Real-Time Customer Data Platform?
- Wie werden Profile basierend auf Zusammenführungsrichtlinien verteilt?
- Welche Zusammenführungsrichtlinie hat die höchste Profilanzahl?

Die SQL-Abfrage, die diese Einblicke generiert, lautet wie folgt:

```sql
SELECT qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name,
       sum(qsaccel.profile_agg.adwh_fact_profile.count_of_profiles) CNT
  FROM qsaccel.profile_agg.adwh_fact_profile
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_id=adwh_fact_profile.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile.date_key='2024-01-10'
    AND qsaccel.profile_agg.adwh_fact_profile.merge_policy_id = 2027892989
  GROUP BY qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name;
```

Vollständige Informationen zum Aussehen und zur Funktionalität dieser insight finden Sie im [Handbuch zu Widgets für die Profilanzahl](https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/profiles.html#profile-count).

Weitere Informationen [ Erscheinungsbild und Funktionalität dieser insight finden Sie in ](../guides/profiles.md#profile-count) Dokumentation zum Widget „Profilanzahl“ .

## Änderung der Profilanzahl {#profile-count-change}

Fragen, die von diesem insight beantwortet werden:

- Wie ist der Trend bei den Änderungen der Gesamtprofilanzahl?
- Was hat zu signifikanten Spitzen oder Rückgängen der Profilanzahl geführt?
- Gibt es bestimmte Zusammenführungsrichtlinien, die die Änderung der Profilanzahl bewirken?

+++Auswählen, um die SQL anzuzeigen, die diese insight generiert

```sql
SELECT (sum(count_of_profiles) - sum(count_of_profiles_days_ago)) profiles_added
  FROM
    (SELECT sum(qsaccel.profile_agg.adwh_fact_profile.count_of_profiles) count_of_profiles,
            0 count_of_profiles_days_ago
    FROM qsaccel.profile_agg.adwh_fact_profile
    WHERE qsaccel.profile_agg.adwh_fact_profile.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile.date_key = '2024-01-10'
    UNION ALL SELECT 0 count_of_profiles,
                      CASE
                          WHEN sum(cntondatediff) =0 THEN sum(cntmin)
                          ELSE sum(cntondatediff)
                      END AS count_of_profiles_days_ago
    FROM
      (SELECT coalesce(sum(qsaccel.profile_agg.adwh_fact_profile_by_trendlines.count_of_profiles), 0) cntondatediff,
              0 cntmin
        FROM qsaccel.profile_agg.adwh_fact_profile_by_trendlines
        WHERE qsaccel.profile_agg.adwh_fact_profile_by_trendlines.merge_policy_id =2027892989
          AND qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key =dateadd(DAY, - 30, '2024-01-10')
        UNION ALL SELECT 0 cntondatediff,
                        sum(qsaccel.profile_agg.adwh_fact_profile_by_trendlines.count_of_profiles) countMin
        FROM qsaccel.profile_agg.adwh_fact_profile_by_trendlines
        WHERE qsaccel.profile_agg.adwh_fact_profile_by_trendlines.merge_policy_id = 2027892989
          AND qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key =
            (SELECT min(qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key) col
            FROM qsaccel.profile_agg.adwh_fact_profile_by_trendlines
            WHERE qsaccel.profile_agg.adwh_fact_profile_by_trendlines.merge_policy_id =2027892989
              AND qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key >= dateadd(DAY, - 30, '2024-01-10')
              AND qsaccel.profile_agg.adwh_fact_profile_by_trendlines.count_of_profiles IS NOT NULL) )b) a;
```

+++

Weitere [ über das Erscheinungsbild und die Funktionalität dieser insight finden ](../guides/profiles.md#profile-count-change) in der Dokumentation zum Widget Änderung der Profilanzahl .

## Trend der Änderung der Profilanzahl {#profile-count-change-trend}

Fragen, die von diesem insight beantwortet werden:

- Wie sieht der allgemeine Trend der Änderung der Profilanzahl in den letzten 12 Monaten basierend auf der Zusammenführungsrichtlinie aus?
- Gibt es bestimmte Muster oder Schwankungen in der Profilanzahl, die innerhalb der letzten 30 Tage geändert werden und Beachtung erfordern?
- Wie ändert sich die Profilanzahl in den letzten 90 Tagen im Vergleich zum Gesamttrend?

+++Auswählen, um die SQL anzuzeigen, die diese insight generiert

```sql
SELECT date_key,
         profiles_count_change
  FROM
    (SELECT rn_num,
            date_key,
            (count_of_profiles-lag(count_of_profiles, 1, 0) over(
                                                            ORDER BY date_key))profiles_count_change
    FROM
      (SELECT qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key,
              sum(qsaccel.profile_agg.adwh_fact_profile_by_trendlines.count_of_profiles) count_of_profiles,
              row_number() OVER (
                              ORDER BY qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key) rn_num
      FROM qsaccel.profile_agg.adwh_fact_profile_by_trendlines
  WHERE qsaccel.profile_agg.adwh_fact_profile_by_trendlines.merge_policy_id = 2027892989
    AND qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key >=dateadd(DAY, - 30 -1, '2024-01-10')
  GROUP BY qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key)a)b
  WHERE rn_num > 1;
```

+++

Weitere [ über das Erscheinungsbild und die Funktionalität dieser insight finden ](../guides/profiles.md#profile-count-change-trend) in der Widget-Dokumentation zum Trend der Änderung der Profilanzahl .

## Entwicklung der Profilanzahl {#profile-count-trend}

Fragen, die von diesem insight beantwortet werden:

- Wie ist der allgemeine Trend der Profilanzahl basierend auf der Zusammenführungsrichtlinie in den letzten 30 Tagen?
- Wie lässt sich dieser Trend mit den längerfristigen Trends (z. B. 90 Tage und 12 Monate) vergleichen?
- Welche Zusammenführungsrichtlinie trägt am meisten zur Erhöhung oder Verringerung der Profilanzahl über die angegebenen Zeiträume (30 Tage, 90 Tage und 12 Monate) bei?
- Gibt es bestimmte Spitzen oder Rückgänge bei der Profilanzahl, die mit bestimmten Ereignissen oder Zeiträumen innerhalb des 30-tägigen Zeitraums korrelieren?

+++Auswählen, um die SQL anzuzeigen, die diese insight generiert

```sql
SELECT date_key,
       sum(count_of_profiles) AS count_of_profiles
  FROM qsaccel.profile_agg.adwh_fact_profile_by_trendlines x
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
     FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
     WHERE process_name = 'FACT_TABLES_PROCESSING'
       AND process_status = 'SUCCESSFUL'
     GROUP BY merge_policy_id) y ON x.merge_policy_id = y.merge_policy_id
  WHERE date_key >= dateadd(DAY, -365, y.last_process_date)
    AND x.merge_policy_id = 2027892989
  GROUP BY date_key;
```

+++

Weitere [ über das Erscheinungsbild und die Funktionen ](../guides/profiles.md#profile-count-trend) insight finden Sie in der Dokumentation zum Widget „Trend der Profilanzahl“ .

## Profile nach Identität {#profiles-by-identity}

Fragen, die von diesem insight beantwortet werden:

- Welcher Identitätstyp nimmt unter der Gesamtzahl der Profile einen höheren Anteil ein?
- Gibt es signifikante Unterschiede zwischen den Identitätstypen?
- Wie ist die Gesamtverteilung der Identitätstypen?
- Gibt es signifikante Unterschiede oder Anomalien bei der Identitätszählung?

+++Auswählen, um die SQL anzuzeigen, die diese insight generiert

```sql
SELECT qsaccel.profile_agg.adwh_dim_namespaces.namespace_description,
        sum(qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.count_of_profiles) count_of_profiles
  FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
  AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = 2027892989
    AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key = '2024-01-10'
  GROUP BY qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key,
          qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id,
          qsaccel.profile_agg.adwh_dim_namespaces.namespace_description
  ORDER BY count_of_profiles DESC;
```

+++

Weitere Informationen [ Erscheinungsbild und Funktionalität dieser insight finden Sie in ](../guides/profiles.md#profiles-by-identity) Dokumentation zum Widget „Profile nach Identität .

## Trend der Änderung der Profilanzahl {#profiles-count-change-trend}

Fragen, die von diesem insight beantwortet werden:

- Wie ist der allgemeine Trend bei der Änderung der Profilanzahl in den letzten 12 Monaten, basierend auf der Zusammenführungsrichtlinie?
- Gibt es bestimmte Muster oder Schwankungen in der Änderung der Profilanzahl in den letzten 30 Tagen, die Aufmerksamkeit erfordern?
- Wie lässt sich die Änderung der Profilanzahl in den letzten 90 Tagen im Vergleich zum Gesamttrend vergleichen?

+++Auswählen, um die SQL anzuzeigen, die diese insight generiert

```sql
SELECT date_key,
         profiles_count_change
  FROM
    (SELECT rn_num,
            date_key,
            (count_of_profiles-lag(count_of_profiles, 1, 0) over(
                                                            ORDER BY date_key))profiles_count_change
    FROM
      (SELECT qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key,
              sum(qsaccel.profile_agg.adwh_fact_profile_by_trendlines.count_of_profiles) count_of_profiles,
              row_number() OVER (
                              ORDER BY qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key) rn_num
      FROM qsaccel.profile_agg.adwh_fact_profile_by_trendlines
  WHERE qsaccel.profile_agg.adwh_fact_profile_by_trendlines.merge_policy_id = 2027892989
    AND qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key >=dateadd(DAY, - 30 -1, '2024-01-10')
  GROUP BY qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key)a)b
  WHERE rn_num > 1;
```

+++

Weitere [ über das Erscheinungsbild und die Funktionalität dieser insight finden Sie ](../guides/profiles.md#profiles-count-change-trend) der Widget-Dokumentation zum Trend der Änderung der Profilanzahl .

## Trend zur Änderung der Profilanzahl nach Identität {#profiles-count-change-trend-by-identity}

Fragen, die von diesem insight beantwortet werden:

- Wie ist der allgemeine Trend bei der Änderung der Profilanzahl über verschiedene Identitäten hinweg in den letzten 12 Monaten?
- Gibt es bestimmte Identitätstrends, die innerhalb der letzten 30 Tage signifikante Änderungen aufweisen?
- Wie unterscheiden sich die Änderungen der Profilanzahl beim Vergleich der Trends von 30 Tagen, 90 Tagen und 12 Monaten für eine bestimmte Identität?

+++Auswählen, um die SQL anzuzeigen, die diese insight generiert

```sql
SELECT date_key,
        namespace_description,
        profiles_count_change
  FROM
    (SELECT rn_num,
            date_key,
            namespace_description,
            (count_of_profiles - lag(count_of_profiles, 1, 0) over(PARTITION BY namespace_description
                                                                  ORDER BY date_key)) profiles_count_change
    FROM
      (SELECT qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key,
              qsaccel.profile_agg.adwh_dim_namespaces.namespace_description,
              sum(qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.count_of_profiles) count_of_profiles,
              row_number() OVER (PARTITION BY qsaccel.profile_agg.adwh_dim_namespaces.namespace_description
                                  ORDER BY qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key) rn_num
        FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines
        LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
        AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
        WHERE qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = 2027892989
          AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id= -1042977439
          AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key >= dateadd(DAY, - 30 -1, '2024-01-10')
        GROUP BY qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key,
                adwh_dim_namespaces.namespace_description)a)b
  WHERE rn_num > 1;
```

+++

Weitere Informationen [ Erscheinungsbild und Funktionalität dieser insight finden Sie in der ](../guides/profiles.md#profiles-count-change-trend-by-identity) zum Widget „Trend der Änderung der Profilanzahl nach Identität .

## Einzelne Identitätsprofile {#single-identity-profiles}

Fragen, die von diesem insight beantwortet werden:

- Werden meine Kundenidentitätsdaten konsistent mit einzelnen Identitäten dargestellt?
- Welcher Prozentsatz meiner Benutzerbasis besteht aus Profilen mit nur einem einzigen Identitätstyp?
- Wie wirkt sich dies auf die Vollständigkeit des Profils aus, wenn es sich um Profile mit nur einem Identitätstyp handelt?
- Gibt es eine Korrelation zwischen dem häufigsten Identitätstyp und der Anzahl einzelner Identitätsprofile?

+++Auswählen, um die SQL anzuzeigen, die diese insight generiert

```sql
SELECT qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name,
       sum(qsaccel.profile_agg.adwh_fact_profile.count_of_Single_Identity_profiles) CNT
  FROM qsaccel.profile_agg.adwh_fact_profile
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_id=adwh_fact_profile.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile.date_key='2024-01-10'
    AND qsaccel.profile_agg.adwh_fact_profile.merge_policy_id = 2027892989
  GROUP BY qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name;
```

+++

Weitere Informationen [ Erscheinungsbild und Funktionalität dieser insight finden Sie in ](../guides/profiles.md#single-identity-profiles) Dokumentation zum Widget „Einzelne Identitätsprofile .

## Einzelne Identitätsprofile nach Identität {#single-identity-profiles-by-identity}

Fragen, die von diesem insight beantwortet werden:

- Wie viele Unique Customers haben sich mit einer einzigen Identität (z. B. E-Mail oder Telefonnummer) registriert?
- Wie ist die Verteilung einzelner Identitätsprofile auf verschiedene Identitätstypen wie E-Mail oder Telefonnummern?
- Gibt es Identitätsmuster oder -verschiebungen innerhalb der einzelnen Identitätsprofile?

+++Auswählen, um die SQL anzuzeigen, die diese insight generiert

```sql
SELECT qsaccel.profile_agg.adwh_dim_namespaces.namespace_description,
        sum(qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.count_of_Single_Identity_profiles) count_of_Single_Identity_profiles
  FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
  AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = 2027892989
    AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key = '2024-01-10'
  GROUP BY qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key,
          qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id,
          qsaccel.profile_agg.adwh_dim_namespaces.namespace_description;
```

+++

Weitere Informationen [ Erscheinungsbild und Funktionalität dieser insight finden Sie in der ](../guides/profiles.md#single-identity-profiles-by-identity) zu Identitäts-Widgets Einzelprofile .

## Nicht segmentierte Profile {#unsegmented-profiles}

Fragen, die von diesem insight beantwortet werden:

- Wie viele Profile sind nicht Teil einer Zielgruppe?
- Welcher Prozentsatz der gesamten Zielgruppe wird durch nicht segmentierte Profile dargestellt?
- Trägt eine Zusammenführungsrichtlinie zu einer großen Anzahl nicht segmentierter Profile bei?

+++Auswählen, um die SQL anzuzeigen, die diese insight generiert

```sql
SELECT qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name,
       sum(qsaccel.profile_agg.adwh_fact_profile.count_of_Orphan_profiles) CNT
  FROM qsaccel.profile_agg.adwh_fact_profile
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_id=adwh_fact_profile.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile.date_key='2024-01-10'
    AND qsaccel.profile_agg.adwh_fact_profile.merge_policy_id = 2027892989
  GROUP BY qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name;
```

+++

Weitere Informationen [ Erscheinungsbild und Funktionalität dieser insight finden ](../guides/profiles.md#unsegmented-profiles) in der Widget-Dokumentation zu nicht segmentierten Profilen .

## Nächste Schritte

Durch das Lesen dieses Dokuments wissen Sie jetzt, welche SQL-Daten Dashboard-Einblicke generieren und welche häufigen Fragen diese Analyse löst. Sie können jetzt SQL bearbeiten und iterieren, um eigene Einblicke zu generieren.

In der [SQL-Dokumentation anzeigen](../view-sql.md) finden Sie weitere Informationen darüber, wie Sie die SQL Ihrer Insights direkt über die Platform-Benutzeroberfläche anpassen können.

Sie können auch die SQL lesen und verstehen, die Einblicke für die Dashboards [Zielgruppen](./audiences.md), [Kontoprofile](./account-profiles.md) und [Ziele](./destinations.md) generiert.
