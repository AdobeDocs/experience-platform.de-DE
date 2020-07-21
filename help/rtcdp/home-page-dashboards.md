---
title: Startseite und Dashboards der Echtzeit-Kundendatenplattform
seo-title: Startseite und Dashboards der Echtzeit-Kundendatenplattform
description: Dashboards, Startseite und erstmalige Nutzung von Adobe Experience Platform
seo-description: Dashboards, Startseite und erstmalige Nutzung von Adobe Experience Platform
translation-type: tm+mt
source-git-commit: b96286f6a06f0583b45343a513ee64f0025d79a7
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 94%

---


# [!DNL Real-time Customer Data Platform] Metriken - Übersicht

Die Startseite der Echtzeit-Kundendatenplattform von Adobe, die ein Metriken-Dashboard enthält, wird angezeigt, sobald Sie sich bei der Echtzeit-Kundendatenplattform anmelden.

Die Startseite ist nur einer der Orte, an denen Metrikkarten angezeigt werden. Die Echtzeit-Kundendatenplattform stellt Metrikkarten während des gesamten Erlebnisses bereit. Diese Metriken informieren Sie über die Daten-, Profil- und Segmentzielgruppen im System.

![Bild](assets/home2.jpg)

Wenn zum Zeitpunkt der Anmeldung bei der Echtzeit-Kundendatenplattform keine Daten im System vorhanden sind, wird das Dashboard auf der Startseite nicht angezeigt. In dem Fall enthält die Startseite Lernmaterial für die erstmalige Nutzung. Im Zuge der Sammlung von Daten, d. h. wenn <!--sources-->Datensätze, Profile, Segmente und Ziele erstellt werden und Daten in das System fließen, wird das Dashboard automatisch aktualisiert, um Informationen zu diesen Daten anzuzeigen<!-- in metric cards-->.

## Dashboard-Ansicht auf der Startseite

<!--The dashboard shows information in several areas. Each category of information displays for the time range shown beneath the data.-->

Das Dashboard ist wie folgt unterteilt<!-- two areas.-->:

* Das **Leaderboard** befindet sich oben im Dashboard. Im Leaderboard wird die Zahl der Datensätze, Profile, Segmente und Ziele im System angezeigt.

   ![Bild](assets/home-leaderboard2.jpg)

<!-- * **Metric cards** display beneath the leaderboard. Metric cards show additional information, such as percentages or trends. Metric cards appear as data is collected.
    ![image](assets/home-metrics.jpg)
Some information is shown in different ways on both the leaderboard and metric cards. -->
* Unter **Letzte Elemente** werden die fünf Datensätze, Quellen, Segmente und Ziele aufgeführt, die dem System zuletzt hinzugefügt wurden.

   ![Bild](assets/home-recent.jpg)

Zusätzliche Metriken (z. B. für Profile und Segmente) stehen in anderen Teilen der Echtzeit-Kundendatenplattform zur Verfügung.

### Datensätze

The **[!UICONTROL Datasets]** counter shows the number of datasets in the system and the amount of data in [!DNL Platform]. Dieser Zähler wird aktualisiert, sobald ein neuer Datensatz erstellt wird.

Weiterführende Informationen über Datensätze finden Sie in der [Datensatzübersicht](../catalog/datasets/overview.md).

### Profile

The **[!UICONTROL Profiles]** count shows the total number of people with profiles in the [!DNL Real-time Customer Profile]. Profilfragmente werden nicht einbezogen. Dabei handelt es sich um Ihre gesamte adressierbare Zielgruppe.

Der Zähler nutzt die standardmäßige [Zusammenführungsrichtlinie](profile/merge-policies.md), die in der Konfiguration der Zusammenführungsrichtlinien im einheitlichen Profil festgelegt ist.

Die Zahl der Profile wird alle 24 Stunden aktualisiert.

Weiterführende Informationen zu Profilen finden Sie unter [Einheitliche Sicht auf Kunden in der Echtzeit-Kundendatenplattform](profile/profile-overview.md).

### Segmente

**[!UICONTROL Segmente]** gibt die Gesamtzahl der für das Unternehmen erstellten Segmente an. Diese Zahl wird aktualisiert, sobald neue Segmente erstellt werden.

Weiterführende Informationen zu Segmenten finden Sie unter [Segmentierungsdienst – Übersicht](segmentation/segmentation-overview.md).

### Ziele

**[!UICONTROL Ziele]** gibt die Gesamtzahl der Ziele an, die für das Unternehmen erstellt wurden. Diese Zahl wird aktualisiert, sobald neue Ziele erstellt werden.

Weiterführende Informationen zu Zielen finden Sie unter [Zielübersicht](destinations/destinations-overview.md).

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

Auf der Karte **[!UICONTROL Letzte Datensätze]** werden die fünf letzten Datensätze angezeigt, die im Unternehmen erstellt wurden. Diese Liste wird aktualisiert, sobald ein neuer Datensatz erstellt wird.

Klicken Sie auf einen Datensatz, um die Details zu diesem Element anzuzeigen, oder auf **[!UICONTROL Alle anzeigen]**, um die Liste der Datensätze anzuzeigen. Hier können Sie auf eine bestimmte Quelle klicken, um weitere Details aufzurufen.

Weiterführende Informationen über Datensätze finden Sie in der [Datensatzübersicht](../catalog/datasets/overview.md).

### Letzte Quellen

Auf der Metrikkarte **[!UICONTROL Letzte Quellen]** werden die fünf Quellen angezeigt, die im Unternehmen zuletzt erstellt wurden. Diese Liste wird aktualisiert, sobald eine neue Quelle erstellt wird.

Klicken Sie auf eine Quelle, um die Details zu diesem Element anzuzeigen, oder auf **[!UICONTROL Alle anzeigen]**, um die Liste der Quellen anzuzeigen. Hier können Sie auf eine bestimmte Quelle klicken, um weitere Details aufzurufen.

Weiterführende Informationen zu Quellen finden Sie in der [Quellenübersicht](sources/sources-overview.md).

### Letzte Segmente

Auf der Metrikkarte **[!UICONTROL Letzte Segmente]** werden die fünf Segmente angezeigt, die im Unternehmen zuletzt erstellt wurden. Diese Liste wird aktualisiert, sobald ein neues Segment erstellt wird.

Klicken Sie auf ein Segment, um die Details zu diesem Element anzuzeigen, oder auf **[!UICONTROL Alle anzeigen]**, um Informationen über weitere Segmente zu erhalten.

Weiterführende Informationen zu Segmenten finden Sie unter [Segmentierungsdienst – Übersicht](segmentation/segmentation-overview.md).

### Letzte Ziele

Auf der Metrikkarte **[!UICONTROL Letzte Ziele]** werden die fünf Ziele angezeigt, die im Unternehmen zuletzt erstellt wurden. Diese Liste wird aktualisiert, sobald ein neues Ziel erstellt wird.

Klicken Sie auf ein Ziel, um die Details zu diesem Element anzuzeigen, oder auf **[!UICONTROL Alle anzeigen]**, um Informationen über weitere Ziele zu erhalten.

Weiterführende Informationen zu Zielen finden Sie unter [Zielübersicht](destinations/destinations-overview.md).
