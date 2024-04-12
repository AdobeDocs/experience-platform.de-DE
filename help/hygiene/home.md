---
title: Überblick über die erweiterte Lebenszyklusverwaltung
description: Mit der erweiterten Lebenszyklusverwaltung können Sie den Lebenszyklus Ihrer Daten verwalten, indem Sie veraltete oder ungenaue Datensätze aktualisieren oder bereinigen.
exl-id: 104a2bb8-3242-4a20-b98d-ad6df8071a16
source-git-commit: fc55e9a0849767d43c7f2a3bc3c540e776c8a072
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 58%

---

# Erweiterte Lebenszyklusverwaltung in Adobe Experience Platform

Adobe Experience Platform bietet leistungsstarke Tools zur Verwaltung großer, komplizierter Datenvorgänge, was die Orchestrierung von Customer Experiences ermöglicht. Da im Laufe der Zeit Daten in das System aufgenommen werden, ist es wichtig, Ihre Datenspeicher so zu verwalten, dass Daten wie vorgesehen verwendet werden. So müssen Daten aktualisiert werden, um falsche Einträge zu korrigieren, und Daten gelöscht werden, wenn dies aufgrund von Unternehmensrichtlinien erforderlich ist.

<!-- Platform's data lifecycle capabilities allow you to manage your stored data through the following:

* Scheduling automated dataset expirations
* Deleting individual records from one or all datasets

>[!IMPORTANT]
>
>Record deletes are meant to be used for data cleansing, removing anonymous data, or data minimization. They are **not** to be used for data subject rights requests (compliance) as pertaining to privacy regulations like the General Data Protection Regulation (GDPR). For all compliance use cases, use [Adobe Experience Platform Privacy Service](../privacy-service/home.md) instead. -->

