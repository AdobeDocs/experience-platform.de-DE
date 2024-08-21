---
title: Exportieren von Dateien On-Demand an Batch-Ziele über die Experience Platform-Benutzeroberfläche
type: Tutorial
description: Erfahren Sie, wie Sie Dateien bei Bedarf mithilfe der Experience Platform-Benutzeroberfläche in Batch-Ziele exportieren.
exl-id: 0cbe5089-b73d-4584-8451-2fc34d47c357
source-git-commit: 47d0e2a7fae973edfda035d046f66c88d34bf8b2
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 16%

---


# Exportieren von Dateien On-Demand an Batch-Ziele über die Experience Platform-Benutzeroberfläche

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

## **[!UICONTROL Datei jetzt exportieren]** – Übersicht {#overview}

>[!CONTEXTUALHELP]
>id="platform_destinations_activationchaining_activatenow"
>title="Datei jetzt exportieren"
>abstract="Wählen Sie diese Option, um zusätzlich zu eventuell zuvor geplanten Exporten einen vollständigen Dateiexport vorzunehmen. Der Dateiexport wird sofort ausgelöst und die neuesten Ergebnisse der Segmentierungsdurchgänge von Experience Platform werden abgerufen."

In diesem Artikel wird erläutert, wie Sie mit der Experience Platform-Benutzeroberfläche Dateien bei Bedarf an Batch-Zielen wie [Cloud-Speicher](/help/destinations/catalog/cloud-storage/overview.md) und [E-Mail-Marketing](/help/destinations/catalog/email-marketing/overview.md)-Zielen exportieren können.

Mit dem Steuerelement **[!UICONTROL Datei jetzt exportieren]** können Sie eine vollständige Datei exportieren, ohne den aktuellen Exportplan einer zuvor geplanten Audience zu unterbrechen. Dieser Export erfolgt zusätzlich zu den zuvor geplanten Exporten und ändert nicht die Exportfrequenz der Audience. Der Dateiexport wird sofort ausgelöst und die neuesten Ergebnisse der Segmentierungsdurchgänge von Experience Platform werden abgerufen.

