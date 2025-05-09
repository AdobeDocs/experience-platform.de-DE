---
keywords: Experience Platform;Startseite;beliebte Themen;Datumsbereich
title: Warnhinweise – Übersicht
description: Erfahren Sie mehr über Warnhinweise in Adobe Experience Platform, einschließlich der Struktur der Definition von Warnhinweisregeln.
feature: Alerts
exl-id: c38a93c6-1618-4ef9-8f94-41c7ab4af43c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '804'
ht-degree: 69%

---

# Warnhinweise – Übersicht

>[!NOTE]
>
>Da Warnhinweise sowohl in Produktions- als auch in Entwicklungs-Sandboxes unterstützt werden, können Sie sie in jeder beliebigen Sandbox abonnieren. Wenn eine Sandbox zurückgesetzt wird, werden auch alle Abonnement-Warnhinweise zurückgesetzt. Wenn eine Sandbox gelöscht wird, werden alle Abonnement-Warnhinweise gelöscht.

Mit Adobe Experience Platform können Sie ereignisbasierte Warnhinweise zu Adobe Experience Platform-Aktivitäten abonnieren. Warnhinweise verringern oder beseitigen die Notwendigkeit, die [[!DNL Observability Insights] API](../api/overview.md) abzufragen, um zu überprüfen, ob ein Auftrag abgeschlossen wurde, ob ein bestimmter Meilenstein innerhalb eines Arbeitsablaufs erreicht wurde oder ob Fehler aufgetreten sind.

Wenn bestimmte Bedingungen in Ihren Experience Platform-Vorgängen erfüllt sind (z. B. ein potenzielles Problem, wenn das System einen Schwellenwert überschreitet), kann Experience Platform allen Benutzenden in Ihrem Unternehmen, die sich dafür angemeldet haben, Warnhinweise zusenden. Diese Nachrichten können sich über einen vordefinierten Zeitraum wiederholen, bis der Warnhinweis behoben wurde.

Dieses Dokument bietet eine Übersicht zu Warnhinweisen in Adobe Experience Platform, einschließlich der Struktur zum Definieren von Warnhinweisregeln.

## Einmalige Warnhinweise im Vergleich zu sich wiederholenden Warnhinweisen

Experience Platform-Warnhinweise können einmal gesendet werden oder in einem vordefinierten Intervall so lange wiederholt werden, bis sie aufgelöst werden. Die Anwendungsfälle dieser einzelnen Optionen sollen sich wie folgt unterscheiden:

| Einmaliger Warnhinweis | Sich wiederholender Warnhinweis |
| --- | --- |
| Zeigt nicht unbedingt ein Problem an. | Gibt einen potenziell unerwünschten Status an. |
| Wiederholt sich nicht. | Kann sich wiederholen, wenn die anormale Bedingung bestehen bleibt. |
| Zu den Beispielen gehören:<ul><li>Die Datenaufnahme wurde erfolgreich abgeschlossen.</li><li>Die Ausführung einer Abfrage wurde abgeschlossen.</li><li>Die Daten wurden gelöscht.</li></ul> | Zu den Beispielen gehören:<ul><li>Die Aufnahmedauer überschreitet den übersteigt das vereinbarte Service-Niveau (SLA).</li><li>Die tägliche Aufnahme erfolgte in den letzten 24 Stunden nicht.</li><li>Die Fehlerrate des Stream-Prozessors liegt über dem konfigurierten Schwellenwert.</li><li>Die Gesamtzahl der Profile übersteigt die zulässige Anzahl.</li></ul> |

{style="table-layout:auto"}

## Anatomie eines Warnhinweises

Ein Warnhinweis kann in die folgenden Komponenten unterteilt werden:

| Komponente | Beschreibung |
| --- | --- |
| **Metrik** | Eine Beobachtbarkeits-[Metrik](../api/metrics.md#available-metrics), deren Wert den Warnhinweis auslöst, z. B. die Anzahl fehlgeschlagener Batch-Erfassungsereignisse (`timeseries.ingestion.dataset.batchfailed.count`). |
| **Bedingung** | Eine Bedingung für die Metrik, die den Warnhinweis auslöst, wenn sie „true“ angibt, z. B. eine Zählmetrik, die eine bestimmte Anzahl überschreitet. Diese Bedingung kann mit einem vordefinierten Zeitfenster verknüpft werden. |
| **Fenster** | (Optional) Die Bedingung für einen Warnhinweis kann auf ein vordefiniertes Zeitfenster beschränkt sein. Beispielsweise kann ein Warnhinweis abhängig von der Anzahl fehlgeschlagener Batches in den letzten fünf Minuten ausgelöst werden. |
| **Aktion** | Wenn ein Warnhinweis ausgelöst wird, wird eine Aktion ausgeführt. Insbesondere werden Nachrichten über einen Versandkanal an die entsprechenden Empfänger gesendet, z. B. einen vorkonfigurierten Webhook oder die Experience Platform-Benutzeroberfläche. |
| **Häufigkeit** | (Optional) Ein Warnhinweis kann so konfiguriert werden, dass er seine Aktion in einem bestimmten Intervall wiederholt, solange seine Bedingung wahr bleibt oder anderweitig ungelöst ist. |

{style="table-layout:auto"}

## Empfangen und Verwalten von Warnungen

Warnhinweise können über zwei Kanäle empfangen und verwaltet werden:

* [Adobe I/O-Ereignisse](#events)
* [Experience Platform-Benutzeroberfläche](#ui)

### I/O-Ereignisse {#events}

Warnhinweise können an einen konfigurierten Webhook gesendet werden, um eine effiziente Automatisierung der Aktivitätsüberwachung zu ermöglichen. Um Warnhinweise über einen Webhook zu erhalten, müssen Sie Ihren Webhook für Experience Platform-Warnhinweise in Adobe Developer Console registrieren. Spezifische Schritte finden Sie im Handbuch [Abonnieren von Adobe I/O Event-Benachrichtigungen](./subscribe.md).

### Experience Platform-Benutzeroberfläche {#ui}

Die Benutzeroberfläche von Experience Platform ermöglicht die Anzeige empfangener Warnhinweise und die Verwaltung von Warnhinweisregeln. Das folgende Video bietet eine Einführung in diese Funktionen.

>[!VIDEO](https://video.tv.adobe.com/v/336218?quality=12&learn=on)

Um mit Warnhinweisen in der Experience Platform-Benutzeroberfläche zu arbeiten, müssen Sie die folgenden Zugriffssteuerungsberechtigungen über Adobe Admin Console aktiviert haben:

| Berechtigung | Beschreibung |
| --- | --- |
| Anzeigen von Warnhinweisen | Ermöglicht die Anzeige der empfangenen Warnmeldungen. |
| Verlauf von Warnhinweisen anzeigen* | Ermöglicht die Anzeige eines Verlaufs der empfangenen Warnhinweise in der Registerkarte [!UICONTROL Warnhinweise]. |
| Verwalten von Warnhinweisen* | Ermöglicht die Aktivierung und Deaktivierung von Warnhinweisregeln über die Registerkarte [!UICONTROL Warnhinweise]. |
| Auflösen von Warnhinweisen* | Ermöglicht die Auflösung von ausgelösten Warnhinweisen über die Registerkarte [!UICONTROL Warnhinweise]. |

{style="table-layout:auto"}

* *Um auf die Registerkarte [!UICONTROL Warnhinweise] zugreifen zu können, müssen Sie außerdem über die Berechtigung „Warnhinweise anzeigen“ verfügen.*

>[!NOTE]
>
>Weitere Informationen zum Verwalten von Berechtigungen in Experience Platform finden Sie in der [Dokumentation zur Zugriffssteuerung](../../access-control/ui/overview.md).

Mit der Berechtigung „Warnhinweise anzeigen“ können Sie erhaltene Warnhinweise anzeigen, indem Sie oben rechts das Glockensymbol (![Glockensymbol](/help/images/icons/bell.png)) auswählen.

![](../images/alerts/overview/ui.png)

>[!NOTE]
>
> Wählen Sie einen Warnhinweis aus, um zu einem zugehörigen Dashboard zu navigieren, um genauere Informationen zur Ursache des Warnhinweises zu erhalten.

Darüber hinaus ermöglicht die Registerkarte [!UICONTROL Warnhinweise] in der Benutzeroberfläche es einzelnen Benutzern, sich für bestimmte Warnhinweistypen zu abonnieren, und gibt Administratoren die Möglichkeit, Warnhinweisregeln vollständig zu aktivieren oder zu deaktivieren. Weitere Informationen zum Verwalten von Warnhinweisen finden Sie im [Handbuch zur Benutzeroberfläche](./ui.md).

## Nächste Schritte

Durch das Lesen dieses Dokuments haben Sie sich mit Experience Platform-Warnhinweisen und ihrer Rolle im Experience Platform-Ökosystem vertraut gemacht. Lesen Sie die Prozessdokumentation, auf die in dieser Übersicht verlinkt wird, um zu erfahren, wie Sie Warnhinweise empfangen und verwalten können.
