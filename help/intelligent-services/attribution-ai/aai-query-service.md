---
keywords: Insights;Attributions-KI;Attributions-KI-Insights;AAI-Query-Service;Attributionsabfragen;Attributionsbewertungen
feature: Attribution AI
title: Analyse von Attributionsbewertungen mithilfe von Query Service
description: Erfahren Sie, wie Sie mit Adobe Experience Platform Query Service Attribution AI-Bewertungen analysieren können.
exl-id: 35d7f6f2-a118-4093-8dbc-cb020ec35e90
source-git-commit: 66d20dc1141ff33211635ba74d320350f8b27fb7
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 2%

---

# Analyse von Attributionswerten mithilfe von Query Service

Jede Zeile in den Daten stellt eine Konversion dar, in der Informationen für verwandte Touchpoints als Array von Strukturen unter der Spalte `touchpointsDetail` gespeichert werden.

| Touchpoint-Informationen | Spalte |
| ---------------------- | ------ |
| Touchpoint-Name | `touchpointsDetail. touchpointName` |
| Touchpoint-Kanal | `touchpointsDetail.touchPoint.mediaChannel` |
| Algorithmische Werte für Touchpoint-Attribution AI | <li>`touchpointsDetail.scores.algorithmicSourced`</li> <li> `touchpointsDetail.scores.algorithmicInfluenced` </li> |

## Suchen nach Datenpfaden

Wählen Sie in der Adobe Experience Platform-Benutzeroberfläche im linken Navigationsbereich **[!UICONTROL Datensätze]** aus. Die Seite **[!UICONTROL Datensätze]** wird angezeigt. Wählen Sie als Nächstes die Registerkarte **[!UICONTROL Durchsuchen]** aus und suchen Sie den Ausgabedatensatz für Ihre Attribution AI-Bewertungen.

![Zugriff auf Ihr Modell](./images/aai-query/datasets_browse.png)

Wählen Sie Ihren Ausgabedatensatz aus. Die Seite mit der Datensatzaktivität wird angezeigt.

![Datensatzaktivität-Seite](./images/aai-query/select_preview.png)

Wählen Sie auf der Seite mit der Datensatzaktivität **[!UICONTROL Datensatz-Vorschau]** in der oberen rechten Ecke aus, um Ihre Daten in der Vorschau anzuzeigen und sicherzustellen, dass sie erwartungsgemäß erfasst wurden.

![Vorschau-Datensatz](./images/aai-query/preview_dataset.JPG)

Wählen Sie nach der Vorschau Ihrer Daten das Schema in der rechten Leiste aus. Es wird ein Popover mit dem Schemanamen und der Beschreibung angezeigt. Wählen Sie den Hyperlink für den Schemanamen aus, um zum Scoring-Schema umzuleiten.

![Wählen Sie das Schema aus](./images/aai-query/select_schema.png)

Mithilfe des Scoring-Schemas können Sie einen Wert auswählen oder suchen. Nach der Auswahl wird die Seitenleiste **[!UICONTROL Feldeigenschaften]** geöffnet, in der Sie den Pfad kopieren können, der zum Erstellen von Abfragen verwendet werden soll.

![Kopieren Sie den Pfad](./images/aai-query/copy_path.png)

## Zugriff auf Query Service

Um über die Platform-Benutzeroberfläche auf Query Service zuzugreifen, wählen Sie zunächst **[!UICONTROL Abfragen]** im linken Navigationsbereich und dann die Registerkarte **[!UICONTROL Durchsuchen]** aus. Eine Liste der zuvor gespeicherten Abfragen wird geladen.

![Query Service Browse](./images/aai-query/query_tab.png)

Wählen Sie dann oben rechts **[!UICONTROL Abfrage erstellen]** aus. Der Abfrage-Editor wird geladen. Mithilfe des Abfrage-Editors können Sie mit der Erstellung von Abfragen mit Ihren Scoring-Daten beginnen.

![Abfrageeditor](./images/aai-query/query_example.png)

Weitere Informationen zum Abfrage-Editor finden Sie im [Benutzerhandbuch zum Abfrage-Editor](../../query-service/ui/user-guide.md).

## Abfragevorlagen für die Attributionswertanalyse

Die folgenden Abfragen können als Vorlage für verschiedene Bewertungsanalyseszenarien verwendet werden. Sie müssen die Werte `_tenantId` und `your_score_output_dataset` durch die entsprechenden Werte in Ihrem Scoring-Ausgabeschema ersetzen.

