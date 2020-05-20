---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Konfigurieren eines Datenflusses für einen Protokollanschluss in der Benutzeroberfläche
topic: overview
translation-type: tm+mt
source-git-commit: 8a331e6711fab6f1823ff2ad030e5077e24d22d3
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 1%

---


# Konfigurieren eines Datenflusses für einen Protokollanschluss in der Benutzeroberfläche

Ein Datenfluss ist eine geplante Aufgabe, mit der Daten aus einer Quelle abgerufen und in einen Adobe Experience Platform-Datensatz aufgenommen werden. Dieses Lernprogramm enthält Schritte zum Konfigurieren eines neuen Datensatzflusses mit Ihrem Protokollkonto.

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

- [Erlebnis-Datenmodell (XDM)-System](../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   - [Grundlagen der Zusammensetzung](../../../../xdm/schema/composition.md)des Schemas: Erfahren Sie mehr über die grundlegenden Bausteine von XDM-Schemas, einschließlich der wichtigsten Grundsätze und Best Practices bei der Schema-Komposition.
   - [Schema-Editor-Lernprogramm](../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
- [Echtzeit-Profil](../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

Darüber hinaus erfordert dieses Lernprogramm, dass Sie bereits ein Protokollkonto erstellt haben. Eine Liste von Übungen zum Erstellen verschiedener Protokollschnittstellen in der Benutzeroberfläche finden Sie in der Übersicht über die [Quellschnittstellen](../../../home.md).

## Daten auswählen

Nachdem Sie Ihr Protokollkonto erstellt haben, wird der Schritt Daten ** auswählen angezeigt und bietet eine interaktive Oberfläche, über die Sie Ihre Dateihierarchie untersuchen können.

- Die linke Hälfte der Oberfläche ist ein Ordnerbrowser, der die Dateien und Ordner Ihres Servers anzeigt.
- In der rechten Hälfte der Oberfläche können Sie bis zu 100 Datenzeilen aus einer kompatiblen Datei Vorschau werden.

Wählen Sie den Ordner aus, den Sie verwenden möchten, und klicken Sie dann auf **Weiter**.

![add-data](../../../images/tutorials/dataflow/protocols/add-data.png)

## Zuordnen von Datenfeldern zu einem XDM-Schema

Der Schritt *Zuordnung* wird angezeigt und bietet eine interaktive Schnittstelle, um die Quelldaten einem Plattformdatensatz zuzuordnen.

Wählen Sie einen Datensatz, in den eingehende Daten aufgenommen werden sollen. Sie können entweder einen vorhandenen Datensatz verwenden oder einen neuen Datensatz erstellen.

### Vorhandenen Datensatz verwenden

Um Daten in einen vorhandenen Datensatz zu erfassen, wählen Sie &quot;Vorhandenen Datensatz **verwenden**&quot;und klicken Sie dann auf das Dataset-Symbol.

![use-existing-dataset](../../../images/tutorials/dataflow/protocols/use-existing-dataset.png)

Das Dialogfeld &quot;Datensatz *auswählen* &quot;wird angezeigt. Suchen Sie den gewünschten Datensatz, wählen Sie ihn aus und klicken Sie dann auf **Weiter**.

![select-existing-dataset](../../../images/tutorials/dataflow/protocols/select-existing-dataset.png)

### Verwenden eines neuen Datensatzes

Um Daten in einen neuen Datensatz zu erfassen, wählen Sie &quot;Neuen Datensatz **erstellen** &quot;und geben Sie einen Namen und eine Beschreibung für den Datensatz in die entsprechenden Felder ein.

Während dieses Prozesses können Sie auch die *teilweise Erfassung* und *Fehlerdiagnose* aktivieren. Durch Aktivierung der *partiellen Erfassung* können Daten mit Fehlern bis zu einem bestimmten Schwellenwert erfasst werden, den Sie festlegen können. Wenn Sie die Fehlerdiagnose aktivieren, erhalten Sie Details zu allen falschen Daten, die separat in Batches aufgenommen werden. Weitere Informationen finden Sie in der Übersicht über die [teilweise Stapelverarbeitung](../../../../ingestion/batch-ingestion/partial.md).

Klicken Sie abschließend auf das Symbol Schema.

![create-new-dataset](../../../images/tutorials/dataflow/protocols/use-new-dataset.png)

Das Dialogfeld &quot;Schema *auswählen* &quot;wird angezeigt. Wählen Sie das Schema aus, das Sie auf den neuen Datensatz anwenden möchten, und klicken Sie dann auf **Fertig**.

![select-Schema](../../../images/tutorials/dataflow/protocols/select-existing-schema.png)

Je nach Bedarf können Sie Felder direkt zuordnen oder mithilfe der Zuordnungsfunktionen Quelldaten transformieren, um berechnete oder berechnete Werte abzuleiten. Weitere Informationen zu Funktionen für die Datenzuordnung und -zuordnung finden Sie im Lernprogramm zur [Zuordnung von CSV-Daten zu XDM-Schema-Feldern](../../../../ingestion/tutorials/map-a-csv-file.md).

Im *Anzeigebereich &quot;Zuordnung* &quot;können Sie auch eine *Delta-Spalte* festlegen. Wenn der Datenfluss erstellt wird, können Sie jedes beliebige Zeitstempelfeld als Grundlage für die Entscheidung festlegen, welche Datensätze in geplanten inkrementellen Aufrufen erfasst werden sollen.

Nachdem Sie die Quelldaten zugeordnet haben, klicken Sie auf **Weiter**.

![](../../../images/tutorials/dataflow/protocols/mapping.png)

Der Schritt *Planung* wird angezeigt, mit dem Sie einen Erfassungszeitplan konfigurieren können, um die ausgewählten Quelldaten automatisch mit den konfigurierten Zuordnungen zu erfassen. In der folgenden Tabelle sind die verschiedenen konfigurierbaren Felder für die Planung aufgeführt:

| Feld | Beschreibung |
| --- | --- |
| Häufigkeit | Zu den auswählbaren Frequenzen gehören Minute, Stunde, Tag und Woche. |
| Intervall | Eine Ganzzahl, die das Intervall für die ausgewählte Frequenz festlegt. |
| Beginn | Ein UTC-Zeitstempel, bei dem die erste Erfassung erfolgt. |
| Aufstockung | Ein boolescher Wert, der bestimmt, welche Daten ursprünglich erfasst werden. Wenn die *Aufstockung* aktiviert ist, werden alle aktuellen Dateien im angegebenen Pfad während der ersten geplanten Erfassung erfasst. Wenn die *Aufstockung* deaktiviert ist, werden nur die Dateien aufgenommen, die zwischen der ersten Ausführung der Erfassung und der *Beginn* geladen wurden. Dateien, die vor dem *Beginn* geladen wurden, werden nicht erfasst. |

Dataset-Datenflüsse sind so konzipiert, dass Daten auf planmäßiger Basis automatisch erfasst werden. Wenn Sie nur einmal über diesen Arbeitsablauf erfassen möchten, können Sie dies tun, indem Sie die **Häufigkeit** auf &quot;Tag&quot;konfigurieren und eine sehr große Zahl für das **Intervall**, z. B. 10000 oder Ähnliches, anwenden.

Geben Sie Werte für den Zeitplan ein und klicken Sie auf **Weiter**.

![scheduling](../../../images/tutorials/dataflow/protocols/scheduling.png)

## Benennen des Datenflusses

Der Schritt *Datenfluss* im Detail wird angezeigt, in dem Sie einen Namen und eine optionale Beschreibung für den Datenfluss angeben müssen. Klicken Sie auf **Weiter**, wenn Sie fertig sind.

![dataset-flow-details](../../../images/tutorials/dataflow/protocols/dataset-flow-details.png)

## Überprüfen des Datenflusses

Der *Schritt zum Überprüfen* wird angezeigt, mit dem Sie Ihren neuen Datenpfad überprüfen können, bevor er erstellt wird. Details werden in den folgenden Kategorien gruppiert:

- *Verbindung*: Zeigt den Quelltyp, den relevanten Pfad der ausgewählten Quelldatei und die Anzahl der Spalten in dieser Quelldatei an.
- *Zuweisen von Dataset- und Zuordnungsfeldern*: Zeigt, in welchen Datensatz die Quelldaten aufgenommen werden, einschließlich des Schemas, das der Datensatz einhält.
- *Planung*: Zeigt den aktiven Zeitraum, die Häufigkeit und das Intervall des Aufnahmeplans an.

Klicken Sie nach Überprüfung des Datenflusses auf **Fertig stellen** und lassen Sie die Erstellung des Datenflusses etwas Zeit.

![überprüfen](../../../images/tutorials/dataflow/protocols/review.png)

## Überwachen des Datenflusses

Nachdem Sie den Datenfluss erstellt haben, können Sie die Daten überwachen, die über den Dataset aufgenommen werden. Weitere Informationen zur Überwachung der Datenflüsse finden Sie im Lernprogramm zu [Konten und Datenflüssen](../monitor.md).

## Nächste Schritte

In diesem Lernprogramm haben Sie erfolgreich einen Dataset-Fluss erstellt, um Daten aus einem Marketingautomatisierungssystem einzubringen und Einblicke in die Überwachung von Datensätzen zu erhalten. Eingehende Daten können jetzt von nachgeschalteten Plattformdiensten wie Real-time Customer Profil und Data Science Workspace verwendet werden. Weitere Informationen finden Sie in den folgenden Dokumenten:

- [Übersicht über das Echtzeit-Kundenprofil](../../../../profile/home.md)
- [Übersicht über den Data Science Workspace](../../../../data-science-workspace/home.md)

## Anhang

Die folgenden Abschnitte enthalten zusätzliche Informationen zum Arbeiten mit Quellschnittstellen.

### Datenfluss deaktivieren

Wenn ein Datenfluss erstellt wird, wird er sofort aktiv und erfasst Daten gemäß dem Zeitplan, den er erhalten hat. Sie können einen aktiven Datenfluss jederzeit deaktivieren, indem Sie die unten stehenden Anweisungen befolgen.

Wählen Sie im Bildschirm &quot; *Datenfluss* &quot;den Namen des Datensatzflusses aus, den Sie deaktivieren möchten.

![browse-dataset-flow](../../../images/tutorials/dataflow/protocols/view-dataset-flows.png)

Die Spalte &quot; *Eigenschaften* &quot;wird auf der rechten Seite des Bildschirms angezeigt. Dieses Bedienfeld enthält eine **Aktivierungsschaltfläche** . Klicken Sie auf den Umschalter, um den Datenflug zu deaktivieren. Derselbe Umschalter kann verwendet werden, um einen Datenflug nach dessen Deaktivierung erneut zu aktivieren.

![disable](../../../images/tutorials/dataflow/protocols/disable.png)

### Aktivieren von Eingangsdaten für die Profil-Population

Eingehende Daten aus Ihrem Quell-Connector können zur Bereicherung und zum Ausfüllen Ihrer Echtzeit-Kundendaten verwendet werden. Weitere Informationen zum Ausfüllen von Daten zum Real-Customer-Profil finden Sie im Lernprogramm zur [Profil-Population](../profile.md).