---
keywords: Experience Platform;Startseite;beliebte Themen;Streaming;Cloud-Speicher-Connector;Cloud-Speicher
solution: Experience Platform
title: Erstellen eines Streaming-Datenflusses für eine Cloud-Speicherquelle in der Benutzeroberfläche
type: Tutorial
description: Ein Datenfluss ist eine geplante Aufgabe, mit der Daten aus einer Quelle abgerufen und in einen Experience Platform-Datensatz aufgenommen werden. In diesem Tutorial finden Sie die Schritte zum Konfigurieren eines neuen Datenflusses mithilfe Ihres Cloud-Speicher-Basis-Connectors.
exl-id: 75deead6-ef3c-48be-aed2-c43d1f432178
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1078'
ht-degree: 20%

---

# Erstellen eines Streaming-Datenflusses für eine Cloud-Speicherquelle in der Benutzeroberfläche

Ein Datenfluss ist eine geplante Aufgabe, mit der Daten aus einer Quelle abgerufen und in einen Adobe Experience Platform-Datensatz aufgenommen werden. In diesem Tutorial werden Schritte zum Erstellen eines Streaming-Datenflusses für eine Cloud-Speicherquelle in der Benutzeroberfläche beschrieben.

Bevor Sie dieses Tutorial durchführen können, müssen Sie zunächst eine gültige und authentifizierte Verbindung zwischen Ihrem Cloud-Speicherkonto und Experience Platform herstellen. Wenn Sie noch keine authentifizierte Verbindung haben, finden Sie in einem der folgenden Tutorials Informationen zum Authentifizieren Ihrer Streaming-Cloud-Speicherkonten:

- [[!DNL Amazon Kinesis]](../../../ui/create/cloud-storage/kinesis.md)
- [[!DNL Azure Event Hubs]](../../../ui/create/cloud-storage/eventhub.md)
- [[!DNL Google PubSub]](../../../ui/create/cloud-storage/google-pubsub.md)

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [Datenflüsse](../../../../../dataflows/home.md): Datenflüsse sind eine Darstellung von Datenvorgängen, die Daten über Experience Platform verschieben. Datenflüsse werden über verschiedene Services konfiguriert, von Quellen über [!DNL Identity Service] zu [!DNL Profile] und [!DNL Destinations].
- [Datenvorbereitung](../../../../../data-prep/home.md): Die Datenvorbereitung ermöglicht es Dateningenieuren, Daten dem Experience-Datenmodell (XDM) zuzuordnen, umzuformen und zu validieren. Die Datenvorbereitung wird als „Map“-Schritt in den Datenaufnahmemechanismen, einschließlich des Workflows der CSV-Aufnahme, angezeigt.
- [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   - [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   - [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

## Daten hinzufügen

>[!NOTE]
>
>Pro Verbrauchergruppe kann für einen bestimmten Event Hub nur ein Quelldatenfluss erstellt werden.

Nachdem Sie Ihr Streaming-Cloud-Speicherkonto authentifiziert haben, wird der Schritt **[!UICONTROL Daten auswählen]** angezeigt, in dem Sie über eine Oberfläche auswählen können, welchen Datenstrom Sie an Experience Platform senden möchten.

- Der linke Teil der Benutzeroberfläche ist ein Browser, mit dem Sie die verfügbaren Datenströme in Ihrem Konto anzeigen können.
- Im rechten Teil der Benutzeroberfläche können Sie eine Vorschau von bis zu 100 Datenzeilen aus einer JSON-Datei anzeigen.

![Schnittstelle](../../../../images/tutorials/dataflow/cloud-storage/streaming/interface.png)

Wählen Sie den zu verwendenden Datenstrom aus und wählen Sie dann **[!UICONTROL Datei auswählen]** aus, um ein Beispielschema hochzuladen.

>[!TIP]
>
>Wenn Ihre Daten XDM-kompatibel sind, können Sie das Hochladen eines Beispielschemas überspringen und auf **[!UICONTROL Weiter]** klicken, um fortzufahren.

![select-stream](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-stream.png)

Nachdem Ihr Schema hochgeladen wurde, wird die Vorschau-Oberfläche aktualisiert, um eine Vorschau des hochgeladenen Schemas anzuzeigen. In der Vorschauoberfläche können Sie den Inhalt und die Struktur einer Datei überprüfen. Sie können auch das Dienstprogramm [!UICONTROL Suchfeld] verwenden, um innerhalb Ihres Schemas auf bestimmte Elemente zuzugreifen.

Wenn Sie fertig sind, klicken Sie auf die Schaltfläche **[!UICONTROL Weiter]**.

![schema-preview](../../../../images/tutorials/dataflow/cloud-storage/streaming/schema-preview.png)

## Zuordnung

Der **[!UICONTROL Zuordnungsschritt]** wird angezeigt und stellt eine Schnittstelle zum Zuordnen der Quelldaten zu einem Experience Platform-Datensatz bereit.

Wählen Sie einen Datensatz aus, in den eingehende Daten aufgenommen werden sollen. Sie können entweder einen vorhandenen Datensatz verwenden oder einen neuen erstellen.

### Neuer Datensatz

Um Daten in einen neuen Datensatz aufzunehmen, wählen Sie **[!UICONTROL Neuer Datensatz]** und geben Sie einen Namen und eine Beschreibung für den Datensatz in die entsprechenden Felder ein. Um ein Schema hinzuzufügen, können Sie einen vorhandenen Schemanamen im Dialogfeld **[!UICONTROL Schema auswählen]** eingeben. Alternativ können Sie auf **[!UICONTROL Erweiterte Schemasuche]** klicken, um nach einem geeigneten Schema zu suchen.

![new-dataset](../../../../images/tutorials/dataflow/cloud-storage/streaming/new-dataset.png)

Das Fenster [!UICONTROL Schema auswählen] wird angezeigt, in dem eine Liste der verfügbaren Schemata zur Auswahl steht. Wählen Sie ein Schema aus der Liste aus, um die rechte Leiste zu aktualisieren und Details anzuzeigen, die für das ausgewählte Schema spezifisch sind, einschließlich Informationen darüber, ob das Schema für die [!DNL Profile] aktiviert ist.

Nachdem Sie das gewünschte Schema identifiziert und ausgewählt haben, klicken Sie auf **[!UICONTROL Fertig]**.

![select-schema](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-schema.png)

Die Seite [!UICONTROL Zieldatensatz] wird mit Ihrem ausgewählten Schema aktualisiert, das als Teil des Datensatzes angezeigt wird. In diesem Schritt können Sie Ihren Datensatz für die [!DNL Profile] aktivieren und eine ganzheitliche Ansicht der Attribute und Verhaltensweisen einer Entität erstellen. Daten aus allen aktivierten Datensätzen werden in [!DNL Profile] eingeschlossen und Änderungen werden angewendet, wenn Sie Ihren Datenfluss speichern.

Schalten Sie die Schaltfläche **[!UICONTROL Profildatensatz]** um, um Ihren Zieldatensatz für die [!DNL Profile] zu aktivieren.

![new-profile](../../../../images/tutorials/dataflow/cloud-storage/streaming/new-profile.png)

### Vorhandener Datensatz

Um Daten in einen vorhandenen Datensatz aufzunehmen, wählen Sie **[!UICONTROL Vorhandener Datensatz]** und dann das Datensatzsymbol aus.

![existing-dataset](../../../../images/tutorials/dataflow/cloud-storage/streaming/existing-dataset.png)

Das **[!UICONTROL Datensatz auswählen]** wird angezeigt und enthält eine Liste der verfügbaren Datensätze. Wählen Sie einen Datensatz aus der Liste aus, um die rechte Leiste zu aktualisieren und Details anzuzeigen, die für den ausgewählten Datensatz spezifisch sind, einschließlich Informationen dazu, ob der Datensatz für die [!DNL Profile] aktiviert werden kann.

Nachdem Sie den zu verwendenden Datensatz identifiziert und ausgewählt haben, klicken Sie auf **[!UICONTROL Fertig]**.

![select-dataset](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-dataset.png)

Nachdem Sie Ihren Datensatz ausgewählt haben, klicken Sie auf den Umschalter [!DNL Profile] , um Ihren Datensatz für die [!DNL Profile] zu aktivieren.

![existing-profile](../../../../images/tutorials/dataflow/cloud-storage/streaming/existing-profile.png)

### Standardfelder zuordnen

Nachdem Sie Ihren Datensatz und Ihr Schema eingerichtet haben, wird **[!UICONTROL Schnittstelle „Standardfelder zuordnen]** angezeigt, über die Sie Zuordnungsfelder für Ihre Daten manuell konfigurieren können.

>[!TIP]
>
>Experience Platform bietet intelligente Empfehlungen für automatisch zugeordnete Felder, die auf dem ausgewählten Zielschema oder Datensatz basieren. Sie können die Zuordnungsregeln manuell an Ihre Anwendungsfälle anpassen.

Je nach Bedarf können Sie wahlweise Felder direkt zuordnen oder mithilfe von Datenvorbereitungsfunktionen Quelldaten transformieren, um berechnete oder anderweitig ermittelte Werte abzuleiten. Eine ausführliche Anleitung zur Verwendung der Zuordnungsschnittstelle und berechneter Felder finden Sie im [Handbuch zur Datenvorbereitungs-Benutzeroberfläche](../../../../../data-prep/ui/mapping.md).

Nachdem Ihre Quelldaten zugeordnet wurden, klicken Sie auf **[!UICONTROL Weiter]**.

![Zuordnung](../../../../images/tutorials/dataflow/cloud-storage/streaming/mapping.png)

## Datenflussdetails

Der Schritt **[!UICONTROL Datenflussdetails]** wird angezeigt, in dem Sie Ihren neuen Datenfluss benennen und kurz beschreiben können.

Geben Sie Werte für den Datenfluss an und wählen Sie **[!UICONTROL Weiter]**.

![dataflow-detail](../../../../images/tutorials/dataflow/cloud-storage/streaming/dataflow-detail.png)

### Überprüfung

Der Schritt **[!UICONTROL Überprüfung]** wird angezeigt, sodass Sie Ihren neuen Datenfluss überprüfen können, bevor er hergestellt wird. Die Details lassen sich wie folgt kategorisieren:

- **[!UICONTROL Verbindung]**: Zeigt Ihren Kontonamen, den Quelltyp und andere verschiedene Informationen an, die für die von Ihnen verwendete Streaming-Cloud-Speicherquelle spezifisch sind.
- **[!UICONTROL Datensatz zuweisen und Felder zuordnen]**: Zeigt den Zieldatensatz und das Schema an, die Sie für Ihren Datenfluss verwenden.

Nachdem Sie Ihren Datenfluss überprüft haben, klicken Sie auf **[!UICONTROL Beenden]** und gewähren Sie etwas Zeit für die Erstellung des Datenflusses.

![überprüfen](../../../../images/tutorials/dataflow/cloud-storage/streaming/review.png)

## Überwachen und Löschen des Datenflusses

Nachdem Ihr Streaming-Cloud-Speicher-Datenfluss erstellt wurde, können Sie die Daten überwachen, die über ihn aufgenommen werden. Weitere Informationen zum Überwachen und Löschen von Streaming-Datenflüssen finden Sie im Tutorial [Überwachen von Streaming-Datenflüssen](../../monitor-streaming.md).

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich einen Datenfluss erstellt, um Daten aus einer Cloud-Speicherquelle zu streamen. Eingehende Daten können jetzt von nachgelagerten Experience Platform-Services wie [!DNL Real-Time Customer Profile] und [!DNL Data Science Workspace] verwendet werden. Weiterführende Informationen finden Sie in folgenden Dokumenten:

- [[!DNL Real-Time Customer Profile] – Übersicht](../../../../../profile/home.md)
- [[!DNL Data Science Workspace] – Übersicht](../../../../../data-science-workspace/home.md)