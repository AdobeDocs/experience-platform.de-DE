---
keywords: Einblicke;Zuordnungsai;Zuordnungs-ai-Einblicke;AAI-Abfrage-Dienst;Zuordnungs-Abfragen;Zuordnungswerte
solution: Intelligent Services, Experience Platform
title: Analysieren von Zuordnungswerten mithilfe des Abfrage Service
topic: Attribution AI queries
description: Erfahren Sie, wie Sie mit dem Adobe Experience Platform Abfrage Service Attribution AI-Ergebnisse analysieren können.
translation-type: tm+mt
source-git-commit: eb163949f91b0d1e9cc23180bb372b6f94fc951f
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---


# Analysieren von Zuordnungswerten mithilfe des Abfrage Service

Jede Zeile in den Daten stellt eine Konversion dar, bei der Informationen für verwandte Touchpoints als Strukturarray unter der Spalte `touchpointsDetail` gespeichert werden.

| Touchpoint-Informationen | Spalte |
| ---------------------- | ------ |
| Touchpoint-Name | `touchpointsDetail. touchpointName` |
| Touchpoint-Kanal | `touchpointsDetail.touchPoint.mediaChannel` |
| Algorithmische Ergebnisse des Touchpoint-Attribution AIS | <li>`touchpointsDetail.scores.algorithmicSourced`</li> <li> `touchpointsDetail.scores.algorithmicInfluenced` </li> |

## Suchen von Datenpfaden

Wählen Sie in der Adobe Experience Platform-Benutzeroberfläche in der linken Navigation **[!UICONTROL Datensätze]**. Die Seite **[!UICONTROL Datensätze]** wird angezeigt. Wählen Sie anschließend die Registerkarte **[!UICONTROL Durchsuchen]** und suchen Sie den Ausgabedatensatz für Ihre Attribution AI-Ergebnisse.

![Zugreifen auf Ihre Instanz](./images/aai-query/datasets_browse.png)

Wählen Sie Ihren Ausgabedatensatz aus. Die Seite zur Aktivität des Datensatzes wird angezeigt.

![Dataset-Aktivität](./images/aai-query/select_preview.png)

Wählen Sie auf der Seite &quot;Aktivität des Datensatzes&quot;in der rechten oberen Ecke **[!UICONTROL Vorschau-Datensatz]** aus, um Ihre Daten Vorschau und sicherzustellen, dass sie erwartungsgemäß aufgenommen wurden.

![Vorschau DataSet](./images/aai-query/preview_dataset.JPG)

Wählen Sie nach der Vorschau Ihrer Daten das Schema in der rechten Leiste aus. Es wird ein Popup mit dem Namen und der Beschreibung des Schemas angezeigt. Wählen Sie den Hyperlink &quot;Schema-Name&quot;, um zum bewerteten Schema umzuleiten.

![Schema auswählen](./images/aai-query/select_schema.png)

Mithilfe des Schemas &quot;Bewertung&quot;können Sie einen Wert auswählen oder suchen. Nach der Auswahl wird die Seitenleiste **[!UICONTROL Feldeigenschaften]** geöffnet, damit Sie den Pfad kopieren können, der zum Erstellen von Abfragen verwendet werden soll.

![den Pfad kopieren](./images/aai-query/copy_path.png)

## Abfrage-Dienst aufrufen

Um von der Plattformbenutzeroberfläche aus auf den Abfrage-Dienst zuzugreifen, wählen Sie im Beginn **[!UICONTROL Abfragen]** in der linken Navigation und dann die Registerkarte **[!UICONTROL Durchsuchen]**. Eine Liste der zuvor gespeicherten Abfragen wird geladen.

![Durchsuchen des Abfrage-Dienstes](./images/aai-query/query_tab.png)

Wählen Sie dann **[!UICONTROL Abfrage]** oben rechts aus. Der Abfragen-Editor wird geladen. Mit dem Abfragen-Editor können Sie mit der Erstellung von Abfragen mit Ihren Bewertungsdaten beginnen.

![Abfrage-Editor](./images/aai-query/query_example.png)

Weitere Informationen zum Abfragen-Editor finden Sie im Benutzerhandbuch [Abfrage-Editor](../../query-service/ui/user-guide.md).

