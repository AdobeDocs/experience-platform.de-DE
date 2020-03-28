---
title: Arbeitsbereich „Ziele“
seo-title: Arbeitsbereich „Ziele“
description: Wählen Sie in der Echtzeit-Kundendatenplattform von Adobe in der linken Navigationsleiste die Option „Ziele“, um auf den Arbeitsbereich „Ziele“ zuzugreifen.
seo-description: Wählen Sie in der Echtzeit-Kundendatenplattform von Adobe in der linken Navigationsleiste die Option „Ziele“, um auf den Arbeitsbereich „Ziele“ zuzugreifen.
translation-type: tm+mt
source-git-commit: 336aa90cf1e059a92a36dd0ef3222ef6a6f5123b

---


# Arbeitsbereich „Ziele“ {#destinations-workspace}

In Adobe Real-time Customer Data Platform, select **[!UICONTROL Destinations]** from the left navigation bar to access the [!UICONTROL Destinations] workspace.

Der [!UICONTROL Destinations] Arbeitsbereich besteht aus vier Abschnitten **[!UICONTROL Catalog]**, **[!UICONTROL Browse]**, **[!UICONTROL Accounts]** und **[!UICONTROL System View]**, die in den folgenden Abschnitten beschrieben werden.

![Zielüberblick](/help/rtcdp/destinations/assets/destinations-overview.png)

## [!UICONTROL Catalog] {#catalog}

The **[!UICONTROL Catalog]** tab displays a list of all destinations offered by Adobe, that you can send data to.

Verwenden Sie die Suchfunktion auf der Seite, um ein bestimmtes Ziel oder ein bestimmtes Filterziel mithilfe des **[!UICONTROL Categories]** Steuerelements zu suchen.

Wählen Sie ein Ziel im Katalog aus, um die rechte Leiste zu öffnen. Here, you can set up a connection to the destination (**[!UICONTROL Connect destination]**), view existing destination connections (**[!UICONTROL Browse destinations]**) or learn more detailed information about each destination by viewing the documentation (**[!UICONTROL View documentation]**).

![Optionen im Zielkatalog](/help/rtcdp/destinations/assets/destination-ui-catalog-options.png)

Weiterführende Informationen zu Zielkategorien sowie Informationen zu einzelnen Zielen finden Sie unter [Zielkatalog](/help/rtcdp/destinations/destinations-catalog.md).

## [!UICONTROL Browse] {#browse}

The **[!UICONTROL Browse]** tab displays the destinations with which you have established a connection. Destinations with the **[!UICONTROL enabled]** toggle turned on set the destination to active and vice-versa. You can also view the destinations where you have data flowing by selecting **[!UICONTROL Segments > Browse]** and selecting a segment to inspect. Die nachstehende Tabelle enthält alle Informationen, die für die einzelnen Ziele auf der Registerkarte „Durchsuchen“ verfügbar sind:

![Registerkarte „Durchsuchen“](/help/rtcdp/destinations/assets/browse-tab.png)

| Element | Beschreibung |
---------|----------
| Name | Der Name, den Sie für den Aktivierungsfluss zu diesem Ziel angegeben haben. |
| [!UICONTROL Destination] | Die Zielplattform, die Sie für Ihren Aktivierungsfluss ausgewählt haben. |
| [!UICONTROL Connection Type] | Stellt den Verbindungstyp zu Ihrem Datenspeicherung-Behälter oder -Ziel dar. <ul><li>Für E-Mail-Marketingziele: Kann S3 oder FTP sein.</li><li>Für Werbeziele in Echtzeit: Server-zu-Server</li></ul> |
| [!UICONTROL Username] | Die Kontoanmeldedaten, die Sie für den Zielfluss ausgewählt haben. |
| [!UICONTROL Segments] | Die Zahl der Segmente, die für dieses Ziel aktiviert werden. |
| [!UICONTROL Created] | Datum und Uhrzeit (UTC) der Erstellung des Aktivierungsflusses zum Ziel. |
| [!UICONTROL Status] | `Active` oder `Inactive`. Gibt an, ob für dieses Ziel derzeit Daten aktiviert sind. Informationen zum Bearbeiten des Status finden Sie unter [Aktivierung deaktivieren](/help/rtcdp/destinations/activate-destinations.md#disable-activation). |

Klicken Sie auf eine Zielzeile, um weitere Informationen zum Ziel in der rechten Leiste anzuzeigen.

![Auf Zielzeile klicken](/help/rtcdp/destinations/assets/click-destination-row.png)

Wählen Sie den Zielnamen aus, um Informationen zu den für dieses Ziel aktivierten Segmenten anzuzeigen. Click **[!UICONTROL Edit activation]** to modify or add to the segments that are being sent to this destination.

## [!UICONTROL Accounts] {#accounts}

In the **[!UICONTROL Accounts]** tab, you can learn more about the connections that you have established with various destinations. Die nachstehende Tabelle enthält alle Informationen zu den einzelnen Zielen:

![Registerkarte „Konten“](/help/rtcdp/destinations/assets/accounts-tab.png)

| Element | Beschreibung |
---------|----------
| [!UICONTROL Platform] | Das Ziel, für das Sie die Verbindung eingerichtet haben. |
| [!UICONTROL Connection Type] | Stellt den Verbindungstyp zu Ihrem Datenspeicherung-Behälter oder -Ziel dar. <ul><li>Für E-Mail-Marketingziele: Kann S3 oder FTP sein.</li><li>Für Werbeziele in Echtzeit: Server-zu-Server</li><li>Für Amazon S3 Cloud-Datenspeicherung-Ziele: Zugriffsschlüssel </li><li>Für SFTP-Cloud-Datenspeicherung-Ziele: Grundlegende Authentifizierung für SFTP</li></ul> |
| [!UICONTROL Username] | Der Benutzername, den Sie im [Zielverbindungsassistenten](/help/rtcdp/destinations/email-marketing-destinations.md#connect-destination) ausgewählt haben. |
| [!UICONTROL Data Flows] | Gibt die Zahl der eindeutigen erfolgreich verbundenen Zielflüsse mit grundlegenden Informationen an, die für ein Ziel erstellt wurden. |
| [!UICONTROL Authorized] | Das Datum, an dem die Verbindung zu diesem Ziel genehmigt wurde. |
| [!UICONTROL Status] | `Active` oder `Inactive`. Gibt an, ob für dieses Ziel derzeit Daten aktiviert sind. Informationen zum Bearbeiten des Status finden Sie unter [Aktivierung deaktivieren](/help/rtcdp/destinations/activate-destinations.md#disable-activation). |

## [!UICONTROL System View] {#system-view}

The **[!UICONTROL System View]** tab displays a graphic representation of the activation flows that you have set up in the Real-time Customer Data Platform.

![Datenflüsse1](/help/rtcdp/destinations/assets/data-flows1.png)

Select any of the destinations displayed on the page and press **[!UICONTROL View flows]** to see information on all the connections you have set up for each destination.

![Datenflüsse2](/help/rtcdp/destinations/assets/data-flows2.png)