---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Konfigurieren eines Datenflusses für einen Datenbankanschluss in der Benutzeroberfläche
topic: overview
translation-type: tm+mt
source-git-commit: c55e48a90d57e538f3d096b31eae639a1cca882c

---


# Konfigurieren eines Datenflusses für einen Datenbankanschluss in der Benutzeroberfläche

Ein Datennachweis ist eine geplante Aufgabe, mit der Daten aus einer Quelle abgerufen und in einen Platform-Datensatz aufgenommen werden. In diesem Lernprogramm werden Schritte zum Konfigurieren eines neuen Datenflusses mit Ihrem Datenbankanschluss beschrieben.

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

Wählen Sie die gewünschte Datenbank aus und klicken Sie auf **Weiter**.

![](../../../images/tutorials/dataflow/databases/select-data-next.png)

## Zuordnen von Datenfeldern zu einem XDM-Schema

Der Schritt *Zuordnung* wird angezeigt und bietet eine interaktive Schnittstelle, um die Quelldaten einem Plattformdatensatz zuzuordnen.

Wählen Sie einen Datensatz, in den eingehende Daten aufgenommen werden sollen. Sie können entweder einen vorhandenen Datensatz verwenden oder einen neuen Datensatz erstellen.

### Vorhandenen Datensatz verwenden

Um Daten in einen vorhandenen Datensatz zu erfassen, wählen Sie &quot;Vorhandenen Datensatz **verwenden**&quot;und klicken Sie dann auf das Dataset-Symbol.

![](../../../images/tutorials/dataflow/databases/use-existing-dataset.png)

Das Dialogfeld &quot;Datensatz _auswählen_ &quot;wird angezeigt. Suchen Sie den gewünschten Datensatz, wählen Sie ihn aus und klicken Sie dann auf **Weiter**.

![](../../../images/tutorials/dataflow/databases/select-dataset.png)

### Verwenden eines neuen Datensatzes

Um Daten in einen neuen Datensatz zu erfassen, wählen Sie &quot;Neuen Datensatz **erstellen** &quot;und geben Sie einen Namen und eine Beschreibung für den Datensatz in die entsprechenden Felder ein. Klicken Sie anschließend auf das Symbol Schema.

![](../../../images/tutorials/dataflow/databases/use-new-dataset.png)

Das Dialogfeld &quot;Schema _auswählen_ &quot;wird angezeigt. Wählen Sie das Schema aus, das Sie auf den neuen Datensatz anwenden möchten, und klicken Sie dann auf **Fertig**.

![](../../../images/tutorials/dataflow/databases/select-schema.png)

Je nach Bedarf können Sie Felder direkt zuordnen oder mithilfe der Zuordnungsfunktionen Quelldaten transformieren, um berechnete oder berechnete Werte abzuleiten. Weitere Informationen zu Funktionen für die Datenzuordnung und -zuordnung finden Sie im Lernprogramm zur [Zuordnung von CSV-Daten zu XDM-Schema-Feldern](../../../../ingestion/tutorials/map-a-csv-file.md).

Nachdem Sie die Quelldaten zugeordnet haben, klicken Sie auf **Weiter**.

![](../../../images/tutorials/dataflow/databases/mapping-data.png)

## Planen von Erfassungsabläufen

Der Schritt *Planung* wird angezeigt, mit dem Sie einen Erfassungszeitplan konfigurieren können, um die ausgewählten Quelldaten automatisch mit den konfigurierten Zuordnungen zu erfassen. In der folgenden Tabelle sind die verschiedenen konfigurierbaren Felder für die Planung aufgeführt:

| Feld | Beschreibung |
| --- | --- |
| Häufigkeit | Zu den auswählbaren Frequenzen gehören Minute, Stunde, Tag und Woche. |
| Intervall | Eine Ganzzahl, die das Intervall für die ausgewählte Frequenz festlegt. |
| Beginn | Ein UTC-Zeitstempel, bei dem die erste Erfassung erfolgt. |
| Aufstockung | Ein boolescher Wert, der bestimmt, welche Daten ursprünglich erfasst werden. Wenn die *Aufstockung* aktiviert ist, werden alle aktuellen Dateien im angegebenen Pfad während der ersten geplanten Erfassung erfasst. Wenn die *Aufstockung* deaktiviert ist, werden nur die Dateien aufgenommen, die zwischen der ersten Ausführung der Erfassung und der *Beginn* geladen wurden. Dateien, die vor dem *Beginn* geladen wurden, werden nicht erfasst. |

Datenflüsse sind so konzipiert, dass Daten auf planmäßiger Basis automatisch erfasst werden. Wenn Sie nur einmal über diesen Arbeitsablauf erfassen möchten, können Sie dies tun, indem Sie die **Häufigkeit** auf &quot;Tag&quot;konfigurieren und eine sehr große Zahl für das **Intervall**, z. B. 10000 oder Ähnliches, anwenden.

Geben Sie Werte für den Zeitplan ein und klicken Sie auf **Weiter**.

![](../../../images/tutorials/dataflow/databases/scheduling.png)

## Benennen des Datenflusses

