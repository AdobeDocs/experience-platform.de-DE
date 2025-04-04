---
title: Zuordnen einer CSV-Datei zu einem XDM-Schema mithilfe von KI-generierten Empfehlungen
description: In diesem Tutorial wird beschrieben, wie Sie eine CSV-Datei mithilfe von KI-generierten Empfehlungen einem XDM-Schema zuordnen.
exl-id: 1daedf0b-5a25-4ca5-ae5d-e9ee1eae9e4d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1179'
ht-degree: 64%

---

# Zuordnen einer CSV-Datei zu einem XDM-Schema mithilfe von KI-generierten Empfehlungen

>[!NOTE]
>
>Informationen zu den allgemein verfügbaren CSV-Zuordnungsfunktionen in Experience Platform finden Sie im Dokument [Zuordnen einer CSV-Datei zu einem vorhandenen Schema](./existing-schema.md).

Um CSV-Daten in [!DNL Adobe Experience Platform] aufzunehmen, müssen die Daten einem [!DNL Experience Data Model] (XDM)-Schema zugeordnet werden. Sie können die Zuordnung zu [einem vorhandenen Schema](./existing-schema.md) auswählen. Wenn Sie jedoch nicht genau wissen, welches Schema verwendet werden soll oder wie es strukturiert sein soll, können Sie dynamische Empfehlungen auf der Grundlage von ML-Modellen (maschinelles Lernen) in der Experience Platform-Benutzeroberfläche verwenden.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von [!DNL Experience Platform] voraus.

