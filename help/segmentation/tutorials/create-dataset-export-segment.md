---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Datensatzes zum Exportieren eines Segments für eine Audience
topic: tutorial
translation-type: tm+mt
source-git-commit: 6d24637dc6cc282f98288b6416e4a3b7cebe42ea
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 0%

---


# Erstellen eines Datensatzes zum Exportieren eines Segments für eine Audience

Mit der Adobe Experience Platform können Sie Kundenattribute ganz einfach in Audiencen segmentieren. Nachdem Segmente erstellt wurden, können Sie diese Audience in ein Dataset exportieren, in dem sie aufgerufen und bearbeitet werden kann. Damit der Export erfolgreich sein kann, muss der Datensatz ordnungsgemäß konfiguriert werden.

In diesem Lernprogramm werden die Schritte erläutert, die zum Erstellen eines Datensatzes erforderlich sind, der zum Exportieren eines Segments für Audiencen mithilfe der Experience Platform-Benutzeroberfläche verwendet werden kann.

Dieses Tutorial steht in direktem Zusammenhang zu den Schritten, die im Tutorial zur [Auswertung und zum Zugriff auf Segmentergebnisse](./evaluate-a-segment.md)beschrieben werden. In der Übung zum Auswerten eines Segments werden Schritte zum Erstellen eines Datensatzes mithilfe der Katalog-API beschrieben, während in dieser Übung die Schritte zum Erstellen eines Datensatzes mithilfe der Benutzeroberfläche der Experience Platform beschrieben werden.

## Erste Schritte

