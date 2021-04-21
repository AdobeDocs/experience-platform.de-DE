---
keywords: Einblicke;Zuordnungsai;Zuordnungs-ai-Einblicke;AAI-Abfrage-Dienst;Zuordnungs-Abfragen;Zuordnungswerte
solution: Intelligent Services, Experience Platform
title: Analysieren von Zuordnungswerten mithilfe des Abfrage Service
topic-legacy: Attribution AI queries
description: Erfahren Sie, wie Sie mit dem Adobe Experience Platform Abfrage Service Attribution AI-Ergebnisse analysieren können.
exl-id: 35d7f6f2-a118-4093-8dbc-cb020ec35e90
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '589'
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

Die folgenden Abfragen können als Vorlage für verschiedene Szenarien zur Analyse des Punktwerts verwendet werden. Sie müssen die Werte `_tenantId` und `your_score_output_dataset` durch die entsprechenden Werte in Ihrem bewerteten Schema ersetzen.

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

### Beispiel für die Distribution-Analyse

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

### Beispiel zum Reduzieren und Explodieren von Schemas

Diese Abfrage reduziert die Strukturspalte in mehrere Einzelspalten und explodiert Arrays in mehrere Zeilen. Auf diese Weise können Sie Zuordnungswerte in ein CSV-Format umwandeln. Die Ausgabe dieser Abfrage enthält eine Konvertierung und einen der Touchpoints, die dieser Konvertierung in jeder Zeile entsprechen.

>[!TIP]
>
> In diesem Beispiel müssen Sie `{COLUMN_NAME}` zusätzlich zu `_tenantId` und `your_score_output_dataset` ersetzen. Die Variable `COLUMN_NAME` kann die Werte der optionalen Übergabe durch Spaltennamen (Berichte-Spalten) annehmen, die während der Konfiguration der Attribution AI-Instanz hinzugefügt wurden. Bitte überprüfen Sie Ihr Schema für die Bewertungsausgabe, um die `{COLUMN_NAME}`-Werte zu finden, die zum Abschluss dieser Abfrage erforderlich sind.

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