>[!NOTE]
>
> Je nachdem, wie Ihre Daten erfasst wurden, können die unten verwendeten Werte wie `timestamp` in einem anderen Format vorliegen.

### Validierungsbeispiele

**Gesamtanzahl der Konversionen nach Konversionsereignis (innerhalb eines Konvertierungsfensters)**

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

**Gesamtanzahl der reinen Konversionsereignisse (innerhalb eines Konvertierungsfensters)**

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

### Beispiel für Trend-Analyse

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

### Beispiel einer Verteilungsanalyse

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

**Inkrementelle Einheiten - Aufschlüsselung nach Touchpoint- und Konversionsdatum (innerhalb eines Konvertierungsfensters)**

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

**Inkrementelle Einheiten - Aufschlüsselung nach Touchpoint- und Touchpoint-Datum (innerhalb eines Konvertierungsfensters)**

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

**Aggregierte Werte für einen bestimmten Touchpoint-Typ für alle Scoring-Modelle (innerhalb eines Konvertierungsfensters)**

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

**Erweitert - Pfadlängenanalyse**

Rufen Sie eine Pfadlängenverteilung für jeden Konversionsereignistyp ab:

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

**Erweitert - Bestimmte Anzahl von Touchpoints auf der Analyse von Konversionspfaden**

Rufen Sie die Verteilung für die Anzahl unterschiedlicher Touchpoints auf einem Konversionspfad für jeden Konversionsereignistyp ab:

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

### Beispiel für Schema-Abflachung und -Explosion

Diese Abfrage reduziert die Strukturspalte in mehrere Einzelspalten und explodiert Arrays in mehrere Zeilen. Dies hilft beim Transformieren von Attributionswerten in ein CSV-Format. Die Ausgabe dieser Abfrage weist in jeder Zeile eine Konversion und einen der Touchpoints auf, die dieser Konversion entsprechen.

>[!TIP]
>
> In diesem Beispiel müssen Sie zusätzlich zu `_tenantId` und `your_score_output_dataset` `{COLUMN_NAME}` ersetzen. Die Variable &quot;`COLUMN_NAME`&quot; kann die Werte der optionalen Übergabe durch Spaltennamen (Berichtsspalten) annehmen, die bei der Konfiguration Ihres Attribution AI-Modells hinzugefügt wurden. Überprüfen Sie Ihr Scoring-Ausgabeschema, um die `{COLUMN_NAME}` -Werte zu finden, die zum Abschließen dieser Abfrage erforderlich sind.

```sql
SELECT 
  segmentation,
  conversionName,
  scoreCreatedTime,
  aaid, _id, eventMergeId,
  conversion.eventType as conversion_eventType,
  conversion.quantity as conversion_quantity,
  conversion.eventSource as conversion_eventSource,
  conversion.priceTotal as conversion_priceTotal,
  conversion.timestamp as conversion_timestamp,
  conversion.geo as conversion_geo,
  conversion.receivedTimestamp as conversion_receivedTimestamp,
  conversion.dataSource as conversion_dataSource,
  conversion.productType as conversion_productType,
  conversion.passThrough.{COLUMN_NAME} as conversion_passThru_column,
  conversion.skuId as conversion_skuId,
  conversion.product as conversion_product,
  touchpointName,
  touchPoint.campaignGroup as tp_campaignGroup, 
  touchPoint.mediaType as tp_mediaType,
  touchPoint.campaignTag as tp_campaignTag,
  touchPoint.timestamp as tp_timestamp,
  touchPoint.geo as tp_geo,
  touchPoint.receivedTimestamp as tp_receivedTimestamp,
  touchPoint.passThrough.{COLUMN_NAME} as tp_passThru_column,
  touchPoint.campaignName as tp_campaignName,
  touchPoint.mediaAction as tp_mediaAction,
  touchPoint.mediaChannel as tp_mediaChannel,
  touchPoint.eventid as tp_eventid,
  scores.*
FROM (
  SELECT
        _tenantId.your_score_output_dataset.segmentation,
        _tenantId.your_score_output_dataset.conversionName,
        _tenantId.your_score_output_dataset.scoreCreatedTime,
        _tenantId.your_score_output_dataset.conversion,
        _id,
        eventMergeId,
        map_values(identityMap)[0][0].id as aaid,
        inline(_tenantId.your_score_output_dataset.touchpointsDetail)
  FROM
        your_score_output_dataset
)
```
