---
keywords: Metriken - Übersicht; Übersicht über rtcdp-Metriken
title: Real-time Customer Data Platform-Homepage und Dashboards
description: Erhalten Sie ein Verständnis für die verschiedenen Dashboards, die Startseite und die ersten Benutzererfahrungen mit Adobe Real-Time CDP.
feature: Dashboards, Get Started
exl-id: ced5b69c-5bb5-4e06-9cb4-938e36e6e5cc
source-git-commit: 2704184446f7945c744e7e2d2a8c3cda3fc12527
workflow-type: tm+mt
source-wordcount: '919'
ht-degree: 10%

---

# [!DNL Real-Time Customer Data Platform] Homepage

Die Startseite von Adobe Real-time Customer Data Platform (Real-Time CDP) ist die erste Seite, die nach der Anmeldung bei Real-Time CDP angezeigt wird.

Die Real-Time CDP-Startseite enthält ein Widget &quot;Erste Schritte&quot;, mit dem Sie schnell auf verschiedene Funktionen zugreifen können, sowie einen Metrikabschnitt, der aktuelle Informationen zu Daten in Ihrem Unternehmen anzeigt.

Dieses Dokument bietet einen Überblick über die Real-Time CDP-Startseite und das Dashboard für Metriken.

![Startseite der Platform-Benutzeroberfläche.](assets/platform-home/home.png)

## Widget &quot;Erste Schritte&quot;

Das Widget [!UICONTROL Erste Schritte mit dem Echtzeit-Kundenprofil] ist in vier Abschnitte unterteilt:

* **Aufnehmen von Daten in Platform**: Dieses Widget leitet Sie zum Quellkatalog. Wählen Sie im Quellkatalog eine Quelle aus und erfassen Sie Ihre Daten auf Experience Platform. Wählen Sie **[Quellen konfigurieren]** aus, um zum Quellkatalog zu navigieren. Weitere Informationen finden Sie in der [Quellenübersicht](../sources/home.md).
* **Modelldatenstrukturen**: Dieses Widget leitet Sie zur Übersicht über Schemata. Verwenden Sie die Übersicht über Schemata , um nach vorhandenen Schemata zu suchen oder einen Entwurf zu erstellen, der die Struktur Ihrer Daten beschreibt. Wählen Sie **[!UICONTROL Schema erstellen]** aus, um zur Benutzeroberfläche zur Schemaerstellung zu navigieren. Weitere Informationen finden Sie in der [Übersicht über Schemas](../xdm/home.md).
* **Erstellen von Zielgruppen**: Dieses Widget leitet Sie zum Segment Builder in der Benutzeroberfläche. Verwenden Sie den Segmentaufbau, um mit Profildatenelementen zu interagieren und die Kriterien für Ihre Segmentdefinition zu definieren. Wählen Sie **[!UICONTROL Zielgruppe erstellen]** aus, um zum Segment Builder zu navigieren. Weitere Informationen finden Sie in der Übersicht über den [Segmentation Service](../segmentation/home.md) .
* **Daten an Ziele senden**: Dieses Widget leitet Sie zum Zielkatalog. Verwenden Sie den Zielkatalog, um ein Ziel auszuwählen, mit dem Sie dann eine Verbindung herstellen und Zielgruppen senden können. Wählen Sie **[!UICONTROL Ziele einrichten]** aus, um zum Zielkatalog zu navigieren. Weitere Informationen finden Sie in der [Zielübersicht](../destinations/home.md).

![Die Startseite der Platform-Benutzeroberfläche mit dem Widget &quot;Erste Schritte&quot;](assets/platform-home/getting-started-widget.png)

## Metriken-Dashboard {#metrics-dashboard}

