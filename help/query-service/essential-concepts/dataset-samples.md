---
title: Datensatzbeispiele
description: Mit den Beispieldatensätzen des Abfrage-Service können Sie explorative Abfragen zu Big Data durchführen. Dies verkürzt die Verarbeitungszeit, verringert jedoch die Abfragegenauigkeit. In diesem Handbuch erfahren Sie, wie Sie Ihre Beispiele für die annähernde Abfrageverarbeitung verwalten können
exl-id: 9e676d7c-c24f-4234-878f-3e57bf57af44
source-git-commit: 13779e619345c228ff2a1981efabf5b1917c4fdb
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 76%

---

# Datensatzbeispiele

Der Abfrage-Service von Adobe Experience Platform bietet Beispieldatensätze als Teil der Funktionen zur annähernden Abfrageverarbeitung. Beispieldatensätze werden mit einheitlichen Zufallsproben aus vorhandenen [!DNL Azure Data Lake Storage](ADLS)-Datensätzen erstellt, die nur einen geringen Prozentsatz der Datensätze aus dem Original verwenden. Dieser Prozentsatz wird als Stichprobenrate bezeichnet. Durch die Anpassung der Stichprobenrate zur Gleichgewichtskontrolle zwischen Genauigkeit und Verarbeitungszeit können Sie explorative Abfragen zu Big Data durchführen, wobei die Verarbeitungszeit auf Kosten der Genauigkeit der Abfrage erheblich verkürzt wird.

Da viele Benutzende keine genaue Antwort für einen Aggregatvorgang für einen Datensatz benötigen, ist das Ausgeben einer annähernden Abfrage zur Rückgabe einer ungefähren Antwort für explorative Abfragen über große Datensätze effizienter. Da Beispieldatensätze nur einen geringen Prozentsatz der Daten aus dem ursprünglichen Datensatz enthalten, können Sie die Abfragegenauigkeit gegen eine verbesserte Antwortzeit eintauschen. Bei der Lesezeit muss der Abfrage-Service weniger Zeilen scannen, was Ergebnisse schneller generiert als bei der Abfrage des gesamten Datensatzes.

Um Ihnen bei der Verwaltung Ihrer Beispiele für die annähernde Abfrageverarbeitung zu helfen, unterstützt der Abfrage-Service die folgenden Vorgänge für Datensatzbeispiele:

- [Erstellen einer einheitlichen Stichprobe für zufällige Datensätze.](#create-a-sample)
- [Optional Filterkriterien angeben](##optional-filter-criteria)
- [Anzeigen der Beispielliste für eine ADLS-Tabelle.](#view-list-of-samples)
- [Direktes Abfragen der Beispieldatensätze.](#query-sample-datasets)
- [Löschen eines Beispiels.](#delete-a-sample)
- Löschen der zugehörigen Beispiele, wenn die ursprüngliche ADLS-Tabelle abgelegt wird.

## Erste Schritte {#get-started}

Um die in diesem Dokument beschriebenen Funktionen zum Erstellen und Löschen von Näherungsabfragen zu verwenden, müssen Sie das Sitzungs-Flag auf `true`. Geben Sie in der Befehlszeile des Abfrage-Editors oder Ihres PSQL-Clients die `SET aqp=true;` Befehl.

>[!NOTE]
>
>Sie müssen das Sitzungs-Flag jedes Mal aktivieren, wenn Sie sich bei Platform anmelden.

![Der Abfrage-Editor mit dem hervorgehobenen Befehl &quot;SET aqp=true;&quot;.](../images/essential-concepts/set-session-flag.png)

## Erstellen einer einheitlichen Stichprobe zufälliger Datensätze {#create-a-sample}

Verwenden Sie den Bfehl `ANALYZE TABLE <table_name> TABLESAMPLE SAMPLERATE x` mit einem Datensatznamen, um eine einheitliche zufällige Stichprobe aus diesem Datensatz zu erstellen.

Die Stichprobenrate ist der Prozentsatz der Datensätze, die aus dem ursprünglichen Datensatz entnommen wurden. Sie können die Stichprobenrate mithilfe der Keywords `TABLESAMPLE SAMPLERATE` steuern. In diesem Beispiel entspricht der Wert 5,0 einer Stichprobenrate von 50 %. Ein Wert von 2,5 würde 25 % entsprechen usw.

>[!IMPORTANT]
>
>Das System lässt für jeden Datensatz maximal fünf Stichproben zu. Wenn Sie versuchen, einen sechsten Beispieldatensatz zu erstellen, wird auf dem Bildschirm eine Fehlermeldung angezeigt, die besagt, dass die Stichprobenbegrenzung erreicht wurde.

```sql
ANALYZE TABLE example_dataset_name TABLESAMPLE SAMPLERATE 5.0;
```

## Optional Filterkriterien angeben {#optional-filter-criteria}

Sie können auch ein Filterkriterium für Ihre einheitlichen zufälligen Proben festlegen. Auf diese Weise können Sie ein Muster erstellen, das auf der gefilterten Untergruppe der analysierten Tabelle basiert.

Beim Erstellen eines Beispiels wird zunächst der optionale Filter angewendet, dann wird das Beispiel aus der gefilterten Ansicht des Datensatzes erstellt. Ein Datensatzbeispiel mit angewendetem Filter folgt dem folgenden Abfrageformat:

```sql
ANALYZE TABLE <tableToAnalyze> TABLESAMPLE FILTERCONTEXT (<filter_condition>) SAMPLERATE X.Y;
ANALYZE TABLE <tableToAnalyze> TABLESAMPLE FILTERCONTEXT (<filter_condition_1> AND/OR <filter_condition_2>) SAMPLERATE X.Y;
ANALYZE TABLE <tableToAnalyze> TABLESAMPLE FILTERCONTEXT (<filter_condition_1> AND (<filter_condition_2> OR <filter_condition_3>)) SAMPLERATE X.Y;
```

Praktische Beispiele für diesen Typ von gefiltertem Beispieldatensatz sind:

```sql
Analyze TABLE large_table TABLESAMPLE FILTERCONTEXT (month(to_timestamp(timestamp)) in ('8', '9')) SAMPLERATE 10;
Analyze TABLE large_table TABLESAMPLE FILTERCONTEXT (month(to_timestamp(timestamp)) in ('8', '9') AND product.name = "product1") SAMPLERATE 10;
Analyze TABLE large_table TABLESAMPLE FILTERCONTEXT (month(to_timestamp(timestamp)) in ('8', '9') AND (product.name = "product1" OR product.name = "product2")) SAMPLERATE 10;
```

In den bereitgestellten Beispielen lautet der Tabellenname `large_table`, lautet die Filterbedingung für die ursprüngliche Tabelle . `month(to_timestamp(timestamp)) in ('8', '9')`und die Stichprobenrate (X % der gefilterten Daten) beträgt, in diesem Fall `10`.

## Anzeigen der Liste der Stichproben {#view-list-of-samples}

Verwenden Sie die Funktion `sample_meta()`, um die Liste der mit einer ADLS-Tabelle verknüpften Stichproben anzuzeigen.

```sql
SELECT sample_meta('example_dataset_name')
```

Die Liste der Datensatzbeispiele wird im Format des folgenden Beispiels angezeigt.

```shell
                  sample_table_name                  |    sample_dataset_id     |    parent_dataset_id     | sample_type | sampling_rate | sample_num_rows |       created      
-----------------------------------------------------+--------------------------+--------------------------+-------------+---------------+-----------------+---------------------
 x5e5cd8ea0a83c418a8ef0928_uniform_4_0_percent_ughk7 | 62ff19853d338f1c07b18965 | 5e5cd8ea0a83c418a8ef0928 | uniform     |           4.0 |             391 | 19/08/2022 05:03:01
(1 row)
```

## Abfragen des Beispieldatensatzes {#query-sample-datasets}

Verwenden Sie den `{EXAMPLE_DATASET_NAME}`, um Beispieltabellen direkt abzufragen. Alternativ können Sie das Keyword `WITHAPPROXIMATE` an das Ende einer Abfrage anhängen. Der Abfrage-Service verwendet automatisch die zuletzt erstellte Stichprobe.

```sql
SELECT * FROM example_dataset_name WITHAPPROXIMATE;
```

## Löschen von Datensatzbeispielen {#delete-a-sample}

Mit dem Löschvorgang können Sie neue Stichproben erstellen, sobald die maximale Begrenzung von fünf Datensatzstichproben erreicht wurde.

```sql
DROP TABLE SAMPLE x5e5cd8ea0a83c418a8ef0928_uniform_2_0_percent_bnhmc;
```

>[!NOTE]
>
>Wenn Sie mehrere Beispieldatensätze aus einem ursprünglichen ADLS-Datensatz haben, werden beim Ablegen des Originals auch alle zugehörigen Stichproben gelöscht.
