---
keywords: Experience Platform; Startseite; beliebte Themen; Segmentierungsdienst; Segmentierung; Segmentierung; Datensatz erstellen; Zielgruppensegment exportieren; Segment exportieren
solution: Experience Platform
title: Erstellen eines Datensatzes zum Exportieren eines Zielgruppensegments
topic-legacy: tutorial
type: Tutorial
description: Dieses Tutorial führt Sie durch die Schritte, die zum Erstellen eines Datensatzes erforderlich sind, der zum Exportieren eines Zielgruppensegments mithilfe der Experience Platform-Benutzeroberfläche verwendet werden kann.
exl-id: 1cd16e43-b050-42ba-a894-d7ea477b65f3
source-git-commit: 44d7e11e79ed0e6041ff2e4438ddb7141ae3532d
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 15%

---

# Datensatz zum Exportieren eines Zielgruppensegments erstellen

[!DNL Adobe Experience Platform] ermöglicht die Segmentierung von Kundenprofilen in Zielgruppen basierend auf bestimmten Attributen. Nachdem ein Segment erstellt wurde, können Sie diese Zielgruppe in einen Datensatz exportieren, in dem darauf zugegriffen und darauf reagiert werden kann. Damit der Export erfolgreich ist, muss der Datensatz ordnungsgemäß konfiguriert werden.

Dieses Tutorial führt Sie durch die Schritte, die zum Erstellen eines Datensatzes erforderlich sind, der zum Exportieren eines Zielgruppensegments mithilfe der [!DNL Experience Platform] -Benutzeroberfläche verwendet werden kann.

Dieses Tutorial steht in direktem Zusammenhang zu den Schritten, die im Tutorial zum [Auswerten und Zugreifen auf Segmentergebnisse](./evaluate-a-segment.md) beschrieben werden. Das Tutorial zur Segmentbewertung enthält Schritte zum Erstellen eines Datensatzes mithilfe der [!DNL Catalog Service]-API, während in diesem Tutorial Schritte zum Erstellen eines Datensatzes mithilfe der [!DNL Experience Platform]-Benutzeroberfläche beschrieben werden.

## Erste Schritte

