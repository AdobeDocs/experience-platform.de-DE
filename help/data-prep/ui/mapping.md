---
keywords: Experience Platform;Startseite;beliebte Themen;CSV zuordnen;CSV-Datei zuordnen;CSV-Datei zu xdm zuordnen;CSV zu xdm zuordnen;ui-Handbuch;Mapper;Zuordnung;Datenvorbereitung;Datenvorbereitung;Vorbereiten von Daten;
title: Anleitung zur Datenvorbereitung-Benutzeroberfläche
description: In diesem Dokument erfahren Sie, wie Sie mithilfe von Datenvorbereitungsfunktionen in der Platform-Benutzeroberfläche CSV-Dateien einem XDM-Schema zuordnen können.
source-git-commit: 4c2e3380881e6a032100ef00502b55112f3b103f
workflow-type: tm+mt
source-wordcount: '1665'
ht-degree: 17%

---

# Anleitung zur Datenvorbereitung-Benutzeroberfläche

In diesem Dokument erfahren Sie, wie Sie in der Adobe Experience Platform-Benutzeroberfläche mithilfe von Datenvorbereitungsfunktionen CSV-Dateien einem XDM-Schema zuordnen können.

## Erste Schritte

Dieses Tutorial setzt ein Verständnis der folgenden Platform-Komponenten voraus:

* [[!DNL Experience Data Model (XDM)] System](../../xdm/home.md): Das standardisierte Framework, mit dem Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   * [Tutorial zum Schema Editor](../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemas mithilfe der Benutzeroberfläche des Schema-Editors erstellen.
* [Identity Service](../../identity-service/home.md): Sorgt für eine bessere Darstellung einzelner Kunden und deren Verhalten, indem Identitäten zwischen Geräten und Systemen überbrückt werden.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
* [Quellen](../../sources/home.md): Experience Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von Platform-Diensten zu strukturieren, zu beschriften und zu erweitern.

## Datenflussdetails

>[!TIP]
>
>Sie können auf Datenflussdetails zugreifen, indem Sie eine beliebige Quelle aus dem Quellkatalog auswählen. Weitere Informationen finden Sie unter [Quellen - Übersicht](../../sources/home.md).

Bevor Sie Ihre CSV-Daten einem XDM-Schema zuordnen können, müssen Sie zunächst die Details Ihres Datenflusses festlegen.

Die [!UICONTROL Datenflussdetails] -Seite können Sie auswählen, ob Sie Ihre CSV-Daten in einen vorhandenen Zieldatensatz oder einen neuen Zieldatensatz aufnehmen möchten. Ein vorhandener Datensatz enthält ein vordefiniertes Zielschema, dem Ihre Daten zugeordnet werden können. Für einen neuen Datensatz müssen Sie jedoch ein vorhandenes Schema auswählen oder ein neues Schema erstellen, dem Ihre Daten zugeordnet werden sollen.

### Vorhandenen Zieldatensatz verwenden

Um Ihre CSV-Daten in einen vorhandenen Datensatz zu erfassen, wählen Sie **[!UICONTROL Vorhandener Datensatz]**. Sie können einen vorhandenen Datensatz entweder mit der [!UICONTROL Erweiterte Suche] oder durch Scrollen durch die Liste der vorhandenen Datensätze im Dropdown-Menü.

Geben Sie bei ausgewähltem Datensatz einen Namen für Ihren Datenfluss und eine optionale Beschreibung an.

Während dieses Vorgangs können Sie auch [!UICONTROL Fehlerdiagnose] und [!UICONTROL Partielle Erfassung]. [!UICONTROL Fehlerdiagnose] ermöglicht eine detaillierte Erzeugung von Fehlermeldungen für alle fehlerhaften Datensätze, die in Ihrem Datenfluss auftreten, während [!UICONTROL Partielle Erfassung] ermöglicht die Aufnahme von fehlerhaften Daten bis zu einem bestimmten Schwellenwert, den Sie manuell definieren. Siehe [partielle Batch-Erfassung - Übersicht](../../ingestion/batch-ingestion/partial.md) für weitere Informationen.

![existing-dataset](../images/ui/mapping/existing-dataset.png)

### Verwenden eines neuen Zieldatensatzes

Um Ihre CSV-Daten in einen neuen Datensatz zu erfassen, wählen Sie **[!UICONTROL Neuer Datensatz]** und geben Sie dann einen Namen für den Ausgabedatensatz und eine optionale Beschreibung an. Wählen Sie als Nächstes ein Schema aus, das mithilfe des [!UICONTROL Erweiterte Suche] oder durch Scrollen durch die Liste der vorhandenen Schemas im Dropdown-Menü.

Geben Sie bei ausgewähltem Schema einen Namen für Ihren Datenfluss und eine optionale Beschreibung ein und wenden Sie dann die [!UICONTROL Fehlerdiagnose] und [!UICONTROL Partielle Erfassung] -Einstellungen, die Sie für Ihren Datenfluss benötigen. Wenn Sie fertig sind, klicken Sie auf **[!UICONTROL Weiter]**.

![new-dataset](../images/ui/mapping/new-dataset.png)

## Daten auswählen

Die [!UICONTROL Daten auswählen] -Schritt angezeigt werden. Sie erhalten eine Oberfläche zum Hochladen Ihrer lokalen Dateien und zur Vorschau ihrer Struktur und Inhalte. Auswählen **[!UICONTROL Dateien auswählen]** , um eine CSV-Datei von Ihrem lokalen System hochzuladen. Alternativ können Sie die CSV-Datei, die Sie hochladen möchten, per Drag-and-Drop in die [!UICONTROL Dateien per Drag &amp; Drop verschieben] Bereich.

>[!TIP]
>
>Derzeit werden nur CSV-Dateien vom lokalen Datei-Upload unterstützt. Die maximale Dateigröße pro Datei beträgt 1 GB.

![choice-files](../images/ui/mapping/choose-files.png)

Nach dem Hochladen Ihrer Datei wird die Vorschau-Oberfläche aktualisiert, um Inhalt und Struktur der Datei anzuzeigen.

![preview-sample-data](../images/ui/mapping/preview-sample-data.png)

Je nach Datei können Sie ein Spaltentrennzeichen wie Tabulatoren, Kommas, senkrechte Striche oder ein benutzerdefiniertes Spaltentrennzeichen für die Quelldaten auswählen. Wählen Sie die **[!UICONTROL Trennzeichen]** Dropdown-Pfeil und wählen Sie dann das entsprechende Trennzeichen aus dem Menü aus.

Wenn Sie fertig sind, klicken Sie auf **[!UICONTROL Weiter]**.

![delimiter](../images/ui/mapping/delimiter.png)

## Zuordnung

Die **[!UICONTROL Mapping]** -Schnittstelle bietet Ihnen ein umfassendes Tool zur Zuordnung von Quellfeldern aus Ihrem Quellschema zu den entsprechenden Ziel-XDM-Feldern im Zielschema.

![map-csv-to-xdm](../images/ui/mapping/map-csv-to-xdm.png)

### Grundlegendes zur Zuordnungsschnittstelle

Die Zuordnungsoberfläche enthält ein Dashboard, das Informationen zum Zustand Ihrer Zuordnungssätze im Kontext des Aufnahme-Workflows bereitstellt. Im Dashboard werden die folgenden Details zu Ihren Zuordnungssätzen angezeigt:

| Eigenschaft | Beschreibung |
| --- | --- |
| [!UICONTROL Zugeordnete Felder] | Zeigt die Gesamtzahl der Quellfelder an, die einem Ziel-XDM-Feld zugeordnet wurden, unabhängig von Fehlern. |
| [!UICONTROL Erforderliche Felder] | Zeigt die Anzahl der erforderlichen Zuordnungsfelder an. |
| [!UICONTROL Identitätsfelder] | Zeigt die Gesamtzahl der als Identität definierten Zuordnungssätze an. Diese Zuordnungssätze werden durch ein Fingerabdrucksymbol dargestellt. |
| [!UICONTROL Fehler] | Zeigt die Anzahl fehlerhafter Zuordnungssätze an. |

![oberer Bereich](../images/ui/mapping/top-panel.png)

Die Zuordnungsoberfläche bietet außerdem ein Optionsfeld, aus dem Sie auswählen können, um Ihre Zuordnungssätze besser zu interagieren oder zu filtern.

![zweites Bedienfeld](../images/ui/mapping/second-panel.png)

Um nach einem bestimmten Zuordnungssatz zu suchen, wählen Sie **[!UICONTROL Suchquellfelder]** und geben Sie den Namen der Quelldaten ein, die Sie isolieren möchten.

![Suchen](../images/ui/mapping/search.png)

Auswählen **[!UICONTROL Alle Quellfelder]** um ein Dropdown-Menü mit Filteroptionen anzuzeigen, um Ihre Ansicht der Zuordnungsschnittstelle besser einzugrenzen.

Die Filteroptionen sind:

| Quellfelder | Beschreibung |
| --- | --- |
| [!UICONTROL Alle Quellfelder] | Diese Option zeigt alle Quellfelder Ihres Quellschemas an. Diese Option wird standardmäßig angezeigt. |
| [!UICONTROL Erforderliche Felder] | Diese Option filtert das Quellschema so, dass nur die Felder angezeigt werden, die zum Abschließen der Zuordnung erforderlich sind. |
| [!UICONTROL Identitätsfelder] | Diese Option filtert das Quellschema so, dass nur die Felder angezeigt werden, die für Identity markiert sind. |
| [!UICONTROL Zugeordnete Felder] | Diese Option filtert das Quellschema so, dass nur die Felder angezeigt werden, die bereits zugeordnet wurden. |
| [!UICONTROL Nicht zugeordnete Felder] | Diese Option filtert das Quellschema so, dass nur die Felder angezeigt werden, die noch zugeordnet werden müssen. |
| [!UICONTROL Felder mit Empfehlung] | Diese Option filtert das Quellschema so, dass nur die Felder angezeigt werden, die Zuordnungsempfehlungen enthalten. |

Auswählen **[!UICONTROL Felder mit Fehlern]** um alle Zuordnungssätze mit Fehlern anzuzeigen.

![filter](../images/ui/mapping/filter.png)

Eine isolierte Ansicht fehlerhafter Zuordnungssätze wird angezeigt, sodass Sie Fehler durch intelligente Zuordnungsempfehlungen oder durch die manuelle Zuordnungsstruktur beheben können.

![fields-with-errors](../images/ui/mapping/fields-with-errors.png)

### Neuen Feldtyp hinzufügen

Sie können ein neues Zuordnungsfeld oder ein berechnetes Feld hinzufügen, indem Sie **[!UICONTROL Neuer Feldtyp]**.

#### Neues Zuordnungsfeld

Um ein neues Zuordnungsfeld hinzuzufügen, wählen Sie **[!UICONTROL Neuer Feldtyp]** und wählen Sie **[!UICONTROL Neues Feld hinzufügen]** aus dem Dropdown-Menü, das angezeigt wird.

![add-new-field](../images/ui/mapping/add-new-field.png)

Wählen Sie als Nächstes das Quellfeld aus, das Sie hinzufügen möchten, und wählen Sie dann aus der angezeigten Quellschemastruktur aus. **[!UICONTROL Auswählen]**.

![select-new-field](../images/ui/mapping/select-new-field.png)

Die Zuordnungsschnittstelle wird mit dem ausgewählten Quellfeld und einem leeren Zielfeld aktualisiert. Auswählen **[!UICONTROL Zielfeld zuordnen]** , um das neue Quellfeld seinem entsprechenden Ziel-XDM-Feld zuzuordnen.

![map-target-field](../images/ui/mapping/map-target-field.png)

Eine interaktive Zielschemastruktur wird angezeigt, in der Sie manuell durch das Zielschema navigieren und das entsprechende Ziel-XDM-Feld für Ihr Quellfeld finden können.

![manuelles Mapping](../images/ui/mapping/manual-mapping.png)

Wenn Sie fertig sind, wählen Sie das Schemasymbol aus, um die Zielschemaschnittstelle zu schließen.

![schema-tree](../images/ui/mapping/schema-tree.png)

#### Berechnete Felder {#calculated-fields}

Berechnete Felder ermöglichen die Erstellung von Werten anhand der Attribute im Eingabeschema. Diese Werte können dann Attributen im Zielschema zugewiesen und mit einem Namen und einer Beschreibung versehen werden, um eine einfachere Referenz zu ermöglichen.

Um ein berechnetes Feld zu erstellen, wählen Sie **[!UICONTROL Neuer Feldtyp]** und wählen Sie **[!UICONTROL Berechnetes Feld hinzufügen]**

![add-calculated-field](../images/ui/mapping/add-calculated-field.png)

Das Bedienfeld **[!UICONTROL Berechnetes Feld erstellen]** wird angezeigt. Das linke Dialogfeld enthält die Felder, Funktionen und Operatoren, die in berechneten Feldern unterstützt werden. Wählen Sie eine der Registerkarten aus, um Funktionen, Felder oder Operatoren zum Ausdruckseditor hinzuzufügen.

| Tab | Beschreibung |
| --- | ----------- |
| [!UICONTROL Funktion] | Auf der Registerkarte „Funktionen“ werden die Funktionen aufgelistet, die zur Transformation der Daten verfügbar sind. Weitere Informationen zu den Funktionen, die Sie in berechneten Feldern verwenden können, finden Sie im Handbuch [Verwendung der Funktionen zur Datenvorbereitung (Mapper)](../functions.md). |
| [!UICONTROL Feld] | Auf der Registerkarte „Felder“ werden die im Quellschema verfügbaren Felder und Attribute aufgelistet. |
| [!UICONTROL Operator] | Auf der Registerkarte „Operatoren“ werden die zur Transformation der Daten verfügbaren Operatoren aufgelistet. |

![Tabs](../images/ui/mapping/tabs.png)

Mithilfe des Ausdruckseditors in der Mitte können Sie manuell Felder, Funktionen und Operatoren hinzufügen. Wählen Sie den Editor aus, um mit der Erstellung eines Ausdrucks zu beginnen. Nachdem Sie fertig sind, wählen Sie **[!UICONTROL Speichern]** um fortzufahren.

![create-calculated-field](../images/ui/mapping/create-calculated-field.png)

Auswählen **[!UICONTROL Datenvorschau]** , um die Zuordnungsergebnisse von bis zu 100 Zeilen mit Beispieldaten aus dem ausgewählten Datensatz anzuzeigen.

![preview-data](../images/ui/mapping/preview-data.png)

Während der Vorschau wird die Identitätsspalte als erstes Feld priorisiert, da dies die wichtigsten Informationen ist, die bei der Validierung der Zuordnungsergebnisse erforderlich sind. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Schließen]**.

