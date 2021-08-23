---
keywords: Experience Platform; Startseite; beliebte Themen; lokales System; Datei-Upload; CSV zuordnen; CSV-Datei zuordnen; CSV-Datei xdm zuordnen; CSV-Datei xdm zuordnen; Handbuch zu ui;
solution: Experience Platform
title: Erstellen eines Connectors für lokale Datei-Upload-Quelle in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie eine Quellverbindung für Ihr lokales System erstellen, um lokale Dateien auf Platform zu bringen.
source-git-commit: 1bf112db27b534e2ec977be7b47e3becf75ee066
workflow-type: tm+mt
source-wordcount: '1271'
ht-degree: 5%

---

# Erstellen eines Quell-Connectors für den lokalen Datei-Upload über die Benutzeroberfläche

In diesem Tutorial werden die Schritte zum Erstellen eines Quell-Connectors für den lokalen Datei-Upload beschrieben, um mithilfe der Benutzeroberfläche lokale Dateien in Platform zu erfassen.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) zum Schema Editor: Erfahren Sie, wie Sie benutzerdefinierte Schemas mithilfe der Benutzeroberfläche des Schema-Editors erstellen.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

## Hochladen lokaler Dateien in Platform

Wählen Sie in der Platform-Benutzeroberfläche **[!UICONTROL Quellen]** aus der linken Navigationsleiste aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der Bildschirm [!UICONTROL Katalog] enthält eine Vielzahl von Quellen, für die Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter der Kategorie [!UICONTROL Lokales System] die Option **[!UICONTROL Lokaler Datei-Upload]** und klicken Sie dann auf **[!UICONTROL Konfigurieren]**.

![Katalog](../../../../images/tutorials/create/local/catalog.png)

### Vorhandenen Datensatz verwenden

Auf der Seite [!UICONTROL Datenfluss-Detail] können Sie auswählen, ob Sie Ihre CSV-Daten in einen vorhandenen Datensatz oder in einen neuen Datensatz aufnehmen möchten.

Um Ihre CSV-Daten in einen vorhandenen Datensatz zu erfassen, wählen Sie **[!UICONTROL Vorhandenen Datensatz]** aus. Sie können einen vorhandenen Datensatz entweder mit der Option [!UICONTROL Erweiterte Suche] abrufen oder indem Sie im Dropdown-Menü durch die Liste der vorhandenen Datensätze scrollen.

![select-existing-dataset](../../../../images/tutorials/create/local/select-existing-dataset.png)

Geben Sie bei ausgewähltem Datensatz einen Namen für Ihren Datenfluss und eine optionale Beschreibung an.

Während dieses Prozesses können Sie auch [!UICONTROL Fehlerdiagnose] und [!UICONTROL Partielle Erfassung] aktivieren. [!UICONTROL Die ] Fehlerdiagnose ermöglicht eine detaillierte Erzeugung von Fehlermeldungen für alle fehlerhaften Datensätze, die in Ihrem Datenfluss auftreten. Bei der  [!UICONTROL partiellen ] Erfassung können Sie Daten mit Fehlern bis zu einem bestimmten Schwellenwert erfassen, den Sie manuell definieren. Weitere Informationen finden Sie unter [Übersicht über die partielle Batch-Erfassung](../../../../../ingestion/batch-ingestion/partial.md) .

![dataflow-detail-existing](../../../../images/tutorials/create/local/dataflow-detail-existing.png)

### Verwenden eines neuen Datensatzes

Um Ihre CSV-Daten in einen neuen Datensatz zu erfassen, wählen Sie **[!UICONTROL Neuer Datensatz]** aus und geben Sie dann einen Namen für den Ausgabedatensatz und eine optionale Beschreibung an. Wählen Sie anschließend ein Schema aus, das mithilfe der Option [!UICONTROL Erweiterte Suche] zugeordnet werden soll, oder scrollen Sie durch die Liste der vorhandenen Schemas im Dropdown-Menü.

![select-new-dataset](../../../../images/tutorials/create/local/select-new-dataset.png)

Geben Sie bei ausgewähltem Schema einen Namen für Ihren Datenfluss und eine optionale Beschreibung ein und wenden Sie dann die Einstellungen [!UICONTROL Fehlerdiagnose] und [!UICONTROL Partielle Erfassung] an, die Sie für Ihren Datenfluss benötigen. Wählen Sie nach Abschluss **[!UICONTROL Weiter]** aus.

### Daten auswählen

