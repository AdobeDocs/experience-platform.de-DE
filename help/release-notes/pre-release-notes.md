---
title: Hinweise zu Vorabversionen von Experience Platform
description: Eine Vorschau der neuesten Versionshinweise für Adobe Experience Platform.
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: efa50881315d986940f7cb3afcbfcc30ef67c3a7
workflow-type: tm+mt
source-wordcount: '1411'
ht-degree: 16%

---

# Hinweise zu Vorabversionen von Adobe Experience Platform

>[!IMPORTANT]
>
>Dieses Dokument ist als **Vorschau** der Versionshinweise für den aktuellen Monat gedacht. Release-Elemente können sich ändern und in der endgültigen Version hinzugefügt oder entfernt werden.

>[!TIP]
>
>Versionshinweise zu anderen Adobe Experience Platform-Programmen finden Sie in der folgenden Dokumentation:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/de/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/de/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/de/docs/analytics-platform/using/releases/latest)
>- [Komposition föderierter Zielgruppen](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/en/docs/real-time-cdp-collaboration/using/latest)

**Veröffentlichungsdatum: März 2026**

Neue Funktionen und Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Erweiterte Verwaltung des Datenlebenszyklus](#advanced-data-lifecycle-management)
- [Agent Orchestrator](#agent-orchestrator)
- [Ziele](#destinations)
- [Abfrage-Service](#query-service)
- [Echtzeit-Kundenprofil](#profile)
- [Ausführung und Bedienung](#run-and-operate)
- [Segmentierungs-Service](#segmentation-service)
- [Quellen](#sources)

## Erweiterte Verwaltung des Datenlebenszyklus {#advanced-data-lifecycle-management}

Experience Platform bietet eine Reihe von Datenhygiene-Funktionen, mit denen Sie Ihre gespeicherten Daten durch programmgesteuerte Löschungen von Verbraucherdatensätzen verwalten können. Mithilfe des Datenlebenszyklus-Arbeitsbereichs in der Benutzeroberfläche oder durch Aufrufe der Datenhygiene-API können Sie Ihre Datenspeicher effektiv verwalten. Verwenden Sie diese Funktionen, um sicherzustellen, dass Informationen erwartungsgemäß verwendet werden, aktualisiert werden, wenn falsche Daten korrigiert werden müssen, und gelöscht werden, wenn dies aufgrund von Unternehmensrichtlinien erforderlich ist.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Löschen von Datensätzen mit mehreren Datensätzen und nur Profilen (nur API) | Sie können eine einzelne Datensatz-ID, eine durch Kommas getrennte Liste von Datensatz-IDs oder das Literal `ALL` senden, `datasetId` Identitäten in einem, mehreren oder allen Datensätzen zu löschen. Sie können das Löschen auch auf Profil-Services beschränken, indem Sie `targetServices` auf `["identity","profile","ajo"]` festlegen, wodurch der Datalake unverändert bleibt. Weitere Informationen finden [ im Handbuch ](../hygiene/api/workorder.md) Löschen von Arbeitsaufträgen . |

{style="table-layout:auto"}

Weitere Informationen finden Sie im Abschnitt [Übersicht über das erweiterte Daten-Lifecycle-Management](../hygiene/home.md).

## Agent Orchestrator {#agent-orchestrator}

Mit Agent Orchestrator können Sie KI-gestützte Agenten erstellen und bereitstellen, die Workflows automatisieren und kanalübergreifend mit Kunden interagieren können.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Adobe Marketing Agent für [!DNL Microsoft 365 Copilot] | Adobe Marketing Agent for [!DNL Microsoft 365 Copilot] ist Ihr eingebetteter Agent, der Marketing-Intelligenz von Adobe direkt in alltägliche Tools wie [!DNL Teams], [!DNL Word], [!DNL PowerPoint] und andere [!DNL Microsoft 365]-Apps einbringt. Sie können diesen Agenten verwenden, um vertrauenswürdige Kampagneneinblicke aus Adobe-Programmen zu gewinnen, während Sie Kampagnen planen, Zielgruppen überprüfen oder mit Kollegen zusammenarbeiten, Kundenfragen beantworten und datenbasierte Entscheidungen treffen, ohne Ihren [!DNL Microsoft 365]-Workflow verlassen zu müssen. |

{style="table-layout:auto"}

Weitere Informationen finden Sie in der Dokumentation zu [Agent Orchestrator](https://experienceleague.adobe.com/de/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator).

## Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Funktionen**

| Ziel | Beschreibung |
| --- | --- |
| Unterstützung für [Snowflake](../destinations/catalog/warehouses/snowflake.md)Streaming, mehrere Regionen | Der Snowflake Streaming-Connector ist jetzt für Kunden außerhalb der US-amerikanischen VA7-Region verfügbar. Verwenden Sie den Dropdown-Selektor Region , um die Region Snowflake auszuwählen, in der sich Ihr Konto befindet. Die Dokumentation wurde mit der erwarteten Datenstruktur für Snowflake-Streaming-Tabellen aktualisiert. |
| Regionsauswahl für {0[Snowflake Streaming und {2](../destinations/catalog/warehouses/snowflake.md)Snowflake Batch)[](../destinations/catalog/warehouses/snowflake-batch.md) | Mit dem neuen durchsuchbaren Dropdown-Menü, in dem Suche und Dropdown zu einem Steuerelement kombiniert sind, können Sie Ihre Region jetzt einfacher finden. |
| Exportieren von Zielgruppen-Metadaten in [Snowflake Batch](../destinations/catalog/warehouses/snowflake-batch.md)-Ziele | Die an dieses Ziel exportierten Dateien enthalten jetzt Zielgruppen-Metadaten. Die neue Tabellenstruktur gilt für alle neuen Zielverbindungen, die in Zukunft eingerichtet werden. Die alte Tabellenstruktur wird noch weitere drei Monate beibehalten, bevor sie entfernt wird. |
| [!DNL Adobe Advertising Cloud DSP]-Verbindung | Die neue Adobe Advertising DSP-Verbindung bietet dieselben Funktionen wie die alte Verbindung sowie Unterstützung für zusätzliche Identitäten. |
| Unterstützung externer Zielgruppen für [The Trade Desk CRM](../destinations/catalog/advertising/tradedesk-emails.md), [Criteo](../destinations/catalog/advertising/criteo.md) und [Pinterest](../destinations/catalog/advertising/pinterest.md) | Sie können jetzt Zielgruppen über die Segmentierungs-Service-Segmente hinaus für das Trade Desk-CRM, Criteo und Pinterest aktivieren, einschließlich benutzerdefinierter Upload-Zielgruppen (aus CSV importiert), Lookalike-Zielgruppen, Federated-Zielgruppen und Zielgruppen, die in anderen Experience Platform-Programmen wie Adobe Journey Optimizer erstellt wurden. Weitere Informationen finden Sie [ Abschnitt ](../destinations/catalog/advertising/criteo.md#supported-audiences)Unterstützte Zielgruppen“ auf der Katalogseite jedes Ziels. |
| Zielgruppenfilter im Aktivierungs-Workflow | Sie können Zielgruppen im **[!UICONTROL Select audiences]** Schritt jetzt mit demselben Erlebnis wie die Seite Zielgruppen suchen und filtern. Sie können beispielsweise nach der Herkunft der Zielgruppe filtern, um die gesuchte Zielgruppe einfach zu finden. |
| Erhöhtes Limit für benutzerdefinierte Upload-Zielgruppen | Sie können jetzt bis zu 20 benutzerdefinierte Upload-Zielgruppen pro Zielinstanz aktivieren. Zuvor war diese Grenze 10. |
| [Datei jetzt exportieren](../destinations/ui/export-file-now.md) und [Ad-hoc-Aktivierungs-API](../destinations/api/ad-hoc-activation-api.md)Unterstützung für externe Zielgruppen | Sie können jetzt beim Aktivieren für Batch-dateibasierte Ziele die API „Datei jetzt exportieren“ (UI) und die Ad-hoc-Aktivierungs-API mit externen Zielgruppen (z. B. benutzerdefiniertes Hochladen, Lookalike, Federated und Zielgruppen aus anderen Experience Platform-Programmen) verwenden. |
| HTTP-API-Ziele mit OAuth 2 und mTLS | Sie können jetzt HTTP-API-Ziele erstellen und authentifizieren, die OAuth 2 verwenden, wenn der Authentifizierungsendpunkt gegenseitiges TLS (mTLS) erfordert. Der Token-Abruf während der Zieleinrichtung unterstützt jetzt mTLS. |
| Ziel des ZoomInfo-Kontos | Sie können jetzt Account-Zielgruppen von Real-Time Customer Data Platform (B2B) an ZoomInfo senden. |

{style="table-layout:auto"}

**Fehlerbehebungen und Verbesserungen**

| Fehlerbehebung | Beschreibung |
| --- | --- |
| [Snowflake Streaming](../destinations/catalog/warehouses/snowflake.md) Konto-ID-Validierung | Zum Schritt Konto-ID wurde ein Validator für reguläre Ausdrücke hinzugefügt. Wenn Sie Ihre ID eingeben, wird sie jetzt validiert, um sicherzustellen, dass die Organisations-ID und die Konto-ID im richtigen Format (durch einen Punkt getrennt) vorliegen. |
| Hashing der [TikTok](../destinations/catalog/social/tiktok.md)-Connector-Telefonnummern | Es wurde ein Problem behoben, bei dem aufgrund einer fehlerhaften Konfiguration in der Zielkarte Identitäten, die von Telefonnummern abgeleitet wurden, nicht für TikTok aktiviert wurden. |

{style="table-layout:auto"}

Weitere Informationen finden Sie unter [Ziele - Übersicht](../destinations/home.md).

## Echtzeit-Kundenprofil {#profile}

Adobe Experience Platform ermöglicht die Bereitstellung koordinierter, konsistenter und relevanter Erlebnisse für Ihre Kundinnen und Kunden, unabhängig davon, wo und wann sie mit Ihrer Marke interagieren. Das Echtzeit-Kundenprofil liefert eine ganzheitliche Sicht auf jeden einzelnen Kunden, indem es Daten aus Online- und Offline-Kanälen ebenso wie aus CRMs und Drittanbieter-Datenquellen und anderen Kanälen miteinander kombiniert.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Zeitauswahl der Profilereignisse | Sie können jetzt auf der Registerkarte Profilereignisse ein Zeitfenster festlegen, um Ereignisse innerhalb dieses Bereichs anzuzeigen und zu analysieren. Sie können das Zeitfenster auf bis zu 30 Tage einstellen. Standardmäßig werden Ereignisse der letzten 48 Stunden angezeigt. |

{style="table-layout:auto"}

Weitere Informationen finden Sie unter [Übersicht über das Echtzeit-Kundenprofil](../profile/home.md).

## Abfrage-Service {#query-service}

Der Abfrage-Service ermöglicht Ihnen die Verwendung von Standard-SQL zur Abfrage von Daten in Adobe Experience Platform [!DNL Data Lake]. Sie können beliebige Datensätze aus dem [!DNL Data Lake] verbinden und die Abfrageergebnisse als neuen Datensatz für die Verwendung in Berichten, im Datenwissenschafts-Arbeitsbereich oder für die Aufnahme in das Echtzeit-Kundenprofil verwenden.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Daten-Distiller-Beschleuniger | Sie können jetzt auf der Registerkarte „Beschleuniger“ einen Beschleuniger auswählen, die erforderlichen Parameter eingeben und die generierte SQL ausführen oder planen, ohne sie selbst zu schreiben. Klonen Sie jeden Beschleuniger in eine benutzerdefinierte Vorlage, um ihn zu bearbeiten. |

{style="table-layout:auto"}

Weitere Informationen finden Sie unter [Query Service - Übersicht](../query-service/home.md).

## Ausführung und Bedienung {#run-and-operate}

Überprüfen, beheben und optimieren Sie Ihre Experience Platform-Implementierungen mit den Tools „Ausführen und Bedienen“. Gewinnen Sie Einblicke in geplante Batch-Aktivierungen, identifizieren Sie Konfigurationsprobleme und verbessern Sie die Systemzuverlässigkeit.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| [Vorgangszeitpläne](../run-and-operate/job-schedules.md) allgemeine Verfügbarkeit | [!DNL Job Schedules] bietet eine einheitliche Ansicht aller geplanten Batch-Verarbeitungsaufträge in Ihrer Datenpipeline, von der Aufnahme bis zur Zielaktivierung. Überprüfen Sie den Ausführungsstatus, ermitteln Sie Planungskonflikte und diagnostizieren Sie Konfigurationsprobleme, bevor sie sich auf Ihre Geschäftsvorgänge auswirken. |
| Konsistenzprüfungen - allgemeine Verfügbarkeit | Schlechte Schema- und Identitätskonfigurationen führen zu erheblichen nachgelagerten Problemen, einschließlich falscher Profilerstellung, fehlgeschlagener Segmentqualifikation und ungenauer Aktivierung. <br>Konsistenzprüfungen ändern Ihren Ansatz von der reaktiven Fehlerbehebung zu proaktiver, präventiver Wartung. Konsistenzprüfungen sind stets aktive Scans Ihrer Schemata und Identitäten, die in Ihrer Sandbox verwendet werden, und bieten eine Zusammenfassung von Problemen, die Sie zur Untersuchung und Fehlerbehebung verwenden können. |

{style="table-layout:auto"}

Weitere Informationen finden Sie in der [Übersicht über Ausführung und Betrieb](../run-and-operate/overview.md), [Prüfen von ](../run-and-operate/job-schedules.md) und im [Handbuch zur Platform-Benutzeroberfläche](../landing/ui-guide.md).

## Segmentierungs-Service {#segmentation}

Experience Platform ermöglicht Ihnen die Erstellung von Zielgruppensegmenten aus Ihren Kundendaten und ermöglicht eine vollständige Lebenszyklusverwaltung dieser Zielgruppen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Quelle der Aufnahme in Audience Builder | Sie können jetzt sehen, ob jedes Attribut aus einer Batch-, Streaming- oder Edge-Quelle in Audience Builder stammt, um das Erstellen ungültiger oder ineffizienter Streaming-Zielgruppen zu vermeiden. |
| Nur Felder mit Daten im Konto-Audience-Builder anzeigen | Sie können jetzt filtern, um beim Erstellen von Konto-Zielgruppen nur Attribute anzuzeigen, die Daten enthalten. |

{style="table-layout:auto"}

Weitere Informationen finden Sie im Abschnitt [Zielgruppen - Übersicht](../segmentation/home.md).

## Quellen {#sources}

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue oder aktualisierte Quellen**

| Quelle | Beschreibung |
| --- | --- |
| Verbesserte Unterstützung für Change Data Capture | Sie können jetzt die Änderungsdatenerfassung mit den [!DNL Marketo Engage]-, [!DNL Microsoft Dynamics]- und [!DNL Salesforce CRM] verwenden. |

{style="table-layout:auto"}

Weitere Informationen finden Sie unter [Quelle – Übersicht](../sources/home.md).

<!--

| [!DNL Deltashare] | The new [!DNL Deltashare] source lets you securely bring live, shared datasets from your partners or internal lakehouse environments directly into Adobe's applications without copying or manually uploading files. You connect to a [!DNL Deltashare] endpoint, choose the tables you need, and you can then use that governed, up-to-date data alongside your existing profiles and insights, so you spend less time on data wrangling and more time activating and analyzing it in your marketing workflows. |
| [!DNL Kobie] | The new [!DNL Kobie] source connector lets you directly ingest rich loyalty data from [!DNL Kobie] into Adobe's applications, so you can activate it alongside your existing customer profiles and insights. You connect your [!DNL Kobie] environment, configure the data objects you want to bring in (such as member status, transactions, and engagement), and then you can use that up-to-date loyalty information to build audiences, personalize experiences, and measure performance without juggling separate systems. |
| [!DNL Talon.One] | The new Talon.One source lets you seamlessly bring promotion and incentive data from Talon.One into Adobe's applications, so you can use it alongside your existing customer profiles and behavioral data. You connect your Talon.One account, select the entities and events you want to ingest (such as campaigns, coupons, and redemptions), and then you can use that real-time promotion context to build smarter audiences, personalize offers, and better understand which incentives are driving performance—without managing separate, disconnected systems. |

-->

<!--

| Data Engineering Agent | The following new and updated skills are available in the Data Engineering Agent:<br><br><ul><li><strong>Data onboarding:</strong> Follow step-by-step workflows and example prompts to connect sources, check data quality, enrich data semantically, and ingest data for B2C and B2B flows, with expected outputs and troubleshooting guidance in the docs.</li><li><strong>Data quality and validation:</strong> Validate data fields and datasets using two new skills (DataField and DataSet).</li><li><strong>Data collection:</strong> Get in-context guidance for complex Data Collection configurations and use conversational insights to explore lineage, dependencies, and relationships across your data collection objects.</li></ul> |

-->