* [[!DNL Experience Data Model (XDM System)]](../../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten von [!DNL Experience Platform] organisiert werden.
   * Sie müssen mindestens das Konzept der [Verhalten in XDM](../../../xdm/home.md#data-behaviors) verstehen, damit Sie entscheiden können, ob Sie Ihre Daten einer [!UICONTROL Profil]-Klasse (Datensatzverhalten) oder einer [!UICONTROL ExperienceEvent]-Klasse (Zeitreihenverhalten) zuordnen.
* [Batch-Aufnahme](../../batch-ingestion/overview.md): Die Methode, mit der [!DNL Experience Platform] Daten aus vom Benutzer bereitgestellten Datendateien aufnimmt.
* [Adobe Experience Platform-Datenvorbereitung](../../batch-ingestion/overview.md): Eine Reihe von Funktionen, mit denen Sie aufgenommene Daten entsprechend zu XDM-Schemata zuordnen und transformieren können. Die Dokumentation von [Funktionen zur Datenvorbereitung](../../../data-prep/functions.md) ist speziell für die Schemazuordnung relevant.

## Angeben von Datenflussdetails

Klicken Sie in der Benutzeroberfläche von Experience Platform im linken Navigationsbereich auf **[!UICONTROL Quellen]**. Navigieren Sie in der **[!UICONTROL Katalog]**-Ansicht zur Kategorie **[!UICONTROL Lokales System]**. Wählen Sie unter **[!UICONTROL Lokaler Datei-Upload]** die Option **[!UICONTROL Daten hinzufügen]** aus.

![Der [!UICONTROL Quellen]-Katalog in der Experience Platform-Benutzeroberfläche, wobei [!UICONTROL Daten hinzufügen] unter [!UICONTROL Lokaler Datei-Upload] ausgewählt ist.](../../images/tutorials/map-csv-recommendations/local-file-upload.png)

Der Workflow **[!UICONTROL CSV-XDM-Schema zuordnen]** wird angezeigt, beginnend mit dem Schritt **[!UICONTROL Datenflussdetails]**.

Wählen Sie **[!UICONTROL Erstellen eines neuen Schemas mit ML-Empfehlungen]**, woraufhin neue Steuerelemente angezeigt werden. Wählen Sie die entsprechende Klasse für die CSV-Daten aus, die Sie zuordnen möchten ([!UICONTROL Profil] oder [!UICONTROL ExperienceEvent]). Sie können optional das Dropdown-Menü verwenden, um die relevante Branche für Ihr Unternehmen auszuwählen, oder Sie lassen es leer, wenn die vorhandenen Kategorien nicht auf Sie zutreffen. Wenn Ihr Unternehmen mit einem [B2B](../../../xdm/tutorials/relationship-b2b.md)-Modell (Business-to-Business) operiert, markieren Sie das Kontrollkästchen **[!UICONTROL B2B-Daten]**.

![Der Schritt [!UICONTROL Datenflussdetails], wobei die Option „ML-Empfehlung“ ausgewählt wurde. Als Klasse ist [!UICONTROL Profil] ausgewählt und als Branche [!UICONTROL Telekommunikation]](../../images/tutorials/map-csv-recommendations/select-class-and-industry.png)

Geben Sie von hier aus einen Namen für das Schema an, das aus den CSV-Daten erstellt wird, sowie einen Namen für den Ausgabedatensatz, der die unter diesem Schema aufgenommenen Daten enthält.

Bevor Sie fortfahren, können Sie optional die folgenden zusätzlichen Funktionen für den Datenfluss konfigurieren:

| Name eingeben | Beschreibung |
| --- | --- |
| [!UICONTROL Beschreibung] | Eine Beschreibung für den Datenfluss. |
| [!UICONTROL Fehlerdiagnose] | Wenn diese Option aktiviert ist, werden Fehlermeldungen für neu aufgenommene Batches generiert, die beim Abrufen des entsprechenden Batches in der [API](../../batch-ingestion/api-overview.md) angezeigt werden können. |
| [!UICONTROL Partielle Aufnahme] | Wenn diese Option aktiviert ist, werden gültige Datensätze für neue Batch-Daten innerhalb eines bestimmten Fehlerschwellenwerts aufgenommen. Mit diesem Schwellenwert können Sie den Prozentsatz der akzeptablen Fehler konfigurieren, ab dem der gesamte Batch fehlschlägt. |
| [!UICONTROL Datenflussdetails] | Geben Sie einen Namen und eine optionale Beschreibung für den Datenfluss ein, der die CSV-Daten in Experience Platform bringt. Dem Datenfluss wird beim Starten dieses Workflows automatisch ein Standardname zugewiesen. Das Ändern des Namens ist optional. |
| [!UICONTROL Warnhinweise] | Wählen Sie aus einer Liste von [Warnhinweisen innerhalb des Produkts](../../../observability/alerts/overview.md) diejenigen aus, die Sie bezüglich des Status des Datenflusses erhalten möchten, nachdem er initiiert wurde. |

{style="table-layout:auto"}

Wenn Sie mit der Konfiguration des Datenflusses fertig sind, klicken Sie auf **[!UICONTROL Weiter]**.

![Der Abschnitt [!UICONTROL Datenflussdetails] ist abgeschlossen.](../../images/tutorials/map-csv-recommendations/dataflow-detail-complete.png)

## Daten auswählen

Verwenden Sie im Schritt **[!UICONTROL Daten auswählen]** die linke Spalte, um Ihre CSV-Datei hochzuladen. Sie können auf **[!UICONTROL Dateien auswählen]** klicken, um ein Dateiexplorer-Dialogfeld zur Auswahl der Datei zu öffnen, oder Sie können die Datei direkt in die Spalte ziehen und dort ablegen.

![Die Schaltfläche [!UICONTROL Dateien auswählen] und der Drag-and-Drop-Bereich, die beide hervorgehoben sind, im Schritt [!UICONTROL Daten auswählen].](../../images/tutorials/map-csv-recommendations/upload-files.png)

Nach dem Hochladen der Datei wird ein Abschnitt mit Beispieldaten angezeigt, in dem die ersten zehn Zeilen der empfangenen Daten angezeigt werden, sodass Sie überprüfen können, ob die Daten korrekt hochgeladen wurden. Klicken Sie auf **[!UICONTROL Weiter]**, um fortzufahren.

![Beispieldatenzeilen werden im Arbeitsbereich gefüllt](../../images/tutorials/map-csv-recommendations/data-uploaded.png)

## Konfigurieren von Schemazuordnungen

Die ML-Modelle werden ausgeführt, um basierend auf Ihrer Datenfluss-Konfiguration und Ihrer hochgeladenen CSV-Datei ein neues Schema zu generieren. Wenn der Prozess abgeschlossen ist, werden im Schritt [!UICONTROL Zuordnung] Felder gefüllt, um die Zuordnungen für jedes einzelne Feld neben der vollständig navigierbaren Ansicht der generierten Schemastruktur anzuzeigen.

![Der Schritt [!UICONTROL Zuordnung] in der Benutzeroberfläche mit allen zugeordneten CSV-Feldern und der daraus resultierenden Schemastruktur.](../../images/tutorials/map-csv-recommendations/schema-generated.png)

>[!NOTE]
>
>Sie können während des Workflows für die Zuordnung von Quell- zu Zielfeldern alle Felder in Ihrem Schema anhand einer Vielzahl von Kriterien filtern. Das Standardverhalten besteht darin, alle zugeordneten Felder anzuzeigen. Um die angezeigten Felder zu ändern, klicken Sie auf das Filtersymbol neben dem Sucheingabefeld und wählen Sie aus den Dropdown-Optionen aus.<br> ![Die Zuordnungsphase des Workflows zur Erstellung von CSV- zu XDM-Schemata mit dem hervorgehobenen Filtersymbol und Dropdown-Menü.](../../images/tutorials/map-csv-recommendations/source-field-to-target-mapping-filter.png "Die Zuordnungsphase des Workflows zur Erstellung von CSV- zu XDM-Schemata mit dem hervorgehobenen Filtersymbol und Dropdown-Menü."){width="100" zoomable="yes"}

Von hier aus können Sie optional [die Feldzuordnungen bearbeiten](#edit-mappings) oder [die Feldergruppen ändern, denen sie zugeordnet sind](#edit-schema), je nach ihrem Bedarf. Wenn Sie zufrieden sind, klicken Sie auf **[!UICONTROL Beenden]**, um die Zuordnung abzuschließen und den zuvor konfigurierten Datenfluss zu starten. Die CSV-Daten werden in das System aufgenommen und basierend auf der generierten Schemastruktur in einen Datensatz eingefügt, der für nachgelagerte Experience Platform-Services nutzbar ist.

![Die ausgewählte Schaltfläche [!UICONTROL Beenden], was den CSV-Zuordnungsprozess abschließt.](../../images/tutorials/map-csv-recommendations/finish-mapping.png)

### Bearbeiten von Feldzuordnungen {#edit-mappings}

Verwenden Sie die Vorschau für die Feldzuordnung, um vorhandene Zuordnungen zu bearbeiten oder vollständig zu entfernen. Weitere Informationen zum Verwalten eines Zuordnungssatzes in der Benutzeroberfläche finden Sie im [Handbuch zur Benutzeroberfläche für die Datenvorbereitung und Zuordnung](../../../data-prep/ui/mapping.md#mapping-interface).

### Bearbeiten von Feldergruppen {#edit-field-groups}

Die CSV-Felder werden mithilfe von ML-Modellen automatisch vorhandenen XDM-Feldergruppen zugeordnet. Wenn Sie die Feldergruppe für ein bestimmtes CSV-Feld ändern möchten, wählen Sie **[!UICONTROL Bearbeiten]** neben der Schemastruktur aus.

![Die ausgewählte Schaltfläche [!UICONTROL Bearbeiten] neben der Schemastruktur.](../../images/tutorials/map-csv-recommendations/edit-schema-structure.png)

Ein Dialogfeld wird angezeigt, in dem Sie den Anzeigenamen, den Datentyp und die Feldergruppe für jedes Feld in der Zuordnung bearbeiten können. Klicken Sie auf das Bearbeitungssymbol (![Bearbeiten-Symbol](/help/images/icons/edit.png)) neben einem Quellfeld, um dessen Details in der rechten Spalte zu bearbeiten, bevor Sie **[!UICONTROL Anwenden]** auswählen.

![Die empfohlene Feldergruppe für ein Quellfeld, das geändert wird.](../../images/tutorials/map-csv-recommendations/select-schema-field.png)

Wenn Sie mit der Anpassung der Schemaempfehlungen für Ihre Quellfelder fertig sind, klicken Sie auf **[!UICONTROL Speichern]**, um die Änderungen anzuwenden.

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie eine CSV-Datei mithilfe von KI-generierten Empfehlungen einem XDM-Schema zuordnen, sodass Sie diese Daten durch Batch-Aufnahme in Experience Platform importieren können.

Schritte zum Zuordnen einer CSV-Datei zu einem vorhandenen Schema finden Sie im [Zuordnungs-Workflow für vorhandene Schemata](./existing-schema.md). Informationen zum Echtzeit-Streaming von Daten an Experience Platform über vordefinierte Quellverbindungen finden Sie im Abschnitt [Quellen - Übersicht](../../../sources/home.md).

Sie können auch Algorithmen des maschinellen Lernens (ML) verwenden, um **aus CSV-Beispieldaten ein Schema zu generieren**. Dieser Workflow erstellt automatisch ein neues Schema basierend auf der Struktur und dem Inhalt Ihrer CSV-Datei. Dieses neu erstellte Schema entspricht dem Format Ihrer Daten, um Zeit zu sparen und die Genauigkeit bei der Definition der Struktur, Felder und Datentypen für große komplexe Datensätze zu erhöhen. Weitere Informationen zu [ Workflow finden Sie ](../../../xdm/ui/ml-assisted-schema-creation.md) Handbuch zur Erstellung von XML-unterstützten Schemata .
