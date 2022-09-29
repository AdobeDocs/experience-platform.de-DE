---
title: Durchsuchen von Datenhygiene-Arbeitsaufträgen
description: Erfahren Sie, wie Sie bestehende Datenhygiene-Arbeitsaufträge in der Benutzeroberfläche von Adobe Experience Platform anzeigen und verwalten können.
exl-id: 76d4a809-cc2c-434d-90b1-23d88f29c022
source-git-commit: e4cc78591d0d3b4abd660956b1263092697d63d5
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 75%

---

# Durchsuchen von Datenhygiene-Arbeitsaufträgen {#browse-work-orders}

>[!CONTEXTUALHELP]
>id="platform_hygiene_workorders"
>title="IDs für Arbeitsaufträge"
>abstract="Wenn eine Datenhygiene-Anfrage an das System gesendet wird, wird ein Arbeitsauftrag erstellt, um die angeforderte Aufgabe auszuführen. Anders ausgedrückt, ist ein Arbeitsauftrag ein spezifischer Datenhygiene-Prozess, der seinen aktuellen Status und andere zugehörige Details enthält. Bei der Erstellung eines Arbeitsauftrags wird diesem automatisch eine eigene eindeutige ID zugewiesen."
>text="See the data hygiene UI guide to learn more."

>[!IMPORTANT]
>
>Die Funktionen zur Datenhygiene in Adobe Experience Platform stehen derzeit nur Organisationen zur Verfügung, die Adobe Healthcare Shield oder Privacy Shield erworben haben.

Wenn eine Datenhygiene-Anfrage an das System gesendet wird, wird ein Arbeitsauftrag erstellt, um die angeforderte Aufgabe auszuführen. Ein Arbeitsauftrag stellt einen spezifischen Datenhygiene-Prozess dar, z. B. das geplante Ablaufen eines Datensatzes, wobei sein aktueller Status und andere zugehörige Details enthalten sind.

In diesem Handbuch wird beschrieben, wie Sie bestehende Arbeitsaufträge in der Adobe Experience Platform-Benutzeroberfläche anzeigen und verwalten können.

## Auflisten und Filtern vorhandener Arbeitsaufträge

Wenn Sie zum ersten Mal auf den Arbeitsbereich **[!UICONTROL Datenhygiene]** in der Benutzeroberfläche zugreifen, wird eine Liste der vorhandenen Arbeitsaufträge mit allgemeinen Details angezeigt.

![Bild, das den Arbeitsbereich [!UICONTROL Datenhygiene] in der Platform-Benutzeroberfläche zeigt](../images/ui/browse/work-order-list.png)

In der Liste werden nur Arbeitsaufträge für jeweils eine Kategorie angezeigt. Auswählen **[!UICONTROL Verbraucher]** um eine Liste der Aufgaben zum Löschen für Verbraucher anzuzeigen, und **[!UICONTROL Datensatz]** , um eine Liste der geplanten Datensatzabläufe anzuzeigen.

![Bild, das die Registerkarte [!UICONTROL Datensatz] zeigt](../images/ui/browse/dataset-tab.png)

Wählen Sie das Trichtersymbol (![Bild des Trichtersymbols](../images/ui/browse/funnel-icon.png)) aus, um eine Liste von Filtern für die angezeigten Arbeitsaufträge aufzurufen.

![Bild der angezeigten Arbeitsauftragsfilter](../images/ui/browse/filters.png)

Je nach angezeigtem Arbeitstyp sind unterschiedliche Filteroptionen verfügbar.

### Filter für Löschen durch Verbraucher

Die folgenden Filter gelten für Löschanfragen von Verbrauchern:

| Filter | Beschreibung |
| --- | --- |
| [!UICONTROL Status] | Filtern Sie nach dem aktuellen Status des Arbeitsauftrags:<ul><li>**[!UICONTROL Abgeschlossen]**: Der Vorgang ist abgeschlossen.</li><li>**[!UICONTROL Fehlgeschlagen]**: Beim Auftrag ist ein Fehler aufgetreten und konnte nicht abgeschlossen werden.</li><li>**[!UICONTROL Verarbeitung]**: Die Anfrage wurde gestartet und wird derzeit verarbeitet.</li></ul> |
| [!UICONTROL Erstellt am] | Filtern Sie nach dem Zeitpunkt, zu dem der Arbeitsauftrag erstellt wurde. |
| [!UICONTROL Aktualisierungsdatum] | Filtern Sie nach dem Zeitpunkt, zu dem die Arbeitsreihenfolge zuletzt aktualisiert wurde. Kreationen werden als Aktualisierungen gezählt. |

