---
title: Anonymer Block in Query Service
description: Der anonyme Baustein ist eine SQL-Syntax, die von Adobe Experience Platform Query Service unterstützt wird und mit der Abfragen effizient ausgeführt werden können.
exl-id: ec497475-9d2b-43aa-bcf4-75a430590496
source-git-commit: 43c5bdbfa93872ba54bde72bbea8201b73e9dfee
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 1%

---

# Anonymer Block in Query Service

Adobe Experience Platform Query Service unterstützt anonyme Bausteine. Mit der Funktion für anonyme Bausteine können Sie eine oder mehrere SQL-Anweisungen ketten, die nacheinander ausgeführt werden. Sie ermöglichen auch die Möglichkeit der Ausnahmebehandlung.

Die Funktion für anonyme Bausteine bietet eine effiziente Möglichkeit, eine Abfolge von Vorgängen oder Abfragen durchzuführen. Die Kette von Abfragen innerhalb des Blocks kann als Vorlage gespeichert und für eine bestimmte Zeit oder ein bestimmtes Intervall geplant werden. Diese Abfragen können zum Schreiben und Anhängen von Daten verwendet werden, um einen neuen Datensatz zu erstellen. Sie werden normalerweise dort verwendet, wo Sie eine Abhängigkeit haben.

>[!IMPORTANT]
>
>Die Planung von Abfragen mithilfe anonymer Bausteine ist derzeit nur über das [!DNL Query Service] API. Weitere Informationen finden Sie in der Dokumentation für [vollständige Anweisungen zur Planung von Abfragen über die API](../api/scheduled-queries.md).

Die Tabelle enthält eine Aufschlüsselung der Hauptabschnitte des Blocks: Ausführung und Ausnahmebehandlung. Die Abschnitte werden durch die Schlüsselwörter definiert `BEGIN`, `END`und `EXCEPTION`.

| sein muss | description |
|---|---|
| execution | Ein ausführbarer Abschnitt beginnt mit dem Suchbegriff `BEGIN` und endet mit dem Keyword `END`. Alle Anweisungen, die in der `BEGIN` und `END` Suchbegriffe werden nacheinander ausgeführt und stellt sicher, dass nachfolgende Abfragen erst ausgeführt werden, nachdem die vorherige Abfrage in der Sequenz abgeschlossen wurde. |
| Ausnahmebehandlung | Der optionale Abschnitt zur Ausnahmebehandlung beginnt mit dem Schlüsselwort . `EXCEPTION`. Sie enthält den Code zum Erfassen und Verarbeiten von Ausnahmen, falls eine der SQL-Anweisungen im Ausführungsabschnitt fehlschlägt. Wenn eine der Abfragen fehlschlägt, wird der gesamte Block angehalten. |

Beachten Sie, dass ein Block eine ausführbare Anweisung ist und daher in anderen Blöcken verschachtelt werden kann.

>[!NOTE]
>
> Es wird dringend empfohlen, Ihre Abfragen für kleinere Datensätze zu testen und sicherzustellen, dass sie erwartungsgemäß funktionieren. Wenn bei einer Abfrage ein Syntaxfehler auftritt, wird die Ausnahme ausgelöst und der gesamte Block wird abgebrochen. Nachdem Sie die Integrität der Abfragen überprüft haben, können Sie mit ihrer Verkettung beginnen. Dadurch wird sichergestellt, dass der Block wie erwartet funktioniert, bevor Sie ihn in Betrieb nehmen.

## Anonyme Beispiel-Blockabfragen

Die folgende Abfrage zeigt ein Beispiel für die Verkettung von SQL-Anweisungen. Siehe [SQL-Syntax in Query Service](../sql/syntax.md) für weitere Informationen zur verwendeten SQL-Syntax.

```SQL
$$ BEGIN
    CREATE TABLE ADLS_TABLE_A AS SELECT * FROM ADLS_TABLE_1....;
    ....
    CREATE TABLE ADLS_TABLE_D AS SELECT * FROM ADLS_TABLE_C....; 
    EXCEPTION WHEN OTHER THEN SET @ret = SELECT 'ERROR';
END
$$;
```

Im folgenden Beispiel: `SET` behält das Ergebnis eines `SELECT` Abfrage in der angegebenen lokalen Variablen. Die Variable wird auf den anonymen Block übertragen.

Die Snapshot-ID wird als lokale Variable (`@current_sid`). Sie wird dann in der nächsten Abfrage verwendet, um Ergebnisse basierend auf SNAPSHOT aus demselben Datensatz/derselben Tabelle zurückzugeben.

Ein Datenbank-Snapshot ist eine schreibgeschützte statische Ansicht einer SQL Server-Datenbank. Für mehr [Informationen zur Snapshot-Klausel](../sql/syntax.md#SNAPSHOT-clause) Weitere Informationen finden Sie in der Dokumentation zur SQL-Syntax .

```SQL
$$ BEGIN                                             
  SET @current_sid = SELECT parent_id  FROM (SELECT history_meta('your_table_name')) WHERE  is_current = true;
  CREATE temp table abcd_temp_table AS SELECT count(1) FROM your_table_name  SNAPSHOT SINCE @current_sid;                                                                                           
END
$$;
```

## Nächste Schritte

Durch Lesen dieses Dokuments erhalten Sie jetzt ein klares Verständnis der anonymen Bausteine und ihrer Struktur. [Weitere Informationen zur Ausführung von Abfragen](./writing-queries.md), lesen Sie bitte das Handbuch zur Ausführung von Abfragen in Query Service.

Sie sollten auch [Verwendung des anonymen Bausteins mit dem Muster für das inkrementelle Laden](./incremental-load.md) , um die Abfrageeffizienz zu erhöhen.
