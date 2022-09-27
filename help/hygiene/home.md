---
title: Data Hygiene - Übersicht
description: Mit der Datenhygiene von Adobe Experience Platform können Sie den Lebenszyklus Ihrer Daten verwalten, indem Sie veraltete oder falsche Datensätze aktualisieren oder bereinigen.
exl-id: 104a2bb8-3242-4a20-b98d-ad6df8071a16
source-git-commit: 51181dccbd37df60e438f34090ebaeb9e327c4ce
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 26%

---

# Datenhygiene in Adobe Experience Platform

Adobe Experience Platform bietet leistungsstarke Tools zur Verwaltung großer, komplizierter Datenvorgänge, was die Orchestrierung von Customer Experiences ermöglicht. Da im Laufe der Zeit Daten in das System aufgenommen werden, ist es wichtig, Ihre Datenspeicher so zu verwalten, dass Daten wie vorgesehen verwendet werden. So müssen Daten aktualisiert werden, um falsche Einträge zu korrigieren, und Daten gelöscht werden, wenn dies aufgrund von Unternehmensrichtlinien erforderlich ist.

Mit den Datenhygiene-Funktionen von Platform können Sie Ihre gespeicherten Verbraucherdaten wie folgt verwalten:

* Planen automatisierter Datensatzabläufe
* Löschen von Verbraucherdaten basierend auf aufgenommenen Identitäten

>[!NOTE]
>
>Löschanfragen von Verbrauchern stehen nur Organisationen zur Verfügung, die Adobe Healthcare Shield oder Privacy Shield erworben haben.

