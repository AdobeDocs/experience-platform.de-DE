---
title: Adobe Experience Platform – Versionshinweise März 2026
description: Versionshinweise März 2026 für Adobe Experience Platform.
exl-id: 66b948fd-caa0-4e5e-83dd-3b15b77c09fa
source-git-commit: 381d1f952067cece9f9a9618a00bbed304214906
workflow-type: tm+mt
source-wordcount: '1747'
ht-degree: 12%

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
- [Datenströme](#datastreams)
- [Ziele](#destinations)
- [Experience-Datenmodell (XDM)](#xdm)
- [Echtzeit-Kundenprofil](#real-time-customer-profile)
- [Segmentierungs-Service](#segmentation-service)
- [Quellen](#sources)

## Erweiterte Verwaltung des Datenlebenszyklus {#advanced-data-lifecycle-management}

Experience Platform bietet eine Reihe von Datenhygiene-Funktionen, mit denen Sie Ihre gespeicherten Daten durch programmgesteuerte Löschungen von Verbraucherdatensätzen verwalten können. Mithilfe des Datenlebenszyklus-Arbeitsbereichs in der Benutzeroberfläche oder Aufrufen der Datenhygiene-API können Sie Ihre Datenspeicher effektiv verwalten. Verwenden Sie diese Funktionen, um sicherzustellen, dass Informationen erwartungsgemäß verwendet werden, aktualisiert werden, wenn falsche Daten korrigiert werden müssen, und gelöscht werden, wenn dies aufgrund von Unternehmensrichtlinien erforderlich ist.

| Funktion | Beschreibung |
| --- | --- |
| Löschen von Datensätzen mit mehreren Datensätzen und nur Profilen (nur API) | Sie können eine einzelne Datensatz-ID, eine durch Kommas getrennte Liste von Datensatz-IDs oder das Literal `ALL` senden, `datasetId` Identitäten in einem, mehreren oder allen Datensätzen zu löschen. Sie können das Löschen auch auf profilbezogene Services beschränken, indem Sie `targetServices` auf `["identity","profile","ajo"]` festlegen. Dadurch bleibt der Datalake unverändert. Diese Funktion ist nur über die Data Hygiene API verfügbar. Weitere Informationen finden [&#x200B; im Handbuch zum Löschen von Arbeitsaufträgen &#x200B;](../../hygiene/api/workorder.md) Datensatz . |

{style="table-layout:auto"}

Weitere Informationen finden Sie im Abschnitt [Übersicht über das erweiterte Daten-Lifecycle-Management](../../hygiene/home.md).

## Agent Orchestrator {#agent-orchestrator}

Verwenden Sie Agent Orchestrator, um KI-gestützte Agenten zu erstellen und bereitzustellen, die Workflows automatisieren und kanalübergreifend mit Kunden interagieren.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| [Adobe Marketing Agent für [!DNL Microsoft 365 Copilot]](https://experienceleague.adobe.com/de/docs/experience-cloud-ai/experience-cloud-ai/agents/ama-ms) | Adobe Marketing Agent for [!DNL Microsoft 365 Copilot] ist Ihr eingebetteter Agent, der Marketing-Intelligenz von Adobe direkt in alltägliche Tools wie [!DNL Teams], [!DNL Word], [!DNL PowerPoint] und andere [!DNL Microsoft 365]-Apps einbringt. Sie können diesen Agenten verwenden, um vertrauenswürdige Kampagneneinblicke aus Adobe-Programmen zu gewinnen, während Sie Kampagnen planen, Zielgruppen überprüfen, mit Kollegen zusammenarbeiten, um Kundenfragen zu beantworten, und um dateninformierte Entscheidungen zu treffen, ohne Ihren [!DNL Microsoft 365]-Workflow verlassen zu müssen. |

{style="table-layout:auto"}

Weitere Informationen finden Sie in der Dokumentation zu [Agent Orchestrator](https://experienceleague.adobe.com/de/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator).

## Datenströme {#datastreams}

Ein Datenstrom stellt die Server-seitige Konfiguration bei der Implementierung der Adobe Experience Platform Web- und Mobile-SDKs und der Adobe Experience Platform Edge Network Server-API dar. Der Befehl zur Datenstromkonfiguration in den SDKs verarbeitet alle Services, mit denen ein Client interagiert.

| Funktion | Beschreibung |
| --- | --- |
| Dynamische Datenstromkonfigurationen - allgemeine Verfügbarkeit | Dynamische Datenstromkonfigurationen sind jetzt allgemein verfügbar. Mit dynamischen Datenstromkonfigurationen können Sie benutzerkonfigurierbare Regelsätze für jeden Service definieren, der für Ihren Datenstrom aktiviert ist. Diese bestimmen, welche Experience Cloud-Lösung die einzelnen Datentypen erhalten soll. Weitere Informationen finden Sie [&#x200B; Handbuch &#x200B;](../../datastreams/configure-dynamic-datastream.md) dynamische Datenstromkonfigurationen . |

{style="table-layout:auto"}

Weitere Informationen finden Sie unter [Datenströme - Übersicht](../../datastreams/overview.md).

## Ziele {#destinations}

[!DNL Destinations] sind vordefinierte Integrationen mit Zielplattformen. Verwenden Sie Ziele, um Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle zu aktivieren.

**Neue oder aktualisierte Funktionen**

| Ziel | Beschreibung |
| --- | --- |
| [Regionsauswahl für Snowflake &#x200B;](../../destinations/catalog/warehouses/snowflake-batch.md)Batch) | Mit dem neuen durchsuchbaren Dropdown-Menü, in dem Suche und Dropdown zu einem Steuerelement kombiniert sind, können Sie Ihre Region jetzt einfacher finden. Diese Aktualisierung wird bis Ende März eingeführt. |
| Neue Tabellenstruktur für [Snowflake Batch](../../destinations/catalog/warehouses/snowflake-batch.md)-Ziele | In Ihrem Snowflake-Konto freigegebene Tabellen haben jetzt eine neue Struktur, die separate Spalten für Zielgruppennamen und Zielgruppenursprung enthält. Die neue Tabellenstruktur gilt für alle neuen Zielverbindungen, die in Zukunft eingerichtet werden. Für alle neu eingerichteten Verbindungen werden beide Tabellenstrukturen erstellt: Der neuen Struktur wird das Präfix V2 vorangestellt, und die alte Struktur wird bis Ende Juni 2026 beibehalten. Danach wird sie eingestellt. Weitere Informationen finden Sie [&#x200B; Abschnitt &#x200B;](../../destinations/catalog/warehouses/snowflake-batch.md#exported-data) exportierten Daten in der Snowflake-Batch-Dokumentation. Diese Aktualisierung wird bis Ende März eingeführt. |
| [Adobe Advertising DSP](../../destinations/catalog/advertising/adobe-advertising-dsp-connection.md)-Verbindung | Die neue Adobe Advertising DSP-Verbindung bietet dieselben Funktionen wie die alte Verbindung sowie Unterstützung für zusätzliche Identitäten. Mit dem neuen Connector können Sie auch Cookie-basierte Identitäten nach Adobe Advertising DSP exportieren. |
| [FreeWheel](../../destinations/catalog/advertising/freewheel.md)-Verbindung | Senden Sie [!DNL Real-Time CDP] Zielgruppen als tägliche Batch-Dateien an FreeWheel, damit Sie sie in FreeWheel-Angeboten und -Kampagnen für TV, Video und Display ansprechen können. Wenden Sie sich an Ihr Adobe-Accountteam, um Zugriff zu erhalten. |
| Unterstützung externer Zielgruppen für [The Trade Desk CRM](../../destinations/catalog/advertising/tradedesk-emails.md) und [Pinterest](../../destinations/catalog/advertising/pinterest.md) | Sie können jetzt Zielgruppen aus anderen Quellen als dem Segmentierungs-Service für das Trade Desk-CRM, Criteo und Pinterest aktivieren, einschließlich benutzerdefinierter Upload-Zielgruppen (importiert aus CSV), Lookalike-Zielgruppen, Federated-Zielgruppen und Zielgruppen, die in anderen Experience Platform-Programmen wie [!DNL Adobe Journey Optimizer] erstellt wurden. Diese Aktualisierung wird bis Ende März eingeführt. Weitere Informationen finden Sie [&#x200B; Abschnitt &#x200B;](../../destinations/catalog/advertising/criteo.md#supported-audiences)Unterstützte Zielgruppen“ auf der Katalogseite jedes Ziels. |
| Erhöhte Begrenzung für benutzerdefinierte Upload-Zielgruppen | Sie können jetzt bis zu 20 benutzerdefinierte Upload-Zielgruppen pro Zielinstanz aktivieren. Zuvor war diese Grenze 10. Weitere Informationen finden Sie [&#x200B; Leitplanken &#x200B;](../../destinations/guardrails.md#batch-file-based-activation) Ziele . |
| [Datei jetzt exportieren](../../destinations/ui/export-file-now.md) und [Ad-hoc-Aktivierungs-API](../../destinations/api/ad-hoc-activation-api.md)Unterstützung für externe Zielgruppen | Sie können jetzt beim Aktivieren für Batch-dateibasierte Ziele die API „Datei jetzt exportieren“ (UI) und die Ad-hoc-Aktivierungs-API mit externen Zielgruppen (z. B. benutzerdefiniertes Hochladen, Lookalike, Federated und Zielgruppen aus anderen Experience Platform-Programmen) verwenden. Diese Aktualisierung wird bis Ende März eingeführt. |
| [HTTP-API](../../destinations/catalog/streaming/http-destination.md)-Ziele mit OAuth 2 und mTLS | Sie können jetzt HTTP-API-Ziele erstellen und authentifizieren, die OAuth 2 verwenden, wenn der Authentifizierungsendpunkt gegenseitiges TLS (mTLS) erfordert. Der Token-Abruf während der Zieleinrichtung unterstützt jetzt mTLS. Diese Aktualisierung wird bis Ende März eingeführt. |

{style="table-layout:auto"}

**Fehlerbehebungen und Verbesserungen**

| Fehlerbehebung | Beschreibung |
| --- | --- |
| Hashing der [TikTok](../../destinations/catalog/social/tiktok.md)-Connector-Telefonnummern | Es wurde ein Problem behoben, bei dem aufgrund einer fehlerhaften Konfiguration in der Zielkarte Identitäten, die von Telefonnummern abgeleitet wurden, nicht für TikTok aktiviert wurden. Um von dieser Fehlerbehebung zu profitieren, richten Sie einen neuen Aktivierungsfluss ein oder entfernen Sie die Telefonnummern-Zuordnung aus Ihrem vorhandenen Fluss, speichern Sie sie und fügen Sie sie erneut hinzu. |
| [Snowflake Streaming](../../destinations/catalog/warehouses/snowflake.md) und [Snowflake Batch](../../destinations/catalog/warehouses/snowflake-batch.md) Konto-ID-Validierung | Zum Schritt Konto-ID wurde ein Validator für reguläre Ausdrücke hinzugefügt. Wenn Sie Ihre ID eingeben, wird sie jetzt validiert, um sicherzustellen, dass die Organisations-ID und die Konto-ID im richtigen Format (durch einen Punkt getrennt) vorliegen. Diese Aktualisierung wird bis Ende März eingeführt. |

{style="table-layout:auto"}

Weitere Informationen finden Sie unter [Ziele - Übersicht](../../destinations/home.md).

## Experience-Datenmodell (XDM) {#xdm}

XDM ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen (Schemata) für Daten bereitstellt, die in Experience Platform importiert werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

| Funktion | Beschreibung |
| --- | --- |
| XDM-Entitätsaktionen und Löschunterstützung | Greifen Sie auf Aktionen für Schemata, Klassen, Feldergruppen und Datentypen direkt über Inline-Tabellenmenüs und Detailseiten-Kopfzeilenmenüs zu. Wenn Sie über die erforderlichen Berechtigungen verfügen, können Sie auch die Entitäten Ihrer Organisation löschen, wenn sie nicht von Datensätzen verwendet und nicht für Profil aktiviert sind. Weitere Informationen finden Sie [&#x200B; Handbuch zur XDM](../../xdm/ui/explore.md)Benutzeroberfläche . |

Weitere Informationen finden Sie in der [XDM-Übersicht](../../xdm/home.md).

## Echtzeit-Kundenprofil {#real-time-customer-profile}

Das Echtzeit-Kundenprofil liefert Ihnen einen vollständigen Überblick über jeden einzelnen Kunden, indem es Daten aus verschiedenen Kanälen, einschließlich Online-, Offline-, CRM- und Drittanbieterdaten, kombiniert. Mit dem Profil können Sie Ihre Kundendaten in einer zentralen Ansicht zusammenführen, die eine aussagekräftige, Darstellung jeder Kundeninteraktion mit Zeitstempel bietet.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Ereignisse | Sie können jetzt die Lookback-Periode von Ereignissen beim Durchsuchen Ihrer Profile festlegen. Auf diese Weise können Sie die Ereignisse anzeigen, mit denen das Profil für den angegebenen Zeitraum verknüpft ist. Weitere Informationen finden Sie im [Handbuch zur Profil-Benutzeroberfläche](../../profile/ui/user-guide.md#events). |

{style="table-layout:auto"}

Weitere Informationen finden Sie in der [[!DNL Real-Time Customer Profile] Übersicht](../../profile/home.md).

## Ausführung und Bedienung {#run-and-operate}

Überprüfen, beheben und optimieren Sie Ihre Experience Platform-Implementierungen mit den Tools „Ausführen und Bedienen“. Gewinnen Sie Einblicke in geplante Batch-Aktivierungen, identifizieren Sie Konfigurationsprobleme und verbessern Sie die Systemzuverlässigkeit.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| [Vorgangszeitpläne](../../run-and-operate/job-schedules.md) allgemeine Verfügbarkeit | [!DNL Job Schedules] bietet eine einheitliche Ansicht aller geplanten Batch-Verarbeitungsaufträge in Ihrer Datenpipeline, von der Aufnahme bis zur Zielaktivierung. Überprüfen Sie den Ausführungsstatus, ermitteln Sie Planungskonflikte und diagnostizieren Sie Konfigurationsprobleme, bevor sie sich auf Ihre Geschäftsvorgänge auswirken. |
| [Konsistenzprüfungen](../../run-and-operate/health-checks.md) allgemeine Verfügbarkeit | Schlechte Schema- und Identitätskonfigurationen führen zu erheblichen nachgelagerten Problemen, einschließlich falscher Profilerstellung, fehlgeschlagener Segmentqualifikation und ungenauer Aktivierung. <br>Konsistenzprüfungen ändern Ihren Ansatz von der reaktiven Fehlerbehebung zu proaktiver, präventiver Wartung. Konsistenzprüfungen sind stets aktive Scans Ihrer Schemata und Identitäten, die in Ihrer Sandbox verwendet werden, und bieten eine Zusammenfassung von Problemen, die Sie zur Untersuchung und Fehlerbehebung verwenden können. |

{style="table-layout:auto"}

Weitere Informationen finden Sie in der [Übersicht über Ausführung und Betrieb](../../run-and-operate/overview.md), [Prüfen von &#x200B;](../../run-and-operate/job-schedules.md) und im [Handbuch zur Platform-Benutzeroberfläche](../../landing/ui-guide.md).

## Segmentierungs-Service {#segmentation-service}

[!DNL Segmentation Service] definiert eine bestimmte Teilmenge von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Zielgruppen können auf Datensatzdaten (z. B. demografische Informationen) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Aufnahmetyp | Sie können jetzt den Aufnahmetyp Ihrer Attribute anzeigen. Auf diese Weise erfahren Sie, woher Ihre Daten stammen, und können so bessere Zielgruppen erstellen. Weitere Informationen zu dieser Funktion finden Sie im [Segment Builder-Handbuch](../../segmentation/ui/segment-builder.md). |
| Zusammenfassungsdaten | Sie können jetzt die Zusammenfassungsdaten für Ihre Attribute für Konto- und personenbasierte Zielgruppen anzeigen. Weitere Informationen zu dieser Funktion in Konto-Zielgruppen finden Sie im Handbuch zu [&#x200B; . &#x200B;](../../rtcdp/segmentation/audience-builder.md) Weitere Informationen zu dieser Funktion in personenbasierten Zielgruppen finden Sie im [Segment Builder-Handbuch](../../segmentation/ui/segment-builder.md). |

Weitere Informationen finden Sie in der [[!DNL Segmentation Service] Übersicht](../../segmentation/home.md).

## Quellen {#sources}

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Verwenden Sie diese Quellverbindungen, um sich zu authentifizieren und eine Verbindung zu externen Speichersystemen und CRM-Services herzustellen, Zeiten für Aufnahmedurchgänge festzulegen und den Datenaufnahmedurchsatz zu verwalten.

**Neue oder aktualisierte Quellen**

| Quelle | Beschreibung |
| --- | --- |
| [!DNL Talon.One] | Sie können Experience Platform jetzt mit [!DNL Talon.One] verbinden, indem Sie die neuen [!DNL Talon.One] ([) &#x200B;](../../sources/tutorials/ui/create/loyalty/talon-one-batch.md) [Streaming](../../sources/tutorials/ui/create/loyalty/talon-one-streaming.md) verwenden. Verwenden Sie die neuen Quellen, um Treueprofildaten sowie Transaktions- und Treueprogramm-Aktivitätsereignisse in Experience Platform aufzunehmen. |
| Neue IP-Adressen zur Zulassungsliste | Neue IP-Adressen für GBR9: Großbritannien wurde in die Liste der Adressen aufgenommen, die erfolgreich mit Experience Platform auf Azure verbunden werden müssen. Weitere Informationen finden Sie in der Liste [Handbuch zur IP](../../sources/ip-address-allow-list.md#gbr9-united-kingdom)Zulassungsliste). |
| Verbesserte Unterstützung für Change Data Capture | Sie können jetzt die Änderungsdatenerfassung mit den [!DNL Marketo Engage]-, [!DNL Microsoft Dynamics]- und [!DNL Salesforce CRM] verwenden. |
| Verbessertes Authentifizierungshandbuch für [[!DNL Google BigQuery]](../../sources/connectors/databases/bigquery.md) | Das Authentifizierungshandbuch für die [!DNL Google BigQuery] wurde um die folgenden Informationen erweitert: <ul><li>Die erforderlichen Bereiche für das Aktualisierungs-Token.</li><li>Die für die [!DNL Google] Identität erforderlichen IAM-Rollen.</li><li>Zusätzliche Anleitungen zur Verwendung von `largeResultsDataSetId`.</li></ul> |

{style="table-layout:auto"}

Weitere Informationen finden Sie unter [Quelle – Übersicht](../../sources/home.md).
