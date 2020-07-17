---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Datensatzes zum Exportieren eines Segments für eine Audience
topic: tutorial
translation-type: tm+mt
source-git-commit: cb6a2f91eb6c18835bd9542e5b66af4682227491
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 32%

---


# Erstellen eines Datensatzes zum Exportieren eines Segments für eine Audience

[!DNL Adobe Experience Platform] ermöglicht die einfache Segmentierung von Kundenattributen in Audiencen. Nachdem Segmente erstellt wurden, können Sie diese Audience in ein Dataset exportieren, in dem sie aufgerufen und bearbeitet werden kann. Damit der Export erfolgreich sein kann, muss der Datensatz ordnungsgemäß konfiguriert werden.

In diesem Lernprogramm werden die Schritte erläutert, die zum Erstellen eines Datensatzes erforderlich sind, der zum Exportieren eines Segments für Audiencen mithilfe der [!DNL Experience Platform] Benutzeroberfläche verwendet werden kann.

Dieses Tutorial steht in direktem Zusammenhang zu den Schritten, die im Tutorial zur [Auswertung und zum Zugriff auf Segmentergebnisse](./evaluate-a-segment.md)beschrieben werden. Im Tutorial zum Auswerten eines Segments werden Schritte zum Erstellen eines Datensatzes mithilfe der [!DNL Catalog Service] API beschrieben, während in diesem Tutorial die Schritte zum Erstellen eines Datensatzes mithilfe der [!DNL Experience Platform] Benutzeroberfläche beschrieben werden.

## Erste Schritte

