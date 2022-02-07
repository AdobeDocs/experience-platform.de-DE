---
keywords: Ziele löschen, Ziele löschen, Ziel löschen
title: Ziele löschen
type: Tutorial
description: In diesem Tutorial werden die Schritte zum Löschen eines vorhandenen Ziels in der Adobe Experience Platform-Benutzeroberfläche aufgeführt
exl-id: 7b672859-e61a-4b3c-9db9-62048258f0aa
source-git-commit: 1ef6430b6661a2b8b5aef196b75cfaf3f6220aab
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 1%

---

# Ziele löschen {#delete-destinations}

## Übersicht {#overview}

In der Adobe Experience Platform-Benutzeroberfläche können Sie vorhandene Verbindungen zu Zielen löschen.

Durch das Löschen eines Ziels werden alle vorhandenen Datenflüsse zu diesem Ziel entfernt. Alle Segmente, die für die Ziele aktiviert sind, die Sie löschen, werden vor dem Löschen des Datenflusses nicht zugeordnet.

Es gibt zwei Möglichkeiten, Ziele aus dem [!DNL Platform] [!DNL UI]. Sie haben folgende Möglichkeiten:

* [Löschen Sie Ziele aus dem [!UICONTROL Durchsuchen] tab](#delete-browse-tab)
* [Ziele von der Seite mit den Zieldetails löschen](#delete-destination-details-page)

## Löschen von Zielen über die Registerkarte &quot;Durchsuchen&quot;{#delete-browse-tab}

Gehen Sie wie folgt vor, um ein Ziel aus dem [!UICONTROL Durchsuchen] Registerkarte.

1. Melden Sie sich bei der [Experience Platform-Benutzeroberfläche](https://platform.adobe.com/) und wählen Sie **[!UICONTROL Ziele]** über die linke Navigationsleiste. Um Ihre vorhandenen Ziele anzuzeigen, wählen Sie **[!UICONTROL Durchsuchen]** aus der oberen Kopfzeile.

   ![Ziele durchsuchen](../assets/ui/delete-destinations/browse-destinations.png)

2. Filtersymbol auswählen ![Filter-Symbol](../assets/ui/delete-destinations/filter.png) oben links, um das Sortierungsfenster zu öffnen. Das Sortierungsfenster bietet eine Liste aller Ziele. Sie können mehr als ein Ziel aus der Liste auswählen, um eine gefilterte Auswahl von Datenflüssen anzuzeigen, die mit dem ausgewählten Ziel verknüpft sind.

   ![Ziele filtern](../assets/ui/delete-destinations/filter-destinations.png)

3. Wählen Sie die ![Schaltfläche Mehr](../assets/ui/delete-destinations/more-icon.png) in der Spalte &quot;Name&quot;und wählen Sie ![Schaltfläche &quot;Löschen&quot;](../assets/ui/delete-destinations/delete-icon.png) **[!UICONTROL Löschen]** , um eine vorhandene Zielverbindung zu entfernen.
   ![Ziele löschen](../assets/ui/delete-destinations/delete-destinations.png)

4. Auswählen **[!UICONTROL Löschen]** , um das Entfernen der Zielverbindung zu bestätigen.

   ![Löschziel bestätigen](../assets/ui/delete-destinations/delete-destinations-confirm.png)

## Ziele von der Seite mit den Zieldetails löschen{#delete-destination-details-page}

Gehen Sie wie folgt vor, um ein Ziel auf der Seite mit den Zieldetails zu löschen.

1. Melden Sie sich bei der [Experience Platform-Benutzeroberfläche](https://platform.adobe.com/) und wählen Sie **[!UICONTROL Ziele]** über die linke Navigationsleiste. Um Ihre vorhandenen Ziele anzuzeigen, wählen Sie **[!UICONTROL Durchsuchen]** aus der oberen Kopfzeile.

   ![Ziele durchsuchen](../assets/ui/delete-destinations/browse-destinations.png)

2. Filtersymbol auswählen ![Filter-Symbol](../assets/ui/delete-destinations/filter.png) oben links, um das Sortierungsfenster zu öffnen. Das Sortierungsfenster bietet eine Liste aller Ziele. Sie können mehr als ein Ziel aus der Liste auswählen, um eine gefilterte Auswahl von Datenflüssen anzuzeigen, die mit dem ausgewählten Ziel verknüpft sind.

   ![Ziele filtern](../assets/ui/delete-destinations/filter-destinations.png)

3. Wählen Sie den Namen des Ziels aus, das Sie löschen möchten.

   ![Ziel auswählen](../assets/ui/delete-destinations/delete-destination-select.png)

   * Wenn das Ziel über einen vorhandenen Datenfluss verfügt, werden Sie zum [!UICONTROL Datenfluss-Abläufe] Registerkarte.

      ![Registerkarte &quot;Datenfluss&quot;](../assets/ui/delete-destinations/destination-details-dataflows.png)

   * Wenn das Ziel keine vorhandenen Datenflüsse aufweist, gelangen Sie zu einer leeren Seite, auf der Sie Zielgruppen aktivieren können.

      ![Zieldetails](../assets/ui/delete-destinations/destination-details-empty.png)

4. Auswählen **[!UICONTROL Löschen]** in der rechten Leiste.

   ![Ziel löschen](../assets/ui/delete-destinations/delete-destinations-button.png)

5. Auswählen **[!UICONTROL Löschen]** im Bestätigungsdialogfeld, um das Ziel zu entfernen.

   ![Zielbestätigung löschen](..//assets/ui/delete-destinations/delete-destinations-delete.png)

   >[!NOTE]
   >
   >Je nach Server-Load kann es einige Minuten dauern [!DNL Platform] , um das Ziel zu löschen.
