---
keywords: Experience Platform;Startseite;beliebte Themen;Datumsbereich
title: Standardmäßige Warnhinweisregeln
description: In diesem Dokument werden die von Experience Platform bereitgestellten vordefinierten Warnhinweisregeln behandelt.
feature: Alerts
exl-id: b4af1c15-b1bc-4e4b-a447-09cc17a63988
source-git-commit: d82487f34c0879ed27ac55e42d70346f45806131
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 17%

---

# Standardmäßige Warnhinweisregeln

Adobe Experience Platform bietet mehrere vordefinierte Warnhinweisregeln, die Sie für Ihr Unternehmen aktivieren können. Die nachstehende Tabelle enthält die Einzelheiten dieser von der Adobe bereitgestellten Warnregeln. Allgemeine Informationen zu Warnhinweisen in Experience Platform finden Sie in der [Warnhinweise - Übersicht](./overview.md).

| Regel  | Beschreibung | Auswertungsfrequenz | Wiederholungsfenster |
| --- | --- | --- | --- |
| Erfolgreiche Ausführung des Quellenflusses | Dieser Warnhinweis wird Trigger, wenn Daten erfolgreich aus einer Quellverbindung erfasst werden. | K. A. | K. A. |
| Fehler beim Ausführen des Quellflusses | Dieser Warnhinweis wird Trigger, wenn bei der Aufnahme von Daten aus einer Quellverbindung ein Fehler auftritt. | K. A. | K. A. |
| Verzögerung bei Segmentaufträgen | Dieser Warnhinweis wird Trigger, wenn der Abschluss von Segmentaufträgen länger als 150 Minuten dauert. | 30 Sekunden | 3 Stunden |
| Segmentdefinition deaktiviert | Dieser Warnhinweis wird Trigger, wenn eine Segmentdefinition deaktiviert ist. | K. A. | K. A. |

{style=&quot;table-layout:auto&quot;}

<!-- (Definitions to be added once available)
| Entitlement Threshold Exceeded | This alert triggers when the number of created profiles exceeds 80% of your organization's entitlement. | 30 seconds | N/A |
| No ingestion activity in past 24 hours | This alert triggers when no new data has been ingested in the last 24-hour period. | 1 day | 1 day |
| SFTP source has not ingested data | This alert triggers when an [SFTP source](../../sources/connectors/cloud-storage/sftp.md) has not ingested any data within a certain time period. | 1 day | 1 day |
| Ingestion error rate exceeded | This alert triggers when the error rate for data ingestion exceeds 20%. | 30 seconds | 30 seconds |
| Feed Message | This alert when an identity sharing feed message has been sent to a user using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Access Revoked | This alert triggers when another Platform user revokes access to an identity sharing feed using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Modified | This alert triggers when an identity sharing feed is modified by a user using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Shared | This alert triggers when a user shares a new feed in [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Link Request | This alert triggers when a user requests to connect for partner sharing. | N/A | N/A |
| Link Action | This alert triggers when a user accepts a request to connect for partner sharing. | N/A | N/A |
-->
