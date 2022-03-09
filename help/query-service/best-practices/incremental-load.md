---
title: Inkrementelle Belastung in Query Service
description: Die inkrementelle Ladefunktion verwendet sowohl anonyme Block- als auch Snapshot-Funktionen, um eine nahezu Echtzeit-Lösung zum Verschieben von Daten aus dem Data Lake in Ihr Data Warehouse zu bieten, ohne übereinstimmende Daten zu ignorieren.
exl-id: 1418d041-29ce-4153-90bf-06bd8da8fb78
source-git-commit: 7087991c7a3daad57c5acd92a20c7024a1152c7e
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 2%

---

# Inkrementelle Belastung in Query Service

Das inkrementelle Lastdesign-Muster ist eine Lösung für die Datenverwaltung. Das Muster verarbeitet nur Informationen im Datensatz, die seit der letzten Ausführung des Ladevorgangs erstellt oder geändert wurden.

Inkrementelle Belastung verwendet verschiedene Funktionen, die vom Adobe Experience Platform Query Service bereitgestellt werden, wie anonyme Bausteine und Momentaufnahmen. Dieses Designmuster erhöht die Verarbeitungseffizienz, da alle bereits aus der Quelle verarbeiteten Daten übersprungen werden. Sie kann sowohl mit Streaming- als auch mit der Batch-Datenverarbeitung verwendet werden.

Dieses Dokument enthält eine Reihe von Anweisungen zum Erstellen eines Designmusters für die inkrementelle Verarbeitung. Diese Schritte können als Vorlage für Ihre eigenen inkrementellen Datenladeabfragen verwendet werden.

## Erste Schritte

Die SQL-Beispiele in diesem Dokument erfordern ein Verständnis der Funktionen des anonymen Blocks und der Momentaufnahme. Es wird empfohlen, die [Anonyme Beispielblockabfragen](./anonymous-block.md) Dokumentation und [Snapshot-Klausel](../sql/syntax.md#snapshot-clause) Dokumentation.

Eine Anleitung zu den in diesem Handbuch verwendeten Terminologie finden Sie im Abschnitt [SQL-Syntaxhandbuch](../sql/syntax.md).

## Inkrementelle Ladedaten

Die folgenden Schritte zeigen, wie Sie Daten mithilfe von Momentaufnahmen und der Funktion für anonyme Bausteine erstellen und inkrementell laden können. Das Designmuster kann als Vorlage für Ihre eigene Abfolge von Abfragen verwendet werden.

1 Erstellen Sie eine `checkpoint_log` -Tabelle, um den neuesten Schnappschuss zu verfolgen, der zur erfolgreichen Verarbeitung von Daten verwendet wurde. Die Tracking-Tabelle (`checkpoint_log` in diesem Beispiel) muss zuerst initialisiert werden auf `null` , um einen Datensatz schrittweise zu verarbeiten.

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

2 Füllen Sie die `checkpoint_log` mit einem leeren Datensatz für den Datensatz, der eine inkrementelle Verarbeitung erfordert. `DIM_TABLE_ABC` ist der Datensatz, der im folgenden Beispiel verarbeitet werden soll. Erstmalige Verarbeitung `DIM_TABLE_ABC`, die `last_snapshot_id` initialisiert wird als `null`. Auf diese Weise können Sie den gesamten Datensatz beim ersten Mal und danach schrittweise verarbeiten.

```SQL
INSERT INTO
   checkpoint_log
   SELECT
       'DIM_TABLE_ABC' process_name,
       'SUCCESSFUL' process_status,
       cast(NULL AS string) last_snapshot_id,
       CURRENT_TIMESTAMP process_timestamp;
```

3 Nächste, initialisieren `DIM_TABLE_ABC_Incremental` enthält verarbeitete Ausgabe von `DIM_TABLE_ABC`. Der anonyme Block im **erforderlich** Der Ausführungsabschnitt des SQL-Beispiels unten, wie in den Schritten 1 bis 4 beschrieben, wird nacheinander ausgeführt, um Daten inkrementell zu verarbeiten.

1. Legen Sie die `from_snapshot_id` , der angibt, wo die Verarbeitung beginnt. Die `from_snapshot_id` im Beispiel aus der `checkpoint_log` Tabelle zur Verwendung mit `DIM_TABLE_ABC`. Beim ersten Ausführen wird die Snapshot-ID `null` bedeutet, dass der gesamte Datensatz verarbeitet wird.
2. Legen Sie die `to_snapshot_id` als aktuelle Momentaufnahme-ID der Quelltabelle (`DIM_TABLE_ABC`). Im Beispiel wird dies aus der Metadatentabelle der Quelltabelle abgefragt.
3. Verwenden Sie die `CREATE` Zu erstellender Suchbegriff `DIM_TABLE_ABC_Incremenal` als Zieltabelle. Die Zieltabelle behält die verarbeiteten Daten aus dem Quelldatensatz (`DIM_TABLE_ABC`). Dadurch können die verarbeiteten Daten aus der Quelltabelle zwischen `from_snapshot_id` und `to_snapshot_id`, um schrittweise an die Zieltabelle angehängt zu werden.
4. Aktualisieren Sie die `checkpoint_log` mit der `to_snapshot_id` für die Quelldaten, die `DIM_TABLE_ABC` erfolgreich verarbeitet wurde.
5. Wenn eine der sequenziell ausgeführten Abfragen des anonymen Blocks fehlschlägt, wird die **optional** Ausnahmeabschnitt ausgeführt wird. Dadurch wird ein Fehler zurückgegeben und der Prozess wird beendet.

>[!NOTE]
>
>Die `history_meta('source table name')` ist eine praktische Methode, mit der Sie auf verfügbare Momentaufnahmen in einem Datensatz zugreifen können.

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

4 Verwenden Sie die inkrementelle Datenladelogik im Beispiel für anonyme Bausteine unten, um zu ermöglichen, dass neue Daten aus dem Quelldatensatz (seit dem letzten Zeitstempel) verarbeitet und regelmäßig an die Zieltabelle angehängt werden. Im Beispiel ändern sich die Daten in `DIM_TABLE_ABC` wird verarbeitet und an `DIM_TABLE_ABC_incremental`.

>[!NOTE]
>
> `_ID` ist der Primäre Schlüssel in beiden `DIM_TABLE_ABC_Incremental` und `SELECT history_meta('DIM_TABLE_ABC')`.

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

Diese Logik kann auf jede Tabelle angewendet werden, um inkrementelle Lasten durchzuführen.

## Abgelaufene Momentaufnahmen

>[!IMPORTANT]
>
>Momentaufnahmen-Metadaten laufen nach ab **two** Tage. Eine abgelaufene Momentaufnahme macht die Logik des oben angegebenen Skripts ungültig.

Um das Problem einer abgelaufenen Snapshot-ID zu beheben, fügen Sie den folgenden Befehl am Anfang des anonymen Blocks ein. Die folgende Codezeile überschreibt die `@from_snapshot_id` mit der frühesten verfügbaren `snapshot_id` aus Metadaten.

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

Durch Lesen dieses Dokuments sollten Sie besser verstehen, wie Sie anonyme Block- und Snapshot-Funktionen verwenden können, um inkrementelle Ladevorgänge durchzuführen, und diese Logik auf Ihre eigenen spezifischen Abfragen anwenden können. Allgemeine Hinweise zur Ausführung von Abfragen finden Sie im [Handbuch zum Ausführen von Abfragen in Query Service](./writing-queries.md).
