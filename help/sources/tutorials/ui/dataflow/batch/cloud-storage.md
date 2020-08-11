---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Konfigurieren eines Datenflusses für einen Batch-Connector für eine Cloud-Datenspeicherung in der Benutzeroberfläche
topic: overview
translation-type: tm+mt
source-git-commit: d80622aaa8408d640a1a80b6a37f4083344e7fa1
workflow-type: tm+mt
source-wordcount: '1534'
ht-degree: 5%

---


# Konfigurieren eines Datenflusses für einen Batch-Connector für eine Cloud-Datenspeicherung in der Benutzeroberfläche

A dataflow is a scheduled task that retrieves and ingests data from a source to a [!DNL Platform] dataset. This tutorial provides steps to configure a new dataflow using your cloud storage account.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Experience-Datenmodell (XDM)-System](../../../../../xdm/home.md)[!DNL Experience Platform]: Das standardisierte Framework, mit dem Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   * [Schema Editor tutorial](../../../../../xdm/tutorials/create-schema-ui.md): Learn how to create custom schemas using the Schema Editor UI.
* [Echtzeit-Kundenprofil](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Additionally, this tutorial requires that you have an established cloud storage account. A list of tutorials for creating different cloud storage accounts in the UI can be found in the [source connectors overview](../../../../home.md).

### Unterstützte Dateiformate

[!DNL Experience Platform] supports the following file formats to be ingested from external storages:

* Delimiter-separated values (DSV): Support for DSV-formatted data files is currently limited to comma-separated values. The value of field headers within DSV formatted files must only consist of alphanumeric characters and underscores. Support for general DSV files will be provided in the future.
* [!DNL JavaScript Object Notation] (JSON): JSON-formatted data files must be XDM-compliant.
* [!DNL Apache Parquet]: Parquet-formatted data files must be XDM-compliant.

## Select data

After creating your cloud storage account, the *[!UICONTROL Select data]* step appears, providing an interactive interface for you to explore your cloud storage hierarchy.

* The left half of the interface is a directory browser, displaying your server&#39;s files and directories.
* In der rechten Hälfte der Oberfläche können Sie bis zu 100 Datenzeilen aus einer kompatiblen Datei Vorschau werden.

Selecting a listed folder allows you to traverse the folder hierarchy into deeper folders. Wenn Sie eine kompatible Datei oder einen kompatiblen Ordner ausgewählt haben, wird das Dropdownmenü Datenformat **[!UICONTROL auswählen]** angezeigt, in dem Sie ein Format auswählen können, in dem die Daten im Fenster Vorschau angezeigt werden.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-data.png)

Nach dem Ausfüllen des Fensters &quot;Vorschau&quot;können Sie &quot; **[!UICONTROL Weiter]** &quot;auswählen, um alle Dateien im ausgewählten Ordner hochzuladen. Wenn Sie eine Datei in eine bestimmte Datei hochladen möchten, wählen Sie diese Datei in der Liste aus, bevor Sie **[!UICONTROL Weiter]** auswählen.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-data-preview.png)

### Parquet- oder JSON-Dateien aufnehmen

Unterstützte Dateiformate für ein Cloud-Datenspeicherung-Konto umfassen auch JSON und Parquet. JSON- und Parquet-Dateien müssen XDM-kompatibel sein. Um JSON- oder Parquet-Dateien zu erfassen, wählen Sie das entsprechende Dateiformat im Ordnerbrowser aus und wenden Sie auf der rechten Benutzeroberfläche das kompatible Datenformat an. Wählen Sie **[!UICONTROL Weiter]** , um fortzufahren.

>[!IMPORTANT]
>
>Im Gegensatz zu getrennten Dateitypen stehen JSON- und Parquet-formatierte Dateien nicht zur Vorschau zur Verfügung.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-data-parquet.png)

## Zuordnen von Datenfeldern zu einem XDM-Schema

Der Schritt *[!UICONTROL Zuordnung]* wird angezeigt und bietet eine interaktive Schnittstelle, um die Quelldaten einem [!DNL Platform] Datensatz zuzuordnen. Quelldateien, die in JSON oder Parquet formatiert sind, müssen XDM-konform sein und müssen nicht manuell konfiguriert werden. Bei CSV-Dateien müssen Sie die Zuordnung explizit konfigurieren. Sie können jedoch festlegen, welche Quelldatenfelder zugeordnet werden sollen.

Wählen Sie einen Datensatz, in den eingehende Daten aufgenommen werden sollen. Sie können entweder einen vorhandenen Datensatz verwenden oder einen neuen erstellen.

