---
title: Erstellen abgeleiteter Datensätze mit SQL
description: Erfahren Sie, wie Sie SQL verwenden, um einen abgeleiteten Datensatz zu erstellen, der für Profil aktiviert ist, und wie Sie den Datensatz für das Echtzeit-Kundenprofil und den Segmentierungs-Service verwenden.
exl-id: bb1a1d8d-4662-40b0-857a-36efb8e78746
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1238'
ht-degree: 2%

---

# Erstellen abgeleiteter Datensätze mit SQL

Erfahren Sie, wie Sie mit SQL-Abfragen Daten aus vorhandenen Datensätzen bearbeiten und transformieren können, um einen abgeleiteten Datensatz zu erstellen, der für Profil aktiviert ist. Dieser Workflow bietet eine effiziente, alternative Methode zum Erstellen abgeleiteter Datensätze für Ihre geschäftlichen Anwendungsfälle des Echtzeit-Kundenprofils.

In diesem Dokument werden verschiedene praktische SQL-Erweiterungen beschrieben, die einen abgeleiteten Datensatz für die Verwendung mit dem Echtzeit-Kundenprofil generieren. Der Workflow vereinfacht den Prozess, den Sie andernfalls durch verschiedene API-Aufrufe oder Experience Platform-Benutzeroberflächeninteraktionen abschließen müssten.

Normalerweise umfasst das Generieren und Veröffentlichen eines abgeleiteten Datensatzes für das Echtzeit-Kundenprofil die folgenden Schritte:

* Erstellen Sie einen Identity-Namespace, falls noch kein Namespace vorhanden ist.
* Erstellen Sie bei Bedarf den Datentyp, um den abgeleiteten Datensatz zu speichern.
* Erstellen Sie eine Feldergruppe mit diesem Datentyp, um die abgeleiteten Datensatzinformationen zu speichern.
* Erstellen oder weisen Sie eine primäre Identitätsspalte mit dem zuvor erstellten Namespace zu.
* Erstellen Sie ein Schema mit der zuvor erstellten Feldergruppe und dem Datentyp.
* Erstellen Sie mithilfe Ihres Schemas einen neuen Datensatz und aktivieren Sie ihn bei Bedarf für das Profil.
* Optional können Sie einen Datensatz als profilaktiviert markieren.

Nachdem Sie die oben genannten Schritte ausgeführt haben, können Sie den Datensatz ausfüllen. Wenn Sie den Datensatz für das Profil aktiviert haben, können Sie auch Segmente erstellen, die auf den neuen Datensatz verweisen, und mit der Erstellung von Einblicken beginnen.

Query Service ermöglicht Ihnen, alle oben aufgeführten Aktionen mithilfe von SQL-Abfragen durchzuführen. Dazu gehört, bei Bedarf Änderungen an Ihren Datensätzen und Feldergruppen vorzunehmen.

## Erstellen einer Tabelle mit einer Option, um sie für ein Profil zu aktivieren {#enable-dataset-for-profile}

>[!NOTE]
>
>Die unten bereitgestellte SQL-Abfrage setzt die Verwendung eines bereits vorhandenen Namespace voraus.

Verwenden Sie eine Abfrage vom Typ Tabelle als Auswahl erstellen (CTAS), um einen Datensatz zu erstellen, Datentypen zuzuweisen, eine primäre Identität festzulegen, ein Schema zu erstellen und ihn als profilaktiviert zu markieren. Die folgende SQL-Beispielanweisung erstellt einen Datensatz und stellt ihn für Real-Time Customer Data Platform (Real-Time CDP) zur Verfügung. Ihre SQL-Abfrage folgt dem Format, das im folgenden Beispiel gezeigt wird:

```sql
CREATE TABLE <your_table_name> [IF NOT EXISTS] (fieldname <your_data_type> primary identity namespace <your_namespace>, [field_name2 <your_data_type>]) [WITH(LABEL='PROFILE')];
```

