---
title: Homepage und Dashboards zur Echtzeit-Datenplattform
seo-title: Homepage und Dashboards zur Echtzeit-Datenplattform
description: Dashboards, Homepage und Erlebnis für erstmalige Benutzer mit Adobe Experience Platform
seo-description: Dashboards, Homepage und Erlebnis für erstmalige Benutzer mit Adobe Experience Platform
translation-type: tm+mt
source-git-commit: 6dde6c90fe9073c50c0a9d3dd43ef045730d1e13

---


# Übersicht über die Echtzeit-Metriken der Kundendatenplattform

Die Homepage von Adobe Echtzeit-Kundendatenplattform (Echtzeit-CDP), die ein Metriken-Dashboard enthält, wird angezeigt, wenn Sie sich bei CDP in Echtzeit anmelden.

Die Homepage ist nur einer der Orte, an denen Metrikkarten angezeigt werden. Echtzeit-CDP bietet Metrikkarten für das gesamte Erlebnis. Diese Metriken informieren Sie über die Daten-, Profil- und Segmentzielgruppen im System.

![„image“](assets/home2.jpg)

Wenn beim Anmelden bei CDP in Echtzeit keine Daten im System vorhanden sind, wird das Dashboard auf der Homepage nicht angezeigt. In diesem Fall bietet die Homepage Lernmaterial für ein erstmaliges Benutzererlebnis. Während Daten gesammelt werden, d. h. wenn <!--sources-->Datensätze, Profile, Segmente und Ziele erstellt und Daten in das System fließen, wird das Dashboard automatisch aktualisiert, um Informationen zu diesen Daten<!-- in metric cards-->anzuzeigen.

## Homepage-Dashboard-Ansicht

<!--The dashboard shows information in several areas. Each category of information displays for the time range shown beneath the data.-->

Das Dashboard ist wie folgt unterteilt<!-- two areas.-->:

* **Die Leiste** befindet sich oben im Dashboard. Die Lederboard zeigt die Anzahl der Datensätze, Profile, Segmente und Ziele im System an.

   ![„image“](assets/home-leaderboard2.jpg)

<!-- * **Metric cards** display beneath the leaderboard. Metric cards show additional information, such as percentages or trends. Metric cards appear as data is collected.
    ![image](assets/home-metrics.jpg)
Some information is shown in different ways on both the leaderboard and metric cards. -->
* **In den letzten Elementen** werden die fünf zuletzt hinzugefügten Datensätze, Quellen, Segmente und Ziele aufgelistet.

   ![„image“](assets/home-recent.jpg)

Zusätzliche Metriken - z. B. für Profile und Segmente - stehen in anderen Teilen der Echtzeit-Kundendatenplattform zur Verfügung.

### Datensätze

Der Zähler **[!UICONTROL für Datensätze]** zeigt die Anzahl der Datensätze im System und die Datenmenge in Plattform an. Dieser Zähler wird aktualisiert, wenn ein Datensatz erstellt wird.

Weitere Informationen zu Datensätzen finden Sie unter Daten [in Adobe Experience Platform](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/data_ingestion_tutorial/data_ingestion_tutorial.md)erfassen.

### Profile

Die Anzahl der **[!UICONTROL Profile]** zeigt die Gesamtzahl der Personen mit Profilen im Echtzeit-Kundenprofil an. Es werden keine Profilfragmente einbezogen. Dies ist Ihre gesamte adressierbare Zielgruppe.

Diese Anzahl verwendet die Standardrichtlinie für die [Zusammenführung](profile/merge-policies.md) , die in der Konfiguration der Zusammenführungsrichtlinie in Unified Profile festgelegt ist.

Die Anzahl der Profile wird alle 24 Stunden aktualisiert.

Weitere Informationen zu Profilen finden Sie unter [Eine einheitliche Ansicht Ihres Kunden in Echtzeit-CDP](profile/profile-overview.md).

### Segmente

**[!UICONTROL Segmente]** zeigen die Gesamtzahl der für das Unternehmen erstellten Segmente an. Diese Zahl wird aktualisiert, wenn neue Segmente erstellt werden.

Weitere Informationen zu Segmenten finden Sie unter Übersicht über den [Segmentierungsdienst](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!end-user/markdown/segmentation_overview/segmentation.md).

### Ziele

