---
keywords: Plattform; Ziele; Arbeitsbereich "Ziele"; Arbeitsbereich; UI; Ziele in der Benutzeroberfläche; Katalog; Zielkatalog;
title: Arbeitsbereich „Ziele“
description: 'Der Arbeitsbereich Ziele besteht aus vier Bereichen: Katalog, Durchsuchen, Konten und Systemansicht. Sie werden in den folgenden Abschnitten beschrieben.'
seo-description: In Adobe Experience Platform, select Destinations from the left navigation bar to access the destinations workspace.
exl-id: 0f46f08d-0fe3-441d-933a-86bc146c0f19
source-git-commit: b275621d9c6552327e0e55c00c8fcf0397088168
workflow-type: tm+mt
source-wordcount: '1156'
ht-degree: 18%

---

# Arbeitsbereich „Ziele“ {#destinations-workspace}

Wählen Sie in Adobe Experience Platform **[!UICONTROL Ziele]** über die linke Navigationsleiste, um auf die [!UICONTROL Ziele] Arbeitsbereich.

Die [!UICONTROL Ziele] Arbeitsbereich besteht aus fünf Bereichen, [!UICONTROL Übersicht], [!UICONTROL Katalog], [!UICONTROL Durchsuchen], [!UICONTROL Konten]und [!UICONTROL Systemansicht], wie in den folgenden Abschnitten beschrieben.

![Zielüberblick](../assets/ui/workspace/destinations-overview.png)

## [!UICONTROL Übersicht] {#overview}

Die **[!UICONTROL Übersicht]** angezeigt wird, [!UICONTROL Ziele] Dashboard, das wichtige Metriken zu den Zieldaten Ihres Unternehmens bereitstellt. Weitere Informationen finden Sie unter [[!UICONTROL Ziele] Dashboard-Handbuch](../../dashboards/guides/destinations.md).

