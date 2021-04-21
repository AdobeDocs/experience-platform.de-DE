---
keywords: Experience Platform;Home;beliebte Themen;Cloud-Datenspeicherung-Connector;Cloud-Datenspeicherung
solution: Experience Platform
title: Konfigurieren eines Datenflusses für einen Cloud Datenspeicherung Streaming Connector in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
description: Ein Datennachweis ist eine geplante Aufgabe, mit der Daten aus einer Quelle abgerufen und in einen Platform-Datensatz aufgenommen werden. In diesem Lernprogramm werden die Schritte zum Konfigurieren eines neuen Datenflusses mit Ihrem Cloud-Datenspeicherung-Basisanschluss beschrieben.
exl-id: 75deead6-ef3c-48be-aed2-c43d1f432178
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 6%

---

# Konfigurieren eines Datenflusses für eine Cloud-Datenspeicherung-Streaming-Verbindung in der Benutzeroberfläche

Ein Datennachweis ist eine geplante Aufgabe, mit der Daten aus einer Quelle abgerufen und in einen [!DNL Platform]-Datensatz eingefügt werden. In diesem Lernprogramm werden die Schritte zum Konfigurieren eines neuen Datenflusses mit Ihrem Cloud-Datenspeicherung-Basisanschluss beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten  [!DNL Experience Platform] organisiert werden.
   - [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   - [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

Außerdem müssen Sie für dieses Lernprogramm bereits einen Cloud-Datenspeicherung-Connector erstellt haben. Eine Liste von Lernprogrammen zum Erstellen verschiedener Cloud-Datenspeicherung-Connectors in der Benutzeroberfläche finden Sie unter [Übersicht über die Quellschnittstellen](../../../../home.md).

## Daten auswählen

Nachdem Sie den Cloud-Datenspeicherung-Connector erstellt haben, wird der Schritt *Daten auswählen* angezeigt, auf dem Sie auswählen können, von welchem Stream Sie Daten streamen möchten.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-data.png)

## Zuordnen von Datenfeldern zu einem XDM-Schema

Der Schritt **[!UICONTROL Zuordnung]** wird angezeigt und stellt eine interaktive Schnittstelle bereit, um die Quelldaten einem [!DNL Platform]-Datensatz zuzuordnen.

Wählen Sie einen Datensatz, in den eingehende Daten aufgenommen werden sollen. Sie können entweder einen vorhandenen Datensatz verwenden oder einen neuen erstellen.

**Vorhandenen Datensatz verwenden**

Um Daten in einen vorhandenen Datensatz zu erfassen, wählen Sie **[!UICONTROL Vorhandenen Datensatz verwenden]** und klicken Sie dann auf das Dataset-Symbol.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/use-existing-data.png)

Das Dialogfeld **[!UICONTROL Datensatz auswählen]** wird angezeigt. Suchen Sie den gewünschten Datensatz, wählen Sie ihn aus und klicken Sie dann auf **[!UICONTROL Weiter]**.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-existing-data.png)

**Verwenden eines neuen Datensatzes**

Um Daten in einen neuen Datensatz zu erfassen, wählen Sie **[!UICONTROL Neuen Datensatz erstellen]** und geben Sie in die entsprechenden Felder einen Namen und eine Beschreibung für den Datensatz ein. Wählen Sie dann das gewünschte Schema im Dropdown-Menü aus.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/use-new-dataset.png)

## Benennen des Datenflusses

Der Schritt **[!UICONTROL Datentiefe]** wird angezeigt, mit dem Sie einen Namen eingeben und eine kurze Beschreibung zu Ihrem neuen Datenpfad geben können.

Geben Sie Werte für den Datenfluss ein und klicken Sie auf **[!UICONTROL Weiter]**.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/name-your-dataflow.png)

### Überprüfen Sie Ihren Datenfluss

Der Schritt **[!UICONTROL Überprüfen]** wird angezeigt, mit dem Sie Ihren neuen Datenpfad überprüfen können, bevor er erstellt wird. Details werden in den folgenden Kategorien gruppiert:

- **[!UICONTROL Quelldetails]**: Zeigt den Quelltyp und andere relevante Details zur Quelle an.
- **[!UICONTROL Angaben]** zur Zielgruppe: Zeigt, in welchen Datensatz die Quelldaten aufgenommen werden, einschließlich des Schemas, das der Datensatz einhält.

Klicken Sie nach Überprüfung Ihres Datenflusses auf **[!UICONTROL Fertig stellen]** und lassen Sie etwas Zeit für die Erstellung des Datenflusses zu.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/review.png)

## Überwachen und Löschen Ihres Datenflusses

Nachdem Sie den DataFlow für die Cloud-Datenspeicherung erstellt haben, können Sie die Daten überwachen, die über den Datenfluss aufgenommen werden. Weitere Informationen zum Überwachen und Löschen von Datenflüssen finden Sie im Tutorial zu [Überwachungsdataflows](../../../../../ingestion/quality/monitor-data-ingestion.md).

## Nächste Schritte

In diesem Lernprogramm haben Sie erfolgreich einen Datenbogen erstellt, um Daten aus einer externen Cloud-Datenspeicherung einzubringen, und Einblicke in die Überwachung von Datensätzen erhalten. Eingangsdaten können nun von nachgeschalteten [!DNL Platform]-Diensten wie [!DNL Real-time Customer Profile] und [!DNL Data Science Workspace] verwendet werden. Weitere Informationen finden Sie in den folgenden Dokumenten:

- [[!DNL Real-time Customer Profile] Übersicht](../../../../../profile/home.md)
- [[!DNL Data Science Workspace] Übersicht](../../../../../data-science-workspace/home.md)

## Anhang

Die folgenden Abschnitte enthalten zusätzliche Informationen zum Arbeiten mit Quellschnittstellen.

### Datentaflow deaktivieren

Beim Erstellen eines Datenflusses wird dieser sofort aktiv und erfasst Daten gemäß dem festgelegten Zeitplan. Sie können einen aktiven Datenfeed jederzeit deaktivieren, indem Sie die unten stehenden Anweisungen befolgen.

Klicken Sie im Arbeitsbereich **[!UICONTROL Quellen]** auf die Registerkarte **[!UICONTROL Durchsuchen]**. Klicken Sie anschließend auf den Namen der Verbindung, die mit dem aktiven Datenpfad verknüpft ist, den Sie deaktivieren möchten.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/browse.png)

Die Aktivität **[!UICONTROL Quelle]** wird angezeigt. Wählen Sie den aktiven Datenfluss aus der Liste aus, um die zugehörige Spalte **[!UICONTROL Properties]** auf der rechten Seite des Bildschirms zu öffnen, die die Umschalter **[!UICONTROL Enabled]** enthält. Klicken Sie auf den Umschalter, um den Datenflug zu deaktivieren. Derselbe Umschalter kann verwendet werden, um einen Datenflug nach dessen Deaktivierung erneut zu aktivieren.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/disable-source.png)

### Aktivieren von Eingangsdaten für [!DNL Profile] Population

Eingehende Daten aus Ihrem Quellanschluss können zur Anreicherung und zum Ausfüllen Ihrer [!DNL Real-time Customer Profile]-Daten verwendet werden. Weitere Informationen zum Ausfüllen der [!DNL Real-time Customer Profile]-Daten finden Sie im Lernprogramm [Profil population](../../profile.md).
