---
keywords: Experience Platform; Startseite; beliebte Themen; Streaming; Cloud-Speicher-Connector; Cloud-Speicher
solution: Experience Platform
title: Erstellen eines Streaming-Datenflusses für eine Cloud-Speicherquelle in der Benutzeroberfläche
type: Tutorial
description: Ein Datenfluss ist eine geplante Aufgabe, die Daten aus einer Quelle abruft und in einen Platform-Datensatz aufnimmt. In diesem Tutorial werden Schritte zum Konfigurieren eines neuen Datenflusses mit Ihrem Cloud-Speicher-Basis-Connector beschrieben.
exl-id: 75deead6-ef3c-48be-aed2-c43d1f432178
source-git-commit: 6419ae7648a91dc7f9432281c1960beccc65bdb0
workflow-type: tm+mt
source-wordcount: '1071'
ht-degree: 23%

---

# Erstellen eines Streaming-Datenflusses für eine Cloud-Speicherquelle in der Benutzeroberfläche

Ein Datenfluss ist eine geplante Aufgabe, die Daten aus einer Quelle abruft und in einen Adobe Experience Platform-Datensatz aufnimmt. In diesem Tutorial werden Schritte zum Erstellen eines Streaming-Datenflusses für eine Cloud-Speicherquelle in der Benutzeroberfläche beschrieben.

Bevor Sie dieses Tutorial durchführen, müssen Sie zunächst eine gültige und authentifizierte Verbindung zwischen Ihrem Cloud-Speicher-Konto und Platform herstellen. Wenn Sie noch keine authentifizierte Verbindung haben, finden Sie in einem der folgenden Tutorials Informationen zum Authentifizieren Ihrer Streaming-Cloud-Speicher-Konten:

- [[!DNL Amazon Kinesis]](../../../ui/create/cloud-storage/kinesis.md)
- [[!DNL Azure Event Hubs]](../../../ui/create/cloud-storage/eventhub.md)
- [[!DNL Google PubSub]](../../../ui/create/cloud-storage/google-pubsub.md)

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [Datenflüsse](../../../../../dataflows/home.md): Datenflüsse sind eine Darstellung von Datenvorgängen, die Daten über Platform verschieben. Datenflüsse werden für verschiedene Dienste konfiguriert, von Quellen über [!DNL Identity Service] bis [!DNL Profile] und bis zu [!DNL Destinations].
- [Datenvorbereitung](../../../../../data-prep/home.md): Mit der Datenvorbereitung können Dateningenieure Daten dem Experience-Datenmodell (XDM) und aus ihm zuordnen, umwandeln und validieren. Die Datenvorbereitung wird als „Map“-Schritt in den Datenaufnahmemechanismen, einschließlich des Workflows der CSV-Aufnahme, angezeigt.
- [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   - [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   - [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

## Daten hinzufügen

>[!NOTE]
>
>Sie können für einen bestimmten Ereignis-Hub nur einen Datenfluss pro Konsumentengruppe erstellen.

Nach der Erstellung Ihrer Authentifizierung für Ihr Streaming-Cloud-Speicherkonto wird der Schritt **[!UICONTROL Daten auswählen]** angezeigt und bietet eine Oberfläche, über die Sie auswählen können, welcher Datenstrom Sie an Platform bringen.

- Der linke Teil der Benutzeroberfläche ist ein Browser, mit dem Sie die verfügbaren Datenströme in Ihrem Konto anzeigen können.
- Im rechten Bereich der Benutzeroberfläche können Sie eine Vorschau von bis zu 100 Zeilen mit Daten aus einer JSON-Datei anzeigen.

![interface](../../../../images/tutorials/dataflow/cloud-storage/streaming/interface.png)

Wählen Sie den gewünschten Datenstrom aus und klicken Sie dann auf **[!UICONTROL Datei auswählen]** , um ein Beispielschema hochzuladen.

>[!TIP]
>
>Wenn Ihre Daten XDM-konform sind, können Sie das Hochladen eines Beispielschemas überspringen und **[!UICONTROL Weiter]** auswählen, um fortzufahren.

![select-stream](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-stream.png)

Nach dem Hochladen des Schemas wird die Vorschau-Oberfläche aktualisiert, um eine Vorschau des hochgeladenen Schemas anzuzeigen. Über die Vorschau-Oberfläche können Sie den Inhalt und die Struktur einer Datei überprüfen. Sie können auch das Dienstprogramm [!UICONTROL Suchfeld] verwenden, um auf bestimmte Elemente innerhalb Ihres Schemas zuzugreifen.

Wenn Sie fertig sind, klicken Sie auf die Schaltfläche **[!UICONTROL Weiter]**.

![schema-preview](../../../../images/tutorials/dataflow/cloud-storage/streaming/schema-preview.png)

## Zuordnung

Der Schritt **[!UICONTROL Zuordnung]** wird angezeigt und bietet eine Schnittstelle zum Zuordnen der Quelldaten zu einem Platform-Datensatz.

Wählen Sie einen Datensatz aus, in den eingehende Daten aufgenommen werden sollen. Sie können entweder einen vorhandenen Datensatz verwenden oder einen neuen erstellen.

### Neuer Datensatz

Um Daten in einen neuen Datensatz zu erfassen, wählen Sie **[!UICONTROL Neuer Datensatz]** aus und geben Sie einen Namen und eine Beschreibung für den Datensatz in die bereitgestellten Felder ein. Um ein Schema hinzuzufügen, können Sie einen vorhandenen Schemanamen im Dialogfeld **[!UICONTROL Schema auswählen]** eingeben. Alternativ können Sie **[!UICONTROL Erweiterte Schemasuche]** auswählen, um nach einem geeigneten Schema zu suchen.

![new-dataset](../../../../images/tutorials/dataflow/cloud-storage/streaming/new-dataset.png)

Das Fenster [!UICONTROL Schema auswählen] wird angezeigt und enthält eine Liste der verfügbaren Schemas, aus denen Sie auswählen können. Wählen Sie ein Schema aus der Liste aus, um die rechte Leiste zu aktualisieren und Details anzuzeigen, die für das ausgewählte Schema spezifisch sind, einschließlich Informationen darüber, ob das Schema für [!DNL Profile] aktiviert ist.

Nachdem Sie das Schema, das Sie verwenden möchten, identifiziert und ausgewählt haben, wählen Sie **[!UICONTROL Fertig]** aus.

![select-schema](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-schema.png)

Die Seite [!UICONTROL Ziel-Datensatz] wird mit dem ausgewählten Schema aktualisiert, das als Teil des Datensatzes angezeigt wird. Während dieses Schritts können Sie Ihren Datensatz für [!DNL Profile] aktivieren und eine ganzheitliche Ansicht der Attribute und Verhaltensweisen einer Entität erstellen. Daten aus allen aktivierten Datensätzen werden in [!DNL Profile] aufgenommen und Änderungen werden angewendet, wenn Sie Ihren Datenfluss speichern.

Schalten Sie die Schaltfläche **[!UICONTROL Profildatensatz]** um, um Ihren Zieldatensatz für [!DNL Profile] zu aktivieren.

![new-profile](../../../../images/tutorials/dataflow/cloud-storage/streaming/new-profile.png)

### Vorhandener Datensatz

Um Daten in einen vorhandenen Datensatz zu erfassen, wählen Sie **[!UICONTROL Vorhandenen Datensatz]** und dann das Datensatzsymbol aus.

![existing-dataset](../../../../images/tutorials/dataflow/cloud-storage/streaming/existing-dataset.png)

Das Dialogfeld **[!UICONTROL Datensatz auswählen]** wird angezeigt und enthält eine Liste der verfügbaren Datensätze, aus denen Sie auswählen können. Wählen Sie einen Datensatz aus der Liste aus, um die rechte Leiste zu aktualisieren und Details anzuzeigen, die für den ausgewählten Datensatz spezifisch sind, einschließlich Informationen dazu, ob der Datensatz für [!DNL Profile] aktiviert werden kann.

Nachdem Sie den zu verwendenden Datensatz identifiziert und ausgewählt haben, wählen Sie **[!UICONTROL Fertig]** aus.

![select-dataset](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-dataset.png)

Nachdem Sie Ihren Datensatz ausgewählt haben, wählen Sie den Umschalter [!DNL Profile] aus, um Ihren Datensatz für [!DNL Profile] zu aktivieren.

![existing-profile](../../../../images/tutorials/dataflow/cloud-storage/streaming/existing-profile.png)

### Standardfelder zuordnen

Nachdem Ihr Datensatz und Ihr Schema erstellt wurden, wird die Benutzeroberfläche **[!UICONTROL Standard-Felder zuordnen]** angezeigt, über die Sie die Zuordnungsfelder für Ihre Daten manuell konfigurieren können.

>[!TIP]
>
>Platform bietet intelligente Empfehlungen für automatisch zugeordnete Felder, die auf dem ausgewählten Zielschema oder Datensatz basieren. Sie können die Zuordnungsregeln manuell an Ihre Anwendungsfälle anpassen.

Je nach Bedarf können Sie wahlweise Felder direkt zuordnen oder mithilfe von Datenvorbereitungsfunktionen Quelldaten transformieren, um berechnete oder anderweitig ermittelte Werte abzuleiten. Umfassende Schritte zur Verwendung der Zuordnungsoberfläche und der berechneten Felder finden Sie im Handbuch [Data Prep UI guide](../../../../../data-prep/ui/mapping.md).

Nachdem die Quelldaten zugeordnet wurden, wählen Sie **[!UICONTROL Weiter]** aus.

![Zuordnung](../../../../images/tutorials/dataflow/cloud-storage/streaming/mapping.png)

## Datenflussdetails

Der Schritt **[!UICONTROL Datenfluss-Detail]** wird angezeigt, in dem Sie einen Namen eingeben und eine kurze Beschreibung zu Ihrem neuen Datenfluss angeben können.

Geben Sie Werte für den Datenfluss ein und wählen Sie **[!UICONTROL Weiter]** aus.

![dataflow-detail](../../../../images/tutorials/dataflow/cloud-storage/streaming/dataflow-detail.png)

### Überprüfung

Der Schritt **[!UICONTROL Überprüfung]** wird angezeigt, sodass Sie Ihren neuen Datenfluss überprüfen können, bevor er hergestellt wird. Die Details lassen sich wie folgt kategorisieren:

- **[!UICONTROL Verbindung]**: Zeigt Ihren Kontonamen, den Typ der Quelle und andere spezifische Informationen zur verwendeten Streaming-Cloud-Speicherquelle an.
- **[!UICONTROL Datensatz- und Zuordnungsfelder zuweisen]**: Zeigt den Zieldatensatz und das Schema an, die Sie für Ihren Datenfluss verwenden.

Nachdem Sie Ihren Datenfluss überprüft haben, klicken Sie auf **[!UICONTROL Beenden]** und gewähren Sie etwas Zeit für die Erstellung des Datenflusses.

![überprüfen](../../../../images/tutorials/dataflow/cloud-storage/streaming/review.png)

## Überwachen und Löschen Ihres Datenflusses

Nachdem Ihr Streaming-Cloud-Speicher-Datenfluss erstellt wurde, können Sie die Daten überwachen, die über ihn erfasst werden. Weitere Informationen zum Überwachen und Löschen von Streaming-Datenflüssen finden Sie im Tutorial zum [Überwachen von Streaming-Datenflüssen](../../monitor-streaming.md) .

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich einen Datenfluss erstellt, um Daten von einer Cloud-Speicherquelle zu streamen. Eingehende Daten können jetzt von nachgelagerten Platform-Services wie [!DNL Real-Time Customer Profile] und [!DNL Data Science Workspace] verwendet werden. Weiterführende Informationen finden Sie in folgenden Dokumenten:

- [[!DNL Real-Time Customer Profile] – Übersicht](../../../../../profile/home.md)
- [[!DNL Data Science Workspace] – Übersicht](../../../../../data-science-workspace/home.md)