---
keywords: Experience Platform;Startseite;beliebte Themen;Datenflug;Datenflug
solution: Experience Platform
title: Konfigurieren eines Datenflusses für einen Cloud-Datenspeicherung-Batch-Connector in der Benutzeroberfläche
topic: Übersicht
type: Tutorial
description: Ein Datennachweis ist eine geplante Aufgabe, mit der Daten aus einer Quelle abgerufen und in einen Platform-Datensatz aufgenommen werden. In diesem Lernprogramm werden die Schritte zum Konfigurieren eines neuen Datenflusses mit Ihrem Cloud-Datenspeicherung-Konto beschrieben.
translation-type: tm+mt
source-git-commit: 115442a90ab56a93748bf161aa2e7ed680980f6e
workflow-type: tm+mt
source-wordcount: '1874'
ht-degree: 2%

---


# Konfigurieren eines Datenflusses für eine Cloud-Datenspeicherung-Batch-Verbindung in der Benutzeroberfläche

Ein Datennachweis ist eine geplante Aufgabe, mit der Daten aus einer Quelle abgerufen und in einen [!DNL Platform]-Datensatz eingefügt werden. In diesem Lernprogramm werden die Schritte zum Konfigurieren eines neuen Datenflusses mit Ihrem Cloud-Datenspeicherung-Konto beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten  [!DNL Experience Platform] organisiert werden.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   * [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

Darüber hinaus erfordert dieses Lernprogramm, dass Sie über ein Konto für die Cloud-Datenspeicherung verfügen. Eine Liste von Übungen zum Erstellen verschiedener Cloud-Datenspeicherung-Konten in der Benutzeroberfläche finden Sie unter [Übersicht über die Quellschnittstellen](../../../../home.md).

### Unterstützte Dateiformate

[!DNL Experience Platform] unterstützt die folgenden Dateiformate, die von externen Datenspeicherung erfasst werden:

* Trennzeichen-getrennte Werte (DSV): Jeder einzelne Wert kann als Trennzeichen für DSV-formatierte Datendateien verwendet werden.
* [!DNL JavaScript Object Notation] (JSON): JSON-formatierte Datendateien müssen XDM-konform sein.
* [!DNL Apache Parquet]: Parquet-formatierte Datendateien müssen XDM-konform sein.

## Daten auswählen

Nachdem Sie Ihr Cloud-Datenspeicherung-Konto erstellt haben, wird der Schritt **[!UICONTROL Daten auswählen]** angezeigt und bietet eine Oberfläche, über die Sie die Dateihierarchie in Ihrer Cloud-Datenspeicherung untersuchen können.

* Die linke Hälfte der Oberfläche ist ein Ordnerbrowser, der die Dateien und Ordner Ihres Servers anzeigt.
* In der rechten Hälfte der Oberfläche können Sie bis zu 100 Datenzeilen aus einer kompatiblen Datei Vorschau werden.

Wenn Sie einen aufgelisteten Ordner auswählen, können Sie die Ordnerhierarchie in tiefere Ordner durchlaufen. Wenn Sie eine kompatible Datei oder einen kompatiblen Ordner ausgewählt haben, wird das Dropdown-Menü **[!UICONTROL Datenformat auswählen]** angezeigt, in dem Sie ein Format auswählen können, in dem die Daten im Fenster &quot;Vorschau&quot;angezeigt werden sollen.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-data.png)

Wählen Sie das gewünschte Datenformat für die zu erfassende Datei aus und lassen Sie das Ausfüllen des Fensters &quot;Vorschau&quot;einige Sekunden lang zu.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/data-format.png)

Sie können beim Eingeben von getrennten Dateien ein benutzerdefiniertes Trennzeichen festlegen. Wählen Sie die Option **[!UICONTROL Trennzeichen]** und dann ein Trennzeichen aus dem Dropdown-Menü. Im Menü werden die am häufigsten verwendeten Optionen für Trennzeichen angezeigt, darunter ein Komma (`,`), ein Tabulator (`\t`) und ein Rohr (`|`). Alternativ dazu können Sie **[!UICONTROL Benutzerdefiniert]** auswählen und in der Popup-Eingabeleiste ein benutzerdefiniertes Trennzeichen Ihrer Wahl eingeben.

