---
keywords: Plattform;Ziele;Arbeitsbereich Ziele;Arbeitsbereich;Benutzeroberfläche;Ziele in der Benutzeroberfläche;Katalog;Zielkatalog;
title: Arbeitsbereich „Ziele“
description: 'Der Arbeitsbereich „Ziele“ besteht aus fünf Bereichen: Übersicht, Katalog, Durchsuchen, Konten und Systemansicht. Sie werden in den folgenden Abschnitten beschrieben.'
exl-id: 0f46f08d-0fe3-441d-933a-86bc146c0f19
source-git-commit: a2420f86e650ce1ca8a5dc01d9a29548663d3f7c
workflow-type: tm+mt
source-wordcount: '1300'
ht-degree: 75%

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

Die [!DNL Experience Platform]-Benutzeroberfläche bietet mehrere Such- und Filteroptionen auf der Zielkatalogseite:

* Verwenden Sie die Suchfunktion auf der Seite, um ein bestimmtes Ziel zu finden.
* Filtern Sie Ziele mithilfe der Steuerung [!UICONTROL Kategorien].
* Schalten Sie zwischen [!UICONTROL Alle Ziele] und [!UICONTROL Meine Ziele] um. Wenn Sie **[!UICONTROL Alle Ziele]** auswählen, werden alle verfügbar [!DNL Experience Platform]-Ziele angezeigt. Wenn Sie **[!UICONTROL Meine Ziele]** auswählen, können Sie nur die Ziele sehen, zu denen Sie eine Verbindung hergestellt haben.
* Wählen Sie aus, die Typen von **[!UICONTROL Verbindungen]** und/oder **[!UICONTROL Erweiterungen]** anzuzeigen. Um den Unterschied zwischen den beiden Kategorien zu verstehen, lesen Sie [Zieltypen und -kategorien](../destination-types.md).

![Zielkatalog mit einigen Werbe- und Cloud-Speicher-Zielen.](../assets/ui/workspace/catalog.png)

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

## [!UICONTROL Konten] {#accounts}

Die Registerkarte **[!UICONTROL Konten]** zeigt Details zu den Verbindungen an, die Sie mit verschiedenen Zielen hergestellt haben, und ermöglicht es Ihnen, vorhandene Kontodetails zu aktualisieren oder zu löschen. In der nachstehenden Tabelle sehen Sie alle Informationen, die Sie über jedes Zielkonto erhalten können.

