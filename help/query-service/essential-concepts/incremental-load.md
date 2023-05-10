---
title: Inkrementelles Laden im Abfrage-Service
description: Die inkrementelle Ladefunktion verwendet Funktionen sowohl für anonyme Blöcke als auch für Momentaufnahmen, um eine nahezu in Echtzeit entstehende Lösung zum Verschieben von Daten aus dem Data Lake in Ihr Data Warehouse zu bieten, ohne übereinstimmende Daten zu berücksichtigen.
exl-id: 1418d041-29ce-4153-90bf-06bd8da8fb78
source-git-commit: 11a947addce65887385c983ac81d884fb4244291
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 100%

---

# Inkrementelles Laden im Abfrage-Service

Das Designmuster für inkrementelles Laden ist eine Lösung für die Datenverwaltung. Das Muster verarbeitet nur Informationen im Datensatz, die seit der letzten Ladeausführung erstellt oder geändert wurden.

Inkrementelles Laden verwendet verschiedene Funktionen, die der Adobe Experience Platform-Abfrage-Service bereitstellt, wie anonyme Blöcke und Momentaufnahmen. Dieses Designmuster erhöht die Verarbeitungseffizienz, da alle bereits verarbeiteten Daten aus der Quelle übersprungen werden. Es kann sowohl bei der Streaming- als auch bei der Batch-Datenverarbeitung verwendet werden.

Dieses Dokument enthält eine Reihe von Anweisungen zum Erstellen eines Designmusters für die inkrementelle Verarbeitung. Diese Schritte können als Vorlage für die Erstellung Ihrer eigenen inkrementellen Datenladeabfragen verwendet werden.

## Erste Schritte

