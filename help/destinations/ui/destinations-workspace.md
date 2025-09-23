---
keywords: Plattform;Ziele;Arbeitsbereich Ziele;Arbeitsbereich;Benutzeroberfläche;Ziele in der Benutzeroberfläche;Katalog;Zielkatalog;
title: Arbeitsbereich „Ziele“
description: 'Der Arbeitsbereich „Ziele“ besteht aus fünf Bereichen: Übersicht, Katalog, Durchsuchen, Konten und Systemansicht. Sie werden in den folgenden Abschnitten beschrieben.'
exl-id: 0f46f08d-0fe3-441d-933a-86bc146c0f19
source-git-commit: ff566e6ec409d237d3831d787d7428859dd4b566
workflow-type: tm+mt
source-wordcount: '2369'
ht-degree: 33%

---

# Arbeitsbereich „Ziele“ {#destinations-workspace}

Wählen Sie in der linken Navigationsleiste von Adobe Experience Platform die Option **[!UICONTROL Ziele]** aus, um auf den Arbeitsbereich [!UICONTROL Ziele] zuzugreifen.

Der Arbeitsbereich [!UICONTROL Ziele] besteht aus fünf Abschnitten: [!UICONTROL Übersicht], [!UICONTROL Katalog], [!UICONTROL Durchsuchen], [!UICONTROL Konten] und [!UICONTROL Systemansicht]. Diese werden in den folgenden Abschnitten beschrieben.

![Dashboard der Zielübersicht mit drei Widgets.](../assets/ui/workspace/destinations-overview.png)

## [!UICONTROL Übersicht] {#overview}

Die Registerkarte **[!UICONTROL Übersicht]** zeigt das Dashboard [!UICONTROL Ziele] an, das Schlüsselmetriken zu den Zieldaten Ihrer Organisation bereitstellt. Weitere Informationen finden Sie im Handbuch für das Dashboard [[!UICONTROL Ziele]](../../dashboards/guides/destinations.md).

