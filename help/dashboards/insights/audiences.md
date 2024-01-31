---
title: Audiences Insights
description: Entdecken Sie die SQL, die Ihre Zielgruppeneinblicke ermöglicht und nutzen Sie diese Abfragen, um benutzerdefinierte Einblicke zu generieren und Zielgruppendaten aus Adobe Experience Platform weiter zu untersuchen.
source-git-commit: ee9ef2cf777c72fbd19cfccd80a37ea66591216d
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 1%

---

# Einblicke in Zielgruppen

Die aus der Analyse Ihres Datenmodells gewonnenen Erkenntnisse machen Ihre Adobe Real-time Customer Data Platform-Daten leichter zugänglich, verständlich und für die Entscheidungsfindung wirkungsvoll.

Machen Sie sich mit den Einblicken Ihrer Zielgruppe vertraut, indem Sie auf die SQL zugreifen, über die diese Benutzer verfügen, und dann Ihre eigenen Einblicke generieren, um die Identitäten und Profile Ihrer Zielgruppen weiter zu untersuchen. Transformieren Sie Ihre Rohdaten in neue umsetzbare Einblicke, indem Sie die vorhandene SQL des Real-Time CDP-Datenmodells als Anregung verwenden, um Abfragen für Ihre individuellen Geschäftsanforderungen zu erstellen.

<!-- This link will go in during the January release.
See the [View SQL documentation]() for more information on how to adapt your insights' SQL directly through the PLatform UI.  -->

