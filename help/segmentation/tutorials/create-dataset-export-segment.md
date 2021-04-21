---
keywords: Experience Platform;Startseite;beliebte Themen;Segmentierungsdienst;Segmentierung;Segmentierung;Erstellen eines Datensatzes;Exportsegments für Audiencen;Exportsegment;
solution: Experience Platform
title: Erstellen eines Datensatzes zum Exportieren eines Segments für Audiencen
topic-legacy: tutorial
type: Tutorial
description: In diesem Lernprogramm werden die Schritte erläutert, die zum Erstellen eines Datensatzes erforderlich sind, der zum Exportieren eines Segments für Audiencen mithilfe der Benutzeroberfläche für Experience Platformen verwendet werden kann.
exl-id: 1cd16e43-b050-42ba-a894-d7ea477b65f3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 23%

---

# Erstellen eines Datensatzes zum Exportieren eines Segments für eine Audience

[!DNL Adobe Experience Platform] ermöglicht die einfache Segmentierung von Kundenattributen in Audiencen. Nachdem Segmente erstellt wurden, können Sie diese Audience in ein Dataset exportieren, in dem sie aufgerufen und bearbeitet werden kann. Damit der Export erfolgreich sein kann, muss der Datensatz ordnungsgemäß konfiguriert werden.

In diesem Lernprogramm werden die Schritte erläutert, die zum Erstellen eines Datensatzes erforderlich sind, der zum Exportieren eines Segments mit der Audience [!DNL Experience Platform] verwendet werden kann.

Dieses Tutorial steht in direktem Zusammenhang zu den Schritten, die im Tutorial für [Evaluierung und Zugriff auf Segmentergebnisse](./evaluate-a-segment.md) beschrieben werden. Das Evaluierungstraining für ein Segment enthält Schritte zum Erstellen eines Datensatzes mit der API [!DNL Catalog Service], während dieses Lernprogramm Schritte zum Erstellen eines Datensatzes mit der Oberfläche [!DNL Experience Platform] beschreibt.

## Erste Schritte

