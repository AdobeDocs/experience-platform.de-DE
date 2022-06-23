---
title: (Beta) Exportieren Sie Dateien On-Demand mithilfe der Experience Platform-Benutzeroberfläche in Batch-Ziele
type: Tutorial
description: Erfahren Sie, wie Sie Dateien bei Bedarf mithilfe der Experience Platform-Benutzeroberfläche in Batch-Ziele exportieren.
hide: true
hidefromtoc: true
source-git-commit: ff0fe836b2bb181ae4395f1d04c04b8e51a5bac6
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 6%

---

# (Beta) Exportieren Sie Dateien On-Demand mithilfe der Experience Platform-Benutzeroberfläche in Batch-Ziele

>[!IMPORTANT]
>
>Die **[!UICONTROL Datei jetzt exportieren]** -Option in Adobe Experience Platform Destination SDK ist derzeit als Betaversion verfügbar. Dokumentation und Funktionalität können sich ändern.

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

## **[!UICONTROL Datei jetzt exportieren]** Übersicht {#overview}

>[!CONTEXTUALHELP]
>id="platform_destinations_activationchaining_activatenow"
>title="Datei jetzt exportieren"
>abstract="Wählen Sie dieses Steuerelement aus, um zusätzlich zu allen zuvor geplanten Exporten einen vollständigen Dateiexport bereitzustellen. Der Dateiexport wird sofort ausgelöst und es werden die neuesten Ergebnisse aus der Experience Platform-Segmentierung abgerufen."

In diesem Artikel wird erläutert, wie Sie die Experience Platform-Benutzeroberfläche verwenden können, um Dateien bei Bedarf an Batch-Zielen wie [Cloud-Speicher](/help/destinations/catalog/cloud-storage/overview.md) und [E-Mail-Marketing](/help/destinations/catalog/email-marketing/overview.md) Ziele.

Die **[!UICONTROL Datei jetzt exportieren]** Mit dieser Kontrolle können Sie eine vollständige Datei exportieren, ohne die aktuelle Exportplanung eines zuvor geplanten Segments zu unterbrechen. Dieser Export erfolgt zusätzlich zu den zuvor geplanten Exporten und ändert nicht die Exportfrequenz des Segments. Der Dateiexport wird sofort ausgelöst und es werden die neuesten Ergebnisse aus der Experience Platform-Segmentierung abgerufen.

Zu diesem Zweck können Sie auch die Experience Platform-APIs verwenden. Lesen der Anleitung [Aktivieren von Zielgruppensegmenten bei Bedarf für Batch-Ziele über die Ad-hoc-Aktivierungs-API](/help/destinations/api/ad-hoc-activation-api.md).

## Voraussetzungen {#prerequisites}

Um Dateien On-Demand an Batch-Ziele zu exportieren, müssen Sie erfolgreich [mit Ziel verbunden](./connect-destination.md). Wenn Sie das noch nicht getan haben, navigieren Sie zum [Zielkatalog](../catalog/overview.md), durchsuchen Sie die unterstützten Ziele und konfigurieren Sie das Ziel, das Sie verwenden möchten.

## Exportieren von Dateien bei Bedarf {#how-to-export-files-on-demand}

1. Navigieren Sie zu **[!UICONTROL Verbindungen > Ziele]**, wählen Sie die **[!UICONTROL Durchsuchen]** und das Filtersymbol, um vorhandene Verbindungen zu den gewünschten Batch-Zielen anzuzeigen.

   ![Bild, das zeigt, wie Sie zur Registerkarte &quot;Durchsuchen&quot;gelangen und vorhandene Datenflüsse filtern können.](../assets/ui/activate-on-demand/browse-tab.png)

2. Wählen Sie die gewünschte Zielverbindung aus, um den vorhandenen Datenfluss zum Ziel zu überprüfen.

   ![Bild, das einen gefilterten Datenfluss markiert.](../assets/ui/activate-on-demand/filtered-dataflow.png)

