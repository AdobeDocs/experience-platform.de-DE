---
keywords: Experience Platform;Startseite;beliebte Themen;Datumsbereich
title: Standardmäßige Warnhinweisregeln
description: In diesem Dokument werden die von Experience Platform bereitgestellten vordefinierten Warnhinweisregeln behandelt.
feature: Alerts
exl-id: b4af1c15-b1bc-4e4b-a447-09cc17a63988
source-git-commit: d8ada2de0ee0408e4e10f0dc45652af6eb6352cf
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 16%

---

# Standardmäßige Warnhinweisregeln

Adobe Experience Platform bietet mehrere vordefinierte Warnhinweisregeln, die Sie für Ihr Unternehmen aktivieren können. In diesem Dokument werden die Einzelheiten dieser von der Adobe bereitgestellten Warnregeln behandelt. Allgemeine Informationen zu Warnhinweisen in Experience Platform finden Sie in der [Übersicht zu Warnhinweisen](./overview.md).

Wann [Anzeigen von Warnregeln in der Platform-Benutzeroberfläche](./ui.md)können Sie jede Regel einzeln abonnieren. Beim Abonnieren von Warnhinweisen über [E/A-Ereignisbenachrichtigungen](./subscribe.md)Warnhinweisregeln sind jedoch in verschiedene Abonnementpakete unterteilt. In den unten stehenden Tabellen wird jede Regel mit dem zugehörigen E/A-Ereignis-Abonnementnamen angezeigt.

## Datenaufnahme

Die folgenden Warnhinweisregeln sind spezifisch für [Datenerfassung](../../ingestion/home.md) und  [sources](../../sources/home.md):

| E/A-Ereignis-Abonnement | Warnregel | Beschreibung |
| --- | --- | --- |
| Informationen zum Ablauf des Quellflusses | Start des Quellablaufs | Dieser Warnhinweis wird Trigger, wenn eine Quellverbindung mit der Verarbeitung von Daten beginnt. |
| Informationen zum Ablauf des Quellflusses | Erfolgreiche Ausführung des Quellflusses | Dieser Warnhinweis wird ausgelöst, wenn Daten erfolgreich aus einer Quellverbindung aufgenommen werden. |
| Verzögerungen, Fehler und Fehler bei der Ausführung des Quellflusses | Fehler beim Ausführen des Quellflusses | Dieser Warnhinweis wird ausgelöst, wenn bei der Aufnahme von Daten aus einer Quellverbindung ein Fehler auftritt. |
| Verzögerungen, Fehler und Fehler bei der Ausführung des Quellflusses | Aufnahmeverzögerung | Dieser Warnhinweis wird Trigger, wenn die Verarbeitung eines Batch-Erfassungsablaufs länger als 150 Minuten dauert. |

{style=&quot;table-layout:auto&quot;}

## Identity Service

Die folgenden Warnhinweisregeln sind spezifisch für [Identity Service](../../identity-service/home.md):

| E/A-Ereignis-Abonnement | Warnregel | Beschreibung |
| --- | --- | --- |
| Informationen zur Identitätsaufnahme | Start des ID-Dienstflusses | Dieser Warnhinweis wird Trigger, wenn ein Identity Service-Workflow mit der Verarbeitung von Daten beginnt. Anders ausgedrückt werden erfasste Daten vom Data Lake in den Identity Service geladen. |
| Informationen zur Identitätsaufnahme | Identity Service Flow Run Success | Dieser Warnhinweis wird Trigger, wenn Daten erfolgreich aus dem Data Lake in den Identity-Dienst geladen werden. |
| Verzögerungen, Fehler und Fehler bei der Identitätsaufnahme | Verzögerung bei der Ausführung des Identity Service | Dieser Warnhinweis wird Trigger, wenn die Verarbeitung eines Identity Service-Flusses länger als 150 Minuten dauert. |
| Verzögerungen, Fehler und Fehler bei der Identitätsaufnahme | Fehler beim Ausführen des Identity Service-Flusses | Dieser Warnhinweis wird Trigger, wenn bei der Aufnahme von Daten in Identity Service ein Fehler auftritt. |

{style=&quot;table-layout:auto&quot;}

## Echtzeit-Kundenprofil

Die folgenden Warnhinweisregeln sind spezifisch für [Echtzeit-Kundenprofil](../../profile/home.md):

| E/A-Ereignis-Abonnement | Warnregel | Beschreibung |
| --- | --- | --- |
| Informationen zur Profilaufnahme | Start des Profilflussablaufs | Dieser Warnhinweis wird Trigger, wenn mit der Verarbeitung von Daten durch einen Profilfluss begonnen wird. |
| Informationen zur Profilaufnahme | Profil-Fluss - Erfolg | Diese Warnung wird Trigger, wenn Daten erfolgreich aus dem Data Lake in das Profil geladen wurden. |
| Verzögerungen, Fehler und Fehler bei der Profilaufnahme | Verzögerung bei der Profilflussausführung | Die Verarbeitung dieser Warnung dauert länger als 150 Minuten, wenn Trigger Daten aus dem Data Lake in das Profil laden. |
| Verzögerungen, Fehler und Fehler bei der Profilaufnahme | Fehler beim Ausführen des Profilflusses | Dieser Warnhinweis wird Trigger, wenn bei der Aufnahme von Daten in das Profil ein Fehler auftritt. |

