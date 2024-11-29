---
title: Profileinblicke
description: Entdecken Sie die SQL, die Ihre Profileinblicke nutzt, um benutzerdefinierte Einblicke zu generieren, mit denen Sie Ihre Kunden und deren Kundenerlebnisse weiter untersuchen können.
exl-id: f3792076-3e01-4e26-8788-32927202a2e5
source-git-commit: cce576c00823a0c02e4b639f0888a466a5af6a0c
workflow-type: tm+mt
source-wordcount: '1659'
ht-degree: 3%

---

# Profileinblicke

Die aus der Analyse Ihres Datenmodells gewonnenen Erkenntnisse machen Ihre Adobe Real-Time CDP-Daten leichter zugänglich, verständlich und für die Entscheidungsfindung wirkungsvoll.

Machen Sie sich mit Ihren Profileinblicken vertraut, indem Sie auf die SQL zugreifen, über die diese Benutzer verfügen, und dann Ihre eigenen Einblicke generieren, um Ihre Kunden und deren Kundenerlebnisse, aus denen sich Ihre Profile zusammensetzen, weiter zu untersuchen. Transformieren Sie Ihre Rohdaten in neue umsetzbare Einblicke, indem Sie die vorhandene SQL des Real-Time CDP-Datenmodells als Anregung verwenden, um Abfragen für Ihre individuellen Geschäftsanforderungen zu erstellen.

Weitere Informationen zum direkten Anpassen der SQL Ihrer Einblicke über die Platform-Benutzeroberfläche finden Sie in der [SQL-Dokumentation anzeigen](../view-sql.md) .