>[!CONTEXTUALHELP]
>id="platform_home_metrics_totalProfiles"
>title="Gesamtanzahl der Profile"
>abstract="Die Gesamtanzahl der Profile, die Ihr Unternehmen innerhalb von Experience Platform hat. Diese Anzahl basiert auf der Zusammenführungsrichtlinie Ihres Unternehmens und umfasst keine Profilfragmente. Die Zahl der Profile wird alle 24 Stunden aktualisiert."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/ui/user-guide.html?lang=de#profile-count" text="Weitere Informationen finden Sie in der Dokumentation"

Das Metriken-Dashboard zeigt aktuelle Informationen zu Ihren Experience Platform-Daten an. Das Dashboard ist in zwei Bereiche unterteilt:

### Die Leaderboard

Das Leaderboard zeigt die aktuelle Gesamtzahl der Schemas, Datensätze, Profile und Zielgruppen in Ihrer Organisation sowie das aktuelle Aktualisierungsdatum an.

![Der Leaderboard-Abschnitt auf der Startseite der Platform-Benutzeroberfläche.](assets/platform-home/leaderboard.png)

* **Schemas insgesamt**: Der Zähler **Schemas insgesamt** zeigt die Anzahl der Schemas im System an. Dieser Zähler wird bei der Erstellung eines Schemas aktualisiert. Weitere Informationen finden Sie in der [Übersicht über Schemas](../xdm/home.md).
* **Datensätze insgesamt**: Der Zähler für die **Datensätze insgesamt** zeigt die Anzahl der Datensätze im System und die Datenmenge im Experience Platform an. Dieser Zähler wird bei der Erstellung eines Datensatzes aktualisiert. Weitere Informationen zu Datensätzen finden Sie in der [Datensatzübersicht](../catalog/datasets/overview.md).
* **Profile insgesamt**: Die Anzahl der **Profile** gibt die Gesamtanzahl der Profile an, die Ihr Unternehmen auf Experience Platform hat. Profilfragmente werden nicht einbezogen. Dies ist Ihre gesamte adressierbare Zielgruppe. Diese Anzahl verwendet die standardmäßige [Zusammenführungsrichtlinie](profile/merge-policies.md), die in der Konfiguration der Zusammenführungsrichtlinien im Echtzeit-Kundenprofil festgelegt ist. Die Anzahl der Profile wird alle 24 Stunden aktualisiert. Wählen Sie **[!UICONTROL Profile]** aus, um zur Seite Profilübersicht zu navigieren und alle Profilmetriken anzuzeigen. Weitere Informationen zu Profilen finden Sie in der [Übersicht über das Echtzeit-Kundenprofil](../profile/home.md).
* **Gesamtzielgruppen**: Der Zähler **Gesamtzielgruppen** zeigt die Gesamtanzahl der für Ihre Organisation erstellten Zielgruppen an. Diese Zahl wird bei der Erstellung neuer Zielgruppen aktualisiert. Weitere Informationen zu Zielgruppen finden Sie in der Übersicht über den [Segmentation Service](../segmentation/home.md) .

### Letzte Elemente

Unter Letzte Elemente werden die neuesten Änderungen in Ihrer Organisation aufgeführt. Im folgenden Beispiel beziehen sich die letzten Änderungen auf Datensätze, Quellen, Zielgruppen und Ziele.

![Der Abschnitt zu den letzten Elementen auf der Startseite der Platform-Benutzeroberfläche.](assets/platform-home/recent-items.png)