Diese Aktivitäten können mithilfe der Variablen [[!UICONTROL Datenhygiene] UI-Arbeitsbereich](#ui) oder [Data Hygiene API](#api). Wenn ein Datenhygienefunktion ausgeführt wird, stellt das System bei jedem Prozessschritt Aktualisierungen der Transparenz bereit. Siehe Abschnitt zu [Fristen und Transparenz](#timelines-and-transparency) für weitere Informationen darüber, wie die einzelnen Auftragstypen im System dargestellt werden.

## Arbeitsbereich [!UICONTROL Datenhygiene] in der Benutzeroberfläche {#ui}

Der Arbeitsbereich [!UICONTROL Datenhygiene] in der Platform-Benutzeroberfläche ermöglicht es Ihnen, Datenhygienevorgänge zu konfigurieren und zu planen, um sicherzustellen, dass Ihre Datensätze wie vorgesehen gepflegt werden.

Ausführliche Anleitungen zum Verwalten von Datenhygiene-Aufgaben in der Benutzeroberfläche finden Sie im [Handbuch zur Datenhygiene-Benutzeroberfläche](./ui/overview.md).

## Data Hygiene API {#api}

Die [!UICONTROL Datenhygiene]-Benutzeroberfläche basiert auf der Data Hygiene API, deren Endpunkte Sie direkt zur Automatisierung Ihrer Datenhygiene-Aktivitäten verwenden können. Weitere Informationen dazu finden Sie im [Handbuch zur Data Hygiene API](./api/overview.md).

## Fristen und Transparenz

Löschanfragen für Verbraucher und Ablaufanfragen für Datensätze verfügen jeweils über eigene Verarbeitungszeitpläne und stellen Transparenzaktualisierungen an zentralen Punkten in ihren jeweiligen Workflows bereit. Weitere Informationen zu den einzelnen Auftragstypen finden Sie in den folgenden Abschnitten.

### Datensatzgültigkeiten {#dataset-expiration-transparency}

Folgendes geschieht, wenn ein [Datensatzablaufanfrage](./ui/dataset-expiration.md) wird erstellt:

| Staging | Zeit nach geplantem Ablauf | Beschreibung |
| --- | --- | --- |
| Anfrage wird gesendet | 0 Stunden | Ein Data Steward oder Datenschutzanalyst sendet eine Anfrage, wonach ein Datensatz zu einem bestimmten Zeitpunkt ablaufen soll. Die Anforderung wird im [!UICONTROL Data Hygiene UI] nachdem sie gesendet wurde und sich bis zur geplanten Ablaufzeit im Status &quot;Ausstehend&quot;befindet, nach der die Anfrage ausgeführt wird. |
| Datensatz wird entfernt | 1 Stunde | Der Datensatz wird aus dem [Datensatzinventarseite](../catalog/datasets/user-guide.md) in der Benutzeroberfläche. Die Daten im Data Lake werden nur weich gelöscht und bleiben so bis zum Ende des Prozesses erhalten, nach dem sie schwer gelöscht werden. |
| Profilanzahl aktualisiert | 30 Stunden | Die durch den Ablauf des Datensatzes verursachte Änderung der Profilzahlen wird in [Dashboard-Widgets](../dashboards/guides/profiles.md#profile-count-trend) und anderen Berichten. |
| Segmente aktualisiert | 48 Stunden | Nachdem Profile entfernt wurden, werden alle zugehörigen [Segmente](../segmentation/home.md) aktualisiert werden, um ihre neue Größe widerzuspiegeln. |
| Journey und Ziele aktualisiert | 50 Stunden | [Journey](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [Kampagnen](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html)und [Ziele](../destinations/home.md) werden entsprechend den Änderungen in verwandten Segmenten aktualisiert. |
| Abschließen der Hard-Löschung | 14 Tage | Alle Daten, die sich auf den Datensatz beziehen, werden aus dem Data Lake schwer gelöscht. Die [Status des Hygieneauftrags](./ui/browse.md#view-details) , wodurch der Datensatz gelöscht wurde, aktualisiert wird, um dies widerzuspiegeln. |

{style=&quot;table-layout:auto&quot;}

### Löschen durch Verbraucher {#consumer-delete-transparency}

Folgendes geschieht, wenn ein [Löschanfrage für Verbraucher](./ui/delete-consumer.md) wird erstellt:

| Staging | Zeit nach der Anforderungsübermittlung | Beschreibung |
| --- | --- | --- |
| Anfrage wird gesendet | 0 Stunden | Ein Data Steward oder Datenschutzanalyst sendet eine Löschanfrage an Verbraucher. Die Anforderung wird im [!UICONTROL Data Hygiene UI] nach der Übermittlung. |
| Profilsuche aktualisiert | 3 Stunden | Die durch die gelöschte Identität verursachte Änderung der Profilanzahl wird in [Dashboard-Widgets](../dashboards/guides/profiles.md#profile-count-trend) und anderen Berichten. |
| Segmente aktualisiert | 24 Stunden | Nachdem Profile entfernt wurden, werden alle zugehörigen [Segmente](../segmentation/home.md) aktualisiert werden, um ihre neue Größe widerzuspiegeln. |
| Journey und Ziele aktualisiert | 26 Stunden | [Journey](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [Kampagnen](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html)und [Ziele](../destinations/home.md) werden entsprechend den Änderungen in verwandten Segmenten aktualisiert. |
| Leere Datensätze gelöscht im Data Lake | 7 Tage | Die Daten werden weich aus dem Data Lake gelöscht. |
| Datenaktualisierung abgeschlossen | 14 Tage | Die [Status des Hygieneauftrags](./ui/browse.md#view-details) Aktualisierungen, die anzeigen, dass der Auftrag abgeschlossen wurde, d. h., dass die Datenlöschung am Data Lake abgeschlossen und die relevanten Datensätze schwer gelöscht wurden. |

{style=&quot;table-layout:auto&quot;}

## Nächste Schritte

In diesem Dokument erhalten Sie einen Überblick über die Datenhygiene-Funktionen von Platform. Informationen zu den ersten Schritten bei Datenhygiene-Anfragen in der Benutzeroberfläche finden Sie im Abschnitt [UI-Handbuch](./ui/overview.md). Informationen zum programmgesteuerten Erstellen von Datenhygiene-Aufträgen finden Sie im Abschnitt [Data Hygiene API-Handbuch](./api/overview.md)
