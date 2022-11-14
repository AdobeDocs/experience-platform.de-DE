---
title: Übersicht über die Datenhygiene
description: Mit der Datenhygiene von Adobe Experience Platform können Sie den Lebenszyklus Ihrer Daten verwalten, indem Sie veraltete oder falsche Datensätze aktualisieren oder bereinigen.
exl-id: 104a2bb8-3242-4a20-b98d-ad6df8071a16
source-git-commit: b76e1bc6d5b346c32ea09612e24b68c6636f7deb
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 84%

---

# Datenhygiene in Adobe Experience Platform

>[!IMPORTANT]
>
>Datenhygiene ist derzeit nur für Organisationen verfügbar, die **Adobe Gesundheitsschild** oder **Adobe Privacy &amp; Security Shield**.

Adobe Experience Platform bietet leistungsstarke Tools zur Verwaltung großer, komplizierter Datenvorgänge, was die Orchestrierung von Customer Experiences ermöglicht. Da im Laufe der Zeit Daten in das System aufgenommen werden, ist es wichtig, Ihre Datenspeicher so zu verwalten, dass Daten wie vorgesehen verwendet werden. So müssen Daten aktualisiert werden, um falsche Einträge zu korrigieren, und Daten gelöscht werden, wenn dies aufgrund von Unternehmensrichtlinien erforderlich ist.

Mit den Datenhygiene-Funktionen von Platform können Sie Ihre gespeicherten Daten von Privatkunden wie folgt verwalten:

* Planen automatisierter Datensatzgültigkeiten
* Löschen von Privatkundendaten basierend auf aufgenommenen Identitäten

