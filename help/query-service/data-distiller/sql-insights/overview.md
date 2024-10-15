---
title: SQL Insights
description: Erfahren Sie mehr über die Anwendungsfälle, die wichtigsten Funktionen und erforderlichen Schritte zur Entwicklung eines SQL Insights-Dashboards mit Data Distiller. Erfahren Sie, wie die SQL Insights-Funktion in Data Distiller die Transparenz verbessert und betriebliche Einblicke in verschiedene Dimensionen wie Profile, Zielgruppen, Kampagnen, Journey, Berechtigungen und Einverständniserklärungen erhält.
exl-id: f807d0fd-c8ec-42d4-96a0-5ffc5681943b
source-git-commit: ddf886052aedc025ff125c03ab63877cb049583d
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 5%

---

# SQL Insights

Erstellen Sie maßgeschneiderte Berichtsdatenmodelle, um tiefere Einblicke zu gewinnen, Strategien zu optimieren und Analysen an spezifische Geschäftsanforderungen mit Data Distiller SQL Insights anzupassen. Verwenden Sie die SQL Insights-Funktion, um die Transparenz zu erhöhen und operative Einblicke aus Ihren Adobe Experience Platform-Daten über Dimensionen wie Profile, Zielgruppen, Kampagnen, Journey, Berechtigungen und Einverständniserklärungen hinweg zu gewinnen. Diese Funktion bietet eine vielseitige, adaptive Lösung, um die Berichtsdatenmodelle Ihres Unternehmens an Ihre spezifischen Geschäftsanforderungen anzupassen.

Um [Ihre SQL Insights](../../../dashboards/sql-insights-query-pro-mode/overview.md) zu visualisieren, können Sie [query pro mode](../../../dashboards/sql-insights-query-pro-mode/overview.md) verwenden, um komplexe Analysen mit benutzerdefinierten SQL-Abfragen durchzuführen und Ihre Daten in leicht verständliche Diagramme umzuwandeln. Verwenden Sie den Abfragepro-Modus, um individuelle Einblicke und Visualisierungen in Ihren Dashboards zu erstellen und sowohl technische als auch nicht technische Zielgruppen zu berücksichtigen, indem Sie Ihre Einblicke als CSV-Dateien herunterladen.

In diesem Dokument werden die Anwendungsfälle, grundlegenden Funktionen und erforderlichen Schritte zum Entwickeln eines SQL Insights-Dashboards mit Data Distiller beschrieben.

## Voraussetzungen

In diesem Tutorial werden benutzerdefinierte Dashboards verwendet, um Daten aus Ihrem benutzerdefinierten Datenmodell innerhalb der Platform-Benutzeroberfläche zu visualisieren. Weitere Informationen zu dieser Funktion finden Sie in der Dokumentation zu [benutzerdefinierten Dashboards](../../../dashboards/standard-dashboards.md) .

## Erste Schritte