{style=&quot;table-layout:auto&quot;}

## Segmentierung

Die folgenden Warnhinweisregeln sind spezifisch für [Segmentierungsdienst](../../segmentation/home.md):

| E/A-Ereignis-Abonnement | Warnregel | Beschreibung |
| --- | --- | --- |
| Informationen zu Segmentauswertungsaufträgen | Start des Segmentauftrags | Dieser Warnhinweis wird Trigger, wenn ein Segmentbewertungsauftrag mit der Verarbeitung von Daten beginnt. |
| Informationen zu Segmentauswertungsaufträgen | Segmentauftragserfolg | Dieser Warnhinweis wird Trigger, wenn ein Segmentbewertungsauftrag erfolgreich abgeschlossen wurde. |
| Verzögerungen, Fehler und Fehler bei Segmentauswertungsaufträgen | Verzögerung bei Segmentaufträgen | Dieser Warnhinweis wird Trigger, wenn der Abschluss von Segmentbewertungsaufträgen länger als 150 Minuten dauert. |
| Verzögerungen, Fehler und Fehler bei Segmentauswertungsaufträgen | Segmentauftragsfehler | Dieser Warnhinweis wird Trigger, wenn ein Segmentbewertungsauftrag zu einem Fehler führt. |
| Verzögerungen, Fehler und Fehler bei Segmentauswertungsaufträgen | Segmentdefinition deaktiviert | Dieser Warnhinweis wird Trigger, wenn eine Segmentdefinition aufgrund eines internen Fehlers deaktiviert ist. Dadurch wird automatisch ein Kriegsraum für ein Adobe-Engineering-Team Trigger, um das Problem zu untersuchen. Dieser Warnhinweis ist nur informativ und erfordert keine Aktion von Ihnen. |

{style=&quot;table-layout:auto&quot;}

## Ziele

Die folgenden Warnhinweisregeln sind spezifisch für [Ziele](../../destinations/home.md):

| E/A-Ereignis-Abonnement | Warnregel | Beschreibung |
| --- | --- | --- |
| Informationen zum Zielflussablauf | Start des Zielflussablaufs | Dieser Warnhinweis wird Trigger, wenn ein Zielflussablauf mit der Aktivierung eines Segments beginnt. |
| Informationen zum Zielflussablauf | Erfolg des Zielflussablaufs | Dieser Warnhinweis wird Trigger, wenn ein Segment erfolgreich für ein Ziel aktiviert wurde. |
| Verzögerungen, Fehler und Fehler bei der Ausführung des Zielflusses | Verzögerung bei der Ausführung des Zielflusses | Dieser Warnhinweis wird Trigger, wenn die Aktivierung eines Segments länger als 150 Minuten in Anspruch nimmt. |
| Verzögerungen, Fehler und Fehler bei der Ausführung des Zielflusses | Fehler beim Zielflusslauf | Dieser Warnhinweis wird Trigger, wenn beim Aktivieren eines Segments für ein Ziel ein Fehler auftritt. |

{style=&quot;table-layout:auto&quot;}

<!-- (Definitions to be added once available)
| Segment Job Delay | This alert triggers when a segment job takes longer than 150 minutes to complete. | N/A | 30 seconds | 3 hours |
| No Ingestion Activity in Past 24 Hours | This alert triggers when no new data has been ingested in the last 24-hour period. | N/A | 1 day | 1 day |
| Ingestion Error Rate Exceeded | This alert triggers when the error rate for data ingestion exceeds the allotted threshold. | 20% | 30 seconds | 30 seconds |
| Entitlement Threshold Exceeded | This alert triggers when the number of created profiles exceeds 80% of your organization's entitlement. | 30 seconds | N/A |
| SFTP source has not ingested data | This alert triggers when an [SFTP source](../../sources/connectors/cloud-storage/sftp.md) has not ingested any data within a certain time period. | 1 day | 1 day |
| Feed Message | This alert when an identity sharing feed message has been sent to a user using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Access Revoked | This alert triggers when another Platform user revokes access to an identity sharing feed using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Modified | This alert triggers when an identity sharing feed is modified by a user using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Shared | This alert triggers when a user shares a new feed in [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Link Request | This alert triggers when a user requests to connect for partner sharing. | N/A | N/A |
| Link Action | This alert triggers when a user accepts a request to connect for partner sharing. | N/A | N/A |
-->
