---
title: Berechnung der Datensatzstatistiken
description: In diesem Dokument wird beschrieben, wie Sie mit SQL-Befehlen Statistiken auf Spaltenebene für Azure Data Lake Storage(ADLS)-Datensätze berechnen.
exl-id: 66f11cd4-b115-40b8-ba8a-c4bb3606bbbf
source-git-commit: 37aeff5131b9f67dbc99f6199918403e699478c8
workflow-type: tm+mt
source-wordcount: '1085'
ht-degree: 100%

---

# Berechnung der Datensatzstatistiken

Sie können nun Statistiken auf Spaltenebene für [!DNL Azure Data Lake Storage] (ADLS)-Datensätze mit dem SQL-Befehl `COMPUTE STATISTICS` berechnen. Die SQL-Befehle, die Datensatzstatistiken berechnen, sind eine Erweiterung des Befehls `ANALYZE TABLE`. Vollständige Informationen zum Befehl `ANALYZE TABLE` finden Sie in der [SQL-Referenzdokumentation](../sql/syntax.md#analyze-table).

>[!NOTE]
>
>Berechnete Statistiken werden in temporären Tabellen gespeichert, die eine Persistenz auf Sitzungsebene aufweisen. Sie können jederzeit während dieser Sitzung auf die Ergebnisse der Berechnungen zugreifen. Ein Zugriff über verschiedene PSQL-Sitzungen hinweg ist nicht möglich.

Um die mit dem Befehl `ANALYZE TABLE COMPUTE STATISTICS` berechneten Statistiken anzuzeigen, können Sie eine SELECT-Abfrage auf den Aliasnamen oder die Statistik-ID verwenden. Sie können den Umfang der statistischen Analyse auch auf den gesamten Datensatz, eine Untergruppe eines Datensatzes, alle Spalten oder eine Untergruppe von Spalten beschränken.

>[!IMPORTANT]
>
>Die Befehle `COMPUTE STATISTICS`, `FILTERCONTEXT` und `FOR COLUMNS` werden bei beschleunigten Speichertabellen nicht unterstützt. Diese Erweiterungen für den Befehl `ANALYZE TABLE` werden derzeit nur für ADLS-Tabellen unterstützt. Weitere Informationen finden Sie im [ANALYZE TABLE-Abschnitt](../sql/syntax.md#analyze-table) des SQL-Syntaxhandbuchs.

Dieses Handbuch hilft Ihnen bei der Strukturierung Ihrer Abfragen, sodass Sie die Spaltenstatistiken eines ADLS-Datensatzes berechnen können. Mithilfe dieser Befehle können Sie die Statistiken anzeigen, die in Ihrer Sitzung über einen PSQL-Client mithilfe einer SQL-Abfrage generiert wurden.

## Berechnen von Statistiken {#compute-statistics}

Der Befehl `ANALYZE TABLE` wurde um zusätzliche Konstrukte erweitert. Dadurch können Sie **Statistiken für eine Datensatzteilmenge und für bestimmte Spalten berechnen**. Zur Berechnung von Datensatzstatistiken müssen Sie das Format `ANALYZE TABLE <tableName> COMPUTE STATISTICS` verwenden.

>[!IMPORTANT]
>
>Standardmäßig werden Statistiken für den **gesamten Datensatz** und für **alle Spalten** berechnet. Zur Berechnung von Statistiken für alle Spalten verwenden Sie das Abfrageformat `ANALYZE TABLE COMPUTE STATISTICS`. Es wird **nicht** empfohlen, den Befehl `COMPUTE STATISTICS` ohne Filter für einen ADLS-Datensatz zu verwenden, da die Größe des Datensatzes sehr groß sein kann (möglicherweise Petabytes an Daten). Stattdessen sollten Sie immer in Erwägung ziehen, den Analysebefehl mit `FILTERCONTEXT` und einer bestimmten Spaltenliste auszuführen. Weiterführende Informationen finden Sie in Abschnitten zum [Begrenzen analysierter Spalten](#limit-included-columns) und [Hinzufügen einer Filterbedingung](#filter-condition).

Im folgenden Beispiel werden Statistiken für den Datensatz `adc_geometric` und für **alle** Spalten im Datensatz berechnet.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS;
```

>[!NOTE]
>
>Der Befehl `COMPUTE STATISTICS` unterstützt keine Array- oder Map-Datentypen. Sie können die Markierung `skip_stats_for_complex_datatypes` festlegen, damit eine Benachrichtigung oder ein Fehler ausgegeben wird, wenn der Eingabe-Datenrahmen Spalten mit Array- und Map-Datentypen umfasst. Standardmäßig ist diese Markierung auf „true“ eingestellt. Verwenden Sie den folgenden Befehl, um Benachrichtigungen oder Fehler zu aktivieren: `SET skip_stats_for_complex_datatypes = false`.

## Erstellen eines Aliasnamens {#alias-name}

Da die Ergebnisse von Berechnungen eine große Datenmenge ausmachen können, ist es nicht sinnvoll, die berechneten Daten direkt in der Konsolenausgabe zurückzugeben. Aliasnamen sind zwar optional, Sie sollten sie jedoch bei der Berechnung von Statistiken als Best Practice verwenden. Geben Sie in der Anweisung einen Aliasnamen an, um die Ergebnisse in Ihren SQL-Abfragen beschreibend zu referenzieren. Alternativ dazu wird eine automatisch generierte `Statistics ID` erzeugt und zur Speicherung der berechneten Informationen verwendet.

Das folgende Beispiel speichert die berechneten Statistiken in der Datei `alias_name` für eine spätere Verwendung. Der in der Abfrage verwendete Aliasname ist als Referenz verfügbar, sobald der Befehl `ANALYZE TABLE` ausgeführt wurde.

```sql
ANALYZE TABLE adc_geometric COMPUTE STATISTICS AS alias_name;
```

Die Ausgabe für das obige Beispiel lautet `SUCCESSFULLY COMPLETED, alias_name`. Die Konsolenausgabe zeigt die Statistiken in der Antwort auf den Befehl zur Tabellenanalyse für die Statistikberechnung nicht an. Um die detaillierten Ergebnisse anzuzeigen, müssen Sie eine SELECT-Abfrage für den Aliasnamen oder die Statistik-ID verwenden.

## Anzeigen der Ausgabe berechneter Statistiken {#view-output-of-computed-statistics}

Wenn Sie im Voraus keinen Aliasnamen angeben, generiert der Abfragedienst automatisch einen Namen für `Statistics ID`, der dem Format `<tableName_stats_{incremental_number}>` entspricht. Wenn ein Aliasname angegeben wird, erscheint er in der Spalte `Statistics ID`.

Ein Ausgabebeispiel für eine `COMPUTE STATISTICS`-Abfrage lautet wie folgt:

```console
| Statistics ID         | 
| --------------------- |
| adc_geometric_stats_1 |
(1 row)
```

Sie können dann **die berechneten Statistiken direkt abfragen**, indem Sie die `Statistics ID` referenzieren. Mit der folgenden Beispielanweisung können Sie die vollständige Ausgabe anzeigen, wenn Sie `Statistics ID` oder den Aliasnamen verwenden.

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

Mit dem Befehl `SHOW STATISTICS` können Sie die Metadaten für alle in der Sitzung erstellten temporären Statistiken anzeigen. Mithilfe dieses Befehls können Sie den Umfang Ihrer statistischen Analyse verfeinern.

Eine Beispielausgabe von `SHOW STATISTICS` wird unten angezeigt.

```console
      statsId         |   tableName   | columnSet |         filterContext       |      timestamp
----------------------+---------------+-----------+-----------------------------+--------------------
adc_geometric_stats_1 | adc_geometric |   (age)   |                             | 25/06/2023 09:22:26
demo_table_stats_1    |  demo_table   |    (*)    |       ((age > 25))          | 25/06/2023 12:50:26
age_stats             | castedtitanic |   (age)   | ((age > 25) AND (age < 40)) | 25/06/2023 09:22:26
```

Nachfolgend finden Sie eine Beschreibung der Metadaten-Spaltennamen.

| Spaltenname | Beschreibung |
|---|---|
| `statsId` | Diese ID verweist auf die temporäre Statistiktabelle, die mit dem Befehl `COMPUTE STATISTICS` erstellt wurde. |
| `tableName` | Die ursprüngliche Tabelle, die für die Analyse verwendet wird. |
| `columnSet` | Eine Liste aller Spalten, die speziell für die Analyse ausgewählt wurden. Ein leerer Wert zeigt an, dass alle Spalten analysiert wurden. Weitere Informationen finden Sie im Abschnitt [Begrenzen von Spalten](#limit-included-columns). |
| `filterContext` | Eine Liste aller auf die Analyse angewendeten Filter. |
| `timestamp` | Alle chronologischen Filter, die auf Ihre Datenanalyse angewendet werden, um sich auf einen bestimmten Zeitraum zu konzentrieren. Weitere Einzelheiten finden Sie im Abschnitt [Zeitstempel-Filterbedingungen](#filter-condition). |

Sie können die Statistik-ID oder den Aliasnamen verwenden, um die berechneten Statistiken mit einer SELECT-Anweisung jederzeit innerhalb dieser Sitzung nachzuschlagen. Die Statistik-ID und die generierten Statistiken sind nur für diese bestimmte Sitzung gültig und können nicht über verschiedene PSQL-Sitzungen hinweg aufgerufen werden. Die berechneten Statistiken sind derzeit nicht persistent. Weitere Einzelheiten finden Sie im Abschnitt [Anzeigen der Ausgabe Ihrer berechneten Statistiken](#view-output-of-computed-statistics).

## Begrenzen der eingeschlossenen Spalten {#limit-included-columns}

Um Ihre Analyse zu fokussieren, können Sie Statistiken für bestimmte Spalten des Datensatzes berechnen, indem Sie diese mit ihrem Namen referenzieren. Verwenden Sie die Syntax `FOR COLUMNS (<col1>, <col2>)`, um bestimmte Spalten als Ziel festzulegen. Im folgenden Beispiel werden Statistiken für die Spalten `commerce`, `id` und `timestamp` für den Datensatz `tableName` berechnet.

```sql
ANALYZE TABLE tableName COMPUTE STATISTICS FOR columns (commerce, id, timestamp);
```

Sie können die Statistiken für jede Stammebene oder verschachtelte Spalte berechnen. Das folgende Beispiel veranschaulicht diese Verweise.

```sql
ANALYZE TABLE adcgeometric COMPUTE STATISTICS FOR columns (commerce, commerce.purchases.value, commerce.productListAdds.value);
```

## Hinzufügen einer Zeitstempel-Filterbedingung {#filter-condition}

Um die Analyse Ihrer Spalten auf der Grundlage der chronologischen Reihenfolge zu konzentrieren, können Sie eine Zeitstempel-Filterbedingung hinzufügen. Diese Bedingung kann verwendet werden, um historische Daten herauszufiltern oder Ihre Datenanalyse auf einen bestimmten Zeitraum zu konzentrieren. Mit dem Befehl `FILTERCONTEXT` werden basierend auf der von Ihnen angegebenen Filterbedingung Statistiken für eine Teilmenge des Datensatzes berechnet.

Im folgenden Beispiel werden Statistiken für alle Spalten des Datensatzes `tableName` berechnet, wobei der Spaltenzeitstempel Werte zwischen dem angegebenen Bereich `2023-04-01 00:00:00` und `2023-04-05 00:00:00` aufweist.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR ALL COLUMNS;
```

Sie können die Spaltenbegrenzung und den Filter kombinieren, um sehr spezifische Rechenabfragen für Ihre Datensatzspalten zu erstellen. Beispielsweise werden mit der folgenden Abfrage Statistiken zu den Spalten `commerce`, `id` und `timestamp` für den Datensatz `tableName` berechnet, wobei der Spaltenzeitstempel Werte zwischen dem angegebenen Bereich zwischen `2023-04-01 00:00:00` und `2023-04-05 00:00:00` aufweist.

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS FOR columns (commerce, id, timestamp);
```

## Nächste Schritte {#next-steps}

Durch Lesen dieses Dokuments können Sie jetzt besser verstehen, wie Sie mit einer SQL-Abfrage Statistiken auf Spaltenebene für einen ADLS-Datensatz generieren. Es wird empfohlen, das [SQl-Syntaxhandbuch](../sql/syntax.md) zu lesen, um weitere Funktionen des Adobe Experience Platform-Abfrage-Service kennenzulernen.
