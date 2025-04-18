---
audience: user
user-guide-title: Hilfe zum Adobe Experience Platform-Abfrageservice
breadcrumb-title: Handbuch zum Abfragedienst
user-guide-description: Verwenden Sie Standard-SQL-Abfragen, um Daten im Data Lake in Experience Platform abzufragen.
feature: Queries
role: User,Developer
source-git-commit: 5e8dccf91e8c83b4734b363539cfb911b5c2ae29
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 70%

---


# Query Service von Adobe Experience Platform {#query}

- [Query Service – Übersicht](home.md)
- [Packaging des Abfrage-Services](packaging.md)
- [Leitplanken des Abfrage-Services](guardrails.md)
- Erste Schritte {#get-started}
   - [Voraussetzungen](get-started/prerequisites.md)
- Data Distiller {#data-distiller}
   - [Übersicht](data-distiller/overview.md)
   - [Lizenznutzung](data-distiller/license-usage.md)
   - Abgeleitete Datensätze {#derived-datasets}
      - [Überblick](data-distiller/derived-datasets/overview.md)
      - [Erstellen abgeleiteter Datensätze mit SQL](data-distiller/derived-datasets/create-derived-datasets-with-sql.md)
      - [Erstellen von dezilbasierten abgeleiteten Datensätzen](data-distiller/derived-datasets/decile-based-derived-attributes.md)
   - SQL Insights für erweiterte App-Berichte {#sql-insights}
      - [Überblick](data-distiller/sql-insights/overview.md)
      - [Abfrage pro Modus](data-distiller/sql-insights/query-pro-mode.md)
      - [Accelerated Store - Übersicht](data-distiller/sql-insights/accelerated-store-overview.md)
      - [Beschleunigte Abfragen senden](data-distiller/sql-insights/send-accelerated-queries.md)
      - [Handbuch zum Reporting-Insights-Datenmodell](data-distiller/sql-insights/reporting-insights-data-model.md)
   - KI/ML-Funktions-Pipelines {#ml-feature-pipelines}
      - [Überblick](data-distiller/ml-feature-pipelines/overview.md)
      - [Verbinden mit Jupyter-Notebooks](data-distiller/ml-feature-pipelines/establish-connection.md)
      - [Explorative Datenanalyse](data-distiller/ml-feature-pipelines/exploratory-analysis.md)
      - [Engineering-Funktionen für ML](data-distiller/ml-feature-pipelines/feature-engineering.md)
      - [Exportieren von Daten in ML-Umgebungen](data-distiller/ml-feature-pipelines/export-data.md)
      - [End-to-End-Workflow zur Anreicherung von KI/ML-Daten](data-distiller/ml-feature-pipelines/end-to-end-notebook-workflow.md)
   - [Sitzung zum Summit 2025](data-distiller/top-tips-to-maximize-value.md)
- Data Distiller-Statistiken und maschinelles Lernen {#advanced-statistics}
   - [Überblick](advanced-statistics/overview.md)
   - [Funktionsentwicklung](advanced-statistics/feature-engineering.md)
   - [Modelle](advanced-statistics/models.md)
   - [Funktionstransformation](advanced-statistics/feature-transformation.md)
   - Implementieren von Modellen {#implement-models}
      - [Implementieren von Modellen](advanced-statistics/implement-models/implement-models.md)
      - [Regression](advanced-statistics/implement-models/regression.md)
      - [Klassifizierung](advanced-statistics/implement-models/classification.md)
      - [Clustering](advanced-statistics/implement-models/clustering.md)
   - Beispiele {#examples}
      - [Bot-Filterung mithilfe von Statistiken und maschinellem Lernen](advanced-statistics/examples/statistics-and-ml-bot-filtering.md)
      - [Prognostizieren der Kundenabwanderung mithilfe der SQL-basierten logistischen Regression](advanced-statistics/examples/predict-customer-churn.md)
- Daten-Distiller-Zielgruppen {#data-distiller-audiences}
   - [Erstellen externer Zielgruppen mithilfe von SQL](data-distiller-audiences/overview.md)
- Beispiele {#use-cases}
   - [Überblick](use-cases/overview.md)
   - [Abgebrochenes Durchsuchen](use-cases/abandoned-browse.md)
   - [Attributionsanalyse](use-cases/attribution-analysis.md)
   - [Bot-Filterung](use-cases/bot-filtering.md)
   - [Bot-Filterung mithilfe von Statistiken und Einführung in maschinelles Lernen](use-cases/statistics-and-ml-bot-filtering-stub.md)
   - [Erstellen eines Trendberichts mit Ereignissen](use-cases/trended-report-of-events.md)
   - [Einverständnisanalyse](use-cases/consent-analysis.md)
   - [Kundenlebenszeitwert](use-cases/customer-lifetime-value.md)
   - [Datenforschung](./use-cases/data-exploration.md)
   - [Dezilbasierte abgeleitete Datensätze](use-cases/deciles-use-case.md)
   - [Ungefähre Übereinstimmung](use-cases/fuzzy-match.md)
   - [Auflisten der Seitenansichten von Benutzenden](use-cases/list-visitor-sessions.md)
   - [Besuchende nach Seitenansichten auflisten](use-cases/visitors-by-number-of-page-views.md)
   - [Prognostizieren der Kundenabwanderung mithilfe von SQL](use-cases/predict-customer-churn-stub.md)
   - [Tendenz-Bewertung](use-cases/propensity-score.md)
   - [Abrufen ähnlicher Datensätze mit Funktionen höherer Ordnung](use-cases/retrieve-similar-records.md)
   - [Zurückgeben und Verwenden von Merchandising-Variablen aus Analysedaten ](use-cases/merchandising-variables.md)
   - [SQLAlchemy](use-cases/sqlalchemy.md)
   - [Anzeigen des Roll-up-Berichts für Besuchende](use-cases/roll-up-report-of-a-visitor.md)
   - [Web- und Mobile-Analyse-Einblicke](use-cases/analytics-insights.md)
- Schlüsselkonzepte {#key-concepts}
   - [Arbeiten mit verschachtelten Datenstrukturen](key-concepts/nested-data-structures.md)
   - [Reduzieren von verschachtelten Datenstrukturen](key-concepts/flatten-nested-data.md)
   - [Anonymer Block](key-concepts/anonymous-block.md)
   - [Inline-Vorlage](key-concepts/inline-templates.md)
   - [Inkrementelles Laden](key-concepts/incremental-load.md)
   - [Deduplizierung von Daten](key-concepts/deduplication.md)
   - [Datensatzbeispiele](key-concepts/dataset-samples.md)
   - [Berechnung der Datensatzstatistiken](key-concepts/dataset-statistics.md)
- Data Distiller Hypercubes {#hypercubes}
   - [Effiziente Big-Data-Analyse mit Hypercubes](hypercubes/overview.md)
- Clients mit Query Service verbinden {#clients}
   - [Kundenverbindungen – Überblick](clients/overview.md)
   - [SSL-Modi](./clients/ssl-modes.md)
   - [Aqua Data Studio](clients/aqua-data-studio.md)
   - [DbVisualizer](./clients/dbvisulaizer.md)
   - [GitHub-Copilot](./clients/github-copilot.md)
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
   - [Parametrierte Abfragen](ui/parameterized-queries.md)
   - [Abfragepläne](ui/query-schedules.md)
   - [Abfrageprotokolle](ui/query-logs.md)
   - [Überwachen von geplanten Abfragen ](ui/monitor-queries.md)
   - [Handbuch zu Anmeldedaten](ui/credentials.md)
   - [Generieren von Ausgabedatensätzen aus Abfrageergebnissen](ui/create-datasets.md)
- Abfrage-Service-API {#api}
   - [Erste Schritte](api/getting-started.md)
   - [Abfragen](api/queries.md)
   - [Verbindungsparameter](api/connection-parameters.md)
   - [Zeitpläne](api/scheduled-queries.md)
   - [Ausführungen für geplante Abfragen](api/runs-scheduled-queries.md)
   - [Abfragevorlagen](api/query-templates.md)
   - [Beschleunigte Abfragen](api/accelerated-queries.md)
   - [Abonnements von Warnhinweisen](api/alert-subscriptions.md)
- Data Distiller Authorization-API {#auth-api}
   - [Übersicht](auth-api/overview.md)
   - [Erste Schritte](auth-api/getting-started.md)
   - [IP-Zugriff](auth-api/ip-access.md)
   - [Überprüfen](auth-api/validate.md)
- Data Governance {#data-governance}
   - [Übersicht](data-governance/overview.md)
   - [Handbuch für Auditprotokolle](data-governance/audit-log-guide.md)
   - [Identitäten in ungeplanten Schema-Datensätzen](data-governance/ad-hoc-schema-identities.md)
   - [Unterstützung der attributbasierten Zugriffskontrolle für ungeplante Schemata](./data-governance/ad-hoc-schema-labels.md)
- Best Practices {#best-practices}
   - [Abfrageausführung](best-practices/writing-queries.md)
   - [Organisation von Daten-Medienelementen](./best-practices/organize-data-assets.md)
- SQL-Referenz {#sql}
   - [SQL – Übersicht](sql/overview.md)
   - [SQL-Syntax](sql/syntax.md)
   - [Adobe-definierte Funktionen](sql/adobe-defined-functions.md)
   - [Funktionen höherer Ordnung](sql/higher-order-functions.md)
   - [Spark SQL-Funktionen](sql/spark-sql-functions.md)
   - [Metadatenbefehle](sql/metadata.md)
   - [Vorbereitete Anweisungen](sql/prepared-statements.md)
- [Häufig gestellte Fragen](troubleshooting-guide.md)
- [Zulassungsliste von IP-Adressen](ip-address-allowlist.md)
- [API-Referenz](https://www.adobe.io/experience-platform-apis/references/query-service/)
- [Versionshinweise zu Experience Platform](https://experienceleague.adobe.com/de/docs/experience-platform/release-notes/latest)
