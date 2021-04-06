---
keywords: Ziele löschen; Löschen von Zielen
title: Ziele löschen
type: Tutorial
description: In diesem Lernprogramm werden die Schritte zum Löschen eines vorhandenen Ziels in der Adobe Experience Platform-Benutzeroberfläche Liste
exl-id: 7b672859-e61a-4b3c-9db9-62048258f0aa
translation-type: tm+mt
source-git-commit: e436d7147c613dad5b2ff596a412759fd60d228c
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 1%

---

# Ziele löschen {#delete-destinations}

## Übersicht {#overview}

In der Adobe Experience Platform-Benutzeroberfläche können Sie bestehende Verbindungen zu Zielen löschen.

Beim Löschen eines Ziels werden alle vorhandenen Datenflüsse zu diesem Ziel entfernt. Alle Segmente, die für die zu löschenden Ziele aktiviert wurden, werden vor dem Löschen des Datenflusses nicht zugeordnet.

Es gibt zwei Möglichkeiten, Ziele aus dem [!DNL Platform] [!DNL UI] zu löschen. Sie haben folgende Möglichkeiten:

* [Ziele aus der   Registerkarte &quot;Durchsuchen&quot;löschen](#delete-browse-tab)
* [Ziele von der Seite mit den Zieldetails löschen](#delete-destination-details-page)

## Ziele aus der Registerkarte &quot;Durchsuchen&quot;löschen{#delete-browse-tab}

Gehen Sie wie folgt vor, um ein Ziel aus der Registerkarte [!UICONTROL Durchsuchen] zu löschen.

1. Melden Sie sich bei [Experience Platform UI](https://platform.adobe.com/) an und wählen Sie **[!UICONTROL Ziele]** in der linken Navigationsleiste aus. Um Ihre vorhandenen Ziele Ansicht, wählen Sie **[!UICONTROL Durchsuchen]** aus der oberen Kopfzeile.

   ![Ziele durchsuchen](../assets/ui/delete-destinations/browse-destinations.png)

2. Wählen Sie oben links das Filtersymbol ![Filtersymbol](../assets/ui/delete-destinations/filter.png) aus, um das Sortierfeld zu starten. Der Bereich &quot;Sortieren&quot;enthält eine Liste aller Ziele. Sie können mehr als ein Ziel aus der Liste auswählen, um eine gefilterte Auswahl an Datenflüssen anzuzeigen, die mit dem ausgewählten Ziel verknüpft sind.

   ![Ziele filtern](../assets/ui/delete-destinations/filter-destinations.png)

3. Wählen Sie die Schaltfläche ![Löschen](../assets/ui/delete-destinations/delete-icon.png) **[!UICONTROL Löschen]** in der Spalte **[!UICONTROL Plattform]**, um ein vorhandenes Ziel zu entfernen.
   ![Ziele löschen](../assets/ui/delete-destinations/delete-destinations.png)

4. Wählen Sie **[!UICONTROL Löschen]**, um das Entfernen des Ziels zu bestätigen.

   ![Löschziel bestätigen](../assets/ui/delete-destinations/delete-destinations-confirm.png)


## Ziele von der Seite mit den Zieldetails löschen{#delete-destination-details-page}

Gehen Sie wie folgt vor, um ein Ziel aus der Seite mit den Zieldetails zu löschen.

1. Melden Sie sich bei [Experience Platform UI](https://platform.adobe.com/) an und wählen Sie **[!UICONTROL Ziele]** in der linken Navigationsleiste aus. Um Ihre vorhandenen Ziele Ansicht, wählen Sie **[!UICONTROL Durchsuchen]** aus der oberen Kopfzeile.

   ![Ziele durchsuchen](../assets/ui/delete-destinations/browse-destinations.png)

2. Wählen Sie oben links das Filtersymbol ![Filtersymbol](../assets/ui/delete-destinations/filter.png) aus, um das Sortierfeld zu starten. Der Bereich &quot;Sortieren&quot;enthält eine Liste aller Ziele. Sie können mehr als ein Ziel aus der Liste auswählen, um eine gefilterte Auswahl an Datenflüssen anzuzeigen, die mit dem ausgewählten Ziel verknüpft sind.

   ![Ziele filtern](../assets/ui/delete-destinations/filter-destinations.png)

3. Wählen Sie den Namen des Ziels aus, das Sie löschen möchten.

   ![Ziel auswählen](../assets/ui/delete-destinations/delete-destination-select.png)

   * Wenn das Ziel über vorhandene Datenflüsse verfügt, werden Sie zur Registerkarte [!UICONTROL Datenflug-Ausführung] geleitet.

      ![Registerkarte &quot;Datenfluss&quot;](../assets/ui/delete-destinations/destination-details-dataflows.png)

   * Wenn für das Ziel keine Datenflüsse vorhanden sind, werden Sie zu einer leeren Seite geleitet, auf der Sie Audiencen aktivieren können.

      ![Zieldetails](../assets/ui/delete-destinations/destination-details-empty.png)


4. Wählen Sie **[!UICONTROL Löschen]** in der rechten Leiste.

   ![Ziel löschen](../assets/ui/delete-destinations/delete-destinations-button.png)

5. Wählen Sie **[!UICONTROL Löschen]** im Bestätigungsdialogfeld aus, um das Ziel zu entfernen.

   ![Zielbestätigung löschen](..//assets/ui/delete-destinations/delete-destinations-delete.png)

   >[!NOTE]
   >
   >Je nach Serverlast kann es einige Minuten dauern, bis [!DNL Platform] das Ziel gelöscht wird.
