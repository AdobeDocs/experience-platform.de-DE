---
keywords: Experience Platform;home;popular topics;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;
solution: Experience Platform
title: Zuordnen einer CSV-Datei zu einem XDM-Schema
topic: tutorial
type: Tutorial
description: In diesem Lernprogramm wird beschrieben, wie Sie eine CSV-Datei mithilfe der Adobe Experience Platform-Benutzeroberfläche einem XDM-Schema zuordnen.
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 2%

---


# Zuordnen einer CSV-Datei zu einem XDM-Schema

In order to ingest CSV data into [!DNL Adobe Experience Platform], the data must be mapped to an [!DNL Experience Data Model] (XDM) schema. In diesem Lernprogramm wird beschrieben, wie Sie eine CSV-Datei einem XDM-Schema mithilfe der [!DNL Platform] Benutzeroberfläche zuordnen.

Darüber hinaus enthält der Anhang zu diesem Lernprogramm weitere Informationen zur Verwendung von [Zuordnungsfunktionen](#mapping-functions).

## Erste Schritte

This tutorial requires a working understanding of the following components of [!DNL Platform]:

- [[!DNL Experience Data Model (XDM-System)]](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten [!DNL Platform] organisiert werden.
- [[!DNL Batch ingestion]](../batch-ingestion/overview.md): Die Methode, mit der Daten aus vom Benutzer bereitgestellten Datendateien [!DNL Platform] erfasst werden.

Für dieses Lernprogramm müssen Sie außerdem bereits einen Datensatz zum Erfassen Ihrer CSV-Daten erstellt haben. Anweisungen zum Erstellen eines Datensatzes in der Benutzeroberfläche finden Sie im Lernprogramm [zur Datenerfassung](./ingest-batch-data.md).

## Ziel auswählen

Melden Sie sich bei [[!DNL Adobe Experience Platform]](https://platform.adobe.com) an und wählen Sie dann in der linken Navigationsleiste **[!UICONTROL Workflows]** aus, um auf den **[!UICONTROL Workflows]** Arbeitsbereich zuzugreifen.

Wählen Sie im **[!UICONTROL Workflows]** -Bildschirm unter &quot; **[!UICONTROL Datenaufnahme]** &quot;die Option &quot;CSV-Datei XDM-Schema **** zuordnen&quot;und wählen Sie dann &quot; **[!UICONTROL Starten]**&quot;aus.

![](../images/tutorials/map-a-csv-file/workflows.png)

Der Arbeitsablauf **[!UICONTROL CSV zu XDM-Schema]** zuordnen wird angezeigt, beginnend mit dem **[!UICONTROL Zielschritt]** . Wählen Sie einen Datensatz, in den eingehende Daten aufgenommen werden sollen. Sie können entweder einen vorhandenen Datensatz verwenden oder einen neuen erstellen.

**Vorhandenen Datensatz verwenden**

Um Ihre CSV-Daten in einen vorhandenen Datensatz zu erfassen, wählen Sie &quot;Vorhandenen Datensatz **[!UICONTROL verwenden&quot;]**. Sie können entweder einen vorhandenen Datensatz mit der Suchfunktion abrufen oder durch einen Bildlauf durch die Liste der vorhandenen Datensätze im Bedienfeld blättern.

![](../images/tutorials/map-a-csv-file/use-existing-dataset.png)

Um Ihre CSV-Daten in einen neuen Datensatz zu erfassen, wählen Sie &quot;Neuen Datensatz **[!UICONTROL erstellen]** &quot;und geben Sie in die entsprechenden Felder einen Namen und eine Beschreibung für den Datensatz ein. Wählen Sie ein Schema aus, indem Sie entweder die Suchfunktion verwenden oder indem Sie durch die Liste der bereitgestellten Schema blättern. Wählen Sie **[!UICONTROL Weiter]** , um fortzufahren.

![](../images/tutorials/map-a-csv-file/create-new-dataset.png)

## hinzufügen

Der Schritt **[!UICONTROL Daten hinzufügen]** wird angezeigt. Ziehen Sie die CSV-Datei in den vorgesehenen Bereich oder wählen Sie &quot;Dateien **[!UICONTROL auswählen]** &quot;, um die CSV-Datei manuell einzugeben.

![](../images/tutorials/map-a-csv-file/add-data.png)

Der Abschnitt **[!UICONTROL Beispieldaten]** wird nach dem Hochladen der Datei mit den ersten zehn Datenzeilen angezeigt. Nachdem Sie bestätigt haben, dass die Daten erwartungsgemäß hochgeladen wurden, wählen Sie &quot; **[!UICONTROL Weiter]**&quot;aus.

![](../images/tutorials/map-a-csv-file/sample-data.png)

## Zuordnen von CSV-Feldern zu XDM-Schema-Feldern

The **[!UICONTROL Mapping]** step appears. Die Spalten der CSV-Datei werden unter &quot; **[!UICONTROL Quellfeld]**&quot;aufgelistet, wobei die entsprechenden XDM-Schema-Felder unter &quot; **[!UICONTROL Zielgruppe-Feld]**&quot;aufgeführt werden. Die Felder für die nicht ausgewählte Zielgruppe sind rot markiert. Mit der Filterfeldoption können Sie die Liste der verfügbaren Quellfelder einschränken.

>[!TIP]
>
>[!DNL Platform] bietet intelligente Empfehlungen für automatisch zugeordnete Zielgruppen, die auf dem von Ihnen ausgewählten Schema oder Datensatz basieren. Sie können Zuordnungsregeln manuell an Ihre Anwendungsfälle anpassen.

Um eine CSV-Spalte einem XDM-Feld zuzuordnen, wählen Sie das Symbol Schema neben dem entsprechenden Spaltenfeld Zielgruppe aus.

![](../images/tutorials/map-a-csv-file/mapping.png)

Das Fenster Schema **[!UICONTROL auswählen]** wird angezeigt. Hier können Sie durch die Struktur des XDM-Schemas navigieren und das Feld suchen, dem Sie die CSV-Spalte zuordnen möchten. Klicken Sie auf ein XDM-Feld, um es auszuwählen, und klicken Sie dann auf **[!UICONTROL Auswählen]**.

![](../images/tutorials/map-a-csv-file/select-schema-field.png)

Nachdem Sie die Schritte für die verbleibenden nicht zugeordneten Quellfelder ausgeführt haben, wird der Bildschirm &quot; **[!UICONTROL Zuordnung]** &quot;erneut angezeigt, wobei das ausgewählte XDM-Feld nun unter &quot;Feld der **[!UICONTROL Zielgruppe&quot;angezeigt wird]**.

![](../images/tutorials/map-a-csv-file/field-mapped.png)

Beim Zuordnen von Feldern können Sie auch Funktionen zur Berechnung von Werten auf der Grundlage von Eingabequellenfeldern einschließen. Weitere Informationen finden Sie im Abschnitt [Zuordnungsfunktionen](#mapping-functions) im Anhang.

### hinzufügen berechnetes Feld

Berechnete Felder ermöglichen die Erstellung von Werten basierend auf den Attributen im Eingabe-Schema. Diese Werte können dann Attributen im Schema &quot;Zielgruppe&quot;zugewiesen und mit einem Namen und einer Beschreibung versehen werden, um eine einfachere Referenz zu ermöglichen.

Klicken Sie auf die Schaltfläche **[!UICONTROL HinzufügenFeld]** , um fortzufahren.

![](../images/tutorials/map-a-csv-file/add-calculate-field.png)

Das Bedienfeld &quot;Berechnetes Feld **[!UICONTROL erstellen&quot;]** wird angezeigt. Das linke Dialogfeld enthält die Felder, Funktionen und Operatoren, die in berechneten Feldern unterstützt werden. Wählen Sie eine der Registerkarten aus, um Beginn Funktionen, Felder oder Operatoren zum Ausdruck-Editor hinzuzufügen.

![](../images/tutorials/map-a-csv-file/create-calculated-fields.png)

| Tab | Beschreibung |
| --------- | ----------- |
| Felder | Auf der Registerkarte &quot;Felder&quot;werden die im Quell-Schema verfügbaren Felder und Attribute Liste. |
| Funktionen | Auf der Registerkarte &quot;Funktionen&quot;werden die verfügbaren Funktionen zum Transformieren der Daten Liste. |
| Operatoren  | Auf der Registerkarte &quot;Operatoren&quot;werden die Operatoren Liste, die zum Transformieren der Daten verfügbar sind. |

Mit dem Ausdruck-Editor in der Mitte können Sie Felder, Funktionen und Operatoren manuell hinzufügen. Wählen Sie den Editor aus, um einen Ausdruck zu erstellen.

![](../images/tutorials/map-a-csv-file/expression-editor.png)

Wählen Sie **[!UICONTROL Speichern]** , um fortzufahren.

Der Anzeigebereich &quot;Zuordnung&quot;wird mit dem neu erstellten Quellfeld erneut angezeigt. Wenden Sie das entsprechende Feld für die Zielgruppe an und wählen Sie &quot; **[!UICONTROL Fertig stellen]** &quot;, um die Zuordnung abzuschließen.

![](../images/tutorials/map-a-csv-file/new-field.png)

## Überwachen des Datenflusses

Nachdem die CSV-Datei zugeordnet und erstellt wurde, können Sie die Daten überwachen, die über sie aufgenommen werden. Weitere Informationen zur Überwachung von Datenflüssen finden Sie im Lernprogramm zur [Überwachung von Streaming-Datenflüssen](../../ingestion/quality/monitor-data-flows.md).

## Zuordnungsfunktionen verwenden

Um eine Funktion zu verwenden, geben Sie sie unter &quot; **[!UICONTROL Quellfeld]** &quot;mit entsprechender Syntax und Eingaben ein.

Um z. B. CSV-Felder für Stadt und Land zu verknüpfen und sie dem XDM-Feld für Stadt zuzuweisen, stellen Sie das Quellfeld auf `concat(city, ", ", county)`.

![](../images/tutorials/map-a-csv-file/mapping-function.png)

Weitere Informationen zum Zuordnen von Spalten zu XDM-Feldern finden Sie im Handbuch zur [Verwendung der Funktionen](../../data-prep/functions.md)&quot;Datenvorgabe&quot;(Mapper).

## Nächste Schritte

In diesem Tutorial haben Sie eine einfache CSV-Datei erfolgreich einem XDM-Schema zugeordnet und in [!DNL Platform]das sie eingefügt wurde. Diese Daten können nun von nachgelagerten [!DNL Platform] Diensten wie [!DNL Real-time Customer Profile]z. B. Weitere Informationen finden Sie in der Übersicht für [[!DNL Echtzeit-Kundendaten]](../../profile/home.md) .
