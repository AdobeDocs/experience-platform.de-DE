---
title: Adobe Experience Platform – Versionshinweise März 2026
description: Versionshinweise März 2026 für Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: d7415a9deefac55b8583eb52a7c1f18caf5f3334
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 20%

---

# Adobe Experience Platform – Versionshinweise

>[!TIP]
>
>Versionshinweise zu anderen Adobe Experience Platform-Programmen finden Sie in der folgenden Dokumentation:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/de/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/de/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/de/docs/analytics-platform/using/releases/latest)
>- [Komposition föderierter Zielgruppen](https://experienceleague.adobe.com/de/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/de/docs/real-time-cdp-collaboration/using/latest)

**Veröffentlichungsdatum: Mittwoch, 24. März 2026**

Neue Funktionen und Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Erweiterte Verwaltung des Datenlebenszyklus](#advanced-data-lifecycle-management)
- [Agent Orchestrator](#agent-orchestrator)
- [Ziele](#destinations)
- [Experience-Datenmodell (XDM)](#xdm)
- [Quellen](#sources)

## Erweiterte Verwaltung des Datenlebenszyklus {#advanced-data-lifecycle-management}

Experience Platform bietet eine Reihe von Datenhygiene-Funktionen, mit denen Sie Ihre gespeicherten Daten durch programmgesteuerte Löschungen von Verbraucherdatensätzen verwalten können. Mithilfe des Datenlebenszyklus-Arbeitsbereichs in der Benutzeroberfläche oder Aufrufen der Datenhygiene-API können Sie Ihre Datenspeicher effektiv verwalten. Verwenden Sie diese Funktionen, um sicherzustellen, dass Informationen erwartungsgemäß verwendet werden, aktualisiert werden, wenn falsche Daten korrigiert werden müssen, und gelöscht werden, wenn dies aufgrund von Unternehmensrichtlinien erforderlich ist.

| Funktion | Beschreibung |
| --- | --- |
| Löschen von Datensätzen mit mehreren Datensätzen und nur Profilen (nur API) | Sie können eine einzelne Datensatz-ID, eine durch Kommas getrennte Liste von Datensatz-IDs oder das Literal `ALL` senden, `datasetId` Identitäten in einem, mehreren oder allen Datensätzen zu löschen. Sie können das Löschen auch auf profilbezogene Services beschränken, indem Sie `targetServices` auf `["identity","profile","ajo"]` festlegen. Dadurch bleibt der Datalake unverändert. Diese Funktion ist nur über die Data Hygiene API verfügbar. Weitere Informationen finden [&#x200B; im Handbuch zum Löschen von Arbeitsaufträgen &#x200B;](../../hygiene/api/workorder.md) Datensatz . |

{style="table-layout:auto"}

Weitere Informationen finden Sie im Abschnitt [Übersicht über das erweiterte Daten-Lifecycle-Management](../../hygiene/home.md).

## Agent Orchestrator {#agent-orchestrator}

Mit Agent Orchestrator können Sie KI-gestützte Agenten erstellen und bereitstellen, die Workflows automatisieren und kanalübergreifend mit Kunden interagieren können.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| [Adobe Marketing Agent für [!DNL Microsoft 365 Copilot]](https://experienceleague.adobe.com/de/docs/experience-cloud-ai/experience-cloud-ai/agents/ama-ms) | Adobe Marketing Agent for [!DNL Microsoft 365 Copilot] ist Ihr eingebetteter Agent, der Marketing-Intelligenz von Adobe direkt in alltägliche Tools wie [!DNL Teams], [!DNL Word], [!DNL PowerPoint] und andere [!DNL Microsoft 365]-Apps einbringt. Sie können diesen Agenten verwenden, um vertrauenswürdige Kampagneneinblicke aus Adobe-Programmen zu gewinnen, während Sie Kampagnen planen, Zielgruppen überprüfen, mit Kollegen zusammenarbeiten, um Kundenfragen zu beantworten, und um dateninformierte Entscheidungen zu treffen, ohne Ihren [!DNL Microsoft 365]-Workflow verlassen zu müssen. |

{style="table-layout:auto"}

Weitere Informationen finden Sie in der Dokumentation zu [Agent Orchestrator](https://experienceleague.adobe.com/de/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator).

## Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Funktionen**

| Ziel | Beschreibung |
| --- | --- |
| [Adobe Advertising DSP](../../destinations/catalog/advertising/adobe-advertising-cloud-connection.md)-Verbindung | Die neue Adobe Advertising DSP-Verbindung bietet dieselben Funktionen wie die alte Verbindung sowie Unterstützung für zusätzliche Identitäten. Mit dem neuen Connector können Sie auch Cookie-basierte Identitäten nach Adobe Advertising DSP exportieren. |
| [FreeWheel](../../destinations/catalog/advertising/freewheel.md)-Verbindung | Senden Sie [!DNL Real-Time CDP] Zielgruppen als tägliche Batch-Dateien an FreeWheel, damit Sie sie in FreeWheel-Angeboten und -Kampagnen für TV, Video und Display ansprechen können. Wenden Sie sich an Ihr Adobe-Accountteam, um Zugriff zu erhalten. |
| Unterstützung externer Zielgruppen für [The Trade Desk CRM](../../destinations/catalog/advertising/tradedesk-emails.md) und [Pinterest](../../destinations/catalog/advertising/pinterest.md) | Sie können jetzt Zielgruppen aus anderen Quellen als dem Segmentierungs-Service für das Trade Desk-CRM, Criteo und Pinterest aktivieren, einschließlich benutzerdefinierter Upload-Zielgruppen (importiert aus CSV), Lookalike-Zielgruppen, Federated-Zielgruppen und Zielgruppen, die in anderen Experience Platform-Programmen wie [!DNL Adobe Journey Optimizer] erstellt wurden. Diese Aktualisierung wird bis Ende März eingeführt. Weitere Informationen finden Sie [&#x200B; Abschnitt &#x200B;](../../destinations/catalog/advertising/criteo.md#supported-audiences)Unterstützte Zielgruppen“ auf der Katalogseite jedes Ziels. |
| Erhöhte Begrenzung für benutzerdefinierte Upload-Zielgruppen | Sie können jetzt bis zu 20 benutzerdefinierte Upload-Zielgruppen pro Zielinstanz aktivieren. Zuvor war diese Grenze 10. Weitere Informationen finden Sie [&#x200B; Leitplanken &#x200B;](../../destinations/guardrails.md#batch-file-based-activation) Ziele . |
| [Datei jetzt exportieren](../../destinations/ui/export-file-now.md) und [Ad-hoc-Aktivierungs-API](../../destinations/api/ad-hoc-activation-api.md)Unterstützung für externe Zielgruppen | Sie können jetzt beim Aktivieren für Batch-dateibasierte Ziele die API „Datei jetzt exportieren“ (UI) und die Ad-hoc-Aktivierungs-API mit externen Zielgruppen (z. B. benutzerdefiniertes Hochladen, Lookalike, Federated und Zielgruppen aus anderen Experience Platform-Programmen) verwenden. Diese Aktualisierung wird bis Ende März eingeführt. |

{style="table-layout:auto"}

**Fehlerbehebungen und Verbesserungen**

| Fehlerbehebung | Beschreibung |
| --- | --- |
| Hashing der [TikTok](../../destinations/catalog/social/tiktok.md)-Connector-Telefonnummern | Es wurde ein Problem behoben, bei dem aufgrund einer fehlerhaften Konfiguration in der Zielkarte Identitäten, die von Telefonnummern abgeleitet wurden, nicht für TikTok aktiviert wurden. Um von dieser Fehlerbehebung zu profitieren, richten Sie einen neuen Aktivierungsfluss ein oder entfernen Sie die Telefonnummern-Zuordnung aus Ihrem vorhandenen Fluss, speichern Sie sie und fügen Sie sie erneut hinzu. |

{style="table-layout:auto"}

Weitere Informationen finden Sie unter [Ziele - Übersicht](../../destinations/home.md).

## Experience-Datenmodell (XDM) {#xdm}

XDM ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen (Schemata) für Daten bereitstellt, die in Experience Platform importiert werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

| Funktion | Beschreibung |
| --- | --- |
| XDM-Entitätsaktionen und Löschunterstützung | Greifen Sie auf Aktionen für Schemata, Klassen, Feldergruppen und Datentypen direkt über Inline-Tabellenmenüs und Detailseiten-Kopfzeilenmenüs zu. Wenn Sie über die erforderlichen Berechtigungen verfügen, können Sie auch die Entitäten Ihrer Organisation löschen, wenn sie nicht von Datensätzen verwendet und nicht für Profil aktiviert sind. Weitere Informationen finden Sie [&#x200B; Handbuch zur XDM](../../xdm/ui/explore.md)Benutzeroberfläche . |

Weitere Informationen finden Sie in der [XDM-Übersicht](../../xdm/home.md).

<!-- 
## Run and Operate {#run-and-operate}

Inspect, troubleshoot, and optimize your Experience Platform implementations with the Run and Operate tools. Gain visibility into scheduled batch activations, identify configuration issues, and improve system reliability.

**New or updated features**

| Feature | Description |
| --- | --- |
| [Job Schedules](../../run-and-operate/job-schedules.md) general availability | [!DNL Job Schedules] provides a unified view of all scheduled batch processing jobs across your data pipeline, from ingestion through destination activation. Inspect execution status, identify scheduling conflicts, and diagnose configuration issues before they impact your business operations. |
| [Health Checks](../../run-and-operate/health-checks.md) general availability | Poor schema and identity configurations lead to significant downstream issues, including incorrect profile creation, failed segment qualification, and inaccurate activation. <br>Health checks shift your approach from reactive troubleshooting to proactive, preventative maintenance. Health checks are always-on scans of your schemas and identities used in your sandbox and provide a summary of issues that you can use to explore and troubleshoot. |

{style="table-layout:auto"}

For more information, read the [Run and Operate overview](../run-and-operate/overview.md), [Inspect job schedules](../run-and-operate/job-schedules.md), and the [Platform UI guide](../landing/ui-guide.md). -->

## Quellen

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue oder aktualisierte Quellen**

| Quelle | Beschreibung |
| --- | --- |
| [!DNL Talon.One] | Sie können Experience Platform jetzt mit [!DNL Talon.One] verbinden, indem Sie die neuen [!DNL Talon.One] ([) &#x200B;](../../sources/tutorials/ui/create/loyalty/talon-one-batch.md) [Streaming](../../sources/tutorials/ui/create/loyalty/talon-one-streaming.md) verwenden. Verwenden Sie die neuen Quellen, um Treueprofildaten sowie Transaktions- und Treueprogramm-Aktivitätsereignisse in Experience Platform aufzunehmen. |
| Neue IP-Adressen zur Zulassungsliste | Neue IP-Adressen für GBR9: Großbritannien wurde in die Liste der Adressen aufgenommen, die erfolgreich mit Experience Platform auf Azure verbunden werden müssen. Weitere Informationen finden Sie in der Liste [Handbuch zur IP](../../sources/ip-address-allow-list.md#gbr9-united-kingdom)Zulassungsliste). |
| Verbesserte Unterstützung für Change Data Capture | Sie können jetzt die Änderungsdatenerfassung mit den [!DNL Marketo Engage]-, [!DNL Microsoft Dynamics]- und [!DNL Salesforce CRM] verwenden. |
| Verbessertes Authentifizierungshandbuch für [[!DNL Google BigQuery]](../../sources/connectors/databases/bigquery.md) | Das Authentifizierungshandbuch für die [!DNL Google BigQuery] wurde um die folgenden Informationen erweitert: <ul><li>Die erforderlichen Bereiche für das Aktualisierungs-Token.</li><li>Die für die [!DNL Google] Identität erforderlichen IAM-Rollen.</li><li>Zusätzliche Anleitungen zur Verwendung von `largeResultsDataSetId`.</li></ul> |

{style="table-layout:auto"}

Weitere Informationen finden Sie unter [Quelle – Übersicht](../../sources/home.md).

<!--

NOTE FOR VLAD, CRITEO WAS REMOVED FROM EXTERNAL AUDIENCE SUPPORT

| Destination | Description |
| --- | --- |
| [Snowflake Batch](../../destinations/catalog/warehouses/snowflake-batch.md) region selector | You can now find your region more easily with the new searchable dropdown, which combines search and dropdown into one control. |
| New table structure for [Snowflake Batch](../../destinations/catalog/warehouses/snowflake-batch.md) destinations | Tables shared into your Snowflake account now have a new structure which includes separate audience name and audience origin columns. The new table structure applies to all new destination connections set up moving forward. For any new connections that you set up, an old format and new format table are created. The old table structure will be kept for another three months before being deprecated. Read more in the [Exported data](../../destinations/catalog/warehouses/snowflake-batch.md#exported-data) section of the Snowflake Batch documentation. |
| [HTTP API](../../destinations/catalog/streaming/http-destination.md) destinations with OAuth 2 and mTLS | You can now create and authenticate HTTP API destinations that use OAuth 2 when the authentication endpoint requires mutual TLS (mTLS); token retrieval during destination setup now supports mTLS. |

| Fix | Description |
| --- | --- |
| [Snowflake Streaming](../../destinations/catalog/warehouses/snowflake.md) and [Snowflake Batch](../../destinations/catalog/warehouses/snowflake-batch.md) account ID validation | A regular expression validator has been added to the Account ID step. When you enter your ID, it is now validated to ensure organization ID and account ID are in the correct format (separated by a dot). |

-->