---
title: Abgeleitete Datensätze mit SQL erstellen
description: Erfahren Sie, wie Sie mit SQL einen abgeleiteten Datensatz erstellen, der für Profile aktiviert ist, und wie Sie den Datensatz für das Echtzeit-Kundenprofil und den Segmentierungsdienst verwenden.
exl-id: bb1a1d8d-4662-40b0-857a-36efb8e78746
source-git-commit: 5bf54374773fd95ae1c40dd00b5dbe633031b70e
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 2%

---

# Erstellen abgeleiteter Datensätze mit SQL

Erfahren Sie, wie Sie mit SQL-Abfragen Daten aus vorhandenen Datensätzen bearbeiten und transformieren können, um einen abgeleiteten Datensatz zu erstellen, der für Profile aktiviert ist. Dieser Workflow bietet eine effiziente, alternative Methode zum Erstellen abgeleiteter Datensätze für Ihre geschäftlichen Anwendungsfälle des Echtzeit-Kundenprofils.

In diesem Dokument werden verschiedene praktische SQL-Erweiterungen beschrieben, die einen abgeleiteten Datensatz zur Verwendung mit dem Echtzeit-Kundenprofil generieren. Der Workflow vereinfacht den Prozess, den Sie andernfalls über verschiedene API-Aufrufe oder Interaktionen mit der Platform-Benutzeroberfläche durchführen müssten.

In der Regel würde das Generieren und Veröffentlichen eines abgeleiteten Datensatzes für das Echtzeit-Kundenprofil die folgenden Schritte umfassen:

* Erstellen Sie einen Identitäts-Namespace, falls noch kein vorhanden ist.
* Erstellen Sie bei Bedarf den Datentyp, um den abgeleiteten Datensatz zu speichern.
* Erstellen Sie eine Feldergruppe mit diesem Datentyp, um die abgeleiteten Datensatzinformationen zu speichern.
* Erstellen oder weisen Sie eine primäre Identitätsspalte mit dem zuvor erstellten Namespace zu.
* Erstellen Sie ein Schema mit der zuvor erstellten Feldergruppe und dem zuvor erstellten Datentyp.
* Erstellen Sie mit Ihrem Schema einen neuen Datensatz und aktivieren Sie ihn bei Bedarf für das Profil.
* Markieren Sie optional einen Datensatz als profilaktiviert.

Nach Abschluss der oben genannten Schritte können Sie den Datensatz ausfüllen. Wenn Sie den Datensatz für Profil aktiviert haben, können Sie auch Segmente erstellen, die auf den neuen Datensatz verweisen, und mit der Erstellung von Einblicken beginnen.

Mit Query Service können Sie alle oben aufgeführten Aktionen mithilfe von SQL-Abfragen durchführen. Dies umfasst bei Bedarf Änderungen an Ihren Datensätzen und Feldergruppen.

## Erstellen einer Tabelle mit einer Option, um sie für ein Profil zu aktivieren {#enable-dataset-for-profile}

>[!NOTE]
>
>Bei der unten bereitgestellten SQL-Abfrage wird von der Verwendung eines bereits vorhandenen Namespace ausgegangen.

Verwenden Sie eine &quot;Tabelle als Auswahl erstellen&quot;(CTAS)-Abfrage, um einen Datensatz zu erstellen, Datentypen zuzuweisen, eine primäre Identität festzulegen, ein Schema zu erstellen und ihn als profilaktiviert zu markieren. Die folgende SQL-Beispielanweisung erstellt einen Datensatz und stellt ihn für Real-time Customer Data Platform (Real-Time CDP) zur Verfügung. Ihre SQL-Abfrage entspricht dem Format, das im folgenden Beispiel gezeigt wird:

```sql
CREATE TABLE <your_table_name> [IF NOT EXISTS] (fieldname <your_data_type> primary identity namespace <your_namespace>, [field_name2 <your_data_type>]) [WITH(LABEL='PROFILE')];
```

Folgende Datentypen werden unterstützt: boolean, date, datetime, text, float, bigint, integer, map, array sowie structure/row.

