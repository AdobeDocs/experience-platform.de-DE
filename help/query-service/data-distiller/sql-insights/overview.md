---
title: SQL Insights
description: Erfahren Sie mehr über die Anwendungsfälle, grundlegenden Funktionen und erforderlichen Schritte zur Entwicklung eines SQL-Insights-Dashboards mit Data Distiller. Erfahren Sie, wie die SQL Insights-Funktion in Data Distiller die Transparenz verbessern und operative Einblicke in verschiedene Dimensionen wie Profile, Audiences, Kampagnen, Journey, Berechtigungen und Einverständnis erhalten kann.
exl-id: f807d0fd-c8ec-42d4-96a0-5ffc5681943b
source-git-commit: ddf886052aedc025ff125c03ab63877cb049583d
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 5%

---

# SQL Insights

Erstellen Sie maßgeschneiderte Reporting-Datenmodelle, um tiefere Einblicke zu gewinnen, Strategien zu optimieren und die Analyse an spezifische Geschäftsanforderungen mit Data Distiller SQL Insights anzupassen. Verwenden Sie die SQL Insights-Funktion, um die Transparenz zu erhöhen und operative Einblicke aus Ihren Adobe Experience Platform-Daten in Dimensionen wie Profile, Audiences, Kampagnen, Journey, Berechtigungen und Einverständnis zu erhalten. Diese Funktion bietet eine vielseitige, adaptive Lösung, mit der Sie die Reporting-Datenmodelle Ihres Unternehmens an Ihre spezifischen Geschäftsanforderungen anpassen können.

Um [SQL Insights zu visualisieren](../../../dashboards/sql-insights-query-pro-mode/overview.md) können Sie den [query pro mode](../../../dashboards/sql-insights-query-pro-mode/overview.md) verwenden, um komplexe Analysen mit benutzerdefinierten SQL-Abfragen durchzuführen und Ihre Daten in leicht verständliche Diagramme umzuwandeln. Verwenden Sie den Abfrage-Pro-Modus, um maßgeschneiderte Einblicke und Visualisierungen in Ihren Dashboards zu erstellen und sowohl technische als auch nicht-technische Zielgruppen zu bedienen, indem Sie Ihre Einblicke als CSV-Dateien herunterladen.

In diesem Dokument werden die Anwendungsfälle, wesentlichen Funktionen und erforderlichen Schritte zur Entwicklung eines SQL Insights-Dashboards mit Data Distiller beschrieben.

## Voraussetzungen

In diesem Tutorial werden benutzerdefinierte Dashboards verwendet, um Daten aus Ihrem benutzerdefinierten Datenmodell innerhalb der Platform-Benutzeroberfläche zu visualisieren. Weitere Informationen [ diese Funktion finden Sie in der ](../../../dashboards/standard-dashboards.md) zu benutzerdefinierten Dashboards .

## Erste Schritte