Der Schritt zum *Namensfluss* wird angezeigt, in dem Sie einen Namen und eine optionale Beschreibung für den Datenflug angeben müssen. Klicken Sie auf Weiter, wenn Sie fertig sind.&quot;

![](../../../images/tutorials/dataflow/databases/name-flow.png)

## Überprüfen Sie Ihren Datenfluss

Der *Schritt zum Überprüfen* wird angezeigt, mit dem Sie Ihren neuen Datenpfad überprüfen können, bevor er erstellt wird. Details werden in den folgenden Kategorien gruppiert:

- *Verbindungsdetails*: Zeigt den Quelltyp, den relevanten Pfad der ausgewählten Quelldatei und die Anzahl der Spalten in dieser Quelldatei an.
- *Zuordnungsdetails*: Zeigt, in welchen Datensatz die Quelldaten aufgenommen werden, einschließlich des Schemas, das der Datensatz einhält.
- *Details* planen: Zeigt den aktiven Zeitraum, die Häufigkeit und das Intervall des Aufnahmeplans an.

Klicken Sie nach Überprüfung des Datenflusses auf **Fertig stellen** und lassen Sie die Erstellung des Datenflusses etwas Zeit.

![](../../../images/tutorials/dataflow/databases/review.png)

## Überwachen des Datenflusses

Nachdem der Datenfluss erstellt wurde, können Sie die Daten überwachen, die über ihn aufgenommen werden. Gehen Sie wie folgt vor, um auf den DataSet-Monitor eines Datenflusses zuzugreifen.

Klicken Sie im Arbeitsbereich &quot; _Quellen_ &quot;auf die Registerkarte &quot; **Durchsuchen** &quot;, um Ihre Basisverbindungen Liste. Suchen Sie in der angezeigten Liste nach der Verbindung, die den zu überwachenden Datendurchlauf enthält, indem Sie auf dessen Namen klicken.

![](../../../images/tutorials/dataflow/databases/browse-base-connectors.png)

Der Bildschirm &quot; *Quell-Aktivität* &quot;wird angezeigt. Klicken Sie von hier auf den Namen des Datensatzes, dessen Aktivität Sie überwachen möchten.

![](../../../images/tutorials/dataflow/databases/select-dataflow-dataset.png)

Der Bildschirm &quot; *Aktivität* des Datensatzes&quot;wird angezeigt. Diese Seite zeigt die Rate der Nachrichten an, die in Form eines Diagramms konsumiert werden.

![](../../../images/tutorials/dataflow/databases/dataset-activity.png)

Weitere Informationen zur Überwachung von Datensätzen und zur Erfassung finden Sie im Lernprogramm zur [Überwachung von Streaming-Datenflüssen](../../../../ingestion/quality/monitor-data-flows.md).

## Nächste Schritte

In diesem Lernprogramm haben Sie erfolgreich einen Datenbogen erstellt, um Daten aus einer externen Datenbank einzubringen und Einblicke in die Überwachung von Datensätzen zu erhalten. Eingehende Daten können jetzt von nachgeschalteten Plattformdiensten wie Real-time Customer Profil und Data Science Workspace verwendet werden. Weitere Informationen finden Sie in den folgenden Dokumenten:

- [Übersicht über das Echtzeit-Kundenprofil](../../../../profile/home.md)
- [Übersicht über den Data Science Workspace](../../../../data-science-workspace/home.md)

## Anhang

Die folgenden Abschnitte enthalten zusätzliche Informationen zum Arbeiten mit Quellschnittstellen.

### Datentaflow deaktivieren

Beim Erstellen eines Datenflusses wird dieser sofort aktiv und erfasst Daten gemäß dem festgelegten Zeitplan. Sie können einen aktiven Datenfeed jederzeit deaktivieren, indem Sie die unten stehenden Anweisungen befolgen.

Klicken Sie im Arbeitsbereich &quot; _Quellen_ &quot;auf die Registerkarte &quot; **Durchsuchen** &quot;. Klicken Sie anschließend auf den Namen der Basisverbindung, die mit dem zu deaktivierenden Datenfeed verknüpft ist.

![](../../../images/tutorials/dataflow/databases/browse-base-connectors.png)

Die Seite &quot; _Quellseite_ &quot;wird angezeigt. Wählen Sie den aktiven Datenfluss aus der Liste aus, um die Spalte &quot; *Eigenschaften* &quot;auf der rechten Seite des Bildschirms mit der Schaltfläche &quot; **Aktiviert** &quot;zu öffnen. Klicken Sie auf den Umschalter, um den Datenflug zu deaktivieren. Derselbe Umschalter kann verwendet werden, um einen Datenflug nach dessen Deaktivierung erneut zu aktivieren.

![](../../../images/tutorials/dataflow/databases/toggle-enabled.png)

### Aktivieren von Eingangsdaten für die Profil-Population

Eingehende Daten aus Ihrem Quell-Connector können zur Bereicherung und zum Ausfüllen Ihrer Echtzeit-Kundendaten verwendet werden. Weitere Informationen zum Ausfüllen von Daten zum Real-Customer-Profil finden Sie im Lernprogramm zur [Profil-Population](../profile.md).