![preview-screen](../images/ui/mapping/preview-screen.png)

Um alle Zuordnungssätze zu entfernen, wählen Sie **[!UICONTROL Alle Zuordnungen löschen]**.

![clear-all](../images/ui/mapping/clear-all.png)

### Zuordnungsschnittstelle verwenden

Platform bietet automatisch intelligente Empfehlungen für automatisch zugeordnete Felder, die auf dem von Ihnen ausgewählten Zielschema oder Datensatz basieren. Sie können die Zuordnungsregeln manuell an Ihre Anwendungsfälle anpassen oder doppelte Zuordnungssätze korrigieren, um Fehler zu löschen.

![mapping-interface](../images/ui/mapping/mapping-interface.png)

Wählen Sie das Glühbirnensymbol im Zielfeld aus, das Sie anpassen möchten.

![mapping-recc](../images/ui/mapping/mapping-recc.png)

Die [!UICONTROL Zuordnen von Empfehlungen] wird ein Popupfenster mit einer Liste empfohlener Zielfelder angezeigt, die einem bestimmten Quellfeld zugeordnet werden können. Standardmäßig wird die erste Empfehlung automatisch angewendet.

Manchmal ist mehr als eine Empfehlung für das Quellschema verfügbar. In diesem Fall zeigt die Zuordnungskarte die auffälligste Empfehlung an, gefolgt von einem Symbol, das die Anzahl der verfügbaren zusätzlichen Empfehlungen enthält. Durch Auswahl des Glühbirnensymbols wird eine Liste der zusätzlichen Empfehlungen angezeigt. Sie können eine der alternativen Empfehlungen auswählen, indem Sie das Kontrollkästchen neben der Empfehlung aktivieren, der Sie die Empfehlung zuordnen möchten.

