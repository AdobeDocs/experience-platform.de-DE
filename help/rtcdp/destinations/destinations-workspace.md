---
title: Arbeitsbereich „Ziele“
seo-title: Arbeitsbereich „Ziele“
description: Wählen Sie in der Echtzeit-Kundendatenplattform von Adobe in der linken Navigationsleiste die Option „Ziele“, um auf den Arbeitsbereich „Ziele“ zuzugreifen.
seo-description: Wählen Sie in der Echtzeit-Kundendatenplattform von Adobe in der linken Navigationsleiste die Option „Ziele“, um auf den Arbeitsbereich „Ziele“ zuzugreifen.
translation-type: tm+mt
source-git-commit: 336aa90cf1e059a92a36dd0ef3222ef6a6f5123b
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 100%

---


# Arbeitsbereich „Ziele“ {#destinations-workspace}

Wählen Sie in der Echtzeit-Kundendatenplattform von Adobe in der linken Navigationsleiste die Option **[!UICONTROL Ziele]**, um auf den Arbeitsbereich [!UICONTROL Ziele] zuzugreifen.

Der Arbeitsbereich [!UICONTROL Ziele] besteht aus vier Bereichen: **[!UICONTROL Katalog]**, **[!UICONTROL Durchsuchen]**, **[!UICONTROL Konten]** und **[!UICONTROL Systemansicht]**. Diese werden in den folgenden Abschnitten beschrieben.

![Zielüberblick](/help/rtcdp/destinations/assets/destinations-overview.png)

## [!UICONTROL Katalog] {#catalog}

Auf der Registerkarte **[!UICONTROL Katalog]** wird eine Liste aller von Adobe angebotenen Ziele angezeigt, an die Sie Daten senden können.

Verwenden Sie die Suchfunktion auf der Seite, um ein bestimmtes Ziel zu suchen oder Ziele mithilfe des Steuerelements **[!UICONTROL Kategorien]** zu filtern.

Wählen Sie ein Ziel im Katalog aus, um die rechte Leiste zu öffnen. Hier können Sie eine Verbindung zum Ziel herstellen (**[!UICONTROL Ziel verbinden]**), vorhandene Zielverbindungen anzeigen (**[!UICONTROL Ziele durchsuchen]**) oder genauere Informationen zu den einzelnen Zielen erhalten, indem Sie die Dokumentation anzeigen (**[!UICONTROL Dokumentation anzeigen]**).

![Optionen im Zielkatalog](/help/rtcdp/destinations/assets/destination-ui-catalog-options.png)

Weiterführende Informationen zu Zielkategorien sowie Informationen zu einzelnen Zielen finden Sie unter [Zielkatalog](/help/rtcdp/destinations/destinations-catalog.md).

## [!UICONTROL Durchsuchen] {#browse}

Auf der Registerkarte **[!UICONTROL Durchsuchen]** werden die Ziele angezeigt, mit denen Sie eine Verbindung hergestellt haben. Ziele, bei denen der Umschalter **[!UICONTROL Aktiviert]** aktiviert ist, setzen das Ziel auf „aktiv“ und umgekehrt. Sie können auch jene Ziele, bei denen Daten fließen, anzeigen, indem Sie **[!UICONTROL Segmente > Durchsuchen]** wählen und ein zu prüfendes Segment auswählen. Die nachstehende Tabelle enthält alle Informationen, die für die einzelnen Ziele auf der Registerkarte „Durchsuchen“ verfügbar sind:

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