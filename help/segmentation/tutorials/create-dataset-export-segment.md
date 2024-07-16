---
solution: Experience Platform
title: Erstellen eines Datensatzes zum Exportieren einer Zielgruppe
type: Tutorial
description: Erfahren Sie, wie Sie einen Datensatz erstellen, der zum Exportieren einer Zielgruppe mithilfe der Experience Platform-Benutzeroberfläche verwendet werden kann.
exl-id: 1cd16e43-b050-42ba-a894-d7ea477b65f3
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 9%

---

# Erstellen eines Datensatzes zum Exportieren einer Zielgruppe

Mit [!DNL Adobe Experience Platform] können Sie Kundenprofile basierend auf bestimmten Attributen in Zielgruppen unterteilen. Nachdem eine Segmentdefinition erstellt wurde, können Sie die resultierende Zielgruppe in einen Datensatz exportieren, in dem sie aufgerufen und bearbeitet werden kann. Damit der Export erfolgreich ist, muss der Datensatz ordnungsgemäß konfiguriert werden.

Dieses Tutorial führt Sie durch die Schritte, die zum Erstellen eines Datensatzes erforderlich sind, der zum Exportieren einer Zielgruppe mithilfe der Benutzeroberfläche von [!DNL Experience Platform] verwendet werden kann.

Dieses Tutorial steht in direktem Zusammenhang zu den Schritten, die im Tutorial zum [Auswerten und Aufrufen von Segmentierungsergebnissen](./evaluate-a-segment.md) beschrieben werden. Das Tutorial zur Bewertung der Segmentdefinition enthält Schritte zum Erstellen eines Datensatzes mithilfe der [!DNL Catalog Service] -API, während dieses Tutorial Schritte zum Erstellen eines Datensatzes mithilfe der [!DNL Experience Platform] -Benutzeroberfläche beschreibt.

## Erste Schritte