* **Letzte Datensätze**: Auf der Karte **[!UICONTROL Letzte Datensätze]** werden die fünf letzten Datensätze angezeigt, die innerhalb der Organisation erstellt wurden. Diese Liste wird aktualisiert, wenn ein neuer Datensatz erstellt wird. Wählen Sie einen Datensatz aus, um die Details zu diesem Element anzuzeigen, oder wählen Sie **[!UICONTROL Alle anzeigen]** für eine Liste von Datensätzen aus. Dort können Sie eine bestimmte Quelle für Details auswählen. Weiterführende Informationen über Datensätze finden Sie in der [Datensatzübersicht](../catalog/datasets/overview.md).
* **Letzte Quellen**: Auf der Metrikkarte **[!UICONTROL Letzte Quellen]** werden die fünf Quellen angezeigt, die im Unternehmen zuletzt erstellt wurden. Diese Liste wird aktualisiert, wenn eine neue Quelle erstellt wird. Wählen Sie eine Quelle aus, um die Details für dieses Element anzuzeigen, oder wählen Sie **[!UICONTROL Alle anzeigen]** für eine Liste von Quellen. Dort können Sie eine bestimmte Quelle für Details auswählen. Weiterführende Informationen zu Quellen finden Sie in der [Quellenübersicht](../sources/home.md).
* **Letzte Zielgruppen**: Auf der Metrikkarte **[!UICONTROL Letzte Zielgruppen]** werden die fünf zuletzt im Unternehmen erstellten Zielgruppen angezeigt. Diese Liste wird aktualisiert, wenn eine neue Zielgruppe erstellt wird. Wählen Sie eine Zielgruppe aus, um die Details zu diesem Element anzuzeigen, oder wählen Sie für eine Zielgruppenliste die Option **[!UICONTROL Alle anzeigen]** aus. Weitere Informationen zu Zielgruppen finden Sie unter [Segmentation Service - Übersicht](../segmentation/home.md).
* **Letzte Ziele**: Auf der Metrikkarte **[!UICONTROL Letzte Ziele]** werden die fünf Ziele angezeigt, die im Unternehmen zuletzt erstellt wurden. Diese Liste wird aktualisiert, wenn ein neues Ziel erstellt wird. Wählen Sie ein Ziel aus, um die Details für dieses Element anzuzeigen, oder wählen Sie **[!UICONTROL Alle anzeigen]** für eine Liste von Zielen. Weitere Informationen finden Sie in der [Zielübersicht](../destinations/home.md).

## Ressourcen

Schließlich bietet Ihnen das Ressourcen-Widget zusätzliche Dokumentationsressourcen, auf die Sie verweisen können. Dazu gehören:

![Der Ressourcenabschnitt auf der Startseite der Platform-Benutzeroberfläche.](assets/platform-home/resources.png)

* [Verstehen von Schemata](../xdm/schema/composition.md)
* [Verbinden von Quellen](../sources/home.md)
* [So füllen Sie Ihr Echtzeit-Kundenprofil aus](../profile/home.md)
* [Verbinden von Zielen](../destinations/home.md)
* [Verwalten des Zugriffs](../access-control/abac/overview.md)

<!-- ### Successful profile records

In the leaderboard **[!UICONTROL Successful profile records]** shows the total number of records that have been successfully processed into the profile.

There is also a metric card that shows the percentage of successful records. Select **[!UICONTROL View datasets]** to see more details about the profile records. Hover over the colored area of the graph to see additional details:

![image](assets/home-profilerecords-details.PNG)

The number of successful profile records is updated hourly. 

For more information about profiles, see [A unified view of your customer in Real-Time CDP](profile/profile-overview.md).

### Total profile records

The **[!UICONTROL Total profile records]** metric card shows the total number of data records enabled to feed into the profiles, and the percentage that are successful, updated once per day. This does not include all data in the data lake, because some data might not be enabled to feed into the profiles.

 Hover over the colored area of the graph to see additional details about the successful profiles:

![image](assets/home-profile-details.PNG)

Select **[!UICONTROL View profiles]** to see more details about the profile records.

For more information about profiles, see [A unified view of your customer in Real-Time CDP](profile/profile-overview.md).

For more information about viewing a specific profile, see [Profile viewer](profile/profile-viewer.md).

### Failed profile records

In the leaderboard, **[!UICONTROL Failed profile records]** counts the number of records that failed to process into the profile.

The **[!UICONTROL Failed profile records]** metric card shows this count, and includes a graphical representation that helps you see how failures have trended during the time shown below the graphic. This chart is updated hourly. Select **[!UICONTROL View datasets]** to see more details about the profile records.

The number of failed profile records is updated hourly. -->
