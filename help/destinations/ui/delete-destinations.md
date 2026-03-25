---
keywords: Löschen von Zielen, Löschen von Zielen, Löschen von Zielen
title: Löschen von Zielen
type: Tutorial
description: In diesem Tutorial werden die Schritte zum Löschen eines vorhandenen Ziels in der Adobe Experience Platform-Benutzeroberfläche aufgelistet
exl-id: 7b672859-e61a-4b3c-9db9-62048258f0aa
source-git-commit: d946d3dbb09c1fe0163fba3a892b4c0f1b331f87
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 26%

---

# Löschen von Zielen {#delete-destinations}

## Überblick {#overview}

In der [!DNL Adobe Experience Platform]-Benutzeroberfläche können Sie vorhandene Verbindungen zu Zielen löschen.

Durch das Löschen eines Ziels werden alle vorhandenen Datenflüsse zu diesem Ziel entfernt. Alle Zielgruppen, die für die zu löschenden Ziele aktiviert sind, werden nicht zugeordnet, bevor der Datenfluss gelöscht wird.

Es gibt zwei Möglichkeiten, Ziele aus dem [!DNL Experience Platform]-[!DNL UI] zu löschen. Sie haben folgende Möglichkeiten:

* [Löschen von Zielen auf der Registerkarte [!UICONTROL Browse]](#delete-browse-tab)
* [Löschen von Zielen auf der Seite mit den Zieldetails](#delete-destination-details-page)

## Löschen von Zielen auf der Registerkarte Durchsuchen{#delete-browse-tab}

Gehen Sie wie folgt vor, um ein Ziel aus der Registerkarte [!UICONTROL Browse] zu löschen.

1. Melden Sie sich bei der Benutzeroberfläche von [Experience Platform &#x200B;](https://platform.adobe.com/) und wählen Sie **[!UICONTROL Destinations]** über die linke Navigationsleiste aus. Um Ihre vorhandenen Ziele anzuzeigen, wählen Sie **[!UICONTROL Browse]** in der oberen Kopfzeile aus.

   ![Ziele durchsuchen](../assets/ui/delete-destinations/browse-destinations.png)

2. Wählen Sie das Symbol ![Filter](/help/images/icons/filter.png) oben links, um das Sortier-Bedienfeld zu öffnen. Das Sortier-Bedienfeld bietet eine Liste aller Ihrer Ziele. Sie können mehr als ein Ziel aus der Liste auswählen, um eine gefilterte Auswahl von Datenflüssen anzuzeigen, die mit dem ausgewählten Ziel verknüpft sind.

   ![Ziele filtern](../assets/ui/delete-destinations/filter-destinations.png)

3. Wählen Sie in der Spalte „Name![&#x200B; die Schaltfläche &#x200B;](/help/images/icons/more.png)Mehr“ und dann ![Schaltfläche „Löschen](/help/images/icons/delete.png) **[!UICONTROL Delete]**, um eine vorhandene Zielverbindung zu entfernen.
   ![Ziele löschen](../assets/ui/delete-destinations/delete-destinations.png)

4. Wählen Sie **[!UICONTROL Delete]** aus, um das Entfernen der Zielverbindung zu bestätigen.

   ![Löschziel bestätigen](../assets/ui/delete-destinations/delete-destinations-confirm.png)

## Löschen von Zielen auf der Seite mit den Zieldetails{#delete-destination-details-page}

Gehen Sie wie folgt vor, um ein Ziel von der Seite mit den Zieldetails zu löschen.

1. Melden Sie sich bei der Benutzeroberfläche von [Experience Platform &#x200B;](https://platform.adobe.com/) und wählen Sie **[!UICONTROL Destinations]** über die linke Navigationsleiste aus. Um Ihre vorhandenen Ziele anzuzeigen, wählen Sie **[!UICONTROL Browse]** in der oberen Kopfzeile aus.

   ![Ziele durchsuchen](../assets/ui/delete-destinations/browse-destinations.png)

2. Wählen Sie das Symbol ![Filter](/help/images/icons/filter.png) oben links, um das Sortier-Bedienfeld zu öffnen. Das Sortier-Bedienfeld bietet eine Liste aller Ihrer Ziele. Sie können mehr als ein Ziel aus der Liste auswählen, um eine gefilterte Auswahl von Datenflüssen anzuzeigen, die mit dem ausgewählten Ziel verknüpft sind.

   ![Ziele filtern](../assets/ui/delete-destinations/filter-destinations.png)

3. Wählen Sie den Namen des Ziels aus, das Sie löschen möchten.

   ![Auswählen des Ziels](../assets/ui/delete-destinations/delete-destination-select.png)

   * Wenn das Ziel über vorhandene Datenflüsse verfügt, gelangen Sie zur Registerkarte [!UICONTROL Dataflow runs] .

     ![Registerkarte „Datenflussausführungen“](../assets/ui/delete-destinations/destination-details-dataflows.png)

   * Wenn das Ziel nicht über vorhandene Datenflüsse verfügt, gelangen Sie auf eine leere Seite, auf der Sie mit der Aktivierung von Zielgruppen beginnen können.

     ![Zieldetails](../assets/ui/delete-destinations/destination-details-empty.png)

4. Wählen Sie **[!UICONTROL Delete]** in der rechten Leiste aus.

   ![Ziel löschen](../assets/ui/delete-destinations/delete-destinations-button.png)

5. Wählen Sie **[!UICONTROL Delete]** im Bestätigungsdialogfeld aus, um das Ziel zu entfernen.

   ![Ziel löschen bestätigen](..//assets/ui/delete-destinations/delete-destinations-delete.png)

   >[!NOTE]
   >
   >Je nach Server-Last kann es einige Minuten dauern, bis [!DNL Experience Platform] das Ziel löscht.