Die folgenden Einblicke stehen Ihnen als Teil des [Profil-Dashboards](../guides/profiles.md) oder eines benutzerdefinierten [benutzerdefinierten benutzerdefinierten Dashboards](../standard-dashboards.md) zur Verfügung. Anweisungen zum Anpassen Ihres Dashboards oder zum Erstellen und Bearbeiten neuer Widgets ](../customize/custom-widgets.md) in der Widget-Bibliothek und [benutzerdefinierten Dashboards](../standard-dashboards.md#create-widget) finden Sie in der [Übersicht zur Anpassung](../customize/overview.md) .[

## Zielgruppenüberschneidung durch Zusammenführungsrichtlinie {#audience-overlap-by-merge-policy}

Fragen, die durch diesen Einblick beantwortet werden:

- Welche Profile sind für beide Zielgruppen gemeinsam?
- Wie wirkt sich die Überschneidung auf Interaktion oder Konversionsraten aus?
- Wie können Marketingstrategien auf das sich überschneidende Segment zugeschnitten werden?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

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

Informationen zum Erscheinungsbild und zur Funktion dieses Einblicks finden Sie in der Dokumentation zum Widget [Zielgruppenüberschneidung nach Zusammenführungsrichtlinie](../guides/profiles.md#audience-overlap-by-merge-policy) .

## Bericht zur Zielgruppenüberschneidung {#audience-overlap-report}

Fragen, die durch diesen Einblick beantwortet werden:

- Welche 50 Zielgruppen überschneiden sich am meisten?
- Was sind die 50 am wenigsten überlappenden Zielgruppen?
- Wie ändert sich das sich überschneidende Muster durch die Zusammenführungsrichtlinie?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

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

Informationen zum Erscheinungsbild und zur Funktion dieses Einblicks finden Sie in der Dokumentation zum Bericht &quot;Zielgruppenüberschneidung&quot;](../guides/profiles.md#audience-overlap-report) .[

## Zielgruppen (Anzahl) {#audiences}

Fragen, die durch diesen Einblick beantwortet werden:

- Welche Zusammenführungsrichtlinie wird hauptsächlich für die Segmentierung verwendet?
- Wie werden Zielgruppen über Zusammenführungsrichtlinien verteilt?
- Gibt es im Laufe der Zeit signifikante Änderungen an den Zielgruppennummern für bestimmte Zusammenführungsrichtlinien?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

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

Informationen zum Erscheinungsbild und zur Funktion dieses Einblicks finden Sie in der Dokumentation zum [Zielgruppen-Widget](../guides/profiles.md#audiences) .

## Zielgruppen, die dem Zielstatus zugeordnet sind {#audiences-mapped-to-destination-status}

Fragen, die durch diesen Einblick beantwortet werden:

- Wie verteilt sich die Zielgruppe insgesamt auf zugeordnete und nicht zugeordnete Ziele?
- Welche spezifischen Ziele haben die höchste Anzahl gemappter Zielgruppen?
- Welcher Anteil der Gesamtzielgruppen ist noch nicht zugeordnet?
- Gibt es von diesen nicht zugeordneten Zielgruppen Muster oder verknüpfte Trends?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

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

Informationen zum Erscheinungsbild und zur Funktionalität dieses Einblicks finden Sie in der Dokumentation zum Widget [Zielgruppen, die dem Zielstatus-Widget zugeordnet sind](../guides/profiles.md#audiences-mapped-to-destination-status) .

## Zielgruppengröße {#audiences-size}

Fragen, die durch diesen Einblick beantwortet werden:

- Welches Zielgruppensegment hat die größte Größe?
- Was sind die fünf größten Zielgruppen?
- Wie ändert sich die Verteilung der Zielgruppengröße im Laufe der Zeit für die höchste Zielgruppe?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

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

Informationen zum Erscheinungsbild und zur Funktion dieses Einblicks finden Sie in der Dokumentation zum Widget [Größe von Zielgruppen](../guides/profiles.md#audiences-size) .

## Kunden-KI – Verteilung der Scores {#customer-ai-distribution-of-scores}

Fragen, die durch diesen Einblick beantwortet werden:

- Wie verteilt sich die Punktzahl auf Behälter für jedes meiner Customer AI-Modelle?
- Wie verteilt sich die Punktzahl nach hohen, mittleren und niedrigen Werten?
- Wie schlüsselt sich die Scoring-Verteilung nach Zusammenführungsrichtlinien auf?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

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

Informationen zum Erscheinungsbild und zur Funktionalität dieses Einblicks finden Sie in der Dokumentation zur [Verteilung von Bewertungen-Widgets durch Kunden-KI](../guides/profiles.md#customer-ai-distribution-of-scores) .

## Zusammenfassung der KI-Kundenbewertung {#customer-ai-scoring-summary}

Fragen, die durch diesen Einblick beantwortet werden:

- Wie lautet die Bewertungszusammenfassung für jedes meiner Customer AI-Modelle?
- Wie ändern sich die Tendenzwerte meiner Customer AI für verschiedene Zielgruppen?
- Wie ändert sich meine Bewertungszusammenfassung im Vergleich zu anderen KPIs in der Profilübersicht?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

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

Weitere Informationen zum Erscheinungsbild und zur Funktion dieses Einblicks finden Sie in der Dokumentation zum Widget [Customer AI Scoring summary](../guides/profiles.md#customer-ai-scoring-summary) .

## Identitätsüberschneidung {#identity-overlap}

Fragen, die durch diesen Einblick beantwortet werden:

- Was ist die gemeinsame Schnittmenge zwischen [!UICONTROL Identitätstyp A] und [!UICONTROL Identitätstyp B]?
- Wie kann ich Kundenzielgruppen auf der Grundlage der Überschneidung bestimmter Identitätstypen einschränken, um zielgerichtete Marketing-Strategien zu verbessern?
- Welche Erkenntnisse lassen sich aus der Bewertung der Kampagnenleistung in den sich überschneidenden Bereichen gewinnen?
- Wie können zukünftige Marketing-Maßnahmen mithilfe dieses Einblicks zur Kampagnenleistung optimiert werden?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

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

Informationen zum Erscheinungsbild und zur Funktion dieses Einblicks finden Sie in der Dokumentation zum Widget [Identitätsüberschneidung](../guides/profiles.md#identity-overlap) .

## Anzahl der Profile {#profile-count}

Fragen, die durch diesen Einblick beantwortet werden:

- Wie hoch ist die Gesamtanzahl der Profile in der Adobe Real-time Customer Data Platform?
- Wie werden Profile basierend auf Zusammenführungsrichtlinien verteilt?
- Welche Zusammenführungsrichtlinie hat die höchste Profilanzahl?

Das SQl, das diese Einblicke generiert, lautet wie folgt:

```sql
SELECT qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name,
       sum(qsaccel.profile_agg.adwh_fact_profile.count_of_profiles) CNT
  FROM qsaccel.profile_agg.adwh_fact_profile
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_id=adwh_fact_profile.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile.date_key='2024-01-10'
    AND qsaccel.profile_agg.adwh_fact_profile.merge_policy_id = 2027892989
  GROUP BY qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name;
```

Vollständige Informationen zum Erscheinungsbild und zur Funktionalität dieses Einblicks finden Sie im Widget [Profilanzahl](https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/profiles.html#profile-count) .

Informationen zum Erscheinungsbild und zur Funktion dieses Einblicks finden Sie in der Dokumentation zum Widget [Profilanzahl .](../guides/profiles.md#profile-count)

## Änderung der Profilanzahl {#profile-count-change}

Fragen, die durch diesen Einblick beantwortet werden:

- Wie sieht der Trend bei den Änderungen der Gesamtanzahl der Profile aus?
- Was verursachte signifikante Spitzen oder Rückgänge bei der Profilanzahl?
- Gibt es bestimmte Zusammenführungsrichtlinien, die die Änderung der Profilanzahl bewirken?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

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

Informationen zum Erscheinungsbild und zur Funktion dieses Einblicks finden Sie in der Dokumentation zum Widget [Änderung der Profilanzahl](../guides/profiles.md#profile-count-change) .

## Trend zur Änderung der Profilanzahl {#profile-count-change-trend}

Fragen, die durch diesen Einblick beantwortet werden:

- Wie hat sich der allgemeine Trend bei der Profilzählung in den letzten 12 Monaten basierend auf der Zusammenführungsrichtlinie verändert?
- Gibt es innerhalb der letzten 30 Tage spezifische Muster oder Schwankungen bei der Profilanzahl, die beachtet werden müssen?
- Wie ändert sich die Anzahl der Profile in den letzten 90 Tagen im Vergleich zum allgemeinen Trend?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

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

Informationen zum Erscheinungsbild und zur Funktionalität dieses Einblicks finden Sie in der Dokumentation zum Widget [Trends bei Profilzählung ändern](../guides/profiles.md#profile-count-change-trend) .

## Entwicklung der Profilanzahl {#profile-count-trend}

Fragen, die durch diesen Einblick beantwortet werden:

- Wie lautet der allgemeine Trend bei der Profilzählung basierend auf der Zusammenführungsrichtlinie in den letzten 30 Tagen?
- Wie lässt sich dieser Trend mit den längerfristigen Trends (z. B. 90 Tage und 12 Monate) vergleichen?
- Welche Zusammenführungsrichtlinie trägt am meisten zur Erhöhung oder Verringerung der Profilanzahl in den angegebenen Zeiträumen (30 Tage, 90 Tage und 12 Monate) bei?
- Gibt es bestimmte Spitzen oder Rückgänge bei der Profilanzahl, die innerhalb des 30-Tage-Zeitraums mit bestimmten Ereignissen oder Zeiträumen korrelieren?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

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

Informationen zum Erscheinungsbild und zur Funktion dieses Einblicks finden Sie in der Dokumentation zum Widget zum Trend der Profilanzahl [Profil-Anzahl .](../guides/profiles.md#profile-count-trend)

## Profile nach Identität {#profiles-by-identity}

Fragen, die durch diesen Einblick beantwortet werden:

- Welcher Identitätstyp weist unter den Profilen insgesamt einen höheren Anteil auf?
- Gibt es erhebliche Unterschiede zwischen den Identitätstypen?
- Wie verteilt sich die Identität insgesamt?
- Gibt es wesentliche Unterschiede oder Anomalien bei den Identitätszahlen?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

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

Informationen zum Erscheinungsbild und zur Funktion dieses Einblicks finden Sie in der Dokumentation zum [Profile nach Identitäts-Widget](../guides/profiles.md#profiles-by-identity) .

## Trend der Änderung der Profilanzahl {#profiles-count-change-trend}

Fragen, die durch diesen Einblick beantwortet werden:

- Wie sieht der allgemeine Trend bei der Veränderung der Profilanzahl in den letzten 12 Monaten aus, basierend auf der Zusammenführungsrichtlinie?
- Gibt es bestimmte Muster oder Schwankungen bei der Änderung der Profilanzahl in den letzten 30 Tagen, die beachtet werden müssen?
- Wie lässt sich die Veränderung der Profilanzahl in den letzten 90 Tagen mit dem Gesamttrend vergleichen?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

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

Informationen zum Erscheinungsbild und zur Funktionalität dieses Einblicks finden Sie in der Dokumentation zum Trend-Widget ](../guides/profiles.md#profiles-count-change-trend) zur Änderung der Profilanzahl.[

## Trend zur Änderung der Profilanzahl nach Identität {#profiles-count-change-trend-by-identity}

Fragen, die durch diesen Einblick beantwortet werden:

- Welchen allgemeinen Trend hat es in den letzten 12 Monaten bei der Veränderung der Profilanzahl verschiedener Identitäten gegeben?
- Gibt es bestimmte Identitätstrends, die innerhalb der letzten 30 Tage signifikante Änderungen zeigen?
- Wie unterscheiden sich die Änderungen in der Profilanzahl beim Vergleich der 30-Tage-, 90-Tage- und 12-Monats-Trends für eine bestimmte Identität?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

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

Informationen zum Erscheinungsbild und zur Funktionalität dieses Einblicks finden Sie in der Dokumentation zum Thema [Trends zur Änderung der Profilanzahl nach Identitäts-Widget](../guides/profiles.md#profiles-count-change-trend-by-identity) .

## Einzelne Identitätsprofile {#single-identity-profiles}

Fragen, die durch diesen Einblick beantwortet werden:

- Werden meine Kundenidentitätsdaten konsistent mit einzelnen Identitäten dargestellt?
- Welcher Prozentsatz meiner Benutzerbasis besteht aus Profilen mit nur einem Identitätstyp?
- Wie wirkt sich dies auf die Vollständigkeit des Profils von nur einem Identitätstyp aus?
- Besteht eine Korrelation zwischen dem am häufigsten verwendeten Identitätstyp und der Anzahl einzelner Identitätsprofile?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

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

Informationen zum Erscheinungsbild und zur Funktion dieses Einblicks finden Sie in der Dokumentation zum Widget [Einzelidentitätsprofile](../guides/profiles.md#single-identity-profiles) .

## Einzelne Identitätsprofile nach Identität {#single-identity-profiles-by-identity}

Fragen, die durch diesen Einblick beantwortet werden:

- Wie viele Unique Customers haben sich mit einer einzigen Identität registriert (z. B. E-Mail- oder Telefonnummer)?
- Wie werden einzelne Identitätsprofile unter verschiedenen Identitätstypen verteilt, z. B. E-Mail- oder Telefonnummern?
- Gibt es aufstrebende Identitätsmuster oder Verschiebungen innerhalb der einzelnen Identitätsprofile?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

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

Informationen zum Erscheinungsbild und zur Funktionalität dieses Einblicks finden Sie in der Dokumentation zu [Einzelne Identitätsprofile nach Identitäts-Widget](../guides/profiles.md#single-identity-profiles-by-identity) .

## Nicht segmentierte Profile {#unsegmented-profiles}

Fragen, die durch diesen Einblick beantwortet werden:

- Wie viele Profile sind nicht Teil einer Zielgruppe?
- Welcher Prozentsatz der Gesamtzielgruppe wird durch nicht segmentierte Profile repräsentiert?
- Beitragen Zusammenführungsrichtlinien zu einer großen Anzahl nicht segmentierter Profile?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

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

Informationen zum Erscheinungsbild und zur Funktion dieses Einblicks finden Sie in der Dokumentation zum Widget [Nicht segmentierte Profile](../guides/profiles.md#unsegmented-profiles) .

## Nächste Schritte

Durch Lesen dieses Dokuments verstehen Sie jetzt die SQL-Datenbank, die Dashboard-Einblicke generiert, und welche häufig gestellten Fragen diese Analyse löst. Jetzt können Sie die SQL bearbeiten und iterieren, um Ihre eigenen Einblicke zu generieren.

Weitere Informationen zum direkten Anpassen der SQL Ihrer Einblicke über die PLatform-Benutzeroberfläche finden Sie in der [SQL-Dokumentation anzeigen](../view-sql.md) .

Sie können auch die SQL lesen und verstehen, die Einblicke in die Dashboards [Zielgruppen](./audiences.md), [Kontoprofile](./account-profiles.md) und [Ziele](./destinations.md) generiert.