Um ein Segment zu exportieren, muss der Datensatz auf dem Schema XDM Individuelle Profil-Vereinigung basieren. Ein Vereinigung-Schema ist ein systemgeneriertes, schreibgeschütztes Schema, das die Felder aller Schema, die dieselbe Klasse besitzen, Aggregat, in diesem Fall die XDM Individual Profil-Klasse. Weitere Informationen zu Schemas der Vereinigung Ansicht finden Sie im Abschnitt zum [Echtzeit-Kundenmanagement im Schema Registry-Entwicklerhandbuch](../../xdm/schema/composition.md#union).

Klicken Sie zur Ansicht der Schemas der Vereinigung in der Benutzeroberfläche auf **Profile** in der linken Navigation und dann auf die Registerkarte *Vereinigung Schema* , wie unten dargestellt.

![Registerkarte &quot;Vereinigung Schema&quot;in der Experience Platform-Benutzeroberfläche](../images/tutorials/segment-export-dataset/union-schema-ui.png)


## Datenarbeitsbereich

Der Arbeitsbereich &quot;Datensätze&quot;in der Benutzeroberfläche der Experience Platform ermöglicht die Ansicht und Verwaltung aller Datensätze, die Ihr IMS-Unternehmen erstellt hat, sowie die Erstellung neuer Datensätze.

Klicken Sie zur Ansicht des Datensatzarbeitsbereichs in der linken Navigation auf **Datensätze** und dann auf die Registerkarte *Durchsuchen* . The datasets workspace contains a list of datasets, including columns showing *Name*, *Created* (date and time), *Source*, *Schema*, and *Last Batch Status*, as well as the date and time the dataset was *Last Updated*. Je nach Breite der einzelnen Spalten müssen Sie ggf. nach links oder rechts blättern, um alle Spalten anzuzeigen.

>[!NOTE] Klicken Sie auf das Filtersymbol neben der Suchleiste, um Filterfunktionen zu verwenden, um nur die für das Echtzeit-Kundenkonto aktivierten Datensätze Ansicht.

![Ansicht aller Datensätze](../images/tutorials/segment-export-dataset/datasets-workspace.png)

## Datensatz erstellen

Um einen Datensatz zu erstellen, klicken Sie in der oberen rechten Ecke des Datensatzarbeitsbereichs auf &quot;Datensatz **erstellen&quot;** .

![Klicken Sie auf Datensatz erstellen](../images/tutorials/segment-export-dataset/dataset-click-create.png)

Klicken Sie im Bildschirm &quot; *Datensatz* erstellen&quot;auf &quot;Datensatz aus Schema **** erstellen&quot;, um fortzufahren.

![Datenquelle auswählen](../images/tutorials/segment-export-dataset/create-dataset.png)

## XDM Individuelles Profil Vereinigung Schema auswählen

Um das XDM Individual Profil Vereinigung Schema zur Verwendung in Ihrem Dataset auszuwählen, suchen Sie im Bildschirm &quot;Schema *auswählen* &quot;das Schema &quot;XDM Individuelles Profil&quot;mit dem Typ &quot;Vereinigung&quot;.

Markieren Sie das Optionsfeld neben **XDM Individuelles Profil** und klicken Sie dann oben rechts auf **Weiter** .

![Schema auswählen](../images/tutorials/segment-export-dataset/select-schema.png)

## Dataset konfigurieren

Im Bildschirm &quot;Datensatz **konfigurieren** &quot;müssen Sie dem Datensatz einen *Namen* geben und möglicherweise auch eine *Beschreibung* des Datensatzes angeben.

**Hinweise zu Dataset-Namen:**
- Dataset-Namen sollten kurz und beschreibend sein, damit der Datensatz später leicht in der Bibliothek gefunden werden kann.
- Dataset-Namen müssen eindeutig sein, d. h. sie sollten auch so spezifisch sein, dass sie in Zukunft nicht wiederverwendet werden.
- Es empfiehlt sich, zusätzliche Informationen über den Datensatz mithilfe des Beschreibungsfelds bereitzustellen, da dies anderen Benutzern helfen kann, in Zukunft zwischen Datensätzen zu unterscheiden.

Sobald der Datensatz einen Namen und eine Beschreibung enthält, klicken Sie auf **Fertig stellen**.

![Dataset konfigurieren](../images/tutorials/segment-export-dataset/configure-dataset.png)

## Datenbestand-Aktivität

Es wurde jetzt ein leerer Datensatz erstellt und Sie wurden zur Registerkarte &quot; *Datenaset-Aktivität* &quot;im Arbeitsbereich &quot;Datasets&quot;zurückgeleitet. Sie sollten den Namen des Datensatzes in der oberen linken Ecke des Arbeitsbereichs sowie die Benachrichtigung anzeigen, dass keine Stapel hinzugefügt wurden. Dies ist zu erwarten, da Sie diesem Datensatz noch keine Stapel hinzugefügt haben.

Auf der rechten Seite des Datensatzarbeitsbereichs finden Sie die Registerkarte &quot; **Info** &quot;mit Informationen zu Ihrem neuen Datensatz, wie z. B. *DataSet-ID*, *Name*, *Beschreibung*, *Tabellenname*,Schema,Streaming- *Brief, DirektübertragungSource-* Archiv ****. Die Registerkarte &quot;Info&quot;enthält außerdem Informationen zum Zeitpunkt der *Erstellung* des Datensatzes und zum *Datum seiner letzten Änderung* .

Bitte beachten Sie die **Dataset-ID**, da dieser Wert erforderlich ist, um den Arbeitsablauf für den Segmentexport in der Audience abzuschließen.

![Datenbestand-Aktivität](../images/tutorials/segment-export-dataset/dataset-activity.png)

## Nächste Schritte

Nachdem Sie nun einen Datensatz auf Grundlage des Schemas XDM Individuelle Profil-Vereinigung erstellt haben, können Sie die **Dataset-ID** verwenden, um das Lernprogramm zum [Auswerten und Zugreifen auf Segmentergebnisse](./evaluate-a-segment.md) fortzusetzen.

Kehren Sie zu diesem Zeitpunkt zum Tutorial zu den ausgewerteten Segmentergebnissen zurück und nehmen Sie im Schritt [Generate XDM Individual Profils for Audience members](./evaluate-a-segment.md#generate-profiles-for-audience-members) den Schritt zum [Exportieren eines Segmentarbeitsablaufs](./evaluate-a-segment.md#export-a-segment) auf.
