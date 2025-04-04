---
title: On-Demand-Aufnahme für Datenflüsse von Quellen in der Benutzeroberfläche
description: Erfahren Sie, wie Sie Datenflüsse bei Bedarf für Ihre Quellverbindungen mithilfe der Experience Platform-Benutzeroberfläche erstellen.
exl-id: e5a70044-2484-416a-8098-48e6d99c2d98
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 0%

---

# On-Demand-Aufnahme von Quellen für Datenflüsse in der Benutzeroberfläche

Sie können die On-Demand-Aufnahme verwenden, um eine Flusslaufiteration eines bestehenden Datenflusses mithilfe des Arbeitsbereichs „Quellen“ in der Benutzeroberfläche von Adobe Experience Platform in Trigger zu setzen.

In diesem Dokument erfahren Sie, wie Sie bei Bedarf Datenflüsse für Quellen erstellen und Flussausführungen wiederholen, die verarbeitet wurden oder fehlgeschlagen sind.

>[!BEGINSHADEBOX]

**Was ist eine Flussausführung?**

Flussausführungen stellen eine Instanz der Datenflussausführung dar. Wenn ein Datenfluss beispielsweise so geplant ist, dass er stündlich um 9:00 Uhr, 10:00 Uhr und 11:00 Uhr ausgeführt wird, gibt es drei Instanzen eines Flussdurchgangs. Flussausführungen sind spezifisch für Ihre bestimmte Organisation.

>[!ENDSHADEBOX]

## Erste Schritte

>[!NOTE]
>
>Um eine Flussausführung zu erstellen, müssen Sie zunächst über die Fluss-ID eines Datenflusses verfügen, der für die einmalige Aufnahme geplant ist.

Dieses Dokument setzt ein Verständnis der folgenden Komponenten von Experience Platform voraus:

* [Quellen](../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Datenflüsse](../../../dataflows/home.md): Ein Datenfluss ist eine Darstellung von Datenvorgängen, die Daten über Experience Platform verschieben. Datenflüsse werden über verschiedene Services konfiguriert und helfen beim Verschieben von Daten aus Quell-Connectoren in Zieldatensätze, in Identity Service, in Echtzeit-Kundenprofile und in Ziele.
* [Sandboxes](../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

## Erstellen eines Datenflusses bei Bedarf {#create-a-dataflow-on-demand}

Navigieren Sie zur *[!UICONTROL Datenflüsse]* im Arbeitsbereich Quellen . Suchen Sie hier nach dem Datenfluss, den Sie bei Bedarf ausführen möchten, und wählen Sie dann die Auslassungszeichen (**`...`**) neben Ihrem Datenflussnamen aus.

![Eine Liste der Datenflüsse im Quellarbeitsbereich.](../../images/tutorials/on-demand/select-dataflow.png)

Wählen Sie als Nächstes **[!UICONTROL Auf Anforderung ausführen]** aus dem angezeigten Dropdown-Menü aus.

![Ein Dropdown-Menü mit ausgewählter Option Auf Anforderung ausführen.](../../images/tutorials/on-demand/run-on-demand.png)

Konfigurieren Sie den Zeitplan für die On-Demand-Aufnahme. Wählen Sie **[!UICONTROL Aufnahmestartzeit]**, die **[!UICONTROL Startzeit des Datumsbereichs]** und die **[!UICONTROL Endzeit des Datumsbereichs]**.

| Konfiguration planen | Beschreibung |
| --- | --- |
| [!UICONTROL Startzeit der Aufnahme] | Der geplante Zeitpunkt, zu dem die Ausführung des On-Demand-Flusses beginnt. |
| [!UICONTROL Startzeit des Datumsbereichs] | Das früheste Datum und die früheste Uhrzeit, von dem/der die Daten abgerufen werden. |
| [!UICONTROL Endzeit des Datumsbereichs] | Datum und Uhrzeit, zu der die Daten abgerufen werden. |

Wählen Sie **[!UICONTROL Zeitplan]** aus und gewähren Sie etwas Zeit für Ihren On-Demand-Datenfluss zum Trigger.

![Das Zeitplankonfigurationsfenster für die On-Demand-Aufnahme.](../../images/tutorials/on-demand/configure-schedule.png)

Wählen Sie Ihren Datenflussnamen aus, um Ihre Datenflussaktivität anzuzeigen. Hier sehen Sie eine Liste Ihrer Datenflussausführungen, die verarbeitet wurden. Sie können einzelne Iterationen Ihrer Datenflussausführungen erneut ausführen, unabhängig davon, ob sie fehlgeschlagen oder erfolgreich waren. Bei fehlgeschlagenen Ausführungsiterationen können Sie mit **[!UICONTROL Wiederholen]** den Durchlauf erneut starten, nachdem Sie etwaige Fehler, die während des Erstellungsprozesses aufgetreten sind, diagnostiziert und behoben haben.

![Eine Liste verarbeiteter Flussausführungen für einen ausgewählten Datenfluss.](../../images/tutorials/on-demand/processed.png)

Wählen Sie **[!UICONTROL Geplant]** aus, um eine Liste der Datenflussausführungen anzuzeigen, die für die zukünftige Aufnahme geplant sind.

![Eine Liste geplanter Flussdurchgänge für einen ausgewählten Datenfluss.](../../images/tutorials/on-demand/scheduled.png)

## Nächste Schritte

Durch das Lesen dieses Dokuments haben Sie gelernt, wie Sie bei Bedarf Flussausführungen für bestehende Datenflüsse von Quellen erstellen können. Weitere Informationen zu Quellen finden Sie im Abschnitt [Quellen - Übersicht](../../home.md)
