---
title: Erweiterte Übersicht über die Verwaltung des Datenlebenszyklus
description: Mit dem erweiterten Daten-Lifecycle-Management können Sie den Lebenszyklus Ihrer Daten verwalten, indem Sie veraltete oder ungenaue Datensätze aktualisieren oder bereinigen.
exl-id: 104a2bb8-3242-4a20-b98d-ad6df8071a16
source-git-commit: fc71e61fd33fe216f8cd326b9df048958c07077a
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 32%

---

# Erweitertes Daten-Lifecycle-Management in Adobe Experience Platform

Adobe Experience Platform bietet leistungsstarke Tools zur Verwaltung großer, komplizierter Datenvorgänge, was die Orchestrierung von Customer Experiences ermöglicht. Da im Laufe der Zeit Daten in das System aufgenommen werden, ist es wichtig, Ihre Datenspeicher so zu verwalten, dass Daten wie vorgesehen verwendet werden. So müssen Daten aktualisiert werden, um falsche Einträge zu korrigieren, und Daten gelöscht werden, wenn dies aufgrund von Unternehmensrichtlinien erforderlich ist.

Diese Aktivitäten können mit dem Arbeitsbereich der [[!UICONTROL Data Lifecycle]-Benutzeroberfläche &#x200B;](#ui) der [Datenhygiene-API) &#x200B;](#api). Wenn ein Datenlebenszyklusauftrag ausgeführt wird, stellt das System bei jedem Prozessschritt Aktualisierungen der Transparenz bereit. Weitere Informationen darüber, wie die einzelnen Auftragstypen im System dargestellt werden, finden Sie im Abschnitt zu [Timelines und Transparenz](#timelines-and-transparency).

>[!NOTE]
>
>Advanced Data Lifecycle Management unterstützt das Löschen von Datensätzen über den [Datensatzgültigkeits-Endpunkt](./api/dataset-expiration.md) und ID-Löschungen (Daten auf Zeilenebene) mithilfe primärer Identitäten über den [Arbeitsauftrags-Endpunkt](./api/workorder.md). Sie können das Löschen von [Datensatzgültigkeiten](./ui/dataset-expiration.md) und [Datensätzen](./ui/record-delete.md) auch über die Experience Platform-Benutzeroberfläche verwalten. Weitere Informationen finden Sie in der verknüpften Dokumentation . Beachten Sie, dass der Datenlebenszyklus das Löschen von Batches nicht unterstützt.

## [!UICONTROL Data Lifecycle] Arbeitsbereich der Benutzeroberfläche {#ui}

Der [!UICONTROL Data Lifecycle] Arbeitsbereich in der Experience Platform-Benutzeroberfläche ermöglicht die Konfiguration und Planung von Datenlebenszyklusvorgängen, wodurch Sie sicherstellen können, dass Ihre Datensätze wie vorgesehen gepflegt werden.

Ausführliche Anweisungen zum Verwalten von Datenlebenszyklusaufgaben in der Benutzeroberfläche finden Sie im [Handbuch zur Datenlebenszyklus-Benutzeroberfläche](./ui/overview.md).

## Data Hygiene API {#api}

Die [!UICONTROL Data Lifecycle] Benutzeroberfläche basiert auf der Data Hygiene API, deren Endpunkte Sie direkt zur Automatisierung Ihrer Datenlebenszyklusaktivitäten verwenden können. Weitere Informationen dazu finden Sie im [Handbuch zur Data Hygiene API](./api/overview.md).

## Timelines und Transparenz {#timelines-and-transparency}

Anfragen zum [Löschen von Datensätzen](./ui/record-delete.md) und zur Datensatzgültigkeit haben jeweils ihre eigenen Verarbeitungszeitpläne und bieten Transparenzaktualisierungen an wichtigen Punkten in ihren jeweiligen Workflows.

>[!TIP]
>
>Informationen zur Überwachung der aktuellen Nutzung in Bezug auf Kontingentbeschränkungen finden Sie [&#x200B; „Kontingentreferenzhandbuch](./api/quota.md).\
>Berechtigungsregeln, monatliche Begrenzungen, SLA-Zeitleisten und Richtlinien zur Ausnahmebehandlung finden Sie in der Dokumentation [Löschen von Datensätzen (](./ui/record-delete.md#quotas)) und [Arbeitsauftrag (API)](./api/workorder.md#quotas).

[Datensatzgültigkeitsanfrage](./ui/dataset-expiration.md) wird erstellt:

| Staging | Zeit nach planmäßiger Gültigkeit | Beschreibung |
| --- | --- | --- |
| Anfrage wird übermittelt | 0 Stunden | Ein Data Steward oder Datenschutzanalyst übermittelt eine Anfrage, dass ein Datensatz zu einem bestimmten Zeitpunkt ablaufen soll. Nachdem sie übermittelt wurde, ist die Anfrage in der [!UICONTROL Data Lifecycle UI] sichtbar und verbleibt bis zum Ablauf der planmäßigen Gültigkeitsdauer im Status „Ausstehend“, wonach die Anfrage ausgeführt wird. |
| Datensatz wird aus dem Data Lake gelöscht | 1 Stunde | Der Datensatz wird aus der [Datensatzinventarseite](../catalog/datasets/user-guide.md) in der Benutzeroberfläche gelöscht. Die Daten im Data Lake werden nur vorläufig gelöscht und bleiben so bis zum Ende des Prozesses erhalten, wonach sie dauerhaft gelöscht werden. |
| Datensatz wird aus dem Profil-Service gelöscht | 3 Stunden | Ab diesem Zeitpunkt werden bei Vorgängen wie Batch- und Streaming-Segmentierung, Vorschau oder Schätzung, Export und Entitätszugriff keine Daten mehr aus diesem Datensatz gelesen. Die Daten im Profil-Service werden nur vorläufig gelöscht und bleiben so bis zum Ende des Prozesses erhalten, wonach sie dauerhaft gelöscht werden. |
| Profilanzahl und Zielgruppen aktualisiert | 48 Stunden | Sobald alle betroffenen Profile aktualisiert worden sind, werden alle zugehörigen [Zielgruppen](../segmentation/home.md) aktualisiert, damit ihre neue Größe widergespiegelt wird. Je nach entferntem Datensatz und den Attributen, nach denen Sie segmentieren, kann sich die Größe der einzelnen Zielgruppen aufgrund des Löschens erhöhen oder verringern. An dieser Stelle werden alle resultierenden Änderungen der Gesamtprofilanzahl in [Dashboard-Widgets](../dashboards/guides/profiles.md#profile-count-trend) und anderen Berichten widergespiegelt. |
| Journeys und Ziele werden aktualisiert | 50 Stunden | [Journeys](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html?lang=de), [Kampagnen](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html?lang=de) und [Ziele](../destinations/home.md) werden entsprechend den Änderungen in den zugehörigen Segmenten aktualisiert. |
| Dauerhafte Löschung wird abgeschlossen | 15 Tage | Alle mit dem Datensatz verknüpften Daten werden dauerhaft aus dem Data Lake und Profil-Service gelöscht. Der [Status des Datenlebenszyklusauftrags](./ui/browse.md#view-details) der den Datensatz gelöscht hat, wird aktualisiert, um dies widerzuspiegeln. |

{style="table-layout:auto"}

## Nächste Schritte

Dieses Dokument bietet einen Überblick über die Datenlebenszyklusfunktionen von Experience Platform. Informationen zu den ersten Schritten bei Datenhygiene-Anfragen in der Benutzeroberfläche finden Sie im [Handbuch zur Benutzeroberfläche](./ui/overview.md) Informationen zum programmgesteuerten Erstellen von Datenlebenszyklus-Aufträgen finden Sie im [Data Hygiene API-Handbuch](./api/overview.md)