Die Data Distiller SKU ist erforderlich, um ein benutzerdefiniertes Datenmodell für Ihre Reporting-Insights zu erstellen und um die Real-Time CDP-Datenmodelle zu erweitern, die angereicherte Platform-Daten enthalten. Siehe die [Packaging](../../packaging.md), [Leitplanken](../../guardrails.md#query-accelerated-store) und [Lizenzierung](../../data-distiller/license-usage.md), die sich auf die Data Distiller SKU beziehen. Wenn Sie nicht über die Data Distiller SKU verfügen, wenden Sie sich an den Kundendienst von Adobe, um weitere Informationen zu erhalten.

## Anwendungsfälle für SQL Insights {#use-cases}

Im Folgenden finden Sie gängige Anwendungsfälle, die effektiv durch SQL Insights in Data Distiller behoben werden können.

### Transparenz der Profil- und Zielgruppennutzung {#usage-transparency}

**Herausforderung:** Aufschlüsselung der Key Performance Indicators (KPIs) nach bestimmten Kriterien wie Geschäftseinheiten, Treuestatus oder Customer Lifetime Value (CLTV).

**SQL Insights-Lösung:** Data Distiller ermöglicht die Erweiterung von Reporting-Datenmodellen in Adobe Experience Platform und [ das Hinzufügen benutzerdefinierter Profilattribute wie CLTV ](../../use-cases/customer-lifetime-value.md) Treuestatus.

### Anomalieverfolgung für Einverständnis {#consent-anomaly-tracking}

**Herausforderung:** Anwenden von Trend-Zeilenberichten zu Zielgruppenüberschneidungen und -größen auf benutzerdefinierte Einverständnisattribute für Kanäle wie E-Mail, SMS und Telefon.

**SQL Insights-Lösung** Das Berichtsdatenmodell kann erweitert werden, um Änderungen der Einverständnisvoreinstellungen im Laufe der Zeit zu verfolgen. Dazu gehört die Erstellung zusätzlicher Fakten- und Dimensionstabellen für die Voreinstellungen für das Trend-Einverständnis und [ Planung (inkrementelle Datenaktualisierung](../../key-concepts/incremental-load.md).

### Optimieren der Zielgruppensegmentierungsstrategie {#optimize-audience-segmentation-strategy}

**Herausforderung:** Integrieren von durch das ML-Modell (maschinelles Lernen) generierten Tendenzwerten in die KPI-Berichte der Zielgruppe.

**SQL Insights-Lösung:** Data Distiller ermöglicht die Einbeziehung von [Tendenz-Scores aus benutzerdefinierten ML-Modellen](../../use-cases/propensity-score.md) wodurch die Berechnung aggregierter Scores auf Audience-Ebene erleichtert wird. Diese Daten können dann zusammen mit Standard-KPIs gemeldet werden.

### Zielgruppenerweiterung {#audience-expansion}

**Herausforderung:** Sie, wie Sie in Berichten zu Zielgruppenüberschneidungen mehr als nur Profilzahlen erfassen und zusätzliche demografische Daten oder Voreinstellungen für Zielgruppenerweiterungsstrategien erhalten.

**SQL Insights-Lösung** Durch die Erweiterung des Berichtsdatenmodells können Benutzer zusätzliche Profilattribute einbeziehen, wodurch der Bericht zur Zielgruppenüberschneidung um relevante demografische Daten und Voreinstellungen erweitert wird.

## Schlüsselfunktionen zum Generieren von SQL Insights {#key-capabilities}

Die folgende Abbildung zeigt einige wichtige Funktionen zum Generieren von SQL Insights. Zu diesen Funktionen gehören:

1. **Datenvisualisierungen:** Sie visuelle Elemente wie Trends und Balkendiagramme ein, um eine umfassende Ansicht der Datentrends zu erhalten.
1. **Dashboard-Authoring:** Erstellung benutzerdefinierter Dashboards, die auf bestimmte Anwendungsfälle zugeschnitten sind, wodurch ein stärker personalisiertes und zielgerichtetes Analyseerlebnis geboten wird.
1. **Flexible SQL-Datenmodellierung:** Verwenden Sie einen vielseitigen SQL-Datenmodellierungsansatz, der es Benutzern ermöglicht, verschiedene Datensätze nahtlos zu kombinieren und zu bearbeiten, wodurch die Anpassungsfähigkeit und die Analysetiefe verbessert werden.
1. **Beschleunigter Speicher:** Implementieren eines beschleunigten Speichermechanismus zur effizienten Bereitstellung aggregierter Einblicke über SQL, um einen optimierten und schnellen Zugriff auf wertvolle Informationen sicherzustellen.
1. **BI-Konnektivität:** nahtlose Integration mit gängigen Business Intelligence-Tools (BI), einschließlich Power BI, Tableau, Looker und Apache Superset. Diese Konnektivität stellt die Kompatibilität mit verschiedenen BI-Umgebungen sicher und bietet Benutzern die Flexibilität, ihr bevorzugtes Tool für die ausführliche Analyse und Berichterstellung zu verwenden.

![Visuelle Darstellungen der Schlüsselfunktionen von Data Distiller SQL Insights.](../../images/data-distiller/sql-insights/key-capabilities-of-customizable-insights.png)

## Schritte zum Erstellen von SQL Insights {#steps-to-create}

Gehen Sie wie folgt vor, um in Data Distiller ein SQL Insights-Dashboard zu entwickeln.

1. **Ad-hoc-Abfrage-Exploration:** Führen Sie zunächst Ad-hoc-`SELECT`-Abfragen aus, um Rohdaten im Data Lake zu untersuchen. Dies ermöglicht eine spontane explorative Datenanalyse zum Experimentieren und Validieren von Daten, bei denen die Ergebnisse der Abfragen nicht im Data Lake gespeichert werden.
1. **Nutzung von Batch-Abfragen:** Verwenden Sie Batch-Abfragen, um [geplante Aufträge zu erstellen](../../api/scheduled-queries.md#create-a-new-scheduled-query) um Insights-Aggregattabellen zu generieren und so einen systematischen und automatisierten Ansatz für die Datenverarbeitung sicherzustellen. Batch-Abfragen führen `INSERT TABLE AS SELECT` und `CREATE TABLE AS SELECT` Abfragen aus, um Daten zu bereinigen, zu formen, zu bearbeiten und anzureichern. Die Ergebnisse dieser Abfragen werden im Data Lake gespeichert.
1. **Laden aggregierter Insights:** Laden der generierten aggregierten Insights in den beschleunigten Speicher und Verwenden von SQL zum Testen von Abfragen sowie zum Sicherstellen der Genauigkeit und Effizienz des Datenabrufs. Weitere Informationen zum [Erstellen statusloser Abfragen an den beschleunigten Speicher](../../api/accelerated-queries.md) finden Sie in der Dokumentation.
1. **Zugriff und Integration:** Greifen Sie nahtlos auf die Erkenntnisse zu, die im beschleunigten Speicher gespeichert sind, indem Sie sie mit Adobe Experience Platform [benutzerdefinierten Dashboards](../../../dashboards/standard-dashboards.md) oder anderen bevorzugten Business Intelligence-Tools (BI) integrieren. Diese Integrationen mit Drittanbieter-Clients ermöglichen Benutzern ein einheitliches und intuitives Benutzererlebnis.

![Eine Infografik, die die vier Schritte zum Erstellen von SQL Insights in Data Distiller veranschaulicht.](../../images/data-distiller/sql-insights/steps-to-customizable-insights.png)

## Nächste Schritte

Durch das Lesen dieses Dokuments haben Sie jetzt ein besseres Verständnis für die Anwendungsfälle, wesentlichen Funktionen und erforderlichen Schritte zur Entwicklung eines SQL-Insights-Dashboards mit Data Distiller. Weitere Informationen zum Erstellen maßgeschneiderter Reporting-Datenmodelle finden Sie im [Reporting Insights-Datenmodell-Handbuch](./reporting-insights-data-model.md).
