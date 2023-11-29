---
title: Anonymer Block in Query Service
description: Der anonyme Block ist eine SQL-Syntax, die von Adobe Experience Platform Query Service unterstützt wird und mit der Abfragen effizient ausgeführt werden können.
exl-id: ec497475-9d2b-43aa-bcf4-75a430590496
source-git-commit: 99cd69234006e6424be604556829b77236e92ad7
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 100%

---

# Anonymer Block in Query Service

Adobe Experience Platform Query Service unterstützt anonyme Blöcke. Mit der Funktion für anonyme Blöcke können Sie eine oder mehrere SQL-Anweisungen verketten, die nacheinander ausgeführt werden. Sie beinhalten auch die Möglichkeit der Ausnahmebehandlung.

Die Funktion für anonyme Blöcke bietet eine effiziente Möglichkeit, um mehrere Vorgänge oder Abfragen nacheinander auszuführen. Die Kette von Abfragen innerhalb des Blocks kann als Vorlage gespeichert und zur Ausführung zu einer bestimmten Zeit oder in einem bestimmten Intervall geplant werden. Diese Abfragen können zum Schreiben und Anhängen von Daten verwendet werden, um einen neuen Datensatz zu erstellen. Sie werden normalerweise im Falle von Abhängigkeiten verwendet.

>[!IMPORTANT]
>
>Die Planung von Abfragen mithilfe anonymer Blöcke ist derzeit nur über die [!DNL Query Service]-API möglich. Weitere Informationen finden Sie in der Dokumentation für [vollständige Anweisungen zum Planen von Abfragen über die API](../api/scheduled-queries.md).

Die folgende Tabelle ist nach den Hauptabschnitten des Blocks unterteilt: Ausführung und Ausnahmebehandlung. Die Abschnitte sind durch die Schlüsselwörter `BEGIN`, `END` und `EXCEPTION` definiert.

| Abschnitt | Beschreibung |
|---|---|
| Ausführung | Ein ausführbarer Abschnitt beginnt mit dem Schlüsselwort `BEGIN` und endet mit dem Schlüsselwort `END`. Alle Anweisungen zwischen den Schlüsselwörtern `BEGIN` und `END` werden nacheinander ausgeführt. Dabei wird sichergestellt, dass nachfolgende Abfragen erst ausgeführt werden, nachdem die vorherige Abfrage in der Sequenz abgeschlossen wurde. |
| Ausnahmebehandlung | Der optionale Abschnitt zur Ausnahmebehandlung beginnt mit dem Schlüsselwort `EXCEPTION`. Er enthält den Code zum Erfassen und Verarbeiten von Ausnahmen, falls eine der SQL-Anweisungen im Ausführungsabschnitt fehlschlägt. Wenn eine der Abfragen fehlschlägt, wird der gesamte Block angehalten. |

Beachten Sie, dass ein Block eine ausführbare Anweisung ist und daher in anderen Blöcken verschachtelt werden kann.

>[!NOTE]
>
> Es wird dringend empfohlen, Ihre Abfragen mit kleineren Datensätzen zu testen und sicherzustellen, dass sie erwartungsgemäß funktionieren. Wenn eine Abfrage einen Syntaxfehler enthält, wird die Ausnahme ausgelöst und der gesamte Block wird abgebrochen. Nachdem Sie die Integrität der Abfragen überprüft haben, können Sie mit ihrer Verkettung beginnen. Dadurch wird sichergestellt, dass der Block wie erwartet funktioniert, bevor Sie ihn in Betrieb nehmen.

## Anonyme Beispiel-Blockabfragen

Die folgende Abfrage zeigt ein Beispiel für die Verkettung von SQL-Anweisungen. Weitere Informationen zur verwendeten SQL-Syntax finden Sie unter [SQL-Syntax in Query Service](../sql/syntax.md).

```SQL
$$ BEGIN
    CREATE TABLE ADLS_TABLE_A AS SELECT * FROM ADLS_TABLE_1....;
    ....
    CREATE TABLE ADLS_TABLE_D AS SELECT * FROM ADLS_TABLE_C....; 
    EXCEPTION WHEN OTHER THEN SET @ret = SELECT 'ERROR';
END
$$;
```

Im folgenden Beispiel behält `SET` das Ergebnis einer `SELECT`-Abfrage in der angegebenen lokalen Variablen. Die Variable wird dem anonymen Block zugeordnet.

Die Snapshot-ID wird als lokale Variable (`@current_sid`) gespeichert. Sie wird dann in der nächsten Abfrage verwendet, um Ergebnisse basierend auf SNAPSHOT aus demselben Datensatz/derselben Tabelle zurückzugeben.

Ein Datenbank-Snapshot ist eine schreibgeschützte statische Ansicht einer SQL Server-Datenbank. Weitere [Informationen zur Snapshot-Klausel](../sql/syntax.md#SNAPSHOT-clause) finden Sie in der SQL-Syntax-Dokumentation.

```SQL
$$ BEGIN                                             
  SET @current_sid = SELECT parent_id  FROM (SELECT history_meta('your_table_name')) WHERE  is_current = true;
  CREATE temp table abcd_temp_table AS SELECT count(1) FROM your_table_name  SNAPSHOT SINCE @current_sid;                                                                                           
END
$$;
```

## Nächste Schritte

Durch das Lesen dieses Dokuments verstehen Sie nun anonyme Blöcke und ihre Struktur besser. [Weitere Informationen zur Ausführung von Abfragen](../best-practices/writing-queries.md) finden Sie im Handbuch zum Ausführen von Abfragen in Query Service.

Sie sollten auch das Thema über die [Verwendung des anonymen Blocks mit dem Design-Muster zum inkrementellen Laden](./incremental-load.md) lesen, um die Abfrageeffizienz zu erhöhen.
