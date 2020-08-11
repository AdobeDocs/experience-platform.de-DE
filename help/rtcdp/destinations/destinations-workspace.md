---
title: Arbeitsbereich „Ziele“
seo-title: Arbeitsbereich „Ziele“
description: Wählen Sie in der Echtzeit-Kundendatenplattform von Adobe in der linken Navigationsleiste die Option „Ziele“, um auf den Arbeitsbereich „Ziele“ zuzugreifen.
seo-description: Wählen Sie in der Echtzeit-Kundendatenplattform von Adobe in der linken Navigationsleiste die Option „Ziele“, um auf den Arbeitsbereich „Ziele“ zuzugreifen.
translation-type: tm+mt
source-git-commit: f3e489416a9bc80cfb0502d3973a86748123a687
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 61%

---


# Arbeitsbereich „Ziele“ {#destinations-workspace}

Wählen Sie in der Echtzeit-Kundendatenplattform von Adobe in der linken Navigationsleiste die Option **[!UICONTROL Ziele]**, um auf den Arbeitsbereich [!UICONTROL Ziele] zuzugreifen.

Der Arbeitsbereich [!UICONTROL Ziele] besteht aus vier Bereichen: **[!UICONTROL Katalog]**, **[!UICONTROL Durchsuchen]**, **[!UICONTROL Konten]** und **[!UICONTROL Systemansicht]**. Diese werden in den folgenden Abschnitten beschrieben.

![Zielüberblick](/help/rtcdp/destinations/assets/destinations-overview.png)

## [!UICONTROL Katalog] {#catalog}

The **[!UICONTROL Catalog]** tab displays a list of all destinations available in Adobe Real-time CDP, that you can send data to.

Die CDP-Benutzeroberfläche &quot;Adobe in Echtzeit&quot;bietet eine Reihe von Such- und Filteroptionen auf der Zielkatalogseite:

* Verwenden Sie die Suchfunktion auf der Seite, um ein bestimmtes Ziel zu finden.
* Filtern Sie Ziele mithilfe des Steuerelements **[!UICONTROL Kategorien]** .
* Toggle between **[!UICONTROL All destinations]** and **[!UICONTROL My destinations]**. Wenn &quot; **[!UICONTROL Alle Ziele]** &quot;ausgewählt ist, werden alle verfügbaren CDP-Ziele für Adoben in Echtzeit angezeigt. Wenn **[!UICONTROL Meine Ziele]** ausgewählt sind, können Sie nur die Ziele sehen, zu denen Sie eine Verbindung hergestellt haben.
* Select to view **[!UICONTROL Connections]** and/or **[!UICONTROL Extensions]**. Informationen zum Unterschied zwischen den beiden Kategorien finden Sie unter [Zieltypen und Kategorien](/help/rtcdp/destinations/destination-types.md).

![Filtern und Suchdemo von Zielen](/help/rtcdp/destinations/assets/destinations-search-and-filter.gif)

Die Zielkarten enthalten entweder ein **[!UICONTROL Configure]** - oder ein **[!UICONTROL Activate]** -Steuerelement und ein sekundäres Steuerelement, das mehr Optionen aufruft. Diese sind alle nachstehend beschrieben:

| Kontrolle | Beschreibung |
---------|----------
| [!UICONTROL Konfigurieren] | Ermöglicht Ihnen das Erstellen einer Verbindung mit dem Ziel. |
| [!UICONTROL Aktivieren] | Nachdem Sie eine Verbindung zum Ziel hergestellt haben, können Sie Segmente aktivieren. |
| [!UICONTROL Ansichten-Konto] | Ansicht der Konten, die Sie für ein Ziel verbunden haben. |
| [!UICONTROL Ansicht DataFlows] | View the data activation flows that exist for a destination |
| [!UICONTROL Dokumentation zur Ansicht] | Öffnet einen Link zur Dokumentationsseite für dieses spezifische Ziel, um weitere Informationen zu erhalten und die Einrichtung zu erleichtern. |

![Steuerelemente auf der Zielkarte](/help/rtcdp/destinations/assets/destination-card-options.png)

Select a destination card in the catalog to open the right rail.  Hier sehen Sie eine Beschreibung des Ziels. Die rechte Leiste bietet dieselben in der obigen Tabelle beschriebenen Steuerelemente sowie eine Beschreibung des Ziels und eine Angabe der Kategorie und des Typs des Ziels.

![Optionen im Zielkatalog](/help/rtcdp/destinations/assets/destination-right-rail.png)

Weitere Informationen zu den Ziel-Kategorien und Informationen zu den einzelnen Zielen finden Sie im [Zielkatalog](/help/rtcdp/destinations/destinations-catalog.md) und in den [Zieltypen und Kategorien](/help/rtcdp/destinations/destination-types.md).

## [!UICONTROL Durchsuchen] {#browse}