**Vorhandenen Datensatz verwenden**

Um Daten in einen vorhandenen Datensatz zu erfassen, wählen Sie &quot; **[!UICONTROL Vorhandener Datensatz]**&quot;und klicken Sie dann auf das Dataset-Symbol.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/use-existing-data.png)

The *[!UICONTROL Select dataset]* dialog appears. Suchen Sie den gewünschten Datensatz, wählen Sie ihn aus und klicken Sie dann auf **[!UICONTROL Weiter]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-existing-dataset.png)

**Verwenden eines neuen Datensatzes**

Um Daten in einen neuen Datensatz zu erfassen, wählen Sie &quot; **[!UICONTROL Neuer Datensatz]** &quot;und geben Sie einen Namen und eine Beschreibung für den Datensatz in die entsprechenden Felder ein. Um ein Schema hinzuzufügen, können Sie im Dialogfeld &quot;Schema *[!UICONTROL auswählen]* &quot;einen vorhandenen Schema eingeben. Alternativ dazu können Sie die erweiterte **[!UICONTROL Schema-Suche]** auswählen, um nach einem geeigneten Schema zu suchen.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/use-new-dataset.png)

The *[!UICONTROL Select schema]* dialog appears. Wählen Sie das Schema, das Sie auf den neuen Datensatz anwenden möchten, und wählen Sie dann **[!UICONTROL Fertig]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-schema.png)

Je nach Bedarf können Sie Felder direkt zuordnen oder mithilfe der Zuordnungsfunktionen Quelldaten transformieren, um berechnete oder berechnete Werte abzuleiten. Weitere Informationen zu Funktionen für die Datenzuordnung und -zuordnung finden Sie im Lernprogramm zur [Zuordnung von CSV-Daten zu XDM-Schema-Feldern](../../../../../ingestion/tutorials/map-a-csv-file.md).

Once your source data is mapped, select **[!UICONTROL Next]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/mapping.png)

## Schedule ingestion runs

The *[!UICONTROL Scheduling]* step appears, allowing you to configure an ingestion schedule to automatically ingest the selected source data using the configured mappings. The following table outlines the different configurable fields for scheduling:

| Feld | Beschreibung |
| --- | --- |
| Häufigkeit | Selectable frequencies include `Once`, `Minute`, `Hour`, `Day`, and `Week`. |
| Interval | An integer that sets the interval for the selected frequency. |
| Start time | A UTC timestamp indicating when the very first ingestion is set to occur. |
| Backfill | A boolean value that determines what data is initially ingested. If *[!UICONTROL Backfill]* is enabled, all current files in the specified path will be ingested during the first scheduled ingestion. If *Backfill* is disabled, only the files that are loaded in between the first run of ingestion and the *[!UICONTROL Start time]* will be ingested. Files loaded prior to *[!UICONTROL Start time]* will not be ingested. |

Datenflüsse sind so konzipiert, dass Daten auf planmäßiger Basis automatisch erfasst werden. Start by selecting the ingestion frequency. Legen Sie als Nächstes das Intervall fest, um den Zeitraum zwischen zwei Flussläufen festzulegen. Der Wert des Intervalls sollte eine Ganzzahl ungleich null sein und auf größer oder gleich 15 gesetzt werden.

Um die Erfassungszeit des Beginns festzulegen, passen Sie das Datum und die Uhrzeit an, die im Feld &quot;Beginn&quot;angezeigt werden. Alternativ können Sie das Kalendersymbol auswählen, um den Zeitwert des Beginns zu bearbeiten. Die Beginn-Zeit muss größer oder gleich der aktuellen Uhrzeit in UTC sein.

Geben Sie Werte für den Zeitplan ein und wählen Sie **[!UICONTROL Weiter]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/scheduling-interval-on.png)

### Einrichten eines einmaligen Erfassungsdataflow

Um eine einmalige Erfassung einzurichten, wählen Sie den Dropdown-Pfeil für die Häufigkeit aus und klicken Sie auf **[!UICONTROL Einmal]**. Sie können die Bearbeitung eines Datensatzes für eine einmalige Erfassung der Häufigkeit fortsetzen, solange der Beginn in der Zukunft verbleibt. Nach Ablauf des Beginns kann der Wert für die einmalige Häufigkeit nicht mehr bearbeitet werden.

>[!TIP]
>
>**[!UICONTROL Intervall]** und **[!UICONTROL Aufstockung]** sind während einer einmaligen Erfassung nicht sichtbar.

