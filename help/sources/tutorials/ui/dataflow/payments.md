---
keywords: Experience Platform;home;popular topics;payment connector
solution: Experience Platform
title: Konfigurieren eines Datenflusses für einen Zahlungsanschluss in der Benutzeroberfläche
topic: overview
description: Ein Datennachweis ist eine geplante Aufgabe, mit der Daten aus einer Quelle abgerufen und in einen Adobe Experience Platform-Datensatz aufgenommen werden. Dieses Lernprogramm enthält Schritte zum Konfigurieren eines neuen Datenflusses mit Ihrem Zahlungskonto.
translation-type: tm+mt
source-git-commit: 785bc95ff3460ebbb1a126ac5fec85ad165ca973
workflow-type: tm+mt
source-wordcount: '1370'
ht-degree: 3%

---


# Konfigurieren eines Datenflusses für einen Zahlungsanschluss in der Benutzeroberfläche

Ein Datennachweis ist eine geplante Aufgabe, mit der Daten aus einer Quelle abgerufen und in einen Adobe Experience Platform-Datensatz aufgenommen werden. Dieses Lernprogramm enthält Schritte zum Konfigurieren eines neuen Datenflusses mit Ihrem Zahlungskonto.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [[!DNL Experience Data Model] (XDM) System](../../../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten [!DNL Experience Platform] organisiert werden.
   - [Grundlagen der Schemakomposition](../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   - [Schema-Editor-Lernprogramm](../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
- [[!DNL Echtzeit-Profil]](../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

Darüber hinaus erfordert dieses Lernprogramm, dass Sie bereits ein Zahlungskonto erstellt haben. Eine Liste von Übungen zum Erstellen verschiedener Zahlungsschnittstellen in der Benutzeroberfläche finden Sie in der Übersicht über die [Quell-Connectors](../../../home.md).

## Daten auswählen

Nach dem Erstellen Ihres Zahlungskontos wird der Schritt Daten **** auswählen angezeigt und bietet eine interaktive Oberfläche, über die Sie Ihre Dateihierarchie untersuchen können.

- Die linke Hälfte der Oberfläche ist ein Ordnerbrowser, der die Dateien und Ordner Ihres Servers anzeigt.
- In der rechten Hälfte der Oberfläche können Sie bis zu 100 Datenzeilen aus einer kompatiblen Datei Vorschau werden.

Mit der Option &quot; **[!UICONTROL Suchen]** &quot;oben auf der Seite können Sie die Quelldaten, die Sie verwenden möchten, schnell identifizieren.

>[!NOTE]
>
>Die Suchquellendaten-Option steht allen tabellarischen Quellschnittstellen mit Ausnahme der Connectors für Analytics, Classifications, Ereignis Hubs und Kinesis zur Verfügung.

Nachdem Sie die Quelldaten gefunden haben, wählen Sie das Verzeichnis aus und klicken Sie auf **[!UICONTROL Weiter]**.

![select-data](../../../images/tutorials/dataflow/all-tabular/select-data.png)

## Zuordnen von Datenfeldern zu einem XDM-Schema

Der Schritt **[!UICONTROL Zuordnung]** wird angezeigt und bietet eine interaktive Schnittstelle, um die Quelldaten einem [!DNL Platform] Datensatz zuzuordnen.

Wählen Sie einen Datensatz, in den eingehende Daten aufgenommen werden sollen. Sie können entweder einen vorhandenen Datensatz verwenden oder einen neuen Datensatz erstellen.

### Vorhandenen Datensatz verwenden

Um Daten in einen vorhandenen Datensatz zu erfassen, wählen Sie &quot;Vorhandenen Datensatz **[!UICONTROL verwenden]**&quot;und klicken Sie dann auf das Dataset-Symbol.

![use-existing-dataset](../../../images/tutorials/dataflow/payments/existing-dataset.png)

The **[!UICONTROL Select dataset]** dialog appears. Suchen Sie den gewünschten Datensatz, wählen Sie ihn aus und klicken Sie dann auf **[!UICONTROL Weiter]**.

![select-existing-dataset](../../../images/tutorials/dataflow/payments/select-dataset.png)

### Verwenden eines neuen Datensatzes

Um Daten in einen neuen Datensatz zu erfassen, wählen Sie &quot;Neuen Datensatz **[!UICONTROL erstellen]** &quot;und geben Sie einen Namen und eine Beschreibung für den Datensatz in die entsprechenden Felder ein.

Sie können ein Schema anhängen, indem Sie in der Suchleiste &quot;Schema **[!UICONTROL auswählen]** &quot;einen Schema eingeben. Sie können auch das Dropdownsymbol auswählen, um eine Liste der vorhandenen Schema anzuzeigen. Alternativ dazu können Sie die Option &quot; **[!UICONTROL Erweiterte Suche]** &quot;auswählen, um auf den Bildschirm der vorhandenen Schema mit den zugehörigen Details zuzugreifen.

![create-new-dataset](../../../images/tutorials/dataflow/all-tabular/new-target-dataset.png)

The **[!UICONTROL Select schema]** dialog appears. Wählen Sie das Schema aus, das Sie auf den neuen Datensatz anwenden möchten, und klicken Sie dann auf **[!UICONTROL Fertig]**.

![select-Schema](../../../images/tutorials/dataflow/payments/select-schema.png)

Je nach Bedarf können Sie Felder direkt zuordnen oder mithilfe der Zuordnungsfunktionen Quelldaten transformieren, um berechnete oder berechnete Werte abzuleiten. Weitere Informationen zu Funktionen für die Datenzuordnung und -zuordnung finden Sie im Lernprogramm zur [Zuordnung von CSV-Daten zu XDM-Schema-Feldern](../../../../ingestion/tutorials/map-a-csv-file.md).

>[!TIP]
>
>[!DNL Platform] bietet intelligente Empfehlungen für automatisch zugeordnete Zielgruppen, die auf dem von Ihnen ausgewählten Schema oder Datensatz basieren. Sie können Zuordnungsregeln manuell an Ihre Anwendungsfälle anpassen.

Nachdem Sie die Quelldaten zugeordnet haben, wählen Sie **[!UICONTROL Weiter]**.

![](../../../images/tutorials/dataflow/all-tabular/mapping.png)

## Planen von Erfassungsabläufen

Der Schritt **[!UICONTROL Planung]** wird angezeigt, mit dem Sie einen Erfassungszeitplan konfigurieren können, um die ausgewählten Quelldaten automatisch mit den konfigurierten Zuordnungen zu erfassen. In der folgenden Tabelle sind die verschiedenen konfigurierbaren Felder für die Planung aufgeführt:

| Feld | Beschreibung |
| --- | --- |
| Häufigkeit | Zu den auswählbaren Frequenzen gehören `Once`, `Minute`, `Hour`, `Day`und `Week`. |
| Intervall | Eine Ganzzahl, die das Intervall für die ausgewählte Frequenz festlegt. |
| Beginn | Ein UTC-Zeitstempel, der angibt, wann die erste Erfassung erfolgen soll. |
| Aufstockung | Ein boolescher Wert, der bestimmt, welche Daten ursprünglich erfasst werden. Wenn die **[!UICONTROL Aufstockung]** aktiviert ist, werden alle aktuellen Dateien im angegebenen Pfad während der ersten geplanten Erfassung erfasst. Wenn die **[!UICONTROL Aufstockung]** deaktiviert ist, werden nur die Dateien aufgenommen, die zwischen der ersten Ausführung der Erfassung und der **[!UICONTROL Beginn]** geladen wurden. Dateien, die vor dem **[!UICONTROL Beginn]** geladen wurden, werden nicht erfasst. |
| Delta-Spalte | Eine Option mit gefilterten Quelldatumsfeldern vom Typ, Schema oder Uhrzeit. Dieses Feld wird verwendet, um zwischen neuen und vorhandenen Daten zu unterscheiden. Inkrementelle Daten werden basierend auf dem Zeitstempel der ausgewählten Spalte erfasst. |

Datenflüsse sind so konzipiert, dass Daten auf planmäßiger Basis automatisch erfasst werden. Beginn durch Auswahl der Aufnahmefrequenz. Legen Sie als Nächstes das Intervall fest, um den Zeitraum zwischen zwei Flussläufen festzulegen. Der Wert des Intervalls sollte eine Ganzzahl ungleich null sein und auf größer oder gleich 15 gesetzt werden.

Um die Erfassungszeit des Beginns festzulegen, passen Sie das Datum und die Uhrzeit an, die im Feld &quot;Beginn&quot;angezeigt werden. Alternativ können Sie das Kalendersymbol auswählen, um den Zeitwert des Beginns zu bearbeiten. Die Beginn-Zeit muss größer oder gleich der aktuellen UTC-Zeit sein.

Wählen Sie Inkrementelle Daten **[!UICONTROL laden, indem]** Sie die Delta-Spalte zuweisen. In diesem Feld wird zwischen neuen und vorhandenen Daten unterschieden.

![](../../../images/tutorials/dataflow/databases/schedule-interval-on.png)

### Einrichten eines einmaligen Erfassungsdataflow

Um eine einmalige Erfassung einzurichten, wählen Sie den Dropdown-Pfeil für die Häufigkeit aus und klicken Sie auf **[!UICONTROL Einmal]**.

>[!TIP]
>
>**[!UICONTROL Intervall]** und **[!UICONTROL Aufstockung]** sind während einer einmaligen Erfassung nicht sichtbar.

Nachdem Sie die entsprechenden Werte für den Zeitplan angegeben haben, wählen Sie **[!UICONTROL Weiter]**.

![](../../../images/tutorials/dataflow/databases/schedule-once.png)

## Datennachrichtendetails angeben

Der Schritt **[!UICONTROL Datennachweis]** wird angezeigt, mit dem Sie einen Namen eingeben und eine kurze Beschreibung zu Ihrem neuen Datennachweis geben können.

Während dieses Prozesses können Sie auch die **[!UICONTROL teilweise Erfassung]** und **[!UICONTROL Fehlerdiagnose]** aktivieren. Enabling **[!UICONTROL Partial ingestion]** provides the ability to ingest data containing errors up to a certain threshold. Sobald die **[!UICONTROL teilweise Erfassung]** aktiviert ist, ziehen Sie den **[!UICONTROL Fehlerschwellenwert %]** , um den Fehlerschwellenwert des Stapels anzupassen. Alternativ können Sie den Schwellenwert manuell anpassen, indem Sie das Eingabefeld auswählen. Weitere Informationen finden Sie in der Übersicht über die [teilweise Stapelverarbeitung](../../../../ingestion/batch-ingestion/partial.md).

Geben Sie Werte für den Datenflug ein und wählen Sie **[!UICONTROL Weiter]**.

![dataflow-details](../../../images/tutorials/dataflow/all-tabular/dataflow-detail.png)

## Überprüfen Sie Ihren Datenfluss

Der **[!UICONTROL Schritt zum Überprüfen]** wird angezeigt, mit dem Sie Ihren neuen Datenpfad überprüfen können, bevor er erstellt wird. Details werden in den folgenden Kategorien gruppiert:

- **[!UICONTROL Verbindung]**: Zeigt den Quelltyp, den relevanten Pfad der ausgewählten Quelldatei und die Anzahl der Spalten in dieser Quelldatei an.
- **[!UICONTROL Zuweisen von Dataset- und Zuordnungsfeldern]**: Zeigt, in welchen Datensatz die Quelldaten aufgenommen werden, einschließlich des Schemas, das der Datensatz einhält.
- **[!UICONTROL Planung]**: Zeigt den aktiven Zeitraum, die Häufigkeit und das Intervall des Aufnahmeplans an.

Klicken Sie nach Überprüfung des Datenflusses auf **[!UICONTROL Fertig stellen]** und lassen Sie die Erstellung des Datenflusses etwas Zeit.

![überprüfen](../../../images/tutorials/dataflow/payments/review.png)

## Überwachen des Datenflusses

Nachdem Sie Ihren Datenbogen erstellt haben, können Sie die Daten überwachen, die über ihn erfasst werden, um Informationen zu Erfassungsraten, Erfolgen und Fehlern anzuzeigen. Weitere Informationen zur Überwachung des Datenflusses finden Sie im Lernprogramm zu [Überwachungskonten und Datenflüssen in der Benutzeroberfläche](../monitor.md).

## Datenflug löschen

Sie können Datenflüsse löschen, die nicht mehr benötigt werden oder mit der Funktion &quot; **[!UICONTROL Löschen]** &quot;im Arbeitsbereich &quot; **[!UICONTROL Datenflüsse]** &quot;falsch erstellt wurden. Weitere Informationen zum Löschen von Datenflüssen finden Sie im Lernprogramm zum [Löschen von Datenflüssen in der Benutzeroberfläche](../delete.md).

## Nächste Schritte

In diesem Lernprogramm haben Sie erfolgreich einen Datenbogen erstellt, um Daten aus einem Marketingautomatisierungssystem einzubringen und Einblicke in die Überwachung von Datensätzen zu erhalten. Eingehende Daten können nun von nachgelagerten [!DNL Platform] Diensten wie [!DNL Real-time Customer Profile] und [!DNL Data Science Workspace]genutzt werden. Weitere Informationen finden Sie in den folgenden Dokumenten:

- [[!DNL Real-time Customer Profile] Übersicht](../../../../profile/home.md)
- [[!DNL Data Science Workspace] Übersicht](../../../../data-science-workspace/home.md)

## Anhang

Die folgenden Abschnitte enthalten zusätzliche Informationen zum Arbeiten mit Quellschnittstellen.

### Datentaflow deaktivieren

Beim Erstellen eines Datenflusses wird dieser sofort aktiv und erfasst Daten gemäß dem festgelegten Zeitplan. Sie können einen aktiven Datenfeed jederzeit deaktivieren, indem Sie die unten stehenden Anweisungen befolgen.

Wählen Sie im Bildschirm &quot; **[!UICONTROL Datenflüsse]** &quot;den Namen des Datenflusses aus, den Sie deaktivieren möchten.

![browse-dataset-flow](../../../images/tutorials/dataflow/payments/view-dataset-flows.png)

Die Spalte &quot; **[!UICONTROL Eigenschaften]** &quot;wird auf der rechten Seite des Bildschirms angezeigt. Dieses Bedienfeld enthält eine **[!UICONTROL Aktivierungsschaltfläche]** . Klicken Sie auf den Umschalter, um den Datenflug zu deaktivieren. Derselbe Umschalter kann verwendet werden, um einen Datenflug nach dessen Deaktivierung erneut zu aktivieren.

![disable](../../../images/tutorials/dataflow/payments/disable.png)

### Aktivieren von Eingangsdaten für die [!DNL Profile] Bevölkerung

Eingehende Daten aus Ihrem Quellanschluss können zur Anreicherung und zum Ausfüllen Ihrer [!DNL Real-time Customer Profile] Daten verwendet werden. Weitere Informationen zum Ausfüllen Ihrer [!DNL Real-time Customer Profile] Daten finden Sie im Tutorial zur [Profil-Population](../profile.md).
