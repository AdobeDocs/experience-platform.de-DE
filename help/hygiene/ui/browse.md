---
title: Durchsuchen von Datenhygiene-Arbeitsaufträgen
description: Erfahren Sie, wie Sie bestehende Datenhygiene-Arbeitsaufträge in der Benutzeroberfläche von Adobe Experience Platform anzeigen und verwalten können.
exl-id: 76d4a809-cc2c-434d-90b1-23d88f29c022
source-git-commit: 49ba5263c6dc8eccac2ffe339476cf316c68e486
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 68%

---

# Durchsuchen von Datenhygiene-Arbeitsaufträgen {#browse-work-orders}

>[!CONTEXTUALHELP]
>id="platform_hygiene_workorders"
>title="IDs für Arbeitsaufträge"
>abstract="Wenn eine Datenhygiene-Anfrage an das System gesendet wird, wird ein Arbeitsauftrag erstellt, um die angeforderte Aufgabe auszuführen. Anders ausgedrückt, ist ein Arbeitsauftrag ein spezifischer Datenhygiene-Prozess, der seinen aktuellen Status und andere zugehörige Details enthält. Bei der Erstellung eines Arbeitsauftrags wird diesem automatisch eine eigene eindeutige ID zugewiesen."
>text="See the data hygiene UI guide to learn more."

>[!IMPORTANT]
>
>Die Datenhygiene-Funktionen in Adobe Experience Platform sind derzeit nur für Organisationen verfügbar, die Healthcare Shield erworben haben.

Wenn eine Datenhygiene-Anfrage an das System gesendet wird, wird ein Arbeitsauftrag erstellt, um die angeforderte Aufgabe auszuführen. Eine Arbeitsanweisung stellt einen bestimmten Datenhygieneprozess dar, z. B. einen geplanten Datensatzablauf, der den aktuellen Status und andere zugehörige Details enthält.

In diesem Handbuch wird beschrieben, wie Sie bestehende Arbeitsaufträge in der Adobe Experience Platform-Benutzeroberfläche anzeigen und verwalten können.

## Auflisten und Filtern vorhandener Arbeitsaufträge

Wenn Sie zum ersten Mal auf den Arbeitsbereich **[!UICONTROL Datenhygiene]** in der Benutzeroberfläche zugreifen, wird eine Liste der vorhandenen Arbeitsaufträge mit allgemeinen Details angezeigt.

![Bild, das den Arbeitsbereich [!UICONTROL Datenhygiene] in der Platform-Benutzeroberfläche zeigt](../images/ui/browse/work-order-list.png)

<!-- The list only shows work orders for one category at a time. Select **[!UICONTROL Consumer]** to view a list of consumer deletion tasks, and **[!UICONTROL Dataset]** to view a list of scheduled dataset expirations.

![Image showing the [!UICONTROL Dataset] tab](../images/ui/browse/dataset-tab.png) -->

Wählen Sie das Trichtersymbol (![Bild des Trichtersymbols](../images/ui/browse/funnel-icon.png)) aus, um eine Liste von Filtern für die angezeigten Arbeitsaufträge aufzurufen.

![Bild der angezeigten Arbeitsauftragsfilter](../images/ui/browse/filters.png)

| Filter | Beschreibung |
| --- | --- |
| [!UICONTROL Status] | Filtern Sie nach dem aktuellen Status des Arbeitsauftrags:<ul><li>**[!UICONTROL Abgeschlossen]**: Der Vorgang ist abgeschlossen.</li><li>**[!UICONTROL Ausstehend]**: Der Vorgang wurde erstellt, aber noch nicht ausgeführt. A [Datensatzablaufanfrage](./dataset-expiration.md) nimmt diesen Status vor dem geplanten Löschdatum an. Zum Löschdatum ändert sich der Status auf [!UICONTROL Wird ausgeführt], sofern der Vorgang nicht zuvor bereits abgebrochen wurde.</li><li>**[!UICONTROL Wird ausgeführt]**: Die Anfrage zum Ablauf des Datensatzes wurde gestartet und wird derzeit verarbeitet.</li><li>**[!UICONTROL Abgebrochen]**: Der Vorgang wurde im Rahmen einer manuellen Benutzeranfrage abgebrochen.</li></ul> |
| [!UICONTROL Erstellt am] | Filtern Sie nach dem Zeitpunkt, zu dem der Arbeitsauftrag erstellt wurde. |
| [!UICONTROL Ablaufdatum] | Filtern Sie die Anforderungen zum Ablauf von Datensätzen basierend auf dem geplanten Löschdatum für den betreffenden Datensatz. |
| [!UICONTROL Aktualisierungsdatum] | Filtern Sie die Anforderungen zum Ablauf von Datensätzen basierend auf dem Zeitpunkt, zu dem die Arbeitsreihenfolge zuletzt aktualisiert wurde. Kreationen und Abläufe werden als Updates gezählt. |

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

### Dataset expiration details -->

Die Detailseite für den Ablauf eines Datensatzes enthält Informationen zu seinen grundlegenden Attributen, einschließlich des geplanten Ablaufdatums für die Tage, die vor dem Löschvorgang verbleiben. In der rechten Leiste können Sie Steuerelemente verwenden, um den Ablauf zu bearbeiten oder abzubrechen.

![Bild mit der Detailseite für eine Arbeitsreihenfolge zum Ablauf eines Datensatzes](../images/ui/browse/ttl-details.png)

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie vorhandene Datenhygiene-Arbeitsaufträge in der Platform-Benutzeroberfläche anzeigen und verwalten können. Informationen zum Erstellen eigener Arbeitsaufträge finden Sie im Handbuch unter [Planen des Ablaufs eines Datensatzes](./dataset-expiration.md).