Um eine Zielgruppe zu exportieren, muss der Datensatz auf dem [!DNL XDM Individual Profile Union Schema] basieren. Ein Vereinigungsschema ist ein systemgeneriertes, schreibgeschütztes Schema, das die Felder aller Schemas aggregiert, die dieselbe Klasse aufweisen. Weiterführende Informationen zu Vereinigungsschemata finden Sie im Handbuch [Grundlagen der Schemakomposition](../../xdm/schema/composition.md#union) .

Um Vereinigungsschemas in der Benutzeroberfläche anzuzeigen, wählen Sie im linken Navigationsbereich **[!UICONTROL Profile]** und dann **[!UICONTROL Vereinigungsschema]** aus, wie unten dargestellt.

![Die Registerkarte für das Vereinigungsschema ist hervorgehoben.](../images/tutorials/segment-export-dataset/union.png)

## Arbeitsbereich „Datensätze“

Im Arbeitsbereich [!UICONTROL Datensätze] können Sie alle Datensätze für Ihr Unternehmen anzeigen und verwalten.

Wählen Sie im linken Navigationsbereich **[!UICONTROL Datensätze]** aus, um auf den Arbeitsbereich zuzugreifen, und wählen Sie dann **[!UICONTROL Durchsuchen]** aus. Auf dieser Registerkarte wird eine Liste der Datensätze und deren Details angezeigt. Je nach Breite der einzelnen Spalten müssen Sie ggf. nach links oder rechts scrollen, um alle Spalten anzuzeigen.

>[!NOTE]
>
>Wählen Sie das Filtersymbol neben der Suchleiste aus, um Filterfunktionen zu verwenden und nur die für [!DNL Real-Time Customer Profile] aktivierten Datensätze anzuzeigen.

![Der Arbeitsbereich &quot;Datensätze&quot;wird angezeigt.](../images/tutorials/segment-export-dataset/browse.png)

## Erstellen eines Datensatzes

Um einen Datensatz zu erstellen, wählen Sie **[!UICONTROL Datensatz erstellen]** aus.

![Die Schaltfläche Datensatz erstellen ist hervorgehoben.](../images/tutorials/segment-export-dataset/create-dataset.png)

Wählen Sie im nächsten Bildschirm **[!UICONTROL Datensatz aus Schema erstellen]** aus.

![Die Option Datensatz aus Schema erstellen ist hervorgehoben.](../images/tutorials/segment-export-dataset/create-from-schema.png)

## XDM Individual Profile Union Schema auswählen

Um das Schema &quot;[!DNL XDM Individual Profile Union Schema]&quot; für die Verwendung in Ihrem Datensatz auszuwählen, suchen Sie das Schema &quot;[!UICONTROL XDM Individual Profile]&quot;auf dem Bildschirm &quot;**[!UICONTROL Schema auswählen]**&quot;. Nachdem Sie das Schema ausgewählt haben, können Sie in der rechten Leiste unter **[!UICONTROL API-Nutzung]** überprüfen, ob es das Vereinigungsschema ist. Wenn der Pfad [!UICONTROL Schema] mit `_union` endet, handelt es sich um ein Vereinigungsschema.

>[!NOTE]
>
>Obwohl Vereinigungsschemas per Definition am Echtzeit-Kundenprofil teilnehmen, werden sie als &quot;Nicht aktiviert&quot;aufgeführt, da sie nicht wie herkömmliche Schemas für Profil aktiviert sind.

Wählen Sie das Optionsfeld neben **[!UICONTROL XDM Individual Profile]** und dann **[!UICONTROL Weiter]** aus.

![Das Schema &quot;XDM Individual Profile&quot;ist hervorgehoben.](../images/tutorials/segment-export-dataset/select-schema.png)

## Datensatz konfigurieren

Im nächsten Bildschirm müssen Sie Ihrem Datensatz einen Namen geben. Sie können auch eine optionale Beschreibung hinzufügen.

**Hinweise zu Datensatznamen:**

* Datensatznamen sollten kurz und beschreibend sein, damit sich der Datensatz in der Bibliothek später leicht finden lässt.
* Datensatznamen müssen eindeutig sein, d. h. sie sollten so spezifisch sein, dass sie in Zukunft nicht wiederverwendet werden.
* Sie sollten mithilfe des Beschreibungsfelds zusätzliche Informationen über den Datensatz bereitstellen, da dies anderen Benutzern helfen kann, in Zukunft zwischen Datensätzen zu unterscheiden.

Sobald der Datensatz einen Namen und eine Beschreibung aufweist, wählen Sie **[!UICONTROL Beenden]** aus.

![Die Seite Datensatz konfigurieren wird angezeigt. Die Konfigurationsoptionen sind hervorgehoben.](../images/tutorials/segment-export-dataset/configure-dataset.png)

## Datensatzaktivität

Nachdem der Datensatz erstellt wurde, erhalten Sie die Aktivitätsseite für diesen Datensatz. Sie sollten oben links im Arbeitsbereich den Namen des Datensatzes sowie eine Benachrichtigung sehen, die Ihnen mitteilt, dass keine Batches hinzugefügt wurden. Das ist zu erwarten, da Sie dem Datensatz noch keine Batches hinzugefügt haben.

Die rechte Leiste enthält Informationen zu Ihrem neuen Datensatz, wie z. B. Datensatz-ID, Name, Beschreibung, Schema und mehr. Notieren Sie sich die **[!UICONTROL Datensatz-ID]**, da dieser Wert erforderlich ist, um den Workflow für den Zielgruppenexport abzuschließen.

![Die Seite mit der Datensatzaktivität wird angezeigt. Die Datensatz-ID wird hervorgehoben, da dieser Wert für zukünftige Schritte vermerkt werden muss.](../images/tutorials/segment-export-dataset/activity.png)

## Nächste Schritte

Nachdem Sie nun einen Datensatz basierend auf [!DNL XDM Individual Profile Union Schema] erstellt haben, können Sie die Datensatz-ID verwenden, um das Tutorial [Auswerten und Zugreifen auf Segmentdefinitionsergebnisse](./evaluate-a-segment.md) fortzusetzen.

Kehren Sie zu diesem Zeitpunkt zum Tutorial mit den Ergebnissen der Segmentdefinition zurück und wählen Sie aus dem Schritt [Generieren von Profilen für Zielgruppenmitglieder](./evaluate-a-segment.md#generate-profiles) des Export-Audience-Workflows aus.