Nachdem Sie das Datenformat ausgewählt und das Trennzeichen festgelegt haben, wählen Sie **[!UICONTROL Weiter]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/delimiter.png)

### Parquet- oder JSON-Dateien aufnehmen

Cloud-Datenspeicherung-Konten unterstützen auch JSON- und Parquet-Dateien. Parquet-Dateien müssen XDM-konform sein, während JSON-Dateien keine XDM-Beschwerde sein müssen. Um JSON- oder Parquet-Dateien zu erfassen, wählen Sie das entsprechende Dateiformat im Ordnerbrowser aus und wenden Sie auf der rechten Benutzeroberfläche das kompatible Datenformat an.

Wenn das Datenformat in JSON vorliegt, wird eine Vorschau mit Informationen zu den Daten in der Datei angezeigt. Im Bildschirm &quot;Vorschau&quot;können Sie mithilfe der Dropdownliste **[!UICONTROL XDM-kompatibel]** auswählen, ob JSON XDM-konform ist.

Wählen Sie **[!UICONTROL Weiter]**, um fortzufahren.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/json-preview.png)

>[!IMPORTANT]
>
>Im Gegensatz zu getrennten und JSON-Dateitypen stehen parquet-formatierte Dateien nicht zur Vorschau zur Verfügung.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-data-parquet.png)

## Zuordnen von Datenfeldern zu einem XDM-Schema

Der Schritt **[!UICONTROL Zuordnung]** wird angezeigt und stellt eine interaktive Schnittstelle bereit, um die Quelldaten einem [!DNL Platform]-Datensatz zuzuordnen. Quelldateien, die in Parquet formatiert wurden, müssen XDM-konform sein und müssen nicht manuell konfiguriert werden, während für CSV-Dateien explizit die Zuordnung konfiguriert werden muss. Sie müssen jedoch festlegen, welche Quelldatenfelder zugeordnet werden sollen. JSON-Dateien, die als XDM-Beschwerde markiert sind, müssen nicht manuell konfiguriert werden. Wenn es jedoch nicht als XDM-kompatibel markiert ist, müssen Sie die Zuordnung explizit konfigurieren.

Wählen Sie einen Datensatz, in den eingehende Daten aufgenommen werden sollen. Sie können entweder einen vorhandenen Datensatz verwenden oder einen neuen erstellen.

**Vorhandenen Datensatz verwenden**

Um Daten in einen vorhandenen Datensatz zu erfassen, wählen Sie **[!UICONTROL Vorhandener Datensatz]** und klicken Sie dann auf das Dataset-Symbol.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/use-existing-data.png)

Das Dialogfeld **[!UICONTROL Datensatz auswählen]** wird angezeigt. Suchen Sie den gewünschten Datensatz, wählen Sie ihn aus und klicken Sie dann auf **[!UICONTROL Weiter]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-existing-dataset.png)

**Verwenden eines neuen Datensatzes**

Um Daten in einen neuen Datensatz zu erfassen, wählen Sie **[!UICONTROL Neuer Datensatz]** aus und geben Sie in die entsprechenden Felder einen Namen und eine Beschreibung für den Datensatz ein. Um ein Schema hinzuzufügen, können Sie im Dialogfeld **[!UICONTROL Schema]** auswählen einen vorhandenen Schema eingeben. Alternativ können Sie die erweiterte Suche **[!UICONTROL Schema]** auswählen, um nach einem geeigneten Schema zu suchen.

In diesem Schritt können Sie Ihren Datensatz für [!DNL Real-time Customer Profile] aktivieren und eine holistische Ansicht der Attribute und Verhaltensweisen einer Entität erstellen. Daten aus allen aktivierten Datensätzen werden in [!DNL Profile] eingeschlossen und beim Speichern des Datenflusses werden Änderungen angewendet.

