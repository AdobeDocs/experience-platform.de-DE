---
title: Durchsuchen von Arbeitshygiene-Aufträgen
description: Erfahren Sie, wie Sie bestehende Workflows zur Datenhygiene in der Benutzeroberfläche von Adobe Experience Platform anzeigen und verwalten.
exl-id: 76d4a809-cc2c-434d-90b1-23d88f29c022
hide: true
hidefromtoc: true
source-git-commit: c2e7cf1859f6a2b277783cdec535ecc208703fac
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 2%

---

# Arbeitserstellungen zur Datenhygiene durchsuchen

>[!CONTEXTUALHELP]
>id="platform_hygiene_workorders"
>title="IDs für Arbeitsaufträge"
>abstract="Wenn an das System eine Anforderung zur Datenhygiene gesendet wird, wird eine Arbeitsreihenfolge erstellt, um die angeforderte Aufgabe auszuführen. Mit anderen Worten, ein Arbeitsauftrag stellt einen spezifischen Datenhygiene-Prozess dar, der seinen aktuellen Status und andere zugehörige Details enthält. Bei der Erstellung wird jedem Arbeitsauftrag automatisch eine eigene eindeutige ID zugewiesen. Weitere Informationen finden Sie im Handbuch zur Benutzeroberfläche für Datenhygiene."

>[!IMPORTANT]
>
>Die Funktionen zur Datenhygiene in Adobe Experience Platform sind derzeit nur für Organisationen verfügbar, die Adobe Shield für das Gesundheitswesen erworben haben.

Wenn an das System eine Anforderung zur Datenhygiene gesendet wird, wird eine Arbeitsreihenfolge erstellt, um die angeforderte Aufgabe auszuführen. Ein Arbeitsauftrag stellt einen spezifischen Datenhygieneprozess dar (z. B. das Löschen von Verbraucherdaten), der den aktuellen Status und andere zugehörige Details enthält.

In diesem Handbuch wird beschrieben, wie Sie bestehende Arbeitsaufträge in der Adobe Experience Platform-Benutzeroberfläche anzeigen und verwalten.

## Auflisten und Filtern vorhandener Arbeitsaufträge

Wenn Sie zum ersten Mal auf **[!UICONTROL Datenhygiene]** Arbeitsbereich in der Benutzeroberfläche werden eine Liste der vorhandenen Arbeitsaufträge mit ihren grundlegenden Details angezeigt.

![Bild, das die [!UICONTROL Datenhygiene] Workspace in der Platform-Benutzeroberfläche](../images/ui/browse/work-order-list.png)

Die Liste zeigt nur Arbeitsaufträge für eine Kategorie an. Auswählen **[!UICONTROL Verbraucher]** eine Liste der Aufgaben zum Löschen von Verbrauchern anzuzeigen, und **[!UICONTROL Datensatz]** , um eine Liste der Time-to-Live (TTL)-Zeitpläne für Datensätze anzuzeigen.

![Bild, das die [!UICONTROL Datensatz] tab](../images/ui/browse/dataset-tab.png)

Wählen Sie das Trichtersymbol (![Bild des Trichtersymbols](../images/ui/browse/funnel-icon.png)), um eine Liste von Filtern für die angezeigten Arbeitsaufträge anzuzeigen.

![Bild der angezeigten Arbeitsreihenfilter](../images/ui/browse/filters.png)

Je nach angezeigtem Tab stehen unterschiedliche Filter zur Verfügung:

| Filter | Kategorie | Beschreibung |
| --- | --- | --- |
| [!UICONTROL Status] | [!UICONTROL Verbraucher] &amp; [!UICONTROL Datensatz] | Filtern Sie nach dem aktuellen Status der Arbeitsreihenfolge. |
| [!UICONTROL Erstellungsdatum] | [!UICONTROL Verbraucher] | Filtern Sie nach dem Zeitpunkt, zu dem der Verbraucher eine Löschanfrage gestellt hat. |
| [!UICONTROL Erstellungsdatum] | [!UICONTROL Datensatz] | Filtern Sie nach dem Zeitpunkt, zu dem der Verbraucher eine Löschanfrage gestellt hat. |
| [!UICONTROL Löschdatum] | [!UICONTROL Datensatz] | Filtern Sie nach dem Löschdatum, das die TTL geplant hat. |
| [!UICONTROL Datum aktualisiert] | [!UICONTROL Datensatz] | Filtern Sie nach dem Zeitpunkt, zu dem die TTL des Datensatzes zuletzt aktualisiert wurde. TTL-Erstellung und -Gültigkeit werden als Aktualisierungen gezählt. |

{style=&quot;table-layout:auto&quot;}

## Details eines Arbeitsauftrags anzeigen

Wählen Sie die ID einer aufgelisteten Arbeitsreihenfolge aus, um deren Details anzuzeigen.

![Bild, das die ausgewählte Workflow-Bestell-ID anzeigt](../images/ui/browse/select-work-order.png)

Je nach ausgewähltem Arbeitstyp werden unterschiedliche Informationen und Steuerelemente bereitgestellt. Diese werden in den folgenden Abschnitten behandelt.

### Details zum Löschen von Verbrauchern

<!-- (Not available for initial release)
>[!CONTEXTUALHELP]
>id="platform_hygiene_responsemessages"
>title="Consumer delete response"
>abstract="When a consumer deletion process receives a response from the system, these messages are displayed under the **[!UICONTROL Result]** section. If a problem occurs while a work order is processing, any relevant error messages will appear in this section to help you troubleshoot the issue. To learn more, see the data hygiene UI guide."
-->

Die Details einer Anfrage zum Löschen durch Verbraucher sind schreibgeschützt und zeigen die grundlegenden Attribute wie den aktuellen Status und die seit der Anforderung verstrichene Zeit an.

![Bild mit der Detailseite für einen Verbraucher, der einen Arbeitsauftrag zum Löschen ausgibt](../images/ui/browse/consumer-delete-details.png)

### TTL-Details zum Datensatz

Die Detailseite für einen Datensatz-TTL enthält Informationen zu seinen grundlegenden Attributen, einschließlich des geplanten Ablaufdatums für die Tage, die vor dem Löschen verbleiben. In der rechten Leiste können Sie Steuerelemente verwenden, um die TTL zu bearbeiten oder abzubrechen.

![Bild, das die Detailseite für eine TTL-Arbeitsreihenfolge des Datensatzes anzeigt](../images/ui/browse/ttl-details.png)

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie bestehende Workflows zur Datenhygiene in der Platform-Benutzeroberfläche anzeigen und verwalten. Informationen zum Erstellen eigener Arbeitsaufträge finden Sie in der folgenden Dokumentation:

* [Verbraucher löschen](./delete-consumer.md)
* [Datensatz-TTL planen](./ttl.md)
