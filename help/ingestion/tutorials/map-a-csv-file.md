---
keywords: Experience Platform;Startseite;beliebte Themen;CSV zuordnen;CSV-Datei zuordnen;CSV-Datei xdm zuordnen;CSV xdm zuordnen;ui-Handbuch
solution: Experience Platform
title: Zuordnen einer CSV-Datei zu einem XDM-Schema
topic-legacy: tutorial
type: Tutorial
description: In diesem Tutorial wird beschrieben, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine CSV-Datei einem XDM-Schema zuordnen.
exl-id: 15f55562-269d-421d-ad3a-5c10fb8f109c
source-git-commit: 0e79d339ddc0301486ea3e53a3fd52877ff6a2c8
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 24%

---

# Zuordnen einer CSV-Datei zu einem XDM-Schema

Um CSV-Daten in [!DNL Adobe Experience Platform] zu erfassen, müssen die Daten einem [!DNL Experience Data Model] (XDM)-Schema zugeordnet sein. In diesem Tutorial wird beschrieben, wie Sie eine CSV-Datei mithilfe der [!DNL Platform]-Benutzeroberfläche einem XDM-Schema zuordnen.

Darüber hinaus enthält der Anhang zu diesem Tutorial weitere Informationen zur Verwendung von [Zuordnungsfunktionen](#mapping-functions).

## Erste Schritte

Dieses Tutorial setzt ein Verständnis der folgenden Komponenten von [!DNL Platform] voraus:

- [[!DNL Experience Data Model (XDM System)]](../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Platform] Kundenerlebnisdaten organisiert.
- [[!DNL Batch ingestion]](../batch-ingestion/overview.md): Die Methode, mit der Daten aus vom Benutzer bereitgestellten Datendateien  [!DNL Platform] erfasst werden.

Für dieses Tutorial müssen Sie außerdem bereits einen Datensatz erstellt haben, in den Sie Ihre CSV-Daten aufnehmen können. Anweisungen zum Erstellen eines Datensatzes in der Benutzeroberfläche finden Sie im [Tutorial zur Datenerfassung](./ingest-batch-data.md).

## Ziel auswählen

Melden Sie sich bei [[!DNL Adobe Experience Platform]](https://platform.adobe.com) an und wählen Sie dann **[!UICONTROL Workflows]** aus der linken Navigationsleiste aus, um auf den Arbeitsbereich **[!UICONTROL Workflows]** zuzugreifen.

Wählen Sie im Bildschirm **[!UICONTROL Workflows]** die Option **[!UICONTROL CSV dem XDM-Schema zuordnen]** unter dem Abschnitt **[!UICONTROL Datenerfassung]** aus und wählen Sie dann **[!UICONTROL Launch]**.

![](../images/tutorials/map-a-csv-file/workflows.png)

Der Workflow **[!UICONTROL CSV dem XDM-Schema zuordnen]** wird angezeigt, beginnend mit dem Schritt **[!UICONTROL Ziel]** . Wählen Sie einen Datensatz für eingehende Daten aus, die in aufgenommen werden sollen. Sie können entweder einen vorhandenen Datensatz verwenden oder einen neuen erstellen.

**Vorhandenen Datensatz verwenden**

Um Ihre CSV-Daten in einen vorhandenen Datensatz zu erfassen, wählen Sie **[!UICONTROL Vorhandenen Datensatz verwenden]** aus. Sie können entweder einen vorhandenen Datensatz mit der Suchfunktion abrufen oder durch Scrollen durch die Liste der vorhandenen Datensätze im Bereich blättern.

![](../images/tutorials/map-a-csv-file/use-existing-dataset.png)

Um Ihre CSV-Daten in einen neuen Datensatz zu erfassen, wählen Sie **[!UICONTROL Neuen Datensatz erstellen]** aus und geben Sie einen Namen und eine Beschreibung für den Datensatz in die bereitgestellten Felder ein. Wählen Sie ein Schema entweder mithilfe der Suchfunktion aus oder scrollen Sie durch die Liste der bereitgestellten Schemata. Wählen Sie **[!UICONTROL Weiter]** aus, um fortzufahren.

![](../images/tutorials/map-a-csv-file/create-new-dataset.png)

## Daten hinzufügen

Der Schritt **[!UICONTROL Daten hinzufügen]** wird angezeigt. Ziehen Sie Ihre CSV-Datei in den dafür vorgesehenen Bereich oder wählen Sie **[!UICONTROL Dateien auswählen]** aus, um Ihre CSV-Datei manuell einzugeben.

![](../images/tutorials/map-a-csv-file/add-data.png)

Der Abschnitt **[!UICONTROL Beispieldaten]** wird nach dem Hochladen der Datei mit den ersten zehn Datenzeilen angezeigt. Nachdem Sie bestätigt haben, dass die Daten erwartungsgemäß hochgeladen wurden, wählen Sie **[!UICONTROL Weiter]** aus.

![](../images/tutorials/map-a-csv-file/sample-data.png)

## Zuordnen von CSV-Feldern zu XDM-Schemafeldern

Der Schritt **[!UICONTROL Mapping]** wird angezeigt. Die Spalten der CSV-Datei werden unter **[!UICONTROL Quellfeld]** aufgelistet, wobei die entsprechenden XDM-Schemafelder unter **[!UICONTROL Zielfeld]** aufgeführt sind.

[!DNL Platform] stellt automatisch intelligente Empfehlungen für automatisch zugeordnete Felder basierend auf dem ausgewählten Zielschema oder Datensatz bereit. Sie können die Zuordnungsregeln manuell an Ihre Anwendungsfälle anpassen.

![](../images/tutorials/map-a-csv-file/mapping-with-suggestions.png)

Um alle automatisch generierenden Zuordnungswerte zu akzeptieren, aktivieren Sie das Kontrollkästchen &quot;[!UICONTROL Alle Zielfelder akzeptieren]&quot;.

![](../images/tutorials/map-a-csv-file/filled-mapping-with-suggestions.png)

Manchmal ist mehr als eine Empfehlung für das Quellschema verfügbar. In diesem Fall zeigt die Zuordnungskarte die auffälligste Empfehlung an, gefolgt von einem blauen Kreis, der die Anzahl der verfügbaren zusätzlichen Empfehlungen enthält. Durch Auswahl des Glühbirnensymbols wird eine Liste der zusätzlichen Empfehlungen angezeigt. Sie können eine der alternativen Empfehlungen auswählen, indem Sie das Kontrollkästchen neben der Empfehlung aktivieren, der Sie die Empfehlung zuordnen möchten.

![](../images/tutorials/map-a-csv-file/multiple-recommendations.png)

Alternativ können Sie Ihr Quellschema manuell Ihrem Zielschema zuordnen. Bewegen Sie den Mauszeiger über das Quellschema, das Sie zuordnen möchten, und wählen Sie dann das Pluszeichen aus.

![](../images/tutorials/map-a-csv-file/mapping-with-suggestions-and-buttons.png)

Das Popup **[!UICONTROL Quelle dem Zielfeld zuordnen]** wird angezeigt. Von hier aus können Sie auswählen, welches Feld Sie zuordnen möchten, gefolgt von **[!UICONTROL Speichern]**, um Ihre neue Zuordnung hinzuzufügen.

![](../images/tutorials/map-a-csv-file/manual-mapping.png)

Wenn Sie eine der Zuordnungen entfernen möchten, halten Sie den Mauszeiger über diese Zuordnung und wählen Sie dann das Minussymbol aus.

### Berechnetes Feld hinzufügen {#add-calculated-field}

Berechnete Felder ermöglichen die Erstellung von Werten anhand der Attribute im Eingabeschema. Diese Werte können dann Attributen im Zielschema zugewiesen und mit einem Namen und einer Beschreibung versehen werden, um eine einfachere Referenz zu ermöglichen.

Wählen Sie die Schaltfläche **[!UICONTROL Berechnetes Feld hinzufügen]** aus, um fortzufahren.

![](../images/tutorials/map-a-csv-file/add-calculated-field.png)

Das Bedienfeld **[!UICONTROL Berechnetes Feld erstellen]** wird angezeigt. Das linke Dialogfeld enthält die Felder, Funktionen und Operatoren, die in berechneten Feldern unterstützt werden. Wählen Sie eine der Registerkarten aus, um Funktionen, Felder oder Operatoren zum Ausdruckseditor hinzuzufügen.

![](../images/tutorials/map-a-csv-file/create-calculated-fields.png)

| Tab | Beschreibung |
| --------- | ----------- |
| Felder | Auf der Registerkarte „Felder“ werden die im Quellschema verfügbaren Felder und Attribute aufgelistet. |
| Funktionen | Auf der Registerkarte „Funktionen“ werden die Funktionen aufgelistet, die zur Transformation der Daten verfügbar sind. Weitere Informationen zu den Funktionen, die Sie in berechneten Feldern verwenden können, finden Sie im Handbuch [Verwendung der Funktionen zur Datenvorbereitung (Mapper)](../../data-prep/functions.md). |
| Operatoren | Auf der Registerkarte „Operatoren“ werden die zur Transformation der Daten verfügbaren Operatoren aufgelistet. |

Mithilfe des Ausdruckseditors in der Mitte können Sie manuell Felder, Funktionen und Operatoren hinzufügen. Wählen Sie den Editor aus, um mit der Erstellung eines Ausdrucks zu beginnen.

![](../images/tutorials/map-a-csv-file/create-calculated-field.png)

Wählen Sie **[!UICONTROL Speichern]** aus, um fortzufahren.

Der Zuordnungsbildschirm wird mit dem neu erstellten Quellfeld erneut angezeigt. Wenden Sie das entsprechende Zielfeld an und wählen Sie **[!UICONTROL Beenden]** aus, um die Zuordnung abzuschließen.

![](../images/tutorials/map-a-csv-file/new-calculated-field.png)

## Überwachen der Datenerfassung

Nachdem Ihre CSV-Datei zugeordnet und erstellt wurde, können Sie die Daten überwachen, die über sie erfasst werden. Weitere Informationen zur Überwachung der Datenerfassung finden Sie im Tutorial zur [Überwachung der Datenerfassung](../../ingestion/quality/monitor-data-ingestion.md).

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich eine flache CSV-Datei einem XDM-Schema zugeordnet und in [!DNL Platform] aufgenommen. Diese Daten können jetzt von nachgelagerten [!DNL Platform]-Diensten wie [!DNL Real-time Customer Profile] verwendet werden. Weitere Informationen finden Sie in der Übersicht zu [[!DNL Real-time Customer Profile]](../../profile/home.md) .
