---
keywords: Insights;Attributions-KI;Attributions-KI-Insights;AAI-Query-Service;Attributionsabfragen;Attributionsbewertungen
feature: Attribution AI
title: Analysieren von Attributionsbewertungen mit dem Abfrage-Service
description: Erfahren Sie, wie Sie mit dem Abfrage-Service von Adobe Experience Platform Attribution AI-Bewertungen analysieren können.
exl-id: 35d7f6f2-a118-4093-8dbc-cb020ec35e90
source-git-commit: 66d20dc1141ff33211635ba74d320350f8b27fb7
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 2%

---

# Analysieren von Attributionsbewertungen mit dem Abfrage-Service

Jede Zeile in den Daten stellt eine Konversion dar, bei der Informationen zu zugehörigen Touchpoints als Array von Strukturen unter der `touchpointsDetail` Spalte gespeichert werden.

| Touchpoint-Informationen | Spalte |
| ---------------------- | ------ |
| Touchpoint-Name | `touchpointsDetail. touchpointName` |
| Touchpoint-Kanal | `touchpointsDetail.touchPoint.mediaChannel` |
| Algorithmische Punktzahlen für Touchpoint Attribution AI | <li>`touchpointsDetail.scores.algorithmicSourced`</li> <li> `touchpointsDetail.scores.algorithmicInfluenced` </li> |

## Ermitteln von Datenpfaden

Wählen Sie in der Benutzeroberfläche von Adobe Experience Platform **[!UICONTROL Datensätze]** im linken Navigationsbereich aus. Die **[!UICONTROL Datensätze]** wird angezeigt. Wählen Sie als Nächstes die **[!UICONTROL Durchsuchen]** und suchen Sie den Ausgabedatensatz für Ihre Attribution AI-Bewertungen.

![Zugriff auf Ihr Modell](./images/aai-query/datasets_browse.png)

Wählen Sie Ihren Ausgabedatensatz aus. Die Seite Datensatzaktivität wird angezeigt.

![Seite Datensatzaktivität](./images/aai-query/select_preview.png)

Wählen Sie auf der Seite Datensatzaktivität **[!UICONTROL Vorschau des Datensatzes]** in der oberen rechten Ecke aus, um eine Vorschau Ihrer Daten anzuzeigen und sicherzustellen, dass sie wie erwartet aufgenommen wurden.

![Vorschau des Datensatzes](./images/aai-query/preview_dataset.JPG)

Wählen Sie nach der Vorschau Ihrer Daten das Schema in der rechten Leiste aus. Es wird ein Pop-up mit dem Schemanamen und der Beschreibung angezeigt. Wählen Sie den Hyperlink für den Schemanamen aus, um zum Scoring-Schema weiterzuleiten.

![Schema auswählen](./images/aai-query/select_schema.png)

Mithilfe des Scoring-Schemas können Sie einen Wert auswählen oder suchen. Nach der Auswahl **[!UICONTROL sich die Seitenleiste]** Feldeigenschaften“, in der Sie den Pfad kopieren können, der zum Erstellen von Abfragen verwendet werden soll.

![Kopieren Sie den Pfad](./images/aai-query/copy_path.png)

## Zugriff auf Query Service

Um über die Platform-Benutzeroberfläche auf den Abfrage-Service zuzugreifen, wählen Sie zunächst im linken Navigationsbereich **[!UICONTROL Abfragen]** und dann die Registerkarte **[!UICONTROL Durchsuchen]** aus. Eine Liste der zuvor gespeicherten Abfragen wird geladen.

![Query Service durchsuchen](./images/aai-query/query_tab.png)

Wählen Sie als Nächstes **[!UICONTROL Abfrage erstellen]** in der oberen rechten Ecke. Der Abfrage-Editor wird geladen. Mit dem Abfrage-Editor können Sie Abfragen mithilfe Ihrer Bewertungsdaten erstellen.

![Abfrage-Editor](./images/aai-query/query_example.png)

Weitere Informationen zum Abfrage-Editor finden Sie im [Benutzerhandbuch zum Abfrage-Editor](../../query-service/ui/user-guide.md).

## Abfragevorlagen für die Attributionsbewertungsanalyse

Die folgenden Abfragen können als Vorlage für verschiedene Bewertungsszenarien verwendet werden. Sie müssen die `_tenantId` und `your_score_output_dataset` durch die richtigen Werte ersetzen, die in Ihrem Scoring-Ausgabeschema gefunden wurden.

>[!NOTE]
>
> Je nachdem, wie Ihre Daten aufgenommen wurden, können die unten verwendeten Werte, wie `timestamp`, in einem anderen Format vorliegen.

### Validierungsbeispiele

**Gesamtzahl der Konvertierungen nach Konversionsereignis (innerhalb eines Konversionsfensters)**

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

**Gesamtzahl der Nur-Konversions-Ereignisse (innerhalb eines Konversionsfensters)**

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

### Beispiel für eine Trendanalyse

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

**Anzahl der Touchpoints auf Konversionspfaden nach definiertem Typ (innerhalb eines Konversionsfensters)**

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

### Beispiele für die Erstellung von Einblicken

**Inkrementelle Aufschlüsselung der Einheiten nach Touchpoint und Konversionsdatum (innerhalb eines Konversionsfensters)**

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

**Inkrementelle Aufschlüsselung der Einheiten nach Touchpoint und Touchpoint-Datum (innerhalb eines Konversionsfensters)**

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

**Aggregierte Werte für einen bestimmten Touchpoint-Typ für alle Bewertungsmodelle (innerhalb eines Konversionsfensters)**

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

Abrufen einer Pfadlängenverteilung für jeden Konversionsereignistyp:

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

**Erweitert - unterschiedliche Anzahl von Touchpoints bei der Konversionspfaderanalyse**

Abrufen der Verteilung der Anzahl unterschiedlicher Touchpoints auf einem Konversionspfad für jeden Konversionsereignistyp:

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

### Beispiel für Schemareduzierung und -explosion

Mit dieser Abfrage wird die Struktur-Spalte in mehrere einzelne Spalten reduziert und Arrays in mehrere Zeilen aufgelöst. Dies hilft bei der Umwandlung von Attributionsbewertungen in ein CSV-Format. Die Ausgabe dieser Abfrage hat in jeder Zeile eine Konversion und einen der Touchpoints, die dieser Konversion entsprechen.

>[!TIP]
>
> In diesem Beispiel müssen Sie `{COLUMN_NAME}` zusätzlich zu `_tenantId` und `your_score_output_dataset` ersetzen. Die Variable `COLUMN_NAME` kann die Werte optionaler Durchlaufspaltennamen (Berichtsspalten) übernehmen, die bei der Konfiguration Ihres Attribution AI-Modells hinzugefügt wurden. Bitte überprüfen Sie Ihr Scoring-Ausgabeschema, um die `{COLUMN_NAME}` Werte zu finden, die zum Durchführen dieser Abfrage benötigt werden.

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
