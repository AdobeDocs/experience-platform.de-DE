---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Benutzerhandbuch zu Datensätzen
topic: datasets
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '1135'
ht-degree: 76%

---


# Benutzerhandbuch zu Datensätzen

Dieses Benutzerhandbuch enthält Anweisungen zur Ausführung allgemeiner Aktionen beim Verwenden von Datensätzen in der Benutzeroberfläche von Adobe Experience Platform.

## Erste Schritte

Das Benutzerhandbuch setzt ein grundlegendes Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Datensätze](overview.md): Das Speicher- und Verwaltungskonstrukt für Datenpersistenz in [!DNL Experience Platform].
* [!DNL Experience Data Model (XDM) System](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten [!DNL Experience Platform] organisiert werden.
   * [Grundlagen zum Aufbau von Schemas](../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   * [Schema-Editor](../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie Ihre eigenen benutzerdefinierten XDM-Schema mithilfe der [!DNL Schema Editor] in der [!DNL Platform] Benutzeroberfläche erstellen.
* [!DNL Real-time Customer Profile](../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
* [!DNL Data Governance](../../data-governance/home.md): Sorgen Sie bei der Nutzung von Kundendaten für die Einhaltung von Vorschriften, Begrenzungen und Richtlinien.

## Datensätze anzeigen

In the [!DNL Experience Platform] UI, click **[!UICONTROL Datasets]** in the left-navigation to open the *[!UICONTROL Datasets]* dashboard. Das Dashboard listet alle verfügbaren Datensätze für Ihre Organisation auf. Zu jedem aufgelisteten Datensatz werden Details angezeigt, einschließlich seines Namens, des Schemas, dem der Datensatz entspricht, und des Status des letzten Erfassungslaufs.

![](../images/datasets/user-guide/browse_datasets.png)

Klicken Sie auf den Namen eines Datensatzes, um auf seinen *[!UICONTROL Datensatzaktivität]*-Bildschirm zuzugreifen und Details zum ausgewählten Datensatz anzuzeigen. Der Tab „Aktivität“ enthält ein Diagramm, das die Rate der konsumierten Nachrichten sowie eine Liste erfolgreicher und fehlgeschlagener Batches visuell darstellt.

![](../images/datasets/user-guide/dataset_activity_1.png)
![](../images/datasets/user-guide/dataset_activity_2.png)

## Vorschau für Datensatz anzeigen

Klicken Sie im Bildschirm *[!UICONTROL Datensatzaktivität]* oben rechts im Bildschirm auf **[!UICONTROL Vorschau für Datensatz anzeigen]**, um bis zu 100 Datenzeilen als Vorschau anzuzeigen. Wenn der Datensatz leer ist, wird der Vorschau-Link deaktiviert und stattdessen darauf hingewiesen, dass die **[!UICONTROL Vorschau nicht verfügbar]** ist.

![](../images/datasets/user-guide/click_to_preview.png)

Im Vorschaufenster wird rechts für den Datensatz die hierarchische Ansicht des Schemas angezeigt.

![](../images/datasets/user-guide/preview_dataset.png)

For more robust methods to access your data, [!DNL Experience Platform] provides downstream services such as [!DNL Query Service] and [!DNL JupyterLab] to explore and analyze data. Weiterführende Informationen finden Sie in folgenden Dokumenten:

* [Übersicht über Query Service](../../query-service/home.md)
* [JupyterLab-Benutzerhandbuch](../../data-science-workspace/jupyterlab/overview.md)

## Datensatz erstellen {#create}

Um einen neuen Datensatz zu erstellen, klicken Sie zunächst im Dashboard **[!UICONTROL Datensätze]** auf *[!UICONTROL Datensatz erstellen]*.

![](../images/datasets/user-guide/click_to_create.png)

Im folgenden Bildschirm werden Ihnen die folgenden zwei Optionen zum Erstellen eines neuen Datensatzes angezeigt:

* [Datensatz aus Schema erstellen](#create-a-dataset-with-an-existing-schema)
* [Datensatz aus CSV-Datei erstellen](#create-a-dataset-with-a-csv-file)

### Datensatz mit vorhandenem Schema erstellen

Klicken Sie im Bildschirm *[!UICONTROL Datensatz erstellen]* auf **[!UICONTROL Datensatz aus Schema erstellen]**, um einen neuen leeren Datensatz zu erstellen.

![](../images/datasets/user-guide/create_dataset_schema.png)

Der Schritt *[!UICONTROL Schema auswählen]* wird angezeigt. Durchsuchen Sie die Schemaliste und wählen Sie das Schema aus, dem der Datensatz entsprechen soll, bevor Sie auf **[!UICONTROL Weiter]** klicken.

![](../images/datasets/user-guide/select_schema.png)

Der Schritt *[!UICONTROL Datensatz konfigurieren]* wird angezeigt. Geben Sie dem Datensatz einen Namen und eine optionale Beschreibung, bevor Sie auf **[!UICONTROL Beenden]** klicken, um den Datensatz zu erstellen.

![](../images/datasets/user-guide/configure_dataset_schema.png)

### Datensatz mit einer CSV-Datei erstellen

Wenn Sie einen Datensatz mit einer CSV-Datei erstellen, wird ein Ad-hoc-Schema erstellt, um dem Datensatz eine Struktur zu geben, die mit der bereitgestellten CSV-Datei übereinstimmt. Klicken Sie im Bildschirm *[!UICONTROL Datensatz erstellen]* auf das Feld **[!UICONTROL Datensatz aus CSV-Datei erstellen]**.

![](../images/datasets/user-guide/create_dataset_csv.png)

Der Schritt *[!UICONTROL Konfigurieren]* wird angezeigt. Geben Sie dem Datensatz einen Namen und eine optionale Beschreibung und klicken Sie auf **[!UICONTROL Weiter]**.

![](../images/datasets/user-guide/configure_dataset_csv.png)

Der Schritt *[!UICONTROL Daten hinzufügen]* wird angezeigt. Laden Sie die CSV-Datei hoch, indem Sie sie entweder in die Mitte des Bildschirms ziehen und dort ablegen oder auf **[!UICONTROL Durchsuchen]** klicken, um das Dateiverzeichnis zu durchsuchen. Die Datei darf maximal 10 Gigabyte groß sein. Klicken Sie nach dem Hochladen der CSV-Datei auf **[!UICONTROL Speichern]**, um den Datensatz zu erstellen.

>[!NOTE]
>
>Namen von CSV-Spalten müssen mit alphanumerischen Zeichen beginnen und dürfen ausschließlich Buchstaben, Ziffern und Unterstriche enthalten.

![](../images/datasets/user-guide/add_csv_data.png)

## Datensatz für Echtzeit-Kundenprofile aktivieren

Jeder Datensatz bietet die Möglichkeit, Kundenprofile mit den erfassten Daten anzureichern. To do so, the schema that the dataset adheres to must be compatible for use in [!DNL Real-time Customer Profile]. Ein kompatibles Schema erfüllt folgende Anforderungen:

* Das Schema weist mindestens ein Attribut auf, das als Identitätseigenschaft definiert wurde.
* Das Schema verfügt über eine Identitätseigenschaft, die als primäre Identität definiert wurde.

For more information on enabling a schema for [!DNL Profile], see the [Schema Editor user guide](../../xdm/tutorials/create-schema-ui.md).

Um einen Datensatz für Profil zu aktivieren, rufen Sie seinen *[!UICONTROL Datensatzaktivität]*-Bildschirm auf und klicken Sie auf den **[!UICONTROL Profil]**-Umschalter in der Spalte *[!UICONTROL Eigenschaften]*. Nach der Aktivierung werden Daten, die in den Datensatz aufgenommen werden, auch zum Ausfüllen von Kundenprofilen verwendet.

![](../images/datasets/user-guide/enable_dataset_profiles.png)

If a dataset already contains data and is then enabled for [!DNL Profile], the existing data is not consumed by [!DNL Profile]. After a dataset is enabled for [!DNL Profile], it is recommended that you re-ingest any existing data to have them populate customer profiles.

## Data Governance in einem Datensatz verwalten und durchsetzen

Data Usage Labeling and Enforcement (DULE) ist der zentrale Data Governance-Mechanismus in [!DNL Experience Platform]. Mit DULE-Bezeichnungen können Sie Datensätze und Felder entsprechend den für diese Daten geltenden Nutzungsrichtlinien kategorisieren. Weiterführende Informationen zu Bezeichnungen finden Sie in der [Übersicht zu Data Governance](../../data-governance/home.md) oder im [Benutzerhandbuch zu Datennutzungsbezeichnungen](../../data-governance/labels/overview.md), wo beschrieben wird, wie Sie Bezeichnungen auf Datensätze anwenden können.

## Datensatz löschen

Sie können einen Datensatz löschen, indem Sie zunächst auf den Bildschirm *[!UICONTROL Datensatzaktivität]* zugreifen. Klicken Sie dann auf **[!UICONTROL Datensatz löschen]**, um den gewünschten Datensatz zu löschen.

>[!NOTE]
>
>Datasets created and utilized by Adobe applications and services (such as Adobe Analytics, Adobe Audience Manager, or [!DNL Decisioning Service]) cannot be deleted.

![](../images/datasets/user-guide/delete_dataset.png)

Ein Bestätigungsdialog wird angezeigt. Klicken Sie auf **[!UICONTROL Löschen]**, um das Löschen des Datensatzes zu bestätigen.

![](../images/datasets/user-guide/confirm_delete.png)

## Profil-aktivierten Datensatz löschen

If a dataset is enabled for [!DNL Profile], deleting it through the UI disables the dataset for ingestion, but does not automatically delete the dataset in the backend. Damit der Datensatz einschließlich der Profil- und Identitätsdaten, die er enthält, vollständig gelöscht wird, muss eine zusätzliche Löschanfrage gestellt werden. For steps on how to properly delete data from the [!DNL Profile] store, see the [!DNL Real-time Customer Profile] API [sub-guide on profile system jobs, also known as &quot;delete requests&quot;](../../profile/api/profile-system-jobs.md).

## Datenerfassung überwachen

In the [!DNL Experience Platform] UI, click **[!UICONTROL Monitoring]** in the left-navigation. Mit dem *[!UICONTROL Monitoring]*-Dashboard können Sie die Status von aus der Batch- oder Streaming-Erfassung eingehenden Daten anzeigen. Um die Status einzelner Batches anzuzeigen, klicken Sie entweder auf *[!UICONTROL Batch End-to-End]* oder auf *[!UICONTROL Streaming End-to-End]*. Die Dashboards führen alle Batch- oder Streaming-Erfassungsläufe auf, einschließlich jener, die erfolgreich waren, fehlgeschlagen sind oder noch ausgeführt werden. Jede Auflistung enthält Details zum Batch, einschließlich der Batch-Kennung, dem Namen des Zieldatensatzes und der Zahl der erfassten Einträge. If the target dataset is enabled for [!DNL Profile], the number of ingested identity and profile records is also displayed.

![](../images/datasets/user-guide/batch_listing.png)

Sie können auf eine bestimmte **[!UICONTROL Batch-Kennung]** klicken, um auf das Dashboard *[!UICONTROL Batch-Übersicht]* zuzugreifen und Details zum Batch aufzurufen (einschließlich Fehlerprotokollen, falls der Batch nicht erfolgreich erfasst wurde).

![](../images/datasets/user-guide/batch_overview.png)

Wenn Sie den Batch löschen möchten, klicken Sie rechts oben im Dashboard auf **[!UICONTROL Batch löschen]**. Dadurch werden seine Einträge auch aus dem Datensatz entfernt, in dem der Batch ursprünglich erfasst wurde.

![](../images/datasets/user-guide/delete_batch.png)

## Nächste Schritte

This user guide provided instructions for performing common actions when working with datasets in the [!DNL Experience Platform] user interface. For steps on performing common [!DNL Platform] workflows involving datasets, please refer to the following tutorials:

* [Datensatz mit APIs erstellen](create.md)
* [Datensatzdaten mit der Data Access-API abfragen](../../data-access/home.md)
* [Datensatz für Echtzeit-Kundenprofil und Identity Service mithilfe von APIs konfigurieren](../../profile/tutorials/dataset-configuration.md)