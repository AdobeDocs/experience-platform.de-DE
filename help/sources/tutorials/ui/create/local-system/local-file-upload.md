---
keywords: Experience Platform; Startseite; beliebte Themen; lokales System; Datei-Upload; CSV zuordnen; CSV-Datei zuordnen; CSV-Datei xdm zuordnen; CSV-Datei xdm zuordnen; Handbuch zu ui;
solution: Experience Platform
title: Erstellen eines Connectors für lokale Datei-Upload-Quelle in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie eine Quellverbindung für Ihr lokales System erstellen, um lokale Dateien auf Platform zu bringen.
exl-id: 9ce15362-c30d-40cc-9d9c-caa650579390
source-git-commit: 08805ed0d89d3d6908ddccdafda55d2f862e727e
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 8%

---

# Erstellen eines Quell-Connectors für den lokalen Datei-Upload über die Benutzeroberfläche

In diesem Tutorial werden die Schritte zum Erstellen eines Quell-Connectors für den lokalen Datei-Upload beschrieben, um mithilfe der Benutzeroberfläche lokale Dateien in Platform zu erfassen.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   * [Tutorial zum Schema Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemas mithilfe der Benutzeroberfläche des Schema-Editors erstellen.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

## Hochladen lokaler Dateien in Platform

Wählen Sie in der Platform-Benutzeroberfläche die Option **[!UICONTROL Quellen]** über die linke Navigationsleiste, um auf die [!UICONTROL Quellen] Arbeitsbereich. Die [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, für die Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Unter dem [!UICONTROL Lokales System] category, select **[!UICONTROL Lokaler Datei-Upload]** und wählen Sie **[!UICONTROL Daten hinzufügen]**.

![Katalog](../../../../images/tutorials/create/local/catalog.png)

### Vorhandenen Datensatz verwenden

Die [!UICONTROL Datenflussdetails] -Seite können Sie auswählen, ob Sie Ihre CSV-Daten in einen vorhandenen Datensatz oder in einen neuen Datensatz aufnehmen möchten.

Um Ihre CSV-Daten in einen vorhandenen Datensatz zu erfassen, wählen Sie **[!UICONTROL Vorhandener Datensatz]**. Sie können einen vorhandenen Datensatz entweder mit der [!UICONTROL Erweiterte Suche] oder durch Scrollen durch die Liste der vorhandenen Datensätze im Dropdown-Menü.

Geben Sie bei ausgewähltem Datensatz einen Namen für Ihren Datenfluss und eine optionale Beschreibung an.

Während dieses Vorgangs können Sie auch [!UICONTROL Fehlerdiagnose] und [!UICONTROL Partielle Erfassung]. [!UICONTROL Fehlerdiagnose] ermöglicht eine detaillierte Erzeugung von Fehlermeldungen für alle fehlerhaften Datensätze, die in Ihrem Datenfluss auftreten, während [!UICONTROL Partielle Erfassung] ermöglicht die Aufnahme von fehlerhaften Daten bis zu einem bestimmten Schwellenwert, den Sie manuell definieren. Siehe [partielle Batch-Erfassung - Übersicht](../../../../../ingestion/batch-ingestion/partial.md) für weitere Informationen.

![existing-dataset](../../../../images/tutorials/create/local/existing-dataset.png)

### Verwenden eines neuen Datensatzes

Um Ihre CSV-Daten in einen neuen Datensatz zu erfassen, wählen Sie **[!UICONTROL Neuer Datensatz]** und geben Sie dann einen Namen für den Ausgabedatensatz und eine optionale Beschreibung an. Wählen Sie als Nächstes ein Schema aus, das mithilfe des [!UICONTROL Erweiterte Suche] oder durch Scrollen durch die Liste der vorhandenen Schemas im Dropdown-Menü.

Geben Sie bei ausgewähltem Schema einen Namen für Ihren Datenfluss und eine optionale Beschreibung ein und wenden Sie dann die [!UICONTROL Fehlerdiagnose] und [!UICONTROL Partielle Erfassung] -Einstellungen, die Sie für Ihren Datenfluss benötigen. Wenn Sie fertig sind, klicken Sie auf **[!UICONTROL Weiter]**.

![new-dataset](../../../../images/tutorials/create/local/new-dataset.png)

### Daten auswählen

Die [!UICONTROL Daten auswählen] -Schritt angezeigt werden. Sie erhalten eine Oberfläche zum Hochladen Ihrer lokalen Dateien und zur Vorschau ihrer Struktur und Inhalte. Auswählen **[!UICONTROL Dateien auswählen]** , um eine CSV-Datei von Ihrem lokalen System hochzuladen. Alternativ können Sie die CSV-Datei, die Sie hochladen möchten, per Drag-and-Drop in die [!UICONTROL Dateien per Drag &amp; Drop verschieben] Bereich.

>[!TIP]
>
>Derzeit werden nur CSV-Dateien vom lokalen Datei-Upload unterstützt. Die maximale Dateigröße pro Datei beträgt 1 GB.

![choice-files](../../../../images/tutorials/create/local/choose-files.png)

Nach dem Hochladen Ihrer Datei wird die Vorschau-Oberfläche aktualisiert, um Inhalt und Struktur der Datei anzuzeigen.

![preview-sample-data](../../../../images/tutorials/create/local/preview-sample-data.png)

Je nach Datei können Sie ein Spaltentrennzeichen wie Tabulatoren, Kommas, senkrechte Striche oder ein benutzerdefiniertes Spaltentrennzeichen für die Quelldaten auswählen. Wählen Sie die **[!UICONTROL Trennzeichen]** Dropdown-Pfeil und wählen Sie dann das entsprechende Trennzeichen aus dem Menü aus.

Wenn Sie fertig sind, klicken Sie auf **[!UICONTROL Weiter]**.

![delimiter](../../../../images/tutorials/create/local/delimiter.png)

## Zuordnung

Die [!UICONTROL Zuordnung] -Schritt angezeigt werden. Sie erhalten eine Schnittstelle, über die Sie die Quellfelder aus Ihrem Quellschema den entsprechenden Ziel-XDM-Feldern im Zielschema zuordnen können.

Je nach Bedarf können Sie Felder direkt zuordnen oder mithilfe von Datenvorbereitungsfunktionen Quelldaten transformieren, um berechnete oder berechnete Werte abzuleiten. Umfassende Schritte zur Verwendung der Zuordnungsschnittstelle finden Sie in der [Handbuch zur Datenvorbereitung-Benutzeroberfläche](../../../../../data-prep/ui/mapping.md).

Sobald Ihre Zuordnungssätze fertig sind, wählen Sie **[!UICONTROL Beenden]** und lassen einige Momente zu, damit der neue Datenfluss erstellt wird.

![Mapping](../../../../images/tutorials/create/local/mapping.png)

## Überwachen der Datenerfassung

Nachdem Ihre CSV-Datei zugeordnet und erstellt wurde, können Sie die über sie erfassten Daten mithilfe des Monitoring-Dashboards überwachen. Weitere Informationen finden Sie im Tutorial zu [Überwachen von Datenflüssen aus Quellen in der Benutzeroberfläche](../../../../../dataflows/ui/monitor-sources.md).

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich eine flache CSV-Datei einem XDM-Schema zugeordnet und in Platform aufgenommen. Diese Daten können jetzt nachgelagert verwendet werden [!DNL Platform] Dienste wie [!DNL Real-time Customer Profile]. Siehe Übersicht für [[!DNL Real-time Customer Profile]](../../../../../profile/home.md) für weitere Informationen.
