---
keywords: Plattform;Ziele;Ziel-Arbeitsbereich;Arbeitsbereich;Benutzeroberfläche;Ziele ui;Katalog;Zielkatalog; Zielkatalog;
title: Arbeitsbereich „Ziele“
description: 'Der Arbeitsbereich Ziele besteht aus vier Bereichen: Katalog, Durchsuchen, Konten und Systemansicht. Diese werden in den folgenden Abschnitten beschrieben.'
seo-description: Wählen Sie in Adobe Experience Platform in der linken Navigationsleiste "Ziele"aus, um auf den Zielarbeitsbereich zuzugreifen.
translation-type: tm+mt
source-git-commit: 4f5e7dfee17b2dde371efb82cf52d91c08696f39
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 31%

---


# Arbeitsbereich „Ziele“ {#destinations-workspace}

## Übersicht {#overview}

Wählen Sie in Adobe Experience Platform **[!UICONTROL Ziele]** aus der linken Navigationsleiste, um auf den Arbeitsbereich [!UICONTROL Ziele] zuzugreifen.

Der Arbeitsbereich [!UICONTROL Ziele] besteht aus vier Abschnitten: [!UICONTROL Katalog], [!UICONTROL Durchsuchen], [!UICONTROL Konten] und [!UICONTROL Ansicht des Systems], wie in den folgenden Abschnitten beschrieben.

![Zielüberblick](../assets/ui/workspace/destinations-overview.png)

## [!UICONTROL Katalog] {#catalog}

Auf der Registerkarte **[!UICONTROL Katalog]** wird eine Liste aller in der Plattform verfügbaren Ziele angezeigt, an die Sie Daten senden können.

Die Benutzeroberfläche &quot;Plattform&quot;bietet verschiedene Such- und Filteroptionen auf der Katalogseite &quot;Ziele&quot;:

* Verwenden Sie die Suchfunktion auf der Seite, um ein bestimmtes Ziel zu finden.
* Filtern Sie Ziele mithilfe des Steuerelements [!UICONTROL Kategorien].
* Wechsel zwischen [!UICONTROL Alle Ziele] und [!UICONTROL Meine Ziele]. Wenn **[!UICONTROL Alle Ziele]** ausgewählt ist, werden alle verfügbaren Plattformziele angezeigt. Wenn **[!UICONTROL Meine Ziele]** ausgewählt ist, können Sie nur die Ziele sehen, zu denen Sie eine Verbindung hergestellt haben.
* Wählen Sie zur Ansicht **[!UICONTROL Verbindungen]** und/oder **[!UICONTROL Erweiterungen]**. Informationen zum Unterschied zwischen den beiden Kategorien finden Sie unter [Zieltypen und Kategorien](../destination-types.md).

![Filtern und Suchdemo von Zielen](../assets/ui/workspace/destinations-search-and-filter.gif)

Die Zielkarten enthalten entweder ein **[!UICONTROL Configure]**- oder ein **[!UICONTROL Activate]**-Steuerelement und ein sekundäres Steuerelement, das weitere Optionen aufruft. Diese Kontrollen werden nachfolgend beschrieben:

| Kontrolle | Beschreibung |
---------|----------
| [!UICONTROL Konfigurieren von] | Ermöglicht Ihnen das Erstellen einer Verbindung mit dem Ziel. |
| [!UICONTROL Aktivieren] | Nachdem Sie eine Verbindung zum Ziel hergestellt haben, können Sie Segmente aktivieren. |
| [!UICONTROL Ansichten-Konto] | Ansicht der Konten, die Sie für ein Ziel verbunden haben. |
| [!UICONTROL Ansicht DataFlows] | Ansicht der Datenflüsse, die für ein Ziel vorhanden sind. |
| [!UICONTROL Dokumentation zur Ansicht] | Öffnet einen Link zur Dokumentationsseite für dieses spezifische Ziel, um weitere Informationen zu erhalten und die Einrichtung zu erleichtern. |

{style=&quot;table-layout:auto&quot;}

![Steuerelemente auf der Zielkarte](../assets/ui/workspace/destination-card-options.png)

Wählen Sie eine Zielkarte im Katalog aus, um die rechte Leiste zu öffnen. Hier sehen Sie eine Beschreibung des Ziels. Die rechte Leiste bietet dieselben in der obigen Tabelle beschriebenen Steuerelemente sowie eine Beschreibung des Ziels und eine Angabe der Kategorie und des Typs des Ziels.

