---
audience: user
user-guide-title: Hilfe zum Adobe Experience Platform-Abfrageservice
breadcrumb-title: Anleitung zum Query Service
user-guide-description: Verwenden Sie Standard-SQL, um Daten im Data Lake in Experience Platform abzufragen.
feature: Queries
source-git-commit: 59fb31697d7a9f132f7e8700422538026ae24b8c
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 67%

---


# Query Service von Adobe Experience Platform {#query}

- [Query Service – Übersicht](home.md)
- [Query Service-Verpackung](packages.md)
- [Limits für Query Service](guardrails.md)
- Data Distiller {#data-distiller}
   - [Lizenzverwendung](data-distiller/licence-usage.md)
- Erste Schritte {#get-started}
   - [Voraussetzungen](get-started/prerequisites.md)
- Anwendungsfälle {#use-cases}
   - [Abgebrochener Browser](use-cases/abandoned-browse.md)
   - [Aktivitätsanalyse mit Adobe Target](use-cases/activity-analysis-with-adobe-target.md)
   - [Attributionsanalyse](use-cases/attribution-analysis.md)
   - [Bot-Filterung](use-cases/bot-filtering.md)
   - [Web- und mobile Analyseeinblicke](use-cases/analytics-insights.md)
- Query Service-API {#api}
   - [Erste Schritte](api/getting-started.md)
   - [Abfragen](api/queries.md)
   - [Verbindungsparameter](api/connection-parameters.md)
   - [Geplante Abfragen](api/scheduled-queries.md)
   - [Ausführungen für geplante Abfragen](api/runs-scheduled-queries.md)
   - [Abfragevorlagen](api/query-templates.md)
- Benutzeroberfläche von Query Service {#ui}
   - [Benutzeroberfläche – Übersicht](ui/overview.md)
   - [Benutzerhandbuch zum Abfrage-Editor](ui/user-guide.md)
   - [Abfragevorlagen](ui/query-templates.md)
   - [Verwenden von Query Service-Anmeldeinformationen](ui/credentials.md)
   - [Generieren von Datensätzen aus Abfrageergebnissen](ui/create-datasets.md)
- [Abfragen überwachen](monitor-queries.md)
- Abfrage-beschleunigter Speicher{#query-accelerated-store}
   - [Berichtseinblicke-Datenmodell](query-accelerated-store/reporting-insights-data-model.md)
- Best Practices {#best-practices}
   - [Allgemeine Leitlinien für die Ausführung von Abfragen](best-practices/writing-queries.md)
   - [Informationen zur Ordnung von Daten-Medienelementen](./best-practices/organize-data-assets.md)
   - [Arbeiten mit verschachtelten Datenstrukturen](best-practices/nested-data-structures.md)
   - [Reduzieren verschachtelter Datenstrukturen](best-practices/flatten-nested-data.md)
   - [Anonymer Block](best-practices/anonymous-block.md)
   - [Inkrementelles Laden](best-practices/incremental-load.md)
   - [Deduplizierung von Daten](best-practices/deduplication.md)
- Abgeleitete Attribute {#derived-attributes}
   - [Übersicht](derived-attributes/overview.md)
   - [Anwendungsfall: Deciles](derived-attributes/deciles-use-case.md)
- Beispielabfragen {#sample-queries}
   - [Beispielabfragen von Erlebnisereignissen](sample-queries/experience-event.md)
   - [Beispielabfragen von Adobe Analytics](sample-queries/adobe-analytics.md)
- SQL-Referenz {#sql}
   - [SQL – Übersicht](sql/overview.md)
   - [SQL-Syntax](sql/syntax.md)
   - [Adobe-definierte Funktionen](sql/adobe-defined-functions.md)
   - [Spark SQL-Funktionen](sql/spark-sql-functions.md)
   - [Metadatenbefehle](sql/metadata.md)
   - [Vorbereitete Anweisungen](sql/prepared-statements.md)
   - [Datensatzbeispiele](sql/dataset-samples.md)
- Clients mit Query Service verbinden {#clients}
   - [Kundenverbindungen – Überblick](clients/overview.md)
   - [SSL-Modi](./clients/ssl-modes.md)
   - [Aqua Data Studio](clients/aqua-data-studio.md)
   - [DbVisualizer](./clients/dbvisulaizer.md)
   - [Jupyter Notebook](clients//jupyter-notebook.md)
   - [Looker](clients/looker.md)
   - [Postico](clients/postico.md)
   - [Power BI](clients/power-bi.md)
   - [PSQL](clients/psql.md)
   - [RStudio](clients/rstudio.md)
   - [Tableau](clients/tableau.md)
- Data Governance {#data-governance}
   - [Übersicht](data-governance/overview.md)
   - [Auditprotokoll-Handbuch](data-governance/audit-log-guide.md)
   - [Identitäten in Ad-hoc-Schemata-Datensätzen](data-governance/ad-hoc-schema-identities.md)
   - [Unterstützung der attributbasierten Zugriffskontrolle für Ad-hoc-Schemata](./data-governance/ad-hoc-schema-labels.md)
- [Handbuch zur Fehlerbehebung](troubleshooting-guide.md)
- [API-Referenz](https://www.adobe.io/experience-platform-apis/references/query-service/)
- [Platform – Versionshinweise](https://docs.adobe.com/content/help/de-DE/experience-platform/release-notes/latest.html)