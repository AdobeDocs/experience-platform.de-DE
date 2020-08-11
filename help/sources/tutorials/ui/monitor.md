---
keywords: Experience Platform;home;popular topics; monitor accounts; monitor dataflows
description: Source connectors in Adobe Experience Platform provide the ability to ingest externally sourced data on a scheduled basis. This tutorial provides steps for viewing existing accounts and dataflows from the Sources workspace.
solution: Experience Platform
title: Überwachen von Konten und Datenflüssen
topic: overview
translation-type: tm+mt
source-git-commit: 8bdd0493444c2c3b0f56db1166a6fa5d616e41be
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 8%

---


# Überwachen von Konten und Datenflüssen in der Benutzeroberfläche

Die Source Connectors in Adobe Experience Platform bieten die Möglichkeit, extern beschaffte Daten planmäßig zu erfassen. This tutorial provides steps for viewing existing accounts and dataflows from the *[!UICONTROL Sources]* workspace.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [Experience-Datenmodell (XDM)-System](../../../xdm/home.md)[!DNL Experience Platform]: Das standardisierte Framework, mit dem Kundenerlebnisdaten organisiert.
   - [Grundlagen der Schemakomposition](../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   - [Schema Editor tutorial](../../../xdm/tutorials/create-schema-ui.md): Learn how to create custom schemas using the Schema Editor UI.
- [Echtzeit-Kundenprofil](../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

## Monitor accounts

Log in to [Adobe Experience Platform](https://platform.adobe.com) and then select **[!UICONTROL Sources]** from the left navigation bar to access the *[!UICONTROL Sources]* workspace. Im Anzeigebereich &quot; *[!UICONTROL Katalog]* &quot;werden verschiedene Quellen angezeigt, für die Sie Konten und Datenflüsse erstellen können. Jede Quelle zeigt die Anzahl der vorhandenen Konten und Datenflüsse, die ihnen zugeordnet sind.

Wählen Sie *[!UICONTROL Konten]* aus der oberen Kopfzeile zur Ansicht vorhandener Konten.

![Katalog](../../images/tutorials/monitor/catalog-accounts.png)

The *[!UICONTROL Accounts]* pages appears. On this page is a list of viewable accounts, including information about their source, username, number of dataflows, and date of creation.

Select the funnel icon on the top left to launch the sort window.

![accounts](../../images/tutorials/monitor/accounts-list.png)

Über das Sortierfeld können Sie auf Konten aus einer bestimmten Quelle zugreifen. Wählen Sie die Quelle aus, mit der Sie arbeiten möchten, und wählen Sie das Konto in der Liste auf der rechten Seite aus.

![accounts-select](../../images/tutorials/monitor/accounts-sort.png)

Auf der Seite &quot; *[!UICONTROL Konten]* &quot;können Sie eine Liste mit vorhandenen Datenflüssen oder Zielgruppen-Datensätzen, die mit dem Konto, auf das Sie zugegriffen haben, verknüpft sind, Ansicht haben.

![Datenflüsse](../../images/tutorials/monitor/dataflows.png)

## Überwachen von Datenflüssen

Datenflüsse können direkt von der Seite &quot; *[!UICONTROL Katalog]* &quot;aus aufgerufen werden, ohne *[!UICONTROL Konten]* anzuzeigen. Wählen Sie *[!UICONTROL Datenflüsse]* aus der oberen Kopfzeile aus, um eine Liste der vorhandenen Datenflüsse Ansicht.

![catalog-dataflows](../../images/tutorials/monitor/catalog-dataflows.png)

Eine Liste der vorhandenen Datenflüsse wird angezeigt. Auf dieser Seite finden Sie eine Liste mit anzeigbaren Datenflüssen, einschließlich Informationen zu Quelle, Benutzername, Anzahl der Datenflüsse und Status. Wählen Sie das Trichtersymbol oben links, das sortiert werden soll.

![dataflows-Liste](../../images/tutorials/monitor/dataflows-list.png)

Das Sortierfeld wird angezeigt. Wählen Sie im Bildlaufmenü die Quelle aus, auf die Sie zugreifen möchten, und wählen Sie dann in der Liste auf der rechten Seite den Datendurchlauf aus.

![sort-dataflows](../../images/tutorials/monitor/dataflows-sort.png)

Auf der Seite &quot; *[!UICONTROL Dataflow-Aktivität]* &quot;finden Sie Angaben zur Anzahl der erfassten und fehlgeschlagenen Datensätze sowie Informationen zum Datenaflow-Status und zur Verarbeitungszeit. Wählen Sie das Kalendersymbol oberhalb des Datenflusses aus, um den Zeitraum Ihrer Erfassungsdatensätze anzupassen.

![datflow-Aktivität](../../images/tutorials/monitor/dataflow-activity.png)

Der Kalender ermöglicht die Ansicht der verschiedenen Zeitrahmen für erfasste Datensätze. You can choose to select one of the two pre-set options *[!UICONTROL Last 7 days]* or *[!UICONTROL Last 30 days]*. Alternatively, you can set a custom time frame using the calendar. Select your time frame of choice and select **[!UICONTROL Apply]** to continue.

![flow-calendar](../../images/tutorials/monitor/flow-calendar.png)

Standardmäßig wird in der Aktivität *[!UICONTROL &quot;]* Dataflow&quot;das Bedienfeld &quot; *[!UICONTROL Eigenschaften]* &quot;angezeigt, das mit dem Datenflug verknüpft ist. Wählen Sie den Fluss aus, der von der Liste ausgeführt wird, um die zugehörigen Metadaten einschließlich Informationen zur eindeutigen Ausführen-ID anzuzeigen.

Wählen Sie &quot; **[!UICONTROL Datenaflow-Run-Beginn]** &quot;aus, um auf die *[!UICONTROL Datenaflow-Übersicht]* zuzugreifen.

![runs](../../images/tutorials/monitor/run-metadata.png)

The *[!UICONTROL Dataflow run overview]* displays information on the dataflow including its metadata, *[!UICONTROL Partial ingestion]* status, and assigned *[!UICONTROL Error threshold]*. The upper header also includes an *[!UICONTROL Error summary]*. Die *[!UICONTROL Fehlerzusammenfassung]* enthält den spezifischen Fehler der obersten Ebene, der anzeigt, in welchem Schritt beim Erfassungsvorgang ein Fehler aufgetreten ist.

![dataflow-run-overview](../../images/tutorials/monitor/dataflow-run-overview.png)

In der folgenden Tabelle finden Sie Fehlercodes, die in der *[!UICONTROL Fehlerzusammenfassung]* angezeigt werden können.

| Error code | Fehlermeldung |
| ---------- | ----------- |
| `CONNECTOR-1001-500` | &quot;Bei der Aktivität zum Kopieren ist ein Problem aufgetreten.&quot; |
| `CONNECTOR-2001-500` | &quot;Beim Kopieren der Experience Platform in den Datensatz ist ein Problem aufgetreten.&quot; |
| `CONNECTOR-3001-500` | &quot;Beim Flow-Provider ist beim Erstellen des Stapels mit der Massen-Erfassungsschnittstelle ein Problem aufgetreten.&quot; |

Die untere Hälfte des Bildschirms enthält Informationen zu *[!UICONTROL Dataflow-Ausführungsfehlern]*. Von hier aus können Sie auch die erfassten Dateien Ansicht, die Fehlerdiagnose für Vorschau und Download durchführen oder das Dateimanifest herunterladen.

Im Abschnitt &quot; *[!UICONTROL Datenflussausführungsfehler]* &quot;werden der *[!UICONTROL Fehlercode]*, die Anzahl der fehlgeschlagenen Datensätze und die Informationen zum Fehler angezeigt.

Wählen Sie **[!UICONTROL Fehlerdiagnose]** für Vorschauen aus, um weitere Informationen zum Erfassungsfehler anzuzeigen.

![Datenflusslauffehler](../../images/tutorials/monitor/dataflow-run-errors.png)

The *[!UICONTROL Error diagnostics preview]* panel appears. This screen displays specific information regarding the ingestion failure, including the *[!UICONTROL File name]*, *[!UICONTROL Error code]*, the name of the column in which the error occurred, and a description of the error.

Dieser Abschnitt enthält auch eine Vorschau der Spalte, die den Fehler enthält.

> [!IMPORTANT] Zur Aktivierung der *[!UICONTROL Fehlerdiagnose-Vorschau]* müssen Sie beim Konfigurieren eines Datenflusses die *[!UICONTROL teilweise Erfassung]* und *[!UICONTROL Fehlerdiagnose]* aktivieren. Dadurch kann das System alle während der Ausführung erfassten Datensätze überprüfen.

![Preview-error-diagnostics](../../images/tutorials/monitor/preview-error-diagnostics.png)

After previewing the errors, you can select **[!UICONTROL Download]** from within the *[UICONTROL dataflow runs overview]* panel to access full error diagnostics and download the file manifest. See the documents on [error diagnostics](../../../ingestion/batch-ingestion/partial.md#retrieve-errors) and [downloading metadata](../../../ingestion/batch-ingestion/partial.md#download-metadata) for more information.

![Preview-error-diagnostics](../../images/tutorials/monitor/download.png)

Weitere Informationen zur Überwachung von Datenflüssen und zur Erfassung finden Sie im Lernprogramm zur [Überwachung von Streaming-Datenflüssen](../../../ingestion/quality/monitor-data-flows.md).

## Nächste Schritte

By following this tutorial, you have successfully accessed existing accounts and dataflows from the *[!UICONTROL Sources]* workspace. Incoming data can now be used by downstream [!DNL Platform] services such as [!DNL Real-time Customer Profile] and [!DNL Data Science Workspace]. Weitere Informationen finden Sie in den folgenden Dokumenten:

- [Übersicht über das Echtzeit-Kundenprofil](../../../profile/home.md)
- [Übersicht über den Data Science Workspace](../../../data-science-workspace/home.md)