Der Schritt [!UICONTROL Daten auswählen] wird angezeigt und bietet Ihnen eine Oberfläche zum Hochladen Ihrer lokalen Dateien und zur Vorschau ihrer Struktur und Inhalte. Wählen Sie **[!UICONTROL Dateien]** aus, um eine CSV-Datei von Ihrem lokalen System hochzuladen. Alternativ können Sie die CSV-Datei, die Sie hochladen möchten, per Drag-and-Drop in das Bedienfeld [!UICONTROL Drag-and-Drop von Dateien] ziehen.

>[!TIP]
>
>Derzeit werden nur CSV-Dateien vom lokalen Datei-Upload unterstützt. Die maximale Dateigröße pro Datei beträgt 1 GB.

![choice-files](../../../../images/tutorials/create/local/choose-files.png)

Nach dem Hochladen Ihrer Datei wird die Vorschau-Oberfläche aktualisiert, um Inhalt und Struktur der Datei anzuzeigen.

![preview-sample-data](../../../../images/tutorials/create/local/preview-sample-data.png)

Je nach Datei können Sie ein Spaltentrennzeichen wie Tabulatoren, Kommas, senkrechte Striche oder ein benutzerdefiniertes Spaltentrennzeichen für die Quelldaten auswählen. Wählen Sie den Dropdown-Pfeil **[!UICONTROL Trennzeichen]** aus und wählen Sie dann das entsprechende Trennzeichen aus dem Menü aus.

Wählen Sie nach Abschluss **[!UICONTROL Weiter]** aus.

![delimiter](../../../../images/tutorials/create/local/delimiter.png)

### Zuordnung

Der Schritt [!UICONTROL Mapping] wird angezeigt und bietet Ihnen eine Schnittstelle zum Zuordnen der Quellfelder aus Ihrem Quellschema zu den entsprechenden Ziel-XDM-Feldern im Zielschema.

![mapping-interface](../../../../images/tutorials/create/local/mapping-interface.png)

#### Vorschau der Daten

Wählen Sie **[!UICONTROL Vorschau der Daten]** aus, um die Zuordnungsergebnisse von bis zu 100 Zeilen mit Beispieldaten aus dem ausgewählten Datensatz anzuzeigen.

![preview-mapping](../../../../images/tutorials/create/local/preview-mapping.png)

Während der Vorschau wird die Identitätsspalte als erstes Feld priorisiert, da dies die wichtigsten Informationen ist, die bei der Validierung der Zuordnungsergebnisse erforderlich sind. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Close]** aus.

![preview-panel](../../../../images/tutorials/create/local/preview-panel.png)

#### Berechnetes Feld hinzufügen

Berechnete Felder ermöglichen die Erstellung von Werten anhand der Attribute im Eingabeschema. Diese Werte können dann Attributen im Zielschema zugewiesen und mit einem Namen und einer Beschreibung versehen werden, um eine einfachere Referenz zu ermöglichen.

Wählen Sie die Schaltfläche **[!UICONTROL Berechnetes Feld hinzufügen]** aus, um fortzufahren.

![add-calculated-field](../../../../images/tutorials/create/local/add-calculated-field.png)

Das Bedienfeld [!UICONTROL Berechnetes Feld erstellen] wird angezeigt. Das linke Dialogfeld enthält die Felder, Funktionen und Operatoren, die in berechneten Feldern unterstützt werden. Wählen Sie eine der Registerkarten aus, um dem Ausdruckseditor Funktionen, Felder oder Operatoren hinzuzufügen.

![create-calculated-field](../../../../images/tutorials/create/local/create-calculated-field.png)

| Tab | Beschreibung |
| --------- | ----------- |
| Funktion | Im Tab Funktionen werden die Funktionen aufgelistet, die zur Transformation der Daten verfügbar sind. Weitere Informationen zu den Funktionen, die Sie in berechneten Feldern verwenden können, finden Sie im Handbuch [Verwendung der Datenvorbereitung (Mapper)-Funktionen](../../../../../data-prep/functions.md). |
| Feld | Auf der Registerkarte Felder werden die im Quellschema verfügbaren Felder und Attribute aufgelistet. |
| Operator | Im Tab Operatoren werden die zur Transformation der Daten verfügbaren Operatoren aufgelistet. |

Wählen Sie den Ausdruckseditor aus, um Felder, Funktionen und Operatoren manuell hinzuzufügen. Nachdem Sie ein berechnetes Feld erstellt haben, wählen Sie **[!UICONTROL Speichern]** aus, um fortzufahren.

![expression-editor](../../../../images/tutorials/create/local/expression-editor.png)