Diese Aktivitäten können mithilfe der Variablen [[!UICONTROL Lebenszyklus der Daten] Benutzeroberfläche](#ui) oder [Data Hygiene API](#api). Wenn ein Datenlebenszyklusauftrag ausgeführt wird, stellt das System bei jedem Prozessschritt Transparenzaktualisierungen bereit. Weitere Informationen darüber, wie die einzelnen Vorgangstypen im System dargestellt werden, finden Sie im Abschnitt zu [Timelines und Transparenz](#timelines-and-transparency).

## [!UICONTROL Lebenszyklus der Daten] Benutzeroberfläche {#ui}

Die [!UICONTROL Lebenszyklus der Daten] Mit Workspace in der Platform-Benutzeroberfläche können Sie Datenlebenszyklusvorgänge konfigurieren und planen, um sicherzustellen, dass Ihre Datensätze erwartungsgemäß gepflegt werden.

Ausführliche Anweisungen zum Verwalten von Lebenszyklusaufgaben in der Benutzeroberfläche finden Sie in der [Handbuch zur Benutzeroberfläche für die Datenlebenszyklusbenutzeroberfläche](./ui/overview.md).

## Data Hygiene API {#api}

Die [!UICONTROL Lebenszyklus der Daten] Die Benutzeroberfläche basiert auf der Data Hygiene API, deren Endpunkte Sie direkt verwenden können, wenn Sie es vorziehen, Ihre Datenlebenszyklusaktivitäten zu automatisieren. Weitere Informationen dazu finden Sie im [Handbuch zur Data Hygiene API](./api/overview.md).

## Timelines und Transparenz

[Löschung von Datensätzen](./ui/record-delete.md) und Datensatzablaufanfragen verfügen jeweils über eigene Verarbeitungszeitpläne und stellen an den zentralen Punkten in ihren jeweiligen Workflows Transparenzaktualisierungen bereit.

<!-- ### Dataset expirations {#dataset-expiration-transparency} -->

[Datensatzgültigkeitsanfrage](./ui/dataset-expiration.md) wird erstellt:

| Staging | Zeit nach planmäßiger Gültigkeit | Beschreibung |
| --- | --- | --- |
| Anfrage wird übermittelt | 0 Stunden | Ein Data Steward oder Datenschutzanalyst übermittelt eine Anfrage, dass ein Datensatz zu einem bestimmten Zeitpunkt ungültig werden soll. Die Anforderung wird im [!UICONTROL Data Lifecycle-Benutzeroberfläche] nachdem sie gesendet wurde und sich bis zur geplanten Ablaufzeit im Status &quot;Ausstehend&quot;befindet, nach der die Anfrage ausgeführt wird. |
| Datensatz wird gelöscht | 1 Stunde | Der Datensatz wird aus der [Datensatzinventarseite](../catalog/datasets/user-guide.md) in der Benutzeroberfläche gelöscht. Die Daten im Data Lake werden nur vorläufig gelöscht und bleiben so bis zum Ende des Prozesses erhalten, wonach sie dauerhaft gelöscht werden. |
| Anzahl der Profile wird aktualisiert | 30 Stunden | Je nach Inhalt des zu löschenden Datensatzes können einige Profile aus dem System entfernt werden, wenn alle zugehörigen Komponentenattribute mit diesem Datensatz verknüpft sind. 30 Stunden nach dem Löschen des Datensatzes werden alle resultierenden Änderungen der Gesamtprofilanzahl in [Dashboard-Widgets](../dashboards/guides/profiles.md#profile-count-trend) und anderen Berichten widergespiegelt. |
| Zielgruppen aktualisiert | 48 Stunden | Sobald alle betroffenen Profile aktualisiert worden sind, werden alle zugehörigen [Zielgruppen](../segmentation/home.md) aktualisiert, damit ihre neue Größe widergespiegelt wird. Je nach entferntem Datensatz und den Attributen, nach denen Sie segmentieren, kann sich die Größe der einzelnen Zielgruppen infolge des Löschens vergrößern oder verkleinern. |
| Journeys und Ziele werden aktualisiert | 50 Stunden | [Journeys](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html?lang=de), [Kampagnen](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html?lang=de) und [Ziele](../destinations/home.md) werden entsprechend den Änderungen in den zugehörigen Segmenten aktualisiert. |
| Dauerhafte Löschung wird abgeschlossen | 15 Tage | Alle Daten, die mit dem Datensatz in Zusammenhang stehen, werden dauerhaft aus dem Data Lake gelöscht. Die [Status des Datenlebenszyklusauftrags](./ui/browse.md#view-details) wurde, wird der Datensatz entsprechend aktualisiert. |

{style="table-layout:auto"}

<!-- ### Record deletes {#record-delete-transparency}

The following takes place when a [record delete request](./ui/record-delete.md) is created:

| Stage | Time after request submission | Description |
| --- | --- | --- |
| Request is submitted | 0 hours | A data steward or privacy analyist submits a record delete request. The request is visible in the [!UICONTROL Data Lifecycle UI] after it has been submitted. |
| Profile lookups updated | 3 hours | The change in profile counts caused by the deleted identity are reflected in [dashboard widgets](../dashboards/guides/profiles.md#profile-count-trend) and other reports. |
| Segments updated | 24 hours | Once profiles are removed, all related [segments](../segmentation/home.md) are updated to reflect their new size. |
| Journeys and destinations updated | 26 hours | [Journeys](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [campaigns](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html), and [destinations](../destinations/home.md) are updated according to changes in related segments. |
| Records soft deleted in data lake | 7 days | The data is soft deleted from the data lake. |
| Data vacuuming completed | 14 days | The [status of the lifecycle job](./ui/browse.md#view-details) updates to indicate that the job has completed, meaning that data vacuuming has been completed on the data lake and the relevant records have been hard deleted. |

{style="table-layout:auto"} -->

## Nächste Schritte

Dieses Dokument bietet einen Überblick über die Funktionen von Platform für den Datenlebenszyklus. Informationen zu den ersten Schritten bei Datenhygiene-Anfragen in der Benutzeroberfläche finden Sie im [Handbuch zur Benutzeroberfläche](./ui/overview.md) Informationen zum programmgesteuerten Erstellen von Data Lifecycle-Aufträgen finden Sie im Abschnitt [Data Hygiene API-Handbuch](./api/overview.md)
