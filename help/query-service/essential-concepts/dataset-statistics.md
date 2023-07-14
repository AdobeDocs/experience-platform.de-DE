---
title: Berechnung der Datensatzstatistiken
description: In diesem Dokument wird beschrieben, wie Sie Statistiken auf Spaltenebene in Azure Data Lake Storage (ADLS)-Datensätzen mit SQL-Befehlen berechnen.
source-git-commit: c7bc395038906e27449c82c518bd33ede05c5691
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 0%

---

# Berechnung der Datensatzstatistiken

Sie können nun Statistiken auf Spaltenebene berechnen über [!DNL Azure Data Lake Storage] (ADLS)-Datensätzen mit der `COMPUTE STATISTICS` und `SHOW STATISTICS` SQL-Befehle. Die SQL-Befehle, die Datensatzstatistiken berechnen, sind eine Erweiterung der `ANALYZE TABLE` Befehl. Vollständige Informationen zu `ANALYZE TABLE` -Befehl finden Sie im [SQL-Referenzdokumentation](../sql/syntax.md#analyze-table).

>[!NOTE]
>
>Derzeit sind die generierten Statistiken nur für diese Sitzung gültig und nicht zwischen Sitzungen persistent. Sie können nicht über verschiedene PSQL-Sitzungen hinweg aufgerufen werden.

Mit dem `SHOW STATISTICS FOR <alias_name>` -Befehl, sehen Sie die Statistiken, die mit der `ANALYZE TABLE COMPUTE STATISTICS` Befehl. Durch die Kombination dieser Befehle können Sie nun Spaltenstatistiken entweder für den gesamten Datensatz, eine Untergruppe eines Datensatzes, alle Spalten oder eine Untergruppe von Spalten berechnen.

>[!IMPORTANT]
>
>Die `COMPUTE STATISTICS`, `FILTERCONTEXT`, `FOR COLUMNS`und `SHOW STATISTICS` -Befehle werden in Data Warehouse-Tabellen nicht unterstützt. Diese Erweiterungen für `ANALYZE TABLE` -Befehl werden derzeit nur für ADLS-Tabellen unterstützt. Weitere Informationen finden Sie unter [ABSCHNITT &quot;ANALYSE TABLE&quot;](../sql/syntax.md#analyze-table) des SQL-Syntaxhandbuchs.

Dieses Handbuch hilft Ihnen bei der Struktur Ihrer Abfragen, sodass Sie die Spaltenstatistiken eines ADLS-Datensatzes berechnen können. Mithilfe dieser Befehle können Sie die Statistiken anzeigen, die in Ihrer Sitzung über einen PSQL-Client mithilfe einer SQL-Abfrage generiert wurden.

## Berechnen von Statistiken {#compute-statistics}

Zusätzliche Konstrukte wurden zum `ANALYZE TABLE` -Befehl, mit dem Sie **Statistiken für eine Teilmenge eines Datensatzes und für bestimmte Spalten berechnen**. Dazu müssen Sie die `ANALYZE TABLE <tableName> COMPUTE STATISTICS` Format.

>[!IMPORTANT]
>
>Das Standardverhalten berechnet Statistiken für die **gesamter Datensatz** und **Alle Spalten**. Zur Berechnung der Statistiken für alle Spalten verwenden Sie das Abfrageformat `ANALYZE TABLE COMPUTE STATISTICS`. Sie sind **not** empfohlen, dies für einen ADLS-Datensatz zu verwenden, da die Größe des Datensatzes sehr groß sein kann (potenziell Petabyte von Daten). Stattdessen sollten Sie immer in Erwägung ziehen, den Analysebefehl mit `FILTERCONTEXT` und eine bestimmte Spaltenliste. Siehe die Abschnitte unter [Analysierte Spalten begrenzen](#limit-included-columns) und [Filterbedingung hinzufügen](#filter-condition) für weitere Details.

Im folgenden Beispiel werden Statistiken für die `adc_geometric` Datensatz und für **all** Spalten im Datensatz.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS;
```

>[!NOTE]
>
>`COMPUTE STATISTICS` unterstützt keine Array- oder Zuordnungs-Datentypen. Sie können eine `skip_stats_for_complex_datatypes` Markierung, die benachrichtigt werden soll, oder Fehler-out, wenn der Eingabedataframe Spalten mit Arrays und Zuordnungs-Datentypen enthält. Standardmäßig ist das Flag auf &quot;true&quot;gesetzt. Verwenden Sie den folgenden Befehl, um Benachrichtigungen oder Fehler zu aktivieren: `SET skip_stats_for_complex_datatypes = false`.

<!-- Commented out until the <alias_name> feature is released.
This second example, is a more real-world example as it uses an alias name. See the [alias name section](#alias-name) for more details on this feature.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS as <alias_name>;
``` -->

In der Konsolenausgabe werden die Statistiken nicht als Antwort auf den Befehl zur Analyse der Tabellenberechnung angezeigt. Stattdessen zeigt die Konsole eine einzelne Zeilenspalte von `Statistics ID` mit einer universellen eindeutigen Kennung, um auf die Ergebnisse zu verweisen. Sie können auch **Abfrage direkt in der`Statistics ID`**. Bei erfolgreichem Abschluss eines `COMPUTE STATISTICS` -Abfrage, werden die Ergebnisse wie folgt angezeigt:

```console
| Statistics ID    | 
| ---------------- |
| adc_geometric_stats_1 |
(1 row)
```

Sie können die Ausgabe der Statistiken direkt abfragen, indem Sie auf die `Statistics ID` wie unten dargestellt:

```sql
SELECT * FROM adc_geometric_stats_1; 
```

Mit dieser Anweisung können Sie die Ausgabe auf ähnliche Weise anzeigen wie mit dem Befehl SHOW STATISTICS bei Verwendung mit dem `Statistics ID`.

Sie können eine Liste aller berechneten Statistiken innerhalb der Sitzung anzeigen, indem Sie den Befehl SHOW STATISTICS ausführen. Nachfolgend finden Sie eine Beispielausgabe des Befehls SHOW STATISTICS .

```console
statsId | tableName | columnSet | filterContext | timestamp
-----------+---------------+-----------+---------------------------------------+---------------
adc_geometric_stats_1 |adc_geometric | (age) | | 25/06/2023 09:22:26
demo_table_stats_1 | demo_table | (*) | ((age > 25)) | 25/06/2023 12:50:26
```

<!-- Commented out until the <alias_name> feature is released.

To see the output, you must use the `SHOW STATISTICS` command. Instructions on [how to show the statistics](#show-statistics) are provided later in the document. 

-->

## Die eingeschlossenen Spalten beschränken {#limit-included-columns}

Sie können Statistiken für bestimmte Datensatzspalten berechnen, indem Sie sie anhand des Namens referenzieren. Verwenden Sie die `FOR COLUMNS (<col1>, <col2>)` Syntax, um bestimmte Spalten als Ziel festzulegen. Im folgenden Beispiel werden Statistiken für die Spalten berechnet  `commerce`, `id`und `timestamp` für den Datensatz `tableName`.

```sql
ANALYZE TABLE tableName COMPUTE STATISTICS FOR columns (commerce, id, timestamp);
```

Sie können die Statistiken für jede Stammebene oder verschachtelte Spalte berechnen. Das folgende Beispiel zeigt diese Verweise.

```sql
ANALYZE TABLE adcgeometric COMPUTE STATISTICS FOR columns (commerce, commerce.purchases.value, commerce.productListAdds.value);
```

## Hinzufügen einer Zeitstempelfilterbedingung {#filter-condition}

Sie können eine Filterbedingung für Zeitstempel hinzufügen, um die Analyse Ihrer Spalten zu fokussieren. Damit können Sie historische Daten herausfiltern oder Ihre Datenanalyse auf einen bestimmten Zeitraum konzentrieren. Die `FILTERCONTEXT` berechnet basierend auf der von Ihnen angegebenen Filterbedingung Statistiken über eine Teilmenge des Datensatzes.

Im folgenden Beispiel werden Statistiken für alle Spalten des Datensatzes berechnet `tableName`, wobei der Spaltenzeitstempel Werte zwischen dem angegebenen Bereich aufweist `2023-04-01 00:00:00` und `2023-04-05 00:00:00`.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR ALL COLUMNS;
```

Sie können die Spaltenbegrenzung und den Filter kombinieren, um sehr spezifische Rechenabfragen für Ihre Datensatzspalten zu erstellen. Beispielsweise berechnet die folgende Abfrage Statistiken über die Spalten `commerce`, `id`und `timestamp` für den Datensatz `tableName`, wobei der Spaltenzeitstempel Werte zwischen dem angegebenen Bereich aufweist `2023-04-01 00:00:00` und `2023-04-05 00:00:00`.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR columns (commerce, id, timestamp);
```

<!-- Commented out until the <alias_name> feature is released.
## Create an alias name {#alias-name}

Since the filter condition and the column list can target a large amount of data, it is unrealistic to remember the exact values. Instead, you can provide an `<alias_name>` to store this calculated information. If you do not provide an alias name for these calculations, Query Service generates a universally unique identifier for the alias ID. You can then use this alias ID to look up the computed statistics with the `SHOW STATISTICS` command. 

>[!NOTE]
>
>Although alias names are optional, you are recommended to use them as best practice.

The example below stores the output computed statistics in the `alias_name` for later reference.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS FOR ALL COLUMNS as alias_name;
```

The output for the above example is `SUCCESSFULLY COMPLETED, alias_name`. The console output does not display the statistics in the response of the analyze table compute statistics command. To see the output, you must use the `SHOW STATISTICS` command discussed below. 
-->

<!-- Commented out until the <alias_name> feature is released.

## Show the statistics {#show-statistics}

The alias name used in the query is available as soon as the `ANALYZE TABLE` command has been run.  

Even with a filter condition and a column list, the computation can target a large amount of data. Query Service generates a universally unique identifier for the statistics ID to store this calculated information. You can then use this statistics ID to look up the computed statistics with the `SHOW STATISTICS` command at any time within that session. 

The statistics ID and the statistics generated are only valid for this particular session and cannot be accessed across different PSQL sessions. The computed statistics are not currently persistent. To display the statistics, use the command seen below.

```sql
SHOW STATISTICS FOR <STATISTICS_ID>;
```

An output might look similar to the example below. 

```console
                         columnName                         |      mean      |      max       |      min       | standardDeviation | approxDistinctCount | nullCount | dataType  
------------------------------------------------------------+----------------+----------------+----------------+-------------------+---------------------+-----------+-----------
 marketing.trackingcode                                     |            0.0 |            0.0 |            0.0 |               0.0 |              1213.0 |         0 | String
 _experience.analytics.customdimensions.evars.evar13        |            0.0 |            0.0 |            0.0 |               0.0 |              8765.0 |        20 | String
 _experience.analytics.customdimensions.evars.evar74        |            0.0 |            0.0 |            0.0 |               0.0 |                11.0 |         0 | String
 web.webpagedetails.name                                    |            0.0 |            0.0 |            0.0 |               0.0 |                 1.0 |         0 | String
 _experience.analytics.event1to100.event8.value             |            5.0 |         9077.0 |          123.0 |              10.0 |              1001.0 |        80 | Double
 search.ispaid                                              |            0.0 |            0.0 |            0.0 |               0.0 |                 1.0 |         0 | Boolean
 commerce.productlistviews.value                            |            0.0 |            0.0 |            0.0 |               0.0 |                 0.0 |        10 | Double
 device.typeid                                              |            0.0 |            0.0 |            0.0 |               0.0 |                 0.0 |        10 | String
 commerce.purchases.value                                   |          765.0 |        98760.0 |         -980.0 |              32.0 |                99.0 |        90 | Double
 _experience.analytics.customdimensions.props.prop45        |            0.0 |            0.0 |            0.0 |               0.0 |                 1.0 |         0 | String
 environment.browserdetails.javaenabled                     |            0.0 |            0.0 |            0.0 |               0.0 |                 1.0 |         0 | Boolean
 timestamp                                                  |            0.0 |            0.0 |            0.0 |               0.0 |                98.0 |         3 | Timestamp
(12 rows)
```

-->

## Nächste Schritte {#next-steps}

Durch Lesen dieses Dokuments erhalten Sie jetzt ein besseres Verständnis davon, wie Sie mit einer SQL-Abfrage Statistiken auf Spaltenebene aus einem ADLS-Datensatz generieren. Es wird empfohlen, die [SQl-Syntaxhandbuch](../sql/syntax.md) , um weitere Funktionen des Adobe Experience Platform Query Service zu erfahren.
