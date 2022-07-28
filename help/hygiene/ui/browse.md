---
title: Durchsuchen von Datenhygiene-Arbeitsaufträgen
description: Erfahren Sie, wie Sie bestehende Datenhygiene-Arbeitsaufträge in der Benutzeroberfläche von Adobe Experience Platform anzeigen und verwalten können.
exl-id: 76d4a809-cc2c-434d-90b1-23d88f29c022
source-git-commit: 7f1e4bdf54314cab1f69619bcbb34216da94b17e
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 95%

---

# Durchsuchen von Datenhygiene-Arbeitsaufträgen {#browse-work-orders}

>[!CONTEXTUALHELP]
>id="platform_hygiene_workorders"
>title="IDs für Arbeitsaufträge"
>abstract="Wenn eine Datenhygiene-Anfrage an das System gesendet wird, wird ein Arbeitsauftrag erstellt, um die angeforderte Aufgabe auszuführen. Anders ausgedrückt, ist ein Arbeitsauftrag ein spezifischer Datenhygiene-Prozess, der seinen aktuellen Status und andere zugehörige Details enthält. Bei der Erstellung eines Arbeitsauftrags wird diesem automatisch eine eigene eindeutige ID zugewiesen."
>text="See the data hygiene UI guide to learn more."

>[!IMPORTANT]
>
>Die Funktionen zur Datenhygiene in Adobe Experience Platform sind derzeit nur für Organisationen verfügbar, die den Gesundheitsschild erworben haben.

Wenn eine Datenhygiene-Anfrage an das System gesendet wird, wird ein Arbeitsauftrag erstellt, um die angeforderte Aufgabe auszuführen. Ein Arbeitsauftrag stellt einen bestimmten Datenhygieneprozess dar, z. B. eine geplante Time-to-Live (TTL) für einen Datensatz, wobei sein aktueller Status und andere zugehörige Details enthalten sind.

In diesem Handbuch wird beschrieben, wie Sie bestehende Arbeitsaufträge in der Adobe Experience Platform-Benutzeroberfläche anzeigen und verwalten können.

## Auflisten und Filtern vorhandener Arbeitsaufträge

Wenn Sie zum ersten Mal auf den Arbeitsbereich **[!UICONTROL Datenhygiene]** in der Benutzeroberfläche zugreifen, wird eine Liste der vorhandenen Arbeitsaufträge mit allgemeinen Details angezeigt.

![Bild, das den Arbeitsbereich [!UICONTROL Datenhygiene] in der Platform-Benutzeroberfläche zeigt](../images/ui/browse/work-order-list.png)

<!-- The list only shows work orders for one category at a time. Select **[!UICONTROL Consumer]** to view a list of consumer deletion tasks, and **[!UICONTROL Dataset]** to view a list of time-to-live (TTL) schedules for datasets.

![Image showing the [!UICONTROL Dataset] tab](../images/ui/browse/dataset-tab.png) -->

Wählen Sie das Trichtersymbol (![Bild des Trichtersymbols](../images/ui/browse/funnel-icon.png)) aus, um eine Liste von Filtern für die angezeigten Arbeitsaufträge aufzurufen.

![Bild der angezeigten Arbeitsauftragsfilter](../images/ui/browse/filters.png)

| Filter | Beschreibung |
| --- | --- |
| [!UICONTROL Status] | Filtern Sie nach dem aktuellen Status des Arbeitsauftrags. |
| [!UICONTROL Erstellt am] | Filtern Sie auf der Grundlage des Zeitpunkts, zu dem die TTL-Anfrage für den Datensatz gestellt wurde. |
| [!UICONTROL Löschdatum] | Filtern Sie nach dem Löschdatum, das in der TTL geplant ist. |
| [!UICONTROL Aktualisierungsdatum] | Filtern Sie nach dem Zeitpunkt, zu dem die Datensatz-TTL zuletzt aktualisiert wurde. Die Erstellung und das Ablaufen der Gültigkeit der TTL werden als Aktualisierungen gezählt. |

{style=&quot;table-layout:auto&quot;}

## Anzeigen der Details eines Arbeitsauftrags

Wählen Sie die ID eines aufgelisteten Arbeitsauftrags aus, um dessen Details anzuzeigen.

![Bild, das die ausgewählte Arbeitsauftrags-ID anzeigt](../images/ui/browse/select-work-order.png)

<!-- Depending on the type of work order selected, different information and controls are provided. These are covered in the sections below.

### Consumer delete details

>[!CONTEXTUALHELP]
>id="platform_hygiene_responsemessages"
>title="Consumer delete response"
>abstract="When a consumer deletion process receives a response from the system, these messages are displayed under the **[!UICONTROL Result]** section. If a problem occurs while a work order is processing, any relevant error messages will appear in this section to help you troubleshoot the issue. To learn more, see the data hygiene UI guide."


The details of a consumer delete request are read-only, displaying its basic attributes such as its current status and the time elapsed since the request was made.

![Image showing the details page for a consumer delete work order](../images/ui/browse/consumer-delete-details.png)

### Dataset TTL details -->

Die Detailseite für eine Datensatz-TTL enthält Informationen zu allgemeinen Attributen, einschließlich des geplanten Ablaufdatums und der vor der Löschung verbleibenden Tage. In der rechten Leiste können Sie Steuerelemente verwenden, um die TTL zu bearbeiten oder abzubrechen.

![Bild, das die Detailseite für einen Datensatz-TTL-Arbeitsauftrag zeigt](../images/ui/browse/ttl-details.png)

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie vorhandene Datenhygiene-Arbeitsaufträge in der Platform-Benutzeroberfläche anzeigen und verwalten können. Informationen zum Erstellen eigener Arbeitsaufträge finden Sie im Handbuch zum [Planen der TTL eines Datensatzes](./ttl.md).