Nachdem Sie die entsprechenden Werte für den Zeitplan angegeben haben, wählen Sie **[!UICONTROL Weiter]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/scheduling-once.png)

## Datennachrichtendetails angeben

The *[!UICONTROL Dataflow detail]* step appears, allowing you to name and give a brief description about your new dataflow.

During this process, you can also enable *[!UICONTROL Partial ingestion]* and *[!UICONTROL Error diagnostics]*. Enabling *[!UICONTROL Partial ingestion]* provides the ability to ingest data containing errors, up to a certain threshold that you can set. Enabling *[!UICONTROL Error diagnostics]* will provide details on any incorrect data that is batched separately. For more information, see the [partial batch ingestion overview](../../../../../ingestion/batch-ingestion/partial.md).

Provide values for the dataflow and select **[!UICONTROL Next]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/dataflow-detail.png)

## Review your dataflow

The *[!UICONTROL Review]* step appears, allowing you to review your new dataflow before it is created. Details are grouped within the following categories:

* *[!UICONTROL Connection]*: Shows the source type, the relevant path of the chosen source file, and the amount of columns within that source file.
* *[!UICONTROL Assign dataset &amp; map fields]*: Shows which dataset the source data is being ingested into, including the schema that the dataset adheres to.
* *[!UICONTROL Scheduling]*: Shows the active period, frequency, and interval of the ingestion schedule.

Once you have reviewed your dataflow, click **[!UICONTROL Finish]** and allow some time for the dataflow to be created.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/review.png)

## Monitor your dataflow

Once your dataflow has been created, you can monitor the data that is being ingested through it to see information on ingestion rates, success, and errors. Weitere Informationen zur Überwachung des Datenflusses finden Sie im Lernprogramm zu [Überwachungskonten und Datenflüssen in der Benutzeroberfläche](../../monitor.md).

## Datenflug löschen

Sie können Datenflüsse löschen, die nicht mehr benötigt werden oder mit der Funktion &quot; *[!UICONTROL Löschen]* &quot;im Arbeitsbereich &quot; *[!UICONTROL Datenflüsse]* &quot;falsch erstellt wurden. Weitere Informationen zum Löschen von Datenflüssen finden Sie im Lernprogramm zum [Löschen von Datenflüssen in der Benutzeroberfläche](../../delete.md).

## Nächste Schritte

In diesem Lernprogramm haben Sie erfolgreich einen Datenbogen erstellt, um Daten aus einer externen Cloud-Datenspeicherung einzubringen, und Einblicke in die Überwachung von Datensätzen erhalten. Um mehr über das Erstellen von Datenflüssen zu erfahren, können Sie Ihr Lernen durch das Video unten ergänzen. Darüber hinaus können eingehende Daten jetzt auch von nachgelagerten [!DNL Platform] Diensten wie [!DNL Real-time Customer Profile] und [!DNL Data Science Workspace]genutzt werden. See the following documents for more details:

* [Übersicht über das Echtzeit-Kundenprofil](../../../../../profile/home.md)
* [Data Science Workspace overview](../../../../../data-science-workspace/home.md)

>[!WARNING]
>
> Die im folgenden Video dargestellte [!DNL Platform] Benutzeroberfläche ist veraltet. Die neuesten Screenshots und Funktionen der Benutzeroberfläche finden Sie in der obigen Dokumentation.

>[!VIDEO](https://video.tv.adobe.com/v/29695?quality=12&learn=on)

## Anhang

The following sections provide additional information for working with source connectors.

### Disable a dataflow

When a dataflow is created, it immediately becomes active and ingests data according to the schedule it was given. You can disable an active dataflow at any time by following the instructions below.

Within the *[!UICONTROL Sources]* workspace, click the **[!UICONTROL Browse]** tab. Next, click the name of the account that&#39;s associated the active dataflow you wish to disable.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

The *[!UICONTROL Source activity]* page appears. Select the active dataflow from the list to open its *[!UICONTROL Properties]* column on the right-hand side of the screen, which contains an **[!UICONTROL Enabled]** toggle button. Click the toggle to disable the dataflow. Derselbe Umschalter kann verwendet werden, um einen Datenflug nach dessen Deaktivierung erneut zu aktivieren.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/disable-source.png)

### Activate inbound data for [!DNL Profile] population

Inbound data from your source connector can be used towards enriching and populating your [!DNL Real-time Customer Profile] data. For more information on populating your Real-Customer [!DNL Profile] data, see the tutorial on [Profile population](../../profile.md).