Um ein Segment zu exportieren, muss der Datensatz auf dem Schema XDM Individuelle Profil-Vereinigung basieren. Ein Vereinigung-Schema ist ein systemgeneriertes, schreibgeschütztes Schema, das die Felder aller Schema, die dieselbe Klasse besitzen, Aggregat, in diesem Fall die XDM Individual Profil-Klasse. Weitere Informationen zu Schemas der Vereinigung Ansicht finden Sie im Abschnitt zum [Echtzeit-Kundenmanagement im Schema Registry-Entwicklerhandbuch](../../xdm/schema/composition.md#union).

Klicken Sie zur Ansicht der Schemas der Vereinigung in der Benutzeroberfläche auf **[!UICONTROL Profile]** in der linken Navigation und dann auf die Registerkarte **[!UICONTROL Vereinigung Schema]** , wie unten dargestellt.

![Registerkarte &quot;Vereinigung Schema&quot;in der Benutzeroberfläche der Experience Platform](../images/tutorials/segment-export-dataset/union-schema-ui.png)


## Arbeitsbereich „Datensätze“

The datasets workspace within the [!DNL Experience Platform] UI allows you to view and manage all of the datasets that your IMS organization has made, as well as create new ones.

Klicken Sie zur Ansicht des Datensatzarbeitsbereichs in der linken Navigation auf **[!UICONTROL Datensätze]** und dann auf die Registerkarte *[!UICONTROL Durchsuchen]* . The datasets workspace contains a list of datasets, including columns showing *[!UICONTROL Name]*, *[!UICONTROL Created]* (date and time), *[!UICONTROL Source]*, *[!UICONTROL Schema]*, and *[!UICONTROL Last Batch Status]*, as well as the date and time the dataset was *[!UICONTROL Last Updated]*. Je nach Breite der einzelnen Spalten müssen Sie ggf. nach links oder rechts blättern, um alle Spalten anzuzeigen.

>[!NOTE]
>
>Click on the filter icon next to the search bar to use filtering capabilities to view only those datasets enabled for [!DNL Real-time Customer Profile].

![Alle Datensätze anzeigen](../images/tutorials/segment-export-dataset/datasets-workspace.png)

## Datensatz erstellen

Um einen Datensatz zu erstellen, klicken Sie in der oberen rechten Ecke des Arbeitsbereichs „Datensätze“ auf **[!UICONTROL Datensatz erstellen]**.

![Klicken Sie auf Datensatz erstellen](../images/tutorials/segment-export-dataset/dataset-click-create.png)

Klicken Sie im Bildschirm &quot; *[!UICONTROL Datensatz]* erstellen&quot;auf &quot;Datensatz aus Schema **** erstellen&quot;, um fortzufahren.

![Datenquelle auswählen](../images/tutorials/segment-export-dataset/create-dataset.png)

## XDM Individuelles Profil Vereinigung Schema auswählen

Um das XDM Individual Profil Vereinigung Schema zur Verwendung in Ihrem Datensatz auszuwählen, suchen Sie im Bildschirm &quot;Schema[!UICONTROL auswählen]&quot;das Schema &quot;[!UICONTROL XDM Individuelles Profil]&quot;mit dem Typ &quot; *[!UICONTROL Vereinigung]* &quot;.

Markieren Sie das Optionsfeld neben **[!UICONTROL XDM Individuelles Profil]** und klicken Sie dann oben rechts auf **[!UICONTROL Weiter]** .

![Schema auswählen](../images/tutorials/segment-export-dataset/select-schema.png)

## Datensatz konfigurieren

Im Bildschirm **[!UICONTROL Datensatz konfigurieren]** müssen Sie dem Datensatz einen *[!UICONTROL Namen]* geben und möglicherweise auch eine *[!UICONTROL Beschreibung]* des Datensatzes hinzufügen.

**Hinweise zu Datensatznamen:**
- Datensatznamen sollten kurz und beschreibend sein, damit sich der Datensatz in der Bibliothek später leicht finden lässt.
- Datensatznamen müssen eindeutig sein, d. h. sie müssen spezifisch genug sein, damit sie in Zukunft nicht wiederverwendet werden.
- Es empfiehlt sich, mithilfe des Beschreibungsfelds zusätzliche Informationen zum Datensatz anzugeben, um anderen Benutzern in Zukunft dabei zu helfen, zwischen Datensätzen zu unterscheiden.

Sobald der Datensatz einen Namen und eine Beschreibung aufweist, klicken Sie auf **[!UICONTROL Fertig stellen]**.

![Datensatz konfigurieren](../images/tutorials/segment-export-dataset/configure-dataset.png)

## Datensatzaktivität

Es wurde nun ein leerer Datensatz erstellt und Sie befinden sich wieder auf der Registerkarte *[!UICONTROL Datensatzaktivität]* im Arbeitsbereich „Datensätze“.  Sie sollten oben links im Arbeitsbereich den Namen des Datensatzes sowie eine Benachrichtigung sehen, die Ihnen mitteilt, dass keine Batches hinzugefügt wurden. Das ist zu erwarten, da Sie dem Datensatz noch keine Batches hinzugefügt haben.

Auf der rechten Seite des Arbeitsbereichs „Datensätze“ finden Sie die Registerkarte **[!UICONTROL Informationen]** mit Informationen zu Ihrem neuen Datensatz, wie z. B. *[!UICONTROL Datensatz-ID]*, *[!UICONTROL Name]*, *[!UICONTROL Beschreibung]*, *[!UICONTROL Tabellenname]*, *[!UICONTROL Schema]*, *[!UICONTROL Streaming]* und *[!UICONTROL Quelle]*. The [!UICONTROL Info] tab also includes information about when the dataset was *[!UICONTROL Created]* and its *[!UICONTROL Last Modified]* date.

Bitte beachten Sie die **[!UICONTROL Dataset-ID]**, da dieser Wert erforderlich ist, um den Arbeitsablauf für den Segmentexport in der Audience abzuschließen.

![Datensatzaktivität](../images/tutorials/segment-export-dataset/dataset-activity.png)

## Nächste Schritte

Nachdem Sie nun einen Datensatz auf Grundlage des Schemas XDM Individuelle Profil-Vereinigung erstellt haben, können Sie die **[!UICONTROL Dataset-ID]** verwenden, um das Lernprogramm zum [Auswerten und Zugreifen auf Segmentergebnisse](./evaluate-a-segment.md) fortzusetzen.

Kehren Sie zu diesem Zeitpunkt zum Tutorial zu den ausgewerteten Segmentergebnissen zurück und nehmen Sie die [Generierung von Profilen für Audiencen](./evaluate-a-segment.md#generate-profiles) im Schritt zum Exportieren eines Segmentarbeitsablaufs auf.
