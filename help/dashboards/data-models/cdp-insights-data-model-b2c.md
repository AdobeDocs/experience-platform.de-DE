---
title: Real-time Customer Data Platform Insights-Datenmodell B2C Edition
description: Erfahren Sie, wie Sie mit den Real-time Customer Data Platform Insights-Datenmodellen (B2C Edition) SQL-Abfragen verwenden können, um Ihre eigenen Real-Time CDP-Berichte für Ihre Marketing- und KPI-Anwendungsfälle anzupassen.
badgeB2B: label="B2B Edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
badgeB2P: label="B2P Edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 61bc7f23-9f79-4c75-a515-85dd9dda2d02
source-git-commit: ddf886052aedc025ff125c03ab63877cb049583d
workflow-type: tm+mt
source-wordcount: '1155'
ht-degree: 1%

---

# Real-time Customer Data Platform Insights-Datenmodell B2C Edition

Das Real-time Customer Data Platform Insights-Datenmodell für die [B2C Edition](../../rtcdp/overview.md#rtcdp-b2c) stellt die Datenmodelle und SQL bereit, die die Einblicke für verschiedene Profil-, Ziel- und Segmentierungswidgets nutzen. Sie können diese SQL-Abfragevorlagen anpassen, um Real-Time CDP-Berichte für Ihre Marketing- und KPI-Anwendungsfälle (Key Performance Indicators) zu erstellen. Diese Insights können dann als benutzerdefinierte Widgets für benutzerdefinierte Dashboards verwendet werden. Informationen zum Erstellen eines Berichtseinblicks-Datenmodells mit Berichtseinblicken über Query Service für die Verwendung mit beschleunigten Speicherdaten und benutzerdefinierten Dashboards finden Sie in der Dokumentation zu Query Accelerated Store Reporting Insights](../../query-service/data-distiller/sql-insights/reporting-insights-data-model.md) .[

>[!NOTE]
>
>Der Begriff &quot;Segment&quot;wurde in allen Adobe Experience Platform-Systemen auf &quot;Zielgruppe&quot;aktualisiert. Einige Verweise auf Segmente werden weiterhin für Dateipfade und Datensatzbenennungskonventionen verwendet.

## Voraussetzungen

Dieses Handbuch setzt ein Verständnis der [benutzerdefinierten Dashboards-Funktion](../standard-dashboards.md) voraus. Lesen Sie die Dokumentation , bevor Sie mit diesem Handbuch fortfahren.

## Real-Time CDP Insight-Berichte und Anwendungsfälle

Real-Time CDP Reporting bietet Einblicke in Ihre Profildaten und ihre Beziehung zu Zielgruppen und Zielen. Verschiedene Sternschema-Modelle wurden entwickelt, um eine Vielzahl gängiger Marketing-Anwendungsfälle zu beantworten. Jedes Datenmodell kann mehrere Anwendungsfälle unterstützen.

>[!IMPORTANT]
>
>Die für die Real-Time CDP-Berichterstellung verwendeten Daten sind für eine bestimmte Zusammenführungsrichtlinie und aus der letzten täglichen Momentaufnahme korrekt.

### Profilmodell {#profile-model}

Das Profilmodell besteht aus drei Datensätzen:

- `adwh_dim_date`
- `adwh_fact_profile`
- `adwh_dim_merge_policies`

Die folgende Abbildung enthält die relevanten Datenfelder in jedem Datensatz.

![Eine ERD des Profilmodells.](../images/cdp-insights/profile-model.png)

#### Anwendungsfall für die Profilanzahl {#profile-count}

Die für das Widget [!UICONTROL Profilanzahl] verwendete Logik gibt die Gesamtzahl der zusammengeführten Profile im Profilspeicher zum Zeitpunkt der Momentaufnahme zurück. Weitere Informationen finden Sie in der Dokumentation zum Widget [[!UICONTROL Profilanzahl]](../guides/profiles.md#profile-count) .

Die SQL, die das Widget [!UICONTROL Profilanzahl] generiert, wird im ausblendbaren Abschnitt unten angezeigt.

+++SQL-Abfrage

```sql
SELECT qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name,
       sum(qsaccel.profile_agg.adwh_fact_profile.count_of_profiles) CNT
  FROM qsaccel.profile_agg.adwh_fact_profile
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_id=adwh_fact_profile.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile.date_key='2024-01-10'
    AND qsaccel.profile_agg.adwh_fact_profile.merge_policy_id = 2027892989
  GROUP BY qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name;
```

+++

#### Anwendungsfall für einzelne Identitätsprofile {#single-identity-profiles}

Die für das Widget [!UICONTROL Einzelne Identitätsprofile] verwendete Logik liefert die Anzahl der Profile Ihres Unternehmens, die nur über einen ID-Typ verfügen, der ihre Identität erstellt. Weitere Informationen finden Sie in der Dokumentation zum Widget [[!UICONTROL Einzelne Identitätsprofile]](../guides/profiles.md#single-identity-profiles) .

Die SQL, die das Widget [!UICONTROL Single identity profiles] generiert, wird im unten stehenden ausblendbaren Abschnitt angezeigt.

+++SQL-Abfrage

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

### Namespace-Modell {#namespace-model}

Das Namespace-Modell besteht aus den folgenden Datensätzen:

- `adwh_dim_date`
- `adwh_fact_profile_by_namespace`
- `adwh_dim_merge_policies`
- `adwh_dim_namespaces`

Die folgende Abbildung enthält die relevanten Datenfelder in jedem Datensatz.

![Ein ERD des Namespace-Modells.](../images/cdp-insights/namespace-model.png)

#### Profile nach Identitätsanwendungsfall {#profiles-by-identity}

Das Widget [!UICONTROL Profile nach Identität] zeigt die Aufschlüsselung der Identitäten für alle zusammengeführten Profile in Ihrem Profilspeicher an. Weitere Informationen finden Sie in der Dokumentation zum Widget [[!UICONTROL Profile nach Identität]](../guides/profiles.md#profiles-by-identity) .

Die SQL, die das Widget [!UICONTROL Profile nach Identität] generiert, wird im unten stehenden ausblendbaren Abschnitt angezeigt.

+++SQL-Abfrage

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

#### Einzelne Identitätsprofile nach Identitätsanwendungsfall {#single-identity-profiles-by-identity}

Die Logik, die für das Widget [!UICONTROL Einzelne Identitätsprofile nach Identität] verwendet wird, zeigt die Gesamtanzahl der Profile, die mit nur einer eindeutigen Kennung identifiziert werden. Weitere Informationen finden Sie in der Dokumentation zu [Einzelne Identitätsprofile nach Identitäts-Widget](../guides/profiles.md#single-identity-profiles-by-identity) .

Die SQL, die das Widget [!UICONTROL Einzelne Identitätsprofile nach Identität] generiert, wird im unten stehenden ausblendbaren Abschnitt angezeigt.

+++SQL-Abfrage

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

### Zielgruppenmodell {#audience-model}

Das Zielgruppenmodell besteht aus den folgenden Datensätzen:

- `adwh_dim_date`
- `adwh_fact_profile_by_segment`
- `adwh_dim_merge_policies`
- `adwh_dim_segments`
- `adwh_dim_br_segment_destinations`
- `adwh_dim_destination`
- `adwh_dim_destination_platform`

Die folgende Abbildung enthält die relevanten Datenfelder in jedem Datensatz.

![Eine ERD des Zielgruppenmodells.](../images/cdp-insights/audience-model.png)

#### Anwendungsfall: Zielgruppengröße {#audience-size}

Die für das Widget [!UICONTROL Zielgruppengröße] verwendete Logik gibt die Gesamtzahl der zusammengeführten Profile innerhalb der ausgewählten Zielgruppe zum Zeitpunkt der letzten Momentaufnahme zurück. Weitere Informationen finden Sie in der Dokumentation zum Widget [[!UICONTROL Zielgruppengröße]](../guides/audiences.md#audience-size) .

Die SQL, die das Widget [!UICONTROL Zielgruppengröße] generiert, wird im unten stehenden ausblendbaren Abschnitt angezeigt.

+++SQL-Abfrage

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

#### Anwendungsfall zur Änderung der Zielgruppengröße {#audience-size-change-trend}

Die Logik, die für das Widget [!UICONTROL Trend zur Änderung der Zielgruppengröße] verwendet wird, liefert eine Kantengrafik, die den Unterschied zwischen der Gesamtanzahl der Profile veranschaulicht, die sich für eine bestimmte Zielgruppe zwischen den letzten täglichen Momentaufnahmen qualifizieren. Weitere Informationen finden Sie in der Dokumentation zum Widget [[!UICONTROL Trend zur Änderung der Zielgruppengröße]](../guides/audiences.md#audience-size-change-trend) .

Die SQL, die das Widget [!UICONTROL Trend zur Änderung der Zielgruppengröße] generiert, wird im unten stehenden ausblendbaren Abschnitt angezeigt.

+++SQL-Abfrage

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

#### Anwendungsfall für die am häufigsten verwendeten Ziele {#most-used-destinations}

Die im Widget [!UICONTROL Bevorzugte Ziele] verwendete Logik listet die am häufigsten verwendeten Ziele Ihrer Organisation entsprechend der Anzahl der ihnen zugeordneten Zielgruppen auf. Dieses Ranking bietet Einblicke, welche Ziele verwendet werden, und zeigt möglicherweise auch diejenigen, die möglicherweise nicht genutzt werden. Weitere Informationen finden Sie in der Dokumentation zum Widget [[!UICONTROL Am häufigsten verwendete Ziele] .](../guides/destinations.md#most-used-destinations)

Die SQL, die das Widget [!UICONTROL Bevorzugte Ziele] generiert, wird im ausblendbaren Abschnitt unten angezeigt.

+++SQL-Abfrage

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

#### Anwendungsfall für kürzlich aktivierte Zielgruppen {#recently-activated-audiences}

Die Logik für das Widget [!UICONTROL Zuletzt aktivierte Zielgruppen] enthält eine Liste der Zielgruppen, die zuletzt einem Ziel zugeordnet wurden. Diese Liste enthält eine Momentaufnahme der Zielgruppen und Ziele, die aktiv im System verwendet werden, und kann bei der Fehlerbehebung bei fehlerhaften Zuordnungen helfen. Weitere Informationen finden Sie in der Dokumentation zum Widget [[!UICONTROL Zuletzt aktivierte Zielgruppen] .](../guides/destinations.md#recently-activated-audiences)

Die SQL, die das Widget [!UICONTROL Zuletzt aktivierte Zielgruppen] generiert, wird im unten stehenden ausblendbaren Abschnitt angezeigt.

+++SQL-Abfrage

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

### Namespace-Audience-Modell {#namespace-audience-model}

Das Modell namespace-audience besteht aus den folgenden Datensätzen:

- `adwh_dim_date`
- `adwh_dim_namespaces`
- `adwh_fact_profile_by_segment_and_namespace`
- `adwh_dim_merge_policies`
- `adwh_dim_segments`
- `adwh_dim_br_segment_destinations`
- `adwh_dim_destination`
- `adwh_dim_destination_platform`

Die folgende Abbildung enthält die relevanten Datenfelder in jedem Datensatz.

![Ein ERD des Namespace-Audience-Modells.](../images/cdp-insights/namespace-audience-model.png)

#### Profile nach Identität für einen Zielgruppen-Anwendungsfall {#audience-profiles-by-identity}

Die im Widget [!UICONTROL Profile nach Identität] verwendete Logik bietet eine Aufschlüsselung der Identitäten über alle zusammengeführten Profile in Ihrem Profilspeicher für eine bestimmte Zielgruppe hinweg. Weitere Informationen finden Sie in der Dokumentation zum Widget [[!UICONTROL Profile nach Identität]](../guides/audiences.md#profiles-by-identity) .

Die SQL, die das Widget [!UICONTROL Profile nach Identität] generiert, wird im unten stehenden ausblendbaren Abschnitt angezeigt.

+++SQL-Abfrage

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

### Überlagern eines Namespace-Modells

Das Überschneidungs-Namespace-Modell besteht aus den folgenden Datensätzen:

- `adwh_dim_date`
- `adwh_dim_overlap_namespaces`
- `adwh_fact_profile_overlap_of_namespace`
- `adwh_dim_merge_policies`

Die folgende Abbildung enthält die relevanten Datenfelder in jedem Datensatz.

![Ein ERD des Überschneidungs-Namespace-Modells.](../images/cdp-insights/overlap-namespace-model.png)

#### Anwendungsfall: Identitätsüberschneidung (Profile) {#profiles-identity-overlap}

Die im Widget [!UICONTROL Identitätsüberschneidung] verwendete Logik zeigt die Überschneidung von Profilen in Ihrem **Profilspeicher** an, die die beiden ausgewählten Identitäten enthalten. Weitere Informationen finden Sie im Abschnitt [[!UICONTROL Identitätsüberschneidung] des Widgets [!UICONTROL Profile] Dashboard-Dokumentation](../guides/profiles.md#identity-overlap) .

Die SQL, die das Widget [!UICONTROL Identitätsüberschneidung] generiert, wird im unten stehenden ausblendbaren Abschnitt angezeigt.

+++SQL-Abfrage

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

### Namespace nach Zielgruppenmodell überlagern {#overlap-namespace-by-audience-model}

Der Überschneidungs-Namespace nach Zielgruppenmodell besteht aus den folgenden Datensätzen:

- `adwh_dim_date`
- `adwh_dim_overlap_namespaces`
- `adwh_fact_profile_overlap_of_namespace_by_segment`
- `adwh_dim_merge_policies`
- `adwh_dim_segments`
- `adwh_dim_br_segment_destinations`
- `adwh_dim_destination`
- `adwh_dim_destination_platform`

Die folgende Abbildung enthält die relevanten Datenfelder in jedem Datensatz.

![Ein ERD des Überschneidungs-Namespace nach Zielgruppenmodell.](../images/cdp-insights/overlap-namespace-by-audience-model.png)

#### Anwendungsfall: Identitätsüberschneidung (Zielgruppen) {#audiences-identity-overlap}

Die im Widget [!UICONTROL Zielgruppen] Dashboard [!UICONTROL Identitätsüberschneidung] verwendete Logik zeigt die Überschneidung von Profilen, die die beiden ausgewählten Identitäten für eine bestimmte Zielgruppe enthalten. Weitere Informationen finden Sie im Abschnitt [[!UICONTROL Identitätsüberschneidung] des Widgets [!UICONTROL Zielgruppen] Dashboard-Dokumentation](../guides/audiences.md#identity-overlap) .

Die SQL, die das Widget [!UICONTROL Identitätsüberschneidung] generiert, wird im unten stehenden ausblendbaren Abschnitt angezeigt.

+++SQL-Abfrage

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

<!-- Commented out as Anil wanted to add something but did not provide information yet:
### Overlap Namespace-Audience model {#overlap-namespace-audience-model}

The overlap namespace-audience model is comprised of the following datasets: 

- `adwh_fact_profile_overlap_by_namespace_and_segment`
- `adwh_dim_date`
- `adwh_dim_namespace`
- `adwh_dim_overlap_namespaces`
- `adwh_dim_merge_policies`
- `adwh_dim_segments`
- `adwh_dim_br_segment_destinations`
- `adwh_dim_destination`
- `adwh_dim_destination_platform`

![An ERD of the overlap namespace-audience model.](../images/cdp-insights/overlap-namespace-audience-model.png) -->

<!-- What insights are gathered from this particular data model? -->

<!-- Commented out as Anil wanted to add something but did not provide information yet:
### AI model {#ai-model}

The AI model is comprised of the following datasets: 

- `adwh_fact_profile_ai_models`
- `adwh_dim_date`
- `adwh_dim_merge_policies`
- `adwh_dim_ai_models`

![An ERD of the AI model.](./images/cdp-insights/ai-model.png) -->

<!-- What insights are gathered from this particular data model? -->