Die SQL-Beispiele in diesem Dokument erfordern ein Verständnis der Funktionen anonymer Blöcke und der Momentaufnahme. Es wird empfohlen, die Dokumentationen [Beispielabfragen für anonyme Blöcke](./anonymous-block.md) und [Momentaufnahme-Klausel](../sql/syntax.md#snapshot-clause) zu lesen.

Eine Erklärung zu den in diesem Handbuch verwendeten Begriffen finden Sie im [Handbuch zur SQL-Syntax](../sql/syntax.md).

## Inkrementelles Laden von Daten

Die folgenden Schritte zeigen, wie Sie Daten mithilfe von Momentaufnahmen und der Funktion für anonyme Blöcke erstellen und inkrementell laden können. Das Designmuster kann als Vorlage für Ihre eigene Abfolge von Abfragen verwendet werden.

1. Erstellen Sie eine `checkpoint_log`-Tabelle, um die letzte Momentaufnahme festzuhalten, die zur erfolgreichen Verarbeitung von Daten verwendet wurde. Die Tracking-Tabelle (`checkpoint_log` in diesem Beispiel) muss zuerst auf `null` initialisiert werden, um einen Datensatz inkrementell zu verarbeiten.

   ```SQL
   DROP TABLE IF EXISTS checkpoint_log;
   CREATE TABLE  checkpoint_log AS
   SELECT
      cast(NULL AS string) process_name,
      cast(NULL AS string) process_status,
      cast(NULL AS string) last_snapshot_id,
      cast(NULL AS TIMESTAMP) process_timestamp
      WHERE false;
   ```

1. Füllen Sie die `checkpoint_log`-Tabelle mit einer leeren Eingabe für den Datensatz, wodurch eine inkrementelle Verarbeitung erfordert wird. `DIM_TABLE_ABC` ist der Datensatz, der im folgenden Beispiel verarbeitet werden soll. Bei der erstmaligen Verarbeitung von `DIM_TABLE_ABC` ist `last_snapshot_id` als `null` initialisiert. Auf diese Weise können Sie den gesamten Datensatz beim ersten Mal und danach inkrementell verarbeiten.

   ```SQL
   INSERT INTO
      checkpoint_log
      SELECT
         'DIM_TABLE_ABC' process_name,
         'SUCCESSFUL' process_status,
         cast(NULL AS string) last_snapshot_id,
         CURRENT_TIMESTAMP process_timestamp;
   ```

1.  Als Nächstes initialisieren Sie `DIM_TABLE_ABC_Incremental`, um verarbeitete Ausgaben von `DIM_TABLE_ABC` zu enthalten. Der anonyme Block im **erforderlichen** Ausführungsabschnitt des folgenden SQL-Beispiels wird, wie in den Schritten 1 bis 4 beschrieben, sequenziell ausgeführt, um Daten inkrementell zu verarbeiten.

   1. Legen Sie die `from_snapshot_id` fest, die angibt, wo die Verarbeitung beginnt. Die `from_snapshot_id` im Beispiel wird aus der `checkpoint_log`-Tabelle zur Verwendung mit `DIM_TABLE_ABC` abgefragt. Beim ersten Ausführen ist die Momentaufnahme-ID `null`, was bedeutet, dass der gesamte Datensatz verarbeitet wird.
   1. Legen Sie die `to_snapshot_id` als aktuelle Momentaufnahme-ID der Quellentabelle fest (`DIM_TABLE_ABC`). Im Beispiel wird dies aus der Metadatentabelle der Quelltabelle abgefragt.
   1. Verwenden Sie das `CREATE`-Keyword, um `DIM_TABLE_ABC_Incremenal` als Zieltabelle zu erstellen. Die Zieltabelle bewahrt die verarbeiteten Daten aus dem Quelldatensatz auf (`DIM_TABLE_ABC`). Dadurch können die verarbeiteten Daten aus der Quelltabelle zwischen `from_snapshot_id` und `to_snapshot_id` inkrementell an die Zieltabelle angehängt werden.
   1. Aktualisieren Sie die `checkpoint_log`-Tabelle mit der `to_snapshot_id` für die Quelldaten, die `DIM_TABLE_ABC` erfolgreich verarbeitet hat.
   1. Wenn eine der sequenziell ausgeführten Abfragen des anonymen Blocks fehlschlägt, wird der **optionale** Ausnahmeabschnitt ausgeführt. Dadurch wird ein Fehler zurückgegeben und der Prozess beendet.

   >[!NOTE]
   >
   >`history_meta('source table name')` ist eine praktische Methode, um auf verfügbare Momentaufnahmen in einem Datensatz zuzugreifen.

   ```SQL
   $$ BEGIN
       SET @from_snapshot_id = SELECT coalesce(last_snapshot_id, 'HEAD') FROM checkpoint_log a JOIN
                               (SELECT MAX(process_timestamp)process_timestamp FROM checkpoint_log
                                   WHERE process_name = 'DIM_TABLE_ABC' AND process_status = 'SUCCESSFUL' )b
                                   ON a.process_timestamp=b.process_timestamp;
       SET @to_snapshot_id = SELECT snapshot_id FROM (SELECT history_meta('DIM_TABLE_ABC')) WHERE  is_current = true;
       SET @last_updated_timestamp= SELECT CURRENT_TIMESTAMP;
       CREATE TABLE DIM_TABLE_ABC_Incremental AS
        SELECT  *  FROM DIM_TABLE_ABC SNAPSHOT BETWEEN @from_snapshot_id AND @to_snapshot_id ;
   
   INSERT INTO
      checkpoint_log
      SELECT
          'DIM_TABLE_ABC' process_name,
          'SUCCESSFUL' process_status,
         cast( @to_snapshot_id AS string) last_snapshot_id,
         cast( @last_updated_timestamp AS TIMESTAMP) process_timestamp;
   
   EXCEPTION
     WHEN OTHER THEN
       SELECT 'ERROR';
   END 
   $$;
   ```

1. Verwenden Sie die inkrementelle Datenladelogik im folgenden Beispiel für anonyme Blöcke, um zu ermöglichen, dass neue Daten (seit dem letzten Zeitstempel) aus dem Quelldatensatz verarbeitet und regelmäßig an die Zieltabelle angehängt werden. Im Beispiel werden Datenänderungen an `DIM_TABLE_ABC` verarbeitet und an `DIM_TABLE_ABC_incremental` angehängt.

   >[!NOTE]
   >
   > `_ID` ist der Primärschlüssel sowohl in `DIM_TABLE_ABC_Incremental` als auch in `SELECT history_meta('DIM_TABLE_ABC')`.

   ```SQL
   $$ BEGIN
       SET @from_snapshot_id = SELECT coalesce(last_snapshot_id, 'HEAD') FROM checkpoint_log a join
                               (SELECT MAX(process_timestamp)process_timestamp FROM checkpoint_log
                                   WHERE process_name = 'DIM_TABLE_ABC' AND process_status = 'SUCCESSFUL' )b
                                   ON a.process_timestamp=b.process_timestamp;
       SET @to_snapshot_id = SELECT snapshot_id FROM (SELECT history_meta('DIM_TABLE_ABC')) WHERE  is_current = true;
       SET @last_updated_timestamp= SELECT CURRENT_TIMESTAMP;
       INSERT INTO DIM_TABLE_ABC_Incremental
        SELECT  *  FROM DIM_TABLE_ABC SNAPSHOT BETWEEN @from_snapshot_id AND @to_snapshot_id WHERE NOT EXISTS (SELECT _id FROM DIM_TABLE_ABC_Incremental a WHERE _id=a._id);
   
   INSERT INTO
      checkpoint_log
      SELECT
          'DIM_TABLE_ABC' process_name,
          'SUCCESSFUL' process_status,
         cast( @to_snapshot_id AS string) last_snapshot_id,
         cast( @last_updated_timestamp AS TIMESTAMP) process_timestamp;
   
   EXCEPTION
     WHEN OTHER THEN
       SELECT 'ERROR';
   END
   $$;
   ```

Diese Logik kann auf jede Tabelle angewendet werden, um inkrementelles Laden durchzuführen.

## Abgelaufene Momentaufnahmen

>[!IMPORTANT]
>
>Momentaufnahmen-Metadaten laufen nach **zwei** Tagen ab. Eine abgelaufene Momentaufnahme macht die Logik des oben angegebenen Skripts ungültig.

Um das Problem einer abgelaufenen Momentaufnahme-ID zu beheben, fügen Sie den folgenden Befehl am Anfang des anonymen Blocks ein. Die folgende Codezeile überschreibt die `@from_snapshot_id` mit der frühesten verfügbaren `snapshot_id` aus Metadaten.

```SQL
SET resolve_fallback_snapshot_on_failure=true;
```

Der gesamte Codeblock sieht wie folgt aus:

```SQL
$$ BEGIN
    SET resolve_fallback_snapshot_on_failure=true;
    SET @from_snapshot_id = SELECT coalesce(last_snapshot_id, 'HEAD') FROM checkpoint_log a JOIN
                            (SELECT MAX(process_timestamp)process_timestamp FROM checkpoint_log
                                WHERE process_name = 'DIM_TABLE_ABC' AND process_status = 'SUCCESSFUL' )b
                                on a.process_timestamp=b.process_timestamp;
    SET @to_snapshot_id = SELECT snapshot_id FROM (SELECT history_meta('DIM_TABLE_ABC')) WHERE  is_current = true;
    SET @last_updated_timestamp= SELECT CURRENT_TIMESTAMP;
    INSERT INTO DIM_TABLE_ABC_Incremental
     SELECT  *  FROM DIM_TABLE_ABC SNAPSHOT BETWEEN @from_snapshot_id AND @to_snapshot_id WHERE NOT EXISTS (SELECT _id FROM DIM_TABLE_ABC_Incremental a WHERE _id=a._id);
 
Insert Into
   checkpoint_log
   SELECT
       'DIM_TABLE_ABC' process_name,
       'SUCCESSFUL' process_status,
      cast( @to_snapshot_id AS string) last_snapshot_id,
      cast( @last_updated_timestamp AS TIMESTAMP) process_timestamp;
EXCEPTION
  WHEN OTHER THEN
    SELECT 'ERROR';
END
$$;
```

## Nächste Schritte

Durch dieses Dokument sollten Sie besser verstehen, wie Sie Funktionen für anonyme Blöcke und Momentaufnahmen verwenden können, um inkrementelles Laden durchzuführen, und diese Logik auf Ihre eigenen spezifischen Abfragen anwenden können. Allgemeine Hinweise zur Ausführung von Abfragen finden Sie im [Handbuch zum Ausführen von Abfragen in Abfrage-Service](../best-practices/writing-queries.md).
