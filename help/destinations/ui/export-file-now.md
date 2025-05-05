---
title: Exportieren von Dateien nach Bedarf an Batch-Ziele mithilfe der Experience Platform-Benutzeroberfläche
type: Tutorial
description: Erfahren Sie, wie Sie Dateien über die Experience Platform-Benutzeroberfläche bei Bedarf in Batch-Ziele exportieren können.
exl-id: 0cbe5089-b73d-4584-8451-2fc34d47c357
source-git-commit: d3bd76f5b36b6a6afcb67fe923eb8e4f3d7a9415
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 16%

---


# Exportieren von Dateien nach Bedarf an Batch-Ziele mithilfe der Experience Platform-Benutzeroberfläche

>[!IMPORTANT]
> 
>Zum Aktivieren von Daten benötigen Sie die Berechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**&#x200B;[Zugriffssteuerung](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

## **[!UICONTROL Datei jetzt exportieren]** – Übersicht {#overview}

>[!CONTEXTUALHELP]
>id="platform_destinations_activationchaining_activatenow"
>title="Datei jetzt exportieren"
>abstract="Wählen Sie diese Option, um zusätzlich zu eventuell zuvor geplanten Exporten einen vollständigen Dateiexport vorzunehmen. Der Dateiexport wird sofort ausgelöst und die neuesten Ergebnisse der Segmentierungsdurchgänge von Experience Platform werden abgerufen."

In diesem Artikel wird erläutert, wie Sie mit der Experience Platform-Benutzeroberfläche Dateien bei Bedarf in Batch-Ziele wie [Cloud-Speicher](/help/destinations/catalog/cloud-storage/overview.md) und E-[-Marketing](/help/destinations/catalog/email-marketing/overview.md) exportieren können.

Das **[!UICONTROL Datei jetzt exportieren]**-Steuerelement ermöglicht den Export einer vollständigen Datei, ohne den aktuellen Exportzeitplan einer zuvor geplanten Zielgruppe zu unterbrechen. Dieser Export erfolgt zusätzlich zu den zuvor geplanten Exporten und ändert nichts an der Exportfrequenz der Zielgruppe. Der Dateiexport wird sofort ausgelöst und die neuesten Ergebnisse der Segmentierungsdurchgänge von Experience Platform werden abgerufen.

Hierfür können Sie auch die Experience Platform-APIs verwenden. Erfahren Sie[ wie Sie Zielgruppen bei Bedarf über die Ad-hoc-Aktivierungs-API für Batch-Ziele aktivieren ](/help/destinations/api/ad-hoc-activation-api.md).

## Voraussetzungen {#prerequisites}

Um Dateien On-Demand in Batch-Ziele zu exportieren, müssen Sie erfolgreich [mit einem Ziel verbunden](./connect-destination.md). Wenn Sie es noch nicht getan haben, navigieren Sie zum [Zielkatalog](../catalog/overview.md), durchsuchen Sie die unterstützten Ziele und konfigurieren Sie das Ziel, das Sie verwenden möchten.

## Exportieren von Dateien nach Bedarf {#how-to-export-files-on-demand}

1. Gehen Sie zu **[!UICONTROL Verbindungen > Ziele]**, wählen Sie die Registerkarte **[!UICONTROL Durchsuchen]** und das Filtersymbol aus, um vorhandene Verbindungen zu Ihren gewünschten Batch-Zielen anzuzeigen.

   ![Abbildung mit hervorgehobenen Informationen zum Aufrufen der Registerkarte „Durchsuchen“ und zum Filtern vorhandener Datenflüsse.](../assets/ui/activate-on-demand/browse-tab.png)

2. Wählen Sie die gewünschte Zielverbindung aus, um den vorhandenen Datenfluss zum Ziel zu überprüfen.

   ![Abbildung mit hervorgehobener Darstellung eines gefilterten Datenflusses.](../assets/ui/activate-on-demand/filtered-dataflow.png)