## Abfrage-Vorlagen für die Analyse des Zuordnungswerts

Die folgenden Abfragen können als Vorlage für verschiedene Score-Analysen verwendet werden. Sie müssen die Werte `_tenantId` und `your_score_output_dataset` durch die entsprechenden Werte in Ihrem bewerteten Schema ersetzen.

>[!NOTE]
>
> Je nachdem, wie Ihre Daten erfasst wurden, können die unten verwendeten Werte wie `timestamp` in einem anderen Format verwendet werden.

### Überprüfungsbeispiele

**Gesamtanzahl der Konversionen nach Konversions-Ereignis (innerhalb eines Konvertierungsfensters)**

```sql
    SELECT conversionName,
           SUM(scores.firstTouch) as total_conversions,
           SUM(scores.algorithmicSourced) as total_attributed_conversions
    FROM
        (SELECT
                _tenantId.your_score_output_dataset.conversionName
                    as conversionName,
                inline(_tenantId.your_score_output_dataset.touchpointsDetail),
                timestamp as conversion_timestamp
         FROM
                your_score_output_dataset
        )
    WHERE
        conversion_timestamp >= '2020-07-16'
      AND
        conversion_timestamp <  '2020-10-14'
    GROUP BY
        conversionName
```

**Gesamtanzahl der Ereignis, die nur Konversionen durchführen (innerhalb eines Konvertierungsfensters)**

```sql
    SELECT
        _tenantId.your_score_output_dataset.conversionName as conversionName,
        COUNT(1) as convOnly_cnt
    FROM
        your_score_output_dataset
    WHERE
        _tenantId.your_score_output_dataset.touchpointsDetail.touchpointName[0] IS NULL AND
        timestamp >= '2020-07-16' AND
        timestamp <  '2020-10-14'
    GROUP BY
        conversionName
```

### Beispiele für Trend-Analysen

**Anzahl der Konversionen pro Tag**

```sql
    SELECT conversionName,
           DATE(conversion_timestamp) as conversion_date,
           SUM(scores.firstTouch) as convertion_cnt
    FROM
        (SELECT
                _tenantId.your_score_output_dataset.conversionName as conversionName,
                inline(_tenantId.your_score_output_dataset.touchpointsDetail),
                timestamp as conversion_timestamp
         FROM
                your_score_output_dataset
        )
    GROUP BY
        conversionName, DATE(conversion_timestamp)
    ORDER BY
        conversionName, DATE(conversion_timestamp)
    LIMIT 20
```

### Beispiele für die Distribution-Analyse

**Anzahl der Touchpoints auf Konversionspfaden nach definiertem Typ (innerhalb eines Konvertierungsfensters)**

```sql
    SELECT conversionName,
           touchpointName,
           COUNT(1) as tp_count
    FROM
        (SELECT
                _tenantId.your_score_output_dataset.conversionName as conversionName,
                inline(_tenantId.your_score_output_dataset.touchpointsDetail),
                timestamp as conversion_timestamp
         FROM
                your_score_output_dataset
        )
    WHERE
        conversion_timestamp >= '2020-07-16' AND
        conversion_timestamp < '2020-10-14' AND
        touchpointName IS NOT NULL
    GROUP BY
        conversionName, touchpointName
    ORDER BY
        conversionName, tp_count DESC
```

### Beispiele zur Insight-Generierung

**Inkrementelle Einheiten nach Touchpoint- und Konvertierungsdatum (innerhalb eines Konvertierungsfensters)**

```sql
    SELECT conversionName,
           touchpointName,
           DATE(conversion_timestamp) as conversion_date,
           SUM(scores.algorithmicSourced) as incremental_units
    FROM
        (SELECT
                _tenantId.your_score_output_dataset.conversionName as conversionName,
                inline(_tenantId.your_score_output_dataset.touchpointsDetail),
                timestamp as conversion_timestamp
         FROM
                your_score_output_dataset
        )
    WHERE
        conversion_timestamp >= '2020-07-16' AND
        conversion_timestamp < '2020-10-14'  AND
        touchpointName IS NOT NULL
    GROUP BY
        conversionName, touchpointName, DATE(conversion_timestamp)
    ORDER BY
        conversionName, touchpointName, DATE(conversion_timestamp)
```