Die folgenden Einblicke stehen Ihnen als Teil der [Zielgruppen-Dashboard](../guides/audiences.md) oder benutzerdefiniert [Benutzerdefiniertes Dashboard](../user-defined-dashboards.md). Siehe [Anpassungsübersicht](../customize/overview.md) Anweisungen zum Anpassen Ihres Dashboards erhalten Sie oder [Erstellen und Bearbeiten neuer Widgets](../customize/custom-widgets.md) in der Widget-Bibliothek und [Benutzerdefiniertes Dashboard](../user-defined-dashboards.md#create-widget).

Die folgenden Einblicke stehen Ihnen als Teil der [Zielgruppen-Dashboard](../guides/audiences.md) oder ein benutzerdefiniertes Dashboard.

## Bericht &quot;Zielgruppenüberschneidung&quot; {#audience-overlap-report}

Fragen, die durch diesen Einblick beantwortet werden:

- Was sind die 50 am häufigsten überlappenden Zielgruppen einer bestimmten gefilterten Zielgruppe?
- Was sind die 50 am wenigsten überlappenden Zielgruppen einer bestimmten gefilterten Zielgruppe?
- Wie ändert sich das überlappende Muster für eine andere gefilterte Zielgruppe?

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

Siehe [Dokumentation zum Bericht-Widget &quot;Zielgruppenüberschneidung&quot;](../guides/audiences.md#audience-overlap-report) für Informationen über das Erscheinungsbild und die Funktionalität dieses Einblicks.

## Zielgruppenüberschneidung {#audience-overlap}

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

Siehe [Dokumentation zum Widget &quot;Zielgruppenüberschneidung&quot;](../guides/audiences.md#audience-overlap) für Informationen über das Erscheinungsbild und die Funktionalität dieses Einblicks.

## Trend zur Änderung der Zielgruppengröße {#audience-size-change-trend}

Fragen, die durch diesen Einblick beantwortet werden:

- Gibt es innerhalb der letzten 30 Tage, 90 Tage oder 12 Monate signifikante Spitzen oder Tiefpunkte in der Zielgruppengröße?
- Wie ändert sich die Zielgruppengröße an bestimmten Tagen?
- Gab es in den letzten 12 Monaten Anomalien oder sich wiederholende Anomalien bei Spitzen oder Tiefgängen?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

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

Siehe [Dokumentation zum Trend-Widget zur Änderung der Zielgruppengröße](../guides/audiences.md#audience-size-change-trend) für Informationen über das Erscheinungsbild und die Funktionalität dieses Einblicks.

## Trend zur Zielgruppengröße nach Identität {#audience-size-trend-by-identity}

Fragen, die durch diesen Einblick beantwortet werden:

- Steigt, stabilisiert oder erfährt meine Zielgruppe ständig Schwankungen?
- Gibt es eine bestimmte Identität, die im Laufe der Zeit zu Spitzen oder Verwerfungen beim Zielgruppenwachstum führt?
- Gibt es Abweichungen in meinem Identitätswachstum im Zeitverlauf?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

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

Siehe [Trend zur Zielgruppengröße nach Dokumentation des Identitäts-Widgets](../guides/audiences.md#audience-size-trend-by-identity) für Informationen über das Erscheinungsbild und die Funktionalität dieses Einblicks.

## Trend der Zielgruppen-Größe {#audience-size-trend}

Fragen, die durch diesen Einblick beantwortet werden:

- Wie hat sich die Zielgruppengröße im Laufe der Zeit verändert, einschließlich etwaiger Anomalien?
- Wie finde ich den Gesamttrend der Zielgruppengröße über die Zeiträume: 30 Tage, 90 Tage und 12 Monate?
- Welche Hauptmerkmale haben die Zielgruppe, die zu ihrer Größe beitragen? Beispielsweise Spitzen aufgrund von E-Mail-Marketing-Kampagnen.

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

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

Siehe [Dokumentation zum Widget zum Trend der Zielgruppengröße](../guides/audiences.md#audience-size-trend) für Informationen über das Erscheinungsbild und die Funktionalität dieses Einblicks.

## Zielgruppengröße {#audience-size}

Fragen, die durch diesen Einblick beantwortet werden:

- Wie groß ist die aktuelle Gesamtzielgruppe?
- Wie unterscheidet sich die Größe der aktuellen Zielgruppe von früheren Zeiträumen oder bestimmten Zielgruppen?
- Welche Auswirkungen haben aktuelle Marketing-Kampagnen auf die Zielgruppengröße?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

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

Siehe [Dokumentation zum Widget &quot;Zielgruppengröße&quot;](../guides/audiences.md#audience-size) für Informationen über das Erscheinungsbild und die Funktionalität dieses Einblicks.

## Customer AI-Verteilung von Bewertungen {#customer-ai-distribution-of-scores}

Fragen, die durch diesen Einblick beantwortet werden:

- Was ist die Scoring-Verteilung für jeden Behälter meines Customer AI-Modells, der von einer ausgewählten Zielgruppe gefiltert wurde?
- Was ist die Scoring-Verteilung von &quot;Hoch&quot;, &quot;Mittel&quot;und &quot;Niedrig&quot;für eine bestimmte Zielgruppe?
- Wie schlüsselt sich die Verteilung der Scoring-Daten nach verschiedenen Zielgruppen auf?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

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

Siehe [Dokumentation zum Widget zur Verteilung von Bewertungen für Customer AI](../guides/audiences.md#customer-ai-distribution-of-scores) für Informationen über das Erscheinungsbild und die Funktionalität dieses Einblicks.

## Customer AI-Bewertungszusammenfassung {#customer-ai-scoring-summary}

Fragen, die durch diesen Einblick beantwortet werden:

- Wie lautet die Bewertungszusammenfassung für jedes meiner Customer AI-Modelle für eine bestimmte Zielgruppe?
- Wie ändern sich die Tendenzwerte meiner Customer AI für verschiedene Zielgruppen?
- Wie unterscheidet sich meine Bewertungszusammenfassung von den anderen KPIs in der Zielgruppenübersicht?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

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

Siehe [Dokumentation zum Widget zum Customer AI-Scoring](../guides/audiences.md#customer-ai-scoring-summary) für Informationen über das Erscheinungsbild und die Funktionalität dieses Einblicks.

## Identitätsüberschneidung {#identity-overlap}

Fragen, die durch diesen Einblick beantwortet werden:

- Was ist die gemeinsame Schnittmenge zwischen [!UICONTROL Identitätstyp A] und [!UICONTROL Identitätstyp B] für eine gefilterte Zielgruppe?
- Wie kann ich Kundenzielgruppen auf der Grundlage der Überschneidung bestimmter Identitätstypen einschränken, um die zielgerichteten Marketing-Strategien zu verbessern?
- Welche Erkenntnisse lassen sich aus der Bewertung der Kampagnenleistung in den sich überschneidenden Bereichen gewinnen?
- Wie können zukünftige Marketing-Maßnahmen anhand dieser Einblicke optimiert werden?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

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

Siehe [Dokumentation zum Widget zur Identitätsüberschneidung](../guides/audiences.md#identity-overlap) für Informationen über das Erscheinungsbild und die Funktionalität dieses Einblicks.

## Profile nach Identität {#profiles-by-identity}

Fragen, die durch diesen Einblick beantwortet werden:

- Welcher Identitätstyp hat den höchsten Anteil innerhalb der Gesamtzahl der Profile für eine ausgewählte Zielgruppe?
- Gibt es erhebliche Unterschiede zwischen den Identitätstypen für eine ausgewählte Zielgruppe?
- Wie verteilt sich die Gesamtheit der Identitätstypen nach Zielgruppe?
- Gibt es signifikante Unterschiede oder Anomalien bei den Identitätszahlen für verschiedene Zielgruppen?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

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

Siehe [Dokumentation zu Profilen nach Identitäts-Widgets](../guides/audiences.md#profiles-by-identity) für Informationen über das Erscheinungsbild und die Funktionalität dieses Einblicks.

## Geplante Aktivierungen {#scheduled-activations}

Fragen, die durch diesen Einblick beantwortet werden:

- Wie lauten die Start- und Enddaten der leistungsstärksten Aktivierungen für eine bestimmte Zielgruppe auf einer bestimmten Plattform?
- Welche Plattformen wurden am häufigsten für geplante Aktivierungen einer bestimmten Zielgruppe verwendet?
- Gibt es irgendwelche Muster bei der Plattformnutzung, die Entscheidungen über die Priorisierung oder Diversifizierung von Aktivierungsstrategien für eine bestimmte Zielgruppe leiten könnten?

+++Auswählen, um die SQL anzuzeigen, die diesen Einblick generiert

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

Siehe [Dokumentation zum Widget zu geplanten Aktivierungen](../guides/audiences.md#scheduled-activations) für Informationen über das Erscheinungsbild und die Funktionalität dieses Einblicks.

## Nächste Schritte

Durch Lesen dieses Dokuments verstehen Sie jetzt die SQL-Datenbank, die Dashboard-Einblicke generiert, und welche häufig gestellten Fragen diese Analyse löst. Jetzt können Sie die SQL bearbeiten und iterieren, um Ihre eigenen Einblicke zu generieren.

<!-- This link will go in during the January release.
See the [View SQL documentation]() for more information on how to adapt your insights' SQL directly through the PLatform UI. -->

Sie können auch die SQL lesen und verstehen, die Einblicke für die [Profile](./profiles.md) und [Ziele](./destinations.md) Dashboards.