>[!NOTE]
>
>Wenn Ihre Organisation erst seit kurzem Experience Platform nutzt und noch keine aktiven Ziele hat, sind die Dashboards [!UICONTROL Ziele] und [!UICONTROL Übersicht] nicht sichtbar. Wenn Sie [!UICONTROL Ziele] in der linken Navigationsleiste auswählen, wird stattdessen die Registerkarte [[!UICONTROL Katalog] angezeigt](#catalog).

![Die Registerkarte „Übersicht“ des Ziele-Dashboards.](../../dashboards/images/destinations/dashboard-overview.png)

## [!UICONTROL Katalog] {#catalog}

Auf der Registerkarte **[!UICONTROL Katalog]** wird eine Liste aller in [!DNL Experience Platform] verfügbaren Ziele angezeigt, an die Sie Daten senden können.

![Zielkatalog mit mehreren Zielen.](../assets/ui/workspace/catalog.png)

Die [!DNL Experience Platform]-Benutzeroberfläche bietet mehrere Such- und Filteroptionen auf der Zielkatalogseite:

* Verwenden Sie die Suchfunktion auf der Seite, um ein bestimmtes Ziel zu finden.
* Filtern Sie Ziele mithilfe der Steuerung **[!UICONTROL Kategorien]**.
* Schalten Sie zwischen **[!UICONTROL Alle Ziele]** und **[!UICONTROL Meine Ziele]** um. Wenn Sie **[!UICONTROL Alle Ziele]** auswählen, werden alle verfügbar [!DNL Experience Platform]-Ziele angezeigt. Wenn Sie **[!UICONTROL Meine Ziele]** auswählen, können Sie nur die Ziele sehen, zu denen Sie eine Verbindung hergestellt haben.
* Wählen Sie aus, die Typen von **[!UICONTROL Verbindungen]** und/oder **[!UICONTROL Erweiterungen]** anzuzeigen. Um den Unterschied zwischen den beiden Kategorien zu verstehen, lesen Sie [Zieltypen und -kategorien](../destination-types.md).
* Filtern Sie die verfügbaren Ziele auf Grundlage ihres unterstützten [Datentyps](/help/destinations/destination-sdk/functionality/destination-configuration/audience-data-type.md). Wählen Sie zwischen Personen, Audiences, Konto-Audiences, Interessenten-Audiences oder Datensatz-Exporten.

Die Zielkarten enthalten primäre und sekundäre Steuerungsoptionen. Zu den primären Steuerelementen gehören [!UICONTROL Einrichten], [!UICONTROL Aktivieren], [!UICONTROL Zielgruppen aktivieren] oder [!UICONTROL Datensätze exportieren]. Die sekundären Steuerelemente ermöglichen die Anzeige von Optionen. Diese Einstellungen werden nachfolgend beschrieben:

| Kontrollvariante | Beschreibung |
|---------|----------|
| [!UICONTROL Einrichten] | Ermöglicht die Erstellung einer Verbindung zum Ziel. |
| [!UICONTROL Aktivieren] | Nachdem Sie eine Verbindung zum Ziel hergestellt haben, können Sie Zielgruppen aktivieren oder Datensätze zu diesem Ziel exportieren. |
| [!UICONTROL Zielgruppen aktivieren] | Nachdem Sie eine Verbindung zum Ziel hergestellt haben, können Sie Zielgruppen für dieses Ziel aktivieren. |
| [!UICONTROL Datensätze exportieren] | Nachdem Sie eine Verbindung zum Ziel hergestellt haben, können Sie Datensätze zu diesem Ziel exportieren. |
| [!UICONTROL Konto anzeigen] | Zeigt die Konten an, mit denen Sie eine Verbindung zu einem Ziel hergestellt haben. |
| [!UICONTROL Datenflüsse anzeigen] | Zeigt die Datenaktivierungsflüsse an, die für ein Ziel vorhanden sind. |
| [!UICONTROL Dokumentation anzeigen] | Öffnet einen Link zur Dokumentationsseite für dieses spezifische Ziel, um weitere Informationen zu anzuzeigen und Sie bei der Einrichtung zu unterstützen. |

{style="table-layout:auto"}

![Steuerelemente auf der Zielkarte](../assets/ui/workspace/destination-card-options.png)

Wählen Sie ein Ziel im Katalog aus, um die rechte Leiste zu öffnen. Hier können Sie eine Beschreibung des Ziels sehen. Die rechte Leiste bietet dieselben in der obigen Tabelle beschriebenen Steuerelemente, einschließlich einer Beschreibung des Zielorts und einer Angabe der Zielkategorie und des Zieltyps.

![Optionen im Zielkatalog](../assets/ui/workspace/destination-right-rail.png)

Weitere Informationen zu Zielkategorien und Informationen zu den einzelnen Zielen finden Sie im [Zielkatalog](../catalog/overview.md) und unter [Zieltypen und -kategorien](../destination-types.md).

## [!UICONTROL Durchsuchen] {#browse}

Auf **[!UICONTROL Registerkarte]** Durchsuchen“ werden die Ziele angezeigt, mit denen Sie eine Verbindung hergestellt haben.

>[!TIP]
>
> Beginnen Sie mit der [Suchleiste](#search-browse), um bestimmte Datenflüsse zu finden, und verwenden Sie dann die [Seitenleistenfilter](#filter-options-browse), um Ihre Ergebnisse weiter einzugrenzen.

Bei Zielen, für die der Umschalter **[!UICONTROL Aktiviert/Deaktiviert]** aktiviert ist, wird das Ziel **[!UICONTROL Aktiviert]** bzw **[!UICONTROL Deaktiviert]** festgelegt. Sie können auch die Ziele anzeigen, bei denen Daten fließen, indem Sie **[!UICONTROL Zielgruppen]** > **[!UICONTROL Durchsuchen]** und eine zu überprüfende Zielgruppe auswählen.

>[!TIP]
>
> ![Registerkarte „Durchsuchen“](../assets/ui/workspace/browse-tab.png)
> 
> * Klicken Sie auf die Auslassungszeichen (`...`) in der Spalte [!UICONTROL Name] und verwenden Sie das Steuerelement ![Steuerung „Zielgruppen aktivieren](/help/images/icons/data-add.png) **[!UICONTROL Zielgruppen aktivieren]** zum Exportieren von Zielgruppen oder Datensätzen an dieses Ziel.
> * Klicken Sie auf die Auslassungszeichen (`...`) in der Spalte [!UICONTROL Name] und verwenden Sie das Steuerelement ![Zielsteuerung bearbeiten](/help/images/icons/edit.png)**[!UICONTROL Ziel bearbeiten ]**, um vorhandene Zielverbindungen zu bearbeiten. Lesen Sie das Tutorial [Bearbeiten von Zielen](/help/destinations/ui/edit-destination.md) für weitere Informationen.
> * Klicken Sie auf die Auslassungszeichen (`...`) in der Spalte [!UICONTROL Name] und verwenden Sie das Steuerelement ![Steuerung „Marketing-Aktionen bearbeiten](/help/images/icons/edit-marketing-actions.svg) **[!UICONTROL Marketing-Aktionen bearbeiten]**, um die Marketing-Aktionen für [ ausgewählte Ziel ](/help/destinations/ui/edit-activation.md#edit-marketing-actions) ändern.
> * Klicken Sie auf die Auslassungszeichen (`...`) in der Spalte [!UICONTROL Name] und verwenden Sie das Steuerelement ![Steuerung löschen](/help/images/icons/delete.png) **[!UICONTROL Löschen]**, um eine vorhandene Verbindung zu einem Ziel [](delete-destinations.md) entfernen.
> * Klicken Sie auf die Auslassungszeichen (`...`) in der Spalte [!UICONTROL Name] und verwenden Sie das Steuerelement ![Steuerung „Im Monitoring anzeigen](/help/images/icons/monitoring.png) **[!UICONTROL Im Monitoring anzeigen]** zum Anzeigen von Aktivierungsinformationen für dieses Ziel im [Monitoring-Dashboard](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard).
> * Klicken Sie auf die Auslassungszeichen (`...`) in der Spalte [!UICONTROL Name] und verwenden Sie das Steuerelement ![Warnhinweise abonnieren ](/help/images/icons/alert-add.png) **[!UICONTROL Warnhinweise abonnieren]**, um Ziel-Datenfluss-Warnhinweise zu abonnieren. Sie können Warnhinweise abonnieren, um Nachrichten zum Status, Erfolg oder Misserfolg Ihres Datenflusses zu erhalten. Detaillierte [ zu Ziel-Datenfluss-Warnhinweisen finden ](alerts.md) unter Abonnieren von kontextabhängigen Ziel-Warnhinweisen .
> * Klicken Sie auf die Auslassungszeichen (`...`) in der Spalte [!UICONTROL Name] und verwenden Sie das Steuerelement ![Tags verwalten](/help/images/icons/manage-tags.png) **[!UICONTROL Tags verwalten]**, um Tags einem Ziel hinzuzufügen oder daraus zu entfernen. Ausführliche Informationen zur Verwendung von Tags finden [ im Abschnitt ](#manage-tags)Verwalten von Ziel-Tags“.

In der folgenden Tabelle finden Sie alle Informationen, die für die einzelnen Ziele auf der Registerkarte [!UICONTROL Durchsuchen] bereitgestellt werden.

| Element | Beschreibung |
|---------|----------|
| Name | Der Name, den Sie für den Aktivierungsfluss zu diesem Ziel angegeben haben. |
| Datentyp | Der von der Zielverbindung unterstützte Datentyp. Unterstützte Datentypen: <ul><li>**[!UICONTROL Kunden]**</li><li>**[!UICONTROL Interessenten]**</li><li>**[!UICONTROL Konten]**</li><li>**[!UICONTROL Datensätze]**</li></ul> |
| [!UICONTROL Letzter Ausführungsstatus für Datenfluss] | Der Status der letzten Datenflussausführung. Weitere Informationen zur Ausführung von Datenflüssen finden Sie unter [Anzeigen von Zieldetails](destination-details-page.md). |
| [!UICONTROL Letztes Ausführungsdatum für Datenfluss] | Zeit und Datum, an dem der letzte Datenfluss ausgeführt wurde. Wählen Sie die Spaltenüberschrift aus, um auf die Sortieroptionen zuzugreifen (**[!UICONTROL Aufsteigend sortieren]**, **[!UICONTROL Absteigend sortieren]**). Weitere Informationen zur Ausführung von Datenflüssen finden Sie unter [Anzeigen von Zieldetails](destination-details-page.md). |
| [!UICONTROL Ziel] | Die Zielplattform, die Sie für Ihren Aktivierungsfluss ausgewählt haben. |
| [!UICONTROL Ablaufdatum des Kontos] | Das Datum, an dem die Verbindungsautorisierung zu diesem Ziel abläuft. <br> Ein Warnsymbol ![Warnung: Konto-Ablaufsymbol](/help/images/icons/alert-expiration.png) wird vor dem Ablaufdatum angezeigt, um Sie darauf hinzuweisen, dass die Verbindung abläuft und möglicherweise erneuert werden muss. Datenflüsse zu abgelaufenen Verbindungen werden angehalten und Sie müssen sich erneut authentifizieren, um Ihre Aktivierungs-Workflows fortzusetzen. <br>**Wichtig**: Diese Spalte ist derzeit nur für die Verbindungen [Pinterest](../catalog/advertising/pinterest.md), [LinkedIn](../catalog/social/linkedin.md) und [LinkedIn Matched Audiences](../catalog/social/linkedin-b2b.md) verfügbar. <br> ![Beispiel einer Warnung zur Kontogültigkeit auf der Registerkarte „Durchsuchen“](../assets/ui/workspace/account-expiration-browse.png){width="100" zoomable="yes" alt="Screenshot showing the account expiration warning icon and expiration date in the Browse tab."} |
| [!UICONTROL Benutzername] | Die Kontoanmeldedaten, die Sie für den Zielfluss ausgewählt haben. |
| [!UICONTROL Aktivierungsdaten] | Gibt die Anzahl der Zielgruppen an, die für dieses Ziel aktiviert werden. Wählen Sie dieses Steuerelement aus, um mehr über die aktivierten Zielgruppen zu erfahren. Weitere Informationen zu [ aktivierten Zielgruppen finden ](/help/destinations/ui/destination-details-page.md#activation-data) auf der Zieldetailseite unter „Aktivierungsdaten“. |
| [!UICONTROL Erstellt] | Datum und Uhrzeit der Erstellung des Aktivierungsflusses zum Ziel. Klicken Sie auf das Symbol mit dem Pfeil nach oben/unten, um nach den neuesten oder ältesten Aktivierungsflüssen zu sortieren. |
| [!UICONTROL Geändert] | Datum und Uhrzeit der letzten Änderung des Aktivierungsflusses zum Ziel. |
| [!UICONTROL Status] | `Enabled` oder `Disabled`. Gibt an, ob für dieses Ziel Daten aktiviert sind. |
| [!UICONTROL Zugriffs-Labels] | Zeigt alle Zugriffsbeschriftungen an, die diesem Ziel-Datenfluss hinzugefügt wurden. Weitere Informationen [Anwenden von Zugriffskennzeichnungen auf Ziel-Datenflüsse](/help/access-control/abac/apply-access-labels-destinations.md). |
| [!UICONTROL Tags] | Zeigt alle Tags an, die diesem Ziel-Datenfluss hinzugefügt wurden. Verwenden Sie Tags, um Ihre Datenflüsse zu organisieren und zu kategorisieren, um die Verwaltung zu erleichtern. |

Klicken Sie auf eine Zielzeile, um weitere Informationen zum Ziel in der rechten Leiste aufzurufen, z. B. Ziel-ID, Beschreibung, Anzahl der aktivierten Zielgruppen und mehr.

![Auf Zielzeile klicken](../assets/ui/workspace/click-destination-row.png)

Wählen Sie den Zielnamen aus, um Informationen über die für dieses Ziel aktivierten Zielgruppen anzuzeigen. Klicken Sie **[!UICONTROL Ziel bearbeiten]**, um [Zieleinstellungen zu ändern](/help/destinations/ui/edit-destination.md) oder **[!UICONTROL Zielgruppen aktivieren]**, um dem Datenfluss neue Zielgruppen hinzuzufügen.

### Filtern von Datenflüssen in der Registerkarte Durchsuchen {#filter-browse}

Die Registerkarte **[!UICONTROL Durchsuchen]** enthält erweiterte Filter- und Suchfunktionen, mit denen Sie Ihre Zieldatenflüsse schnell finden und verwalten können. Verwenden Sie die linke Seitenleiste, um Filter anzuwenden, und die Suchleiste, um bestimmte Datenflüsse anhand des Namens zu finden.

### Suchfunktion {#search-browse}

Verwenden Sie die Suchleiste oben in der Tabelle, um Datenflüsse schnell nach Namen zu finden. Während der Eingabe werden die Ergebnisse automatisch so gefiltert, dass nur übereinstimmende Datenflüsse angezeigt werden.

>[!NOTE]
>
> Bei der Suche nach Datenflüssen mithilfe des Suchfelds können die Ergebnisse Datenflüsse enthalten, die aufgrund Ihrer [Benutzerzugriffskennzeichnungen](/help/access-control/abac/apply-access-labels-destinations.md) nicht angezeigt werden können. Dieses Verhalten wird in einer zukünftigen Aktualisierung korrigiert. Bei Auswahl dieser Datenflüsse werden die Informationen nicht in der rechten Leiste angezeigt und Benutzende ohne Zugriff auf die erforderlichen Beschriftungen können keine Änderungen vornehmen, z. B. Zielgruppen dem Datenfluss zuordnen oder seinen Zeitplan bearbeiten.

![Animierte Demonstration der Suche nach einem Ziel-Datenfluss auf der Registerkarte Durchsuchen](../assets/ui/workspace/search.gif)

### Filteroptionen {#filter-options-browse}

Verwenden Sie die Filter in der linken Seitenleiste, um die Suche einzugrenzen.

![Zielfilter auf der Registerkarte Durchsuchen](../assets/ui/workspace/destination-filters.png)

* **[!UICONTROL Zielplattform]**: Filtern von Datenflüssen nach bestimmten Zielplattformen (z. B. [!DNL Amazon S3], [!DNL Facebook Custom Audience], [!DNL LinkedIn Matched Audience] usw.). Sie können mehrere Plattformen gleichzeitig auswählen.
* **[!UICONTROL Hat beliebige Tags]**: Filtern Sie Datenflüsse, denen bestimmte Tags zugewiesen sind. Auf diese Weise können Sie Datenflüsse basierend auf Ihren benutzerdefinierten Tags organisieren und finden.
* **[!UICONTROL Status]**: Filtern von Datenflüssen nach ihrem Betriebsstatus:
   * **[!UICONTROL Aktiviert]**: Zeigt nur aktive Datenflüsse an
   * **[!UICONTROL Deaktiviert]**: Zeigt nur inaktive Datenflüsse an
* **[!UICONTROL Kontoname]**: Filtern von Datenflüssen nach dem zugehörigen Kontonamen. Auf diese Weise können Sie alle Datenflüsse finden, die mit einem bestimmten Zielkonto verbunden sind.
* **[!UICONTROL Erstellt]**: Filtern Sie Datenflüsse nach dem Benutzer, der sie erstellt hat. Verwenden Sie diesen Filter, um Datenflüsse zu finden, die von bestimmten Team-Mitgliedern erstellt wurden.
* **[!UICONTROL Geändert von]**: Filtern von Datenflüssen nach dem Benutzer, der sie zuletzt geändert hat. Verwenden Sie diesen Filter, um die letzten Änderungen zu identifizieren, die von bestimmten Benutzern vorgenommen wurden.
* **[!UICONTROL Erstellungsdatum]**: Filtern Sie Datenflüsse anhand ihres Erstellungsdatums unter Verwendung eines Datumsbereichs:
   * **[!UICONTROL Startdatum]**: Den Anfang des Datumsbereichs festlegen
   * **[!UICONTROL Enddatum]**: Das Ende des Datumsbereichs festlegen
* **[!UICONTROL Änderungsdatum]**: Filtern Sie Datenflüsse anhand ihres Änderungsdatums unter Verwendung eines Datumsbereichs:
   * **[!UICONTROL Startdatum]**: Den Anfang des Datumsbereichs festlegen
   * **[!UICONTROL Enddatum]**: Das Ende des Datumsbereichs festlegen

### Aktive Filter {#active-filters-browse}

Wenn Sie Filter anwenden, werden sie als Tags unter der Suchleiste angezeigt.

![Aktive Filter werden als Tags unter der Suchleiste angezeigt](../assets/ui/workspace/active-filters.png)

Dort haben Sie folgende Möglichkeiten:

* Alle derzeit aktiven Filter anzeigen
* Entfernen Sie einzelne Filter, indem Sie auf das Symbol `X` jedes Filter-Tags klicken
* Alle Filter gleichzeitig mit der Option **[!UICONTROL Alle löschen]** löschen

### Verwalten von Ziel-Tags {#manage-tags}

Mit Tags können Sie Ihre Ziel-Datenflüsse organisieren und kategorisieren, um die Verwaltung zu erleichtern. Sie können Tags zu einzelnen Datenflüssen hinzufügen und daraus entfernen, um sie entsprechend Ihren Geschäftsanforderungen zu gruppieren.

Um ein Tag zu einem Datenfluss hinzuzufügen, wählen Sie die Auslassungszeichen (`...`) in der Spalte **[!UICONTROL Name]** und **[!UICONTROL Tags verwalten]** aus dem Kontextmenü aus.
Geben Sie den Namen eines neuen Tags in das Feld **[!UICONTROL Tags]** ein und wählen Sie **[!UICONTROL Speichern]**, um Ihre Änderungen anzuwenden.

![Dialogfeld „Tags verwalten“ mit Optionen zur Tag-Auswahl und -Erstellung](../assets/ui/workspace/tags.gif)

Um ein Tag aus einem Datenfluss zu entfernen, klicken Sie auf die Auslassungszeichen (`...`) in der Spalte **[!UICONTROL Name]** und wählen Sie **[!UICONTROL Tags verwalten]** aus dem Kontextmenü aus. Klicken Sie dann auf das `X` des Tags, das Sie entfernen möchten.

### Best Practices für das Tagging {#tag-best-practices}

Stellen Sie sicher, dass Ihre Ziel-Datenflüsse organisiert, leicht zu finden und verwaltbar bleiben, indem Sie die folgenden Tagging-Richtlinien befolgen.

* **Beschreibende Namen verwenden**: Erstellen Sie Tags, die den Zweck oder die Kategorie des Datenflusses klar angeben (z. B. „Marketing-Kampagnen“, „Kundenbindung“, „Saisonale Werbeaktionen„).
* **Konsistent sein**: Verwenden Sie eine konsistente Namenskonvention in Ihrer gesamten Organisation
* **Einfach halten**: Vermeiden Sie es, zu viele Tags zu erstellen, da dies die Filterung weniger effektiv machen kann
* **Verwenden hierarchischer Tags**: Erwägen Sie die Verwendung von Präfixen zum Gruppieren verwandter Tags (z. B. „Campaign-Q4“, „Campaign-Q1„)

## [!UICONTROL Konten] {#accounts}

Die Registerkarte **[!UICONTROL Konten]** zeigt Details zu den Verbindungen an, die Sie mit verschiedenen Zielen hergestellt haben, und ermöglicht es Ihnen, vorhandene Kontodetails zu aktualisieren oder zu löschen. In der nachstehenden Tabelle sehen Sie alle Informationen, die Sie über jedes Zielkonto erhalten können.

>[!TIP]
>
> * Klicken Sie auf die Auslassungszeichen (`...`) in der Spalte [!UICONTROL Platform] und verwenden Sie das Steuerelement ![Kontrolle aktivieren](/help/images/icons/data-add.png)**[!UICONTROL Aktivieren ]**/**[!UICONTROL  Zielgruppen aktivieren ]**/**[!UICONTROL  Datensätze exportieren ]**, um Zielgruppen oder Datensätze in dieses Ziel zu exportieren.
> * Klicken Sie auf die Auslassungszeichen (`...`) in der Spalte [!UICONTROL Platform] und verwenden Sie das Steuerelement ![Steuerung „Details bearbeiten“](/help/images/icons/edit.png)**[!UICONTROL Details bearbeiten ]**, um die Details eines vorhandenen Zielkontos zu [aktualisieren](update-accounts.md).
> * Klicken Sie auf die Auslassungszeichen (`...`) in der Spalte [!UICONTROL Platform] und verwenden Sie das Steuerelement ![Steuerung „Löschen“](/help/images/icons/delete.png)**[!UICONTROL Löschen ]**, um ein vorhandenes Zielkonto zu [löschen](delete-destination-account.md).

![Registerkarte „Konten“](../assets/ui/workspace/accounts-tab.png)

| Element | Beschreibung |
|---|---|
| [!UICONTROL Name] | Der Name, den Sie dem Zielkonto beim [ des Ziels ](connect-destination.md#authenticate) haben. Wählen Sie die Spaltenüberschrift aus, um auf die Sortieroptionen zuzugreifen (**[!UICONTROL Aufsteigend sortieren]**, **[!UICONTROL Absteigend sortieren]**). |
| [!UICONTROL Ziel] | Der Ziel-Connector, für den Sie die Verbindung eingerichtet haben. |
| [!UICONTROL Verbindungstyp] | Gibt den Kontoverbindungstyp zu Ihrem Speicher-Behälter oder Ziel an. Je nach Ziel stehen folgende Authentifizierungsoptionen zur Verfügung: <ul><li>Bei E-Mail-Marketing-Zielen: S3, FTP oder Azure Blob.</li><li>Bei Echtzeit-Werbezielen: Server-zu-Server.</li><li>Bei Amazon S3-Cloud-Speicherzielen: Zugriffsschlüssel. </li><li>Bei SFTP-Cloud-Speicherzielen: Grundlegende Authentifizierung für SFTP.</li><li>OAuth 1- oder OAuth 2-Authentifizierung</li><li>Authentifizierung über Bearer-Token</li></ul> |
| [!UICONTROL Benutzername] | Der Benutzername, den Sie im Workflow [Ziel verbinden“ ausgewählt ](../catalog/email-marketing/overview.md#connect-destination). |
| [!UICONTROL Verbindungen] | Gibt die Zahl der eindeutigen erfolgreich verbundenen Ziel-Datenflüsse an, die für ein Ziel erstellt wurden, zusammen mit grundlegenden Informationen. |
| [!UICONTROL Autorisierungsdatum] | Das Datum, an dem die Verbindung zu diesem Ziel genehmigt wurde. |
| [!UICONTROL Ablaufdatum] | Das Datum, an dem die Verbindungsautorisierung zu diesem Ziel abläuft. <br> Ein Warnsymbol ![Warnsymbol „Konto abgelaufen“.](/help/images/icons/alert-expiration.png) wird vor dem Ablaufdatum angezeigt, um Sie darauf hinzuweisen, dass die Verbindung abläuft und möglicherweise erneuert werden muss. Datenflüsse zu abgelaufenen Verbindungen werden angehalten und Sie müssen sich erneut authentifizieren, um Ihre Aktivierungs-Workflows fortzusetzen. <br>**Wichtig**: Diese Spalte ist derzeit nur für die Verbindungen [Pinterest](../catalog/advertising/pinterest.md), [LinkedIn](../catalog/social/linkedin.md) und [LinkedIn Matched Audiences](../catalog/social/linkedin-b2b.md) verfügbar. <br> ![](../assets/ui/workspace/expired-accounts.png){width="100" zoomable="yes"} |

{style="table-layout:auto"}

### Konten filtern {#filter-accounts}

Die Registerkarte **[!UICONTROL Konten]** enthält erweiterte Filter- und Suchfunktionen, mit denen Sie Ihre Zielkonten schnell finden und verwalten können. Verwenden Sie die linke Seitenleiste, um Filter anzuwenden, und die Suchleiste, um bestimmte Konten nach Namen zu finden.

#### Nach Konten suchen {#search-accounts}

Verwenden Sie die Suchleiste oben in der Tabelle, um Konten schnell nach Namen zu finden. Während der Eingabe werden die Ergebnisse automatisch so gefiltert, dass nur übereinstimmende Konten angezeigt werden.

![Suchleiste auf der Registerkarte „Konten“](../assets/ui/workspace/accounts-search.gif)

#### Filteroptionen {#filter-options-accounts}

Verwenden Sie die Filter in der linken Seitenleiste, um die Suche einzugrenzen.

![Kontofilter auf der Registerkarte „Konten“](../assets/ui/workspace/account-filters.png)

* **[!UICONTROL Zielplattform]**: Filtern von Konten nach bestimmten Zielplattformen (z. B.: [!DNL Microsoft Bing], [!DNL Amazon S3], [!DNL Facebook Custom Audiences], [!DNL LinkedIn Matched Audiences] usw.). Sie können mehrere Plattformen gleichzeitig auswählen.
* **[!UICONTROL Erstellt von]**: Filtern Sie Konten nach dem Benutzer, der sie erstellt hat. Verwenden Sie diesen Filter, um Konten zu finden, die von bestimmten Team-Mitgliedern erstellt wurden.

#### Aktive Filter {#active-filters-accounts}

Wenn Sie Filter anwenden, werden sie als Tags unter der Suchleiste angezeigt.

![Aktive Filter werden als Tags auf der Registerkarte „Konten“ angezeigt](../assets/ui/workspace/accounts-active-filters.png)

Dort haben Sie folgende Möglichkeiten:

* Alle derzeit aktiven Filter anzeigen
* Entfernen Sie einzelne Filter, indem Sie auf das Symbol `X` jedes Filter-Tags klicken
* Alle Filter gleichzeitig mit der Option **[!UICONTROL Alle löschen]** löschen

## [!UICONTROL Systemansicht] {#system-view}

Auf der Registerkarte **[!UICONTROL Systemansicht]** wird eine grafische Darstellung der Aktivierungsflüsse angezeigt, die Sie in Adobe Experience Platform eingerichtet haben.

![Data-flows1](../assets/ui/workspace/system-view-dataflows.png)

Wählen Sie eines der Ziele aus, die auf der Seite angezeigt werden, und klicken Sie auf **[!UICONTROL Datenflüsse anzeigen]**, um Informationen über alle Verbindungen anzuzeigen, die Sie für die einzelnen Ziele eingerichtet haben.

![Data-flows2](../assets/ui/workspace/system-view-dataflows-2.png)
