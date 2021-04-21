---
keywords: Experience Platform;Home;beliebte Themen;Zahlungsverbindung
solution: Experience Platform
title: Konfigurieren eines Datenflusses für eine Zahlungsquellenverbindung in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
description: Ein Datennachweis ist eine geplante Aufgabe, mit der Daten aus einer Quelle abgerufen und in einen Adobe Experience Platform-Datensatz aufgenommen werden. Dieses Lernprogramm enthält Schritte zum Konfigurieren eines neuen Datenflusses mit Ihrem Zahlungskonto.
exl-id: 7355435b-c038-4310-b04a-8ac6b6723b9b
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1463'
ht-degree: 3%

---

# Konfigurieren eines Datenflusses für eine Zahlungsverbindung in der Benutzeroberfläche

Ein Datennachweis ist eine geplante Aufgabe, mit der Daten aus einer Quelle abgerufen und in einen Adobe Experience Platform-Datensatz aufgenommen werden. Dieses Lernprogramm enthält Schritte zum Konfigurieren eines neuen Datenflusses mit Ihrem Zahlungskonto.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [[!DNL Experience Data Model (XDM)] System](../../../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten  [!DNL Experience Platform] organisiert werden.
   - [Grundlagen der Schemakomposition](../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   - [Schema-Editor-Lernprogramm](../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
- [[!DNL Real-time Customer Profile]](../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

Darüber hinaus erfordert dieses Lernprogramm, dass Sie bereits ein Zahlungskonto erstellt haben. Eine Liste von Übungen zum Erstellen verschiedener Zahlungsschnittstellen in der Benutzeroberfläche finden Sie in der [Übersicht über die Quellschnittstellen](../../../home.md).

## Daten auswählen

Nachdem Sie Ihr Zahlungskonto erstellt haben, wird der Schritt **[!UICONTROL Daten auswählen]** angezeigt und bietet eine interaktive Oberfläche, über die Sie Ihre Dateihierarchie untersuchen können.

- Die linke Hälfte der Oberfläche ist ein Ordnerbrowser, der die Dateien und Ordner Ihres Servers anzeigt.
- In der rechten Hälfte der Oberfläche können Sie bis zu 100 Datenzeilen aus einer kompatiblen Datei Vorschau werden.

Mit der Option **[!UICONTROL Suchen]** oben auf der Seite können Sie schnell die Quelldaten identifizieren, die Sie verwenden möchten.

>[!NOTE]
>
>Die Suchquellendaten-Option steht allen tabellarischen Quellschnittstellen mit Ausnahme der Connectors für Analytics, Classifications, Ereignis Hubs und Kinesis zur Verfügung.

Sobald Sie die Quelldaten gefunden haben, wählen Sie den Ordner aus und klicken Sie dann auf **[!UICONTROL Weiter]**.

![select-data](../../../images/tutorials/dataflow/all-tabular/select-data.png)

## Zuordnen von Datenfeldern zu einem XDM-Schema

Der Schritt **[!UICONTROL Zuordnung]** wird angezeigt und stellt eine interaktive Schnittstelle bereit, um die Quelldaten einem [!DNL Platform]-Datensatz zuzuordnen.

Wählen Sie einen Datensatz, in den eingehende Daten aufgenommen werden sollen. Sie können entweder einen vorhandenen Datensatz verwenden oder einen neuen Datensatz erstellen.

### Vorhandenen Datensatz verwenden

Um Daten in einen vorhandenen Datensatz zu erfassen, wählen Sie **[!UICONTROL Vorhandenen Datensatz verwenden]** und klicken Sie dann auf das Dataset-Symbol.

![use-existing-dataset](../../../images/tutorials/dataflow/payments/existing-dataset.png)

Das Dialogfeld **[!UICONTROL Datensatz auswählen]** wird angezeigt. Suchen Sie den gewünschten Datensatz, wählen Sie ihn aus und klicken Sie dann auf **[!UICONTROL Weiter]**.

![select-existing-dataset](../../../images/tutorials/dataflow/payments/select-dataset.png)

### Verwenden eines neuen Datensatzes

Um Daten in einen neuen Datensatz zu erfassen, wählen Sie **[!UICONTROL Neuen Datensatz erstellen]** und geben Sie in die entsprechenden Felder einen Namen und eine Beschreibung für den Datensatz ein.

Sie können ein Schema anhängen, indem Sie in der Suchleiste **[!UICONTROL Schema]** auswählen einen Schema eingeben. Sie können auch das Dropdownsymbol auswählen, um eine Liste der vorhandenen Schema anzuzeigen. Alternativ können Sie **[!UICONTROL Erweiterte Suche]** auswählen, um auf den Bildschirm der vorhandenen Schema mit den entsprechenden Details zuzugreifen.

In diesem Schritt können Sie Ihren Datensatz für [!DNL Real-time Customer Profile] aktivieren und eine holistische Ansicht der Attribute und Verhaltensweisen einer Entität erstellen. Daten aus allen aktivierten Datensätzen werden in [!DNL Profile] eingeschlossen und beim Speichern des Datenflusses werden Änderungen angewendet.

Schalten Sie die Schaltfläche **[!UICONTROL Profil-Datensatz]** um, um Ihren Zielgruppen-Datensatz für [!DNL Profile] zu aktivieren.

![create-new-dataset](../../../images/tutorials/dataflow/payments/new-dataset.png)

Das Dialogfeld **[!UICONTROL Schema auswählen]** wird angezeigt. Wählen Sie das Schema aus, das Sie auf den neuen Datensatz anwenden möchten, und klicken Sie dann auf **[!UICONTROL Fertig]**.

![select-Schema](../../../images/tutorials/dataflow/payments/select-schema.png)

Je nach Bedarf können Sie Felder direkt zuordnen oder mithilfe der Zuordnungsfunktionen Quelldaten transformieren, um berechnete oder berechnete Werte abzuleiten. Weitere Informationen zu Datenzuordnungs- und -zuordnungsfunktionen finden Sie im Lernprogramm [Zuordnen von CSV-Daten zu XDM-Schema-Feldern](../../../../ingestion/tutorials/map-a-csv-file.md).

>[!TIP]
>
>[!DNL Platform] bietet intelligente Empfehlungen für automatisch zugeordnete Zielgruppen, die auf dem von Ihnen ausgewählten Schema oder Datensatz basieren. Sie können Zuordnungsregeln manuell an Ihre Anwendungsfälle anpassen.

![](../../../images/tutorials/dataflow/all-tabular/mapping.png)

Wählen Sie **[!UICONTROL Vorschau data]** aus, um die Zuordnungsergebnisse von bis zu 100 Zeilen mit Musterdaten aus dem ausgewählten Datensatz anzuzeigen.

Während der Vorschau wird die Identitätsspalte als erstes Feld priorisiert, da sie die wichtigen Informationen darstellt, die bei der Validierung der Zuordnungsergebnisse erforderlich sind.

![](../../../images/tutorials/dataflow/all-tabular/mapping-preview.png)

Sobald die Quelldaten zugeordnet sind, wählen Sie **[!UICONTROL Schließen]**.

## Planen von Erfassungsabläufen

Der Schritt **[!UICONTROL Einplanen]** wird angezeigt, mit dem Sie einen Zeitplan für die Erfassung konfigurieren können, um die ausgewählten Quelldaten automatisch mit den konfigurierten Zuordnungen zu erfassen. In der folgenden Tabelle sind die verschiedenen konfigurierbaren Felder für die Planung aufgeführt:

| Feld | Beschreibung |
| --- | --- |
| Häufigkeit | Zu den auswählbaren Frequenzen gehören `Once`, `Minute`, `Hour`, `Day` und `Week`. |
| Intervall | Eine Ganzzahl, die das Intervall für die ausgewählte Frequenz festlegt. |
| Beginn | Ein UTC-Zeitstempel, der angibt, wann die erste Erfassung erfolgen soll. |
| Aufstockung | Ein boolescher Wert, der bestimmt, welche Daten ursprünglich erfasst werden. Ist **[!UICONTROL Aufstockung]** aktiviert, werden alle aktuellen Dateien im angegebenen Pfad während der ersten geplanten Erfassung erfasst. Wenn **[!UICONTROL Aufstockung]** deaktiviert ist, werden nur die Dateien erfasst, die zwischen der ersten Ausführung der Erfassung und der Beginn geladen werden. Dateien, die vor dem Beginn geladen wurden, werden nicht erfasst. |
| Delta-Spalte | Eine Option mit gefilterten Quelldatumsfeldern vom Typ, Schema oder Uhrzeit. Dieses Feld wird verwendet, um zwischen neuen und vorhandenen Daten zu unterscheiden. Inkrementelle Daten werden basierend auf dem Zeitstempel der ausgewählten Spalte erfasst. |

Datenflüsse sind so konzipiert, dass Daten auf planmäßiger Basis automatisch erfasst werden. Beginn durch Auswahl der Aufnahmefrequenz. Legen Sie als Nächstes das Intervall fest, um den Zeitraum zwischen zwei Flussläufen festzulegen. Der Wert des Intervalls sollte eine Ganzzahl ungleich null sein und auf größer oder gleich 15 gesetzt werden.

Um die Erfassungszeit des Beginns festzulegen, passen Sie das Datum und die Uhrzeit an, die im Feld &quot;Beginn&quot;angezeigt werden. Alternativ können Sie das Kalendersymbol auswählen, um den Zeitwert des Beginns zu bearbeiten. Die Beginn-Zeit muss größer oder gleich der aktuellen UTC-Zeit sein.

Wählen Sie **[!UICONTROL Inkrementelle Daten von]** laden, um die Delta-Spalte zuzuweisen. In diesem Feld wird zwischen neuen und vorhandenen Daten unterschieden.

![](../../../images/tutorials/dataflow/databases/schedule-interval-on.png)

### Einrichten eines einmaligen Erfassungsdataflow

Um eine einmalige Erfassung einzurichten, wählen Sie den Dropdown-Pfeil für die Häufigkeit aus und wählen Sie **[!UICONTROL Once]**.

>[!TIP]
>
>**[!UICONTROL Während einer einmaligen Erfassung sind keine]** Intervalle und  **** Backfillments sichtbar.

Nachdem Sie die entsprechenden Werte für den Zeitplan angegeben haben, wählen Sie **[!UICONTROL Weiter]**.

![](../../../images/tutorials/dataflow/databases/schedule-once.png)

## Datenflussinformationen bereitstellen

Der Schritt **[!UICONTROL Datentiefe]** wird angezeigt, mit dem Sie einen Namen eingeben und eine kurze Beschreibung zu Ihrem neuen Datenpfad geben können.

Während dieses Prozesses können Sie auch die Optionen **[!UICONTROL Partielle Erfassung]** und **[!UICONTROL Fehlerdiagnose]** aktivieren. Durch Aktivierung von **[!UICONTROL Partielle Erfassung]** können Daten mit Fehlern bis zu einem bestimmten Schwellenwert erfasst werden. Sobald **[!UICONTROL Partielle Erfassung]** aktiviert ist, ziehen Sie das **[!UICONTROL Fehlerschwellenwert %]**, um den Fehlerschwellenwert des Stapels anzupassen. Alternativ können Sie den Schwellenwert manuell anpassen, indem Sie das Eingabefeld auswählen. Weitere Informationen finden Sie unter [Übersicht über die teilweise Stapelverarbeitung](../../../../ingestion/batch-ingestion/partial.md).

Geben Sie Werte für den Datenfluss ein und wählen Sie **[!UICONTROL Weiter]**.

![dataflow-details](../../../images/tutorials/dataflow/all-tabular/dataflow-detail.png)

## Überprüfen Sie Ihren Datenfluss

Der Schritt **[!UICONTROL Überprüfen]** wird angezeigt, mit dem Sie Ihren neuen Datenpfad überprüfen können, bevor er erstellt wird. Details werden in den folgenden Kategorien gruppiert:

- **[!UICONTROL Verbindung]**: Zeigt den Quelltyp, den relevanten Pfad der ausgewählten Quelldatei und die Anzahl der Spalten in dieser Quelldatei an.
- **[!UICONTROL Zuweisen von Dataset- und Zuordnungsfeldern]**: Zeigt, in welchen Datensatz die Quelldaten aufgenommen werden, einschließlich des Schemas, das der Datensatz einhält.
- **[!UICONTROL Planung]**: Zeigt den aktiven Zeitraum, die Häufigkeit und das Intervall des Aufnahmeplans an.

Klicken Sie nach Überprüfung Ihres Datenflusses auf **[!UICONTROL Fertig stellen]** und lassen Sie etwas Zeit für die Erstellung des Datenflusses zu.

![überprüfen](../../../images/tutorials/dataflow/payments/review.png)

## Überwachen des Datenflusses

Nachdem Sie Ihren Datenbogen erstellt haben, können Sie die Daten überwachen, die über ihn erfasst werden, um Informationen zu Erfassungsraten, Erfolgen und Fehlern anzuzeigen. Weitere Informationen zur Überwachung des Datenflusses finden Sie im Lernprogramm zu [Überwachungskonten und Datenflüssen in der Benutzeroberfläche](../monitor.md).

## Datenflug löschen

Sie können Datenflüsse löschen, die nicht mehr benötigt werden oder mit der Funktion **[!UICONTROL Delete]**, die im Arbeitsbereich **[!UICONTROL Datenflüsse]** verfügbar ist, falsch erstellt wurden. Weitere Informationen zum Löschen von Datenflüssen finden Sie im Lernprogramm zum [Löschen von Datenflüssen in der Benutzeroberfläche](../delete.md).

## Nächste Schritte

In diesem Lernprogramm haben Sie erfolgreich einen Datenbogen erstellt, um Daten aus einem Marketingautomatisierungssystem einzubringen und Einblicke in die Überwachung von Datensätzen zu erhalten. Eingangsdaten können nun von nachgeschalteten [!DNL Platform]-Diensten wie [!DNL Real-time Customer Profile] und [!DNL Data Science Workspace] verwendet werden. Weitere Informationen finden Sie in den folgenden Dokumenten:

- [[!DNL Real-time Customer Profile] Übersicht](../../../../profile/home.md)
- [[!DNL Data Science Workspace] Übersicht](../../../../data-science-workspace/home.md)

## Anhang

Die folgenden Abschnitte enthalten zusätzliche Informationen zum Arbeiten mit Quellschnittstellen.

### Datentaflow deaktivieren

Beim Erstellen eines Datenflusses wird dieser sofort aktiv und erfasst Daten gemäß dem festgelegten Zeitplan. Sie können einen aktiven Datenfeed jederzeit deaktivieren, indem Sie die unten stehenden Anweisungen befolgen.

Wählen Sie im Bildschirm **[!UICONTROL Datenflüsse]** den Namen des Datenflusses aus, den Sie deaktivieren möchten.

![browse-dataset-flow](../../../images/tutorials/dataflow/payments/view-dataset-flows.png)

Die Spalte **[!UICONTROL Eigenschaften]** wird auf der rechten Seite des Bildschirms angezeigt. Dieses Bedienfeld enthält die Umschalter **[!UICONTROL Aktiviert]**. Klicken Sie auf den Umschalter, um den Datenflug zu deaktivieren. Derselbe Umschalter kann verwendet werden, um einen Datenflug nach dessen Deaktivierung erneut zu aktivieren.

![disable](../../../images/tutorials/dataflow/payments/disable.png)

### Aktivieren von Eingangsdaten für [!DNL Profile] Population

Eingehende Daten aus Ihrem Quellanschluss können zur Anreicherung und zum Ausfüllen Ihrer [!DNL Real-time Customer Profile]-Daten verwendet werden. Weitere Informationen zum Ausfüllen der [!DNL Real-time Customer Profile]-Daten finden Sie im Lernprogramm [Profil population](../profile.md).
