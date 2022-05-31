---
title: Durchsuchen von Arbeitshygiene-Aufträgen
description: Erfahren Sie, wie Sie bestehende Workflows zur Datenhygiene in der Benutzeroberfläche von Adobe Experience Platform anzeigen und verwalten.
exl-id: 76d4a809-cc2c-434d-90b1-23d88f29c022
source-git-commit: c24aa700eb425770266bbee5c187e2e87b15a9ac
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 1%

---

# Arbeitserstellungen zur Datenhygiene durchsuchen {#browse-work-orders}

>[!CONTEXTUALHELP]
>id="platform_hygiene_workorders"
>title="IDs für Arbeitsaufträge"
>abstract="Wenn an das System eine Anforderung zur Datenhygiene gesendet wird, wird eine Arbeitsreihenfolge erstellt, um die angeforderte Aufgabe auszuführen. Mit anderen Worten, ein Arbeitsauftrag stellt einen spezifischen Datenhygiene-Prozess dar, der seinen aktuellen Status und andere zugehörige Details enthält. Bei der Erstellung wird jedem Arbeitsauftrag automatisch eine eigene eindeutige ID zugewiesen."
>text="See the data hygiene UI guide to learn more."

>[!IMPORTANT]
>
>Die Funktionen zur Datenhygiene in Adobe Experience Platform sind derzeit nur für Organisationen verfügbar, die Adobe Shield für das Gesundheitswesen erworben haben.

Wenn an das System eine Anforderung zur Datenhygiene gesendet wird, wird eine Arbeitsreihenfolge erstellt, um die angeforderte Aufgabe auszuführen. Eine Arbeitsreihenfolge stellt einen bestimmten Datenhygieneprozess dar, z. B. eine geplante Live-Zeit (TTL) für einen Datensatz, der seinen aktuellen Status und andere zugehörige Details enthält.

In diesem Handbuch wird beschrieben, wie Sie bestehende Arbeitsaufträge in der Adobe Experience Platform-Benutzeroberfläche anzeigen und verwalten.

## Auflisten und Filtern vorhandener Arbeitsaufträge

Wenn Sie zum ersten Mal auf **[!UICONTROL Datenhygiene]** Arbeitsbereich in der Benutzeroberfläche werden eine Liste der bestehenden Arbeitsaufträge mit ihren grundlegenden Details angezeigt.

![Bild, das die [!UICONTROL Datenhygiene] Workspace in der Platform-Benutzeroberfläche](../images/ui/browse/work-order-list.png)

<!-- The list only shows work orders for one category at a time. Select **[!UICONTROL Consumer]** to view a list of consumer deletion tasks, and **[!UICONTROL Dataset]** to view a list of time-to-live (TTL) schedules for datasets.

![Image showing the [!UICONTROL Dataset] tab](../images/ui/browse/dataset-tab.png) -->

Wählen Sie das Trichtersymbol (![Bild des Trichtersymbols](../images/ui/browse/funnel-icon.png)), um eine Liste von Filtern für die angezeigten Arbeitsaufträge anzuzeigen.

![Bild der angezeigten Arbeitsreihenfilter](../images/ui/browse/filters.png)

| Filter | Beschreibung |
| --- | --- |
| [!UICONTROL Status] | Filtern Sie nach dem aktuellen Status der Arbeitsreihenfolge. |
| [!UICONTROL Erstellungsdatum] | Filtern Sie nach dem Zeitpunkt, zu dem die TTL-Anforderung des Datensatzes gestellt wurde. |
| [!UICONTROL Löschdatum] | Filtern Sie nach dem Löschdatum, das die TTL geplant hat. |
| [!UICONTROL Datum aktualisiert] | Filtern Sie nach dem Zeitpunkt, zu dem die TTL des Datensatzes zuletzt aktualisiert wurde. TTL-Erstellung und -Gültigkeit werden als Aktualisierungen gezählt. |

{style=&quot;table-layout:auto&quot;}

## Details eines Arbeitsauftrags anzeigen

Wählen Sie die ID einer aufgelisteten Arbeitsreihenfolge aus, um deren Details anzuzeigen.

![Bild, das die ausgewählte Workflow-Bestell-ID anzeigt](../images/ui/browse/select-work-order.png)

<!-- Depending on the type of work order selected, different information and controls are provided. These are covered in the sections below.

### Consumer delete details

>[!CONTEXTUALHELP]
>id="platform_hygiene_responsemessages"
>title="Consumer delete response"
>abstract="When a consumer deletion process receives a response from the system, these messages are displayed under the **[!UICONTROL Result]** section. If a problem occurs while a work order is processing, any relevant error messages will appear in this section to help you troubleshoot the issue. To learn more, see the data hygiene UI guide."


The details of a consumer delete request are read-only, displaying its basic attributes such as its current status and the time elapsed since the request was made.

![Image showing the details page for a consumer delete work order](../images/ui/browse/consumer-delete-details.png)

### Dataset TTL details -->

Die Detailseite für einen Datensatz-TTL enthält Informationen zu seinen grundlegenden Attributen, einschließlich des geplanten Ablaufdatums für die Tage, die vor dem Löschen verbleiben. In der rechten Leiste können Sie Steuerelemente verwenden, um die TTL zu bearbeiten oder abzubrechen.

![Bild, das die Detailseite für eine TTL-Arbeitsreihenfolge des Datensatzes anzeigt](../images/ui/browse/ttl-details.png)

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie bestehende Workflows zur Datenhygiene in der Platform-Benutzeroberfläche anzeigen und verwalten. Informationen zum Erstellen eigener Arbeitsaufträge finden Sie im Handbuch unter [Datensatz-TTL planen](./ttl.md).
