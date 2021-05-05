---
keywords: Plattform;Ziele;Ziel-Arbeitsbereich;Arbeitsbereich;Benutzeroberfläche;Ziele ui;Katalog;Zielkatalog; Zielkatalog;
title: Arbeitsbereich „Ziele“
description: 'Der Arbeitsbereich "Ziele"besteht aus vier Bereichen: "Katalog", "Durchsuchen", "Konten"und "System-Ansicht". Sie werden in den folgenden Abschnitten beschrieben.'
seo-description: Wählen Sie in Adobe Experience Platform in der linken Navigationsleiste "Ziele"aus, um auf den Zielarbeitsbereich zuzugreifen.
exl-id: 0f46f08d-0fe3-441d-933a-86bc146c0f19
translation-type: tm+mt
source-git-commit: eaa4a7efc248104d823267eca574f2eca16edc3f
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 21%

---

# Arbeitsbereich „Ziele“ {#destinations-workspace}

## Übersicht {#overview}

Wählen Sie in Adobe Experience Platform **[!UICONTROL Ziele]** aus der linken Navigationsleiste, um auf den Arbeitsbereich [!UICONTROL Ziele] zuzugreifen.

Der Arbeitsbereich [!UICONTROL Ziele] besteht aus vier Abschnitten: [!UICONTROL Katalog], [!UICONTROL Durchsuchen], [!UICONTROL Konten] und [!UICONTROL Ansicht des Systems], wie in den folgenden Abschnitten beschrieben.

![Zielüberblick](../assets/ui/workspace/destinations-workspace.png)

## [!UICONTROL Katalog] {#catalog}

Auf der Registerkarte **[!UICONTROL Katalog]** wird eine Liste aller in [!DNL Platform] verfügbaren Ziele angezeigt, an die Sie Daten senden können.

Die [!DNL Platform]-Benutzeroberfläche bietet verschiedene Such- und Filteroptionen auf der Zielkatalogseite:

* Verwenden Sie die Suchfunktion auf der Seite, um ein bestimmtes Ziel zu finden.
* Filtern Sie Ziele mithilfe des Steuerelements [!UICONTROL Kategorien].
* Wechsel zwischen [!UICONTROL Alle Ziele] und [!UICONTROL Meine Ziele]. Wenn Sie **[!UICONTROL Alle Ziele]** auswählen, werden alle verfügbaren [!DNL Platform]-Ziele angezeigt. Wenn Sie **[!UICONTROL Meine Ziele]** auswählen, können Sie nur die Ziele sehen, zu denen Sie eine Verbindung hergestellt haben.
* Wählen Sie zur Ansicht **[!UICONTROL Verbindungen]** und/oder **[!UICONTROL Erweiterungen]**. Informationen zum Unterschied zwischen den beiden Kategorien finden Sie unter [Zieltypen und Kategorien](../destination-types.md).

![Filtern und Suchdemo von Zielen](../assets/ui/workspace/destinations-search-and-filter.gif)

Die Zielkarten enthalten entweder ein **[!UICONTROL Configure]**- oder ein **[!UICONTROL Activate]**-Steuerelement und ein sekundäres Steuerelement, das weitere Optionen aufruft. Diese Kontrollen werden nachfolgend beschrieben:

| Kontrolle | Beschreibung |
|---------|----------|
| [!UICONTROL Konfigurieren von] | Ermöglicht Ihnen das Erstellen einer Verbindung mit dem Ziel. |
| [!UICONTROL Aktivieren] | Nachdem Sie eine Verbindung zum Ziel hergestellt haben, können Sie Segmente aktivieren. |
| [!UICONTROL Ansichten-Konto] | Ansicht der Konten, die Sie für ein Ziel verbunden haben. |
| [!UICONTROL Ansicht DataFlows] | Ansicht der Datenflüsse, die für ein Ziel vorhanden sind. |
| [!UICONTROL Dokumentation zur Ansicht] | Öffnet einen Link zur Dokumentationsseite für dieses spezifische Ziel, um weitere Informationen zu erhalten und die Einrichtung zu erleichtern. |

{style=&quot;table-layout:auto&quot;}

![Steuerelemente auf der Zielkarte](../assets/ui/workspace/destination-card-options.png)

Wählen Sie eine Zielkarte im Katalog aus, um die rechte Leiste zu öffnen. Hier sehen Sie eine Beschreibung des Ziels. Die rechte Leiste bietet dieselben in der obigen Tabelle beschriebenen Steuerelemente, einschließlich einer Beschreibung des Ziels und einer Angabe der Kategorie und des Typs des Ziels.

![Optionen im Zielkatalog](../assets/ui/workspace/destination-right-rail.png)

Weitere Informationen zu den Ziel-Kategorien und Informationen zu den einzelnen Zielen finden Sie unter [Zielkatalog](../catalog/overview.md) und [Zieltypen und Kategorien](../destination-types.md).

## [!UICONTROL Konten] {#accounts}

Das Register **[!UICONTROL Konten]** zeigt Details zu den Verbindungen an, die Sie mit verschiedenen Zielen eingerichtet haben, und ermöglicht Ihnen das Aktualisieren vorhandener Verbindungsdetails. Detaillierte Anweisungen finden Sie unter [Konten aktualisieren](update-accounts.md).

## [!UICONTROL Durchsuchen] {#browse}

Auf der Registerkarte **[!UICONTROL Durchsuchen]** werden die Ziele angezeigt, mit denen Sie eine Verbindung hergestellt haben. Ziele, bei denen der Umschalter **[!UICONTROL Aktiviert/Deaktiviert]** aktiviert ist, stellen Sie das Ziel auf aktiv bzw. inaktiv ein. Sie können die Ziele, an denen Daten fließen, auch durch Auswahl von **[!UICONTROL Segmente]** > **[!UICONTROL Durchsuchen]** und Auswahl eines zu prüfenden Segments Ansicht haben. Die nachstehende Tabelle enthält alle Informationen, die für die einzelnen Ziele auf der Registerkarte „Durchsuchen“ verfügbar sind:

>[!TIP]
>
> * Verwenden Sie die Schaltfläche ![Hinzufügen Segmente](../assets/ui/workspace/add-data-symbol.png) in der Spalte **[!UICONTROL Name]**, um [](activate-destinations.md) weitere Segmente zu diesem Ziel zu aktivieren.
> * Verwenden Sie die Schaltfläche ![Ziele löschen](../assets/ui/workspace/delete-destination-symbol.png) in der Spalte **[!UICONTROL Name]**, um [eine bestehende Verbindung zu einem Ziel zu löschen.](delete-destinations.md)


![Registerkarte „Durchsuchen“](../assets/ui/workspace/browse-tab.png)

| Element | Beschreibung |
|---------|----------|
| Name | Der Name, den Sie für den Aktivierungsfluss zu diesem Ziel angegeben haben. Dieselbe Spalte enthält zwei Steuerelemente: [!UICONTROL Aktivieren Sie ] und [!UICONTROL Löschen Sie das Ziel]. |
| [!UICONTROL Letzter Flusslaufstatus] | Der Status des letzten Datenflusses wird ausgeführt. Weitere Informationen zu Datenflug-Ansichten finden Sie unter [Zieldetails](destination-details-page.md). |
| [!UICONTROL Letzter Flusslaufdatum] | Zeit und Datum, an dem die letzte Ausführung des Datenflusses stattgefunden hat. Weitere Informationen zu Datenflug-Ansichten finden Sie unter [Zieldetails](destination-details-page.md). |
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