>[!TIP]
>
> * Klicken Sie auf die Auslassungszeichen (`...`) in der Spalte [!UICONTROL Platform] und verwenden Sie das Steuerelement ![Kontrolle aktivieren](/help/images/icons/data-add.png)**[!UICONTROL Aktivieren &#x200B;]**/**[!UICONTROL &#x200B; Zielgruppen aktivieren &#x200B;]**/**[!UICONTROL &#x200B; Datensätze exportieren &#x200B;]**, um Zielgruppen oder Datensätze in dieses Ziel zu exportieren.
> * Klicken Sie auf die Auslassungszeichen (`...`) in der Spalte [!UICONTROL Platform] und verwenden Sie das Steuerelement ![Steuerung „Details bearbeiten“](/help/images/icons/edit.png)**[!UICONTROL Details bearbeiten &#x200B;]**, um die Details eines vorhandenen Zielkontos zu [aktualisieren](update-accounts.md).
> * Klicken Sie auf die Auslassungszeichen (`...`) in der Spalte [!UICONTROL Platform] und verwenden Sie das Steuerelement ![Steuerung „Löschen“](/help/images/icons/delete.png)**[!UICONTROL Löschen &#x200B;]**, um ein vorhandenes Zielkonto zu [löschen](delete-destination-account.md).

![Registerkarte „Konten“](../assets/ui/workspace/destination-account-options.png)

| Element | Beschreibung |
|---|---|
| [!UICONTROL Ziel] | Der Ziel-Connector, für den Sie die Verbindung eingerichtet haben. |
| [!UICONTROL Verbindungstyp] | Gibt den Kontoverbindungstyp zu Ihrem Speicher-Behälter oder Ziel an. Je nach Ziel stehen folgende Authentifizierungsoptionen zur Verfügung: <ul><li>Bei E-Mail-Marketing-Zielen: S3, FTP oder Azure Blob.</li><li>Bei Echtzeit-Werbezielen: Server-zu-Server.</li><li>Bei Amazon S3-Cloud-Speicherzielen: Zugriffsschlüssel. </li><li>Bei SFTP-Cloud-Speicherzielen: Grundlegende Authentifizierung für SFTP.</li><li>OAuth 1- oder OAuth 2-Authentifizierung</li><li>Authentifizierung über Bearer-Token</li></ul> |
| [!UICONTROL Benutzername] | Der Benutzername, den Sie im Workflow [Ziel verbinden“ ausgewählt ](../catalog/email-marketing/overview.md#connect-destination). |
| [!UICONTROL Verbindungen] | Gibt die Zahl der eindeutigen erfolgreich verbundenen Ziel-Datenflüsse an, die für ein Ziel erstellt wurden, zusammen mit grundlegenden Informationen. |
| [!UICONTROL Autorisierungsdatum] | Das Datum, an dem die Verbindung zu diesem Ziel genehmigt wurde. |
| [!UICONTROL Ablaufdatum] | Das Datum, an dem die Verbindungsautorisierung zu diesem Ziel abläuft. <br>**Wichtig**: Diese Spalte ist derzeit nur für die [Facebook“ ](../catalog/social/facebook.md). |

{style="table-layout:auto"}

## [!UICONTROL Durchsuchen] {#browse}

Auf der Registerkarte **[!UICONTROL Durchsuchen]** werden die Ziele angezeigt, mit denen Sie eine Verbindung hergestellt haben. Bei Zielen, für die der Umschalter **[!UICONTROL Aktiviert/Deaktiviert]** eingeschaltet ist, wird das Ziel auf „aktiv“ bzw. „inaktiv“ gesetzt. Sie können auch die Ziele anzeigen, bei denen Daten fließen, indem Sie **[!UICONTROL Zielgruppen]** > **[!UICONTROL Durchsuchen]** und eine zu überprüfende Zielgruppe auswählen. Die nachstehende Tabelle enthält alle Informationen, die für die einzelnen Ziele auf der Registerkarte [!UICONTROL Durchsuchen] verfügbar sind:

>[!TIP]
>
> * Klicken Sie auf die Auslassungszeichen (`...`) in der Spalte [!UICONTROL Name] und verwenden Sie das Steuerelement ![Steuerung „Zielgruppen aktivieren](/help/images/icons/data-add.png)**[!UICONTROL Aktivieren &#x200B;]**, um Zielgruppen oder Datensätze in dieses Ziel zu exportieren.
> * Klicken Sie auf die Auslassungszeichen (`...`) in der Spalte [!UICONTROL Name] und verwenden Sie das Steuerelement ![Steuerung „Löschen“](/help/images/icons/delete.png)**[!UICONTROL Löschen &#x200B;]**, um eine bestehende Verbindung zu einem Ziel zu [löschen](delete-destinations.md).
> * Klicken Sie auf die Auslassungszeichen (`...`) in der Spalte [!UICONTROL Name] und verwenden Sie das Steuerelement ![Steuerung „Im Monitoring anzeigen“](/help/images/icons/monitoring.png)**[!UICONTROL „Im Monitoring anzeigen“]**, um Aktivierungsinformationen für dieses Ziel im [Monitoring-Dashboard](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard) anzuzeigen.
> * Klicken Sie auf die Auslassungszeichen (`...`) in der Spalte [!UICONTROL Name] und verwenden Sie das Steuerelement ![Steuerung „Warnhinweise abonnieren“](/help/images/icons/alert-add.png)**[!UICONTROL Warnhinweise abonnieren &#x200B;]**, um Ziel-Datenfluss-Warnhinweise zu abonnieren. Sie können Warnhinweise abonnieren, um Nachrichten zum Status, Erfolg oder Misserfolg Ihres Datenflusses zu erhalten. Ausführliche Informationen zu Ziel-Datenfluss-Warnhinweisen finden Sie unter [Abonnieren von kontextabhängigen Ziel-Warnhinweisen](alerts.md).

![Registerkarte „Durchsuchen“](../assets/ui/workspace/browse-tab.png)

| Element | Beschreibung |
|---------|----------|
| Name | Der Name, den Sie für den Aktivierungsfluss zu diesem Ziel angegeben haben. Dieselbe Spalte enthält zwei Steuerelemente: [!UICONTROL Aktivieren] und [!UICONTROL Ziel löschen]. |
| Datentyp | Der von der Zielverbindung unterstützte Datentyp. Unterstützte Datentypen: <ul><li>**[!UICONTROL Kunden]**</li><li>**[!UICONTROL Interessenten]**</li><li>**[!UICONTROL Konten]**</li><li>**[!UICONTROL Datensätze]**</li></ul> |
| [!UICONTROL Letzter Ausführungsstatus für Datenfluss] | Der Status der letzten Datenflussausführung. Weitere Informationen zur Ausführung von Datenflüssen finden Sie unter [Anzeigen von Zieldetails](destination-details-page.md). |
| [!UICONTROL Letztes Ausführungsdatum für Datenfluss] | Zeit und Datum, an dem der letzte Datenfluss ausgeführt wurde. Weitere Informationen zur Ausführung von Datenflüssen finden Sie unter [Anzeigen von Zieldetails](destination-details-page.md). |
| [!UICONTROL Ziel] | Die Zielplattform, die Sie für Ihren Aktivierungsfluss ausgewählt haben. |
| [!UICONTROL Ablaufdatum des Kontos] | Das Datum, an dem die Verbindungsautorisierung zu diesem Ziel abläuft. <br>**Wichtig**: Diese Spalte ist derzeit nur für die [Facebook“ ](../catalog/social/facebook.md). |
| [!UICONTROL Verbindungstyp] | Stellt den Verbindungstyp zu Ihrem Speicher-Bucket oder Ziel dar. <ul><li>Bei E-Mail-Marketing-Zielen: S3, FTP oder [!DNL Azure Blob].</li><li>Bei Echtzeit-Werbezielen: Server-zu-Server.</li><li>Bei Streaming-Zielen: [!DNL Azure Event Hubs] oder [!DNL Amazon Kinesis].</li></ul> |
| [!UICONTROL Benutzername] | Die Kontoanmeldedaten, die Sie für den Zielfluss ausgewählt haben. |
| [!UICONTROL Aktivierungsdaten] | Gibt die Anzahl der Zielgruppen an, die für dieses Ziel aktiviert werden. Wählen Sie dieses Steuerelement aus, um mehr über die aktivierten Zielgruppen zu erfahren. Weitere Informationen zu [ aktivierten Zielgruppen finden ](/help/destinations/ui/destination-details-page.md#activation-data) auf der Zieldetailseite unter „Aktivierungsdaten“. |
| [!UICONTROL Erstellt] | Datum und Uhrzeit (UTC) der Erstellung des Aktivierungsflusses zum Ziel. Klicken Sie auf das Symbol mit dem Pfeil nach oben/unten, um nach den neuesten oder ältesten Aktivierungsflüssen zu sortieren. |
| [!UICONTROL Status] | `Enabled` oder `Disabled`. Gibt an, ob für dieses Ziel Daten aktiviert sind. |

Klicken Sie auf eine Zielzeile, um weitere Informationen zum Ziel in der rechten Leiste aufzurufen, z. B. Ziel-ID, Beschreibung, Anzahl der aktivierten Zielgruppen und mehr.

![Auf Zielzeile klicken](../assets/ui/workspace/click-destination-row.png)

Wählen Sie den Zielnamen aus, um Informationen über die für dieses Ziel aktivierten Zielgruppen anzuzeigen. Klicken Sie **[!UICONTROL Aktivierung bearbeiten]**, um die Zielgruppen, die an dieses Ziel gesendet werden, zu ändern oder hinzuzufügen.

## [!UICONTROL Systemansicht] {#system-view}

Auf der Registerkarte **[!UICONTROL Systemansicht]** wird eine grafische Darstellung der Aktivierungsflüsse angezeigt, die Sie in Adobe Experience Platform eingerichtet haben.

![Data-flows1](../assets/ui/workspace/data-flows1.png)

Wählen Sie eines der Ziele aus, die auf der Seite angezeigt werden, und klicken Sie auf **[!UICONTROL Datenflüsse anzeigen]**, um Informationen über alle Verbindungen anzuzeigen, die Sie für die einzelnen Ziele eingerichtet haben.

![Data-flows2](../assets/ui/workspace/data-flows2.png)