Um ein Segment zu exportieren, muss der Datensatz auf dem [!DNL XDM Individual Profile Union Schema] basieren. Ein Vereinigungsschema ist ein systemgeneriertes, schreibgeschütztes Schema, das die Felder aller Schemas aggregiert, die dieselbe Klasse aufweisen. Weiterführende Informationen zu Vereinigungsschemata finden Sie im Handbuch [Grundlagen der Schemakomposition](../../xdm/schema/composition.md#union).

Um Vereinigungsschemas in der Benutzeroberfläche anzuzeigen, wählen Sie **[!UICONTROL Profile]** im linken Navigationsbereich und dann **[!UICONTROL Vereinigungsschema]** wie unten dargestellt aus.

![Registerkarte &quot;Vereinigungsschema&quot;in der Experience Platform-Benutzeroberfläche](../images/tutorials/segment-export-dataset/union.png)


## Arbeitsbereich „Datensätze“

Im Arbeitsbereich [!UICONTROL Datensätze] können Sie alle Datensätze für Ihr Unternehmen anzeigen und verwalten.

Wählen Sie **[!UICONTROL Datensätze]** im linken Navigationsbereich aus, um auf den Arbeitsbereich zuzugreifen, und wählen Sie dann **[!UICONTROL Durchsuchen]** aus. Auf dieser Registerkarte wird eine Liste der Datensätze und deren Details angezeigt. Je nach Breite der einzelnen Spalten müssen Sie ggf. nach links oder rechts scrollen, um alle Spalten anzuzeigen.

>[!NOTE]
>
>Wählen Sie das Filtersymbol neben der Suchleiste aus, um Filterfunktionen zu verwenden und nur die Datensätze anzuzeigen, die für [!DNL Real-time Customer Profile] aktiviert sind.

![Anzeigen von Datensätzen](../images/tutorials/segment-export-dataset/browse.png)

## Erstellen eines Datensatzes

Um einen Datensatz zu erstellen, wählen Sie **[!UICONTROL Datensatz erstellen]** aus.

![Datensatz erstellen auswählen](../images/tutorials/segment-export-dataset/create-dataset.png)

Wählen Sie im nächsten Bildschirm **[!UICONTROL Datensatz aus Schema]** erstellen aus.

![Datenquelle auswählen](../images/tutorials/segment-export-dataset/create-from-schema.png)

## XDM Individual Profile Union Schema auswählen

Um das [!DNL XDM Individual Profile Union Schema] zur Verwendung in Ihrem Datensatz auszuwählen, suchen Sie das Schema &quot;[!UICONTROL XDM Individual Profile]&quot;auf dem Bildschirm **[!UICONTROL Schema]** auswählen. Nachdem Sie das Schema ausgewählt haben, können Sie in der rechten Leiste unter **[!UICONTROL API-Nutzung]** bestätigen, ob es sich um das Vereinigungsschema handelt. Wenn der Pfad [!UICONTROL Schema] mit `_union` endet, handelt es sich um ein Vereinigungsschema.

>[!NOTE]
>
>Obwohl Vereinigungsschemas per Definition am Echtzeit-Kundenprofil teilnehmen, werden sie als &quot;Nicht aktiviert&quot;aufgeführt, da sie nicht wie herkömmliche Schemas für Profil aktiviert sind.

Wählen Sie das Optionsfeld neben **[!UICONTROL XDM Individual Profile]** und wählen Sie dann **[!UICONTROL Weiter]** aus.

![Schema auswählen](../images/tutorials/segment-export-dataset/select-schema.png)

## Datensatz konfigurieren

Im nächsten Bildschirm müssen Sie Ihrem Datensatz einen Namen geben. Sie können auch eine optionale Beschreibung hinzufügen.

**Hinweise zu Datensatznamen:**
* Datensatznamen sollten kurz und beschreibend sein, damit sich der Datensatz in der Bibliothek später leicht finden lässt.
* Datensatznamen müssen eindeutig sein, d. h. sie sollten so spezifisch sein, dass sie in Zukunft nicht wiederverwendet werden.
* Es empfiehlt sich, mithilfe des Beschreibungsfelds zusätzliche Informationen zum Datensatz anzugeben, um anderen Benutzern in Zukunft dabei zu helfen, zwischen Datensätzen zu unterscheiden.

Sobald der Datensatz einen Namen und eine Beschreibung aufweist, wählen Sie **[!UICONTROL Finish]** aus.

![Datensatz konfigurieren](../images/tutorials/segment-export-dataset/configure-dataset.png)

## Datensatzaktivität

Nachdem der Datensatz erstellt wurde, erhalten Sie die Aktivitätsseite für diesen Datensatz. Sie sollten oben links im Arbeitsbereich den Namen des Datensatzes sowie eine Benachrichtigung sehen, die Ihnen mitteilt, dass keine Batches hinzugefügt wurden. Das ist zu erwarten, da Sie dem Datensatz noch keine Batches hinzugefügt haben.

Die rechte Leiste enthält Informationen zu Ihrem neuen Datensatz, wie z. B. Datensatz-ID, Name, Beschreibung, Schema und mehr. Beachten Sie die **[!UICONTROL Datensatz-ID]**, da dieser Wert erforderlich ist, um den Export-Workflow für Zielgruppensegmente abzuschließen.

![Datensatzaktivität](../images/tutorials/segment-export-dataset/activity.png)

## Nächste Schritte

Nachdem Sie nun einen Datensatz basierend auf [!DNL XDM Individual Profile Union Schema] erstellt haben, können Sie die Datensatz-ID verwenden, um das Tutorial [Auswerten und Aufrufen von Segmentergebnissen](./evaluate-a-segment.md) fortzusetzen.

Kehren Sie zu diesem Zeitpunkt zum Tutorial zum Bewerten der Segmentergebnisse zurück und wählen Sie den Schritt [Generieren von Profilen für Zielgruppenmitglieder](./evaluate-a-segment.md#generate-profiles) des Segmentexports aus.
