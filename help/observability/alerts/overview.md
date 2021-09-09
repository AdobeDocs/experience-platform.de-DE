---
keywords: Experience Platform;Startseite;beliebte Themen;Datumsbereich
title: Warnhinweise - Überblick
description: Erfahren Sie mehr über Warnhinweise in Adobe Experience Platform, einschließlich der Struktur der Definition von Warnhinweisregeln.
feature: Alerts
exl-id: c38a93c6-1618-4ef9-8f94-41c7ab4af43c
source-git-commit: d82487f34c0879ed27ac55e42d70346f45806131
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 4%

---

# Warnhinweise - Übersicht

Mit Adobe Experience Platform können Sie ereignisbasierte Warnungen zu Adobe Experience Platform-Aktivitäten abonnieren. Warnhinweise verringern oder beseitigen die Notwendigkeit, die [[!DNL Observability Insights] API](../api/overview.md) abzufragen, um zu überprüfen, ob ein Auftrag abgeschlossen wurde, ob ein bestimmter Meilenstein innerhalb eines Workflows erreicht wurde oder ob Fehler aufgetreten sind.

Wenn bestimmte Bedingungen in Ihren Platform-Vorgängen erreicht sind (z. B. ein potenzielles Problem, wenn das System einen Schwellenwert überschreitet), kann Platform allen Benutzern in Ihrer Organisation, die sich für sie angemeldet haben, Warnhinweise bereitstellen. Diese Nachrichten können sich über einen vordefinierten Zeitraum wiederholen, bis der Warnhinweis behoben wurde.

Dieses Dokument bietet einen Überblick über Warnhinweise in Adobe Experience Platform, einschließlich der Struktur der Definition von Warnregeln.

## Einmalige Warnhinweise im Vergleich zu sich wiederholenden Warnhinweisen

Plattformwarnungen können einmal gesendet werden oder in einem vordefinierten Intervall wiederholt werden, bis sie aufgelöst werden. Die Anwendungsfälle dieser einzelnen Optionen sollen sich wie folgt unterscheiden:

| einmaliger Warnhinweis | Warnhinweis wiederholen |
| --- | --- |
| Zeigt nicht unbedingt ein Problem an. | Gibt einen potenziell unerwünschten Status an. |
| Wiederholt nicht. | Kann sich wiederholen, wenn die anormale Bedingung beibehalten wird. |
| Zu den Beispielen gehören:<ul><li>Die Datenerfassung wurde erfolgreich abgeschlossen.</li><li>Die Ausführung einer Abfrage wurde abgeschlossen.</li><li>Die Daten wurden gelöscht.</li></ul> | Zu den Beispielen gehören:<ul><li>Die Aufnahmedauer überschreitet den Service-Level Agreement (SLA).</li><li>Die tägliche Aufnahme erfolgte in den letzten 24 Stunden nicht.</li><li>Die Fehlerrate des Stream-Prozessors liegt über dem konfigurierten Schwellenwert.</li><li>Die Gesamtzahl der Profile überschreitet die Berechtigung.</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Anatomie eines Warnhinweises

Ein Warnhinweis kann in die folgenden Komponenten unterteilt werden:

| Komponente | Beschreibung |
| --- | --- |
| **Metrik** | Eine Beobachtbarkeit [metric](../api/metrics.md#available-metrics), deren Wert den Warnhinweis Trigger, z. B. die Anzahl fehlgeschlagener Batch-Erfassungsereignisse (`timeseries.ingestion.dataset.batchfailed.count`). |
| **Bedingung** | Eine Bedingung für die Metrik, die den Warnhinweis Trigger, wenn sie auf &quot;true&quot;aufgelöst wird, z. B. eine Zählermetrik, die eine bestimmte Anzahl überschreitet. Diese Bedingung kann mit einem vordefinierten Zeitfenster verknüpft werden. |
| **Fenster** | (Optional) Die Bedingung für einen Warnhinweis kann auf ein vordefiniertes Zeitfenster beschränkt sein. Beispielsweise kann ein Warnhinweis abhängig von der Anzahl fehlgeschlagener Batches in den letzten fünf Minuten Trigger werden. |
| **Aktion** | Wenn ein Warnhinweis ausgelöst wird, wird eine Aktion ausgeführt. Insbesondere werden Nachrichten über einen Versandkanal an die entsprechenden Empfänger gesendet, z. B. einen vorkonfigurierten Webhook oder die Experience Platform-Benutzeroberfläche. |
| **Häufigkeit** | (Optional) Ein Warnhinweis kann so konfiguriert werden, dass er seine Aktion in einem bestimmten Intervall wiederholt, wenn seine Bedingung wahr bleibt oder anderweitig ungelöst ist. |

{style=&quot;table-layout:auto&quot;}

## Warnungen empfangen und verwalten

Warnhinweise können über zwei Kanäle empfangen und verwaltet werden:

* [Adobe I/O-Ereignisse](#events)
* [Platform-Benutzeroberfläche](#ui)

### E/A-Ereignisse {#events}

Warnhinweise können an einen konfigurierten Webhook gesendet werden, um eine effiziente Automatisierung der Aktivitätsüberwachung zu ermöglichen. Um Warnhinweise über Webhook zu erhalten, müssen Sie Ihren Webhook für Plattformwarnungen in der Adobe Developer Console registrieren. Spezifische Schritte finden Sie im Handbuch [Abonnieren von Adobe I/O Event-Benachrichtigungen](./subscribe.md) .

### Platform-Benutzeroberfläche {#ui}

Über die Platform-Benutzeroberfläche können Sie die empfangenen Warnungen anzeigen und Warnungsregeln verwalten. Das folgende Video bietet eine Einführung in diese Funktionen.

>[!VIDEO](https://video.tv.adobe.com/v/336218?quality=12&learn=on)

Um mit Warnhinweisen in der Platform-Benutzeroberfläche zu arbeiten, müssen Sie die folgenden Zugriffssteuerungsberechtigungen über Adobe Admin Console aktiviert haben:

| Berechtigung | Beschreibung |
| --- | --- |
| Warnhinweise anzeigen | Ermöglicht die Anzeige der empfangenen Warnmeldungen. |
| Verlauf von Warnhinweisen anzeigen* | Ermöglicht die Anzeige eines Verlaufs der empfangenen Warnungen im Tab [!UICONTROL Warnungen] . |
| Warnhinweise verwalten* | Ermöglicht die Aktivierung und Deaktivierung von Warnregeln über den Tab [!UICONTROL Warnhinweise] . |
| Warnhinweise auflösen* | Ermöglicht die Auflösung von ausgelösten Warnhinweisen über den Tab [!UICONTROL Warnhinweise] . |

{style=&quot;table-layout:auto&quot;}

**Um auf die Registerkarte [!UICONTROL Warnhinweise] zugreifen zu können, müssen Sie außerdem über die Berechtigung Warnhinweise anzeigen verfügen.*

>[!NOTE]
>
>Weitere Informationen zum Verwalten von Berechtigungen in Platform finden Sie in der [Dokumentation zur Zugriffskontrolle](../../access-control/ui/overview.md).

Mit der Berechtigung Warnhinweise anzeigen können Sie erhaltene Warnhinweise anzeigen, indem Sie oben rechts das Glockensymbol (![Glockensymbol](../images/alerts/overview/icon.png)) auswählen.

![](../images/alerts/overview/ui.png)

Darüber hinaus ermöglicht die Registerkarte [!UICONTROL Warnhinweise] in der Benutzeroberfläche es einzelnen Benutzern, sich für bestimmte Warnhinweistypen anzumelden und Administratoren die Möglichkeit, Warnhinweisregeln vollständig zu aktivieren oder zu deaktivieren. Weitere Informationen zum Verwalten von Warnhinweisen finden Sie im [UI-Handbuch](./ui.md) .

## Nächste Schritte

Durch Lesen dieses Dokuments wurden Sie mit Platform-Warnhinweisen und ihrer Rolle im Platform-Ökosystem vertraut gemacht. Informationen zum Empfang und zur Verwaltung von Warnhinweisen finden Sie in der Prozessdokumentation zu diesem Thema.