3. Wählen Sie auf der Registerkarte **[!UICONTROL Aktivierungsdaten]** die Zielgruppen aus, für die Sie die Dateien bei Bedarf exportieren möchten, und wählen Sie das Steuerelement **[!UICONTROL Datei jetzt exportieren]** aus, um einen einmaligen Trigger zu erstellen, mit dem für jede ausgewählte Zielgruppe eine Datei an Ihr Batch-Ziel gesendet wird.

   ![Abbildung mit hervorgehobener Schaltfläche „Datei jetzt exportieren“](../assets/ui/activate-on-demand/bulk-export-file-now.png)

4. Wählen Sie **[!UICONTROL Ja]** aus, um den Dateiexport zu bestätigen und Trigger.

   ![Bild mit dem Bestätigungsdialogfeld „Datei jetzt exportieren“.](../assets/ui/activate-on-demand/confirm-activation.png)

5. Es wird eine Bestätigungsmeldung angezeigt, die Sie darüber informiert, dass der Dateiexport gestartet wurde.

   ![Bild mit Bestätigung einer erfolgreichen Ad-hoc-Aktivierung.](../assets/ui/activate-on-demand/ad-hoc-success.png)

6. Sie können auch zur Registerkarte **[!UICONTROL Datenflussausführungen]** wechseln, um zu bestätigen, dass der Dateiexport gestartet wurde.

## Zu beachten {#considerations}

Beachten Sie bei der Verwendung des Steuerelements **[!UICONTROL Datei jetzt exportieren]** die folgenden Überlegungen:

* **[!UICONTROL Datei jetzt exportieren]** funktioniert nur für Zielgruppen, deren Zeitplan im Batch-Aktivierungsdatenfluss sich mit dem aktuellen Datum überschneidet. Dazu gehören Zielgruppen mit Zeitplänen, die kein Enddatum haben (Exportfrequenz **[!UICONTROL einmal]**) oder bei denen das Enddatum noch nicht überschritten ist.
* Warten Sie beim Hinzufügen einer Zielgruppe zu einem vorhandenen Datenfluss mindestens **Stunde** bevor Sie das Steuerelement **[!UICONTROL Datei jetzt exportieren]** verwenden.
* Wenn Sie die Zusammenführungsrichtlinie einer Zielgruppe ändern oder eine Zielgruppe erstellen, die eine neue Zusammenführungsrichtlinie verwendet, warten Sie 24 Stunden, bis Sie das Steuerelement **[!UICONTROL Datei jetzt exportieren]** verwenden.

## Fehlermeldungen in der Benutzeroberfläche {#ui-error-messages}

Wenn Sie das Steuerelement **[!UICONTROL Datei jetzt exportieren]** verwenden, können Sie auf eine der unten aufgeführten Fehlermeldungen stoßen. Überprüfen Sie die Tabelle, um zu verstehen, wie Sie darauf reagieren, wenn sie angezeigt werden.

| Fehlermeldung | Auflösung |
|---------|----------|
| Ausführung läuft bereits für Zielgruppen-`segment ID` für `dataflow ID` mit Ausführungs-ID `flow run ID` | Diese Fehlermeldung weist darauf hin, dass derzeit ein Ad-hoc-Aktivierungsfluss für eine Zielgruppe läuft. Warten Sie, bis der Vorgang abgeschlossen ist, bevor Sie den Aktivierungsvorgang erneut auslösen. |
| Zielgruppen `<segment name>` sind nicht Teil dieses Datenflusses oder außerhalb des Zeitplanbereichs! | Diese Fehlermeldung zeigt an, dass die Zielgruppen, die Sie aktivieren möchten, nicht dem Datenfluss zugeordnet sind oder dass der für die Zielgruppen eingerichtete Aktivierungsplan entweder abgelaufen oder noch nicht gestartet wurde. Überprüfen Sie, ob die Zielgruppe tatsächlich dem Datenfluss zugeordnet ist, und stellen Sie sicher, dass sich der Zeitplan für die Zielgruppenaktivierung mit dem aktuellen Datum überschneidet. |

## Verwandte Informationen {#related-information}

* [Aktivieren von Zielgruppen für Batch-Ziele nach Bedarf mithilfe der Experience Platform-APIs](/help/destinations/api/ad-hoc-activation-api.md)
* [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](/help/destinations/ui/activate-batch-profile-destinations.md)
