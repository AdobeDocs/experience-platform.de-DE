---
title: Adobe Experience Platform – Versionshinweise, September 2024
description: Versionshinweise September 2024 zu Adobe Experience Platform.
source-git-commit: eac613434f631cab567ab3fa6e30d33acac79d2f
workflow-type: tm+mt
source-wordcount: '2199'
ht-degree: 23%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: Mittwoch, 24. September 2024**

Aktualisierungen vorhandener Funktionen und Dokumentationen in Adobe Experience Platform:

- [Warnhinweise](#alerts)
- [Dashboards](#dashboards)
- [Datenvorbereitung](#data-prep)
- [Ziele](#destinations)
- [Experience-Datenmodell (XDM)](#xdm)
- [Identity Service](#identity-service)
- [Abfrage-Service](#query-service)
- [Segmentierungs-Service](#segmentation-service)
- [Quellen](#sources)

## Warnhinweise {#alerts}

Mit Experience Platform können Sie ereignisbasierte Warnhinweise zu Adobe Experience Platform-Aktivitäten abonnieren. Sie können unterschiedliche Warnhinweisregeln über die Registerkarte [!UICONTROL Warnhinweise] in der Platform-Benutzeroberfläche abonnieren. Zusätzlich können Sie auswählen, ob Warnhinweise in der Benutzeroberfläche oder über E-Mail-Benachrichtigungen angezeigt werden sollen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Unterstützung von Entwicklungs-Sandboxes | Sie können nun [Warnhinweise abonnieren](../../observability/alerts/ui.md) in Produktions- und Entwicklungs-Sandboxes, wodurch eine nahtlose Überwachung in allen Umgebungen ermöglicht wird. |
| E-Mail-Vorlagen | [E-Mail-Warnungen](../../observability/alerts/ui.md) enthalten jetzt detaillierte Asset-Informationen, um sicherzustellen, dass Sie alle wichtigen Details zur Hand haben. |
| Verbesserte Anpassung | Sie können jetzt [Warnschwellen](../../observability/alerts/ui.md#alert-threshold) konfigurieren, um Warnhinweise flexibler an Ihre spezifischen Anforderungen für die folgenden Warnhinweistypen anzupassen:<br><ul><li>Verzögerung bei Segmentvorgängen</li><li>Verzögerung beim Segmentexport</li><li>Verzögerung bei der Ausführung des Zielflusses</li><li>Verzögerung bei der Ausführung des Identity Service-Flusses</li><li>Verzögerung bei der Ausführung eines Profilflusses</li><li>Verzögerung bei der Ausführung von Quellen</li><li>Verzögerung der Abfrageausführung</li><li>Aktivierungsübersprungrate überschritten</li><li>Fehlerrate der Quellenaufnahme überschritten</ul> |
| Erweiterte Warnhinweise | Warnhinweise zu Audit-Ereignisinformationen stehen nun für die Anmeldung für die folgenden [Warnhinweisregeln](../../observability/alerts/rules.md) zur Verfügung:<br><ul><li>Zielgruppenerstellung</li><li>Zielgruppenaktualisierung</li><li>Zielgruppenlöschung</li><li>Datensatz erstellen</li><li>Datensatz-Update</li><li>Datensatz löschen</li><li>Schema erstellen</li><li>Schemaaktualisierung</li><li>Löschen von Schemas. |

{style="table-layout:auto"}

Weitere Informationen zu Warnhinweisen finden Sie in der [[!DNL Observability Insights] Übersicht](../../observability/home.md) .

## Dashboards {#dashboards}

Experience Platform bietet mehrere Dashboards, über die Sie wichtige Einblicke in die Daten Ihres Unternehmens erhalten, wie sie bei täglichen Momentaufnahmen erfasst werden.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Tabelle mit Add-ons zur Lizenznutzung | Erhalten Sie detaillierte Einblicke in die Lizenznutzung und verwalten Sie Ihre Platform-Ressourcen mit dedizierten Tabellen für Hauptprodukte und Add-ons. Verfolgen und analysieren Sie Schlüsselmetriken für jedes Kernprodukt mit Durchlaufansichten auf Sandbox-Ebene. Add-on-Metriken lassen sich nahtlos in die Kernproduktmetriken integrieren und bieten einen umfassenden Überblick über die Verwendung. Verbesserte Sichtbarkeit hilft Ihnen, die Lizenzverwaltung zu optimieren und Ressourcen an die organisatorischen Anforderungen anzupassen. Weitere Informationen finden Sie im Dashboard-Handbuch [[!UICONTROL Lizenznutzung]](../../dashboards/guides/license-usage.md#overview-tab) . |
| Query Pro Mode - Aktualisierung globaler Filter | Verbessern Sie die Analyse mit dem neuen Datumsfilter von Query Pro Mode. Präzisieren Sie Einblicke mit dynamischen Datumsparametern in Ihren SQL-Abfragen und filtern Sie Daten nach bestimmten Zeitrahmen. Wählen Sie vordefinierte oder benutzerdefinierte Datumsbereiche mit einer intuitiven Benutzeroberfläche aus, in denen Dashboards für alle Benutzer relevant bleiben. Vereinfachung der Workflows, Gewährleistung der Genauigkeit und rechtzeitige Entscheidungsfindung. Weitere Informationen finden Sie im [Handbuch zum Erstellen von Datumsfiltern](../../dashboards/sql-insights-query-pro-mode/filters/global-filter.md) . |
| Query Pro-Modi - Durchgänge | Machen Sie sich mit der Drill Through-Funktion von Query Pro Mode mit tieferen Einblicken vertraut und navigieren Sie nahtlos von Diagrammen auf hoher Ebene zu detaillierten Dashboards. Verwenden Sie diese Funktion, um mühelos von Zusammenfassungen zu einer eingehenden Analyse zu wechseln und Trends, Kundenverhalten und KPIs zu untersuchen. Automatische Filterdurchgänge und mehrstufige Durchsuchen von Durchgängen halten die Daten konsistent und sorgen so für eine reibungslose Exploration. Vereinfachen Sie Workflows, behalten Sie den Kontext und beschleunigen Sie Entscheidungen. Weitere Informationen finden Sie im Schritt-für-Schritt-Handbuch [ zum Erstellen von Drillthroughs](../../dashboards/sql-insights-query-pro-mode/drill-through.md) . |
| Query Pro Mode - Erweiterte Tabellenattribute | Verwenden Sie erweiterte Tabellenattribute des Query Pro-Modus, um die Datenvisualisierung zu optimieren, die Workflow-Effizienz zu steigern und die Datenübersicht zu verbessern. Fügen Sie Ihren Tabellen direkt aus benutzerdefinierten Dashboards automatische Sortierung, Größenanpassung und Paginierung hinzu. Sortieren Sie Spalten, um Schlüsseldaten zu priorisieren, die Größe für eine optimale Lesbarkeit zu ändern und durch große Datensätze zu navigieren, ohne SQL-Abfragen zu ändern. Lesen Sie das Handbuch &quot;[Mehr anzeigen](../../dashboards/sql-insights-query-pro-mode/view-more.md)&quot;, um zu erfahren, wie Sie diese Funktionen integrieren und Ihre Dateneinblicke verbessern können. |
| Datenvolumen insgesamt | Die Metrik &quot;Durchschnittliche Profilreichweite&quot;wurde durch die Metrik &quot;Datenvolumen insgesamt&quot;ersetzt. Gesamtdatenvolumen bezieht sich auf die Gesamtanzahl der verfügbaren Daten, die mit dem Echtzeit-Kundenprofil für Interaktions- und Personalisierungs-Workflows verwendet werden können. Weitere Informationen zu dieser Änderung finden Sie im Handbuch [Datenvolumen insgesamt](../../landing/license-usage-and-guardrails/total-data-volume.md) . |

{style="table-layout:auto"}

Weitere Informationen zu Dashboards, einschließlich der Gewährung von Zugriffsberechtigungen und der Erstellung benutzerdefinierter Widgets, finden Sie in der [Übersicht über Dashboards](../../dashboards/home.md).

## Datenvorbereitung {#data-prep}

Verwenden Sie die Datenvorbereitung zum Zuordnen, Transformieren und Überprüfen von Daten zum Experience-Datenmodell (XDM) und aus ihm.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| [!BADGE Beta]{type=informative} Neue Datenvorgabenfunktionen zur Verwendung in Zielen | Sie können jetzt die folgenden Array-Funktionen für Anwendungsfälle mit Zielen verwenden:<ul><li>`array_to_string`</li><li>`filterArray`</li><li>`transformArray`</li><li>`flattenArray`</li></ul> Weitere Informationen finden Sie im Leitfaden für die [Datenvorbereitung-Funktionen](../../data-prep/functions.md#arrays). |

{style="table-layout:auto"}

Weitere Informationen zur Datenvorbereitung finden Sie in der [Datenvorbereitung - Übersicht](../../data-prep/home.md) .

## Ziele {#destinations}

**Aktualisiert: 30. September 2024**

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Ziele** {#new-updated-destinations}

| Ziel | Beschreibung |
| --- | --- |
| [Amazon Ads](/help/destinations/catalog/advertising/amazon-ads.md) | In der Version vom September 2024 wurde die Zuordnungsoption hinzugefügt, mit der der Parameter `countryCode` in Amazon Ads exportiert werden kann. Verwenden Sie `countryCode` im Schritt [Zuordnen](/help/destinations/catalog/advertising/amazon-ads.md#map) , um Ihre Identitätsübereinstimmungsraten mit Amazon zu verbessern. |
| [[!BADGE B2B]{type=informative} Demandbase](/help/destinations/catalog/advertising/demandbase.md) | Verwenden Sie dieses Ziel, um Ihre Zielgruppen für Account-Based Marketing (ABM) zu aktivieren. Werben Sie über die B2B-Demand Side Platform (DSP) von DemandBase an relevante Personen und Rollen in Ihren Zielkonten. Target-Konten können auch mit Demandbase-Drittanbieterdaten angereichert werden, um sie für andere nachgelagerte Anwendungsfälle in Marketing und Vertrieb nutzen zu können. |

{style="table-layout:auto"}

**Neue oder aktualisierte Funktionen** {#destinations-new-updated-functionality}

| Funktion | Beschreibung |
| --- | --- |
| Verbesserungen beim [Datensatzexport](/help/destinations/ui/export-datasets.md) | Die Experience Platform-Version vom September 2024 enthält mehrere Verbesserungen an den Funktionen der Datensatzexport-Funktion, um verschiedene Anwendungsfälle für Datenaussendungen besser zu unterstützen. Zu diesen Funktionsverbesserungen gehören: <ul><li>Neue Konfigurationsoptionen für Datenordner, einschließlich der Option zum Hinzufügen und Entfernen von Unterordnern.</li><li>Neue Exportoptionen, einschließlich des vollständigen Dateiexports (einmal) und der Möglichkeit, Enddaten anzugeben</li><li>Hinweis: Adobe führt auch das standardmäßige Enddatum 1. Mai 2025 für alle Datenfluss-Datenflüsse ein, die vor der September-Version erstellt wurden. Für jeden dieser Datenflüsse müssen Kunden das Enddatum im Datenfluss manuell vor dem Enddatum aktualisieren. Andernfalls werden die Exporte an diesem Datum beendet.</li></ul> <br> ![Bild der Experience Platform-Benutzeroberfläche, das die Option Zeitplan und Ordner bearbeiten im Planungsschritt hervorhebt.](../2024/assets/september/edit-schedule-folders.png "Bearbeiten Sie die Option Zeitplan und Ordner im Planungsschritt."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

Lesen Sie für Weitere Informationen den [Überblick über die Ziele](../../destinations/home.md).

## Experience-Datenmodell (XDM) {#xdm}

XDM ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen (Schemata) für Daten bereitstellt, die in Adobe Experience Platform importiert werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Verbesserungen am Schema-Editor | Übernehmen Sie die Kontrolle über Ihre Schemabeziehungen mit einem aktualisierten Beziehungs-Workflow im Schema Editor. Einfaches Aktualisieren oder Entfernen vorhandener Beziehungen direkt über die Experience Platform-Benutzeroberfläche, wodurch die Schemaverwaltung einfacher und intuitiver wird. Passen Sie Referenzschemata an und benennen Sie Beziehungen vertrauensvoll um, um eine nahtlose Datenintegrität bei der Segmentierung und anderen wichtigen Prozessen zu gewährleisten. Weitere Informationen zur effizienten Verwaltung Ihrer Schemabeziehungen finden Sie in den Handbüchern zum [Definieren von Beziehungsfeldern in der Benutzeroberfläche](../../xdm/tutorials/relationship-ui.md#create-a-relationship-field-group) und zu [B2B-Beziehungen](../../xdm/tutorials/relationship-b2b.md#edit-a-b2b-schema-relationship) . |

{style="table-layout:auto"}

Weitere Informationen zu XDM finden Sie in der [XDM-Systemübersicht](../../xdm/home.md).

## Identity Service {#identity-service}

Verwenden Sie den Adobe Experience Platform Identity Service, um sich einen besseren Überblick über Ihre Kundinnen und Kunden und deren Verhaltensweisen zu verschaffen, indem Identitäten geräte- und systemübergreifend zusammengeführt werden. So können Sie in Echtzeit für eindrucksvolle und persönliche digitale Erlebnisse sorgen.

**Aktualisierte Funktion**

| Funktion | Beschreibung |
| --- | --- |
| Eingeschränkte Verfügbarkeit von Verknüpfungsregeln für Identitätsdiagramme | Die Regeln zur Verknüpfung von Identitätsdiagrammen sind eine Suite von Tools im Identity Service, die Sie verwenden können, um eine genaue Personalisierung für Ihre Benutzer sicherzustellen. <ul><li>Sie können jetzt den [Identitätsoptimierungsalgorithmus](../../identity-service/identity-graph-linking-rules/identity-optimization-algorithm.md) verwenden, um sicherzustellen, dass ein Identitätsdiagramm für eine einzelne Person repräsentativ ist, und somit die unerwünschte Zusammenführung von Identitäten mit dem Echtzeit-Kundenprofil verhindert.</li><li>Konfigurieren Sie [Namespace-Prioritäten](../../identity-service/identity-graph-linking-rules/namespace-priority.md) , um die Wichtigkeit Ihrer jeweiligen Namespaces zu definieren und zu beeinflussen, wie Ihre Profile gebildet und segmentiert werden.</li><li>Verwenden Sie das [Graph-Simulationstool in der Benutzeroberfläche](../../identity-service/identity-graph-linking-rules/graph-simulation.md), um Identitätsdiagramme mit unterschiedlichen Konfigurationen zu simulieren.</li><li>Verwenden Sie die [Benutzeroberfläche für Identitätseinstellungen](../../identity-service/identity-graph-linking-rules/identity-settings-ui.md), um Ihren eindeutigen Namespace zu bestimmen und Prioritäten für alle Namespaces in Ihrer Organisation festzulegen.</li><li>Metriken und Trends zu Ihren Diagrammdaten finden Sie im [Identitäts-Dashboard](../../identity-service/identity-graph-linking-rules/implementation-guide.md#validate-your-graphs) .</li></ul> Wenden Sie sich an Ihr Adobe-Account-Team, um Zugriff auf Entwicklungs-Sandboxes zu erhalten, um die Verknüpfungsregeln für Identitätsdiagramme auszuprobieren. |

**Aktualisierte Dokumentation**

| Funktion | Beschreibung |
| --- | --- |
| Fehlerbehebungshandbuch für Regeln zur Identitätsdiagrammzuordnung | Lesen Sie das neue [Handbuch zur Fehlerbehebung für Regeln zur Zuordnung von Identitätsdiagrammen](../../identity-service/identity-graph-linking-rules/troubleshooting.md) für Ansätze und Debugging-Lösungen, die Sie zur Lösung häufiger Probleme einsetzen können, auf die Sie beim Arbeiten mit Regeln zur Identitätsdiagrammzuordnung stoßen können. |
| Häufig gestellte Fragen zu Regeln zur Identitätsdiagrammzuordnung | Lesen Sie die neuen FAQ](../../identity-service/identity-graph-linking-rules/troubleshooting.md#frequently-asked-questions) zur [Identitätsdiagramm-Verknüpfungsregeln für eine Liste der Antworten auf häufig gestellte Fragen zur Namespace-Priorität, zum Identitätsoptimierungsalgorithmus und anderen Facetten von Regeln zur Identitätsdiagrammzuordnung. |

{style="table-layout:auto"}

Weiterführende Informationen zu Identity Service finden Sie in der [Übersicht zu Identity Service](../../identity-service/home.md).

## Query Service {#query-service}

Query Service ermöglicht Ihnen die Verwendung von Standard-SQL zur Abfrage von Daten in Adobe Experience Platform [!DNL data lake]. Sie können beliebige Datensätze aus dem Data Lake verbinden und die Abfrageergebnisse als neuen Datensatz für die Verwendung in Berichten, im Datenwissenschafts-Arbeitsbereich oder für die Aufnahme in das Echtzeit-Kundenprofil verwenden.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Data Distiller Audiences | Einfaches Erstellen, Verwalten und Aktivieren von Zielgruppen mit der SQL-Zielgruppenerweiterung in Experience Platform Data Distiller. Definieren Sie Zielgruppensegmente mit SQL-Befehlen direkt aus Ihrem Data Lake, ohne dass Rohdaten in Profilen benötigt werden. Verfeinern Sie Zielgruppenstrategien und synchronisieren Sie Zielgruppen automatisch mit dateibasierten Zielen mit diesem flexiblen, datengesteuerten Ansatz. Optimierung von Workflows, Optimierung des Zielgruppen-Managements und Erschließung des vollen Potenzials von Daten. Lesen Sie das [Handbuch zur Verwendung der SQL-Zielgruppenerweiterung](../../query-service/data-distiller-audiences/overview.md), um Ihre Zielgruppenstrategien zu verbessern. |
| Data Distiller Statistics - Hyperwürfel | Optimieren Sie die Big-Data-Analyse mit Hyperwürfeln. Komplexe Berechnungen - wie eindeutige Zählungen und mehrdimensionale Analysen - ohne die historischen Daten erneut zu verarbeiten. Inkrementelle Aktualisierung von Daten, Optimierung von Workflows und Verkürzung der Verarbeitungszeit unter Beibehaltung von Genauigkeit und Effizienz. Erhalten Sie schnellere, skalierbare und kostengünstige Einblicke, die die Entscheidungsfindung verändern. Lesen Sie das [Handbuch zur Verwendung von Hyperwürfen](../../query-service/hypercubes/overview.md) , um die erweiterte Analyse zu entsperren. |
| Objekt-Browser des Abfrage-Editors | Verbessern der Abfrageleistung mit dem neuen Objektbrowser im Abfrage-Editor. Schnelles Suchen, Filtern und Aufrufen von Datensätzen, um Abfragen schneller zu schreiben und zu verfeinern. Mit Echtzeit-Schemaaktualisierungen und Instant-Tabellen-Metadaten können Sie Workflows optimieren, die Navigationszeit verkürzen und Ihr Abfrageerlebnis verbessern. Erschließen Sie das Potenzial Ihrer Daten und optimieren Sie die Analyse. Weitere Informationen finden Sie im [Handbuch zur Verwendung des Objektbrowsers](../../query-service/ui/user-guide.md#object-browser) . |
| Berechnungsstunden | Gewinnen Sie Kontrolle über die Ressourcennutzung mit der neu sichtbaren Metrik &quot;Compute Hours&quot;für geplante Abfragen. Zeigen Sie die Ausführungszeiten der Abfrage an, um die Ressourcenverwendung für CTAS/ITAS-Batch-Abfragen zu überwachen und zu optimieren. Verfolgen Sie Startzeiten, Abschlussstatus und die Berechnungszeit für jeden Abfrageablauf. Optimieren Sie die Leistung und reduzieren Sie die Kosten mühelos. Informationen zur Maximierung Ihrer Abfrageeffizienz finden Sie im [Handbuch zu Compute Hours](../../query-service/ui/query-schedules.md#compute-hours-at-job-level) . |

{style="table-layout:auto"}

Weitere Informationen zu Query Service finden Sie in der [Query Service - Übersicht](../../query-service/home.md) .

## Segmentierungs-Service {#segmentation-service}

[!DNL Segmentation Service] definiert eine bestimmte Untergruppe von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Segmente können auf Datensatzdaten (z. B. demografische Daten) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Aktualisierung der Streaming-Segmentierungskriterien | Ab der Version vom September 2024 wurden die Kriterien für Ihre Zielgruppen aktualisiert, die für Streaming-Segmentierung infrage kommen. Weitere Informationen zu diesen Änderungen finden Sie im Update der [Eignungskriterien für Streaming-Segmentierung](../../segmentation/eligibility-criteria-update.md) . |
| Einheitliche Suchimplementierung | Das Suchverhalten in Segment Builder verwendet jetzt die einheitliche Suche. Dies ermöglicht ein robusteres Erlebnis bei der Verwaltung und Suche nach Zielgruppen, die für die Segmentzugehörigkeit wiederverwendet werden können. Weitere Informationen zu dieser Änderung finden Sie im [Segment Builder-Handbuch](../../segmentation/ui/segment-builder.md#rule-builder-canvas). |

{style="table-layout:auto"}

Weitere Informationen zu [!DNL Segmentation Service] finden Sie in der [Segmentierungsübersicht](../../segmentation/home.md).

## Quellen {#sources}

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

Verwenden Sie Quellen in Experience Platform, um Daten aus einer Adobe-Anwendung oder einer Datenquelle von Drittanbietern aufzunehmen.

**Aktualisierte Funktion**

| Funktion | Beschreibung |
| --- | --- |
| [!BADGE Beta]{type=Informative} Unterstützung für die verschlüsselte Datenerfassung in der Benutzeroberfläche | Sie können jetzt verschlüsselte Daten aus einer Cloud-Speicher-Batch-Quelle über den Arbeitsbereich &quot;Quellen&quot;in der Experience Platform-Benutzeroberfläche erfassen. Weitere Informationen finden Sie im Tutorial zum [ Erfassen verschlüsselter Daten in der Benutzeroberfläche](../../sources/tutorials/ui/encryped-ingestion.md) . |
| Allgemeine Verfügbarkeit der [!DNL Snowflake Streaming]-Quelle | Die Quelle [!DNL Snowflake Streaming] befindet sich jetzt in GA. Verwenden Sie diese Quelle, um Daten von Ihrem [!DNL Snowflake]-Konto an Experience Platform zu streamen. Weitere Informationen finden Sie in der [[!DNL Snowflake Streaming] Übersicht](../../sources/connectors/databases/snowflake-streaming.md) . |
| Unterstützung für die Authentifizierung von Dienstkonten in [!DNL Google BigQuery] | Sie können jetzt Ihr [!DNL Google BigQuery]-Konto mit der Experience Platform über die Authentifizierung des Dienstkontos mit dem verbinden. Weitere Informationen finden Sie in der [[!DNL Google BigQuery] Übersicht](../../sources/connectors/databases/bigquery.md#generate-your-google-bigquery-credentials) . <br> ![Bild der Experience Platform-Benutzeroberfläche, das die Option Zeitplan und Ordner bearbeiten im Planungsschritt hervorhebt.](../2024/assets/september/service_auth.png "Dienstauthentifizierung für Google BigQuery."){width="250" align="center" zoomable="yes"} |
| Unterstützung für das Überspringen der Beispieldatenvorschau | Sie können jetzt die Datenvorschau bei der Erstellung einer Quellverbindung mit den folgenden Quellen überspringen: <ul><li>[[!DNL Google BigQuery]](../../sources/tutorials/ui/create/databases/bigquery.md#skip-preview-of-sample-data)</li><li>[[!DNL Salesforce]](../../sources/tutorials/ui/create/crm/salesforce.md#skip-preview-of-sample-data)</li><li>[[!DNL Snowflake]](../../sources/tutorials/ui/create/databases/snowflake.md#skip-preview-of-sample-data)</li></ul> Sie können die Datenvorschau überspringen, um eine Zeitüberschreitung zu umgehen, die bei der Aufnahme großer Batch-Daten auftreten kann. Dies kann die automatische Validierung Ihrer berechneten und erforderlichen Felder verhindern. Wenn Sie die Datenvorschau überspringen möchten, müssen Sie Ihre berechneten und erforderlichen Felder möglicherweise während der Zuordnung manuell validieren. |
| Unterstützung für die Deaktivierung des Blockierens in [!DNL SFTP] | Sie können jetzt eine Einstellung konfigurieren, mit der Sie die Blockierung in der Quelle [!DNL SFTP] deaktivieren können. Weitere Informationen finden Sie in der [[!DNL SFTP] Übersicht](../../sources/connectors/cloud-storage/sftp.md) . |

{style="table-layout:auto"}

Weitere Informationen finden Sie unter [Quelle – Übersicht](../../sources/home.md).