#### Zuordnungsstruktur des Quellschemas filtern

Um nach Ihrem Quellschema zu filtern, wählen Sie **[!UICONTROL Alle Quellfelder]** und dann das spezifische Feld, das Sie zuordnen möchten, aus dem Dropdown-Menü aus.

In der folgenden Tabelle werden die Sortieroptionen für die Quellschemastruktur angezeigt:

| Quellfelder | Beschreibung |
| --- | --- |
| [!UICONTROL Alle Quellfelder] | Diese Option zeigt alle Quellfelder Ihres Quellschemas an. Diese Option wird standardmäßig angezeigt. |
| [!UICONTROL Erforderliche Felder] | Diese Option filtert das Quellschema so, dass nur die Felder angezeigt werden, die zum Abschließen der Zuordnung erforderlich sind. |
| [!UICONTROL Identitätsfelder] | Diese Option filtert das Quellschema so, dass nur die Felder angezeigt werden, die für Identity markiert sind. |
| [!UICONTROL Zugeordnete Felder] | Diese Option filtert das Quellschema so, dass nur die Felder angezeigt werden, die bereits zugeordnet wurden. |
| [!UICONTROL Nicht zugeordnete Felder] | Diese Option filtert das Quellschema so, dass nur die Felder angezeigt werden, die noch zugeordnet werden müssen. |
| [!UICONTROL Felder mit Empfehlung] | Diese Option filtert das Quellschema so, dass nur die Felder angezeigt werden, die Zuordnungsempfehlungen enthalten. |

![all-source-fields](../../../../images/tutorials/create/local/all-source-fields.png)

#### Intelligente Empfehlungen

Platform bietet automatisch intelligente Empfehlungen für automatisch zugeordnete Felder, die auf dem von Ihnen ausgewählten Zielschema oder Datensatz basieren. Sie können die Zuordnungsregeln manuell an Ihre Anwendungsfälle anpassen.

![source-schema-tree](../../../../images/tutorials/create/local/source-schema-tree.png)

Um alle automatisch generierenden Zuordnungswerte zu akzeptieren, wählen Sie **[!UICONTROL Alle Zielfelder akzeptieren]**.

![all-target-fields](../../../../images/tutorials/create/local/all-target-fields.png)

Manchmal ist mehr als eine Empfehlung für das Quellschema verfügbar. In diesem Fall zeigt die Zuordnungskarte die auffälligste Empfehlung an, gefolgt von einem blauen Kreis, der die Anzahl der verfügbaren zusätzlichen Empfehlungen enthält. Durch Auswahl des Glühbirnensymbols wird eine Liste der zusätzlichen Empfehlungen angezeigt. Sie können eine der alternativen Empfehlungen auswählen, indem Sie das Kontrollkästchen neben der Empfehlung aktivieren, der Sie die Empfehlung zuordnen möchten.

![manuelles Mapping](../../../../images/tutorials/create/local/manual-mapping.png)

Alternativ können Sie Ihr Quellschema manuell Ihrem Zielschema zuordnen. Bewegen Sie dazu den Mauszeiger über das Quellschema, das Sie zuordnen möchten, und wählen Sie dann das Pluszeichen (`+`) aus.

![select-plus-icon](../../../../images/tutorials/create/local/select-plus-icon.png)

Das Popup **[!UICONTROL Quelle dem Zielfeld zuordnen]** wird angezeigt. Von hier aus können Sie auswählen, welches Feld Sie zuordnen möchten, gefolgt von **[!UICONTROL Speichern]**, um Ihre neue Zuordnung hinzuzufügen.

![map-source-to-target-field](../../../../images/tutorials/create/local/map-source-to-target-field.png)

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Abgeschlossen]** aus.

![Beenden](../../../../images/tutorials/create/local/finish.png)

## Überwachen der Datenerfassung

Nachdem Ihre CSV-Datei zugeordnet und erstellt wurde, können Sie die über sie erfassten Daten mithilfe des Monitoring-Dashboards überwachen. Weitere Informationen finden Sie im Tutorial zum [Überwachen von Datenflüssen zu Quellen in der Benutzeroberfläche](../../../../../dataflows/ui/monitor-sources.md).

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich eine flache CSV-Datei einem XDM-Schema zugeordnet und in Platform aufgenommen. Diese Daten können jetzt von nachgelagerten [!DNL Platform]-Diensten wie [!DNL Real-time Customer Profile] verwendet werden. Weitere Informationen finden Sie in der Übersicht zu [[!DNL Real-time Customer Profile]](../../../../../profile/home.md) .
