---
keywords: Experience Platform;Startseite;beliebte Themen;Datumsbereich
title: Standardmäßige Warnhinweisregeln
description: In diesem Dokument werden die von Experience Platform bereitgestellten vordefinierten Warnhinweisregeln behandelt.
feature: Alerts
exl-id: b4af1c15-b1bc-4e4b-a447-09cc17a63988
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '922'
ht-degree: 82%

---

# Standardmäßige Warnhinweisregeln

Adobe Experience Platform bietet mehrere vordefinierte Warnhinweisregeln, die Sie für Ihr Unternehmen aktivieren können. In diesem Dokument werden die Einzelheiten dieser von Adobe bereitgestellten Warnhinweisregeln behandelt. Allgemeine Informationen zu Warnhinweisen in Experience Platform finden Sie in der [Übersicht zu Warnhinweisen](./overview.md).

Wenn Sie [Warnhinweisregeln in der Platform-Benutzeroberfläche anzeigen](./ui.md), können Sie jede Regel einzeln abonnieren. Beim Abonnieren von Warnhinweisen über [E/A-Ereignisbenachrichtigungen](./subscribe.md) sind Warnhinweisregeln jedoch in verschiedene Abonnementpakete unterteilt. In den unten stehenden Tabellen wird jede Regel mit dem zugehörigen E/A-Ereignis-Abonnementnamen angezeigt.

## Datenaufnahme

Die folgenden Warnhinweisregeln sind spezifisch für [Datenerfassung](../../ingestion/home.md) und [Quellen](../../sources/home.md):

| E/A-Ereignis-Abonnement | Warnhinweisregel | Beschreibung |
| --- | --- | --- |
| Informationen zur Ausführung des Quellflusses | Anfang der Ausführung eines Quellflusses | Dieser Warnhinweis wird ausgelöst, wenn eine Quellverbindung mit der Verarbeitung von Daten beginnt. |
| Informationen zur Ausführung des Quellflusses | Erfolgreiche Ausführung des Quellflusses | Dieser Warnhinweis wird ausgelöst, wenn Daten erfolgreich aus einer Quellverbindung aufgenommen werden. |
| Verzögerungen, Ausfälle und Fehler bei der Ausführung des Quellflusses | Fehler beim Ausführen des Quellflusses | Dieser Warnhinweis wird ausgelöst, wenn bei der Aufnahme von Daten aus einer Quellverbindung ein Fehler auftritt. |
| Verzögerungen, Ausfälle und Fehler bei der Ausführung des Quellflusses | Aufnahmeverzögerung | Dieser Warnhinweis wird ausgelöst, wenn die Verarbeitung eines Batch-Erfassungsablaufs länger als 150 Minuten dauert. |
| Verzögerungen, Ausfälle und Fehler bei der Ausführung des Quellflusses | Aufnahmefehler | Dieser Warnhinweis wird Trigger, wenn das Verhältnis der fehlgeschlagenen Datensätze zu allen Datensätzen einen Schwellenwert von 0,5 % überschreitet. |

{style=&quot;table-layout:auto&quot;}

Wenn Sie zuvor den folgenden Warnhinweistyp abonniert haben, erhalten Sie keine Warnhinweise mehr, da dieser Warnhinweis veraltet ist:

| E/A-Ereignis-Abonnement | Warnhinweisregel | Beschreibung |
| --- | --- | --- |
| Verzögerungen, Ausfälle und Fehler bei der Ausführung des Quellflusses | Fehlende Aufnahme | Dieser Warnhinweis sendet Ihnen eine Nachricht, wenn die Aufnahme um mehr als sieben Stunden verzögert ist und keine Daten an Platform erfasst werden. |

{style=&quot;table-layout:auto&quot;}

## Identity Service

Die folgenden Warnhinweisregeln sind spezifisch für [Identity Service](../../identity-service/home.md):

| E/A-Ereignis-Abonnement | Warnhinweisregel | Beschreibung |
| --- | --- | --- |
| Informationen zur Identitätsaufnahme | Anfang der Ausführung eines Identity Service-Flusses | Dieser Warnhinweis wird ausgelöst, wenn ein Identity Service-Fluss mit der Verarbeitung von Daten beginnt. Anders ausgedrückt werden erfasste Daten vom Data Lake in den Identity Service geladen. |
| Informationen zur Identitätsaufnahme | Erfolgreiche Ausführung des Identity Service-Flusses | Dieser Warnhinweis wird ausgelöst, wenn Daten erfolgreich aus dem Data Lake in den Identity Service geladen werden. |
| Verzögerungen, Fehler und Fehler bei der Identitätsaufnahme | Verzögerung bei der Ausführung des Identity Service-Flusses | Dieser Warnhinweis wird ausgelöst, wenn die Ausführung eines Identity Service-Flusses länger als 150 Minuten dauert. |
| Verzögerungen, Fehler und Fehler bei der Identitätsaufnahme | Fehler beim Ausführen des Identity Service-Flusses | Dieser Warnhinweis wird ausgelöst, wenn bei der Aufnahme von Daten in Identity Service ein Fehler auftritt. |

{style=&quot;table-layout:auto&quot;}

## Echtzeit-Kundenprofil

Die folgenden Warnhinweisregeln sind spezifisch für [Echtzeit-Kundenprofil](../../profile/home.md):