Von hier aus können Sie das ausgewählte Zielfeld ändern, um einen Fehler zu beheben oder Ihrem Anwendungsfall zu entsprechen.

Alternativ können Sie **[!UICONTROL Manuell auswählen]** , um die interaktive Struktur für die Zielschema-Zuordnung manuell zu verwenden.

![recc-panel](../images/ui/mapping/recc-panel.png)

Die Benutzeroberfläche für die Zielschemazuordnung wird in derselben Ansicht wie die Zuordnungssets angezeigt, sodass Sie die Zuordnungspaare im selben Bildschirm ändern können. Wählen Sie das Zielfeld aus, das Ihrem Anwendungsfall entspricht oder Ihre Fehler behebt.

![select-target-field](../images/ui/mapping/select-target-field.png)

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Beenden]** um fortzufahren.

![Beenden](../images/ui/mapping/finish.png)

## Nächste Schritte

Durch Lesen dieses Dokuments haben Sie mithilfe der Zuordnungsschnittstelle in der Platform-Benutzeroberfläche erfolgreich eine CSV-Datei einem Ziel-XDM-Schema zugeordnet. Weiterführende Informationen finden Sie in folgenden Dokumenten:

* [Datenvorbereitung – Übersicht](../home.md)
* [Quellen – Übersicht](../../sources/home.md)
* [Überwachen von Datenflüssen aus Quellen in der Benutzeroberfläche](../../dataflows/ui/monitor-sources.md)