3. Wählen Sie die **[!UICONTROL Aktivierungsdaten]** und wählen Sie das Segment aus, für das Sie eine Datei bei Bedarf exportieren möchten, und wählen Sie die **[!UICONTROL Datei jetzt exportieren]** -Steuerelement, um einen einmaligen Export Trigger, der eine Datei an Ihr Batch-Ziel sendet.

   >[!IMPORTANT]
   >
   >Die Auswahl mehrerer Segmente für den Massenexport von Dateien bei Bedarf wird in der Benutzeroberfläche derzeit nicht unterstützt. Verwenden Sie die [Ad-hoc-Aktivierungs-API](/help/destinations/api/ad-hoc-activation-api.md) zu diesem Zweck.

   ![Bild, das die Schaltfläche Datei jetzt exportieren markiert.](../assets/ui/activate-on-demand/activate-segment-on-demand.png)

4. Auswählen **[!UICONTROL Ja]** , um den Dateiexport zu bestätigen und zu Trigger zu führen.

   ![Bild mit dem Bestätigungsdialogfeld &quot;Datei exportieren&quot;.](../assets/ui/activate-on-demand/confirm-activation.png)

5. Eine Bestätigungsmeldung wird angezeigt, die Sie darüber informiert, dass der Dateiexport gestartet wurde.

   ![Bild mit Bestätigung einer erfolgreichen Ad-hoc-Aktivierung.](../assets/ui/activate-on-demand/ad-hoc-success.png)

6. Sie können auch zum **[!UICONTROL Datenfluss-Abläufe]** um zu bestätigen, dass der Dateiexport gestartet wurde.

## Zu beachten {#considerations}

Beachten Sie bei der Verwendung der **[!UICONTROL Datei jetzt exportieren]** Kontrolle:

* **[!UICONTROL Datei jetzt exportieren]** funktioniert nur für Segmente, deren Zeitplan im Batch-Aktivierungsdataflow sich mit dem aktuellen Datum überschneidet. Dies umfasst Segmente mit Zeitplänen, die kein Enddatum haben (Exporthäufigkeit von **[!UICONTROL Einmal]**) oder wenn das Enddatum noch nicht überschritten wurde.
* Warten Sie beim Hinzufügen eines Segments zu einem vorhandenen Datenfluss mindestens 15 Minuten, bis Sie die Variable **[!UICONTROL Datei jetzt exportieren]** Kontrolle.
* Wenn Sie die Zusammenführungsrichtlinie eines Segments ändern oder ein Segment erstellen, das eine neue Zusammenführungsrichtlinie verwendet, warten Sie 24 Stunden, bis Sie die **[!UICONTROL Datei jetzt exportieren]** Kontrolle.

## Benutzeroberflächenfehlermeldungen {#ui-error-messages}

Bei Verwendung von **[!UICONTROL Datei jetzt exportieren]** -Kontrolle verwenden, können Sie auf eine der unten aufgeführten Fehlermeldungen stoßen. Überprüfen Sie die Tabelle, um zu verstehen, wie Sie sie bearbeiten können, wenn sie angezeigt werden.

| Fehlermeldung | Auflösung |
|---------|----------|
| Bereits für ein Segment ausführen `segment ID` für die Bestellung `dataflow ID` mit Run-ID `flow run ID` | Diese Fehlermeldung weist darauf hin, dass derzeit ein Ad-hoc-Aktivierungsfluss für ein Segment ausgeführt wird. Warten Sie, bis der Auftrag abgeschlossen ist, bevor Sie den Aktivierungsauftrag erneut auslösen. |
| Segmente `<segment name>` sind nicht Teil dieses Datenflusses oder außerhalb des Zeitplanbereichs! | Diese Fehlermeldung weist darauf hin, dass die von Ihnen ausgewählten Segmente nicht dem Datenfluss zugeordnet sind oder dass der für die Segmente eingerichtete Aktivierungsplan entweder abgelaufen ist oder noch nicht gestartet wurde. Überprüfen Sie, ob das Segment tatsächlich dem Datenfluss zugeordnet ist, und stellen Sie sicher, dass sich der Zeitplan für die Segmentaktivierung mit dem aktuellen Datum überschneidet. |

## Verwandte Informationen {#related-information}

* [Aktivieren von Zielgruppensegmenten für Batch-Ziele On-Demand mithilfe der Experience Platform-APIs](/help/destinations/api/ad-hoc-activation-api.md)
* [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](/help/destinations/ui/activate-batch-profile-destinations.md)