Der unten stehende SQl-Codeblock bietet Beispiele zum Definieren von Struktur-/Zeilen-, Zuordnungs- und Array-Datentypen. Zeile eins zeigt die Zeilensyntax. Zeile 2 zeigt die Syntax der Zuordnung und Zeile 3 die Syntax des Arrays.

```sql {line-numbers="true"}
ROW (Column_name <data_type> [, column name <data_type> ]*)
MAP <data_type, data_type>
ARRAY <data_type>
```

Alternativ können Datensätze auch über die Platform-Benutzeroberfläche für das Profil aktiviert werden. Weitere Informationen zum Markieren eines Datensatzes als für ein Profil aktiviert finden Sie in der Dokumentation [Aktivieren eines Datensatzes für das Echtzeit-Kundenprofil ](../../../catalog/datasets/user-guide.md#enable-profile) .

In der folgenden Beispielabfrage wird der Datensatz `decile_table` mit `id` als primäre Identitätsspalte erstellt und hat den Namespace `IDFA`. Es verfügt auch über ein Feld mit dem Namen `decile1Month` des Zuordnungs-Datentyps. Die erstellte Tabelle (`decile_table`) ist für das Profil aktiviert.

```sql
CREATE TABLE decile_table (id text PRIMARY KEY NAMESPACE 'IDFA', 
            decile1Month map<text, integer>) WITH (label='PROFILE');
```

Bei erfolgreicher Ausführung der Abfrage wird die Datensatz-ID an die Konsole zurückgegeben, wie im Beispiel unten dargestellt.

```console
Created Table DataSet Id
>
637fd84969ba291e62dba79f
(1 row)
```

Verwenden Sie `label='PROFILE'` für einen `CREATE TABLE` -Befehl, um einen profilaktivierten Datensatz zu erstellen. Die Funktion `upsert` ist standardmäßig aktiviert. Die `upsert` -Funktion kann mit dem Befehl `ALTER` überschrieben werden, wie im folgenden Beispiel gezeigt.

```sql
ALTER TABLE <your_table_name> DROP label upsert;
```

Weitere Informationen zur Verwendung des Befehls [ALTER TABLE](../../sql/syntax.md#alter-table) und des Befehls [label als Teil einer CTAS-Abfrage](../../sql/syntax.md#create-table-as-select) finden Sie in der SQl-Syntaxdokumentation .

## Konstrukte, die bei der Verwaltung von abgeleiteten Datensätzen über SQL helfen

Die unten beschriebenen Funktionen sind bei der Verwaltung von abgeleiteten Datensätzen über SQL von großem Vorteil.

### Vorhandene Datensätze ändern, damit sie für das Profil aktiviert werden {#enable-existing-dataset-for-profile}

Das SQL-Konstrukt ALTER TABLE kann verwendet werden, um vorhandene Datensätze für das Profil zu aktivieren. Dazu muss ein profilaktiviertes Tag sowohl zum Schema als auch zum entsprechenden Datensatz hinzugefügt werden.

```sql
ALTER TABLE your_decile_table ADD label 'PROFILE';
```

>[!NOTE]
>
>Bei erfolgreicher Ausführung des Befehls `ALTER TABLE` gibt die Konsole `ALTER SUCCESS` zurück.

### Primäre Identität zu einem vorhandenen Datensatz hinzufügen {#add-primary-identity}

Markieren Sie eine vorhandene Spalte in einem Datensatz als primären Identitätssatz. Andernfalls tritt ein Fehler auf. Um eine primäre Identität mithilfe von SQL festzulegen, verwenden Sie das unten dargestellte Abfrageformat.

```sql
ALTER TABLE <your_table_name> ADD CONSTRAINT primary identity NAMESPACE
```

Beispiel:

```sql
ALTER TABLE test1_dataset ADD CONSTRAINT PRIMARY KEY(id2) NAMESPACE 'IDFA';
```

Im bereitgestellten Beispiel ist `id2` eine vorhandene Spalte in `test1_dataset`.

### Datensatz für Profil deaktivieren {#disable-dataset-for-profile}

Wenn Sie Ihre Tabelle für Profilzwecke deaktivieren möchten, müssen Sie den DROP-Befehl verwenden. Unten finden Sie eine SQL-Beispielanweisung, die `DROP` verwendet.

```sql
ALTER TABLE table_name DROP LABEL 'PROFILE';
```

Beispiel:

```sql
ALTER TABLE decile_table DROP label 'PROFILE';
```

Diese SQL-Anweisung bietet eine effiziente alternative Methode zur Verwendung eines API-Aufrufs. Weitere Informationen finden Sie in der Dokumentation zum [Deaktivieren eines Datensatzes für die Verwendung mit Real-Time CDP mithilfe der Datensatz-API](../../../catalog/datasets/enable-upsert.md#disable-the-dataset-for-profile).

### Zulassen der Aktualisierung und des Einfügens von Funktionen für Ihren Datensatz {#enable-upsert-functionality-for-dataset}

Mit dem UPSERT-Befehl können Sie einen neuen Datensatz einfügen oder vorhandene Daten in eine Tabelle aktualisieren. Insbesondere können Sie eine vorhandene Zeile aktualisieren, wenn ein angegebener Wert bereits in einer Tabelle vorhanden ist, oder eine neue Zeile einfügen, wenn der angegebene Wert noch nicht vorhanden ist.

Unten finden Sie eine Beispielanweisung, die das richtige Format verwendet.

```sql
ALTER TABLE table_name ADD LABEL 'UPSERT';
```

Beispiel:

```sql
ALTER TABLE table_with_a_decile ADD label 'UPSERT';
```

Diese SQL-Anweisung bietet eine effiziente alternative Methode zur Verwendung eines API-Aufrufs. Weitere Informationen finden Sie in der Dokumentation zum Aktivieren eines Datensatzes für die Verwendung mit Real-Time CDP und UPSERT mithilfe der Datensatz-API](../../../catalog/datasets/enable-upsert.md#enable-the-dataset).[

### Deaktivieren Sie die Aktualisierungs- und Einfügefunktionen für Ihren Datensatz. {#disable-upsert-functionality-for-dataset}

Dieser Befehl deaktiviert die Möglichkeit, Zeilen zu aktualisieren und in Ihren Datensatz einzufügen.

Unten finden Sie eine Beispielanweisung, die das richtige Format verwendet.

```sql
ALTER TABLE table_name DROP LABEL 'UPSERT';
```

Beispiel:

```sql
ALTER TABLE table_with_a_decile DROP label 'UPSERT';
```

### Zusätzliche Tabelleninformationen für jede Tabelle anzeigen {#show-labels-for-tables}

Zusätzliche Metadaten werden für profilaktivierte Datensätze beibehalten. Verwenden Sie den Befehl `SHOW TABLES` , um eine zusätzliche Spalte `labels` anzuzeigen, die Informationen zu allen Beschriftungen enthält, die mit Tabellen verknüpft sind.

Nachfolgend finden Sie ein Beispiel für die Ausgabe dieses Befehls:

```sql
       name          |        dataSetId         |     dataSet    | description | labels 
---------------------+--------------------------+----------------+-------------+----------
 luma_midvalues      | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues     | 5c86b896b3c162151785b43c | Luma midValues |             | false
 table_with_a_decile | 5c86b896b3c162151785b43c | Luma midValues |             | 'UPSERT', 'PROFILE'
(3 rows)
```

Aus dem Beispiel können Sie sehen, dass `table_with_a_decile` für das Profil aktiviert und mit Bezeichnungen wie [&#39;UPSERT&#39;](#enable-upsert-functionality-for-dataset), [&#39;PROFILE&#39;](#enable-existing-dataset-for-profile) angewendet wurde, wie zuvor beschrieben.

### Erstellen einer Feldergruppe mit SQL

Feldergruppen können jetzt mithilfe von SQL erstellt werden. Dies bietet eine Alternative zur Verwendung des Schema-Editors in der Platform-Benutzeroberfläche oder zum Ausführen eines API-Aufrufs für die Schemaregistrierung.

Unten finden Sie eine Beispielanweisung zum Erstellen einer Feldergruppe.

```sql
CREATE FIELDGROUP <field_group_name> [IF NOT EXISTS]  (field_name <data_type> primary identity namespace <namespace>, [field_name_2 >data_type>]) [ WITH(LABEL='PROFILE') ];
```

>[!IMPORTANT]
>
>Die Feldergruppenerstellung über SQL schlägt fehl, wenn die Markierung `label` nicht in der Anweisung angegeben ist oder die Feldergruppe bereits existiert.
>Stellen Sie sicher, dass die Abfrage eine &quot;`IF NOT EXISTS`&quot;-Klausel enthält, um zu verhindern, dass die Abfrage fehlschlägt, da die Feldergruppe bereits vorhanden ist.

Ein Beispiel für die reale Welt könnte in etwa dem unten gezeigten ähneln.

```sql
CREATE FIELDGROUP field_group_for_test123 (decile1Month map<text, integer>, decile3Month map<text, integer>, decile6Month map<text, integer>, decile9Month map<text, integer>, decile12Month map<text, integer>, decilelietime map<text, integer>) WITH (LABEL-'PROFILE');
```

Bei erfolgreicher Ausführung dieser Anweisung wird die erstellte Feldergruppen-ID zurückgegeben. Beispiel `c731a1eafdfdecae1683c6dca197c66ed2c2b49ecd3a9525`.

Weitere Informationen zu alternativen Methoden finden Sie in der Dokumentation zum [Erstellen einer neuen Feldergruppe im Schema Editor](../../../xdm/ui/resources/field-groups.md#create) oder zur Verwendung der [Schema Registry-API](../../../xdm/api/field-groups.md#create) .

### Eine Feldergruppe ablegen

Gelegentlich kann es erforderlich sein, eine Feldergruppe aus der Schema Registry zu entfernen. Führen Sie dazu den Befehl `DROP FIELDGROUP` mit der Feldergruppen-ID aus.

```sql
DROP FIELDGROUP [IF EXISTS] <your_field_group_id>;
```

Beispiel:

```sql
DROP FIELDGROUP field_group_for_test123;
```

>[!IMPORTANT]
>
>Das Löschen einer Feldergruppe über SQL schlägt fehl, wenn die Feldergruppe nicht vorhanden ist. Stellen Sie sicher, dass die Anweisung eine `IF EXISTS` -Klausel enthält, um zu verhindern, dass die Abfrage fehlschlägt.

### Alle Feldgruppennamen und -IDs für Ihre Tabellen anzeigen

Der Befehl `SHOW FIELDGROUPS` gibt eine Tabelle zurück, die den Namen, die fieldgroupId und den Eigentümer der Tabellen enthält.

Nachfolgend finden Sie ein Beispiel für die Ausgabe dieses Befehls:

```sql
       name                      |        fieldgroupId                             |     owner      |
---------------------------------+-------------------------------------------------+-----------------
 AEP Mobile Lifecycle Details    | _experience.aep-mobile-lifecycle-details        | Luma midValues |
 AEP Web SDK ExperienceEvent     | _experience.aep-web-sdk-experienceevent         | Luma midValues |
 AJO Classification Fields       | _experience.journeyOrchestration.classification | Luma midValues |
 AJO Entity Fields               | _experience.customerJourneyManagement.entities  | Luma midValues |
(4 rows)
```

## Nächste Schritte

Nachdem Sie dieses Dokument gelesen haben, können Sie besser verstehen, wie Sie SQL verwenden, um ein Profil zu erstellen und aktivierten Datensatz basierend auf abgeleiteten Datensätzen zu aktualisieren. Sie können diesen Datensatz jetzt mit Batch-Aufnahme-Workflows verwenden, um Ihre Profildaten zu aktualisieren. Um mehr über die Aufnahme von Daten in Adobe Experience Platform zu erfahren, lesen Sie bitte zunächst die [Übersicht zur Datenaufnahme](../../../ingestion/home.md).