Diese Aktivitäten können mithilfe des Arbeitsbereichs [[!UICONTROL Datenhygiene] in der Benutzeroberfläche](#ui) oder der [Datenhygiene-API](#api) durchgeführt werden Wenn ein Datenhygienevorgang ausgeführt wird, stellt das System bei jedem Prozessschritt Aktualisierungen der Transparenz bereit. Weitere Informationen darüber, wie die einzelnen Vorgangstypen im System dargestellt werden, finden Sie im Abschnitt zu [Timelines und Transparenz](#timelines-and-transparency).

## Arbeitsbereich [!UICONTROL Datenhygiene] in der Benutzeroberfläche {#ui}

Der Arbeitsbereich [!UICONTROL Datenhygiene] in der Platform-Benutzeroberfläche ermöglicht es Ihnen, Datenhygienevorgänge zu konfigurieren und zu planen, um sicherzustellen, dass Ihre Datensätze wie vorgesehen gepflegt werden.

Ausführliche Anleitungen zum Verwalten von Datenhygiene-Aufgaben in der Benutzeroberfläche finden Sie im [Handbuch zur Datenhygiene-Benutzeroberfläche](./ui/overview.md).

## Data Hygiene API {#api}

Die [!UICONTROL Datenhygiene]-Benutzeroberfläche basiert auf der Data Hygiene API, deren Endpunkte Sie direkt zur Automatisierung Ihrer Datenhygiene-Aktivitäten verwenden können. Weitere Informationen dazu finden Sie im [Handbuch zur Data Hygiene API](./api/overview.md).

## Timelines und Transparenz

Privatkunden-Löschvorgänge und Datensatz-Gültigkeitsanfragen weisen jeweils eigene Timelines für die Verarbeitung auf und stellen an wichtigen Punkten in ihren jeweiligen Workflows Transparenzaktualisierungen bereit. Details der einzelnen Auftragstypen finden Sie in den folgenden Abschnitten.

### Datensatzgültigkeiten {#dataset-expiration-transparency}

[Datensatzgültigkeitsanfrage](./ui/dataset-expiration.md) wird erstellt:

| Staging | Zeit nach planmäßiger Gültigkeit | Beschreibung |
| --- | --- | --- |
| Anfrage wird übermittelt | 0 Stunden | Ein Data Steward oder Datenschutzanalyst übermittelt eine Anfrage, dass ein Datensatz zu einem bestimmten Zeitpunkt ungültig werden soll. Nachdem sie übermittelt wurde, ist die Anfrage in der [!UICONTROL Datenhygiene-Benutzeroberfläche] sichtbar und verbleibt bis zum Ablauf der planmäßigen Gültigkeitsdauer im Status „Ausstehend“, wonach die Anfrage ausgeführt wird. |
| Datensatz wird gelöscht | 1 Stunde | Der Datensatz wird aus der [Datensatzinventarseite](../catalog/datasets/user-guide.md) in der Benutzeroberfläche gelöscht. Die Daten im Data Lake werden nur vorläufig gelöscht und bleiben so bis zum Ende des Prozesses erhalten, wonach sie dauerhaft gelöscht werden. |
| Anzahl der Profile wird aktualisiert | 30 Stunden | Je nach Inhalt des zu löschenden Datensatzes können einige Profile aus dem System entfernt werden, wenn alle zugehörigen Komponentenattribute mit diesem Datensatz verknüpft sind. 30 Stunden nach dem Löschen des Datensatzes werden alle resultierenden Änderungen der Gesamtprofilanzahl in [Dashboard-Widgets](../dashboards/guides/profiles.md#profile-count-trend) und anderen Berichten. |
| Segmente werden aktualisiert | 48 Stunden | Sobald alle betroffenen Profile aktualisiert wurden, werden alle zugehörigen [Segmente](../segmentation/home.md) aktualisiert werden, um ihre neue Größe widerzuspiegeln. Je nach entferntem Datensatz und den Attributen, nach denen Sie segmentieren, kann die Größe jedes Segments infolge des Löschens zunehmen oder verringern. |
| Journeys und Ziele werden aktualisiert | 50 Stunden | [Journeys](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html?lang=de), [Kampagnen](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html?lang=de) und [Ziele](../destinations/home.md) werden entsprechend den Änderungen in den zugehörigen Segmenten aktualisiert. |
| Dauerhafte Löschung wird abgeschlossen | 14 Tage | Alle Daten, die mit dem Datensatz in Zusammenhang stehen, werden dauerhaft aus dem Data Lake gelöscht. Der [Status des Hygienevorgangs](./ui/browse.md#view-details), durch den der Datensatz gelöscht wurde, wird aktualisiert, damit dies widergespiegelt wird. |

{style=&quot;table-layout:auto&quot;}

### Privatkunden-Löschvorgänge {#consumer-delete-transparency}

>[!IMPORTANT]
>
>Kundenlöschungen sind nur für Unternehmen verfügbar, die Adobe Healthcare Shield erworben haben.

[Privatkunden betreffende Löschanfrage](./ui/delete-consumer.md) wird erstellt:

| Staging | Zeit nach der Anfrageübermittlung | Beschreibung |
| --- | --- | --- |
| Anfrage wird übermittelt | 0 Stunden | Ein Data Steward oder Datenschutzanalyst übermittelt eine Privatkunden betreffende Löschanfrage. Die Anfrage ist in der [!UICONTROL Datenhygiene-Benutzeroberfläche] sichtbar |
| Profil-Lookups werden aktualisiert | 3 Stunden | Die durch die gelöschte Identität verursachte Änderung der Anzahl der Profile spiegelt sich in [Dashboard-Widgets](../dashboards/guides/profiles.md#profile-count-trend) und anderen Berichten wider. |
| Segmente werden aktualisiert | 24 Stunden | Wenn Profile entfernt worden sind, werden alle zugehörigen [Segmente](../segmentation/home.md) aktualisiert, damit ihre neue Größe widergespiegelt wird. |
| Journeys und Ziele werden aktualisiert | 26 Stunden | [Journeys](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [Kampagnen](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html) und [Ziele](../destinations/home.md) werden entsprechend den Änderungen in verwandten Segmenten aktualisiert. |
| Datensätze im Data Lake vorläufig gelöscht | 7 Tage | Die Daten werden vorläufig aus dem Data Lake gelöscht. |
| Datenbereinigung abgeschlossen | 14 Tage | Der [Status des Hygienevorgangs](./ui/browse.md#view-details) wird aktualisiert, damit angezeigt wird, dass der Vorgang abgeschlossen ist. Das bedeutet, dass die Datenbereinigung im Data Lake abgeschlossen ist und die entsprechenden Datensätze endgültig gelöscht wurden. |

{style=&quot;table-layout:auto&quot;}

## Nächste Schritte

In diesem Dokument erhalten Sie einen Überblick über die Datenhygiene-Funktionen von Platform. Informationen zu den ersten Schritten bei Datenhygiene-Anfragen in der Benutzeroberfläche finden Sie im [Handbuch zur Benutzeroberfläche](./ui/overview.md) Informationen zum programmgesteuerten Erstellen von Datenhygiene-Aufträgen finden Sie im [API-Handbuch zur Datenhygiene](./api/overview.md)