Die Data Distiller SKU ist erforderlich, um ein benutzerdefiniertes Datenmodell für Ihre Reporting-Insights zu erstellen und um die Real-Time CDP-Datenmodelle zu erweitern, die angereicherte Platform-Daten enthalten. Weitere Informationen finden Sie in der Dokumentation zu [packaging](../../packaging.md), [guardrails](../../guardrails.md#query-accelerated-store) und [licensing](../../data-distiller/license-usage.md) , die sich auf die Data Distiller SKU bezieht. Wenn Sie nicht über die Data Distiller-SKU verfügen, wenden Sie sich für weitere Informationen an Ihren Adobe-Kundenbetreuer.

## Anwendungsfälle für SQL Insights {#use-cases}

Im Folgenden finden Sie gängige Anwendungsfälle, die effektiv über SQL Insights in Data Distiller adressiert werden können.

### Transparenz der Profil- und Zielgruppennutzung {#usage-transparency}

**Herausforderung:** Aufschlüsseln der KPIs (Key Performance Indicators) nach bestimmten Kriterien wie Geschäftseinheiten, Treuestatus oder Customer Lifetime Value (CLTV).

**SQL Insights Solution:** Data Distiller ermöglicht die Erweiterung der Berichtsdatenmodelle in Adobe Experience Platform, wodurch [ benutzerdefinierte Profilattribute wie CLTV](../../use-cases/customer-lifetime-value.md) oder der Treuestatus hinzugefügt werden können.

### Tracking von Einverständnisanomalien {#consent-anomaly-tracking}

**Herausforderung:** Anleitung zum Anwenden von Zielgruppenüberschneidungen und zur Größenanpassung von Trendzeilenberichten auf benutzerdefinierte Zustimmungsattribute für Kanäle wie E-Mail, SMS und Telefon.

**SQL Insights Solution:** Das Berichtsdatenmodell kann erweitert werden, um Änderungen an Zustimmungsvoreinstellungen im Laufe der Zeit zu verfolgen. Dazu gehört das Erstellen zusätzlicher Fakten- und Dimensionstabellen zum Trend von Zustimmungsvoreinstellungen und zum Planen der [inkrementellen Datenaktualisierung](../../key-concepts/incremental-load.md).

### Optimieren der Zielgruppensegmentierungsstrategie {#optimize-audience-segmentation-strategy}

**Herausforderung:** Wie integrieren Sie modellgenerierte Tendenzwerte für maschinelles Lernen (ML) in ihre KPI-Berichte für Zielgruppen.

**SQL Insights Solution:** Data Distiller ermöglicht die Einbeziehung von [Propensity Scores aus benutzerdefinierten ML-Modellen](../../use-cases/propensity-score.md), wodurch die Berechnung der aggregierten Werte auf Zielgruppenebene erleichtert wird. Diese Daten können dann zusammen mit standardmäßigen KPIs gemeldet werden.

### Zielgruppenerweiterung {#audience-expansion}

**Herausforderung:** Wie Sie mehr als nur Profilzahlen in Zielgruppenüberschneidungsberichten abrufen und zusätzliche demografische Daten oder Voreinstellungen erhalten, um Zielgruppenerweiterungsstrategien zu steuern.

**SQL Insights Solution:** Durch Erweiterung des Berichtsdatenmodells können Benutzer zusätzliche Profilattribute einbinden, wodurch der Bericht zur Zielgruppenüberschneidung mit relevanten demografischen Daten und Voreinstellungen angereichert wird.

## Wichtige Funktionen zum Generieren von SQL Insights {#key-capabilities}

In der folgenden Abbildung werden einige wichtige Funktionen zum Generieren von SQL Insights hervorgehoben. Zu diesen Funktionen gehören:

1. **Datenvisualisierungen:** Einbeziehen visueller Elemente wie Trends und Balkendiagramme für eine umfassende Ansicht von Datentrends.
1. **Dashboard-Authoring:** Aktivierung der Erstellung benutzerdefinierter Dashboards, die auf bestimmte Anwendungsfälle zugeschnitten sind, und Bereitstellung eines personalisierteren und gezielteren Analyseerlebnisses.
1. **Flexible SQL-Datenmodellierung:** Verwenden Sie einen vielseitigen SQL-Datenmodellierungsansatz, der es Benutzern ermöglicht, verschiedene Datensätze nahtlos zu kombinieren und zu bearbeiten, wodurch Anpassungsfähigkeit und Analysetiefe verbessert werden.
1. **Beschleuniger Speicher:** Implementierung eines beschleunigten Speichermechanismus, um aggregierte Einblicke effizient über SQL bereitzustellen und so einen optimierten und schnellen Zugriff auf wertvolle Informationen zu gewährleisten.
1. **BI-Konnektivität:** Erleichterung der nahtlosen Integration mit gängigen Business Intelligence-Tools (BI), einschließlich Power BI, Tableau, Looker und Apache Superset. Diese Konnektivität stellt die Kompatibilität mit verschiedenen BI-Umgebungen sicher und bietet Anwendern die Flexibilität, ihr bevorzugtes Tool für detaillierte Analysen und Berichte zu verwenden.

![ Visuelle Darstellungen der wichtigsten Funktionen von Data Distiller SQL Insights.](../../images/data-distiller/sql-insights/key-capabilities-of-customizable-insights.png)

## Schritte zum Erstellen von SQL Insights {#steps-to-create}

Um ein SQL Insights-Dashboard in Data Distiller zu entwickeln, folgen Sie den unten stehenden Anweisungen.

1. **Ad-hoc-Abfrageerforschung:** Beginnen Sie mit der Ausführung von Ad-hoc-Abfragen `SELECT`, um Rohdaten im Data Lake zu untersuchen. Dies ermöglicht eine spontane, explorative Datenanalyse zum Experimentieren und Validieren von Daten, in denen die Ergebnisse der Abfragen nicht im Data Lake gespeichert sind.
1. **Nutzung der Batch-Abfrage:** Verwenden Sie Batch-Abfragen, um [geplante Aufträge zu erstellen](../../api/scheduled-queries.md#create-a-new-scheduled-query), um Insights-Aggregattabellen zu generieren und so einen systematischen und automatisierten Ansatz bei der Datenverarbeitung sicherzustellen. Batch-Abfragen führen Abfragen aus `INSERT TABLE AS SELECT` und `CREATE TABLE AS SELECT`, um Daten zu bereinigen, zu formen, zu bearbeiten und anzureichern. Die Ergebnisse dieser Abfragen werden im Data Lake gespeichert.
1. **Laden aggregierter Einblicke:** Laden Sie die generierten aggregierten Einblicke in den beschleunigten Speicher und verwenden Sie SQL, um Abfragen zu testen, und stellen Sie die Genauigkeit und Effizienz des Datenabrufs sicher. Informationen dazu, wie Sie &quot;[stateless&quot;-Abfragen an den beschleunigten Speicher vornehmen](../../api/accelerated-queries.md), finden Sie in der Dokumentation.
1. **Zugriff und Integration:** Greifen Sie nahtlos auf die im beschleunigten Speicher gespeicherten Einblicke zu, indem Sie sie in Adobe Experience Platform [Benutzerdefinierte Dashboards](../../../dashboards/standard-dashboards.md) oder andere bevorzugte Business Intelligence-Tools (BI) integrieren. Diese Integrationen mit Clients von Drittanbietern ermöglichen ein kohärentes und intuitives Benutzererlebnis.

![Eine Infografik, die die vier Schritte zur SQL Insights-Anleitung in Data Distiller veranschaulicht.](../../images/data-distiller/sql-insights/steps-to-customizable-insights.png)

## Nächste Schritte

Durch Lesen dieses Dokuments verfügen Sie nun über ein besseres Verständnis der Anwendungsfälle, der wesentlichen Funktionen und der erforderlichen Schritte zur Entwicklung eines SQL Insights-Dashboards mit Data Distiller. Weitere Informationen zum Erstellen von maßgeschneiderten Berichtsdatenmodellen finden Sie im Leitfaden zum [Reporting-Einblicke-Datenmodell](./reporting-insights-data-model.md) .