| E/A-Ereignis-Abonnement | Warnhinweisregel | Beschreibung |
| --- | --- | --- |
| Informationen zur Profilaufnahme | Anfang der Ausführung eines Profilflusses | Dieser Warnhinweis wird ausgelöst, wenn mit der Verarbeitung von Daten durch einen Profilfluss begonnen wird. |
| Informationen zur Profilaufnahme | Erfolgreiche Ausführung des Profilflusses | Dieser Warnhinweis wird ausgelöst, wenn Daten erfolgreich aus dem Data Lake in das Profil geladen wurden. |
| Verzögerungen, Ausfälle und Fehler bei der Profilaufnahme | Verzögerung bei der Ausführung eines Profilflusses | Dieser Warnhinweis wird ausgelöst, wenn das Laden von Daten aus dem Data Lake in das Profil länger als 150 Minuten dauert. |
| Verzögerungen, Ausfälle und Fehler bei der Profilaufnahme | Fehler beim Ausführen des Profilflusses | Dieser Warnhinweis wird ausgelöst, wenn bei der Aufnahme von Daten in das Profil ein Fehler auftritt. |

{style=&quot;table-layout:auto&quot;}

## Segmentierung

Die folgenden Warnhinweisregeln sind spezifisch für den [Segmentierungs-Service](../../segmentation/home.md):

| E/A-Ereignis-Abonnement | Warnhinweisregel | Beschreibung |
| --- | --- | --- |
| Informationen zu Segmentauswertungsavorgängen | Start des Segmentvorgangs | Dieser Warnhinweis wird ausgelöst, wenn ein Vorgang zur Segmentauswertung mit der Verarbeitung von Daten beginnt. |
| Informationen zu Segmentauswertungsavorgängen | Erfolgreicher Vorgang zur Segmentauswertung | Dieser Warnhinweis wird ausgelöst, wenn ein Vorgang zur Segmentauswertung erfolgreich abgeschlossen wurde. |
| Verzögerungen, Fehler und Fehler bei Vorgängen zur Segmentauswertung | Verzögerung bei Segmentvorgängen | Dieser Warnhinweis wird ausgelöst, wenn ein Vorgang zur Segmentauswertung länger als 150 Minuten dauert. |
| Verzögerungen, Fehler und Fehler bei Vorgängen zur Segmentauswertung | Fehler beim Segmentvorgang | Dieser Warnhinweis wird ausgelöst, wenn ein Vorgang zur Segmentauswertung zu einem Fehler führt. |
| Verzögerungen, Fehler und Fehler bei Vorgängen zur Segmentauswertung | Segmentdefinition deaktiviert | Dieser Warnhinweis wird ausgelöst, wenn eine Segmentdefinition aufgrund eines internen Fehlers deaktiviert ist. Dadurch wird automatisch ein Fehlerbericht für ein Adobe-Entwicklungsteam ausgelöst, um das Problem zu untersuchen. Dieser Warnhinweis dient nur zur Information und erfordert keine Aktion von Ihnen. |

{style=&quot;table-layout:auto&quot;}

## Ziele

Die folgenden Warnhinweisregeln sind spezifisch für [Ziele](../../destinations/home.md):

| E/A-Ereignis-Abonnement | Warnhinweisregel | Beschreibung |
| --- | --- | --- |
| Informationen zur Ausführung des Zielflusses | Start der Ausführung des Zielflusses | Dieser Warnhinweis wird ausgelöst, wenn ein Zielfluss mit der Aktivierung eines Segments beginnt. |
| Informationen zur Ausführung des Zielflusses | Erfolgreiche Ausführung des Zielflusses | Dieser Warnhinweis wird ausgelöst, wenn ein Segment erfolgreich für ein Ziel aktiviert wurde. |
| Verzögerungen, Ausfälle und Fehler bei der Ausführung des Zielflusses | Verzögerung bei der Ausführung des Zielflusses | Dieser Warnhinweis wird ausgelöst, wenn die Aktivierung eines Segments durch einen Zielfluss länger als 150 Minuten in Anspruch nimmt. |
| Verzögerungen, Ausfälle und Fehler bei der Ausführung des Zielflusses | Fehler beim Ausführen des Zielflusses | Dieser Warnhinweis wird ausgelöst, wenn beim Aktivieren eines Segments für ein Ziel ein Fehler auftritt. |
| Verzögerungen, Ausfälle und Fehler bei der Ausführung des Zielflusses | Überspringrate überschreitet Schwellenwert | Dieser Warnhinweis wird Trigger, wenn das Verhältnis zwischen übersprungenen IDs und Gesamt-IDs einen Schwellenwert überschreitet. |

{style=&quot;table-layout:auto&quot;}

## Query Service

Die folgenden Warnhinweisregeln sind spezifisch für [Query Service](../../query-service/home.md):

| E/A-Ereignis-Abonnement | Warnhinweisregel | Beschreibung |
| --- | --- | --- |
| Geplante Abfrageinformationen für Query Service | Geplanter Abfragestart von Query Service | Dieser Warnhinweis wird beim Start einer geplanten Abfrage Trigger. |
| Geplante Abfrageinformationen für Query Service | Geplanter Abfrageerfolg für Query Service | Dieser Warnhinweis wird Trigger, wenn ein geplanter Abfrageauftrag erfolgreich abgeschlossen wurde. |
| Geplante Abfrageverzögerungen, Fehler und Fehler in Query Service | Geplanter Abfragefehler des Abfragedienstes | Dieser Warnhinweis wird Trigger, wenn ein geplanter Abfrageauftrag fehlschlägt. |

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
