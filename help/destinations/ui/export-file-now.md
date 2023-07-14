---
title: (Beta) Exportieren von Dateien nach Bedarf in Batch-Ziele mithilfe der Experience Platform-Benutzeroberfläche
type: Tutorial
description: Erfahren Sie, wie Sie Dateien bei Bedarf mithilfe der Experience Platform-Benutzeroberfläche in Batch-Ziele exportieren.
exl-id: 0cbe5089-b73d-4584-8451-2fc34d47c357
source-git-commit: 165793619437f403045b9301ca6fa5389d55db31
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 22%

---

# (Beta) Exportieren von Dateien nach Bedarf in Batch-Ziele mithilfe der Experience Platform-Benutzeroberfläche

>[!IMPORTANT]
>
>Die **[!UICONTROL Datei jetzt exportieren]** -Option in Adobe Experience Platform ist derzeit als Betaversion verfügbar. Dokumentation und Funktionalitäten können sich ändern.
>Wenden Sie sich an den Adobe-Support-Mitarbeiter, um Zugriff auf diese Funktion zu erhalten.

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die [Zugriffskontrollberechtigungen](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**. Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

## **[!UICONTROL Datei jetzt exportieren]** Übersicht {#overview}

>[!CONTEXTUALHELP]
>id="platform_destinations_activationchaining_activatenow"
>title="Datei jetzt exportieren"
>abstract="Wählen Sie diese Option, um zusätzlich zu eventuell zuvor geplanten Exporten einen vollständigen Dateiexport vorzunehmen. Der Dateiexport wird sofort ausgelöst, und es werden die neuesten Ergebnisse der Segmentierungsläufe von Experience Platform abgerufen."

In diesem Artikel wird erläutert, wie Sie die Experience Platform-Benutzeroberfläche verwenden können, um Dateien bei Bedarf an Batch-Zielen wie [Cloud-Speicher](/help/destinations/catalog/cloud-storage/overview.md) und [E-Mail-Marketing](/help/destinations/catalog/email-marketing/overview.md) Ziele.

Die **[!UICONTROL Datei jetzt exportieren]** Mit dieser Kontrolle können Sie eine vollständige Datei exportieren, ohne den aktuellen Exportplan einer zuvor geplanten Audience zu unterbrechen. Dieser Export erfolgt zusätzlich zu den zuvor geplanten Exporten und ändert nicht die Exportfrequenz der Audience. Der Dateiexport wird sofort ausgelöst, und es werden die neuesten Ergebnisse der Segmentierungsläufe von Experience Platform abgerufen.

Zu diesem Zweck können Sie auch die Experience Platform-APIs verwenden. Lesen der Anleitung [Aktivieren von Zielgruppen bei Bedarf für Batch-Ziele über die Ad-hoc-Aktivierungs-API](/help/destinations/api/ad-hoc-activation-api.md).

## Voraussetzungen {#prerequisites}

Um Dateien On-Demand an Batch-Ziele zu exportieren, müssen Sie erfolgreich [mit Ziel verbunden](./connect-destination.md). Wenn Sie es noch nicht getan haben, navigieren Sie zum [Zielkatalog](../catalog/overview.md), durchsuchen Sie die unterstützten Ziele und konfigurieren Sie das Ziel, das Sie verwenden möchten.

## Exportieren von Dateien bei Bedarf {#how-to-export-files-on-demand}

1. Navigieren Sie zu **[!UICONTROL Verbindungen > Ziele]**, wählen Sie die **[!UICONTROL Durchsuchen]** und das Filtersymbol, um vorhandene Verbindungen zu den gewünschten Batch-Zielen anzuzeigen.

   ![Bild, das zeigt, wie Sie zur Registerkarte &quot;Durchsuchen&quot;gelangen und vorhandene Datenflüsse filtern können.](../assets/ui/activate-on-demand/browse-tab.png)

2. Wählen Sie die gewünschte Zielverbindung aus, um den vorhandenen Datenfluss zum Ziel zu überprüfen.

   ![Bild, das einen gefilterten Datenfluss markiert.](../assets/ui/activate-on-demand/filtered-dataflow.png)

3. Wählen Sie die **[!UICONTROL Aktivierungsdaten]** und wählen Sie die Audience aus, für die Sie eine Datei bei Bedarf exportieren möchten, und wählen Sie die **[!UICONTROL Datei jetzt exportieren]** -Steuerelement, um einen einmaligen Export Trigger, der eine Datei an Ihr Batch-Ziel sendet.

   >[!IMPORTANT]
   >
   >Die Auswahl mehrerer Zielgruppen für den Massenexport von Dateien bei Bedarf wird in der Benutzeroberfläche derzeit nicht unterstützt. Verwenden Sie die [Ad-hoc-Aktivierungs-API](/help/destinations/api/ad-hoc-activation-api.md) zu diesem Zweck.

   ![Bild, das die Schaltfläche Datei jetzt exportieren markiert.](../assets/ui/activate-on-demand/activate-segment-on-demand.png)

4. Auswählen **[!UICONTROL Ja]** , um den Dateiexport zu bestätigen und zu Trigger zu führen.

   ![Bild mit dem Bestätigungsdialogfeld &quot;Datei exportieren&quot;.](../assets/ui/activate-on-demand/confirm-activation.png)

5. Eine Bestätigungsmeldung wird angezeigt, die Sie darüber informiert, dass der Dateiexport gestartet wurde.

   ![Bild mit Bestätigung einer erfolgreichen Ad-hoc-Aktivierung.](../assets/ui/activate-on-demand/ad-hoc-success.png)

6. Sie können auch zum **[!UICONTROL Datenfluss-Abläufe]** um zu bestätigen, dass der Dateiexport gestartet wurde.

## Zu beachten {#considerations}

Beachten Sie bei der Verwendung der **[!UICONTROL Datei jetzt exportieren]** Kontrolle:

* **[!UICONTROL Datei jetzt exportieren]** funktioniert nur für Zielgruppen, deren Zeitplan im Batch-Aktivierungsdataflow sich mit dem aktuellen Datum überschneidet. Dies umfasst Zielgruppen mit Zeitplänen, die kein Enddatum haben (Exportfrequenz von **[!UICONTROL Einmal]**) oder wenn das Enddatum noch nicht überschritten wurde.
* Warten Sie beim Hinzufügen einer Zielgruppe zu einem vorhandenen Datenfluss mindestens 15 Minuten, bis Sie die Variable **[!UICONTROL Datei jetzt exportieren]** Kontrolle.
* Wenn Sie die Zusammenführungsrichtlinie einer Zielgruppe ändern oder eine Zielgruppe erstellen, die eine neue Zusammenführungsrichtlinie verwendet, warten Sie 24 Stunden, bis Sie die **[!UICONTROL Datei jetzt exportieren]** Kontrolle.

## Benutzeroberflächenfehlermeldungen {#ui-error-messages}

Bei Verwendung von **[!UICONTROL Datei jetzt exportieren]** -Kontrolle verwenden, können Sie auf eine der unten aufgeführten Fehlermeldungen stoßen. Überprüfen Sie die Tabelle, um zu verstehen, wie Sie sie bearbeiten können, wenn sie angezeigt werden.

| Fehlermeldung | Auflösung |
|---------|----------|
| Bereits für die Zielgruppe ausgeführt `segment ID` für die Bestellung `dataflow ID` mit Run-ID `flow run ID` | Diese Fehlermeldung weist darauf hin, dass derzeit ein Ad-hoc-Aktivierungsfluss für eine Zielgruppe ausgeführt wird. Warten Sie, bis der Auftrag abgeschlossen ist, bevor Sie den Aktivierungsauftrag erneut auslösen. |
| Zielgruppen `<segment name>` sind nicht Teil dieses Datenflusses oder außerhalb des Zeitplanbereichs! | Diese Fehlermeldung weist darauf hin, dass die von Ihnen ausgewählten Zielgruppen nicht dem Datenfluss zugeordnet sind oder dass der für die Zielgruppen eingerichtete Aktivierungsplan entweder abgelaufen ist oder noch nicht gestartet wurde. Überprüfen Sie, ob die Audience tatsächlich dem Datenfluss zugeordnet ist, und stellen Sie sicher, dass sich der Aktivierungszeitplan für die Zielgruppe mit dem aktuellen Datum überschneidet. |

## Verwandte Informationen {#related-information}

* [Aktivieren von Zielgruppen für Batch-Ziele On-Demand mithilfe der Experience Platform-APIs](/help/destinations/api/ad-hoc-activation-api.md)
* [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](/help/destinations/ui/activate-batch-profile-destinations.md)
