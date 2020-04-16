---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Konfigurieren eines Datenflusses für einen Cloud-Datenspeicherung-Connector in der Benutzeroberfläche
topic: overview
translation-type: tm+mt
source-git-commit: 298afbd97096fc01c7fcc05fa794b8e356c6835e

---


# Konfigurieren eines Datenflusses für einen Cloud-Datenspeicherung-Connector in der Benutzeroberfläche

Ein Datennachweis ist eine geplante Aufgabe, mit der Daten aus einer Quelle abgerufen und in einen Platform-Datensatz aufgenommen werden. In diesem Lernprogramm werden die Schritte zum Konfigurieren eines neuen Datenflusses mit Ihrem Cloud-Datenspeicherung-Basisanschluss beschrieben.

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

* [Erlebnis-Datenmodell (XDM)-System](../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Zusammensetzung](../../../../xdm/schema/composition.md)des Schemas: Erfahren Sie mehr über die grundlegenden Bausteine von XDM-Schemas, einschließlich der wichtigsten Grundsätze und Best Practices bei der Schema-Komposition.
   * [Schema-Editor-Lernprogramm](../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
* [Echtzeit-Profil](../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

Darüber hinaus müssen Sie bei diesem Lernprogramm bereits einen Cloud-Datenspeicherung-Connector erstellt haben. Eine Liste von Übungen zum Erstellen verschiedener Cloud-Datenspeicherung-Connectors in der Benutzeroberfläche finden Sie in der Übersicht über die [Quellschnittstellen](../../../home.md).

### Unterstützte Dateiformate

Experience Platform unterstützt die folgenden Dateiformate, die aus externen Datenspeicherung erfasst werden:

* Trennzeichen-getrennte Werte (DSV): Die Unterstützung für DSV-formatierte Datendateien ist derzeit auf kommagetrennte Werte beschränkt. Der Wert von Feldkopfzeilen in DSV-formatierten Dateien darf nur aus alphanumerischen Zeichen und Unterstrichen bestehen. Die Unterstützung für allgemeine DSV-Dateien wird in Zukunft bereitgestellt.
* JavaScript Object Notation (JSON): JSON-formatierte Datendateien müssen XDM-konform sein.
* Apache Parquet: Parquet-formatierte Datendateien müssen XDM-konform sein.

## Daten auswählen

Nachdem Sie den Cloud-Datenspeicherung-Connector erstellt haben, wird der Schritt Daten ** auswählen angezeigt und bietet eine interaktive Oberfläche, über die Sie die Cloud-Datenspeicherung-Hierarchie untersuchen können.

* Die linke Hälfte der Oberfläche ist ein Ordnerbrowser, der die Dateien und Ordner Ihres Servers anzeigt.
* In der rechten Hälfte der Oberfläche können Sie bis zu 100 Datenzeilen aus einer kompatiblen Datei Vorschau werden.

Durch Klicken auf einen aufgelisteten Ordner können Sie die Ordnerhierarchie in tiefere Ordner durchlaufen. Wenn Sie eine kompatible Datei oder einen kompatiblen Ordner ausgewählt haben, wird das Dropdownmenü Datenformat **auswählen** angezeigt, in dem Sie ein Format auswählen können, in dem die Daten im Fenster Vorschau angezeigt werden.

![](../../../images/tutorials/dataflow/cloud-storage/select-data.png)

Wenn das Fenster &quot;Vorschau&quot;ausgefüllt ist, können Sie auf **Weiter** klicken, um alle Dateien im ausgewählten Ordner hochzuladen. Wenn Sie eine Datei in eine bestimmte Datei hochladen möchten, wählen Sie diese Datei in der Liste aus, bevor Sie auf **Weiter** klicken.

>[!NOTE] Zu den unterstützten Dateiformaten gehören CSV, JSON und Parquet. JSON- und Parquet-Dateien müssen XDM-kompatibel sein.

![](../../../images/tutorials/dataflow/cloud-storage/select-data-next.png)

## Zuordnen von Datenfeldern zu einem XDM-Schema

Der Schritt *Zuordnung* wird angezeigt und bietet eine interaktive Schnittstelle, um die Quelldaten einem Plattformdatensatz zuzuordnen. Quelldateien, die in JSON oder Parquet formatiert sind, müssen XDM-konform sein und müssen nicht manuell konfiguriert werden. Bei CSV-Dateien müssen Sie die Zuordnung explizit konfigurieren. Sie können jedoch festlegen, welche Quelldatenfelder zugeordnet werden sollen.

Wählen Sie einen Datensatz, in den eingehende Daten aufgenommen werden sollen. Sie können entweder einen vorhandenen Datensatz verwenden oder einen neuen erstellen.

**Vorhandenen Datensatz verwenden**

Um Daten in einen vorhandenen Datensatz zu erfassen, wählen Sie &quot;Vorhandenen Datensatz **verwenden**&quot;und klicken Sie dann auf das Dataset-Symbol.

![](../../../images/tutorials/dataflow/cloud-storage/use-existing-data.png)

Das Dialogfeld &quot;Datensatz _auswählen_ &quot;wird angezeigt. Suchen Sie den gewünschten Datensatz, wählen Sie ihn aus und klicken Sie dann auf **Weiter**.

![](../../../images/tutorials/dataflow/cloud-storage/select-existing-data.png)

**Verwenden eines neuen Datensatzes**

Um Daten in einen neuen Datensatz zu erfassen, wählen Sie &quot;Neuen Datensatz **erstellen** &quot;und geben Sie einen Namen und eine Beschreibung für den Datensatz in die entsprechenden Felder ein. Klicken Sie anschließend auf das Symbol Schema.

![](../../../images/tutorials/dataflow/cloud-storage/use-new-schema.png)

Das Dialogfeld &quot;Schema _auswählen_ &quot;wird angezeigt. Wählen Sie das Schema aus, das Sie auf den neuen Datensatz anwenden möchten, und klicken Sie dann auf **Fertig**.

![](../../../images/tutorials/dataflow/cloud-storage/select-schema.png)

Je nach Bedarf können Sie Felder direkt zuordnen oder mithilfe der Zuordnungsfunktionen Quelldaten transformieren, um berechnete oder berechnete Werte abzuleiten. Weitere Informationen zu Funktionen für die Datenzuordnung und -zuordnung finden Sie im Lernprogramm zur [Zuordnung von CSV-Daten zu XDM-Schema-Feldern](../../../../ingestion/tutorials/map-a-csv-file.md).

Nachdem Sie die Quelldaten zugeordnet haben, klicken Sie auf **Weiter**.

![](../../../images/tutorials/dataflow/cloud-storage/mapping.png)

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

![](../../../images/tutorials/dataflow/cloud-storage/scheduling.png)

## Benennen des Datenflusses

Der *Namensfluss* -Schritt wird angezeigt, mit dem Sie einen Namen eingeben und eine kurze Beschreibung zu Ihrem neuen Datenpfad geben können.

Geben Sie Werte für den Datenfluss ein und klicken Sie auf **Weiter**.

![](../../../images/tutorials/dataflow/cloud-storage/name-your-dataflow.png)

### Überprüfen Sie Ihren Datenfluss

Der *Schritt zum Überprüfen* wird angezeigt, mit dem Sie Ihren neuen Datenpfad überprüfen können, bevor er erstellt wird. Details werden in den folgenden Kategorien gruppiert:

* *Quelldetails*: Zeigt den Quelltyp, den relevanten Pfad der ausgewählten Quelldatei und die Anzahl der Spalten in dieser Quelldatei an.
* *Angaben* zur Zielgruppe: Zeigt, in welchen Datensatz die Quelldaten aufgenommen werden, einschließlich des Schemas, das der Datensatz einhält.
* *Details* planen: Zeigt den aktiven Zeitraum, die Häufigkeit und das Intervall des Aufnahmeplans an.

Klicken Sie nach Überprüfung des Datenflusses auf **Fertig stellen** und lassen Sie die Erstellung des Datenflusses etwas Zeit.

![](../../../images/tutorials/dataflow/cloud-storage/review.png)

## Überwachen des Datenflusses

Nachdem Sie den DataFlow für die Cloud-Datenspeicherung erstellt haben, können Sie die Daten überwachen, die über den Datenfluss aufgenommen werden. Gehen Sie wie folgt vor, um auf den DataSet-Monitor eines Datenflusses zuzugreifen.

Klicken Sie im Arbeitsbereich &quot; *Quellen* &quot;auf die Registerkarte &quot; **Durchsuchen** &quot;, um Ihre Basisverbindungen Liste. Suchen Sie in der angezeigten Liste nach der Verbindung, die den zu überwachenden Datendurchlauf enthält, indem Sie auf dessen Namen klicken.

![](../../../images/tutorials/dataflow/cloud-storage/browse.png)

Der Bildschirm &quot; *Quell-Aktivität* &quot;wird angezeigt. Klicken Sie von hier auf den Namen des Datensatzes, dessen Aktivität Sie überwachen möchten.

![](../../../images/tutorials/dataflow/cloud-storage/source-activity.png)

Der Bildschirm &quot; *Aktivität* des Datensatzes&quot;wird angezeigt. Diese Seite zeigt die Rate der Nachrichten an, die in Form eines Diagramms konsumiert werden.

![](../../../images/tutorials/dataflow/cloud-storage/dataset-activity.png)

Unter dem Diagramm befindet sich eine Liste von Stapeln, die in den Datensatz aufgenommen wurden und deren Status (erfolgreich oder fehlgeschlagen) sowie die Anzahl der erfassten Datensätze anzeigen. Wenn ein Stapel in einen Profil-aktivierten Datensatz aufgenommen wird, wird die Anzahl der erfassten Profil und Identitäten angezeigt.

Sie können weitere Details zu einem aufgelisteten Stapel durch Klicken auf seine ID Ansicht haben.

Weitere Informationen zur Überwachung von Datensätzen und zur Erfassung finden Sie im Lernprogramm zur [Überwachung von Streaming-Datenflüssen](../../../../ingestion/quality/monitor-data-flows.md).

## Nächste Schritte

In diesem Lernprogramm haben Sie erfolgreich einen Datenbogen erstellt, um Daten aus einer externen Cloud-Datenspeicherung einzubringen, und Einblicke in die Überwachung von Datensätzen erhalten. Eingehende Daten können jetzt von nachgeschalteten Plattformdiensten wie Real-time Customer Profil und Data Science Workspace verwendet werden. Weitere Informationen finden Sie in den folgenden Dokumenten:

* [Übersicht über das Echtzeit-Kundenprofil](../../../../profile/home.md)
* [Übersicht über den Data Science Workspace](../../../../data-science-workspace/home.md)

## Anhang

Die folgenden Abschnitte enthalten zusätzliche Informationen zum Arbeiten mit Quellschnittstellen.

### Datentaflow deaktivieren

Beim Erstellen eines Datenflusses wird dieser sofort aktiv und erfasst Daten gemäß dem festgelegten Zeitplan. Sie können einen aktiven Datenfeed jederzeit deaktivieren, indem Sie die unten stehenden Anweisungen befolgen.

Klicken Sie im Arbeitsbereich &quot; *Quellen* &quot;auf die Registerkarte &quot; **Durchsuchen** &quot;. Klicken Sie anschließend auf den Namen der Basisverbindung, die mit dem aktiven Datenpfad verknüpft ist, den Sie deaktivieren möchten.

![](../../../images/tutorials/dataflow/cloud-storage/browse.png)

Die Seite &quot; *Quellseite* &quot;wird angezeigt. Wählen Sie den aktiven Datenfluss aus der Liste aus, um die Spalte &quot; *Eigenschaften* &quot;auf der rechten Seite des Bildschirms mit der Schaltfläche &quot; **Aktiviert** &quot;zu öffnen. Klicken Sie auf den Umschalter, um den Datenflug zu deaktivieren. Derselbe Umschalter kann verwendet werden, um einen Datenflug nach dessen Deaktivierung erneut zu aktivieren.

![](../../../images/tutorials/dataflow/cloud-storage/disable-source.png)

### Aktivieren von Eingangsdaten für die Profil-Population

Eingehende Daten aus Ihrem Quell-Connector können zur Bereicherung und zum Ausfüllen Ihrer Echtzeit-Kundendaten verwendet werden. Weitere Informationen zum Ausfüllen von Daten zum Real-Customer-Profil finden Sie im Lernprogramm zur [Profil-Population](../profile.md).
