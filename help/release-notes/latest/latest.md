---
title: Adobe Experience Platform – Versionshinweise, Oktober 2025
description: Versionshinweise von Oktober 2025 für Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 57cb9f5e57c83576a125ec2de5eb3e4526d5b572
workflow-type: tm+mt
source-wordcount: '1004'
ht-degree: 14%

---

# Adobe Experience Platform – Versionshinweise

>[!TIP]
>
>Versionshinweise zu anderen Adobe Experience Platform-Programmen finden Sie in der folgenden Dokumentation:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/de/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/de/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/de/docs/analytics-platform/using/releases/pre-release-notes)
>- [Komposition föderierter Zielgruppen](https://experienceleague.adobe.com/de/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/de/docs/real-time-cdp-collaboration/using/latest)

**Veröffentlichungsdatum: 22. Oktober 2025**

Neue Funktionen und Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Agent Orchestrator](#agent-orchestrator)
- [Warnhinweise](#alerts)
- [Ziele](#destinations)
- [Quellen](#sources)

## Agent Orchestrator {#agent-orchestrator}

Adobe Experience Platform Agent Orchestrator ist die neue agentische Schicht in Adobe Experience Platform.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Audience Agent | Die Audience Agent unterstützt jetzt Account-basierte Zielgruppen für die dialogorientierte Zielgruppenexploration und die Erkennung doppelter Zielgruppen. Weitere Informationen finden Sie in der Dokumentation zu [Audience Agent](https://experienceleague.adobe.com/de/docs/experience-cloud-ai/experience-cloud-ai/agents/audience). |

Weitere Informationen zu Agenten finden Sie in der [Dokumentation zu Agent Orchestrator](https://experienceleague.adobe.com/de/docs/experience-cloud-ai/experience-cloud-ai/home).

## Warnhinweise {#alerts}

Mit Experience Platform können Sie ereignisbasierte Warnhinweise für verschiedene Experience Platform-Aktivitäten abonnieren. Sie können unterschiedliche Warnhinweisregeln über die Registerkarte [!UICONTROL Alerts] in der Benutzeroberfläche von Experience Platform abonnieren. Zusätzlich können Sie auswählen, ob Warnhinweise in der Benutzeroberfläche oder über E-Mail-Benachrichtigungen angezeigt werden sollen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Warnhinweis bei Aktivierungsausfallrate | Für folgende Ziele wurde ein neuer Warnhinweis hinzugefügt **(Aktivierungsfehlerrate überschreitet den Schwellenwert**. Dieser Warnhinweis benachrichtigt Sie, wenn die Anzahl fehlgeschlagener Datensätze während der Datenaktivierung den zulässigen Schwellenwert überschritten hat, sodass Sie schnell auf Aktivierungsprobleme reagieren können. Weitere Informationen finden Sie in der Dokumentation [Standardwarnhinweisregeln](../../observability/alerts/rules.md) . |

{style="table-layout:auto"}

Weitere Informationen zu Warnhinweisen finden Sie im Abschnitt [[!DNL Observability Insights] Übersicht](../../observability/home.md).

## Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Funktionen**

| Ziel | Beschreibung |
| --- | --- |
| [!DNL Adform] | Verwenden Sie dieses Ziel, um Adobe Real-Time CDP-Zielgruppen zur Aktivierung basierend auf der Experience Cloud ID (ECID) und der ID Fusion von [!DNL Adform] an [!DNL Adform] zu senden. ID Fusion von [!DNL Adform] ist ein Service zur ID-Auflösung, mit dem Sie Ihre First-Party-Zielgruppen basierend auf der Experience Cloud ID (ECID) aktivieren können. Weitere Informationen finden [[!DNL Adform]  in &#x200B;](../../destinations/catalog/advertising/adform.md) Dokumentation |
| [!DNL Amazon Ads] | Es wurde eine zusätzliche Unterstützung für persönliche Identifikatoren hinzugefügt. Dazu gehören Felder wie `firstName`, `lastName`, `street`, `city`, `state`, `zip` und `country`. Die Zuordnung dieser Felder als Zielidentitäten kann die Übereinstimmungsraten der Zielgruppen verbessern. Weitere Informationen finden [[!DNL Amazon Ads]  in der &#x200B;](../../destinations/catalog/advertising/amazon-ads.md). |
| [!DNL Snowflake Batch] (eingeschränkte Verfügbarkeit) | Erstellen Sie eine Live [!DNL Snowflake]-Datenfreigabe, um tägliche Zielgruppenaktualisierungen direkt als freigegebene Tabellen in Ihrem Konto zu erhalten. Diese Integration ist derzeit für Kundenorganisationen verfügbar, die in der Region VA7 bereitgestellt sind. Weitere Informationen finden [[!DNL Snowflake Batch]  in der &#x200B;](../../destinations/catalog/warehouses/snowflake-batch.md). |
| [!DNL Snowflake Streaming] (eingeschränkte Verfügbarkeit) | Erstellen Sie eine Live [!DNL Snowflake]-Datenfreigabe, um Aktualisierungen der Streaming-Zielgruppe direkt als freigegebene Tabellen in Ihrem Konto zu erhalten. Diese Integration ist derzeit für Kundenorganisationen verfügbar, die in der Region VA7 bereitgestellt sind. Weitere Informationen finden [[!DNL Snowflake Streaming]  in der &#x200B;](../../destinations/catalog/warehouses/snowflake.md). |

{style="table-layout:auto"}

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| [Verschiedene neue Ziele, die die Überwachung auf Zielgruppenebene unterstützen](../../dataflows/ui/monitor-destinations.md#audience-level-view) | Die folgenden Ziele unterstützen jetzt die Überwachung auf Zielgruppenebene: <ul><li>[!DNL Airship Tags]</li><li>(API) [!DNL Salesforce Marketing Cloud]</li><li>[!DNL Marketo Engage]</li><li>[!DNL Microsoft Bing]</li><li>(v1) [!DNL Pega CDH Realtime Audience]</li><li>(v2) [!DNL Pega CDH Realtime Audience]</li><li>[!DNL Salesforce Marketing Cloud] Kontointeraktion</li><li>[!DNL The Trade Desk]</li></ul> |
| Fehlerbehebung bei Leitplanken für den Datensatzexport | Es wurde eine Korrektur für die Leitplanken für den Datensatzexport implementiert. Zuvor wurden einige Datensätze, die eine Zeitstempelspalte enthielten, aber _nicht_ auf dem XDM-Erlebnisereignis-Schema basierten, fälschlicherweise als Erlebnisereignis-Datensätze behandelt, was die Exporte auf ein 365-tägiges Lookback-Fenster beschränkte. Die dokumentierte 365-Tage-Lookback-Schutzmaßnahme gilt jetzt ausschließlich für Experience Events-Datensätze. Datensätze, die ein anderes Schema als das XDM-Erlebnisereignis-Schema verwenden, werden jetzt von der Leitplanke für 10 Milliarden Datensätze geregelt. Einige Kunden sehen möglicherweise höhere Exportzahlen für Datensätze, die fälschlicherweise unter das 365-tägige Lookback-Fenster fielen. Auf diese Weise können Sie Datensätze für prädiktive Workflows exportieren, die über ein langes Lookback-Fenster verfügen. Weitere Informationen finden Sie unter [Leitplanken für Datensatzexporte](../../destinations/guardrails.md#dataset-exports). |
| Verbessertes Reporting auf Zielgruppenebene für Unternehmensziele | Nach dieser Version erhalten Kundinnen und Kunden genauere Zahlen für Zielgruppenberichte, die nur Zielgruppen enthalten, die für das ausgewählte Ziel relevant sind. Diese Anpassung der Überwachung stellt sicher, dass die Berichterstellung nur Zielgruppen umfasst, die dem Datenfluss zugeordnet sind, und bietet somit klarere Einblicke in die tatsächliche Datenaktivierung. Dies wirkt sich nicht auf die Menge der aktivierten Daten aus. Es handelt sich lediglich um eine Verbesserung der Überwachung zur Verbesserung der Reporting-Genauigkeit. |

{style="table-layout:auto"}

Weitere Informationen finden Sie unter [Ziele - Übersicht](../../destinations/home.md).

## Quellen {#sources}

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Änderung der Datensatzerstellung für die Adobe Analytics-Quelle | Im Rahmen des Erstellungsprozesses eines Datenflusses zwischen Adobe Analytics und Experience Platform wird ein Datensatz über den Katalog-Service erstellt. Dieser Datensatz dient als Container für die Daten, die aufgenommen werden sollen. Derzeit umfasst dieser Prozess eine DataSource-ID, die aus der Analytics-Report Suite abgerufen, an den Katalog-Service gesendet und dann mit dem neu erstellten Datensatz verknüpft wird. Nach der Änderung ist die Option zum Angeben der Datenquellen-ID während der Erstellung des Datensatzes nicht mehr verfügbar. Daher ist neuen Datensätzen, die von der Analytics-Quelle erstellt wurden, im Katalog-Service keine DataSource-ID mehr zugeordnet. Diese Änderung gilt nur für die Metadaten und ändert in keiner Weise die Speicherung der Daten im Datensatz. Beachten Sie jedoch, dass die vom Katalog-Service bereitgestellte DataSource-ID in neu erstellten Datensätzen für Adobe Analytics nicht mehr verfügbar ist. Weitere Informationen zum Adobe Analytics-Quell-Connector finden [&#x200B; in der Dokumentation zum Adobe Analytics-Quell-Connector für &#x200B;](../../sources/connectors/adobe-applications/analytics.md). |
| Allgemeine Verfügbarkeit der [!DNL Google Ads] (nur API) | Die [API-Version der  [!DNL Google Ads]](../../sources/tutorials/api/create/advertising/ads.md)-Quelle ist jetzt allgemein verfügbar. Die API-Dokumentation wurde aktualisiert und zeigt nun, dass die neueste Version `v21` ist. Experience Platform unterstützt alle Versionen v19 und höher. [Die Benutzeroberflächenversion](../../sources/tutorials/ui/create/advertising/ads.md) befindet sich weiterhin in der Beta-Phase und unterstützt nur eine einmalige Aufnahme. Verwenden Sie die API-Route, um die inkrementelle Datenaufnahme zu verwenden. |
| Unterstützung virtueller [!DNL Azure Event Hubs] | Adobe unterstützt jetzt explizit virtuelle Netzwerkverbindungen zu [[!DNL Azure Event Hubs]](../../sources/connectors/cloud-storage/eventhub.md) und ermöglicht so die Datenübertragung über private Netzwerke anstatt über öffentliche Netzwerke. Auf die Zulassungsliste setzen Kunden können mit Experience Platform VNet den Traffic von Event Hubs privat über das private Azure-Backbone routen und so erweiterte Sicherheit und Compliance für Workflows zur Datenaufnahme bieten. |

{style="table-layout:auto"}

Weitere Informationen finden Sie unter [Quelle – Übersicht](../../sources/home.md).

<!--
| Source | Description |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Talon.one] sources for loyalty data | Use the [[!DNL Talon.One] sources](../../sources/connectors/loyalty/talon-one.md) to ingest batch and streaming loyalty data into Experience Platform. The connector supports streaming of profile data, transaction data, and loyalty data including points earned, points redeemed, points expired, and tier data. For more information, read the [!DNL Talon.One] [batch](../../sources/tutorials/ui/create/loyalty/talon-one-batch.md) and [streaming](../../sources/tutorials/ui/create/loyalty/talon-one-streaming.md) documentation. |
-->