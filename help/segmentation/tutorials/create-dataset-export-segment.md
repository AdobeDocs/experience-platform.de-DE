---
keywords: Experience Platform; Startseite; beliebte Themen; Segmentierungsdienst; Segmentierung; Segmentierung; Datensatz erstellen; Zielgruppensegment exportieren; Segment exportieren
solution: Experience Platform
title: Erstellen eines Datensatzes zum Exportieren eines Zielgruppensegments
topic-legacy: tutorial
type: Tutorial
description: Dieses Tutorial führt Sie durch die Schritte, die zum Erstellen eines Datensatzes erforderlich sind, der zum Exportieren eines Zielgruppensegments mithilfe der Experience Platform-Benutzeroberfläche verwendet werden kann.
exl-id: 1cd16e43-b050-42ba-a894-d7ea477b65f3
source-git-commit: f7d204442c8bc2355671ba2adffff4c40ce08784
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 13%

---

# Datensatz zum Exportieren eines Zielgruppensegments erstellen

[!DNL Adobe Experience Platform] ermöglicht die Segmentierung von Kundenprofilen in Zielgruppen basierend auf bestimmten Attributen. Nachdem ein Segment erstellt wurde, können Sie diese Zielgruppe in einen Datensatz exportieren, in dem darauf zugegriffen und darauf reagiert werden kann. Damit der Export erfolgreich ist, muss der Datensatz ordnungsgemäß konfiguriert werden.

In diesem Tutorial werden die Schritte erläutert, die zum Erstellen eines Datensatzes erforderlich sind, der zum Exportieren eines Zielgruppensegments mit dem [!DNL Experience Platform] Benutzeroberfläche.

Dieses Tutorial steht in direktem Zusammenhang zu den Schritten, die im Tutorial zu [Segmentergebnisse bewerten und aufrufen](./evaluate-a-segment.md). Das Tutorial zur Segmentbewertung enthält Schritte zum Erstellen eines Datensatzes mithilfe der [!DNL Catalog Service] API. In diesem Tutorial werden die Schritte zum Erstellen eines Datensatzes mithilfe der [!DNL Experience Platform] Benutzeroberfläche.

## Erste Schritte

