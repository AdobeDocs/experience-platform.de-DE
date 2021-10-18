---
title: Beispiel für anonyme Blockabfragen
description: Der anonyme Block ist eine SQL-Syntax, die von Adobe Experience Platform Query Service unterstützt wird und die die effiziente Ausführung einer Abfragesequenz ermöglicht
exl-id: ec497475-9d2b-43aa-bcf4-75a430590496
source-git-commit: 50d4b49b43cf7882612e6de54cbbd680d549665a
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 1%

---

# Beispielabfragen für anonymen Baustein

Adobe Experience Platform Query Service unterstützt anonyme Bausteine. Mit der Funktion für anonyme Bausteine können Sie eine oder mehrere SQL-Anweisungen ketten, die nacheinander ausgeführt werden. Sie ermöglichen auch die Möglichkeit der Ausnahmebehandlung.

Die Funktion für anonyme Bausteine bietet eine effiziente Möglichkeit, eine Abfolge von Vorgängen oder Abfragen durchzuführen. Die Kette von Abfragen innerhalb des Blocks kann als Vorlage gespeichert und für eine bestimmte Zeit oder ein bestimmtes Intervall geplant werden. Diese Abfragen können zum Schreiben und Anhängen von Daten verwendet werden, um einen neuen Datensatz zu erstellen. Sie werden normalerweise dort verwendet, wo Sie eine Abhängigkeit haben.

Die Tabelle enthält eine Aufschlüsselung der Hauptabschnitte des Blocks: Ausführung und Ausnahmebehandlung. Die Abschnitte werden durch die Keywords `BEGIN`, `END` und `EXCEPTION` definiert.

| sein muss | description |
|---|---|
| execution | Ein ausführbarer Abschnitt beginnt mit dem Keyword `BEGIN` und endet mit dem Keyword `END`. Alle Anweisungen, die in den `BEGIN` - und `END` -Keywords enthalten sind, werden nacheinander ausgeführt und stellen sicher, dass nachfolgende Abfragen erst ausgeführt werden, nachdem die vorherige Abfrage in der Sequenz abgeschlossen wurde. |
| Ausnahmebehandlung | Der optionale Abschnitt zur Ausnahmebehandlung beginnt mit dem Keyword `EXCEPTION`. Sie enthält den Code zum Erfassen und Verarbeiten von Ausnahmen, falls eine der SQL-Anweisungen im Ausführungsabschnitt fehlschlägt. Wenn eine der Abfragen fehlschlägt, wird der gesamte Block angehalten. |

Beachten Sie, dass ein Block eine ausführbare Anweisung ist und daher in anderen Blöcken verschachtelt werden kann.

>[!NOTE]
>
> Es wird dringend empfohlen, Ihre Abfragen für kleinere Datensätze zu testen und sicherzustellen, dass sie erwartungsgemäß funktionieren. Wenn bei einer Abfrage ein Syntaxfehler auftritt, wird die Ausnahme ausgelöst und der gesamte Block wird abgebrochen. Nachdem Sie die Integrität der Abfragen überprüft haben, können Sie mit ihrer Verkettung beginnen. Dadurch wird sichergestellt, dass der Block wie erwartet funktioniert, bevor Sie ihn in Betrieb nehmen.

## Anonyme Beispiel-Blockabfragen

Die folgende Abfrage zeigt ein Beispiel für die Verkettung von SQL-Anweisungen. Weitere Informationen zur verwendeten SQL-Syntax finden Sie im Dokument [SQL-Syntax in Query Service](../sql/syntax.md) .

```SQL
$$BEGIN
     
    CREATE TABLE ADLS_TABLE_A AS SELECT * FROM ADLS_TABLE_1....;
    ....
    CREATE TABLE ADLS_TABLE_D AS SELECT * FROM ADLS_TABLE_C....;
     
    EXCEPTION WHEN OTHER THEN SET @ret = SELECT 'ERROR';
     
END$$;
```

<!-- The block below uses `SET` to persist the result of a select query with a variable. It is used in the anonymous block to store the response from a query as a local variable for use with the `SNAPSHOT` feature. -->

Im folgenden Beispiel behält `SET` das Ergebnis einer `SELECT`-Abfrage in der angegebenen lokalen Variablen bei. Die Variable wird auf den anonymen Block übertragen.

Die Snapshot-ID wird als lokale Variable (`@current_sid`) gespeichert. Sie wird dann in der nächsten Abfrage verwendet, um Ergebnisse basierend auf SNAPSHOT aus demselben Datensatz/derselben Tabelle zurückzugeben.

Ein Datenbank-Snapshot ist eine schreibgeschützte statische Ansicht einer SQL Server-Datenbank. Weitere [Informationen zur Snapshot-Klausel](../sql/syntax.md#SNAPSHOT-clause) finden Sie in der SQL-Syntaxdokumentation.

```SQL
$$BEGIN                                             
  SET @current_sid = SELECT parent_id  FROM (SELECT history_meta('your_table_name')) WHERE  is_current = true;
  CREATE temp table abcd_temp_table AS SELECT count(1) FROM your_table_name  SNAPSHOT SINCE @current_sid;                                                                                                     
END$$;
```

## Nächste Schritte

Durch Lesen dieses Dokuments erhalten Sie jetzt ein klares Verständnis der anonymen Bausteine und ihrer Struktur. [Weiterführende Informationen zur Ausführung](./writing-queries.md) von Abfragen finden Sie im Handbuch zur Ausführung von Abfragen in Query Service.

Weitere Beispiele für Abfragen, die in Query Service verwendet werden können, finden Sie in den Handbüchern zu [Adobe Analytics-Beispielabfragen](./adobe-analytics.md), [Adobe Target-Beispielabfragen](./adobe-target.md) oder [ExperienceEvent-Beispielabfragen](./experience-event-queries.md).