**[!UICONTROL Ziele]** zeigen die Gesamtzahl der Ziele an, die für das Unternehmen erstellt wurden. Diese Nummer wird aktualisiert, wenn neue Ziele erstellt werden.

Weitere Informationen zu Zielen finden Sie unter Übersicht über [Ziele](destinations/destinations-overview.md).

<!-- ### Successful profile records

In the leaderboard **[!UICONTROL Successful profile records]** shows the total number of records that have been successfully processed into the profile.

There is also a metric card that shows the percentage of successful records. Click **[!UICONTROL View datasets]** to see more details about the profile records. Hover over the colored area of the graph to see additional details:

![image](assets/home-profilerecords-details.PNG)

The number of successful profile records is updated hourly. 

For more information about profiles, see [A unified view of your customer in Real-time CDP](profile/profile-overview.md).

### Total profile records

The **[!UICONTROL Total profile records]** metric card shows the total number of data records enabled to feed into the profiles, and the percentage that are successful, updated once per day. This does not include all data in the data lake, because some data might not be enabled to feed into the profiles.

 Hover over the colored area of the graph to see additional details about the successful profiles:

![image](assets/home-profile-details.PNG)

Click **[!UICONTROL View profiles]** to see more details about the profile records.

For more information about profiles, see [A unified view of your customer in Real-time CDP](profile/profile-overview.md).

For more information about viewing a specific profile, see [Profile viewer](profile/profile-viewer.md).

### Failed profile records

In the leaderboard, **[!UICONTROL Failed profile records]** counts the number of records that failed to process into the profile.

The **[!UICONTROL Failed profile records]** metric card shows this count, and includes a graphical representation that helps you see how failures have trended during the time shown below the graphic. This chart is updated hourly. Click **[!UICONTROL View datasets]** to see more details about the profile records.

The number of failed profile records is updated hourly. -->

### Letzte Datensätze

Die Karte **[!UICONTROL Letzte Datensätze]** zeigt die fünf neuesten Datensätze an, die innerhalb des Unternehmens erstellt wurden. Diese Liste wird aktualisiert, wenn ein neuer Datensatz erstellt wird.

Klicken Sie auf einen Datensatz, um die Details zu diesem Element anzuzeigen, oder **[!UICONTROL Alle]** anzeigen, um die Liste der Datensätze anzuzeigen. Von dort aus können Sie auf eine bestimmte Quelle klicken.

Weitere Informationen zu Datensätzen finden Sie unter Daten [in Adobe Experience Platform](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/data_ingestion_tutorial/data_ingestion_tutorial.md)erfassen.

### Letzte Quellen

Die Metrikkarte **[!UICONTROL Letzte Quellen]** zeigt die fünf zuletzt erstellten Quellen innerhalb des Unternehmens an. Diese Liste wird aktualisiert, wenn eine neue Quelle erstellt wird.

Klicken Sie auf eine Quelle, um die Details zu diesem Element anzuzeigen, oder **[!UICONTROL Alle]** anzeigen, um die Liste der Quellen anzuzeigen. Von dort aus können Sie auf eine bestimmte Quelle klicken.

Weitere Informationen zu Quellen finden Sie unter Übersicht über [Quellen](sources/sources-overview.md).

### Letzte Segmente

Die Metrikkarte **[!UICONTROL Letzte Segmente]** zeigt die fünf zuletzt erstellten Segmente innerhalb des Unternehmens an. Diese Liste wird aktualisiert, wenn ein neues Segment erstellt wird.

Klicken Sie auf ein Segment, um die Details zu diesem Element anzuzeigen, oder **[!UICONTROL Alle]** anzeigen, um Informationen zu weiteren Segmenten anzuzeigen.

Weitere Informationen zu Segmenten finden Sie unter Übersicht über den [Segmentierungsdienst](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!end-user/markdown/segmentation_overview/segmentation.md).

### Letzte Ziele

Die Metrikkarte &quot; **[!UICONTROL Zuletzt verwendete Ziele]** &quot;zeigt die fünf zuletzt erstellten Ziele innerhalb des Unternehmens an. Diese Liste wird aktualisiert, wenn ein neues Ziel erstellt wird.

Klicken Sie auf ein Ziel, um die Details zu diesem Element anzuzeigen, oder **[!UICONTROL Alle]** anzeigen, um Informationen zu weiteren Zielen anzuzeigen.

Weitere Informationen zu Zielen finden Sie unter Übersicht über [Ziele](destinations/destinations-overview.md).
