---
keywords: Experience Platform;Startseite;beliebte Themen;Datensatz aktivieren;Datensatz;Datensatz;Datensatz
solution: Experience Platform
title: Handbuch zur Benutzeroberfläche von Datasets
topic-legacy: datasets
description: Erfahren Sie, wie Sie allgemeine Aktionen beim Arbeiten mit Datensätzen in der Adobe Experience Platform-Benutzeroberfläche durchführen.
exl-id: f0d59d4f-4ebd-42cb-bbc3-84f38c1bf973
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1140'
ht-degree: 71%

---

# Handbuch zur Benutzeroberfläche von Datasets

Dieses Benutzerhandbuch enthält Anweisungen zur Ausführung allgemeiner Aktionen beim Verwenden von Datensätzen in der Benutzeroberfläche von Adobe Experience Platform.

## Erste Schritte

Das Benutzerhandbuch setzt ein grundlegendes Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Datensätze](overview.md): Das Speicher- und Verwaltungskonstrukt für Datenpersistenz in [!DNL Experience Platform].
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   * [Schema-Editor](../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie Ihre eigenen benutzerdefinierten XDM-Schema mithilfe der  [!DNL Schema Editor] in der  [!DNL Platform] Benutzeroberfläche erstellen.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
* [[!DNL Adobe Experience Platform Data Governance]](../../data-governance/home.md): Sorgen Sie bei der Nutzung von Kundendaten für die Einhaltung von Vorschriften, Begrenzungen und Richtlinien.

## Anzeigen von Datensätzen

Klicken Sie in der Benutzeroberfläche [!DNL Experience Platform] auf **[!UICONTROL Datensätze]** in der linken Navigation, um das Dashboard **[!UICONTROL Datensätze]** zu öffnen. Das Dashboard listet alle verfügbaren Datensätze für Ihre Organisation auf. Zu jedem aufgelisteten Datensatz werden Details angezeigt, einschließlich seines Namens, des Schemas, dem der Datensatz entspricht, und des Status des letzten Erfassungslaufs.

![](../images/datasets/user-guide/browse_datasets.png)

Klicken Sie auf den Namen eines Datensatzes, um auf seinen **[!UICONTROL Datensatzaktivität]**-Bildschirm zuzugreifen und Details zum ausgewählten Datensatz anzuzeigen. Der Tab „Aktivität“ enthält ein Diagramm, das die Rate der konsumierten Nachrichten sowie eine Liste erfolgreicher und fehlgeschlagener Batches visuell darstellt.

![](../images/datasets/user-guide/dataset_activity_1.png)
![](../images/datasets/user-guide/dataset_activity_2.png)

## Vorschau für Datensatz anzeigen

Klicken Sie im Bildschirm **[!UICONTROL Datensatzaktivität]** oben rechts im Bildschirm auf **[!UICONTROL Vorschau für Datensatz anzeigen]**, um bis zu 100 Datenzeilen als Vorschau anzuzeigen. Wenn der Datensatz leer ist, wird der Link &quot;Vorschau&quot;deaktiviert und stattdessen angegeben, dass die Vorschau nicht verfügbar ist.

![](../images/datasets/user-guide/click_to_preview.png)

Im Vorschaufenster wird rechts für den Datensatz die hierarchische Ansicht des Schemas angezeigt.

![](../images/datasets/user-guide/preview_dataset.png)

Für stabilere Methoden zum Zugriff auf Ihre Daten stellt [!DNL Experience Platform] nachgelagerte Dienste wie [!DNL Query Service] und [!DNL JupyterLab] zur Untersuchung und Analyse von Daten bereit. Weiterführende Informationen finden Sie in folgenden Dokumenten:

* [Query Service – Übersicht](../../query-service/home.md)
* [JupyterLab-Benutzerhandbuch](../../data-science-workspace/jupyterlab/overview.md)

## Erstellen eines Datensatzes {#create}

Um einen neuen Datensatz zu erstellen, klicken Sie zunächst im Dashboard **[!UICONTROL Datensätze]** auf **[!UICONTROL Datensatz erstellen]**.

![](../images/datasets/user-guide/click_to_create.png)

Im folgenden Bildschirm werden Ihnen die folgenden zwei Optionen zum Erstellen eines neuen Datensatzes angezeigt:

* [Datensatz aus Schema erstellen](#schema)
* [Datensatz aus CSV-Datei erstellen](#csv)

### Datensatz mit vorhandenem Schema erstellen  {#schema}

Klicken Sie im Bildschirm **[!UICONTROL Datensatz erstellen]** auf **[!UICONTROL Datensatz aus Schema erstellen]**, um einen neuen leeren Datensatz zu erstellen.

![](../images/datasets/user-guide/create_dataset_schema.png)

Der Schritt **[!UICONTROL Schema auswählen]** wird angezeigt. Durchsuchen Sie die Schemaliste und wählen Sie das Schema aus, dem der Datensatz entsprechen soll, bevor Sie auf **[!UICONTROL Weiter]** klicken.

![](../images/datasets/user-guide/select_schema.png)

Der Schritt **[!UICONTROL Datensatz konfigurieren]** wird angezeigt. Geben Sie dem Datensatz einen Namen und eine optionale Beschreibung, bevor Sie auf **[!UICONTROL Beenden]** klicken, um den Datensatz zu erstellen.

![](../images/datasets/user-guide/configure_dataset_schema.png)

### Datensatz mit einer CSV-Datei erstellen  {#csv}

Wenn Sie einen Datensatz mit einer CSV-Datei erstellen, wird ein Ad-hoc-Schema erstellt, um dem Datensatz eine Struktur zu geben, die mit der bereitgestellten CSV-Datei übereinstimmt. Klicken Sie im Bildschirm **[!UICONTROL Datensatz erstellen]** auf das Feld **[!UICONTROL Datensatz aus CSV-Datei erstellen]**.

![](../images/datasets/user-guide/create_dataset_csv.png)

Der Schritt **[!UICONTROL Konfigurieren]** wird angezeigt. Geben Sie dem Datensatz einen Namen und eine optionale Beschreibung und klicken Sie auf **[!UICONTROL Weiter]**.

![](../images/datasets/user-guide/configure_dataset_csv.png)

Der Schritt **[!UICONTROL Daten hinzufügen]** wird angezeigt. Laden Sie die CSV-Datei hoch, indem Sie sie entweder in die Mitte des Bildschirms ziehen und dort ablegen oder auf **[!UICONTROL Durchsuchen]** klicken, um das Dateiverzeichnis zu durchsuchen. Die Datei darf maximal 10 Gigabyte groß sein. Klicken Sie nach dem Hochladen der CSV-Datei auf **[!UICONTROL Speichern]**, um den Datensatz zu erstellen.

>[!NOTE]
>
>Namen von CSV-Spalten müssen mit alphanumerischen Zeichen beginnen und dürfen ausschließlich Buchstaben, Ziffern und Unterstriche enthalten.

![](../images/datasets/user-guide/add_csv_data.png)

## Datensatz für Echtzeit-Kundenprofile aktivieren {#enable-profile}

Jeder Datensatz bietet die Möglichkeit, Kundenprofile mit den erfassten Daten anzureichern. Zu diesem Zweck muss das Schema, dem der Datensatz entspricht, für die Verwendung in [!DNL Real-time Customer Profile] kompatibel sein. Ein kompatibles Schema erfüllt folgende Anforderungen:

* Das Schema weist mindestens ein Attribut auf, das als Identitätseigenschaft definiert wurde.
* Das Schema verfügt über eine Identitätseigenschaft, die als primäre Identität definiert wurde.

Weitere Informationen zum Aktivieren eines Schemas für [!DNL Profile] finden Sie im [Schema-Editor-Benutzerhandbuch](../../xdm/tutorials/create-schema-ui.md).

Um einen Datensatz für Profil zu aktivieren, rufen Sie seinen **[!UICONTROL Datensatzaktivität]**-Bildschirm auf und klicken Sie auf den **[!UICONTROL Profil]**-Umschalter in der Spalte **[!UICONTROL Eigenschaften]**. Nach der Aktivierung werden Daten, die in den Datensatz aufgenommen werden, auch zum Ausfüllen von Kundenprofilen verwendet.

>[!NOTE]
>
>Wenn ein Datensatz bereits Daten enthält und dann für [!DNL Profile] aktiviert ist, werden die vorhandenen Daten nicht automatisch von [!DNL Profile] genutzt. Nachdem ein Datensatz für [!DNL Profile] aktiviert wurde, sollten Sie alle vorhandenen Daten neu erfassen, damit sie zu den Profilen der Kunden beitragen.

![](../images/datasets/user-guide/enable_dataset_profiles.png)

## Data Governance in einem Datensatz verwalten und durchsetzen

Mit Datennutzungsbeschriftungen können Sie Daten anhand der für diese Daten geltenden Nutzungsrichtlinien kategorisieren. Weiterführende Informationen zu Bezeichnungen finden Sie in der [Übersicht zu Data Governance](../../data-governance/home.md) oder im [Benutzerhandbuch zu Datennutzungsbezeichnungen](../../data-governance/labels/overview.md), wo beschrieben wird, wie Sie Bezeichnungen auf Datensätze anwenden können.

## Datensatz löschen

Sie können einen Datensatz löschen, indem Sie zunächst auf den Bildschirm **[!UICONTROL Datensatzaktivität]** zugreifen. Klicken Sie dann auf **[!UICONTROL Datensatz löschen]**, um den gewünschten Datensatz zu löschen.

>[!NOTE]
>
>Datasets, die von Adobe-Anwendungen und -Diensten erstellt und verwendet werden (z. B. Adobe Analytics, Adobe Audience Manager oder [!DNL Offer Decisioning]), können nicht gelöscht werden.

![](../images/datasets/user-guide/delete_dataset.png)

Ein Bestätigungsdialog wird angezeigt. Klicken Sie auf **[!UICONTROL Löschen]**, um das Löschen des Datensatzes zu bestätigen.

![](../images/datasets/user-guide/confirm_delete.png)

## Profil-aktivierten Datensatz löschen

Wenn ein Datensatz für [!DNL Profile] aktiviert ist, wird er beim Löschen dieses Datensatzes über die Benutzeroberfläche sowohl aus dem Data Lake als auch aus dem Profil-Store in Platform gelöscht.

Sie können einen Datensatz nur aus dem [!DNL Profile]-Speicher löschen (wobei die Daten im Data Lake verbleiben), indem Sie die Echtzeit-Customer Profil-API verwenden. Weitere Informationen finden Sie im Handbuch [API-Endpunkt für Systemaufträge](../../profile/api/profile-system-jobs.md) des Profils.

## Überwachen der Datenerfassung

Klicken Sie in der Benutzeroberfläche [!DNL Experience Platform] in der linken Navigation auf **[!UICONTROL Monitoring]**. Mit dem **[!UICONTROL Monitoring]**-Dashboard können Sie die Status von aus der Batch- oder Streaming-Erfassung eingehenden Daten anzeigen. Um die Status einzelner Batches anzuzeigen, klicken Sie entweder auf **[!UICONTROL Batch End-to-End]** oder auf **[!UICONTROL Streaming End-to-End]**. Die Dashboards führen alle Batch- oder Streaming-Erfassungsläufe auf, einschließlich jener, die erfolgreich waren, fehlgeschlagen sind oder noch ausgeführt werden. Jede Auflistung enthält Details zum Batch, einschließlich der Batch-Kennung, dem Namen des Zieldatensatzes und der Zahl der erfassten Einträge. Wenn der Zielgruppe-Datensatz für [!DNL Profile] aktiviert ist, wird auch die Anzahl der erfassten Identitäts- und Profil-Datensätze angezeigt.

![](../images/datasets/user-guide/batch_listing.png)

Sie können auf eine bestimmte **[!UICONTROL Batch-Kennung]** klicken, um auf das Dashboard **[!UICONTROL Batch-Übersicht]** zuzugreifen und Details zum Batch aufzurufen (einschließlich Fehlerprotokollen, falls der Batch nicht erfolgreich erfasst wurde).

![](../images/datasets/user-guide/batch_overview.png)

Wenn Sie den Batch löschen möchten, klicken Sie rechts oben im Dashboard auf **[!UICONTROL Batch löschen]**. Dadurch werden seine Einträge auch aus dem Datensatz entfernt, in dem der Batch ursprünglich erfasst wurde.

![](../images/datasets/user-guide/delete_batch.png)

## Nächste Schritte

Dieses Benutzerhandbuch enthält Anweisungen zum Ausführen allgemeiner Aktionen beim Arbeiten mit Datensätzen in der [!DNL Experience Platform]-Benutzeroberfläche. Anweisungen zum Durchführen allgemeiner Workflows mit Datensätzen finden Sie in den folgenden Übungen:[!DNL Platform]

* [Datensatz mit APIs erstellen](create.md)
* [Datensatzdaten mit der Data Access-API abfragen](../../data-access/home.md)
* [Datensatz für Echtzeit-Kundenprofil und Identity Service mithilfe von APIs konfigurieren](../../profile/tutorials/dataset-configuration.md)