Um ein Segment zu exportieren, muss der Datensatz auf der [!DNL XDM Individual Profile Union Schema]. Ein Vereinigungsschema ist ein systemgeneriertes, schreibgeschütztes Schema, das die Felder aller Schemas aggregiert, die dieselbe Klasse aufweisen. Weiterführende Informationen zu Vereinigungsschemata finden Sie im Handbuch für [Grundlagen der Schemakomposition](../../xdm/schema/composition.md#union).

Um Vereinigungsschemas in der Benutzeroberfläche anzuzeigen, wählen Sie **[!UICONTROL Profile]** Wählen Sie im linken Navigationsbereich die Option **[!UICONTROL Vereinigungsschema]** wie unten dargestellt.

![Die Registerkarte Vereinigungsschema wird hervorgehoben.](../images/tutorials/segment-export-dataset/union.png)

## Arbeitsbereich „Datensätze“

Die [!UICONTROL Datensätze] Mit Workspace können Sie alle Datensätze für Ihr Unternehmen anzeigen und verwalten.

Auswählen **[!UICONTROL Datensätze]** im linken Navigationsbereich, um auf den Arbeitsbereich zuzugreifen, und wählen Sie dann **[!UICONTROL Durchsuchen]**. Auf dieser Registerkarte wird eine Liste der Datensätze und deren Details angezeigt. Je nach Breite der einzelnen Spalten müssen Sie ggf. nach links oder rechts scrollen, um alle Spalten anzuzeigen.

>[!NOTE]
>
>Wählen Sie das Filtersymbol neben der Suchleiste aus, um Filterfunktionen zu verwenden und nur die Datensätze anzuzeigen, für die [!DNL Real-time Customer Profile].

![Der Arbeitsbereich &quot;Datensätze&quot;wird angezeigt.](../images/tutorials/segment-export-dataset/browse.png)

## Erstellen eines Datensatzes

Um einen Datensatz zu erstellen, wählen Sie **[!UICONTROL Datensatz erstellen]**.

![Die Schaltfläche Datensatz erstellen ist hervorgehoben.](../images/tutorials/segment-export-dataset/create-dataset.png)

Wählen Sie im nächsten Bildschirm **[!UICONTROL Datensatz aus Schema erstellen]**.

![Die Option Datensatz aus Schema erstellen ist hervorgehoben.](../images/tutorials/segment-export-dataset/create-from-schema.png)

## XDM Individual Profile Union Schema auswählen

So wählen Sie die [!DNL XDM Individual Profile Union Schema] für die Verwendung in Ihrem Datensatz suchen Sie nach dem[!UICONTROL XDM Individual Profile]&quot; Schema im **[!UICONTROL Schema auswählen]** angezeigt. Nachdem Sie das Schema ausgewählt haben, können Sie überprüfen, ob es sich um das Vereinigungsschema unter **[!UICONTROL API-Nutzung]** in der rechten Leiste. Wenn die Variable [!UICONTROL Schema] path endet mit `_union`, ist es ein Vereinigungsschema.

>[!NOTE]
>
>Obwohl Vereinigungsschemas per Definition am Echtzeit-Kundenprofil teilnehmen, werden sie als &quot;Nicht aktiviert&quot;aufgeführt, da sie nicht wie herkömmliche Schemas für Profil aktiviert sind.

Wählen Sie das Optionsfeld neben **[!UICONTROL XDM Individual Profile]**, wählen Sie **[!UICONTROL Nächste]**.

![Das Schema &quot;XDM Individual Profile&quot;ist hervorgehoben.](../images/tutorials/segment-export-dataset/select-schema.png)

## Datensatz konfigurieren

Im nächsten Bildschirm müssen Sie Ihrem Datensatz einen Namen geben. Sie können auch eine optionale Beschreibung hinzufügen.

**Hinweise zu Datensatznamen:**

* Datensatznamen sollten kurz und beschreibend sein, damit sich der Datensatz in der Bibliothek später leicht finden lässt.
* Datensatznamen müssen eindeutig sein, d. h. sie sollten so spezifisch sein, dass sie in Zukunft nicht wiederverwendet werden.
* Es empfiehlt sich, mithilfe des Beschreibungsfelds zusätzliche Informationen zum Datensatz anzugeben, um anderen Benutzern in Zukunft dabei zu helfen, zwischen Datensätzen zu unterscheiden.

Sobald der Datensatz einen Namen und eine Beschreibung aufweist, wählen Sie **[!UICONTROL Beenden]**.

![Die Seite Datensatz konfigurieren wird angezeigt. Die Konfigurationsoptionen sind hervorgehoben.](../images/tutorials/segment-export-dataset/configure-dataset.png)

## Datensatzaktivität

Nachdem der Datensatz erstellt wurde, erhalten Sie die Aktivitätsseite für diesen Datensatz. Sie sollten oben links im Arbeitsbereich den Namen des Datensatzes sowie eine Benachrichtigung sehen, die Ihnen mitteilt, dass keine Batches hinzugefügt wurden. Das ist zu erwarten, da Sie dem Datensatz noch keine Batches hinzugefügt haben.

Die rechte Leiste enthält Informationen zu Ihrem neuen Datensatz, wie z. B. Datensatz-ID, Name, Beschreibung, Schema und mehr. Beachten Sie bitte die **[!UICONTROL Datensatz-ID]**, da dieser Wert erforderlich ist, um den Export-Workflow für Zielgruppensegmente abzuschließen.

![Die Seite mit der Datensatzaktivität wird angezeigt. Die Datensatz-ID wird hervorgehoben, da dieser Wert für künftige Schritte beachtet werden muss.](../images/tutorials/segment-export-dataset/activity.png)

## Nächste Schritte

Nachdem Sie nun einen Datensatz erstellt haben, der auf der [!DNL XDM Individual Profile Union Schema]können Sie die Datensatz-ID verwenden, um mit der [Segmentergebnisse bewerten und aufrufen](./evaluate-a-segment.md) Tutorial.

Kehren Sie zu diesem Zeitpunkt zum Tutorial mit den ausgewerteten Segmentergebnissen zurück und wählen Sie aus der [Generieren von Profilen für Zielgruppenmitglieder](./evaluate-a-segment.md#generate-profiles) Schritt des Exportierens eines Segment-Workflows.