Zu diesem Zweck können Sie auch die Experience Platform-APIs verwenden. Erfahren Sie, wie Sie Zielgruppen bei Bedarf über die Ad-hoc-Aktivierungs-API ](/help/destinations/api/ad-hoc-activation-api.md) für Batch-Ziele aktivieren.[

## Voraussetzungen {#prerequisites}

Um Dateien On-Demand an Batch-Ziele zu exportieren, müssen Sie erfolgreich [mit einem Ziel verbunden haben](./connect-destination.md). Wenn Sie es noch nicht getan haben, navigieren Sie zum [Zielkatalog](../catalog/overview.md), durchsuchen Sie die unterstützten Ziele und konfigurieren Sie das Ziel, das Sie verwenden möchten.

## Exportieren von Dateien bei Bedarf {#how-to-export-files-on-demand}

1. Wechseln Sie zu **[!UICONTROL Verbindungen > Ziele]**, wählen Sie die Registerkarte **[!UICONTROL Durchsuchen]** und das Filtersymbol aus, um vorhandene Verbindungen zu Ihren gewünschten Batch-Zielen anzuzeigen.

   ![Bild, das zeigt, wie man zur Registerkarte &quot;Durchsuchen&quot;gelangt und vorhandene Datenflüsse filtert.](../assets/ui/activate-on-demand/browse-tab.png)

2. Wählen Sie die gewünschte Zielverbindung aus, um den vorhandenen Datenfluss zum Ziel zu überprüfen.

   ![ Bild, das einen gefilterten Datenfluss markiert.](../assets/ui/activate-on-demand/filtered-dataflow.png)

3. Wählen Sie den Tab **[!UICONTROL Aktivierungsdaten]** aus, wählen Sie die Zielgruppen aus, für die Sie Dateien On-Demand exportieren möchten, und wählen Sie das Steuerelement **[!UICONTROL Datei jetzt exportieren]** aus, um einen einmaligen Export Trigger, durch den eine Datei für jede ausgewählte Zielgruppe an Ihr Batch-Ziel gesendet wird.

   ![Bild, das die Schaltfläche &quot;Datei jetzt exportieren&quot;markiert.](../assets/ui/activate-on-demand/bulk-export-file-now.png)

4. Wählen Sie **[!UICONTROL Ja]** aus, um den Dateiexport zu bestätigen und Trigger.

   ![ Bild, das die Exportdatei anzeigt, jetzt Bestätigungsdialogfeld.](../assets/ui/activate-on-demand/confirm-activation.png)

5. Eine Bestätigungsmeldung wird angezeigt, die Sie darüber informiert, dass der Dateiexport gestartet wurde.

   ![Bild, das die Bestätigung einer erfolgreichen Ad-hoc-Aktivierung anzeigt.](../assets/ui/activate-on-demand/ad-hoc-success.png)

6. Sie können auch zur Registerkarte **[!UICONTROL Datenfluss-Ausführung]** wechseln, um zu bestätigen, dass der Dateiexport gestartet wurde.

## Zu beachten {#considerations}

Beachten Sie bei Verwendung des Steuerelements **[!UICONTROL Datei jetzt exportieren]** die folgenden Hinweise:

* **[!UICONTROL Datei jetzt exportieren]** funktioniert nur für Zielgruppen, deren Zeitplan im Batch-Aktivierungsdatenfluss mit dem aktuellen Datum überschneidet. Dazu gehören Zielgruppen mit Zeitplänen, die kein Enddatum haben (Exportfrequenz **[!UICONTROL Einmal]**) oder bei denen das Enddatum noch nicht erreicht wurde.
* Warten Sie beim Hinzufügen einer Zielgruppe zu einem vorhandenen Datenfluss mindestens 15 Minuten, bis Sie das Steuerelement **[!UICONTROL Datei jetzt exportieren]** verwenden.
* Wenn Sie die Zusammenführungsrichtlinie einer Zielgruppe ändern oder eine Zielgruppe erstellen, die eine neue Zusammenführungsrichtlinie verwendet, warten Sie 24 Stunden, bis Sie das Steuerelement **[!UICONTROL Datei jetzt exportieren]** verwenden.

## Benutzeroberflächenfehlermeldungen {#ui-error-messages}

Bei Verwendung des Steuerelements **[!UICONTROL Datei jetzt exportieren]** werden möglicherweise die unten aufgeführten Fehlermeldungen angezeigt. Überprüfen Sie die Tabelle, um zu verstehen, wie Sie sie bearbeiten können, wenn sie angezeigt werden.

| Fehlermeldung | Auflösung |
|---------|----------|
| Führen Sie bereits für die Zielgruppe `segment ID` für die Bestellung `dataflow ID` mit der Ausführungskennung `flow run ID` aus. | Diese Fehlermeldung weist darauf hin, dass derzeit ein Ad-hoc-Aktivierungsfluss für eine Zielgruppe ausgeführt wird. Warten Sie, bis der Auftrag abgeschlossen ist, bevor Sie den Aktivierungsauftrag erneut auslösen. |
| Zielgruppen `<segment name>` sind nicht Teil dieses Datenflusses oder außerhalb des festgelegten Zeitraums! | Diese Fehlermeldung weist darauf hin, dass die von Ihnen ausgewählten Zielgruppen nicht dem Datenfluss zugeordnet sind oder dass der für die Zielgruppen eingerichtete Aktivierungsplan entweder abgelaufen ist oder noch nicht gestartet wurde. Überprüfen Sie, ob die Audience tatsächlich dem Datenfluss zugeordnet ist, und stellen Sie sicher, dass sich der Aktivierungszeitplan für die Zielgruppe mit dem aktuellen Datum überschneidet. |

## Verwandte Informationen {#related-information}

* [Aktivieren von Zielgruppen für Batch-Ziele bei Bedarf mithilfe der Experience Platform-APIs](/help/destinations/api/ad-hoc-activation-api.md)
* [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](/help/destinations/ui/activate-batch-profile-destinations.md)
