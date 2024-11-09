---
audience: user
user-guide-title: Hilfe zum Adobe Experience Platform-Abfrageservice
breadcrumb-title: Handbuch zum Abfragedienst
user-guide-description: Verwenden Sie Standard-SQL-Abfragen, um Daten im Data Lake in Experience Platform abzufragen.
feature: Queries
role: User,Developer
source-git-commit: fed47e132e1ff46fdf3df1a5a3f9f3e99bd1340c
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 77%

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
      - [Übersicht](data-distiller/derived-datasets/overview.md)
      - [Erstellen abgeleiteter Datensätze mit SQL](data-distiller/derived-datasets/create-derived-datasets-with-sql.md)
      - [Erstellen von dezimalbasierten abgeleiteten Datensätzen](data-distiller/derived-datasets/decile-based-derived-attributes.md)
   - SQL Insights für erweiterte App-Berichterstellung {#sql-insights}
      - [Übersicht](data-distiller/sql-insights/overview.md)
      - [Abfrage pro Modus](data-distiller/sql-insights/query-pro-mode.md)
      - [Beschleunigte Abfragen senden](data-distiller/sql-insights/send-accelerated-queries.md)
      - [Handbuch zum Reporting-Insights-Datenmodell](data-distiller/sql-insights/reporting-insights-data-model.md)
   - AI-/ML-Funktions-Pipelines {#ml-feature-pipelines}
      - [Übersicht](data-distiller/ml-feature-pipelines/overview.md)
      - [Herstellen einer Verbindung zu Jupyter Notebooks](data-distiller/ml-feature-pipelines/establish-connection.md)
      - [Explorative Datenanalyse](data-distiller/ml-feature-pipelines/exploratory-analysis.md)
      - [Technische Funktionen für ML](data-distiller/ml-feature-pipelines/feature-engineering.md)
      - [Daten in ML-Umgebungen exportieren](data-distiller/ml-feature-pipelines/export-data.md)
      - [End-to-End-Workflow für die Anreicherung der AI-/ML-Datenpipeline](data-distiller/ml-feature-pipelines/end-to-end-notebook-workflow.md)
- Distiller-Statistiken für Daten {#advanced-statistics}
   - [Übersicht](advanced-statistics/overview.md)
   - [Funktionsentwicklung](advanced-statistics/feature-engineering.md)
   - [Modelle](advanced-statistics/models.md)
Modelle implementieren {#implement-models}
      - [Modelle implementieren](advanced-statistics/implement-models/implement-models.md)
      - [Regression](advanced-statistics/implement-models/regression.md)
      - [Klassifizierung](advanced-statistics/implement-models/classification.md)
      - [Clustering](advanced-statistics/implement-models/clustering.md)
   - [Merkmalumwandlung](advanced-statistics/feature-transformation.md)
- Data Distiller Audiences {#data-distiller-audiences}
   - [Erstellen externer Zielgruppen mit SQL](data-distiller-audiences/overview.md)
- Beispiele {#use-cases}
   - [Übersicht](use-cases/overview.md)
   - [Abgebrochenes Durchsuchen](use-cases/abandoned-browse.md)
   - [Attributionsanalyse](use-cases/attribution-analysis.md)
   - [Bot-Filterung](use-cases/bot-filtering.md)
   - [Erstellen eines Trendberichts mit Ereignissen](use-cases/trended-report-of-events.md)
   - [Einverständnisanalyse](use-cases/consent-analysis.md)
   - [Kundenlebenszeitwert](use-cases/customer-lifetime-value.md)
   - [Datenforschung](./use-cases/data-exploration.md)
   - [Dezilbasierte abgeleitete Datensätze](use-cases/deciles-use-case.md)
   - [Ungefähre Übereinstimmung](use-cases/fuzzy-match.md)
   - [Auflisten der Seitenansichten von Benutzenden](use-cases/list-visitor-sessions.md)
   - [Besuchende nach Seitenansichten auflisten](use-cases/visitors-by-number-of-page-views.md)
   - [Tendenz-Bewertung](use-cases/propensity-score.md)
   - [Abrufen ähnlicher Datensätze mit Funktionen höherer Reihenfolge](use-cases/retrieve-similar-records.md)
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
- Distiller-Hyperwürfel {#hypercubes}
   - [Effiziente Big-Data-Analyse mit Hyperwürfen](hypercubes/overview.md)
- Clients mit Query Service verbinden {#clients}
   - [Kundenverbindungen – Überblick](clients/overview.md)
   - [SSL-Modi](./clients/ssl-modes.md)
   - [Aqua Data Studio](clients/aqua-data-studio.md)
   - [DbVisualizer](./clients/dbvisulaizer.md)
   - [GitHub-Kopilot](./clients/github-copilot.md)
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
- Query Service-API {#api}
   - [Erste Schritte](api/getting-started.md)
   - [Abfragen](api/queries.md)
   - [Verbindungsparameter](api/connection-parameters.md)
   - [Zeitpläne](api/scheduled-queries.md)
   - [Ausführungen für geplante Abfragen](api/runs-scheduled-queries.md)
   - [Abfragevorlagen](api/query-templates.md)
   - [Beschleunigte Abfragen](api/accelerated-queries.md)
   - [Abonnements von Warnhinweisen](api/alert-subscriptions.md)
- Query Service-Authentifizierungs-API {#auth-api}
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
   - [Funktionen mit höherer Reihenfolge](sql/higher-order-functions.md)
   - [Spark SQL-Funktionen](sql/spark-sql-functions.md)
   - [Metadatenbefehle](sql/metadata.md)
   - [Vorbereitete Anweisungen](sql/prepared-statements.md)
- [Häufig gestellte Fragen](troubleshooting-guide.md)
- [Zulassungsliste von IP-Adressen](ip-address-allowlist.md)
- [API-Referenz](https://www.adobe.io/experience-platform-apis/references/query-service/)
- [Platform – Versionshinweise](https://experienceleague.adobe.com/de/docs/experience-platform/release-notes/latest)
