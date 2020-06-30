---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Konfigurieren eines Datenflusses für einen Datenbankanschluss in der Benutzeroberfläche
topic: overview
translation-type: tm+mt
source-git-commit: d3c725c4760acb3857a67d0d30b24732c963a030
workflow-type: tm+mt
source-wordcount: '1043'
ht-degree: 1%

---


# Konfigurieren eines Datenflusses für einen Datenbankanschluss in der Benutzeroberfläche

Ein Datennachweis ist eine geplante Aufgabe, mit der Daten aus einer Platform abgerufen und in einen Dataset aufgenommen werden. In diesem Lernprogramm werden Schritte zum Konfigurieren eines neuen Datenflusses mit Ihrem Datenbankanschluss beschrieben.

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

- [Erlebnis-Datenmodell (XDM)-System](../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   - [Grundlagen der Zusammensetzung](../../../../xdm/schema/composition.md)des Schemas: Erfahren Sie mehr über die grundlegenden Bausteine von XDM-Schemas, einschließlich der wichtigsten Grundsätze und Best Practices bei der Schema-Komposition.
   - [Schema-Editor-Lernprogramm](../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
- [Echtzeit-Profil](../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

Außerdem müssen Sie bei diesem Lernprogramm bereits einen Datenbankanschluss erstellt haben. Eine Liste von Übungen zum Erstellen verschiedener Datenbankschnittstellen in der Benutzeroberfläche finden Sie in der Übersicht über die [Quellschnittstellen](../../../home.md).

## Daten auswählen

Nach dem Erstellen des Datenbankconnectors wird der Schritt &quot;Daten ** auswählen&quot;angezeigt und bietet eine interaktive Oberfläche, über die Sie die Datenbankhierarchie untersuchen können.

- Die linke Hälfte der Oberfläche ist ein Browser, der die Liste der Datenbanken Ihres Kontos anzeigt.
- In der rechten Hälfte der Oberfläche können Sie bis zu 100 Datenzeilen Vorschau werden.

Wählen Sie die gewünschte Datenbank aus und klicken Sie auf **[!UICONTROL Weiter]**.

![](../../../images/tutorials/dataflow/databases/add-data.png)

## Zuordnen von Datenfeldern zu einem XDM-Schema

Der *Zuordnungsschritt* wird angezeigt und bietet eine interaktive Schnittstelle, um die Quelldaten einem Platform-Datensatz zuzuordnen.

Wählen Sie einen Datensatz, in den eingehende Daten aufgenommen werden sollen. Sie können entweder einen vorhandenen Datensatz verwenden oder einen neuen Datensatz erstellen.

### Vorhandenen Datensatz verwenden

Um Daten in einen vorhandenen Datensatz zu erfassen, wählen Sie &quot; **[!UICONTROL Vorhandener Datensatz]**&quot;und klicken Sie dann auf das Dataset-Symbol.

![](../../../images/tutorials/dataflow/databases/existing-dataset.png)

Das Dialogfeld &quot;Datensatz *[!UICONTROL auswählen]* &quot;wird angezeigt. Suchen Sie den gewünschten Datensatz, wählen Sie ihn aus und klicken Sie dann auf **[!UICONTROL Weiter]**.

![](../../../images/tutorials/dataflow/databases/select-existing-dataset.png)

### Verwenden eines neuen Datensatzes

Um Daten in einen neuen Datensatz zu erfassen, wählen Sie &quot; **[!UICONTROL Neuer Datensatz]** &quot;und geben Sie einen Namen und eine Beschreibung für den Datensatz in die entsprechenden Felder ein.

Sie können ein Schema anhängen, indem Sie in der Suchleiste &quot;Schema **[!UICONTROL auswählen]** &quot;einen Schema eingeben. Sie können auch das Dropdownsymbol auswählen, um eine Liste der vorhandenen Schema anzuzeigen. Alternativ können Sie die **[!UICONTROL erweiterte Suche]** auswählen, um einen Bildschirm mit vorhandenen Schemas mit den entsprechenden Details anzuzeigen.

![](../../../images/tutorials/dataflow/databases/new-dataset.png)

Das Dialogfeld &quot;Schema[!UICONTROL auswählen] &quot;wird angezeigt. Wählen Sie das Schema aus, das Sie auf den neuen Datensatz anwenden möchten, und klicken Sie dann auf **[!UICONTROL Fertig]**.

![](../../../images/tutorials/dataflow/databases/select-existing-schema.png)

Je nach Bedarf können Sie Felder direkt zuordnen oder mithilfe der Zuordnungsfunktionen Quelldaten transformieren, um berechnete oder berechnete Werte abzuleiten. Weitere Informationen zu Funktionen für die Datenzuordnung und -zuordnung finden Sie im Lernprogramm zur [Zuordnung von CSV-Daten zu XDM-Schema-Feldern](../../../../ingestion/tutorials/map-a-csv-file.md).

Nachdem Sie die Quelldaten zugeordnet haben, klicken Sie auf **[!UICONTROL Weiter]**.

![](../../../images/tutorials/dataflow/databases/mapping.png)

## Planen von Erfassungsabläufen

Der Schritt *[!UICONTROL Planung]* wird angezeigt, mit dem Sie einen Erfassungszeitplan konfigurieren können, um die ausgewählten Quelldaten automatisch mit den konfigurierten Zuordnungen zu erfassen. In der folgenden Tabelle sind die verschiedenen konfigurierbaren Felder für die Planung aufgeführt:

| Feld | Beschreibung |
| --- | --- |
| Häufigkeit | Zu den auswählbaren Frequenzen gehören Minute, Stunde, Tag und Woche. |
| Intervall | Eine Ganzzahl, die das Intervall für die ausgewählte Frequenz festlegt. |
| Beginn | Ein UTC-Zeitstempel, bei dem die erste Erfassung erfolgt. |
| Aufstockung | Ein boolescher Wert, der bestimmt, welche Daten ursprünglich erfasst werden. Wenn die *Aufstockung* aktiviert ist, werden alle aktuellen Dateien im angegebenen Pfad während der ersten geplanten Erfassung erfasst. Wenn die *Aufstockung* deaktiviert ist, werden nur die Dateien aufgenommen, die zwischen der ersten Ausführung der Erfassung und der *Beginn* geladen wurden. Dateien, die vor dem *Beginn* geladen wurden, werden nicht erfasst. |
| Delta-Spalte | Eine Option mit gefilterten Quelldatumsfeldern vom Typ, Schema oder Uhrzeit. Dieses Feld wird verwendet, um zwischen neuen und vorhandenen Daten zu unterscheiden. Inkrementelle Daten werden basierend auf dem Zeitstempel der ausgewählten Spalte erfasst. |

Datenflüsse sind so konzipiert, dass Daten auf planmäßiger Basis automatisch erfasst werden. Wenn Sie nur einmal über diesen Arbeitsablauf erfassen möchten, können Sie dies tun, indem Sie die **[!UICONTROL Häufigkeit]** auf &quot;Tag&quot;konfigurieren und eine sehr große Zahl für das **[!UICONTROL Intervall]**, z. B. 10000 oder Ähnliches, anwenden.

Geben Sie Werte für den Zeitplan ein und wählen Sie **[!UICONTROL Weiter]**.

![](../../../images/tutorials/dataflow/databases/schedule.png)

## Benennen des Datenflusses

Der Schritt *[!UICONTROL für die Datenflug-Details]* wird angezeigt, in dem Sie einen Namen und eine optionale Beschreibung für den Datenflug angeben müssen. Wählen Sie **[!UICONTROL Weiter]** , wenn Sie fertig sind.

![](../../../images/tutorials/dataflow/databases/dataflow-detail.png)

## Überprüfen Sie Ihren Datenfluss

Der *[!UICONTROL Schritt zum Überprüfen]* wird angezeigt, mit dem Sie Ihren neuen Datenpfad überprüfen können, bevor er erstellt wird. Details werden in den folgenden Kategorien gruppiert:

- *Verbindung*: Zeigt den Quelltyp, den relevanten Pfad der ausgewählten Quelldatei und die Anzahl der Spalten in dieser Quelldatei an.
- *Zuweisen von Dataset- und Zuordnungsfeldern*: Zeigt, in welchen Datensatz die Quelldaten aufgenommen werden, einschließlich des Schemas, das der Datensatz einhält.
- *Planung*: Zeigt den aktiven Zeitraum, die Häufigkeit und das Intervall des Aufnahmeplans an.

Klicken Sie nach Überprüfung des Datenflusses auf **[!UICONTROL Fertig stellen]** und lassen Sie die Erstellung des Datenflusses etwas Zeit.

![](../../../images/tutorials/dataflow/databases/review.png)

## Überwachen des Datenflusses

Nachdem der Datenfluss erstellt wurde, können Sie die Daten überwachen, die über ihn aufgenommen werden. Weitere Informationen zur Überwachung der Datenflüsse finden Sie im Lernprogramm zu [Konten und Datenflüssen](../monitor.md).

## Nächste Schritte

In diesem Lernprogramm haben Sie erfolgreich einen Datenbogen erstellt, um Daten aus einer externen Datenbank einzubringen und Einblicke in die Überwachung von Datensätzen zu erhalten. Eingehende Daten können jetzt von Diensten der nachgelagerten Platform wie dem Echtzeit-Profil von Kunden und dem Data Science Workspace verwendet werden. Weitere Informationen finden Sie in den folgenden Dokumenten:

- [Übersicht über das Echtzeit-Kundenprofil](../../../../profile/home.md)
- [Übersicht über den Data Science Workspace](../../../../data-science-workspace/home.md)

## Anhang

Die folgenden Abschnitte enthalten zusätzliche Informationen zum Arbeiten mit Quellschnittstellen.

### Datentaflow deaktivieren

Beim Erstellen eines Datenflusses wird dieser sofort aktiv und erfasst Daten gemäß dem festgelegten Zeitplan. Sie können einen aktiven Datenfeed jederzeit deaktivieren, indem Sie die unten stehenden Anweisungen befolgen.

Wählen Sie im Arbeitsbereich &quot; *[!UICONTROL Quellen]* &quot;die Registerkarte &quot; **[!UICONTROL Datenflüsse]** &quot;aus. Wählen Sie als Nächstes den Datenflug aus, den Sie deaktivieren möchten.

![](../../../images/tutorials/dataflow/databases/list-of-dataflows.png)

Die Spalte &quot; *[!UICONTROL Eigenschaften]* &quot;wird auf der rechten Seite des Bildschirms angezeigt, einschließlich der Schaltfläche &quot; **[!UICONTROL Aktiviert]** &quot;. Wählen Sie den Umschalter aus, um den Datenflug zu deaktivieren. Derselbe Umschalter kann verwendet werden, um einen Datenflug nach dessen Deaktivierung erneut zu aktivieren.

![](../../../images/tutorials/dataflow/databases/disable.png)

### Aktivieren von Eingangsdaten für die [!DNL Profile] Bevölkerung

Eingehende Daten aus Ihrem Quellanschluss können zur Anreicherung und zum Ausfüllen Ihrer [!DNL Real-time Customer Profile] Daten verwendet werden. Weitere Informationen zum Ausfüllen Ihrer [!DNL Real-time Customer Profile] Daten finden Sie im Tutorial zur [Profil-Population](../profile.md).