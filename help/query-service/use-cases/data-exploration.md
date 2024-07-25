---
title: Erkunden, Fehlerbehebung und Überprüfen der Batch-Erfassung mit SQL
description: Erfahren Sie, wie Sie den Datenerfassungsprozess in Adobe Experience Platform verstehen und verwalten. In diesem Dokument wird beschrieben, wie Sie Batches überprüfen und erfasste Daten abfragen.
exl-id: 8f49680c-42ec-488e-8586-50182d50e900
source-git-commit: 692a061e3b2facbfafc65f966832230187f5244d
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 0%

---

# Batch-Erfassung mit SQL analysieren, beheben und überprüfen

In diesem Dokument wird beschrieben, wie Sie Datensätze in erfassten Batches mit SQL überprüfen und validieren. In diesem Dokument lernen Sie Folgendes:

- Zugreifen auf Datensatz-Batch-Metadaten
- Fehlerbehebung und Gewährleistung der Datenintegrität durch Abfragen von Batches

>[!NOTE]
>
>Einige Screenshots in diesem Handbuch stammen aus [!DNL DBVisualizer]. Informationen zum [Verbinden von Query Service mit DBVisualizer](../clients/dbvisulaizer.md) oder anderen [BI-Tools von Drittanbietern](../clients/overview.md) finden Sie in der verknüpften Dokumentation.

## Voraussetzungen

Um Ihr Verständnis der in diesem Dokument behandelten Konzepte zu vermitteln, sollten Sie über die folgenden Themen verfügen:

- **Datenerfassung**: In der [Übersicht über die Datenerfassung](../../ingestion/home.md) erfahren Sie mehr über die Grundlagen der Datenerfassung in der Plattform, einschließlich der verschiedenen beteiligten Methoden und Prozesse.
- **Batch-Erfassung**: Informationen zu den grundlegenden Konzepten der Batch-Erfassung finden Sie in der [Übersicht zur Batch-Aufnahme-API](../../ingestion/batch-ingestion/overview.md) . Insbesondere, was ein &quot;Batch&quot;ist und wie er im Datenerfassungsprozess von Platform funktioniert.
- **Systemmetadaten in Datensätzen**: In der [Übersicht über den Katalogdienst](../../catalog/home.md) erfahren Sie, wie Systemmetadatenfelder zum Verfolgen und Abfragen erfasster Daten verwendet werden.
- **Experience-Datenmodell (XDM)**: In der [Übersicht über die Schemas-Benutzeroberfläche](../../xdm/ui/overview.md) und den [&#39;Grundlagen der Schemakomposition&#39;](../../xdm/schema/composition.md) erfahren Sie mehr über XDM-Schemas und darüber, wie sie die Struktur und das Format der in Platform erfassten Daten darstellen und validieren.

## Zugreifen auf Datensatz-Batch-Metadaten {#access-dataset-batch-metadata}

Verwenden Sie den SQL-Befehl `set drop_system_columns=false` in Ihrem Abfrage-Editor, um sicherzustellen, dass in den Abfrageergebnissen Systemspalten (Metadatenspalten) enthalten sind. Dadurch wird das Verhalten Ihrer SQL-Abfragesitzung konfiguriert. Diese Eingabe muss wiederholt werden, wenn Sie eine neue Sitzung starten.

Führen Sie anschließend eine SELECT all -Anweisung aus, um die Ergebnisse aus dem Datensatz anzuzeigen, z. B. `select * from movie_data`, um die Systemfelder des Datensatzes anzuzeigen. Die Ergebnisse enthalten zwei neue Spalten auf der rechten Seite `_acp_system_metadata` und `_ACP_BATCHID`. Die Metadatenspalten `_acp_system_metadata` und `_ACP_BATCHID` helfen bei der Identifizierung der logischen und physischen Partitionen der aufgenommenen Daten.

![Die DBVisualizer-Benutzeroberfläche mit der Tabelle &quot;movie_data&quot;und den zugehörigen Metadatenspalten, die angezeigt und hervorgehoben werden.](../images/use-cases/movie_data-table-with-metadata-columns.png)

Bei der Erfassung von Daten in Platform wird ihnen anhand der eingehenden Daten eine logische Partition zugewiesen. Diese logische Partition wird durch `_acp_system_metadata.sourceBatchId` dargestellt. Diese ID hilft bei der logischen Gruppierung und Identifizierung der Daten-Batches, bevor sie verarbeitet und gespeichert werden.

Nachdem die Daten verarbeitet und in den Data Lake aufgenommen wurden, wird ihnen eine physische Partition zugewiesen, die durch `_ACP_BATCHID` dargestellt wird. Diese ID spiegelt die tatsächliche Speicherpartition im Data Lake wider, in dem sich die erfassten Daten befinden.

### Verwenden Sie SQL, um logische und physische Partitionen zu verstehen. {#understand-partitions}

Um zu verstehen, wie die Daten nach der Aufnahme gruppiert und verteilt werden, verwenden Sie die folgende Abfrage, um die Anzahl unterschiedlicher physischer Partitionen (`_ACP_BATCHID`) für jede logische Partition (`_acp_system_metadata.sourceBatchId`) zu zählen.

```SQL
SELECT  _acp_system_metadata, COUNT(DISTINCT _ACP_BATCHID) FROM movie_data
GROUP BY _acp_system_metadata
```

Die Ergebnisse dieser Abfrage werden in der Abbildung unten dargestellt.

![Die Ergebnisse einer Abfrage, die die Anzahl unterschiedlicher physischer Partitionen für jede logische Partition anzeigt.](../images/use-cases/logical-and-physical-partition-count.png)

Diese Ergebnisse zeigen, dass die Anzahl der Eingangs-Batches nicht notwendigerweise mit der Anzahl der Ausgabe-Batches übereinstimmt, da das System bestimmt, wie die Daten am effizientesten im Data Lake gestapelt und gespeichert werden.

Für die Zwecke dieses Beispiels wird davon ausgegangen, dass Sie eine CSV-Datei in Platform aufgenommen und einen Datensatz mit dem Namen `drug_checkout_data` erstellt haben.

Die Datei &quot;`drug_checkout_data`&quot; ist ein tief verschachtelter Satz von 35.000 Datensätzen. Verwenden Sie die SQL-Anweisung &quot;`SELECT * FROM drug_orders;`&quot;, um eine Vorschau des ersten Datensatzes im JSON-basierten `drug_orders` Datensatz anzuzeigen.

Das folgende Bild zeigt eine Vorschau der Datei und ihrer Datensätze.

![Eine Vorschau des ersten Datensatzes im JSON-basierten Datensatz &quot;droid_orders&quot;.](../images/use-cases/drug-orders-preview.png)

### Verwenden Sie SQL, um Einblicke in den Batch-Erfassungsvorgang zu generieren. {#sql-insights-on-batch-ingestion}

Verwenden Sie die nachstehende SQL-Anweisung, um Einblicke in die Gruppierung und Verarbeitung der Eingabedatensätze durch den Datenerfassungsprozess zu geben.

```sql
SELECT _acp_system_metadata,
       Count(DISTINCT _acp_batchid) AS numoutputbatches,
       Count(_acp_batchid)          AS recordcount
FROM   drug_orders
GROUP  BY _acp_system_metadata 
```

Die Abfrageergebnisse sind in der Abbildung unten dargestellt.

![Eine Tabelle, die die Verteilung der Art und Weise anzeigt, wie Eingabe-Batches mit Datensatzzählungen gleichzeitig gemeistert wurden.](../images/use-cases/distribution-of-input-batches.png)

Die Ergebnisse zeigen die Effizienz und das Verhalten des Datenerfassungsprozesses. Obwohl drei Eingangs-Batches erstellt wurden - mit jeweils 2000, 24000 und 9000 Datensätzen -, blieb bei der Kombination und Deduplizierung der Datensätze nur ein einziger Batch erhalten.

>[!NOTE]
>
>Alle Datensätze, die in einem Datensatz sichtbar sind, sind diejenigen, die erfolgreich erfasst wurden. Eine erfolgreiche Batch-Erfassung bedeutet nicht, dass alle Datensätze vorhanden sind, die von der Quelleingabe gesendet wurden. Sie müssen nach Fehlern bei der Datenerfassung suchen, um die Batches/Datensätze zu finden, in denen die Daten nicht erfasst wurden.

## Validieren eines Batches mit SQL {#validate-a-batch-with-SQL}

Überprüfen Sie anschließend die Datensätze, die mit SQL in den Datensatz aufgenommen wurden.

>[!TIP]
>
>Um die Batch-Kennung und die mit dieser Batch-Kennung verknüpften Abfragedatensätze abzurufen, müssen Sie zunächst einen Batch in Platform erstellen. Wenn Sie den Prozess selbst testen möchten, können Sie CSV-Daten in Platform erfassen. Lesen Sie das Handbuch zum [Zuordnen einer CSV-Datei zu einem vorhandenen XDM-Schema mithilfe von AI-generierten Empfehlungen](../../ingestion/tutorials/map-csv/recommendations.md).

Nachdem Sie einen Batch erfasst haben, müssen Sie für den Datensatz, in den Sie Daten aufgenommen haben, zur Registerkarte [!UICONTROL Datensatzaktivität] navigieren.

Wählen Sie in der Experience Platform-Benutzeroberfläche im linken Navigationsbereich **[!UICONTROL Datensätze]** aus, um das Dashboard [!UICONTROL Datensätze] zu öffnen. Wählen Sie anschließend den Namen des Datensatzes auf der Registerkarte [!UICONTROL Durchsuchen] aus, um auf den Bildschirm [!UICONTROL Datensatzaktivität] zuzugreifen.

![Das Dashboard der Platform UI-Datensätze mit Datensätzen, deren Datensätze im linken Navigationsbereich hervorgehoben sind.](../images/use-cases/datasets-workspace.png)

Die Ansicht [!UICONTROL Datensatzaktivität] wird angezeigt. Diese Ansicht enthält Details zu Ihrem ausgewählten Datensatz. Sie enthält alle erfassten Batches, die in einem Tabellenformat angezeigt werden.

Wählen Sie einen Batch aus der Liste der verfügbaren Batches aus und kopieren Sie die [!UICONTROL Batch-Kennung] aus dem Detailbereich auf der rechten Seite.

![Die Benutzeroberfläche &quot;Experience Platform-Datensätze&quot;mit den erfassten Datensätzen, deren Batch-Kennung hervorgehoben ist.](../images/use-cases/batch-id.png)

Rufen Sie dann mit der folgenden Abfrage alle Datensätze ab, die im Datensatz als Teil dieses Batches enthalten waren:

```sql
SELECT * FROM movie_data
WHERE  _acp_batchid='01H00BKCTCADYRFACAAKJTVQ8P' 
LIMIT 1;
```

Das Schlüsselwort `_ACP_BATCHID` wird zum Filtern der [!UICONTROL Batch-Kennung] verwendet.

>[!TIP]
>
>Die `LIMIT` -Klausel ist hilfreich, wenn Sie die Anzahl der angezeigten Zeilen beschränken möchten, aber eine Filterbedingung ist empfehlenswerter.

Wenn Sie diese Abfrage im Abfrage-Editor ausführen, werden die Ergebnisse auf 100 Zeilen gekürzt. Der Abfrage-Editor ist für schnelle Vorschau und Untersuchung konzipiert. Um bis zu 50.000 Zeilen abzurufen, können Sie ein Tool eines Drittanbieters wie DBVisualizer oder DBeaver verwenden.

## Nächste Schritte {#next-steps}

Durch Lesen dieses Dokuments haben Sie die Grundlagen der Überprüfung und Validierung von Datensätzen in aufgenommenen Batches im Rahmen des Datenerfassungsprozesses gelernt. Sie haben auch Einblicke in den Zugriff auf Batch-Metadaten von Datensätzen, das Verständnis logischer und physischer Partitionen und die Abfrage bestimmter Batches mithilfe von SQL-Befehlen erhalten. Dieses Wissen kann Ihnen dabei helfen, die Datenintegrität sicherzustellen und Ihre Datenspeicherung in Platform zu optimieren.

Als Nächstes sollten Sie die Datenerfassung durchführen, um die gelernten Konzepte anzuwenden. Erfassen Sie einen Beispieldatensatz in Platform mit den bereitgestellten Beispieldateien oder Ihren eigenen Daten. Wenn Sie dies noch nicht getan haben, lesen Sie das Tutorial zum [Erfassen von Daten in Adobe Experience Platform](../../ingestion/tutorials/ingest-batch-data.md).

Alternativ können Sie erfahren, wie Sie [Abfragen von Service mit einer Vielzahl von Desktop-Clientanwendungen verbinden und überprüfen](../clients/overview.md), um Ihre Datenanalysefunktionen zu verbessern.