Die unterstützten Datentypen sind: Boolesch, Datum, Datum/Uhrzeit, Text, Gleitkommazahl, bigint, Ganzzahl, Zuordnung, Array und Struct/Row.

Der folgende SQL-Codeblock enthält Beispiele zum Definieren von Struktur-/Zeilen-, Zuordnungs- und Array-Datentypen. Zeile 1 zeigt die Zeilensyntax. Zeile zwei zeigt die Zuordnungssyntax und Zeile drei die Array-Syntax.

```sql {line-numbers="true"}
ROW (Column_name <data_type> [, column name <data_type> ]*)
MAP <data_type, data_type>
ARRAY <data_type>
```

Alternativ können Datensätze auch über die Experience Platform-Benutzeroberfläche für Profile aktiviert werden. Weitere Informationen zum Markieren eines Datensatzes als für Profil aktiviert finden Sie in der [Aktivieren eines Datensatzes für das Echtzeit-Kundenprofil](../../../catalog/datasets/user-guide.md#enable-profile).

In der folgenden Beispielabfrage wird der `decile_table` Datensatz mit `id` als primäre Identitätsspalte erstellt und weist den Namespace `IDFA` auf. Es gibt auch ein Feld namens `decile1Month` vom Datentyp Zuordnung . Die erstellte Tabelle (`decile_table`) ist für Profil aktiviert.

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

Verwenden Sie `label='PROFILE'` auf einem `CREATE TABLE`, um einen profilaktivierten Datensatz zu erstellen. Die `upsert` ist standardmäßig aktiviert. Die `upsert` kann mithilfe des Befehls `ALTER` überschrieben werden, wie im folgenden Beispiel gezeigt.

```sql
ALTER TABLE <your_table_name> DROP label upsert;
```

Weitere Informationen zur Verwendung des Befehls [ALTER TABLE](../../sql/syntax.md#alter-table) und „label“ als Teil einer CTAS[Abfrage finden Sie in der SQL](../../sql/syntax.md#create-table-as-select)Syntaxdokumentation .

## Konstrukte zur Unterstützung der Verwaltung abgeleiteter Datensätze mithilfe von SQL

Die unten beschriebenen Funktionen sind bei der Verwaltung abgeleiteter Datensätze über SQL von großem Nutzen.

### Vorhandene Datensätze ändern, damit sie für das Profil aktiviert werden {#enable-existing-dataset-for-profile}

Das SQL-Konstrukt ALTER TABLE kann verwendet werden, um vorhandene Datensätze für das Profil zu aktivieren. Dies erfordert, dass sowohl dem Schema als auch dem entsprechenden Datensatz ein profilaktiviertes Tag hinzugefügt wird.

```sql
ALTER TABLE your_decile_table ADD label 'PROFILE';
```

>[!NOTE]
>
>Bei erfolgreicher Ausführung des `ALTER TABLE`-Befehls gibt die Konsole `ALTER SUCCESS` zurück.

### Hinzufügen einer primären Identität zu einem vorhandenen Datensatz {#add-primary-identity}

Markieren Sie eine vorhandene Spalte in einem Datensatz als primären Identitätssatz. Andernfalls führt dies zu einem Fehler. Um eine primäre Identität mithilfe von SQL festzulegen, verwenden Sie das unten angezeigte Abfrageformat.

```sql
ALTER TABLE <your_table_name> ADD CONSTRAINT primary identity NAMESPACE
```

Beispiel:

```sql
ALTER TABLE test1_dataset ADD CONSTRAINT PRIMARY KEY(id2) NAMESPACE 'IDFA';
```

Im angegebenen Beispiel ist `id2` eine vorhandene Spalte in `test1_dataset`.

### Datensatz für Profil deaktivieren {#disable-dataset-for-profile}

Wenn Sie Ihre Tabelle für die Verwendung durch Profile deaktivieren möchten, müssen Sie den DROP-Befehl verwenden. Nachfolgend finden Sie eine Beispiel-SQL-Anweisung mit dem `DROP` USES .

```sql
ALTER TABLE table_name DROP LABEL 'PROFILE';
```

Beispiel:

```sql
ALTER TABLE decile_table DROP label 'PROFILE';
```

Diese SQL-Anweisung bietet eine effiziente Alternative zur Verwendung eines API-Aufrufs. Weitere Informationen finden Sie in der Dokumentation zum [Deaktivieren eines Datensatzes für die Verwendung mit Real-Time CDP mithilfe der Datasets-API](../../../catalog/datasets/enable-upsert.md#disable-the-dataset-for-profile).

### Zulassen, dass Funktionen für den Datensatz aktualisiert und eingefügt werden {#enable-upsert-functionality-for-dataset}

Mit dem Befehl UPSERT können Sie einen neuen Datensatz einfügen oder vorhandene Daten in einer Tabelle aktualisieren. Insbesondere können Sie eine vorhandene Zeile aktualisieren, wenn ein angegebener Wert bereits in einer Tabelle vorhanden ist, oder eine neue Zeile einfügen, wenn der angegebene Wert noch nicht vorhanden ist.

Nachfolgend finden Sie eine Beispielanweisung mit dem richtigen Format.

```sql
ALTER TABLE table_name ADD LABEL 'UPSERT';
```

Beispiel:

```sql
ALTER TABLE table_with_a_decile ADD label 'UPSERT';
```

Diese SQL-Anweisung bietet eine effiziente Alternative zur Verwendung eines API-Aufrufs. Weitere Informationen finden Sie in der Dokumentation zum [Aktivieren eines Datensatzes für die Verwendung mit Real-Time CDP und UPSERT mithilfe der Datasets-API](../../../catalog/datasets/enable-upsert.md#enable-the-dataset).

### Funktion zum Aktualisieren und Einfügen für Ihren Datensatz deaktivieren {#disable-upsert-functionality-for-dataset}

Dieser Befehl deaktiviert die Möglichkeit, Zeilen zu aktualisieren und in Ihren Datensatz einzufügen.

Nachfolgend finden Sie eine Beispielanweisung mit dem richtigen Format.

```sql
ALTER TABLE table_name DROP LABEL 'UPSERT';
```

Beispiel:

```sql
ALTER TABLE table_with_a_decile DROP label 'UPSERT';
```

### Zusätzliche Tabelleninformationen für jede Tabelle anzeigen {#show-labels-for-tables}

Zusätzliche Metadaten werden für profilaktivierte Datensätze beibehalten. Verwenden Sie den Befehl `SHOW TABLES` , um eine zusätzliche `labels` anzuzeigen, die Informationen zu Beschriftungen bereitstellt, die mit Tabellen verknüpft sind.

Nachfolgend finden Sie ein Beispiel für die Ausgabe dieses Befehls:

```sql
       name          |        dataSetId         |     dataSet    | description | labels 
|---------------------+--------------------------+----------------+-------------+----------
 luma_midvalues      | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues     | 5c86b896b3c162151785b43c | Luma midValues |             | false
 table_with_a_decile | 5c86b896b3c162151785b43c | Luma midValues |             | 'UPSERT', 'PROFILE'
(3 rows)
```

Im Beispiel sehen Sie, dass `table_with_a_decile` für das Profil aktiviert und mit Kennzeichnungen wie [&#39;UPSERT&#39;](#enable-upsert-functionality-for-dataset), [&#39;PROFILE&#39;](#enable-existing-dataset-for-profile) wie zuvor beschrieben angewendet wurde.

### Erstellen einer Feldergruppe mit SQL

Feldergruppen können jetzt mithilfe von SQL erstellt werden. Dies bietet eine Alternative zur Verwendung des Schema-Editors in der Experience Platform-Benutzeroberfläche oder einem API-Aufruf an die Schemaregistrierung.

Nachfolgend finden Sie eine Beispielanweisung zum Erstellen einer Feldergruppe.

```sql
CREATE FIELDGROUP <field_group_name> [IF NOT EXISTS]  (field_name <data_type> primary identity namespace <namespace>, [field_name_2 >data_type>]) [ WITH(LABEL='PROFILE') ];
```

>[!IMPORTANT]
>
>Die Feldergruppenerstellung über SQL schlägt fehl, wenn das `label`-Flag nicht in der Anweisung angegeben wird oder wenn die Feldergruppe bereits vorhanden ist.
>>Stellen Sie sicher, dass die Abfrage eine `IF NOT EXISTS`-Klausel enthält, um zu vermeiden, dass die Abfrage fehlschlägt, da die Feldergruppe bereits vorhanden ist.

Ein reales Beispiel könnte in etwa wie unten dargestellt aussehen.

```sql
CREATE FIELDGROUP field_group_for_test123 (decile1Month map<text, integer>, decile3Month map<text, integer>, decile6Month map<text, integer>, decile9Month map<text, integer>, decile12Month map<text, integer>, decilelietime map<text, integer>) WITH (LABEL-'PROFILE');
```

Bei erfolgreicher Ausführung dieser Anweisung wird die erstellte Feldergruppen-ID zurückgegeben. Beispiel `c731a1eafdfdecae1683c6dca197c66ed2c2b49ecd3a9525`.

Weitere Informationen zu alternativen Methoden finden Sie in [ Dokumentation zum Erstellen einer neuen Feldergruppe ](../../../xdm/ui/resources/field-groups.md#create) Schema-Editor oder [ Verwendung ](../../../xdm/api/field-groups.md#create) Schema-Registrierungs-API .

### Feldergruppe ablegen

Gelegentlich kann es erforderlich sein, eine Feldergruppe aus der Schemaregistrierung zu entfernen. Dazu führen Sie den Befehl `DROP FIELDGROUP` mit der Feldgruppen-ID aus.

```sql
DROP FIELDGROUP [IF EXISTS] <your_field_group_id>;
```

Beispiel:

```sql
DROP FIELDGROUP field_group_for_test123;
```

>[!IMPORTANT]
>
>Das Löschen einer Feldergruppe über SQL schlägt fehl, wenn die Feldergruppe nicht vorhanden ist. Stellen Sie sicher, dass die Anweisung eine `IF EXISTS`-Klausel enthält, um ein Fehlschlagen der Abfrage zu vermeiden.

### Alle Namen und IDs der Feldergruppen für die Tabellen anzeigen

Der Befehl `SHOW FIELDGROUPS` gibt eine Tabelle zurück, die den Namen, die Feldgruppen-ID und den Eigentümer der Tabellen enthält.

Nachfolgend finden Sie ein Beispiel für die Ausgabe dieses Befehls:

```sql
       name                      |        fieldgroupId                             |     owner      |
|---------------------------------+-------------------------------------------------+-----------------
 AEP Mobile Lifecycle Details    | _experience.aep-mobile-lifecycle-details        | Luma midValues |
 AEP Web SDK ExperienceEvent     | _experience.aep-web-sdk-experienceevent         | Luma midValues |
 AJO Classification Fields       | _experience.journeyOrchestration.classification | Luma midValues |
 AJO Entity Fields               | _experience.customerJourneyManagement.entities  | Luma midValues |
(4 rows)
```

## Nächste Schritte

Nach dem Lesen dieses Dokuments wissen Sie besser, wie Sie SQL verwenden können, um ein Profil und einen upsert-aktivierten Datensatz basierend auf abgeleiteten Datensätzen zu erstellen. Sie können diesen Datensatz jetzt mit Batch-Aufnahme-Workflows verwenden, um Aktualisierungen an Ihren Profildaten vorzunehmen. Um mehr über die Aufnahme von Daten in Adobe Experience Platform zu erfahren, lesen Sie bitte zunächst die [Übersicht zur Datenaufnahme](../../../ingestion/home.md).
