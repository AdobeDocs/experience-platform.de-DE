---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Benutzerhandbuch zu Datensätzen
topic: datasets
translation-type: tm+mt
source-git-commit: 7d3f64db787aebe46179c0e08ad01878b0ad2877
workflow-type: tm+mt
source-wordcount: '1181'
ht-degree: 1%

---


# Benutzerhandbuch zu Datensätzen

Dieses Benutzerhandbuch enthält Anweisungen zur Durchführung allgemeiner Aktionen beim Arbeiten mit Datensätzen in der Benutzeroberfläche von Adobe Experience Platform.

## Erste Schritte

Dieses Benutzerhandbuch erfordert ein Verständnis der folgenden Komponenten von Adobe Experience Platform:

* [Datensätze](overview.md): Das Datenspeicherung- und Verwaltungskonstrukt für die Datenpersistenz in Experience Platform.
* [Erlebnis-Datenmodell (XDM)-System](../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Zusammensetzung](../../xdm/schema/composition.md)des Schemas: Erfahren Sie mehr über die grundlegenden Bausteine von XDM-Schemas, einschließlich der wichtigsten Grundsätze und Best Practices bei der Schema-Komposition.
   * [Schema-Editor](../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mithilfe des Schema-Editors in der Plattform-Benutzeroberfläche eigene benutzerdefinierte XDM-Schema erstellen.
* [Echtzeit-Profil](../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
* [Datenverwaltung](../../data-governance/home.md): Gewährleisten Sie die Einhaltung von Vorschriften, Einschränkungen und Richtlinien zur Nutzung von Kundendaten.

## Ansichten-Datensätze

Klicken Sie in der Benutzeroberfläche der Erlebnisplattform im linken Navigationsbereich auf **Datensätze** , um das Dashboard &quot; *Datasets* &quot;zu öffnen. Das Dashboard Liste alle verfügbaren Datensätze für Ihr Unternehmen. Details zu jedem aufgelisteten Datensatz werden angezeigt, einschließlich seines Namens, des Schemas, dem der Datensatz entspricht, und des Status der letzten Erfassungsausführung.

![](../images/datasets/user-guide/browse_datasets.png)

Klicken Sie auf den Namen eines Datensatzes, um auf den Bildschirm &quot; *DataSet-Aktivität* &quot;zuzugreifen und Details zum ausgewählten Datensatz anzuzeigen. Die Registerkarte &quot;Aktivität&quot;enthält ein Diagramm, das die Anzahl der zu verwendenden Meldungen sowie eine Liste erfolgreicher und fehlgeschlagener Stapel darstellt.

![](../images/datasets/user-guide/dataset_activity_1.png)
![](../images/datasets/user-guide/dataset_activity_2.png)

## Vorschau eines Datensatzes

Klicken Sie im Bildschirm &quot; *Dataset-Aktivität* &quot;auf &quot;Dataset- **Vorschau** &quot;in der oberen rechten Ecke des Bildschirms, um bis zu 100 Datenzeilen Vorschau. Wenn der Datensatz leer ist, wird der Link &quot;Vorschau&quot;deaktiviert und stattdessen angegeben, dass keine **Vorschau verfügbar** ist.

![](../images/datasets/user-guide/click_to_preview.png)

Im Fenster &quot;Vorschau&quot;wird die hierarchische Ansicht des Schemas für den Datensatz rechts angezeigt.

![](../images/datasets/user-guide/preview_dataset.png)

Für stabilere Methoden zum Zugriff auf Ihre Daten bietet Experience Platform nachgelagerte Dienste wie Abfrage Service und JupyterLab zur Untersuchung und Analyse von Daten. Weitere Informationen finden Sie in den folgenden Dokumenten:

* [Übersicht über den Abfrage Service](../../query-service/home.md)
* [JupyterLab-Benutzerhandbuch](../../data-science-workspace/jupyterlab/overview.md)

## Datensatz erstellen {#create}

Um einen neuen Datensatz zu erstellen, klicken Sie im Dashboard &quot; **Datensatz** &quot;auf &quot;Datensatz ** erstellen&quot;, um einen neuen Datensatz zu erstellen.

![](../images/datasets/user-guide/click_to_create.png)

Im nächsten Bildschirm werden Ihnen die folgenden zwei Optionen zum Erstellen eines neuen Datensatzes angezeigt:

* [Datensatz aus Schema erstellen](#create-a-dataset-with-an-existing-schema)
* [Datensatz aus CSV-Datei erstellen](#create-a-dataset-with-a-csv-file)

### Datensatz mit einem vorhandenen Schema erstellen

Klicken Sie im Bildschirm &quot;Datensatz *erstellen* &quot;auf Datensatz aus Schema **** erstellen, um einen neuen leeren Datensatz zu erstellen.

![](../images/datasets/user-guide/create_dataset_schema.png)

Der Schritt Schema *auswählen* wird angezeigt. Durchsuchen Sie die Liste Schema und wählen Sie das Schema aus, dem der Datensatz entsprechen soll, bevor Sie auf **Weiter** klicken.

![](../images/datasets/user-guide/select_schema.png)

Der Schritt zum *Konfigurieren des Datensatzes* wird angezeigt. Geben Sie dem Datensatz einen Namen und eine optionale Beschreibung ein und klicken Sie dann auf **Fertig stellen** , um den Datensatz zu erstellen.

![](../images/datasets/user-guide/configure_dataset_schema.png)

### Datensatz mit einer CSV-Datei erstellen

Wenn ein Datensatz mit einer CSV-Datei erstellt wird, wird ein Ad-hoc-Schema erstellt, um dem Datensatz eine Struktur zu geben, die mit der bereitgestellten CSV-Datei übereinstimmt. Klicken Sie im Bildschirm &quot;Datensatz *erstellen* &quot;auf das Feld zum **Erstellen eines Datensatzes aus einer CSV-Datei**.

![](../images/datasets/user-guide/create_dataset_csv.png)

The *Configure* step appears. Geben Sie dem Datensatz einen Namen und eine optionale Beschreibung ein und klicken Sie dann auf **Weiter**.

![](../images/datasets/user-guide/configure_dataset_csv.png)

Der *Hinzufügen Datenschritt* wird angezeigt. Laden Sie die CSV-Datei hoch, indem Sie sie entweder in die Mitte Ihres Bildschirms ziehen und dort ablegen, oder klicken Sie auf **Durchsuchen** , um das Dateiverzeichnis zu durchsuchen. Die Datei kann bis zu zehn Gigabyte groß sein. Klicken Sie nach dem Hochladen der CSV-Datei auf **Speichern** , um den Datensatz zu erstellen.

>[!NOTE] CSV-Spaltennamen müssen mit alphanumerischen Zeichen Beginn haben und dürfen nur Buchstaben, Ziffern und Unterstriche enthalten.

![](../images/datasets/user-guide/add_csv_data.png)

## Datensatz für Echtzeit-Kundenprofile aktivieren

Jeder Datensatz hat die Möglichkeit, Kundendaten mit den erfassten Daten zu bereichern. Zu diesem Zweck muss das Schema, das der Datensatz einhält, für die Verwendung im Echtzeit-Customer-Profil kompatibel sein. Ein kompatibles Schema erfüllt folgende Anforderungen:

* Das Schema hat mindestens ein Attribut, das als Identitätseigenschaft angegeben wurde.
* Das Schema verfügt über eine Identitätseigenschaft, die als primäre Identität definiert ist.

Weitere Informationen zum Aktivieren eines Schemas für Profil finden Sie im [Schema-Editor-Benutzerhandbuch](../../xdm/tutorials/create-schema-ui.md).

Um einen Datensatz zum Profil zu aktivieren, rufen Sie den Anzeigebereich &quot; *DataSet-Aktivität* &quot;auf und klicken Sie in der Spalte &quot; **Eigenschaften** &quot;auf den Umschalter &quot; *Profil* &quot;. Nach der Aktivierung werden Daten, die in den Dataset aufgenommen werden, auch zum Ausfüllen von Kundendaten verwendet.

![](../images/datasets/user-guide/enable_dataset_profiles.png)

Wenn ein Datensatz bereits Daten enthält und dann zum Profil aktiviert ist, werden die vorhandenen Daten nicht von Profil genutzt. Nachdem ein Datensatz zum Profil aktiviert wurde, sollten Sie alle vorhandenen Daten neu erfassen, damit sie die Profil der Kunden ausfüllen.

## Verwalten und Erzwingen der Datenverwaltung in einem Datensatz

Datennutzungskennzeichnung und -durchsetzung (DULE) ist der zentrale Datenverwaltungs-Mechanismus für Experience Platform. Mit den DULE-Beschriftungen können Sie Datensätze und Felder entsprechend den für diese Daten geltenden Nutzungsrichtlinien kategorisieren. Weitere Informationen zu Beschriftungen finden Sie in der Übersicht [zur](../../data-governance/home.md) Datenverwaltung oder im Benutzerhandbuch [zu den](../../data-governance/labels/overview.md) Datenverwendungsbeschriftungen, in dem beschrieben wird, wie Sie Beschriftungen auf Datensätze anwenden.

## Löschen eines Datensatzes

Sie können einen Datensatz löschen, indem Sie zunächst auf den Anzeigebereich &quot; *DataSet-Aktivität* &quot;zugreifen. Klicken Sie dann auf &quot;Datensatz **löschen&quot;** , um ihn zu löschen.

>[!NOTE] Datasets, die von Adobe-Anwendungen und -Diensten erstellt und verwendet werden (z. B. Adobe Analytics, Adobe Audience Manager oder Entscheidungsdienst), können nicht gelöscht werden.

![](../images/datasets/user-guide/delete_dataset.png)

Ein Bestätigungsfeld wird angezeigt. Klicken Sie auf **Löschen** , um das Löschen des Datensatzes zu bestätigen.

![](../images/datasets/user-guide/confirm_delete.png)

## Löschen eines Profil-aktivierten Datensatzes

Wenn ein Datensatz zum Profil aktiviert ist, wird beim Löschen über die Benutzeroberfläche der Datensatz zur Erfassung deaktiviert, der Datensatz jedoch nicht automatisch im Backend gelöscht. Damit der Datensatz einschließlich der Profil- und Identitätsdaten, die er bereitstellt, vollständig gelöscht werden kann, muss eine zusätzliche Löschanforderung gestellt werden. Anweisungen zum ordnungsgemäßen Löschen von Daten aus dem Profil Store finden Sie im [Unterhandbuch zur Echtzeit-Client-Profil-API zu Systemaufträgen im Profil, auch als &quot;Anforderungen löschen&quot;bezeichnet](../../profile/api/profile-system-jobs.md).

## Überwachung der Datenaufnahme

Klicken Sie in der Benutzeroberfläche der Experience Platform im linken Navigationsbereich auf **Überwachung** . Mit dem *Überwachungs* -Dashboard können Sie den Status von Eingangsdaten aus der Batch- oder Streaming-Erfassung Ansicht werden. Um den Status der einzelnen Stapel Ansicht, klicken Sie entweder auf *Stapel von Ende zu Ende* oder auf *Streaming von Ende zu Ende*. Die Dashboards führen alle Batch- oder Streaming-Aufrufe aus, einschließlich solcher, die erfolgreich sind, fehlgeschlagen sind oder noch ausgeführt werden. Jede Auflistung enthält Details zum Stapel, einschließlich der Stapel-ID, dem Namen des Datensatzes zur Zielgruppe und der Anzahl der erfassten Datensätze. Wenn der Zielgruppe-Datensatz zum Profil aktiviert ist, wird auch die Anzahl der erfassten Identitäts- und Profil-Datensätze angezeigt.

![](../images/datasets/user-guide/batch_listing.png)

Sie können auf eine einzelne **Stapel-ID** klicken, um auf das Dashboard *Stapelübersicht* zuzugreifen und Details zum Stapel anzuzeigen, einschließlich Fehlermeldungen, falls der Stapel nicht erfasst werden sollte.

![](../images/datasets/user-guide/batch_overview.png)

Wenn Sie den Stapel löschen möchten, klicken Sie dazu auf Stapel **löschen** , der rechts oben im Dashboard gefunden wurde. Dadurch werden auch die Datensätze aus dem Datensatz entfernt, in den der Stapel ursprünglich aufgenommen wurde.

![](../images/datasets/user-guide/delete_batch.png)

## Nächste Schritte

Dieses Benutzerhandbuch enthält Anweisungen zum Ausführen allgemeiner Aktionen beim Arbeiten mit Datensätzen in der Benutzeroberfläche von Experience Platform. Schritte zum Ausführen gemeinsamer Plattform-Workflows mit Datensätzen finden Sie in den folgenden Lernprogrammen:

* [Erstellen eines Datensatzes mit APIs](create.md)
* [Abfrage von Datensatzdaten mit der Datenzugriffs-API](../../data-access/home.md)
* [Datensatz für Echtzeit-Kundenprofile und Identitätsdienst mithilfe von APIs konfigurieren](../../profile/tutorials/dataset-configuration.md)