Schalten Sie die Schaltfläche **[!UICONTROL Profil-Datensatz]** um, um Ihren Zielgruppen-Datensatz für [!DNL Profile] zu aktivieren.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/new-dataset.png)

Das Dialogfeld **[!UICONTROL Schema auswählen]** wird angezeigt. Wählen Sie das Schema, das Sie auf den neuen Datensatz anwenden möchten, und wählen Sie **[!UICONTROL Fertig]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-schema.png)

Je nach Bedarf können Sie Felder direkt zuordnen oder mithilfe der Zuordnungsfunktionen Quelldaten transformieren, um berechnete oder berechnete Werte abzuleiten. Weitere Informationen zu Datenzuordnungs- und -zuordnungsfunktionen finden Sie im Lernprogramm [Zuordnen von CSV-Daten zu XDM-Schema-Feldern](../../../../../ingestion/tutorials/map-a-csv-file.md).

![](../../../../images/tutorials/dataflow/cloud-storage/batch/mapping.png)

Bei JSON-Datenspeicherung können Sie nicht nur Felder direkt anderen Feldern zuordnen, sondern auch Objekten und Arrays anderen Arrays direkt zuordnen. Komplexe Datentypen wie Arrays in JSON-Dateien können auch über einen Cloud-Quellanschluss Vorschau und zugeordnet werden.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/source-field-json.png)

![](../../../../images/tutorials/dataflow/cloud-storage/batch/target-field-json.png)

Bitte beachten Sie, dass Sie keine Karten für verschiedene Typen erstellen können. Sie können beispielsweise ein Objekt einem Array oder einem Feld einem Objekt nicht zuordnen.

>[!TIP]
>
>[!DNL Platform] bietet intelligente Empfehlungen für automatisch zugeordnete Zielgruppen, die auf dem von Ihnen ausgewählten Schema oder Datensatz basieren. Sie können Zuordnungsregeln manuell an Ihre Anwendungsfälle anpassen.

Wählen Sie **[!UICONTROL Vorschau data]** aus, um die Zuordnungsergebnisse von bis zu 100 Zeilen mit Musterdaten aus dem ausgewählten Datensatz anzuzeigen.

Während der Vorschau wird die Identitätsspalte als erstes Feld priorisiert, da sie die wichtigen Informationen darstellt, die bei der Validierung der Zuordnungsergebnisse erforderlich sind.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/mapping-preview.png)

Sobald die Quelldaten zugeordnet sind, wählen Sie **[!UICONTROL Schließen]**.

## Planen von Erfassungsabläufen

Der Schritt **[!UICONTROL Einplanen]** wird angezeigt, mit dem Sie einen Zeitplan für die Erfassung konfigurieren können, um die ausgewählten Quelldaten automatisch mit den konfigurierten Zuordnungen zu erfassen. In der folgenden Tabelle sind die verschiedenen konfigurierbaren Felder für die Planung aufgeführt:

| Feld | Beschreibung |
| --- | --- |
| Häufigkeit | Zu den auswählbaren Frequenzen gehören `Once`, `Minute`, `Hour`, `Day` und `Week`. |
| Intervall | Eine Ganzzahl, die das Intervall für die ausgewählte Frequenz festlegt. |
| Beginn | Ein UTC-Zeitstempel, der angibt, wann die erste Erfassung erfolgen soll. |
| Aufstockung | Ein boolescher Wert, der bestimmt, welche Daten ursprünglich erfasst werden. Ist **[!UICONTROL Aufstockung]** aktiviert, werden alle aktuellen Dateien im angegebenen Pfad während der ersten geplanten Erfassung erfasst. Wenn **[!UICONTROL Aufstockung]** deaktiviert ist, werden nur die Dateien erfasst, die zwischen der ersten Ausführung der Erfassung und der Beginn geladen werden. Dateien, die vor dem Beginn geladen wurden, werden nicht erfasst. |