Um ein Segment zu exportieren, muss der Datensatz auf dem [!DNL XDM Individual Profile Union Schema] basieren. Ein Vereinigung-Schema ist ein vom System generiertes schreibgeschütztes Schema, das die Felder aller Schema, die dieselbe Klasse teilen, in diesem Fall die [!DNL XDM Individual Profile]-Klasse, Aggregat. Weitere Informationen zu Schemas der Vereinigung Ansicht finden Sie im Abschnitt [Kundenkonto in Echtzeit im Schema Registry Developer Guide](../../xdm/schema/composition.md#union).

Klicken Sie zur Ansicht der Schemas in der Benutzeroberfläche auf **[!UICONTROL Profil]** in der linken Navigation und dann auf die Registerkarte **[!UICONTROL Vereinigung Schema]**, wie unten dargestellt.

![Registerkarte &quot;Vereinigung Schema&quot;in der Benutzeroberfläche der Experience Platform](../images/tutorials/segment-export-dataset/union-schema-ui.png)


## Arbeitsbereich „Datensätze“

Der Arbeitsbereich &quot;Datensätze&quot;in der Benutzeroberfläche von [!DNL Experience Platform] ermöglicht die Ansicht und Verwaltung aller von Ihrem IMS-Unternehmen erstellten Datensätze sowie die Erstellung neuer Datensätze.

Klicken Sie zur Ansicht des Datensatzarbeitsbereichs in der linken Navigation auf **[!UICONTROL Datensätze]** und dann auf die Registerkarte **[!UICONTROL Durchsuchen]**. Der Arbeitsbereich &quot;Datensätze&quot;enthält eine Liste von Datensätzen, einschließlich der Spalten mit dem Namen, dem Erstellungsdatum (Datum und Uhrzeit), der Quelle, dem Schema und dem Status des letzten Stapels sowie dem Datum und der Uhrzeit der letzten Aktualisierung des Datensatzes. Je nach Breite der einzelnen Spalten müssen Sie ggf. nach links oder rechts blättern, um alle Spalten anzuzeigen.

>[!NOTE]
>
>Klicken Sie auf das Filtersymbol neben der Suchleiste, um Filterfunktionen zu verwenden, um nur die für [!DNL Real-time Customer Profile] aktivierten Datensätze Ansicht.

![Alle Datensätze anzeigen](../images/tutorials/segment-export-dataset/datasets-workspace.png)

## Erstellen eines Datensatzes

Um einen Datensatz zu erstellen, klicken Sie in der oberen rechten Ecke des Arbeitsbereichs „Datensätze“ auf **[!UICONTROL Datensatz erstellen]**.****

![Klicken Sie auf Datensatz erstellen](../images/tutorials/segment-export-dataset/dataset-click-create.png)

Klicken Sie im Bildschirm **[!UICONTROL Datensatz erstellen]** auf **[!UICONTROL Datensatz aus Schema]** erstellen, um fortzufahren.

![Datenquelle auswählen](../images/tutorials/segment-export-dataset/create-dataset.png)

## XDM Individuelles Profil Vereinigung Schema auswählen

Um [!DNL XDM Individual Profile Union Schema] zur Verwendung in Ihrem Datensatz auszuwählen, suchen Sie im Bildschirm **[!UICONTROL Schema auswählen]** das Schema &quot;[!UICONTROL XDM Individuelles Profil]&quot;mit dem Typ &quot;[!UICONTROL Vereinigung]&quot;.

Markieren Sie das Optionsfeld neben **[!UICONTROL XDM Individuelles Profil]** und klicken Sie dann in der oberen rechten Ecke auf **[!UICONTROL Weiter]**.

![Schema auswählen](../images/tutorials/segment-export-dataset/select-schema.png)

## Datensatz konfigurieren

Im Bildschirm **[!UICONTROL Datensatz konfigurieren]** müssen Sie dem Datensatz einen Namen geben und möglicherweise auch eine Beschreibung des Datensatzes angeben.

**Hinweise zu Datensatznamen:**
- Datensatznamen sollten kurz und beschreibend sein, damit sich der Datensatz in der Bibliothek später leicht finden lässt.
- Datensatznamen müssen eindeutig sein, d. h. sie müssen spezifisch genug sein, damit sie in Zukunft nicht wiederverwendet werden.
- Es empfiehlt sich, mithilfe des Beschreibungsfelds zusätzliche Informationen zum Datensatz anzugeben, um anderen Benutzern in Zukunft dabei zu helfen, zwischen Datensätzen zu unterscheiden.

Sobald der Datensatz einen Namen und eine Beschreibung aufweist, klicken Sie auf **[!UICONTROL Fertig stellen]**.

![Datensatz konfigurieren](../images/tutorials/segment-export-dataset/configure-dataset.png)

## Datensatzaktivität

Es wurde nun ein leerer Datensatz erstellt und Sie befinden sich wieder auf der Registerkarte **[!UICONTROL Datensatzaktivität]** im Arbeitsbereich „Datensätze“.**** Sie sollten oben links im Arbeitsbereich den Namen des Datensatzes sowie eine Benachrichtigung sehen, die Ihnen mitteilt, dass keine Batches hinzugefügt wurden. Das ist zu erwarten, da Sie dem Datensatz noch keine Batches hinzugefügt haben.

Auf der rechten Seite des Datensatzarbeitsbereichs sehen Sie die Registerkarte **[!UICONTROL Info]** mit Informationen zu Ihrem neuen Datensatz, wie z. B. Dataset-ID, Name, Beschreibung, Tabellenname, Schema, Streaming und Quelle. Die Registerkarte **[!UICONTROL Info]** enthält auch Informationen zum Zeitpunkt der Erstellung und zum Datum der letzten Änderung des Datensatzes.

Bitte beachten Sie die **[!UICONTROL Datenbestand-ID]**, da dieser Wert erforderlich ist, um den Exportarbeitsablauf für Audiencen-Segmente abzuschließen.

![Datensatzaktivität](../images/tutorials/segment-export-dataset/dataset-activity.png)

## Nächste Schritte

Nachdem Sie nun einen Datensatz auf Basis von [!DNL XDM Individual Profile Union Schema] erstellt haben, können Sie die Dataset-ID verwenden, um mit dem Lehrgang [Bewertung und Zugriff auf Segmentergebnisse](./evaluate-a-segment.md) fortzufahren.

Kehren Sie zu diesem Zeitpunkt zum Tutorial zu den ausgewerteten Segmentergebnissen zurück und nehmen Sie die Informationen im Schritt [Generieren von Profilen für Audiencen](./evaluate-a-segment.md#generate-profiles) des Exportierens eines Segmentarbeitsablaufs entgegen.