![Optionen im Zielkatalog](../assets/ui/workspace/destination-right-rail.png)

Weitere Informationen zu den Ziel-Kategorien und Informationen zu den einzelnen Zielen finden Sie im [Zielkatalog](../catalog/overview.md) und im [Zieltypen und -Kategorien](../destination-types.md).

## [!UICONTROL Konten] {#accounts}

Auf der Registerkarte **[!UICONTROL Konten]** erfahren Sie mehr über die Verbindungen, die Sie zu verschiedenen Zielen hergestellt haben. Die nachstehende Tabelle enthält alle Informationen zu den einzelnen Zielen:

>[!TIP]
>
>Verwenden Sie die Schaltfläche ![Hinzufügen in der Spalte **[!UICONTROL Plattform]**, um eine neue Zielverbindung für dieses Konto zu erstellen.](../assets/ui/workspace/add-data-symbol.png)

![Registerkarte „Konten“](../assets/ui/workspace/edit-account-destinations.png)

| Element | Beschreibung |
---------|----------
| [!UICONTROL Plattform] | Das Ziel, für das Sie die Verbindung eingerichtet haben. |
| [!UICONTROL Verbindungstyp] | Stellt den Verbindungstyp zu Ihrem Speicher-Bucket oder Ziel dar. <ul><li>Bei E-Mail-Marketing-Zielen: Kann S3 oder FTP sein.</li><li>Bei Echtzeit-Werbezielen: Server-zu-Server.</li><li>Bei Amazon S3-Cloud-Speicherzielen: Zugriffsschlüssel. </li><li>Bei SFTP-Cloud-Speicherzielen: Grundlegende Authentifizierung für SFTP.</li></ul> |
| [!UICONTROL Benutzername] | Der Benutzername, den Sie im [Zielverbindungsassistenten](../catalog/email-marketing/overview.md#connect-destination) ausgewählt haben. |
| [!UICONTROL Ziele] | Gibt die Zahl der eindeutigen erfolgreich verbundenen Zielflüsse mit grundlegenden Informationen an, die für ein Ziel erstellt wurden. |
| [!UICONTROL Autorisiert] | Das Datum, an dem die Verbindung zu diesem Ziel genehmigt wurde. |

{style=&quot;table-layout:auto&quot;}

Darüber hinaus können Sie Ihre Kontoinformationen bearbeiten oder aktualisieren. Klicken Sie in der Spalte **[!UICONTROL Plattform]** auf die Schaltfläche Konto bearbeiten, um die Kontoinformationen zu bearbeiten.![](../assets/ui/workspace/pencil-icon.png)

Bei Konten, die einen Verbindungstyp `OAuth2` verwenden, können Sie **[!UICONTROL OAuth]** erneut verbinden auswählen, um Ihre Kontoanmeldeinformationen zu verlängern.

![Oauth-Bild](../assets/ui/workspace/reconnect-oauth.png)

Bei Konten mit einem Verbindungstyp `Access Key` oder `ConnectionString` können Sie Ihre Kontoauthentifizierungsinformationen bearbeiten, einschließlich Informationen wie Zugriffskennung, geheime Schlüssel oder Verbindungszeichenfolgen.

![Bild zu Kontoinformationen](../assets/ui/workspace/edit-account-details.png)

Nachdem Sie die Bearbeitung Ihrer Kontodetails abgeschlossen haben, wählen Sie **[!UICONTROL Speichern]**, um die Aktualisierung abzuschließen.

## [!UICONTROL Durchsuchen] {#browse}

Auf der Registerkarte **[!UICONTROL Durchsuchen]** werden die Ziele angezeigt, mit denen Sie eine Verbindung hergestellt haben. Ziele, bei denen der Umschalter **[!UICONTROL Aktiviert]** aktiviert ist, stellen Sie das Ziel auf &quot;aktiv&quot;und umgekehrt ein. Sie können die Ziele, an denen Daten fließen, auch durch Auswahl von **[!UICONTROL Segmente]** > **[!UICONTROL Durchsuchen]** und Auswahl eines zu prüfenden Segments Ansicht haben. Die nachstehende Tabelle enthält alle Informationen, die für die einzelnen Ziele auf der Registerkarte „Durchsuchen“ verfügbar sind:

>[!TIP]
>
> * Verwenden Sie die Schaltfläche ![Hinzufügen Segmente](../assets/ui/workspace/add-data-symbol.png) in der Spalte **[!UICONTROL Name]**, um weitere Segmente zu diesem Ziel zu aktivieren.
> * Verwenden Sie die Schaltfläche ![Ziele löschen](../assets/ui/workspace/delete-destination-symbol.png) in der Spalte **[!UICONTROL Name]**, um eine bestehende Verbindung zu einem Ziel zu löschen.


![Registerkarte „Durchsuchen“](../assets/ui/workspace/browse-tab.png)

| Element | Beschreibung |
---------|----------
| Name | Der Name, den Sie für den Aktivierungsfluss zu diesem Ziel angegeben haben. Dieselbe Spalte enthält zwei Steuerelemente: [!UICONTROL Aktivieren Sie ] und [!UICONTROL Löschen Sie das Ziel]. |
| [!UICONTROL Letzter Flusslaufstatus] | Der Status des letzten Datenflusses wird ausgeführt. Weitere Informationen zu Datenflug-Ansichten finden Sie unter [Zieldetails](destination-details-page.md). |
| [!UICONTROL Letzter Flusslaufdatum] | Zeit und Datum, an dem der letzte Datenaflow ausgeführt wurde. Weitere Informationen zu Datenflug-Ansichten finden Sie unter [Zieldetails](destination-details-page.md). |
| [!UICONTROL Ziel] | Die Zielplattform, die Sie für Ihren Aktivierungsfluss ausgewählt haben. |
| [!UICONTROL Verbindungstyp] | Stellt den Verbindungstyp zu Ihrem Speicher-Bucket oder Ziel dar. <ul><li>Für E-Mail-Marketingziele: Kann S3, FTP oder [!DNL Azure Blob] sein.</li><li>Für Werbeziele in Echtzeit: Server-zu-Server.</li><li>Für Streaming-Ziele: Kann [!DNL Azure Event Hubs] oder [!DNL Amazon Kinesis] sein.</li></ul> |
| [!UICONTROL Benutzername] | Die Kontoanmeldedaten, die Sie für den Zielfluss ausgewählt haben. |
| [!UICONTROL Aktivierungen] | Gibt die Anzahl der Segmente an, die für dieses Ziel aktiviert werden. Wählen Sie dieses Steuerelement aus, um mehr über die aktivierten Segmente zu erfahren. Weitere Informationen zu den aktivierten Aktivierungen finden Sie auf der Seite mit den Zieldetails unter [Daten zur ](/help/destinations/ui/destination-details-page.md#activation-data). |
| [!UICONTROL Erstellt] | Datum und Uhrzeit (UTC) der Erstellung des Aktivierungsflusses zum Ziel. |
| [!UICONTROL Status] | `Active` oder `Inactive`. Gibt an, ob Daten für dieses Ziel aktiviert werden. Informationen zum Bearbeiten des Status finden Sie unter [Aktivierung deaktivieren](./activate-destinations.md#disable-activation). |

Klicken Sie auf eine Zielzeile, um weitere Informationen zum Ziel in der rechten Leiste anzuzeigen.

![Auf Zielzeile klicken](../assets/ui/workspace/click-destination-row.png)

Wählen Sie den Zielnamen aus, um Informationen zu den für dieses Ziel aktivierten Segmenten anzuzeigen. Klicken Sie auf **[!UICONTROL Aktivierung bearbeiten]**, um die Segmente, die an dieses Ziel gesendet werden, zu ändern oder hinzuzufügen.

## [!UICONTROL Systemansicht] {#system-view}

Auf der Registerkarte **[!UICONTROL Ansicht des Systems]** wird eine grafische Darstellung der Aktivierungen angezeigt, die Sie in Adobe Experience Platform eingerichtet haben.

![Datenflüsse1](../assets/ui/workspace/data-flows1.png)

Wählen Sie eines der auf der Seite angezeigten Ziele aus und klicken Sie auf **[!UICONTROL Ansicht-Fluss]**, um Informationen zu allen Verbindungen anzuzeigen, die Sie für jedes Ziel eingerichtet haben.

![Datenflüsse2](../assets/ui/workspace/data-flows2.png)