---
title: Adobe Experience Platform – Versionshinweise, September 2024
description: Versionshinweise September 2024 zu Adobe Experience Platform.
exl-id: e5b40712-2a54-4c6f-a4a1-2f078305da59
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2202'
ht-degree: 21%

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

Mit Experience Platform können Sie ereignisbasierte Warnhinweise für verschiedene Experience Platform-Aktivitäten abonnieren. Sie können unterschiedliche Warnhinweisregeln über die Registerkarte [!UICONTROL Warnhinweise] in der Benutzeroberfläche von Experience Platform abonnieren. Zusätzlich können Sie auswählen, ob Warnhinweise in der Benutzeroberfläche oder über E-Mail-Benachrichtigungen angezeigt werden sollen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Unterstützung von Entwicklungs-Sandboxes | Sie können jetzt [Warnhinweise abonnieren](../../observability/alerts/ui.md) sowohl in Produktions- als auch in Entwicklungs-Sandboxes, was eine nahtlose Überwachung über alle Umgebungen hinweg ermöglicht. |
| E-Mail-Vorlagen | [E-Mail](../../observability/alerts/ui.md)Warnungen enthalten jetzt detaillierte Asset-Informationen, um sicherzustellen, dass Sie alle wichtigen Details griffbereit haben. |
| Verbesserte Anpassung | Sie können jetzt [Warnhinweisschwellen](../../observability/alerts/ui.md#alert-threshold) konfigurieren, um Warnhinweise für die folgenden Warnhinweistypen flexibler an Ihre spezifischen Anforderungen anzupassen:<br><ul><li>Verzögerung bei Segmentvorgängen</li><li>Verzögerung beim Segmentexport</li><li>Verzögerung bei der Ausführung des Zielflusses</li><li>Verzögerung bei der Ausführung des Identity Service-Flusses</li><li>Verzögerung bei der Ausführung eines Profilflusses</li><li>Verzögerung bei Flussausführung an der Quelle</li><li>Verzögerung der Abfrageausführung</li><li>Aktivierungsüberspringrate überschritten</li><li>Fehlerrate bei der Quellaufnahme überschritten</ul> |
| Erweiterte Warnhinweise | Audit-Ereignisinformationen-Warnhinweise sind jetzt für die folgenden [Warnhinweisregeln](../../observability/alerts/rules.md) zum Abonnieren verfügbar:<br><ul><li>Zielgruppe erstellen</li><li>Zielgruppen-Update</li><li>Audience löschen</li><li>Datensatz erstellen</li><li>Datensatzaktualisierung</li><li>Löschen eines Datensatzes</li><li>Schema erstellen</li><li>Schema-Aktualisierung</li><li>Löschen des Schemas. |

{style="table-layout:auto"}

Weitere Informationen zu Warnhinweisen finden Sie im Abschnitt [[!DNL Observability Insights] Übersicht](../../observability/home.md).

## Dashboards {#dashboards}

Experience Platform bietet mehrere Dashboards, in denen Sie wichtige Einblicke in die Daten Ihres Unternehmens erhalten, die in täglichen Schnappschüssen erfasst werden.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Tabelle mit Lizenznutzungs-Add-ons | Detaillierte Einblicke in die Lizenznutzung und die Verwaltung Ihrer Experience Platform-Ressourcen mit speziellen Tabellen für Kernprodukte und Add-ons. Verfolgen und analysieren Sie Schlüsselmetriken für jedes Kernprodukt mit Drill-Through-Ansichten auf Sandbox-Ebene. Add-on-Metriken lassen sich nahtlos mit Kernproduktmetriken integrieren und bieten eine umfassende Übersicht über die Nutzung. Durch die verbesserte Transparenz können Sie die Lizenzverwaltung optimieren und die Ressourcen an den Anforderungen Ihres Unternehmens ausrichten. Weitere Informationen finden Sie [[!UICONTROL &#x200B; Handbuch zum Dashboard &#x200B;]Lizenznutzung](../../dashboards/guides/license-usage.md#overview-tab) . |
| Query Pro-Modus - Aktualisierungen des globalen Filters | Verbessern Sie die Analyse mit dem neuen Datumsfilter von Query Pro Mode. Verfeinern Sie Insights mit dynamischen Datumsparametern in Ihren SQL-Abfragen und filtern Sie Daten nach bestimmten Zeitrahmen. Wählen Sie voreingestellte oder benutzerdefinierte Datumsbereiche mit einer intuitiven Benutzeroberfläche aus, damit Dashboards für alle Benutzer relevant sind. Vereinfachen Sie Workflows, halten Sie die Präzision aufrecht und treffen Sie zeitnahe Entscheidungen. Weitere Informationen finden [ im Handbuch ](../../dashboards/sql-insights-query-pro-mode/filters/global-filter.md) Erstellen von Datumsfiltern . |
| Abfrage-PRO-Modi - Drill-Throughs | Erhalten Sie tiefere Einblicke mit der Drill-Through-Funktion von Query Pro Mode und navigieren Sie nahtlos von allgemeinen Diagrammen zu detaillierten Dashboards. Verwenden Sie diese Funktion, um mühelos von Zusammenfassungen zu einer eingehenden Analyse zu wechseln und Trends, Kundenverhalten und KPIs zu untersuchen. Automatische Filter-Passthroughs und Drill-throughs mit mehreren Ebenen sorgen für konsistente Daten und sorgen für eine reibungslose Exploration. Vereinfachen Sie Workflows, behalten Sie den Kontext und beschleunigen Sie Entscheidungen. Weitere Informationen finden [ im „Schritt-für-Schritt-Handbuch zum Erstellen ](../../dashboards/sql-insights-query-pro-mode/drill-through.md) Drill-Throughs“ . |
| Query Pro-Modus - Erweiterte Tabellenattribute | Verwenden Sie erweiterte Tabellenattribute im Query Pro-Modus, um die Datenvisualisierung zu optimieren, die Workflow-Effizienz zu verbessern und die Datenklarheit zu verbessern. Fügen Sie den Tabellen automatische Sortierung, Größenanpassung und Paginierung direkt über benutzerdefinierte Dashboards hinzu. Sortieren Sie Spalten, um Schlüsseldaten zu priorisieren, die Größe zu ändern, um eine optimale Lesbarkeit zu gewährleisten, und navigieren Sie nahtlos in großen Datensätzen, ohne SQL-Abfragen zu ändern. Lesen Sie das Handbuch [Mehr anzeigen](../../dashboards/sql-insights-query-pro-mode/view-more.md), um zu erfahren, wie Sie diese Funktionen integrieren und Ihre Dateneinblicke verbessern können. |
| Gesamtdatenvolumen | Die Metrik „Durchschnittlicher Profilreichhaltigkeitsgrad“ wurde durch die Metrik „Gesamtdatenvolumen“ ersetzt. Das Gesamtdatenvolumen bezieht sich auf die Gesamtmenge der verfügbaren Daten, die mit dem Echtzeit-Kundenprofil für Interaktions- und Personalisierungs-Workflows verwendet werden kann. Weitere Informationen zu dieser Änderung finden Sie im [Handbuch zum Datenvolumen insgesamt](../../landing/license-usage-and-guardrails/total-data-volume.md). |

{style="table-layout:auto"}

Weitere Informationen zu Dashboards, einschließlich der Gewährung von Zugriffsberechtigungen und der Erstellung benutzerdefinierter Widgets, finden Sie in der [Übersicht über Dashboards](../../dashboards/home.md).

## Datenvorbereitung {#data-prep}

Verwenden Sie die Datenvorbereitung zum Zuordnen, Transformieren und Validieren von Daten in und aus dem Experience-Datenmodell (XDM).

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| [!BADGE Beta]{type=Informative} Neue Datenvorbereitungsfunktionen zur Verwendung in Zielen | Sie können jetzt die folgenden Array-Funktionen für Anwendungsfälle für Ziele verwenden:<ul><li>`array_to_string`</li><li>`filterArray`</li><li>`transformArray`</li><li>`flattenArray`</li></ul> Weitere Informationen finden Sie im [Handbuch zu Datenvorbereitungsfunktionen](../../data-prep/functions.md#arrays). |

{style="table-layout:auto"}

Weitere Informationen zur Datenvorbereitung finden Sie unter [Datenvorbereitung - Übersicht](../../data-prep/home.md).

## Ziele {#destinations}

**Aktualisiert: 30. September 2024**

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Ziele** {#new-updated-destinations}

| Ziel | Beschreibung |
| --- | --- |
| [Amazon-Anzeigen](/help/destinations/catalog/advertising/amazon-ads.md) | In der Version vom September 2024 wird die Zuordnungsoption zum Exportieren des `countryCode` in Amazon Ads hinzugefügt. Verwenden Sie `countryCode` im [Zuordnungsschritt](/help/destinations/catalog/advertising/amazon-ads.md#map) um die Übereinstimmungsraten Ihrer Identitäten mit Amazon zu verbessern. |
| [[!BADGE B2B]{type=Informative} Demandbase](/help/destinations/catalog/advertising/demandbase.md) | Verwenden Sie dieses Ziel, um Ihre Konto-Zielgruppen für Account-Based Marketing-Anwendungsfälle (ABM) zu aktivieren. Werben Sie über die B2B-Demand Side Platform (DSP) von DemandBase für relevante Personas und Rollen in Ihren Zielkonten. Zielkonten können auch mit Demandbase-Drittanbieterdaten für andere nachgelagerte Anwendungsfälle in Marketing und Vertrieb angereichert werden. |

{style="table-layout:auto"}

**Neue oder aktualisierte Funktionen** {#destinations-new-updated-functionality}

| Funktion | Beschreibung |
| --- | --- |
| Verbesserungen [Datensatzexport](/help/destinations/ui/export-datasets.md) | Die Experience Platform-Version vom September 2024 enthält mehrere Verbesserungen der Funktionen für den Datensatzexport, um verschiedene Anwendungsfälle für Datenausgänge besser zu unterstützen. Zu diesen Funktionsverbesserungen gehören: <ul><li>Neue Konfigurationsoptionen für Datenordner, einschließlich der Option zum Hinzufügen und Entfernen von Unterordnern.</li><li>Neue Exportoptionen, einschließlich vollständiger Dateiexport (einmal) und der Möglichkeit, Enddaten anzugeben</li><li>Hinweis: Adobe führt auch das standardmäßige Enddatum 1. Mai 2025 für alle Datensatzexport-Datenflüsse ein, die vor der September-Version erstellt wurden. Für jeden dieser Datenflüsse müssen Kunden das Enddatum im Datenfluss vor dem Enddatum manuell aktualisieren, da die Exporte sonst an diesem Datum anhalten.</li></ul> <br> ![Abbildung der Experience Platform-Benutzeroberfläche mit hervorgehobener Option „Zeitplan und Ordner bearbeiten“ im Planungsschritt.](../2024/assets/september/edit-schedule-folders.png "Option „Zeitplan und Ordner bearbeiten“ im Planungsschritt."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

Lesen Sie für Weitere Informationen den [Überblick über die Ziele](../../destinations/home.md).

## Experience-Datenmodell (XDM) {#xdm}

XDM ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen (Schemata) für Daten bereitstellt, die in Adobe Experience Platform importiert werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Verbesserungen am Schema-Editor | Übernehmen Sie die Kontrolle über Ihre Schemabeziehungen mit einem aktualisierten Beziehungs-Workflow im Schema-Editor. Einfaches Aktualisieren oder Entfernen vorhandener Beziehungen direkt über die Experience Platform-Benutzeroberfläche, wodurch die Schemaverwaltung reibungsloser und intuitiver wird. Passen Sie Referenzschemata an und benennen Sie Beziehungen mit Konfidenz um, um eine nahtlose Datenintegrität über Segmentierungen und andere wichtige Prozesse hinweg sicherzustellen. Weitere Informationen zur effizienten Verwaltung Ihrer Schemabeziehungen finden Sie in den Handbüchern unter [Definieren von Beziehungsfeldern in der Benutzeroberfläche](../../xdm/tutorials/relationship-ui.md#create-a-relationship-field-group) und für [B2B-Beziehungen](../../xdm/tutorials/relationship-b2b.md#edit-a-b2b-schema-relationship). |

{style="table-layout:auto"}

Weitere Informationen zu XDM finden Sie in der [XDM-Systemübersicht](../../xdm/home.md).

## Identity Service {#identity-service}

Verwenden Sie den Adobe Experience Platform Identity Service, um sich einen besseren Überblick über Ihre Kundinnen und Kunden und deren Verhaltensweisen zu verschaffen, indem Identitäten geräte- und systemübergreifend zusammengeführt werden. So können Sie in Echtzeit für eindrucksvolle und persönliche digitale Erlebnisse sorgen.

**Aktualisierte Funktion**

| Funktion | Beschreibung |
| --- | --- |
| Eingeschränkte Verfügbarkeit von Regeln zur Identitätsdiagramm-Verknüpfung | Verknüpfungsregeln für Identitätsdiagramme sind eine Suite von Tools in Identity Service, mit denen Sie eine genaue Personalisierung für Ihre Benutzer sicherstellen können. <ul><li>Sie können jetzt den Algorithmus [Identitätsoptimierung) verwenden, ](../../identity-service/identity-graph-linking-rules/identity-optimization-algorithm.md) sicherzustellen, dass ein Identitätsdiagramm für eine einzelne Person repräsentativ ist, und daher die unerwünschte Zusammenführung von Identitäten im Echtzeit-Kundenprofil zu verhindern.</li><li>Konfigurieren Sie [Namespace-](../../identity-service/identity-graph-linking-rules/namespace-priority.md), um die Bedeutung Ihrer jeweiligen Namespaces zu definieren und die Art und Weise zu beeinflussen, wie Ihre Profile gebildet und segmentiert werden.</li><li>Verwenden Sie das [Graphsimulations-Tool in der Benutzeroberfläche](../../identity-service/identity-graph-linking-rules/graph-simulation.md) um Identitätsdiagramme mit unterschiedlichen Konfigurationen zu simulieren.</li><li>Verwenden Sie die [Benutzeroberfläche für Identitätseinstellungen](../../identity-service/identity-graph-linking-rules/identity-settings-ui.md) um Ihren eindeutigen Namespace festzulegen und Prioritäten für alle Namespaces in Ihrer Organisation festzulegen.</li><li>Im [Identitäts-Dashboard](../../identity-service/identity-graph-linking-rules/implementation-guide.md#validate-your-graphs) finden Sie Metriken und Trends zu Ihren Diagrammdaten.</li></ul> Wenden Sie sich an Ihr Adobe-Accountteam, um Zugriff auf Entwicklungs-Sandboxes zu erhalten, um die Regeln zur Verknüpfung von Identitätsdiagrammen auszuprobieren. |

**Aktualisierte Dokumentation**

| Funktion | Beschreibung |
| --- | --- |
| Handbuch zur Fehlerbehebung bei Regeln für die Verknüpfung von Identitätsdiagrammen | Lesen Sie das neue [Handbuch zur Fehlerbehebung bei Regeln für die Verknüpfung von Identitätsdiagrammen](../../identity-service/identity-graph-linking-rules/troubleshooting.md), um Ansätze und Debugging-Lösungen für die Lösung gängiger Probleme zu finden, auf die Sie bei der Arbeit mit Regeln für die Verknüpfung von Identitätsdiagrammen stoßen können. |
| Häufig gestellte Fragen zu Regeln für die Verknüpfung von Identitätsdiagrammen | Lesen Sie die [ FAQ zu Identitätsdiagramm](../../identity-service/identity-graph-linking-rules/troubleshooting.md#frequently-asked-questions)Verknüpfungsregeln , um eine Liste von Antworten auf häufig gestellte Fragen zur Namespace-Priorität, zum Identitätsoptimierungsalgorithmus und zu anderen Facetten von Regeln zur Identitätsdiagramm-Verknüpfung zu erhalten. |

{style="table-layout:auto"}

Weiterführende Informationen zu Identity Service finden Sie in der [Übersicht zu Identity Service](../../identity-service/home.md).

## Query Service {#query-service}

Query Service ermöglicht Ihnen die Verwendung von Standard-SQL zur Abfrage von Daten in Adobe Experience Platform [!DNL data lake]. Sie können beliebige Datensätze aus dem Data Lake verbinden und die Abfrageergebnisse als neuen Datensatz für die Verwendung in Berichten, im Datenwissenschafts-Arbeitsbereich oder für die Aufnahme in das Echtzeit-Kundenprofil verwenden.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Daten-Distiller-Zielgruppen | Einfaches Erstellen, Verwalten und Aktivieren von Zielgruppen mit der SQL-Zielgruppenerweiterung in Experience Platform Data Distiller. Definieren Sie Zielgruppensegmente mit SQL-Befehlen direkt aus Ihrem Data Lake, wobei die Notwendigkeit von Rohdaten in Profilen umgangen wird. Verfeinern Sie Zielgruppenbestimmungsstrategien und synchronisieren Sie Zielgruppen automatisch mit dateibasierten Zielen mit diesem flexiblen, datengesteuerten Ansatz. Optimieren Sie Workflows, optimieren Sie die Verwaltung von Audiences und erschließen Sie das volle Potenzial von Daten. Lesen Sie das [Handbuch zur Verwendung der SQL-Zielgruppenerweiterung](../../query-service/data-distiller-audiences/overview.md), um Ihre Zielgruppenstrategien zu verbessern. |
| Data Distiller-Statistiken - Hypercubes | Optimieren Sie die Big-Data-Analyse mit Hypercubes. Komplexe Berechnungen - wie eindeutige Zählungen und mehrdimensionale Analysen - ohne erneute Verarbeitung historischer Daten handhaben zu müssen. Inkrementelle Aktualisierung von Daten, Optimierung von Workflows und Verkürzung der Verarbeitungszeit bei gleichzeitiger Wahrung von Genauigkeit und Effizienz. Schnellere, skalierbare und kostengünstige Einblicke, die die Entscheidungsfindung verändern. Erkunden Sie die [Anleitung zur Verwendung von Hypercubes](../../query-service/hypercubes/overview.md), um erweiterte Analysen zu erschließen. |
| Abfrage-Editor-Objektbrowser | Steigern Sie die Abfrageeffizienz mit dem neuen Objektbrowser im Abfrage-Editor. Schnelles Suchen, Filtern und Zugreifen auf Datensätze, um Abfragen schneller zu schreiben und zu verfeinern. Mit Echtzeit-Schemaaktualisierungen und sofortigen Tabellenmetadaten können Sie Workflows optimieren, die Navigationszeit verkürzen und Ihr Abfrageerlebnis verbessern. Erschließen Sie das Potenzial Ihrer Daten und optimieren Sie die Analyse. Weitere Informationen finden Sie [Handbuch unter Verwenden ](../../query-service/ui/user-guide.md#object-browser) Objektbrowsers). |
| Stunden berechnen | Erhalten Sie mit der neu sichtbaren Metrik „Stunden berechnen“ für geplante Abfragen die Kontrolle über die Ressourcennutzung. Zeigen Sie Rechenstunden auf der Abfrageausführungsebene an, um die Ressourcennutzung für CTAS/ITAS-Batch-Abfragen zu überwachen und zu optimieren. Startzeiten, Abschlussstatus und Berechnungszeit für jede Abfrageausführung verfolgen. Optimieren Sie die Leistung und senken Sie mühelos die Kosten. Lesen Sie das [Handbuch zu Compute Hours](../../query-service/ui/query-schedules.md#compute-hours-at-job-level), um Informationen zur Maximierung der Abfrageeffizienz zu erhalten. |

{style="table-layout:auto"}

Weitere Informationen über den Abfrage-Service finden Sie unter [Abfrage-Service - Übersicht](../../query-service/home.md).

## Segmentierungs-Service {#segmentation-service}

[!DNL Segmentation Service] definiert eine bestimmte Untergruppe von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Segmente können auf Datensatzdaten (z. B. demografische Daten) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Aktualisierung der Streaming-Segmentierungskriterien | Ab der Version vom September 2024 wurden die Kriterien aktualisiert, damit Ihre Zielgruppen für die Streaming-Segmentierung infrage kommen. Weitere Informationen zu diesen Änderungen finden Sie im Abschnitt Aktualisierung der [Kriterien für die Berechtigung zur Streaming-Segmentierung](../../segmentation/eligibility-criteria-update.md). |
| Unified Search-Implementierung | Das Suchverhalten in Segment Builder verwendet jetzt die einheitliche Suche. Dies ermöglicht ein stabileres Erlebnis bei der Verwaltung und Suche nach Zielgruppen, die für die Segmentzugehörigkeit wiederverwendet werden können. Weitere Informationen zu dieser Änderung finden Sie im [Segment Builder-Handbuch](../../segmentation/ui/segment-builder.md#rule-builder-canvas). |

{style="table-layout:auto"}

Weitere Informationen zu [!DNL Segmentation Service] finden Sie unter [Segmentierung - Übersicht](../../segmentation/home.md).

## Quellen {#sources}

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

Verwenden Sie Quellen in Experience Platform, um Daten aus einer Adobe-Anwendung oder einer Datenquelle von Drittanbietern aufzunehmen.

**Aktualisierte Funktion**

| Funktion | Beschreibung |
| --- | --- |
| [!BADGE Beta]{type=Informative}-Unterstützung für die verschlüsselte Datenaufnahme in der Benutzeroberfläche | Sie können jetzt verschlüsselte Daten aus einer Cloud-Speicher-Batch-Quelle mithilfe des Arbeitsbereichs „Quellen“ in der Benutzeroberfläche von Experience Platform aufnehmen. Weitere Informationen finden Sie im Tutorial [Aufnehmen verschlüsselter Daten in ](../../sources/tutorials/ui/encryped-ingestion.md) Benutzeroberfläche“. |
| Allgemeine Verfügbarkeit der [!DNL Snowflake Streaming] | Die [!DNL Snowflake Streaming] ist jetzt allgemein verfügbar. Verwenden Sie diese Quelle, um Daten von Ihrem [!DNL Snowflake]-Konto zu Experience Platform zu streamen. Weitere Informationen finden Sie [[!DNL Snowflake Streaming] Übersicht](../../sources/connectors/databases/snowflake-streaming.md). |
| Unterstützung der Authentifizierung von Service-Konten in [!DNL Google BigQuery] | Sie können jetzt Ihr [!DNL Google BigQuery]-Konto mit Experience Platform verbinden, indem Sie die Authentifizierung für das Service-Konto verwenden. Weitere Informationen finden Sie [[!DNL Google BigQuery] Übersicht](../../sources/connectors/databases/bigquery.md#generate-your-google-bigquery-credentials) . <br> ![Abbildung der Experience Platform-Benutzeroberfläche mit hervorgehobener Option „Zeitplan und Ordner bearbeiten“ im Planungsschritt.](../2024/assets/september/service_auth.png "Service-Authentifizierung für Google BigQuery."){width="250" align="center" zoomable="yes"} |
| Unterstützung für das Überspringen der Beispieldatenvorschau | Sie können jetzt beim Erstellen einer Quellverbindung mit den folgenden Quellen auswählen, dass die Datenvorschau übersprungen werden soll: <ul><li>[[!DNL Google BigQuery]](../../sources/tutorials/ui/create/databases/bigquery.md#skip-preview-of-sample-data)</li><li>[[!DNL Salesforce]](../../sources/tutorials/ui/create/crm/salesforce.md#skip-preview-of-sample-data)</li><li>[[!DNL Snowflake]](../../sources/tutorials/ui/create/databases/snowflake.md#skip-preview-of-sample-data)</li></ul> Sie können die Datenvorschau überspringen, um eine Zeitüberschreitung zu vermeiden, die bei der Aufnahme großer Datenstapel auftreten kann. Dadurch kann die automatische Validierung Ihrer berechneten und erforderlichen Felder verhindert werden. Wenn Sie sich dafür entscheiden, die Datenvorschau zu überspringen, müssen Sie Ihre berechneten und erforderlichen Felder während der Zuordnung möglicherweise manuell validieren. |
| Unterstützung für das Deaktivieren von Chunking in [!DNL SFTP] | Sie können jetzt eine Einstellung konfigurieren, mit der Sie die Unterteilung in der [!DNL SFTP] deaktivieren können. Weitere Informationen finden Sie [[!DNL SFTP] Übersicht](../../sources/connectors/cloud-storage/sftp.md) . |

{style="table-layout:auto"}

Weitere Informationen finden Sie unter [Quelle – Übersicht](../../sources/home.md).
