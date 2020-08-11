---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Configure a dataflow for a CRM connector in the UI
topic: overview
translation-type: tm+mt
source-git-commit: d80622aaa8408d640a1a80b6a37f4083344e7fa1
workflow-type: tm+mt
source-wordcount: '1325'
ht-degree: 6%

---


# Configure a dataflow for a CRM connector in the UI

A dataflow is a scheduled task that retrieves and ingests data from a source to a [!DNL Platform] dataset. Dieses Lernprogramm enthält Schritte zum Konfigurieren eines neuen Datenflusses mit Ihrem CRM-Konto.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Experience-Datenmodell (XDM)-System](../../../../xdm/home.md)[!DNL Experience Platform]: Das standardisierte Framework, mit dem Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   * [Schema Editor tutorial](../../../../xdm/tutorials/create-schema-ui.md): Learn how to create custom schemas using the Schema Editor UI.
* [Echtzeit-Kundenprofil](../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Darüber hinaus erfordert dieses Lernprogramm, dass Sie bereits ein CRM-Konto erstellt haben. A list of tutorials for creating different CRM connectors in the UI can be found in the [source connectors overview](../../../home.md).

## Select data

After creating your CRM account, the *Select data* step appears, providing an interactive interface for you to explore your file hierarchy.

* The left half of the interface is a directory browser, displaying your server&#39;s files and directories.
* The right half of the interface lets you preview up to 100 rows of data from a compatible file.

Select the directory you wish to use, then click **[!UICONTROL Next]**.

![select-data](../../../images/tutorials/dataflow/crm/select-data.png)

## Map data fields to an XDM schema

The *[!UICONTROL Mapping]* step appears, providing an interactive interface to map the source data to a [!DNL Platform] dataset.

Choose a dataset for inbound data to be ingested into. You can either use an existing dataset or create a new dataset.

### Vorhandenen Datensatz verwenden

Um Daten in einen vorhandenen Datensatz zu erfassen, wählen Sie &quot;Vorhandenen Datensatz **[!UICONTROL verwenden]**&quot;und klicken Sie dann auf das Dataset-Symbol.

![use-existing-dataset](../../../images/tutorials/dataflow/crm/use-existing-dataset.png)

The *[!UICONTROL Select dataset]* dialog appears. Suchen Sie den gewünschten Datensatz, wählen Sie ihn aus und klicken Sie dann auf **[!UICONTROL Weiter]**.

![select-existing-dataset](../../../images/tutorials/dataflow/crm/select-existing-dataset.png)

### Verwenden eines neuen Datensatzes

Um Daten in einen neuen Datensatz zu erfassen, wählen Sie &quot;Neuen Datensatz **[!UICONTROL erstellen]** &quot;und geben Sie einen Namen und eine Beschreibung für den Datensatz in die entsprechenden Felder ein.

Sie können ein Schema anhängen, indem Sie in der Suchleiste &quot;Schema **[!UICONTROL auswählen]** &quot;einen Schema eingeben. Sie können auch das Dropdownsymbol auswählen, um eine Liste der vorhandenen Schema anzuzeigen. Alternativ dazu können Sie die Option &quot; **[!UICONTROL Erweiterte Suche]** &quot;auswählen, um auf den Bildschirm der vorhandenen Schema mit den zugehörigen Details zuzugreifen.

![create-new-dataset](../../../images/tutorials/dataflow/all-tabular/new-target-dataset.png)

The *[!UICONTROL Select schema]* dialog appears. Wählen Sie das Schema aus, das Sie auf den neuen Datensatz anwenden möchten, und klicken Sie dann auf **[!UICONTROL Fertig]**.

![select-Schema](../../../images/tutorials/dataflow/crm/select-schema.png)

Je nach Bedarf können Sie Felder direkt zuordnen oder mithilfe der Zuordnungsfunktionen Quelldaten transformieren, um berechnete oder berechnete Werte abzuleiten. Weitere Informationen zu Funktionen für die Datenzuordnung und -zuordnung finden Sie im Lernprogramm zur [Zuordnung von CSV-Daten zu XDM-Schema-Feldern](../../../../ingestion/tutorials/map-a-csv-file.md).

Nachdem Sie die Quelldaten zugeordnet haben, klicken Sie auf **[!UICONTROL Weiter]**.

![](../../../images/tutorials/dataflow/all-tabular/mapping-updated.png)

## Planen von Erfassungsabläufen

Der Schritt *[!UICONTROL Planung]* wird angezeigt, mit dem Sie einen Erfassungszeitplan konfigurieren können, um die ausgewählten Quelldaten automatisch mit den konfigurierten Zuordnungen zu erfassen. In der folgenden Tabelle sind die verschiedenen konfigurierbaren Felder für die Planung aufgeführt:

| Feld | Beschreibung |
| --- | --- |
| Häufigkeit | Zu den auswählbaren Frequenzen gehören `Once`, `Minute`, `Hour`, `Day`und `Week`. |
| Intervall | Eine Ganzzahl, die das Intervall für die ausgewählte Frequenz festlegt. |
| Beginn | Ein UTC-Zeitstempel, der angibt, wann die erste Erfassung erfolgen soll. |
| Aufstockung | Ein boolescher Wert, der bestimmt, welche Daten ursprünglich erfasst werden. Wenn die *[!UICONTROL Aufstockung]* aktiviert ist, werden alle aktuellen Dateien im angegebenen Pfad während der ersten geplanten Erfassung erfasst. Wenn die *Aufstockung* deaktiviert ist, werden nur die Dateien aufgenommen, die zwischen der ersten Ausführung der Erfassung und der *[!UICONTROL Beginn]* geladen wurden. Dateien, die vor dem *[!UICONTROL Beginn]* geladen wurden, werden nicht erfasst. |
| Delta-Spalte | Eine Option mit gefilterten Quelldatumsfeldern vom Typ, Schema oder Uhrzeit. Dieses Feld wird verwendet, um zwischen neuen und vorhandenen Daten zu unterscheiden. Inkrementelle Daten werden basierend auf dem Zeitstempel der ausgewählten Spalte erfasst. |

Datenflüsse sind so konzipiert, dass Daten auf planmäßiger Basis automatisch erfasst werden. Beginn durch Auswahl der Aufnahmefrequenz. Legen Sie als Nächstes das Intervall fest, um den Zeitraum zwischen zwei Flussläufen festzulegen. Der Wert des Intervalls sollte eine Ganzzahl ungleich null sein und auf größer oder gleich 15 gesetzt werden.

Um die Erfassungszeit des Beginns festzulegen, passen Sie das Datum und die Uhrzeit an, die im Feld &quot;Beginn&quot;angezeigt werden. Alternatively, you can select the calendar icon to edit the start time value. Start time must be greater than or equal to your current UTC time.

Select **[!UICONTROL Load incremental data by]** to assign the delta column. This field provides a distinction between new and existing data.

![](../../../images/tutorials/dataflow/databases/schedule-interval-on.png)

### Set up a one-time ingestion dataflow

To set up one-time ingestion, select the frequency drop down arrow and select **[!UICONTROL Once]**.

>[!TIP]
>
>**[!UICONTROL Interval]** and **[!UICONTROL Backfill]** are not visible during a one-time ingestion.

Once you have provided appropriate values to the schedule, select **[!UICONTROL Next]**.

![schedule-once](../../../images/tutorials/dataflow/databases/schedule-once.png)

## Provide dataflow details

The *[!UICONTROL Dataflow detail]* step appears, allowing you to name and give a brief description about your new dataflow.

During this process, you can also enable *[!UICONTROL Partial ingestion]* and *[!UICONTROL Error diagnostics]*. Enabling *[!UICONTROL Partial ingestion]* provides the ability to ingest data containing errors up to a certain threshold. Once *[!UICONTROL Partial ingestion]* is enabled, drag the *[!UICONTROL Error threshold %]* dial to adjust the error threshold of the batch. Alternatively, you can manually adjust the threshold by selecting the input box. For more information, see the [partial batch ingestion overview](../../../../ingestion/batch-ingestion/partial.md).

Geben Sie Werte für den Datenflug ein und wählen Sie **[!UICONTROL Weiter]**.

![dataflow-details](../../../images/tutorials/dataflow/all-tabular/dataflow-detail.png)

## Überprüfen Sie Ihren Datenfluss

Der *Schritt zum Überprüfen* wird angezeigt, mit dem Sie Ihren neuen Datenpfad überprüfen können, bevor er erstellt wird. Details werden in den folgenden Kategorien gruppiert:

* *[!UICONTROL Verbindungsdetails]*: Zeigt den Quelltyp, den relevanten Pfad der ausgewählten Quelldatei und die Anzahl der Spalten in dieser Quelldatei an.
* *[!UICONTROL Zuordnungsdetails]*: Zeigt, in welchen Datensatz die Quelldaten aufgenommen werden, einschließlich des Schemas, das der Datensatz einhält.
* *[!UICONTROL Details]* planen: Zeigt den aktiven Zeitraum, die Häufigkeit und das Intervall des Aufnahmeplans an.

Klicken Sie nach Überprüfung des Datenflusses auf **[!UICONTROL Fertig stellen]** und lassen Sie die Erstellung des Datenflusses etwas Zeit.

![überprüfen](../../../images/tutorials/dataflow/crm/review.png)

## Überwachen des Datenflusses

Nachdem Sie Ihren Datenbogen erstellt haben, können Sie die Daten überwachen, die über ihn erfasst werden, um Informationen zu Erfassungsraten, Erfolgen und Fehlern anzuzeigen. Weitere Informationen zur Überwachung des Datenflusses finden Sie im Lernprogramm zu [Überwachungskonten und Datenflüssen in der Benutzeroberfläche](../monitor.md).

## Datenflug löschen

Sie können Datenflüsse löschen, die nicht mehr benötigt werden oder mit der Funktion &quot; *[!UICONTROL Löschen]* &quot;im Arbeitsbereich &quot; *[!UICONTROL Datenflüsse]* &quot;falsch erstellt wurden. Weitere Informationen zum Löschen von Datenflüssen finden Sie im Lernprogramm zum [Löschen von Datenflüssen in der Benutzeroberfläche](../delete.md).

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich einen Datenbogen erstellt, um Daten aus einem CRM-System einzubringen und Einblicke in die Überwachung von Datensätzen zu erhalten. Um mehr über das Erstellen von Datenflüssen zu erfahren, können Sie Ihr Lernen durch das Video unten ergänzen. Darüber hinaus können eingehende Daten jetzt auch von nachgelagerten [!DNL Platform] Diensten wie [!DNL Real-time Customer Profile] und [!DNL Data Science Workspace]genutzt werden. Weitere Informationen finden Sie in den folgenden Dokumenten:

* [Übersicht über das Echtzeit-Kundenprofil](../../../../profile/home.md)
* [Übersicht über den Data Science Workspace](../../../../data-science-workspace/home.md)

>[!WARNING]
>
> Die im folgenden Video dargestellte [!DNL Platform] Benutzeroberfläche ist veraltet. Die neuesten Screenshots und Funktionen der Benutzeroberfläche finden Sie in der obigen Dokumentation.

>[!VIDEO](https://video.tv.adobe.com/v/29711?quality=12&learn=on)

## Anhang

Die folgenden Abschnitte enthalten zusätzliche Informationen zum Arbeiten mit Quellschnittstellen.

### Datentaflow deaktivieren

Beim Erstellen eines Datenflusses wird dieser sofort aktiv und erfasst Daten gemäß dem festgelegten Zeitplan. Sie können einen aktiven Datenfeed jederzeit deaktivieren, indem Sie die unten stehenden Anweisungen befolgen.

Wählen Sie im *[!UICONTROL Authentifizierungsbildschirm]* den Namen der Basisverbindung aus, die mit dem zu deaktivierenden Datendurchlauf verknüpft ist.

![](../../../images/tutorials/dataflow/crm/monitor.png)

Die Seite &quot; _Quellseite_ &quot;wird angezeigt. Wählen Sie den aktiven Datenfluss aus der Liste aus, um die Spalte &quot; *[!UICONTROL Eigenschaften]* &quot;auf der rechten Seite des Bildschirms mit der Schaltfläche &quot; **[!UICONTROL Aktiviert]** &quot;zu öffnen. Klicken Sie auf den Umschalter, um den Datenflug zu deaktivieren. Derselbe Umschalter kann verwendet werden, um einen Datenflug nach dessen Deaktivierung erneut zu aktivieren.

![disable](../../../images/tutorials/dataflow/crm/disable.png)

### Aktivieren von Eingangsdaten für die [!DNL Profile] Bevölkerung

Eingehende Daten aus Ihrem Quellanschluss können zur Anreicherung und zum Ausfüllen Ihrer [!DNL Real-time Customer Profile] Daten verwendet werden. Weitere Informationen zum Ausfüllen Ihrer [!DNL Real-time Customer Profile] Daten finden Sie im Tutorial zur [Profil-Population](../profile.md).