---
audience: user
user-guide-title: Hilfe zum Adobe Experience Platform-Abfrageservice
breadcrumb-title: Handbuch zum Abfragedienst
user-guide-description: Verwenden Sie Standard-SQL-Abfragen, um Daten im Data Lake in Experience Platform abzufragen.
feature: Queries
source-git-commit: 135691e0d2b77cc8e2581ff3a614fe26c7969cdd
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 100%

---


# Query Service von Adobe Experience Platform {#query}

- [Query Service – Übersicht](home.md)
- [Packaging des Abfrage-Services](packages.md)
- [Leitplanken des Abfrage-Services](guardrails.md)
- Erste Schritte {#get-started}
   - [Voraussetzungen](get-started/prerequisites.md)
- Data Distiller {#data-distiller}
   - [Übersicht](data-distiller/overview.md)
   - [Lizenznutzung](data-distiller/license-usage.md)
   - Abfrage-beschleunigte Speicherung {#query-accelerated-store}
      - [Beschleunigte Abfragen senden](data-distiller/query-accelerated-store/send-accelerated-queries.md)
      - [Handbuch zum Reporting-Insights-Datenmodell](data-distiller/query-accelerated-store/reporting-insights-data-model.md)
   - Abgeleitete Attribute {#derived-attributes}
      - [Übersicht](data-distiller/derived-attributes/overview.md)
      - [Nahtloser SQL-Fluss](data-distiller/derived-attributes/seamless-sql-flow.md)
      - [Erstellen von dezilbasierten abgeleiteten Attributen](data-distiller/derived-attributes/decile-based-derived-attributes.md)
- Anwendungsfälle {#use-cases}
   - [Abgebrochenes Durchsuchen](use-cases/abandoned-browse.md)
   - [Aktivitätsanalyse mit Adobe Target](use-cases/activity-analysis-with-adobe-target.md)
   - [Attributionsanalyse](use-cases/attribution-analysis.md)
   - [Bot-Filterung](use-cases/bot-filtering.md)
   - [Erstellen eines Trendberichts mit Ereignissen](use-cases/trended-report-of-events.md)
   - [Dezilbasierte abgeleitete Attribute](use-cases/deciles-use-case.md)
   - [Auflisten der Seitenansichten von Benutzenden](use-cases/list-visitor-sessions.md)
   - [Besuchende nach Seitenansichten auflisten](use-cases/visitors-by-number-of-page-views.md)
   - [Tendenz-Bewertung](use-cases/propensity-score.md)
   - [SQLAlchemy](use-cases/sqlalchemy.md)
   - [Zurückgeben und Verwenden von Merchandising-Variablen aus Analysedaten ](use-cases/merchandising-variables.md)
   - [Anzeigen des Roll-up-Berichts für Besuchende](use-cases/roll-up-report-of-a-visitor.md)
   - [Web- und Mobile-Analyse-Einblicke](use-cases/analytics-insights.md)
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
- Benutzeroberfläche von Query Service {#ui}
   - [Benutzeroberfläche – Übersicht](ui/overview.md)
   - [Benutzerhandbuch zum Abfrage-Editor](ui/user-guide.md)
   - [Abfragevorlagen](ui/query-templates.md)
   - [Abfragepläne](ui/query-schedules.md)
   - [Abfrageprotokolle](ui/query-logs.md)
   - [Überwachen von geplanten Abfragen ](ui/monitor-queries.md)
   - [Handbuch zu Anmeldeinformationen](ui/credentials.md)
   - [Generieren von Ausgabedatensätzen aus Abfrageergebnissen](ui/create-datasets.md)
- Abfrage-Service-API-Endpunkte {#api}
   - [Erste Schritte](api/getting-started.md)
   - [Abfragen](api/queries.md)
   - [Verbindungsparameter](api/connection-parameters.md)
   - [Zeitpläne](api/scheduled-queries.md)
   - [Ausführungen für geplante Abfragen](api/runs-scheduled-queries.md)
   - [Abfragevorlagen](api/query-templates.md)
   - [Beschleunigte Abfragen](api/accelerated-queries.md)
   - [Abonnements von Warnhinweisen](api/alert-subscriptions.md)
- Data Governance {#data-governance}
   - [Übersicht](data-governance/overview.md)
   - [Handbuch für Auditprotokolle](data-governance/audit-log-guide.md)
   - [Identitäten in ungeplanten Schema-Datensätzen](data-governance/ad-hoc-schema-identities.md)
   - [Unterstützung der attributbasierten Zugriffskontrolle für ungeplante Schemata](./data-governance/ad-hoc-schema-labels.md)
- Best Practices {#best-practices}
   - [Abfrageausführung](best-practices/writing-queries.md)
   - [Organisation von Daten-Medienelementen](./best-practices/organize-data-assets.md)
- Grundlegende Konzepte {#essential-concepts}
   - [Arbeiten mit verschachtelten Datenstrukturen](essential-concepts/nested-data-structures.md)
   - [Reduzieren von verschachtelten Datenstrukturen](essential-concepts/flatten-nested-data.md)
   - [Anonymer Block](essential-concepts/anonymous-block.md)
   - [Inkrementelles Laden](essential-concepts/incremental-load.md)
   - [Deduplizierung von Daten](essential-concepts/deduplication.md)
   - [Datensatzbeispiele](essential-concepts/dataset-samples.md)
- SQL-Referenz {#sql}
   - [SQL – Übersicht](sql/overview.md)
   - [SQL-Syntax](sql/syntax.md)
   - [Adobe-definierte Funktionen](sql/adobe-defined-functions.md)
   - [Spark SQL-Funktionen](sql/spark-sql-functions.md)
   - [Metadatenbefehle](sql/metadata.md)
   - [Vorbereitete Anweisungen](sql/prepared-statements.md)
- [Häufig gestellte Fragen](troubleshooting-guide.md)
- [API-Referenz](https://www.adobe.io/experience-platform-apis/references/query-service/)
- [Platform – Versionshinweise](https://experienceleague.adobe.com/docs/experience-platform/release-notes/latest.html?lang=de)
