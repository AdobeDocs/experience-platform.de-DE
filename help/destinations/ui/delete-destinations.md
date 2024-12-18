---
keywords: Ziele löschen, Ziele löschen, Ziel löschen
title: Löschen von Zielen
type: Tutorial
description: In diesem Tutorial werden die Schritte zum Löschen eines vorhandenen Ziels in der Adobe Experience Platform-Benutzeroberfläche aufgeführt
exl-id: 7b672859-e61a-4b3c-9db9-62048258f0aa
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 32%

---

# Löschen von Zielen {#delete-destinations}

## Übersicht {#overview}

In der Adobe Experience Platform-Benutzeroberfläche können Sie vorhandene Verbindungen zu Zielen löschen.

Durch das Löschen eines Ziels werden alle vorhandenen Datenflüsse zu diesem Ziel entfernt. Alle Zielgruppen, die für die Ziele aktiviert sind, die Sie löschen, werden vor dem Löschen des Datenflusses nicht zugeordnet.

Es gibt zwei Möglichkeiten, Ziele aus dem [!DNL Platform] [!DNL UI] zu löschen. Sie haben folgende Möglichkeiten:

* [Löschen von Zielen aus der Registerkarte [!UICONTROL Durchsuchen]](#delete-browse-tab)
* [Ziele von der Seite mit den Zieldetails löschen](#delete-destination-details-page)

## Löschen von Zielen über die Registerkarte &quot;Durchsuchen&quot;{#delete-browse-tab}

Gehen Sie wie folgt vor, um ein Ziel auf der Registerkarte [!UICONTROL Durchsuchen] zu löschen.

1. Melden Sie sich bei der [Experience Platform-Benutzeroberfläche](https://platform.adobe.com/) an und wählen Sie **[!UICONTROL Ziele]** über die linke Navigationsleiste aus. Um Ihre vorhandenen Ziele anzuzeigen, wählen Sie **[!UICONTROL Durchsuchen]** aus der oberen Kopfzeile aus.

   ![Ziele durchsuchen](../assets/ui/delete-destinations/browse-destinations.png)

2. Wählen Sie das Symbol ![Filter](/help/images/icons/filter.png) oben links, um das Sortier-Bedienfeld zu öffnen. Das Sortier-Bedienfeld bietet eine Liste aller Ihrer Ziele. Sie können mehr als ein Ziel aus der Liste auswählen, um eine gefilterte Auswahl von Datenflüssen anzuzeigen, die mit dem ausgewählten Ziel verknüpft sind.

   ![Ziele filtern](../assets/ui/delete-destinations/filter-destinations.png)

3. Wählen Sie die Schaltfläche ![Mehr ](/help/images/icons/more.png) in der Spalte &quot;Name&quot;und dann die Schaltfläche ![Löschen](/help/images/icons/delete.png) **[!UICONTROL Löschen]** aus, um eine vorhandene Zielverbindung zu entfernen.
   ![Ziele löschen](../assets/ui/delete-destinations/delete-destinations.png)

4. Wählen Sie **[!UICONTROL Löschen]** aus, um das Entfernen der Zielverbindung zu bestätigen.

   ![Löschziel bestätigen](../assets/ui/delete-destinations/delete-destinations-confirm.png)

## Ziele von der Seite mit den Zieldetails löschen{#delete-destination-details-page}

Gehen Sie wie folgt vor, um ein Ziel auf der Seite mit den Zieldetails zu löschen.

1. Melden Sie sich bei der [Experience Platform-Benutzeroberfläche](https://platform.adobe.com/) an und wählen Sie **[!UICONTROL Ziele]** über die linke Navigationsleiste aus. Um Ihre vorhandenen Ziele anzuzeigen, wählen Sie **[!UICONTROL Durchsuchen]** aus der oberen Kopfzeile aus.

   ![Ziele durchsuchen](../assets/ui/delete-destinations/browse-destinations.png)

2. Wählen Sie das Symbol ![Filter](/help/images/icons/filter.png) oben links, um das Sortier-Bedienfeld zu öffnen. Das Sortier-Bedienfeld bietet eine Liste aller Ihrer Ziele. Sie können mehr als ein Ziel aus der Liste auswählen, um eine gefilterte Auswahl von Datenflüssen anzuzeigen, die mit dem ausgewählten Ziel verknüpft sind.

   ![Ziele filtern](../assets/ui/delete-destinations/filter-destinations.png)

3. Wählen Sie den Namen des Ziels aus, das Sie löschen möchten.

   ![Auswählen des Ziels](../assets/ui/delete-destinations/delete-destination-select.png)

   * Wenn das Ziel über einen vorhandenen Datenfluss verfügt, gelangen Sie zur Registerkarte [!UICONTROL Datenfluss läuft] .

     ![Registerkarte &quot;Datenfluss-Ausführung&quot;](../assets/ui/delete-destinations/destination-details-dataflows.png)

   * Wenn das Ziel keine vorhandenen Datenflüsse aufweist, gelangen Sie zu einer leeren Seite, auf der Sie Zielgruppen aktivieren können.

     ![Zieldetails](../assets/ui/delete-destinations/destination-details-empty.png)

4. Wählen Sie in der rechten Leiste **[!UICONTROL Löschen]** aus.

   ![Ziel löschen](../assets/ui/delete-destinations/delete-destinations-button.png)

5. Wählen Sie **[!UICONTROL Löschen]** im Bestätigungsdialogfeld aus, um das Ziel zu entfernen.

   ![Ziel löschen, Bestätigung löschen](..//assets/ui/delete-destinations/delete-destinations-delete.png)

   >[!NOTE]
   >
   >Je nach Server-Load kann es einige Minuten dauern, bis [!DNL Platform] das Ziel löscht.