>[!NOTE]
>
>Wenn Ihr Unternehmen neu bei Experience Platform ist und noch keine aktiven Ziele hat, wird die [!UICONTROL Ziele] Dashboard und [!UICONTROL Übersicht] nicht sichtbar sind. Wählen Sie stattdessen [!UICONTROL Ziele] über die linke Navigation zeigt die [[!UICONTROL Katalog] tab](#catalog).

![](../../dashboards/images/destinations/dashboard-overview.png)

## [!UICONTROL Katalog] {#catalog}

Die **[!UICONTROL Katalog]** zeigt eine Liste aller Ziele an, die in [!DNL Platform], an die Sie Daten senden können.

Die [!DNL Platform] Die Benutzeroberfläche bietet mehrere Such- und Filteroptionen auf der Zielkatalogseite:

* Verwenden Sie die Suchfunktion auf der Seite, um ein bestimmtes Ziel zu finden.
* Filtern von Zielen mithilfe des [!UICONTROL Kategorien] Kontrolle.
* Zwischen wechseln [!UICONTROL Alle Ziele] und [!UICONTROL Meine Ziele]. Wenn Sie **[!UICONTROL Alle Ziele]**, alle verfügbar [!DNL Platform] -Ziele angezeigt. Wenn Sie **[!UICONTROL Meine Ziele]**, können Sie nur die Ziele sehen, mit denen Sie eine Verbindung hergestellt haben.
* Zum Anzeigen auswählen **[!UICONTROL Verbindungen]** und/oder **[!UICONTROL Erweiterungen]**. Informationen zum Unterschied zwischen den beiden Kategorien finden Sie unter [Zieltypen und -kategorien](../destination-types.md).

![Katalog](../assets/ui/workspace/catalog.png)

Die Zielkarten enthalten entweder eine **[!UICONTROL Einrichten]** oder **[!UICONTROL Segmente aktivieren]** und ein sekundäres Steuerelement, das mehr Optionen anzeigt. Diese Steuerelemente werden nachfolgend beschrieben:

| Kontrolle | Beschreibung |
|---------|----------|
| [!UICONTROL Einrichten] | Ermöglicht die Erstellung einer Verbindung zum Ziel. |
| [!UICONTROL Aktivieren von Segmenten] | Nachdem Sie eine Verbindung zum Ziel hergestellt haben, können Sie Segmente aktivieren. |
| [!UICONTROL Konto anzeigen] | Zeigen Sie die Konten an, mit denen Sie eine Verbindung zu einem Ziel hergestellt haben. |
| [!UICONTROL Datenflüsse anzeigen] | Zeigen Sie die Datenaktivierungsflüsse an, die für ein Ziel vorhanden sind. |
| [!UICONTROL Dokumentation anzeigen] | Öffnet einen Link zur Dokumentationsseite für dieses spezifische Ziel, um weitere Informationen zu erhalten und Sie bei der Einrichtung zu unterstützen. |

{style=&quot;table-layout:auto&quot;}

![Steuerelemente auf der Zielkarte](../assets/ui/workspace/destination-card-options.png)

Wählen Sie eine Zielkarte im Katalog aus, um die rechte Leiste zu öffnen. Hier können Sie eine Beschreibung des Ziels sehen. Die rechte Leiste bietet dieselben in der obigen Tabelle beschriebenen Steuerelemente, einschließlich einer Beschreibung des Zielorts und einer Angabe der Zielkategorie und des Zieltyps.

![Optionen im Zielkatalog](../assets/ui/workspace/destination-right-rail.png)

Weitere Informationen zu Zielkategorien und Informationen zu den einzelnen Zielen finden Sie in der [Zielkatalog](../catalog/overview.md) und [Zieltypen und Kategorien](../destination-types.md).

## [!UICONTROL Konten] {#accounts}

Die **[!UICONTROL Konten]** zeigt Details zu den Verbindungen an, die Sie mit verschiedenen Zielen hergestellt haben, und ermöglicht es Ihnen, vorhandene Kontodetails zu aktualisieren oder zu löschen. Die nachstehende Tabelle enthält alle Informationen zu den einzelnen Zielkonten.

>[!TIP]
>
> * Wählen Sie die drei Punkte im [!UICONTROL Plattform] und verwenden Sie die ![Schaltfläche &quot;Segmente aktivieren&quot;](../assets/ui/workspace/add-data-symbol.png)**[!UICONTROL Segmente aktivieren ]**-Schaltfläche, um Segmente an dieses Ziel zu senden.
> * Wählen Sie die drei Punkte im [!UICONTROL Plattform] und verwenden Sie die ![Schaltfläche &quot;Details bearbeiten&quot;](../assets/ui/workspace/pencil-icon.png)**[!UICONTROL Details bearbeiten ]**Schaltfläche zu [update](update-accounts.md) die Details eines vorhandenen Zielkontos.
> * Wählen Sie die drei Punkte im [!UICONTROL Plattform] und verwenden Sie die ![Schaltfläche &quot;Löschen&quot;](../assets/ui/workspace/delete-destination-symbol.png)**[!UICONTROL Löschen ]**Schaltfläche zu [delete](delete-destination-account.md) ein vorhandenes Zielkonto.


![Registerkarte „Konten“](../assets/ui/workspace/destination-account-options.png)

| Element | Beschreibung |
|---|---|
| [!UICONTROL Plattform] | Das Ziel, für das Sie die Verbindung eingerichtet haben. |
| [!UICONTROL Verbindungstyp] | Stellt den Verbindungstyp des Kontos zu Ihrem Speicherbehälter oder Ziel dar. Je nach Ziel stehen folgende Authentifizierungsoptionen zur Verfügung: <ul><li>Für E-Mail-Marketing-Ziele: Kann S3, FTP oder Azure Blob sein.</li><li>Bei Echtzeit-Werbezielen: Server-zu-Server.</li><li>Bei Amazon S3-Cloud-Speicherzielen: Zugriffsschlüssel. </li><li>Bei SFTP-Cloud-Speicherzielen: Grundlegende Authentifizierung für SFTP.</li><li>OAuth 1- oder OAuth 2-Authentifizierung</li><li>Trägertoken-Authentifizierung</li></ul> |
| [!UICONTROL Benutzername] | Der Benutzername, den Sie im [Zielverbindungsassistenten](../catalog/email-marketing/overview.md#connect-destination) ausgewählt haben. |
| [!UICONTROL Ziele] | Stellt die Anzahl der eindeutigen erfolgreichen Ziel-Datenflüsse dar, die mit grundlegenden Informationen verknüpft sind, die für ein Ziel erstellt wurden. |
| [!UICONTROL Autorisiert] | Das Datum, an dem die Verbindung zu diesem Ziel genehmigt wurde. |

{style=&quot;table-layout:auto&quot;}

## [!UICONTROL Durchsuchen] {#browse}

Auf der Registerkarte **[!UICONTROL Durchsuchen]** werden die Ziele angezeigt, mit denen Sie eine Verbindung hergestellt haben. Ziele mit der **[!UICONTROL Aktiviert/Deaktiviert]** Umschalten aktiviert: Setzen Sie das Ziel auf &quot;aktiv&quot;bzw. &quot;inaktiv&quot;. Sie können auch die Ziele anzeigen, an denen Daten fließen, indem Sie **[!UICONTROL Segmente]** > **[!UICONTROL Durchsuchen]** und wählen Sie ein zu prüfendes Segment aus. Die nachstehende Tabelle enthält alle Informationen, die für die einzelnen Ziele in der [!UICONTROL Durchsuchen] tab:

>[!TIP]
>
> * Wählen Sie die drei Punkte im [!UICONTROL Name] und verwenden Sie die ![Schaltfläche &quot;Segmente aktivieren&quot;](../assets/ui/workspace/add-data-symbol.png)**[!UICONTROL Segmente aktivieren ]**-Schaltfläche, um Segmente an dieses Ziel zu senden.
> * Wählen Sie die drei Punkte im [!UICONTROL Name] und verwenden Sie die ![Schaltfläche &quot;Löschen&quot;](../assets/ui/workspace/delete-destination-symbol.png)**[!UICONTROL Löschen ]**Schaltfläche zu [remove](delete-destinations.md) eine bestehende Verbindung zu einem Ziel.
> * Wählen Sie die drei Punkte im [!UICONTROL Name] und verwenden Sie die ![Anzeigen in Überwachungsschaltfläche](../assets/ui/workspace/monitoring-icon.png)**[!UICONTROL Anzeigen in der Überwachung ]**Schaltfläche zum Anzeigen der Aktivierungsinformationen für dieses Ziel im [Monitoring-Dashboard](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard).
> * Wählen Sie die drei Punkte im [!UICONTROL Name] und verwenden Sie die ![Warnhinweise abonnieren ](../assets/ui/workspace/alerts-icon.png)**[!UICONTROL Warnhinweise abonnieren ]**Schaltfläche zum Abonnieren von Ziel-Datenfluss-Warnhinweisen. Sie können Warnhinweise abonnieren, um Nachrichten zum Status, Erfolg oder Misserfolg Ihrer Workflow-Ausführung zu erhalten. Siehe [In-Context-Zielwarnungen abonnieren](alerts.md) für detaillierte Informationen zu Ziel-Datenfluss-Warnhinweisen.


![Registerkarte „Durchsuchen“](../assets/ui/workspace/browse-tab.png)

| Element | Beschreibung |
|---------|----------|
| Name | Der Name, den Sie für den Aktivierungsfluss zu diesem Ziel angegeben haben. Dieselbe Spalte enthält zwei Steuerelemente: [!UICONTROL Aktivieren ] und [!UICONTROL Ziel löschen]. |
| [!UICONTROL Status des letzten Flusslaufs] | Der Status des letzten Datenflusses. Siehe [Zieldetails anzeigen](destination-details-page.md) für weitere Informationen zu Datenfluss-Läufen. |
| [!UICONTROL Letztes Flusslaufdatum] | Zeit und Datum, an dem der letzte Datenfluss durchgeführt wurde. Siehe [Zieldetails anzeigen](destination-details-page.md) für weitere Informationen zu Datenfluss-Läufen. |
| [!UICONTROL Ziel] | Die Zielplattform, die Sie für Ihren Aktivierungsfluss ausgewählt haben. |
| [!UICONTROL Verbindungstyp] | Stellt den Verbindungstyp zu Ihrem Speicher-Bucket oder Ziel dar. <ul><li>Für E-Mail-Marketing-Ziele: Kann S3, FTP oder [!DNL Azure Blob].</li><li>Für Werbeziele in Echtzeit: Server-zu-Server.</li><li>Für Streaming-Ziele: Kann [!DNL Azure Event Hubs] oder [!DNL Amazon Kinesis].</li></ul> |
| [!UICONTROL Benutzername] | Die Kontoanmeldedaten, die Sie für den Zielfluss ausgewählt haben. |
| [!UICONTROL Aktivierungsdaten] | Gibt die Anzahl der Segmente an, die für dieses Ziel aktiviert werden. Wählen Sie dieses Steuerelement aus, um mehr über die aktivierten Segmente zu erfahren. Siehe [Aktivierungsdaten](/help/destinations/ui/destination-details-page.md#activation-data) auf der Zieldetailseite finden Sie weitere Informationen zu den aktivierten Segmenten. |
| [!UICONTROL Erstellt] | Datum und Uhrzeit (UTC) der Erstellung des Aktivierungsflusses zum Ziel. Wählen Sie das Pfeilsymbol nach oben/unten aus, um die Aktivierungsflüsse zuerst nach dem neuesten oder dem ältesten zu sortieren. |
| [!UICONTROL Status] | `Enabled` oder `Disabled`. Gibt an, ob für dieses Ziel Daten aktiviert werden. |

Klicken Sie auf eine Zielzeile, um weitere Informationen zum Ziel in der rechten Leiste anzuzeigen.

![Auf Zielzeile klicken](../assets/ui/workspace/click-destination-row.png)

Wählen Sie den Zielnamen aus, um Informationen zu den für dieses Ziel aktivierten Segmenten anzuzeigen. Klicken Sie auf **[!UICONTROL Aktivierung bearbeiten]**, um die Segmente, die an dieses Ziel gesendet werden, zu ändern oder hinzuzufügen.

## [!UICONTROL Systemansicht] {#system-view}

Die **[!UICONTROL Systemansicht]** zeigt eine grafische Darstellung der Aktivierungsflüsse an, die Sie in der Adobe Experience Platform eingerichtet haben.

![Datenflüsse1](../assets/ui/workspace/data-flows1.png)

Wählen Sie eines der Ziele aus, die auf der Seite angezeigt werden, und klicken Sie auf **[!UICONTROL Datenflüsse anzeigen]** um Informationen zu allen Verbindungen anzuzeigen, die Sie für jedes Ziel eingerichtet haben.

![Datenflüsse2](../assets/ui/workspace/data-flows2.png)
