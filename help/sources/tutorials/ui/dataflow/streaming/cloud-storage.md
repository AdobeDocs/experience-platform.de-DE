---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Konfigurieren eines Datenflusses für einen Cloud-Datenspeicherung-Streaming-Connector in der Benutzeroberfläche
topic: overview
translation-type: tm+mt
source-git-commit: 168ac3a3ab9f475cb26dc8138cbc90a3e35c836d
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 11%

---


# Konfigurieren eines Datenflusses für einen Cloud-Datenspeicherung-Streaming-Connector in der Benutzeroberfläche

Ein Datennachweis ist eine geplante Aufgabe, mit der Daten aus einer Quelle abgerufen und in einen [!DNL Platform] Datensatz aufgenommen werden. In diesem Lernprogramm werden die Schritte zum Konfigurieren eines neuen Datenflusses mit Ihrem Cloud-Datenspeicherung-Basisanschluss beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [XDM-System (Experience-Datenmodell)](../../../../../xdm/home.md)[!DNL Experience Platform]: Das standardisierte Framework, nach dem Daten zum Kundenerlebnis in organisiert werden.
   - [Grundlagen zum Aufbau von Schemas](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   - [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
- [Echtzeit-Kundenprofil](../../../../../profile/home.md): Ein durch die Zusammenführung von Daten aus verschiedenen Quellen erstelltes Profil, das eine zentrale Echtzeit-Sicht auf Kunden liefert.

Darüber hinaus müssen Sie bei diesem Lernprogramm bereits einen Cloud-Datenspeicherung-Connector erstellt haben. Eine Liste von Übungen zum Erstellen verschiedener Cloud-Datenspeicherung-Connectors in der Benutzeroberfläche finden Sie in der Übersicht über die [Quellschnittstellen](../../../../home.md).

## Daten auswählen

Nachdem Sie den Cloud-Datenspeicherung-Connector erstellt haben, wird der Schritt Daten ** auswählen angezeigt, über den Sie eine Oberfläche zur Auswahl des Streams festlegen können, von dem Sie Daten streamen möchten.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-data.png)

## Zuordnen von Datenfeldern zu einem XDM-Schema

Der Schritt *Zuordnung* wird angezeigt und bietet eine interaktive Schnittstelle, um die Quelldaten einem [!DNL Platform] Datensatz zuzuordnen.

Wählen Sie einen Datensatz, in den eingehende Daten aufgenommen werden sollen. Sie können entweder einen vorhandenen Datensatz verwenden oder einen neuen erstellen.

**Vorhandenen Datensatz verwenden**

Um Daten in einen vorhandenen Datensatz zu erfassen, wählen Sie &quot;Vorhandenen Datensatz **[!UICONTROL verwenden]**&quot;und klicken Sie dann auf das Dataset-Symbol.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/use-existing-data.png)

The _Select dataset_ dialog appears. Suchen Sie den gewünschten Datensatz, wählen Sie ihn aus und klicken Sie dann auf **[!UICONTROL Weiter]**.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-existing-data.png)

**Verwenden eines neuen Datensatzes**

Um Daten in einen neuen Datensatz zu erfassen, wählen Sie &quot;Neuen Datensatz **[!UICONTROL erstellen]** &quot;und geben Sie einen Namen und eine Beschreibung für den Datensatz in die entsprechenden Felder ein. Wählen Sie dann das gewünschte Schema im Dropdown-Menü aus.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/use-new-dataset.png)

## Benennen des Datenflusses

Der Schritt *[!UICONTROL Datennachweis]* wird angezeigt, mit dem Sie einen Namen eingeben und eine kurze Beschreibung zu Ihrem neuen Datennachweis geben können.

Geben Sie Werte für den Datenfluss ein und klicken Sie auf **[!UICONTROL Weiter]**.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/name-your-dataflow.png)

### Überprüfen Sie Ihren Datenfluss

Der *Schritt zum Überprüfen* wird angezeigt, mit dem Sie Ihren neuen Datenpfad überprüfen können, bevor er erstellt wird. Details werden in den folgenden Kategorien gruppiert:

- *[!UICONTROL Quelldetails]*: Zeigt den Quelltyp und andere relevante Details zur Quelle an.
- *[!UICONTROL Angaben]* zur Zielgruppe: Zeigt, in welchen Datensatz die Quelldaten aufgenommen werden, einschließlich des Schemas, das der Datensatz einhält.

Klicken Sie nach Überprüfung des Datenflusses auf **[!UICONTROL Fertig stellen]** und lassen Sie die Erstellung des Datenflusses etwas Zeit.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/review.png)

## Überwachen und Löschen Ihres Datenflusses

Nachdem Sie den DataFlow für die Cloud-Datenspeicherung erstellt haben, können Sie die Daten überwachen, die über den Datenfluss aufgenommen werden. Weitere Informationen zum Überwachen und Löschen von Datenflüssen finden Sie im Lernprogramm zum [Überwachen von Datenflüssen](../../../../../ingestion/quality/monitor-data-flows.md).

## Nächste Schritte

In diesem Lernprogramm haben Sie erfolgreich einen Datenbogen erstellt, um Daten aus einer externen Cloud-Datenspeicherung einzubringen, und Einblicke in die Überwachung von Datensätzen erhalten. Eingehende Daten können nun von nachgelagerten [!DNL Platform] Diensten wie [!DNL Real-time Customer Profile] und [!DNL Data Science Workspace]genutzt werden. Weitere Informationen finden Sie in den folgenden Dokumenten:

- [Übersicht über das Echtzeit-Kundenprofil](../../../../../profile/home.md)
- [Übersicht über den Data Science Workspace](../../../../../data-science-workspace/home.md)

## Anhang

Die folgenden Abschnitte enthalten zusätzliche Informationen zum Arbeiten mit Quellschnittstellen.

### Datentaflow deaktivieren

Beim Erstellen eines Datenflusses wird dieser sofort aktiv und erfasst Daten gemäß dem festgelegten Zeitplan. Sie können einen aktiven Datenfeed jederzeit deaktivieren, indem Sie die unten stehenden Anweisungen befolgen.

Klicken Sie im Arbeitsbereich &quot; *[!UICONTROL Quellen]* &quot;auf die Registerkarte &quot; **[!UICONTROL Durchsuchen]** &quot;. Klicken Sie anschließend auf den Namen der Basisverbindung, die mit dem aktiven Datenpfad verknüpft ist, den Sie deaktivieren möchten.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/browse.png)

Die Seite &quot; *[!UICONTROL Quellseite]* &quot;wird angezeigt. Wählen Sie den aktiven Datenfluss aus der Liste aus, um die Spalte &quot; *Eigenschaften* &quot;auf der rechten Seite des Bildschirms mit der Schaltfläche &quot; **[!UICONTROL Aktiviert]** &quot;zu öffnen. Klicken Sie auf den Umschalter, um den Datenflug zu deaktivieren. Derselbe Umschalter kann verwendet werden, um einen Datenflug nach dessen Deaktivierung erneut zu aktivieren.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/disable-source.png)

### Aktivieren von Eingangsdaten für die [!DNL Profile] Bevölkerung

Eingehende Daten aus Ihrem Quellanschluss können zur Anreicherung und zum Ausfüllen Ihrer [!DNL Real-time Customer Profile] Daten verwendet werden. Weitere Informationen zum Ausfüllen Ihrer [!DNL Real-time Customer Profile] Daten finden Sie im Tutorial zur [Profil-Population](../../profile.md).
