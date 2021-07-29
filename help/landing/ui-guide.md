---
keywords: Experience Platform; Startseite; beliebte Themen; Adobe Experience Platform; Benutzerhandbuch; Benutzerhandbuch; Handbuch zur Plattform-Benutzeroberfläche; Einführung in die Plattform; Dashboard
solution: Experience Platform
title: Übersicht über die Experience Platform-Benutzeroberfläche
topic-legacy: ui guide
description: Adobe Experience Platform
exl-id: 47f9a3fb-731d-4ade-8069-faaa18f224dc
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '1755'
ht-degree: 4%

---

# Handbuch zur Benutzeroberfläche von Adobe Experience Platform

Dieses Handbuch bietet eine Einführung in die Verwendung der Adobe Experience Platform-Benutzeroberfläche, die erklärt, wofür die verschiedenen Komponenten verwendet werden, und Links zu weiteren Dokumentationen mit weiteren Informationen.

Weitere Informationen zu Adobe Experience Platform finden Sie unter [Übersicht über die Experience Platform](home.md).

## Startbildschirm

Nach der Anmeldung bei Adobe Experience Platform befinden Sie sich auf der Seite [!UICONTROL Home], die aus dem [Metriken-Dashboard](#metrics), [aktuellen Daten](#recent-data) und den Abschnitten [Empfohlenes Lernen](#recommended-learning) besteht.

![](images/user-guide/homepage.png)

### Metriken

Das Metriken-Dashboard bietet Karten mit Informationen zu Datensätzen, Profilen, Segmenten und Zielen in Ihrer Organisation.

![](images/user-guide/homepage-dashboard.png)

Im Abschnitt **[!UICONTROL Datensätze]** wird die Anzahl der Datensätze innerhalb Ihrer IMS-Organisation angezeigt. Diese Zahl wird aktualisiert, wenn ein neuer Datensatz erstellt wird. Weitere Informationen zu Datensätzen finden Sie in der [Datensatzübersicht](../catalog/datasets/overview.md).

Im Abschnitt **[!UICONTROL Profile]** wird die Gesamtzahl der Personen mit Profilen innerhalb Ihrer IMS-Organisation angezeigt, ausgenommen Profilfragmente. Diese Gesamtzahl an Personen stellt die gesamte adressierbare Zielgruppe dar und wird alle 24 Stunden aktualisiert. Weitere Informationen zu Profilen finden Sie in der [Übersicht über das Echtzeit-Kundenprofil](../profile/home.md).

Im Abschnitt **[!UICONTROL Segmente]** wird die Gesamtzahl der innerhalb Ihrer IMS-Organisation erstellten Segmente angezeigt. Diese Zahl wird bei der Erstellung eines neuen Segments aktualisiert. Weitere Informationen zu Segmenten finden Sie unter [Segmentation Service - Übersicht](../segmentation/home.md).

Im Abschnitt **[!UICONTROL Ziele]** wird die Gesamtzahl der Ziele angezeigt, die für die IMS-Organisation erstellt wurden. Diese Zahl wird aktualisiert, wenn ein neues Ziel erstellt wird. Weitere Informationen zu Zielen finden Sie in der [Zielübersicht](../destinations/home.md).

### Letzte Daten

Das Daten-Dashboard der letzten Zeit enthält Informationen zu kürzlich erstellten Datensätzen, Quellen, Segmenten und Zielen.

![](images/user-guide/homepage-recent.png)

Im Abschnitt **[!UICONTROL Letzte Datensätze]** werden die fünf zuletzt erstellten Datensätze in Ihrer IMS-Organisation aufgelistet. Diese Liste wird jedes Mal aktualisiert, wenn ein neuer Datensatz erstellt wird. Sie können einen Datensatz aus der Liste auswählen, um weitere Informationen zum angegebenen Datensatz anzuzeigen, oder **[!UICONTROL Alle anzeigen]** auswählen, um eine Liste aller erstellten Datensätze anzuzeigen. Weitere Informationen zu Datensätzen finden Sie in der [Datensatzübersicht](../catalog/datasets/overview.md).

Im Abschnitt **[!UICONTROL Letzte Quellen]** werden die fünf zuletzt erstellten Quell-Connectoren innerhalb Ihrer IMS-Organisation aufgelistet. Diese Liste wird jedes Mal aktualisiert, wenn ein neuer Quell-Connector erstellt wird. Sie können eine Quellverbindung aus der Liste auswählen, um weitere Informationen zum angegebenen Connector anzuzeigen, oder **[!UICONTROL Alle anzeigen]** auswählen, um eine Liste aller erstellten Quellverbindungen anzuzeigen. Weitere Informationen zu Quellen finden Sie in der [Quellenübersicht](../sources/home.md).

Im Abschnitt **[!UICONTROL Letzte Segmente]** werden die fünf zuletzt erstellten Segmentdefinitionen in Ihrer IMS-Organisation aufgelistet. Diese Liste wird jedes Mal aktualisiert, wenn eine neue Segmentdefinition erstellt wird. Sie können eine Segmentdefinition aus der Liste auswählen, um weitere Informationen zur angegebenen Segmentdefinition anzuzeigen, oder **[!UICONTROL Alle anzeigen]** auswählen, um eine Liste aller erstellten Segmentdefinitionen anzuzeigen. Weitere Informationen zu Segmenten finden Sie unter [Segmentation Service - Übersicht](../segmentation/home.md).

Im Abschnitt **[!UICONTROL Letzte Ziele]** werden die fünf Ziele aufgelistet, die Sie in Ihrer IMS-Organisation zuletzt erstellt haben. Diese Liste wird jedes Mal aktualisiert, wenn ein neues Ziel erstellt wird. Sie können ein Ziel aus der Liste auswählen, um weitere Informationen zum angegebenen Ziel anzuzeigen, oder **[!UICONTROL Alle anzeigen]** auswählen, um eine Liste aller erstellten Ziele anzuzeigen. Weitere Informationen zu Zielen finden Sie in der [Zielübersicht](../destinations/home.md).

### Empfohlenes Lernen

Der Abschnitt **[!UICONTROL Empfohlenes Lernen]** enthält Links zu nützlichen Dokumentationen zu den ersten Schritten mit Adobe Experience Platform.

![](images/user-guide/homepage-recommended.png)

## Navigationsleiste oben

In der oberen Navigationsleiste der Platform-Benutzeroberfläche wird die IMS-Organisation angezeigt, bei der Sie sich derzeit angemeldet haben, und es werden verschiedene wichtige Steuerelemente bereitgestellt.

Auf der linken Seite der Navigationsleiste befindet sich das Adobe Experience Platform-Logo. Wenn Sie diese Option jederzeit auswählen, kehren Sie zum Startbildschirm der Platform-Benutzeroberfläche zurück.

![](./images/user-guide/homepage-top-nav-bar.png)

### IMS-Organisationswechsel

Das erste Element auf der rechten Seite der oberen Navigationsleiste ist der **IMS-Organisationsschalter**.

![](./images/user-guide/homepage-ims-org.png)

Wenn Sie den Umschalter auswählen, wird ein Dropdown-Menü mit IMS-Organisationen geöffnet, auf die Sie Zugriff haben, sofern verfügbar. Wählen Sie eine aufgelistete Option aus, um zu dieser IMS-Organisation zu wechseln.

![](./images/user-guide/homepage-ims-org-switcher.png)

### Wechseln von Anwendungen

Das nächste Element auf der rechten Seite der oberen Navigation ist der **Anwendungsschalter**, der durch das Symbol ![Anwendungsschalter](./images/user-guide/app-switcher-icon.png) dargestellt wird. Wenn Sie dieses Symbol auswählen, können Sie zwischen Adobe-Anwendungen, auf die Ihre IMS-Organisation Zugriff hat, wie z. B. Experience Platform, Analytics, Assets und andere wechseln.

### Hilfe

Rechts neben dem Anwendungsschalter befindet sich das **Hilfe- und Support-Menü**, das durch das Symbol ![Fragezeichen/help](./images/user-guide/help-icon.png) dargestellt wird. Wenn Sie dieses Symbol auswählen, wird ein Popover-Menü mit mehreren Hilfe- und Support-Ressourcen angezeigt. Die Registerkarte **[!UICONTROL Hilfe]** enthält eine Liste der relevanten Dokumentation für die Seite, auf der Sie sich gerade befinden. Mit dem Tab **[!UICONTROL Support]** können Sie ein Support-Ticket für das Adobe-Supportteam erstellen. Im Tab **[!UICONTROL Feedback]** können Sie Feedback zu Platform an Adobe senden.

![](images/user-guide/homepage-help-clicked.png)

### Benachrichtigungen und Ankündigungen

Im Abschnitt **Benachrichtigungen**, der durch das Symbol ![bell/Notifications und Announcements](images/user-guide/notification-icon.png) dargestellt wird. Der Tab **[!UICONTROL Benachrichtigungen]** enthält wichtige Informationen zum Produkt und anderen relevanten Aktualisierungen, während der Tab **[!UICONTROL Mitteilungen]** Informationen zur Serviceverwaltung anzeigt.

### Benutzerprofil

Das letzte Element auf der oberen Navigationsleiste sind die **Benutzereinstellungen**, die durch das Symbol ![Benutzereinstellungen/Benutzerprofil](images/user-guide/profile-icon.png) dargestellt werden. Wählen Sie dieses Symbol aus, um Ihre Voreinstellungen zu bearbeiten oder sich abzumelden.

### Sandboxes

Unmittelbar unterhalb der oberen Navigationsleiste befindet sich die Sandbox-Leiste. Diese Leiste zeigt, welche Sandbox Sie derzeit für Platform verwenden. Weitere Informationen zu Sandboxes finden Sie in der [Sandbox-Übersicht](../sandboxes/home.md).

## Linke Navigation {#left-nav}

Im Navigationsbereich auf der linken Bildschirmseite werden alle Dienste aufgelistet, die in der Platform-Benutzeroberfläche unterstützt werden.

>[!IMPORTANT]
>
>Einige der Abschnitte auf der linken Navigationsleiste werden möglicherweise nicht grau dargestellt. Dies liegt daran, dass Sie keinen Zugriff auf diese Funktionen haben. Wenn Sie glauben, dass Sie Zugriff auf diese Abschnitte haben sollten, wenden Sie sich an Ihren Systemadministrator.

![](images/user-guide/homepage-left.png)

Im Abschnitt **[!UICONTROL Home]** können Sie zur Startseite der Platform-Benutzeroberfläche zurückkehren.

Der Abschnitt **[!UICONTROL Workflows]** enthält eine Liste mit mehrstufigen Workflows für die Ausführung von Vorgängen in Platform. Weitere Informationen zu Workflows finden Sie in der [Übersicht über Workflows](./workflows.md).

### [!UICONTROL Verbindungen]

Im Abschnitt **[!UICONTROL Quellen]** können Sie Quellverbindungen erstellen, aktualisieren und löschen, sodass Sie Daten aus externen Quellen in Platform erfassen können. Weitere Informationen zu Quellen finden Sie in der [Quellenübersicht](../sources/home.md).

Im Abschnitt **[!UICONTROL Ziele]** können Sie Ziele erstellen, aktualisieren und löschen, sodass Sie Daten aus Platform in viele externe Ziele exportieren können. Weitere Informationen zu Zielen finden Sie in der [Zielübersicht](../destinations/home.md).

### [!UICONTROL Kunde]

Im Abschnitt **[!UICONTROL Profile]** können Sie Kundenprofile durchsuchen, Profilmetriken anzeigen, Zusammenführungsrichtlinien erstellen und verwalten und Vereinigungsschemata anzeigen. Weitere Informationen zur Verwendung des Abschnitts [!UICONTROL Profile] finden Sie im [[!DNL Profile] Benutzerhandbuch](../profile/ui/user-guide.md). Weitere Informationen zum Echtzeit-Kundenprofil finden Sie in der [Übersicht zum Echtzeit-Kundenprofil](../profile/home.md).

Im Abschnitt **[!UICONTROL Segmente]** können Sie Segmentdefinitionen erstellen und verwalten. Weitere Informationen zur Verwendung des Abschnitts [!UICONTROL Segmente] finden Sie im [Benutzerhandbuch zur Segmentierung](../segmentation/ui/overview.md). Weitere Informationen zum Segmentation Service finden Sie unter [Segmentation Service - Übersicht](../segmentation/home.md).

Im Abschnitt **[!UICONTROL Identitäten]** können Sie Identitäts-Namespaces erstellen und verwalten. Weitere Informationen zum Abschnitt [!UICONTROL Identitäten], einschließlich Informationen zu Identitäts-Namespaces und zur Verwendung von Identitäten in der Platform-Benutzeroberfläche, finden Sie in der [Übersicht über Identitäts-Namespaces](../identity-service/namespaces.md).

### [!UICONTROL Datenschutz]

Im Abschnitt **[!UICONTROL Richtlinien]** können Sie Datennutzungsrichtlinien erstellen und verwalten. Weitere Informationen zur Verwendung des Abschnitts Richtlinien finden Sie im Benutzerhandbuch zu Datennutzungsrichtlinien [a1/>. ](../data-governance/policies/user-guide.md) Weitere Informationen zu Datennutzungsrichtlinien finden Sie unter [Übersicht über Datennutzungsrichtlinien](../data-governance/policies/overview.md).

Im Abschnitt **[!UICONTROL Requests]** können Sie Datenschutzanfragen erstellen und verwalten. Beachten Sie, dass Sie auf die Zulassungsliste gesetzt sein müssen, um Zugriff auf die Benutzeroberfläche von Privacy Service zu erhalten. Weitere Informationen zur Verwendung des Abschnitts Anforderungen finden Sie im [Privacy Service-Benutzerhandbuch](../privacy-service/ui/user-guide.md). Weitere Informationen zu Privacy Service finden Sie in der [Übersicht über Privacy Service](../privacy-service/home.md).

### [!UICONTROL Data Science]

Der Abschnitt **[!UICONTROL Notebooks]** bietet Zugriff auf JupyterLab, eine interaktive Entwicklungsumgebung, mit der Sie Ihre Daten untersuchen, analysieren und modellieren können. Weitere Informationen zur Verwendung des Abschnitts Notebooks finden Sie im [JupyterLab-Benutzerhandbuch](../data-science-workspace/jupyterlab/overview.md). Weitere Informationen zu Data Science Workspace finden Sie in der [Übersicht über Data Science Workspace](../data-science-workspace/home.md)

Im Abschnitt **[!UICONTROL Modelle]** können Sie maschinelles Lernen und künstliche Intelligenz nutzen, um Modelle zu erstellen, zu entwickeln, zu trainieren und anzupassen, um Prognosen zu erstellen. Weitere Informationen zum Abschnitt Modelle finden Sie im Tutorial zum [Trainieren und Auswerten eines Modells](../data-science-workspace/models-recipes/train-evaluate-model-ui.md).

Im Abschnitt **[!UICONTROL Dienste]** können Sie Ihre veröffentlichten Modelle für geplante Schulungen und Auswertungen verwalten oder die Intelligent Services von Adobe nutzen, eine Reihe von KI-Diensten, die Echtzeit-Kundenerlebnisse bieten. Weitere Informationen zum Abschnitt &quot;Dienste&quot;finden Sie im Tutorial [Modell als Dienst veröffentlichen](../data-science-workspace/models-recipes/publish-model-service-ui.md).

### [!UICONTROL Daten-Management]

Im Abschnitt **[!UICONTROL Schemas]** können Sie Experience-Datenmodell (XDM)-Schemas erstellen und verwalten. Weitere Informationen zu Schemata finden Sie im Tutorial zum Erstellen eines Schemas](../xdm/tutorials/create-schema-ui.md). [ Weitere Informationen zu XDM finden Sie in der [XDM-Systemübersicht](../xdm/home.md).

Im Abschnitt **[!UICONTROL Datensätze]** können Sie Datensätze erstellen und verwalten. Weitere Informationen zu Datensätzen finden Sie im [Benutzerhandbuch zu Datensätzen](../catalog/datasets/user-guide.md).

Im Abschnitt **[!UICONTROL Abfragen]** können Sie Abfragen erstellen und verwalten, SQL-Abfragen von Adobe Experience Platform Query Service protokollieren und Ihre PostgreSQL-Anmeldeinformationen anzeigen. Weitere Informationen zu Abfragen finden Sie im [Query Service-Benutzerhandbuch](../query-service/ui/overview.md).

Im Abschnitt **[!UICONTROL Monitoring]** können Sie die Batch- und Streaming-Erfassung überwachen. Weitere Informationen zur Überwachung finden Sie im [Benutzerhandbuch zur Überwachung der Datenerfassung](../ingestion/quality/monitor-data-ingestion.md).

### [!UICONTROL Entscheidungsfindung]

Offer Decisioning ist ein in Adobe Experience Platform integrierter Anwendungsdienst. Damit können Sie Experience Platform nutzen, um Kunden zur richtigen Zeit und an allen Berührungspunkten das optimale Angebot und Erlebnis zu unterbreiten. Weitere Informationen zum Offer decisioning, einschließlich der Arbeit mit [!UICONTROL Angeboten] und [!UICONTROL Aktivitäten] finden Sie in der [Offer decisioning-Dokumentation](https://experienceleague.adobe.com/docs/offer-decisioning.html?lang=de).

### [!UICONTROL Administration]

Die Platform-Benutzeroberfläche bietet ein Dashboard, über das Sie wichtige Informationen zur Lizenznutzung Ihres Unternehmens anzeigen können, wie sie in einer täglichen Momentaufnahme erfasst werden. Sie können darauf zugreifen, indem Sie in der Navigation **[!UICONTROL Lizenznutzung]** auswählen. Weitere Informationen zum Dashboard zur Lizenznutzung finden Sie im [Dashboard zur Lizenznutzung](license-usage-dashboard.md).

>[!IMPORTANT]
>
>Die Dashboard-Funktion zur Lizenznutzung befindet sich derzeit in der Alpha-Phase und steht nicht allen Benutzern zur Verfügung. Die Dokumentation und Funktionalität können sich ändern.

## Nächste Schritte

Durch Lesen dieses Handbuchs wurden Sie nun mit der Startseite und den wichtigsten Navigationselementen der Platform-Benutzeroberfläche vertraut gemacht. Weiterführende Informationen zur Arbeit in der Benutzeroberfläche finden Sie in der Dokumentation für jeden einzelnen Platform-Dienst. Links zu dieser Dokumentation finden Sie im Abschnitt [Linke Navigation](#left-nav) weiter oben in diesem Dokument.
