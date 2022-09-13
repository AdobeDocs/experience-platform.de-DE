---
title: Durchsuchen von Datenhygiene-Arbeitsaufträgen
description: Erfahren Sie, wie Sie bestehende Datenhygiene-Arbeitsaufträge in der Benutzeroberfläche von Adobe Experience Platform anzeigen und verwalten können.
exl-id: 76d4a809-cc2c-434d-90b1-23d88f29c022
source-git-commit: f246a014de7869b627a677ac82e98d4556065010
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 100%

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

Wenn eine Datenhygiene-Anfrage an das System gesendet wird, wird ein Arbeitsauftrag erstellt, um die angeforderte Aufgabe auszuführen. Ein Arbeitsauftrag stellt einen spezifischen Datenhygiene-Prozess dar, z. B. das geplante Ablaufen eines Datensatzes, wobei sein aktueller Status und andere zugehörige Details enthalten sind.

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
| [!UICONTROL Status] | Filtern Sie nach dem aktuellen Status des Arbeitsauftrags:<ul><li>**[!UICONTROL Abgeschlossen]**: Der Vorgang ist abgeschlossen.</li><li>**[!UICONTROL Ausstehend]**: Der Vorgang wurde erstellt, aber noch nicht ausgeführt. Eine [Datensatz-Gültigkeitsanfrage](./dataset-expiration.md) nimmt diesen Status vor dem geplanten Löschdatum an. Zum Löschdatum ändert sich der Status auf [!UICONTROL Wird ausgeführt], sofern der Vorgang nicht zuvor bereits abgebrochen wurde.</li><li>**[!UICONTROL Wird ausgeführt]**: Die Datensatz-Gültigkeitsanfrage wurde gestartet und wird derzeit verarbeitet.</li><li>**[!UICONTROL Abgebrochen]**: Der Vorgang wurde im Rahmen einer manuellen Benutzeranfrage abgebrochen.</li></ul> |
| [!UICONTROL Erstellt am] | Filtern Sie nach dem Zeitpunkt, zu dem der Arbeitsauftrag erstellt wurde. |
| [!UICONTROL Ablaufdatum] | Filtern Sie Datensatz-Gültigkeitsanfragen nach dem geplanten Löschdatum für den jeweiligen Datensatz. |
| [!UICONTROL Aktualisierungsdatum] | Filtern Sie Datensatz-Gültigkeitsanfragen nach dem Zeitpunkt, zu dem der Arbeitsauftrag zuletzt aktualisiert wurde. Erstellungen und Abläufe werden als Aktualisierungen gezählt. |

{style=&quot;table-layout:auto&quot;}

## Anzeigen der Details eines Arbeitsauftrags {#view-details}

>[!CONTEXTUALHELP]
>id="platform_hygiene_statusbyservice"
>title="Status nach Service"
>abstract="Anfragen zur Datenhygiene werden von mehreren Services von Experience Platform unabhängig voneinander bearbeitet. In diesem Abschnitt wird der aktuelle Verarbeitungsstatus der Anfrage für jeden einzelnen Service beschrieben. Weitere Informationen finden Sie im Handbuch zur Datenhygiene-Benutzeroberfläche."

>[!CONTEXTUALHELP]
>id="platform_hygiene_numberofidentities"
>title="Anzahl der Identitäten"
>abstract="Die Anzahl der Identitäten, die im Rahmen dieses Arbeitsauftrags gelöscht werden sollen. Die in der Zählung enthaltenen Identitäten müssen nicht unbedingt in den betroffenen Datensätzen vorhanden sein. Weitere Informationen finden Sie im Handbuch zur Datenhygiene-Benutzeroberfläche."

>[!CONTEXTUALHELP]
>id="platform_hygiene_responsemessages"
>title="Antwort auf die Löschung von Privatkunden"
>abstract="Wenn ein Privatkunden-Löschvorgang eine Antwort vom System erhält, werden diese Meldungen unter dem Abschnitt **[!UICONTROL Ergebnis]** angezeigt. Wenn während der Bearbeitung eines Arbeitsauftrags ein Problem auftritt, werden alle relevanten Fehlermeldungen in diesem Abschnitt angezeigt, um Ihnen bei der Fehlersuche zu helfen. Weitere Informationen finden Sie im Handbuch zur Datenhygiene-Benutzeroberfläche."

Wählen Sie die ID eines aufgelisteten Arbeitsauftrags aus, um dessen Details anzuzeigen.

![Bild, das die ausgewählte Arbeitsauftrags-ID anzeigt](../images/ui/browse/select-work-order.png)

<!-- Depending on the type of work order selected, different information and controls are provided. These are covered in the sections below.

### Consumer delete details {#consumer-delete}

The details of a consumer delete request are read-only, displaying its basic attributes such as its current status and the time elapsed since the request was made.

![Image showing the details page for a consumer delete work order](../images/ui/browse/consumer-delete-details.png)

### Dataset expiration details {#dataset-expiration} -->

Die Detailseite für eine Datensatz-Gültigkeit enthält Informationen zu Standardattributen, einschließlich des geplanten Ablaufdatums und der vor der Löschung verbleibenden Tage. In der rechten Leiste können Sie Steuerelemente verwenden, um die Gültigkeit zu bearbeiten oder abzubrechen.

![Das Bild zeigt die Detailseite für einen Arbeitsauftrag zur Gültigkeit eines Datensatzes](../images/ui/browse/ttl-details.png)

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie vorhandene Datenhygiene-Arbeitsaufträge in der Platform-Benutzeroberfläche anzeigen und verwalten können. Informationen zum Erstellen eigener Arbeitsaufträge finden Sie im Handbuch zum [Planen der Gültigkeit eines Datensatzes](./dataset-expiration.md).
