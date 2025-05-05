---
title: Erkunden, Fehlerbehebung und Verifizierung der Batch-Aufnahme mit SQL
description: Erfahren Sie, wie Sie den Datenaufnahmeprozess in Adobe Experience Platform verstehen und verwalten. Dieses Dokument beschreibt, wie Batches überprüft und aufgenommene Daten abgefragt werden.
exl-id: 8f49680c-42ec-488e-8586-50182d50e900
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 0%

---

# Erkunden, Fehlerbehebung und Verifizierung der Batch-Aufnahme mit SQL

In diesem Dokument wird erläutert, wie Sie Datensätze in aufgenommenen Batches mit SQL überprüfen und validieren können. In diesem Dokument erfahren Sie, wie Sie:

- Zugriff auf Datensatz-Batch-Metadaten
- Fehlerbehebung und Gewährleistung der Datenintegrität durch die Abfrage von Batches

>[!NOTE]
>
>Einige Screenshots in diesem Handbuch stammen von [!DNL DBVisualizer]. Informationen zum Verbinden [Abfrage-Service mit DBVisualizer](../clients/dbvisulaizer.md) oder anderen [BI-Tools von Drittanbietern](../clients/overview.md) finden Sie in der verknüpften Dokumentation.

## Voraussetzungen

Um Ihnen das Verständnis der in diesem Dokument besprochenen Konzepte zu erleichtern, sollten Sie über Kenntnisse in den folgenden Themen verfügen:

- **Datenaufnahme**: In der [Übersicht zur Datenaufnahme](../../ingestion/home.md) erfahren Sie mehr über die Grundlagen, wie Daten in Experience Platform aufgenommen werden, einschließlich der verschiedenen Methoden und Prozesse.
- **Batch-Aufnahme**: In der [Übersicht zur Batch-Aufnahme-](../../ingestion/batch-ingestion/overview.md) erfahren Sie mehr über die grundlegenden Konzepte der Batch-Aufnahme. Im Einzelnen geht es darum, was ein „Batch“ ist und wie er innerhalb des Datenerfassungsprozesses von Experience Platform funktioniert.
- **Systemmetadaten in Datensätzen**: In der [Übersicht über den Katalog-Service](../../catalog/home.md) erfahren Sie, wie Systemmetadatenfelder verwendet werden, um aufgenommene Daten zu verfolgen und abzufragen.
- **Experience-Datenmodell (XDM)**: In der [Übersicht über die Schemabenutzeroberfläche](../../xdm/ui/overview.md) und den [Grundlagen der Schemakomposition&#39; erfahren ](../../xdm/schema/composition.md) mehr über XDM-Schemata und darüber, wie sie die Struktur und das Format von Daten darstellen und validieren, die in Experience Platform aufgenommen werden.

## Zugriff auf Datensatz-Batch-Metadaten {#access-dataset-batch-metadata}

Um sicherzustellen, dass Systemspalten (Metadatenspalten) in den Abfrageergebnissen enthalten sind, verwenden Sie die SQL-`set drop_system_columns=false` im Abfrage-Editor. Dadurch wird das Verhalten Ihrer SQL-Abfragesitzung konfiguriert. Diese Eingabe muss wiederholt werden, wenn Sie eine neue Sitzung starten.

Führen Sie als Nächstes eine SELECT ALL-Anweisung aus, um die Systemfelder des Datensatzes anzuzeigen, z. B. `select * from movie_data`, um die Ergebnisse des Datensatzes anzuzeigen. Die Ergebnisse umfassen zwei neue Spalten auf der rechten Seite `_acp_system_metadata` und `_ACP_BATCHID`. Die Metadatenspalten `_acp_system_metadata` und `_ACP_BATCHID` helfen bei der Identifizierung der logischen und physischen Partitionen der aufgenommenen Daten.

![Die DBVisualizer-Benutzeroberfläche mit der Movie_data-Tabelle und ihren Metadatenspalten, die angezeigt und hervorgehoben werden.](../images/use-cases/movie_data-table-with-metadata-columns.png)

Wenn Daten in Experience Platform aufgenommen werden, wird ihnen auf der Grundlage der eingehenden Daten eine logische Partition zugewiesen. Diese logische Partition wird durch `_acp_system_metadata.sourceBatchId` dargestellt. Diese ID hilft, die Datenstapel logisch zu gruppieren und zu identifizieren, bevor sie verarbeitet und gespeichert werden.

Nachdem die Daten verarbeitet und in den Data Lake aufgenommen wurden, wird ihnen eine physische Partition zugewiesen, die durch `_ACP_BATCHID` dargestellt wird. Diese ID spiegelt die tatsächliche Speicherpartition im Data Lake wider, in dem sich die aufgenommenen Daten befinden.

### SQL verwenden, um logische und physische Partitionen zu verstehen {#understand-partitions}

Um zu verstehen, wie die Daten nach der Aufnahme gruppiert und verteilt werden, verwenden Sie die folgende Abfrage, um die Anzahl der verschiedenen physischen Partitionen (`_ACP_BATCHID`) für jede logische Partition (`_acp_system_metadata.sourceBatchId`) zu zählen.

```SQL
SELECT  _acp_system_metadata, COUNT(DISTINCT _ACP_BATCHID) FROM movie_data
GROUP BY _acp_system_metadata
```

Die Ergebnisse dieser Abfrage werden in der folgenden Abbildung dargestellt.

![Die Ergebnisse einer Abfrage, um die Anzahl der verschiedenen physischen Partitionen für jede logische Partition anzuzeigen.](../images/use-cases/logical-and-physical-partition-count.png)

Diese Ergebnisse zeigen, dass die Anzahl der Eingabestapel nicht unbedingt mit der Anzahl der Ausgabestapel übereinstimmt, da das System festlegt, wie die Daten am effizientesten im Data Lake stapelweise gespeichert werden.

Für dieses Beispiel wird davon ausgegangen, dass Sie eine CSV-Datei in Experience Platform aufgenommen und einen Datensatz mit dem Namen `drug_checkout_data` erstellt haben.

Die `drug_checkout_data`-Datei ist ein tief verschachtelter Satz von 35.000 Datensätzen. Verwenden Sie die SQL-Anweisung `SELECT * FROM drug_orders;`, um eine Vorschau des ersten Satzes von Datensätzen im JSON-basierten `drug_orders`-Datensatz anzuzeigen.

Die folgende Abbildung zeigt eine Vorschau der Datei und ihrer Datensätze.

![Eine Vorschau des ersten Satzes von Datensätzen im JSON-basierten drogen_orders-Datensatz.](../images/use-cases/drug-orders-preview.png)

### SQL verwenden, um Einblicke in den Batch-Erfassungsvorgang zu generieren {#sql-insights-on-batch-ingestion}

Verwenden Sie die unten stehende SQL-Anweisung, um Einblicke in die Gruppierung und Verarbeitung der Eingabedatensätze durch den Datenaufnahmeprozess in Batches zu erhalten.

```sql
SELECT _acp_system_metadata,
       Count(DISTINCT _acp_batchid) AS numoutputbatches,
       Count(_acp_batchid)          AS recordcount
FROM   drug_orders
GROUP  BY _acp_system_metadata 
```

Die Abfrageergebnisse werden in der Abbildung unten angezeigt.

![Eine Tabelle, die die Verteilung der Verarbeitung der Eingabestapel zu einem Zeitpunkt mit Datensatzzählungen anzeigt.](../images/use-cases/distribution-of-input-batches.png)

Die Ergebnisse zeigen die Effizienz und das Verhalten des Datenerfassungsprozesses. Obwohl drei Eingabestapel erstellt wurden - jeder mit 2000, 24000 und 9000 Datensätzen -, wenn die Datensätze kombiniert und dedupliziert wurden, blieb nur ein eindeutiger Batch übrig.

>[!NOTE]
>
>Bei allen Datensätzen, die in einem Datensatz sichtbar sind, handelt es sich um diejenigen, die erfolgreich aufgenommen wurden. Eine erfolgreiche Batch-Aufnahme bedeutet nicht, dass alle Datensätze vorhanden sind, die von der Quelleingabe gesendet wurden. Sie müssen nach Fehlern bei der Datenaufnahme suchen, um die Batches/Datensätze zu finden, die es nicht in geschafft haben.

## Validieren eines Batches mit SQL {#validate-a-batch-with-SQL}

Überprüfen Sie anschließend die Datensätze, die in den Datensatz aufgenommen wurden, mit SQL.

>[!TIP]
>
>Um die Batch-ID und die mit dieser Batch-ID verknüpften Abfragedatensätze abzurufen, müssen Sie zunächst einen Batch in Experience Platform erstellen. Wenn Sie den Prozess selbst testen möchten, können Sie CSV-Daten in Experience Platform aufnehmen. Lesen Sie das Handbuch zum [ (Zuordnen einer CSV-Datei zu einem vorhandenen XDM-Schema mithilfe von KI-generierten Empfehlungen](../../ingestion/tutorials/map-csv/recommendations.md).

Nachdem Sie einen Batch aufgenommen haben, müssen Sie zur Registerkarte [!UICONTROL Datensatzaktivität] für den Datensatz navigieren, in den Sie Daten aufgenommen haben.

Wählen Sie in der Experience Platform-Benutzeroberfläche **[!UICONTROL Datensätze]** im linken Navigationsbereich aus, um das Dashboard [!UICONTROL Datensätze] zu öffnen. Wählen Sie als Nächstes den Namen des Datensatzes auf der Registerkarte [!UICONTROL Durchsuchen] aus, um auf den Bildschirm [!UICONTROL Datensatzaktivität] zuzugreifen.

![Das Dashboard der Experience Platform-Benutzeroberfläche mit Datensätzen, die in der linken Navigationsleiste hervorgehoben sind.](../images/use-cases/datasets-workspace.png)

Die [!UICONTROL Datensatzaktivität] wird angezeigt. Diese Ansicht enthält Details zum ausgewählten Datensatz. Er umfasst alle aufgenommenen Batches, die im Tabellenformat angezeigt werden.

Wählen Sie einen Stapel aus der Liste der verfügbaren Stapel aus und kopieren [!UICONTROL Batch-ID] aus dem Detailbereich auf der rechten Seite.

![Die Benutzeroberfläche &quot;Experience Platform-Datensätze“ mit den aufgenommenen Datensätzen und einer hervorgehobenen Batch-ID.](../images/use-cases/batch-id.png)

Verwenden Sie als Nächstes die folgende Abfrage, um alle Datensätze abzurufen, die im Datensatz als Teil dieses Batches enthalten waren:

```sql
SELECT * FROM movie_data
WHERE  _acp_batchid='01H00BKCTCADYRFACAAKJTVQ8P' 
LIMIT 1;
```

Das Keyword `_ACP_BATCHID` wird zum Filtern der [!UICONTROL Batch-ID“ &#x200B;].

>[!TIP]
>
>Die `LIMIT`-Klausel ist hilfreich, wenn Sie die Anzahl der angezeigten Zeilen einschränken möchten, aber eine Filterbedingung ist wünschenswerter.

Beim Ausführen dieser Abfrage im Abfrage-Editor werden die Ergebnisse auf 100 Zeilen gekürzt. Der Abfrage-Editor ist für schnelle Vorschauen und Untersuchungen konzipiert. Zum Abrufen von bis zu 50.000 Zeilen können Sie ein Tool eines Drittanbieters wie DBVisualizer oder DBeaver verwenden.

## Nächste Schritte {#next-steps}

Durch das Lesen dieses Dokuments haben Sie die Grundlagen gelernt, um Datensätze in aufgenommenen Batches im Rahmen der Datenaufnahme zu überprüfen und zu validieren. Sie haben außerdem Einblicke in den Zugriff auf Datensatz-Batch-Metadaten, das Verständnis logischer und physischer Partitionen und das Abfragen bestimmter Batches mithilfe von SQL-Befehlen erhalten. Mit diesem Wissen können Sie die Datenintegrität sicherstellen und die Datenspeicherung in Experience Platform optimieren.

Als Nächstes sollten Sie die Datenaufnahme üben, um die erlernten Konzepte anzuwenden. Nehmen Sie einen Beispieldatensatz mit den bereitgestellten Beispieldateien oder Ihren eigenen Daten in Experience Platform auf. Wenn Sie dies noch nicht getan haben, lesen Sie das Tutorial zum [Aufnehmen von Daten in Adobe Experience Platform](../../ingestion/tutorials/ingest-batch-data.md).

Alternativ können Sie lernen, wie Sie [Query Service mit einer Vielzahl von Desktop-Client-Anwendungen verbinden und überprüfen](../clients/overview.md) um Ihre Datenanalysefunktionen zu verbessern.