**Inkrementelle Einheiten nach Touchpoint- und Touchpoint-Datum (innerhalb eines Konvertierungsfensters)**

```sql
    SELECT conversionName,
           touchpointName,
           DATE(touchpoint.timestamp) as touchpoint_date,
           SUM(scores.algorithmicSourced) as incremental_units
    FROM
        (SELECT
                _tenantId.your_score_output_dataset.conversionName as conversionName,
                inline(_tenantId.your_score_output_dataset.touchpointsDetail),
                timestamp as conversion_timestamp
         FROM
                your_score_output_dataset
        )
    WHERE
        conversion_timestamp >= '2020-07-16' AND
        conversion_timestamp < '2020-10-14'  AND
        touchpointName IS NOT NULL
    GROUP BY
        conversionName, touchpointName, DATE(touchpoint.timestamp)
    ORDER BY
        conversionName, touchpointName, DATE(touchpoint.timestamp)
    LIMIT 20
```

**Aggregierte Ergebnisse für einen bestimmten Touchpoint-Typ für alle Bewertungsmodelle (innerhalb eines Konvertierungsfensters)**

```sql
    SELECT
           conversionName,
           touchpointName,
           SUM(scores.algorithmicSourced) as total_incremental_units,
           SUM(scores.algorithmicInfluenced) as total_influenced_units,
           SUM(scores.uShape) as total_uShape_units,
           SUM(scores.decayUnits) as total_decay_units,
           SUM(scores.linear) as total_linear_units,
           SUM(scores.lastTouch) as total_lastTouch_units,
           SUM(scores.firstTouch) as total_firstTouch_units
    FROM
        (SELECT
                _tenantId.your_score_output_dataset.conversionName as conversionName,
                inline(_tenantId.your_score_output_dataset.touchpointsDetail),
                timestamp as conversion_timestamp
         FROM
                your_score_output_dataset
        )
    WHERE
        conversion_timestamp >= '2020-07-16' AND
        conversion_timestamp < '2020-10-14'  AND
        touchpointName = 'display'
    GROUP BY
        conversionName, touchpointName
    ORDER BY
        conversionName, touchpointName
```

**Erweitert - Analyse der Pfadlänge**

Abrufen einer Pfadlängenverteilung für jeden Konversions-Ereignistyp:

```sql
    WITH agg_path AS (
          SELECT
            _tenantId.your_score_output_dataset.conversionName as conversionName,
            sum(size(_tenantId.your_score_output_dataset.touchpointsDetail)) as path_length
          FROM
            your_score_output_dataset
          WHERE
            _tenantId.your_score_output_dataset.touchpointsDetail.touchpointName[0] IS NOT NULL AND
            timestamp >= '2020-07-16' AND
            timestamp <  '2020-10-14'
          GROUP BY
            _tenantId.your_score_output_dataset.conversionName,
            eventMergeId
    )
    SELECT
        conversionName,
        path_length,
        count(1) as conversionPath_count
    FROM
        agg_path
    GROUP BY
        conversionName, path_length
    ORDER BY
        conversionName, path_length
```

**Erweitert - eindeutige Anzahl von Touchpoints auf der Analyse von Konversionspfaden**

Rufen Sie die Verteilung für die Anzahl der verschiedenen Touchpoints auf einem Konversionspfad für jeden Konvertierungs-Ereignistyp ab:

```sql
    WITH agg_path AS (
      SELECT
        _tenantId.your_score_output_dataset.conversionName as conversionName,
        size(array_distinct(flatten(collect_list(_tenantId.your_score_output_dataset.touchpointsDetail.touchpointName)))) as num_dist_tp
      FROM
        your_score_output_dataset
      WHERE
        _tenantId.your_score_output_dataset.touchpointsDetail.touchpointName[0] IS NOT NULL AND
        timestamp >= '2020-07-16' AND
        timestamp <  '2020-10-14'
      GROUP BY
        _tenantId.your_score_output_dataset.conversionName,
        eventMergeId
    )
    SELECT
        conversionName,
        num_dist_tp,
        count(1) as conversionPath_count
    FROM
     agg_path
    GROUP BY
        conversionName, num_dist_tp
    ORDER BY
        conversionName, num_dist_tp
```
