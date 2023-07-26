---
title: Berechnung der Datensatzstatistiken
description: In diesem Dokument wird beschrieben, wie Sie mit SQL-Befehlen Statistiken auf Spaltenebene für Azure Data Lake Storage(ADLS)-Datensätze berechnen.
source-git-commit: 66354932ee42137ca98e7033d942556f13c64de1
workflow-type: tm+mt
source-wordcount: '1087'
ht-degree: 39%

---

# Berechnung der Datensatzstatistiken

Sie können nun Statistiken auf Spaltenebene für [!DNL Azure Data Lake Storage](ADLS)-Datensätze mit den SQL-Befehlen `COMPUTE STATISTICS` und `SHOW STATISTICS` berechnen. Die SQL-Befehle, die Datensatzstatistiken berechnen, sind eine Erweiterung des Befehls `ANALYZE TABLE`. Vollständige Informationen zum Befehl `ANALYZE TABLE` finden Sie in der [SQL-Referenzdokumentation](../sql/syntax.md#analyze-table).

>[!NOTE]
>
>Berechnete Statistiken werden in temporären Tabellen gespeichert, die eine Persistenz auf Sitzungsebene aufweisen. Sie können jederzeit während dieser Sitzung auf die Ergebnisse der Berechnungen zugreifen. Ein Zugriff über verschiedene PSQL-Sitzungen hinweg ist nicht möglich.

So zeigen Sie die Statistiken an, die mit der `ANALYZE TABLE COMPUTE STATISTICS` verwenden, können Sie eine SELECT-Abfrage für den Aliasnamen oder die Statistikkennung verwenden. Sie können den Umfang der statistischen Analyse auch auf den gesamten Datensatz, eine Untergruppe eines Datensatzes, alle Spalten oder eine Untergruppe von Spalten beschränken.

>[!IMPORTANT]
>
>Die Befehle `COMPUTE STATISTICS`, `FILTERCONTEXT`, `FOR COLUMNS` und `SHOW STATISTICS` werden in Data-Warehouse-Tabellen nicht unterstützt. Diese Erweiterungen für den Befehl `ANALYZE TABLE` werden derzeit nur für ADLS-Tabellen unterstützt. Weitere Informationen finden Sie im [ANALYZE TABLE-Abschnitt](../sql/syntax.md#analyze-table) des SQL-Syntaxhandbuchs.

Dieses Handbuch hilft Ihnen bei der Strukturierung Ihrer Abfragen, sodass Sie die Spaltenstatistiken eines ADLS-Datensatzes berechnen können. Mithilfe dieser Befehle können Sie die Statistiken anzeigen, die in Ihrer Sitzung über einen PSQL-Client mithilfe einer SQL-Abfrage generiert wurden.

## Berechnen von Statistiken {#compute-statistics}

Zusätzliche Konstrukte wurden zum `ANALYZE TABLE` -Befehl, mit dem Sie **Statistiken für eine Teilmenge eines Datensatzes und für bestimmte Spalten berechnen**. Zur Berechnung der Datensatzstatistiken müssen Sie die Variable `ANALYZE TABLE <tableName> COMPUTE STATISTICS` Format.

>[!IMPORTANT]
>
>Standardmäßig werden Statistiken für den **gesamten Datensatz** und für **alle Spalten** berechnet. Zur Berechnung von Statistiken für alle Spalten verwenden Sie das Abfrageformat `ANALYZE TABLE COMPUTE STATISTICS`. Sie sind **not** wird empfohlen, die `COMPUTE STATISTICS` -Befehl ohne Filter für einen ADLS-Datensatz verwenden, da die Größe des Datensatzes sehr groß sein kann (potenziell Petabyte von Daten). Stattdessen sollten Sie immer in Erwägung ziehen, den Analysebefehl mit `FILTERCONTEXT` und einer bestimmten Spaltenliste auszuführen. Weiterführende Informationen finden Sie in Abschnitten zum [Begrenzen analysierter Spalten](#limit-included-columns) und [Hinzufügen einer Filterbedingung](#filter-condition).

Im folgenden Beispiel werden Statistiken für den Datensatz `adc_geometric` und für **alle** Spalten im Datensatz berechnet.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS;
```

>[!NOTE]
>
>Die `COMPUTE STATISTICS` -Befehl unterstützt keine Array- oder map-Datentypen. Sie können eine `skip_stats_for_complex_datatypes` Markierung, die benachrichtigt werden soll, oder Fehlermeldung, wenn der Eingabedatenrahmen Spalten mit Arrays und Zuordnungs-Datentypen enthält. Standardmäßig ist diese Markierung auf „true“ eingestellt. Verwenden Sie den folgenden Befehl, um Benachrichtigungen oder Fehler zu aktivieren: `SET skip_stats_for_complex_datatypes = false`.

## Aliasnamen erstellen {#alias-name}

Da die Ergebnisse von Berechnungen eine große Datenmenge sein können, ist es nicht sinnvoll, die berechneten Daten direkt in der Konsolenausgabe zurückzugeben. Alias-Namen sind zwar optional, Sie sollten sie jedoch bei der Berechnung von Statistiken als Best Practice verwenden. Geben Sie in der Anweisung einen Aliasnamen an, um die Ergebnisse in Ihren SQL-Abfragen beschreibend zu referenzieren. Alternativ dazu kann automatisch eine `Statistics ID` wird generiert und zum Speichern der berechneten Informationen verwendet.

Im folgenden Beispiel werden die berechneten Ausgabestatistiken im `alias_name` für eine spätere Referenz. Der in der Abfrage verwendete Aliasname kann referenziert werden, sobald die Variable `ANALYZE TABLE` ausgeführt wurde.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS AS alias_name;
```

Die Ausgabe für das obige Beispiel lautet `SUCCESSFULLY COMPLETED, alias_name`. In der Konsolenausgabe werden die Statistiken in der Antwort auf den Befehl zur Analyse der Tabellenberechnung nicht angezeigt. Um die detaillierten Ergebnisse anzuzeigen, müssen Sie eine SELECT-Abfrage für den Aliasnamen oder die Statistiken-ID verwenden.

## Anzeigen der Ausgabe berechneter Statistiken {#view-output-of-computed-statistics}

Wenn Sie im Voraus keinen Aliasnamen angeben, generiert Query Service automatisch einen Namen für die `Statistics ID` , das dem Format von `<tableName_stats_{incremental_number}>`. Wenn ein Aliasname angegeben wird, wird er im `Statistics ID` Spalte.

Eine Beispielausgabe eines `COMPUTE STATISTICS` -Abfrage lautet wie folgt:

```console
| Statistics ID    | 
| ---------------- |
| adc_geometric_stats_1 |
(1 row)
```

Sie können dann **die berechneten Statistiken direkt abfragen** durch Referenzierung der `Statistics ID`. Die folgende Beispielanweisung ermöglicht es Ihnen, die Ausgabe vollständig anzuzeigen, wenn sie mit der `Statistics ID` oder den Aliasnamen.

```sql
SELECT * FROM adc_geometric_stats_1; 
```

Die Ausgabe berechneter Statistiken ähnelt möglicherweise dem unten stehenden Beispiel.

```console
 columnName                                                 |      mean      |      max       |      min       | standardDeviation | approxDistinctCount | nullCount | dataType  
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

## Anzeigen der Metadaten der statistischen Analyse {#show-statistics}

Sie können die `SHOW STATISTICS` -Befehl, um die Metadaten für alle temporären Statistiktabellen anzuzeigen, die in der Sitzung generiert wurden. Mithilfe dieses Befehls können Sie den Umfang Ihrer statistischen Analyse verfeinern.

Eine Beispielausgabe von `SHOW STATISTICS` wird unten angezeigt.

```console
statsId | tableName | columnSet | filterContext | timestamp
--------+-----------+-----------+---------------+---------------
adc_geometric_stats_1 | adc_geometric | (age) |  | 25/06/2023 09:22:26
demo_table_stats_1 | demo_table | (*) | ((age > 25)) | 25/06/2023 12:50:26
age_stats | castedtitanic | (age) | ((age > 25) AND (age < 40)) | 25/06/2023 09:22:26
```

Nachfolgend finden Sie eine Beschreibung der Metadaten-Spaltennamen.

| Spaltenname | Beschreibung |
|---|---|
| `statsId` | Diese ID verweist auf die temporäre Statistiktabelle, die von der `COMPUTE STATISTICS` Befehl. |
| `tableName` | Die ursprüngliche Tabelle, die für die Analyse verwendet wird. |
| `columnSet` | Liste aller Spalten, die speziell für die Analyse ausgewählt wurden. Ein leerer Wert gibt an, dass alle Spalten analysiert wurden. Siehe Abschnitt zu [Spalten begrenzen](#limit-included-columns) für weitere Informationen. |
| `filterContext` | Eine Liste aller auf die Analyse angewendeten Filter. |
| `timestamp` | Alle chronologischen Filter, die auf Ihre Datenanalyse angewendet werden, um sich auf einen bestimmten Zeitraum zu konzentrieren. Siehe [Bedingungsabschnitt für Zeitstempelfilter](#filter-condition) für weitere Details. |

Sie können die Statistiken-ID oder den Aliasnamen verwenden, um die berechneten Statistiken mit einer SELECT-Anweisung jederzeit innerhalb dieser Sitzung nachzuschlagen. Die Statistik-ID und die generierten Statistiken sind nur für diese bestimmte Sitzung gültig und können nicht über verschiedene PSQL-Sitzungen hinweg aufgerufen werden. Die berechneten Statistiken sind derzeit nicht persistent. Siehe den Abschnitt zum [die Ausgabe Ihrer berechneten Statistiken anzeigen](#view-output-of-computed-statistics) für weitere Details.

## Begrenzen der eingeschlossenen Spalten {#limit-included-columns}

Um Ihre Analyse zu fokussieren, können Sie Statistiken für bestimmte Datensatzspalten berechnen, indem Sie sie anhand des Namens referenzieren. Verwenden Sie die Syntax `FOR COLUMNS (<col1>, <col2>)`, um bestimmte Spalten als Ziel festzulegen. Im folgenden Beispiel werden Statistiken für die Spalten `commerce`, `id` und `timestamp` für den Datensatz `tableName` berechnet.

```sql
ANALYZE TABLE tableName COMPUTE STATISTICS FOR columns (commerce, id, timestamp);
```

Sie können die Statistiken für jede Stammebene oder verschachtelte Spalte berechnen. Das folgende Beispiel veranschaulicht diese Verweise.

```sql
ANALYZE TABLE adcgeometric COMPUTE STATISTICS FOR columns (commerce, commerce.purchases.value, commerce.productListAdds.value);
```

## Hinzufügen einer Zeitstempel-Filterbedingung {#filter-condition}

Um die Analyse Ihrer Spalten auf der Basis der Chronologie zu fokussieren, können Sie eine Bedingung für den Zeitstempelfilter hinzufügen. Mit dieser Bedingung können Sie historische Daten herausfiltern oder Ihre Datenanalyse auf einen bestimmten Zeitraum konzentrieren. Die `FILTERCONTEXT` berechnet basierend auf der von Ihnen angegebenen Filterbedingung Statistiken über eine Teilmenge des Datensatzes.

Im folgenden Beispiel werden Statistiken für alle Spalten des Datensatzes `tableName` berechnet, wobei der Spaltenzeitstempel Werte zwischen dem angegebenen Bereich `2023-04-01 00:00:00` und `2023-04-05 00:00:00` aufweist.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR ALL COLUMNS;
```

Sie können die Spaltenbegrenzung und den Filter kombinieren, um sehr spezifische Rechenabfragen für Ihre Datensatzspalten zu erstellen. Beispielsweise werden mit der folgenden Abfrage Statistiken zu den Spalten `commerce`, `id` und `timestamp` für den Datensatz `tableName` berechnet, wobei der Spaltenzeitstempel Werte zwischen dem angegebenen Bereich `2023-04-01 00:00:00` und `2023-04-05 00:00:00` aufweist.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR columns (commerce, id, timestamp);
```

## Nächste Schritte {#next-steps}

Durch Lesen dieses Dokuments können Sie jetzt besser verstehen, wie Sie mit einer SQL-Abfrage Statistiken auf Spaltenebene für einen ADLS-Datensatz generieren. Es wird empfohlen, das [SQl-Syntaxhandbuch](../sql/syntax.md) zu lesen, um weitere Funktionen des Adobe Experience Platform-Abfrage-Service kennenzulernen.