Datenflüsse sind so konzipiert, dass Daten auf planmäßiger Basis automatisch erfasst werden. Beginn durch Auswahl der Aufnahmefrequenz. Legen Sie als Nächstes das Intervall fest, um den Zeitraum zwischen zwei Flussläufen festzulegen. Der Wert des Intervalls sollte eine Ganzzahl ungleich null sein und auf größer oder gleich 15 gesetzt werden.

Um die Erfassungszeit des Beginns festzulegen, passen Sie das Datum und die Uhrzeit an, die im Feld &quot;Beginn&quot;angezeigt werden. Alternativ können Sie das Kalendersymbol auswählen, um den Zeitwert des Beginns zu bearbeiten. Die Beginn-Zeit muss größer oder gleich der aktuellen Uhrzeit in UTC sein.

Geben Sie Werte für den Zeitplan ein und wählen Sie **[!UICONTROL Weiter]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/scheduling-interval-on.png)

### Einrichten eines einmaligen Erfassungsdataflow

Um eine einmalige Erfassung einzurichten, wählen Sie den Dropdown-Pfeil für die Häufigkeit aus und wählen Sie **[!UICONTROL Once]**. Sie können die Bearbeitung eines Datensatzes für eine einmalige Erfassung der Häufigkeit fortsetzen, solange der Beginn in der Zukunft verbleibt. Nach Ablauf des Beginns kann der Wert für die einmalige Häufigkeit nicht mehr bearbeitet werden. **[!UICONTROL Bei der Einrichtung eines einmaligen Datenflusses sind keine]** Intervaland- **** Backfillments sichtbar.

>[!IMPORTANT]
>
>Es wird dringend empfohlen, den Datendurchlauf für eine einmalige Erfassung zu planen, wenn der [FTP Connector](../../../../connectors/cloud-storage/ftp.md) verwendet wird.

Nachdem Sie die entsprechenden Werte für den Zeitplan angegeben haben, wählen Sie **[!UICONTROL Weiter]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/scheduling-once.png)

## Datenflussinformationen bereitstellen

Der Schritt **[!UICONTROL Datentiefe]** wird angezeigt, mit dem Sie einen Namen eingeben und eine kurze Beschreibung zu Ihrem neuen Datenpfad geben können.

Während dieses Prozesses können Sie auch die Optionen **[!UICONTROL Partielle Erfassung]** und **[!UICONTROL Fehlerdiagnose]** aktivieren. Durch Aktivierung von **[!UICONTROL Partielle Erfassung]** können Sie Daten mit Fehlern bis zu einem bestimmten Schwellenwert erfassen, den Sie festlegen können. Wenn Sie **[!UICONTROL Fehlerdiagnose]** aktivieren, werden Details zu fehlerhaften Daten bereitgestellt, die separat gestapelt werden. Weitere Informationen finden Sie unter [Übersicht über die teilweise Stapelverarbeitung](../../../../../ingestion/batch-ingestion/partial.md).

Geben Sie Werte für den Datenfluss ein und wählen Sie **[!UICONTROL Weiter]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/dataflow-detail.png)

## Überprüfen Sie Ihren Datenfluss

Der Schritt **[!UICONTROL Überprüfen]** wird angezeigt, mit dem Sie Ihren neuen Datenpfad überprüfen können, bevor er erstellt wird. Details werden in den folgenden Kategorien gruppiert:

* **[!UICONTROL Verbindung]**: Zeigt den Quelltyp, den relevanten Pfad der ausgewählten Quelldatei und die Anzahl der Spalten in dieser Quelldatei an.
* **[!UICONTROL Zuweisen von Dataset- und Zuordnungsfeldern]**: Zeigt, in welchen Datensatz die Quelldaten aufgenommen werden, einschließlich des Schemas, das der Datensatz einhält.
* **[!UICONTROL Planung]**: Zeigt den aktiven Zeitraum, die Häufigkeit und das Intervall des Aufnahmeplans an.