### Filter für den Ablauf von Datensätzen

Die folgenden Filter gelten für Ablaufanfragen von Datensätzen:

| Filter | Beschreibung |
| --- | --- |
| [!UICONTROL Status] | Filtern Sie nach dem aktuellen Status des Arbeitsauftrags:<ul><li>**[!UICONTROL Abgeschlossen]**: Der Vorgang ist abgeschlossen.</li><li>**[!UICONTROL Ausstehend]**: Der Vorgang wurde erstellt, aber noch nicht ausgeführt. Eine [Datensatz-Gültigkeitsanfrage](./dataset-expiration.md) nimmt diesen Status vor dem geplanten Löschdatum an. Zum Löschdatum ändert sich der Status auf [!UICONTROL Wird ausgeführt], sofern der Vorgang nicht zuvor bereits abgebrochen wurde.</li><li>**[!UICONTROL Wird ausgeführt]**: Die Datensatz-Gültigkeitsanfrage wurde gestartet und wird derzeit verarbeitet.</li><li>**[!UICONTROL Abgebrochen]**: Der Vorgang wurde im Rahmen einer manuellen Benutzeranfrage abgebrochen.</li></ul> |
| [!UICONTROL Erstellt am] | Filtern Sie nach dem Zeitpunkt, zu dem der Arbeitsauftrag erstellt wurde. |
| [!UICONTROL Ablaufdatum] | Filtern Sie Datensatz-Gültigkeitsanfragen nach dem geplanten Löschdatum für den jeweiligen Datensatz. |
| [!UICONTROL Aktualisierungsdatum] | Filtern Sie nach dem Zeitpunkt, zu dem die Arbeitsreihenfolge zuletzt aktualisiert wurde. Erstellungen und Abläufe werden als Aktualisierungen gezählt. |

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
>abstract="Wenn ein Benutzer beim Löschen eine Antwort vom System erhält, werden diese Meldungen unter der **[!UICONTROL Ergebnis]** Abschnitt. Wenn während der Bearbeitung eines Arbeitsauftrags ein Problem auftritt, werden alle relevanten Fehlermeldungen in diesem Abschnitt angezeigt, um Ihnen bei der Fehlersuche zu helfen. Weitere Informationen finden Sie im Handbuch zur Datenhygiene-Benutzeroberfläche."

Wählen Sie die ID eines aufgelisteten Arbeitsauftrags aus, um dessen Details anzuzeigen.

![Bild, das die ausgewählte Arbeitsauftrags-ID anzeigt](../images/ui/browse/select-work-order.png)

Je nach ausgewähltem Typ des Arbeitsauftrags sind unterschiedliche Informationen und Steuerelemente verfügbar. Diese werden in den folgenden Abschnitten erläutert.

### Details zum Löschen von Verbrauchern {#consumer-delete}

Zu den Details einer Löschanfrage eines Verbrauchers gehören der aktuelle Status und die seit der Antragstellung verstrichene Zeit. Jede Anforderung enthält auch **[!UICONTROL Status nach Dienst]** -Abschnitt, der individuelle Statusdetails zu jedem am Löschen beteiligten nachgelagerten Dienst bereitstellt. In der rechten Leiste können Sie mithilfe von Steuerelementen den Namen und die Beschreibung der Arbeitsreihenfolge aktualisieren.

![Bild mit der Detailseite für einen Verbraucher-Löscharbeitsauftrag](../images/ui/browse/consumer-delete-details.png)

### Details zum Datensatzablauf {#dataset-expiration}

Die Detailseite für eine Datensatz-Gültigkeit enthält Informationen zu Standardattributen, einschließlich des geplanten Ablaufdatums und der vor der Löschung verbleibenden Tage. In der rechten Leiste können Sie Steuerelemente verwenden, um die Gültigkeit zu bearbeiten oder abzubrechen.

![Das Bild zeigt die Detailseite für einen Arbeitsauftrag zur Gültigkeit eines Datensatzes](../images/ui/browse/ttl-details.png)

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie vorhandene Datenhygiene-Arbeitsaufträge in der Platform-Benutzeroberfläche anzeigen und verwalten können. Informationen zum Erstellen eigener Arbeitsaufträge finden Sie in der folgenden Dokumentation:

* [Verwalten von Datensatzgültigkeiten](./dataset-expiration.md)
* [Löschen von Benutzern verwalten](./delete-consumer.md)
