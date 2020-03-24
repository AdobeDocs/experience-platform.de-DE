---
title: Arbeitsbereich „Ziele“
seo-title: Arbeitsbereich „Ziele“
description: Wählen Sie in der Echtzeit-Kundendatenplattform von Adobe in der linken Navigationsleiste die Option „Ziele“, um auf den Arbeitsbereich „Ziele“ zuzugreifen.
seo-description: Wählen Sie in der Echtzeit-Kundendatenplattform von Adobe in der linken Navigationsleiste die Option „Ziele“, um auf den Arbeitsbereich „Ziele“ zuzugreifen.
translation-type: tm+mt
source-git-commit: e87ddff936da88b1b2b3cf71c2d6c24ed28b39ab

---


# Arbeitsbereich „Ziele“ {#destinations-workspace}

Wählen Sie in der Echtzeit-Kundendatenplattform von Adobe in der linken Navigationsleiste die Option **Ziele**, um auf den Arbeitsbereich „Ziele“ zuzugreifen.

The Destinations workspace consists of four sections, **Catalog**, **Browse**, **Accounts**, and **System View**, which are described in the sections below.

![Zielüberblick](/help/rtcdp/destinations/assets/destinations-overview.png)

## Katalog {#catalog}

The **[!UICONTROL Catalog]** tab displays a list of all destinations offered by Adobe, that you can send data to.

Verwenden Sie die Suchfunktion auf der Seite, um ein bestimmtes Ziel oder ein bestimmtes Filterziel mithilfe des **[!UICONTROL Categories]** Steuerelements zu suchen.

Wählen Sie ein Ziel im Katalog aus, um die rechte Leiste zu öffnen. Here, you can set up a connection to the destination (**Connect destination**), view existing destination connections (**Browse destinations**) or learn more detailed information about each destination by viewing the documentation (**View documentation**).

![Optionen im Zielkatalog](/help/rtcdp/destinations/assets/destination-ui-catalog-options.png)

Weiterführende Informationen zu Zielkategorien sowie Informationen zu einzelnen Zielen finden Sie unter [Zielkatalog](/help/rtcdp/destinations/destinations-catalog.md).

## Durchsuchen {#browse}

The **[!UICONTROL Browse]** tab displays the destinations with which you have established a connection. Destinations with the **enabled** toggle turned on set the destination to active and vice-versa. Sie können auch jene Ziele, bei denen Daten fließen, anzeigen, indem Sie **Segmente > Durchsuchen** wählen und ein zu prüfendes Segment auswählen. Die nachstehende Tabelle enthält alle Informationen, die für die einzelnen Ziele auf der Registerkarte „Durchsuchen“ verfügbar sind:

![Registerkarte „Durchsuchen“](/help/rtcdp/destinations/assets/browse-tab.png)

| Element | Beschreibung |
---------|----------
| Name | Der Name, den Sie für den Aktivierungsfluss zu diesem Ziel angegeben haben. |
| Ziel | Die Zielplattform, die Sie für Ihren Aktivierungsfluss ausgewählt haben. |
| Verbindungstyp | Stellt den Verbindungstyp zu Ihrem Datenspeicherung-Behälter oder -Ziel dar. <ul><li>Für E-Mail-Marketingziele: Kann S3 oder FTP sein.</li><li>Für Werbeziele in Echtzeit: Server-zu-Server</li></ul> |
| Benutzername | Die Kontoanmeldedaten, die Sie für den Zielfluss ausgewählt haben. |
| Segmente | Die Zahl der Segmente, die für dieses Ziel aktiviert werden. |
| Erstellt | Datum und Uhrzeit (UTC) der Erstellung des Aktivierungsflusses zum Ziel. |
| Status | `Active` oder `Inactive`. Gibt an, ob für dieses Ziel derzeit Daten aktiviert sind. Informationen zum Bearbeiten des Status finden Sie unter [Aktivierung deaktivieren](/help/rtcdp/destinations/activate-destinations.md#disable-activation). |

Klicken Sie auf eine Zielzeile, um weitere Informationen zum Ziel in der rechten Leiste anzuzeigen.

![Auf Zielzeile klicken](/help/rtcdp/destinations/assets/click-destination-row.png)

Wählen Sie den Zielnamen aus, um Informationen zu den für dieses Ziel aktivierten Segmenten anzuzeigen. Click **[!UICONTROL Edit activation]** to modify or add to the segments that are being sent to this destination.

## Konten {#accounts}

In the **[!UICONTROL Accounts]** tab, you can learn more about the connections that you have established with various destinations. Die nachstehende Tabelle enthält alle Informationen zu den einzelnen Zielen:

![Registerkarte „Konten“](/help/rtcdp/destinations/assets/accounts-tab.png)

| Element | Beschreibung |
---------|----------
| Plattform | Das Ziel, für das Sie die Verbindung eingerichtet haben. |
| Verbindungstyp | Stellt den Verbindungstyp zu Ihrem Datenspeicherung-Behälter oder -Ziel dar. <ul><li>Für E-Mail-Marketingziele: Kann S3 oder FTP sein.</li><li>Für Werbeziele in Echtzeit: Server-zu-Server</li><li>Für Amazon S3 Cloud-Datenspeicherung-Ziele: Zugriffsschlüssel </li><li>Für SFTP-Cloud-Datenspeicherung-Ziele: Grundlegende Authentifizierung für SFTP</li></ul> |
| Benutzername | Der Benutzername, den Sie im [Zielverbindungsassistenten](/help/rtcdp/destinations/email-marketing-destinations.md#connect-destination) ausgewählt haben. |
| Datenfluss | Gibt die Zahl der eindeutigen erfolgreich verbundenen Zielflüsse mit grundlegenden Informationen an, die für ein Ziel erstellt wurden. |
| Autorisiert | Das Datum, an dem die Verbindung zu diesem Ziel genehmigt wurde. |
| Status | `Active` oder `Inactive`. Gibt an, ob für dieses Ziel derzeit Daten aktiviert sind. Informationen zum Bearbeiten des Status finden Sie unter [Aktivierung deaktivieren](/help/rtcdp/destinations/activate-destinations.md#disable-activation). |

## System-Ansicht {#system-view}

The **[!UICONTROL System View]** tab displays a graphic representation of the activation flows that you have set up in the Real-time Customer Data Platform.

![Datenflüsse1](/help/rtcdp/destinations/assets/data-flows1.png)

Select any of the destinations displayed on the page and press **[!UICONTROL View flows]** to see information on all the connections you have set up for each destination.

![Datenflüsse2](/help/rtcdp/destinations/assets/data-flows2.png)