Klicken Sie nach Überprüfung Ihres Datenflusses auf **[!UICONTROL Fertig stellen]** und lassen Sie etwas Zeit für die Erstellung des Datenflusses zu.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/review.png)

## Überwachen des Datenflusses

Nachdem Sie Ihren Datenbogen erstellt haben, können Sie die Daten überwachen, die über ihn erfasst werden, um Informationen zu Erfassungsraten, Erfolgen und Fehlern anzuzeigen. Weitere Informationen zur Überwachung des Datenflusses finden Sie im Lernprogramm zu [Überwachungskonten und Datenflüssen in der Benutzeroberfläche](../../monitor.md).

## Datenflug löschen

Sie können Datenflüsse löschen, die nicht mehr benötigt werden oder mit der Funktion **[!UICONTROL Delete]**, die im Arbeitsbereich **[!UICONTROL Datenflüsse]** verfügbar ist, falsch erstellt wurden. Weitere Informationen zum Löschen von Datenflüssen finden Sie im Lernprogramm zum [Löschen von Datenflüssen in der Benutzeroberfläche](../../delete.md).

## Nächste Schritte

In diesem Lernprogramm haben Sie erfolgreich einen Datenbogen erstellt, um Daten aus einer externen Cloud-Datenspeicherung einzubringen, und Einblicke in die Überwachung von Datensätzen erhalten. Um mehr über das Erstellen von Datenflüssen zu erfahren, können Sie Ihr Lernen durch das Video unten ergänzen. Darüber hinaus können eingehende Daten jetzt von nachgeschalteten [!DNL Platform]-Diensten wie [!DNL Real-time Customer Profile] und [!DNL Data Science Workspace] verwendet werden. Weitere Informationen finden Sie in den folgenden Dokumenten:

* [[!DNL Real-time Customer Profile] Übersicht](../../../../../profile/home.md)
* [[!DNL Data Science Workspace] Übersicht](../../../../../data-science-workspace/home.md)

>[!WARNING]
>
> Die im folgenden Video angezeigte [!DNL Platform]-Benutzeroberfläche ist veraltet. Die neuesten Screenshots und Funktionen der Benutzeroberfläche finden Sie in der obigen Dokumentation.

>[!VIDEO](https://video.tv.adobe.com/v/29695?quality=12&learn=on)

## Anhang

Die folgenden Abschnitte enthalten zusätzliche Informationen zum Arbeiten mit Quellschnittstellen.

### Datentaflow deaktivieren

Beim Erstellen eines Datenflusses wird dieser sofort aktiv und erfasst Daten gemäß dem festgelegten Zeitplan. Sie können einen aktiven Datenfeed jederzeit deaktivieren, indem Sie die unten stehenden Anweisungen befolgen.

Klicken Sie im Arbeitsbereich **[!UICONTROL Quellen]** auf die Registerkarte **[!UICONTROL Durchsuchen]**. Klicken Sie anschließend auf den Namen des Kontos, das dem aktiven Datenpfad zugeordnet ist, den Sie deaktivieren möchten.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

Die Aktivität **[!UICONTROL Quelle]** wird angezeigt. Wählen Sie den aktiven Datenfluss aus der Liste aus, um die zugehörige Spalte **[!UICONTROL Properties]** auf der rechten Seite des Bildschirms zu öffnen, die die Umschalter **[!UICONTROL Enabled]** enthält. Klicken Sie auf den Umschalter, um den Datenflug zu deaktivieren. Derselbe Umschalter kann verwendet werden, um einen Datenflug nach dessen Deaktivierung erneut zu aktivieren.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/disable-source.png)

### Aktivieren von Eingangsdaten für [!DNL Profile] Population

Eingehende Daten aus Ihrem Quellanschluss können zur Anreicherung und zum Ausfüllen Ihrer [!DNL Real-time Customer Profile]-Daten verwendet werden. Weitere Informationen zum Ausfüllen der [!DNL Real-time Customer Profile]-Daten finden Sie im Lernprogramm [Profil population](../../profile.md).