Auf der Registerkarte **[!UICONTROL Durchsuchen]** werden die Ziele angezeigt, mit denen Sie eine Verbindung hergestellt haben. Ziele, bei denen der Umschalter **[!UICONTROL Aktiviert]** aktiviert ist, setzen das Ziel auf „aktiv“ und umgekehrt. You can also view the destinations where you have data flowing by selecting **[!UICONTROL Segments]** > **[!UICONTROL Browse]** and selecting a segment to inspect. Die nachstehende Tabelle enthält alle Informationen, die für die einzelnen Ziele auf der Registerkarte „Durchsuchen“ verfügbar sind:

![Registerkarte „Durchsuchen“](/help/rtcdp/destinations/assets/browse-tab.png)

| Element | Beschreibung |
---------|----------
| Name | Der Name, den Sie für den Aktivierungsfluss zu diesem Ziel angegeben haben. |
| [!UICONTROL Ziel] | Die Zielplattform, die Sie für Ihren Aktivierungsfluss ausgewählt haben. |
| [!UICONTROL Verbindungstyp] | Stellt den Verbindungstyp zu Ihrem Speicher-Bucket oder Ziel dar. <ul><li>Bei E-Mail-Marketing-Zielen: Kann S3 oder FTP sein.</li><li>Bei Echtzeit-Werbezielen: Server-zu-Server.</li></ul> |
| [!UICONTROL Benutzername] | Die Kontoanmeldedaten, die Sie für den Zielfluss ausgewählt haben. |
| [!UICONTROL Segmente] | Die Zahl der Segmente, die für dieses Ziel aktiviert werden. |
| [!UICONTROL Erstellt] | Datum und Uhrzeit (UTC) der Erstellung des Aktivierungsflusses zum Ziel. |
| [!UICONTROL Status] | `Active` oder `Inactive`. Gibt an, ob für dieses Ziel derzeit Daten aktiviert sind. Informationen zum Bearbeiten des Status finden Sie unter [Aktivierung deaktivieren](/help/rtcdp/destinations/activate-destinations.md#disable-activation). |

Klicken Sie auf eine Zielzeile, um weitere Informationen zum Ziel in der rechten Leiste anzuzeigen.

![Auf Zielzeile klicken](/help/rtcdp/destinations/assets/click-destination-row.png)

Wählen Sie den Zielnamen aus, um Informationen zu den für dieses Ziel aktivierten Segmenten anzuzeigen. Klicken Sie auf **[!UICONTROL Aktivierung bearbeiten]**, um die Segmente, die an dieses Ziel gesendet werden, zu ändern oder hinzuzufügen.

## [!UICONTROL Konten] {#accounts}

Auf der Registerkarte **[!UICONTROL Konten]** erfahren Sie mehr über die Verbindungen, die Sie zu verschiedenen Zielen hergestellt haben. Die nachstehende Tabelle enthält alle Informationen zu den einzelnen Zielen:

![Registerkarte „Konten“](/help/rtcdp/destinations/assets/accounts-tab.png)

| Element | Beschreibung |
---------|----------
| [!UICONTROL Plattform] | Das Ziel, für das Sie die Verbindung eingerichtet haben. |
| [!UICONTROL Verbindungstyp] | Stellt den Verbindungstyp zu Ihrem Speicher-Bucket oder Ziel dar. <ul><li>Bei E-Mail-Marketing-Zielen: Kann S3 oder FTP sein.</li><li>Bei Echtzeit-Werbezielen: Server-zu-Server.</li><li>Bei Amazon S3-Cloud-Speicherzielen: Zugriffsschlüssel. </li><li>Bei SFTP-Cloud-Speicherzielen: Grundlegende Authentifizierung für SFTP.</li></ul> |
| [!UICONTROL Benutzername] | Der Benutzername, den Sie im [Zielverbindungsassistenten](/help/rtcdp/destinations/email-marketing-destinations.md#connect-destination) ausgewählt haben. |
| [!UICONTROL Datenflüsse] | Gibt die Zahl der eindeutigen erfolgreich verbundenen Zielflüsse mit grundlegenden Informationen an, die für ein Ziel erstellt wurden. |
| [!UICONTROL Autorisiert] | Das Datum, an dem die Verbindung zu diesem Ziel genehmigt wurde. |
| [!UICONTROL Status] | `Active` oder `Inactive`. Gibt an, ob für dieses Ziel derzeit Daten aktiviert sind. Informationen zum Bearbeiten des Status finden Sie unter [Aktivierung deaktivieren](/help/rtcdp/destinations/activate-destinations.md#disable-activation). |

## [!UICONTROL Systemansicht] {#system-view}

Auf der Registerkarte **[!UICONTROL Systemansicht]** wird eine grafische Darstellung der Aktivierungsflüsse angezeigt, die Sie in der Echtzeit-Kundendatenplattform eingerichtet haben.

![Datenflüsse1](/help/rtcdp/destinations/assets/data-flows1.png)

Wählen Sie eines der Ziele aus, die auf der Seite angezeigt werden, und klicken Sie auf **[!UICONTROL Datenflüsse anzeigen]**, um Informationen über alle Verbindungen anzuzeigen, die Sie für die einzelnen Ziele eingerichtet haben.

![Datenflüsse2](/help/rtcdp/destinations/assets/data-flows2.png)