---
title: Anpassbare Insights
description: Erfahren Sie mehr über die Anwendungsfälle, wichtigen Funktionen und erforderlichen Schritte zur Entwicklung eines anpassbaren Einblicke-Dashboards mit Data Distiller. Erfahren Sie, wie die anpassbare Insights-Funktion in Data Distiller die Transparenz verbessert und betriebliche Einblicke in verschiedene Dimensionen wie Profile, Zielgruppen, Kampagnen, Journey, Berechtigungen und Einverständniserklärungen erhält.
exl-id: f807d0fd-c8ec-42d4-96a0-5ffc5681943b
source-git-commit: bb95e0aa8ee92aee5a2f126d85e78308e652a061
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 5%

---

# Anpassbare Insights

Erstellen Sie maßgeschneiderte Berichtsdatenmodelle, um tiefere Einblicke zu gewinnen, Strategien zu optimieren und Analysen an bestimmte Geschäftsanforderungen anzupassen. Dazu nutzen Sie die anpassbaren Einblicke von Data Distiller. Verwenden Sie die Funktion &quot;Anpassbare Einblicke&quot;, um die Transparenz zu erhöhen und operative Einblicke aus Ihren Adobe Experience Platform-Daten über Dimensionen wie Profile, Zielgruppen, Kampagnen, Journey, Berechtigungen und Einverständniserklärungen hinweg zu gewinnen. Diese Funktion bietet eine vielseitige, adaptive Lösung, um die Berichtsdatenmodelle Ihres Unternehmens an Ihre spezifischen Geschäftsanforderungen anzupassen.

Um Ihre anpassbaren Einblicke ](../../../dashboards/data-distiller/overview.md) zu visualisieren, können Sie mit dem [Abfragepro-Modus](../../../dashboards/data-distiller/customizable-insights/query-pro-mode.md) komplexe Analysen mit benutzerdefinierten SQL-Abfragen durchführen und Ihre Daten in leicht verständliche Diagramme umwandeln. [ Verwenden Sie den Abfragepro-Modus, um individuelle Einblicke und Visualisierungen in Ihren Dashboards zu erstellen und sowohl technische als auch nicht technische Zielgruppen zu berücksichtigen, indem Sie Ihre Einblicke als CSV-Dateien herunterladen.

In diesem Dokument werden die Anwendungsfälle, grundlegenden Funktionen und erforderlichen Schritte zum Entwickeln eines anpassbaren Einblicke-Dashboards mit Data Distiller beschrieben.

## Voraussetzungen

In diesem Tutorial werden benutzerdefinierte Dashboards verwendet, um Daten aus Ihrem benutzerdefinierten Datenmodell innerhalb der Platform-Benutzeroberfläche zu visualisieren. Weitere Informationen zu dieser Funktion finden Sie in der Dokumentation zu [benutzerdefinierten Dashboards](../../../dashboards/user-defined-dashboards.md) .

## Erste Schritte

Die Data Distiller SKU ist erforderlich, um ein benutzerdefiniertes Datenmodell für Ihre Reporting-Insights zu erstellen und um die Real-Time CDP-Datenmodelle zu erweitern, die angereicherte Platform-Daten enthalten. Weitere Informationen finden Sie in der Dokumentation zu [packaging](../../packaging.md), [guardrails](../../guardrails.md#query-accelerated-store) und [licensing](../../data-distiller/license-usage.md) , die sich auf die Data Distiller SKU bezieht. Wenn Sie nicht über die Data Distiller-SKU verfügen, wenden Sie sich für weitere Informationen an Ihren Adobe-Kundenbetreuer.

## Anwendungsfälle für anpassbare Insights {#use-cases}

Im Folgenden finden Sie gängige Anwendungsfälle, die effektiv über anpassbare Insights in Data Distiller adressiert werden können.

### Transparenz der Profil- und Zielgruppennutzung {#usage-transparency}

**Herausforderung:** Aufschlüsseln der KPIs (Key Performance Indicators) nach bestimmten Kriterien wie Geschäftseinheiten, Treuestatus oder Customer Lifetime Value (CLTV).

**Anpassbare Insights-Lösung:** Data Distiller ermöglicht die Erweiterung der Berichtsdatenmodelle in Adobe Experience Platform, wodurch [ benutzerdefinierte Profilattribute wie CLTV](../../use-cases/customer-lifetime-value.md) oder der Treuestatus hinzugefügt werden können.

### Tracking von Einverständnisanomalien {#consent-anomaly-tracking}

**Herausforderung:** Anleitung zum Anwenden von Zielgruppenüberschneidungen und zur Größenanpassung von Trendzeilenberichten auf benutzerdefinierte Zustimmungsattribute für Kanäle wie E-Mail, SMS und Telefon.

**Anpassbare Insights-Lösung:** Das Berichtsdatenmodell kann erweitert werden, um Änderungen an Zustimmungseinstellungen im Laufe der Zeit zu verfolgen. Dazu gehört das Erstellen zusätzlicher Fakten- und Dimensionstabellen zum Trend von Zustimmungsvoreinstellungen und zum Planen der [inkrementellen Datenaktualisierung](../../key-concepts/incremental-load.md).

### Optimieren der Zielgruppensegmentierungsstrategie {#optimize-audience-segmentation-strategy}

**Herausforderung:** Wie integrieren Sie modellgenerierte Tendenzwerte für maschinelles Lernen (ML) in ihre KPI-Berichte für Zielgruppen.

**Anpassbare Insights-Lösung:** Data Distiller ermöglicht die Einbeziehung von [Propensity Scores aus benutzerdefinierten ML-Modellen](../../use-cases/propensity-score.md), wodurch die Berechnung der aggregierten Werte auf Zielgruppenebene erleichtert wird. Diese Daten können dann zusammen mit standardmäßigen KPIs gemeldet werden.

### Zielgruppenerweiterung {#audience-expansion}

**Herausforderung:** Wie Sie mehr als nur Profilzahlen in Zielgruppenüberschneidungsberichten abrufen und zusätzliche demografische Daten oder Voreinstellungen erhalten, um Zielgruppenerweiterungsstrategien zu steuern.

**Anpassbare Insights-Lösung:** Durch Erweiterung des Berichtsdatenmodells können Benutzer zusätzliche Profilattribute einbinden und den Bericht zur Zielgruppenüberschneidung mit relevanten demografischen Daten und Voreinstellungen anreichern.

## Wichtige Funktionen zum Generieren von anpassbaren Insights {#key-capabilities}

In der folgenden Abbildung werden einige wichtige Funktionen zum Generieren von anpassbaren Insights hervorgehoben. Zu diesen Funktionen gehören:

1. **Datenvisualisierungen:** Einbeziehen visueller Elemente wie Trends und Balkendiagramme für eine umfassende Ansicht von Datentrends.
1. **Dashboard-Authoring:** Aktivierung der Erstellung benutzerdefinierter Dashboards, die auf bestimmte Anwendungsfälle zugeschnitten sind, und Bereitstellung eines personalisierteren und gezielteren Analyseerlebnisses.
1. **Flexible SQL-Datenmodellierung:** Verwenden Sie einen vielseitigen SQL-Datenmodellierungsansatz, der es Benutzern ermöglicht, verschiedene Datensätze nahtlos zu kombinieren und zu bearbeiten, wodurch Anpassungsfähigkeit und Analysetiefe verbessert werden.
1. **Beschleuniger Speicher:** Implementierung eines beschleunigten Speichermechanismus, um aggregierte Einblicke effizient über SQL bereitzustellen und so einen optimierten und schnellen Zugriff auf wertvolle Informationen zu gewährleisten.
1. **BI-Konnektivität:** Erleichterung der nahtlosen Integration mit gängigen Business Intelligence-Tools (BI), einschließlich Power BI, Tableau, Looker und Apache Superset. Diese Konnektivität stellt die Kompatibilität mit verschiedenen BI-Umgebungen sicher und bietet Anwendern die Flexibilität, ihr bevorzugtes Tool für detaillierte Analysen und Berichte zu verwenden.

![ Visuelle Darstellungen der wichtigsten Funktionen von Data Distillers anpassbaren Einblicken.](../../images/data-distiller/customizable-insights/key-capabilities-of-customizable-insights.png)

## Schritte zum Erstellen von anpassbaren Insights {#steps-to-create}

Gehen Sie wie folgt vor, um in Data Distiller ein Dashboard mit anpassbaren Insights zu entwickeln.

1. **Ad-hoc-Abfrageerforschung:** Beginnen Sie mit der Ausführung von Ad-hoc-Abfragen `SELECT`, um Rohdaten im Data Lake zu untersuchen. Dies ermöglicht eine spontane, explorative Datenanalyse zum Experimentieren und Validieren von Daten, in denen die Ergebnisse der Abfragen nicht im Data Lake gespeichert sind.
1. **Nutzung der Batch-Abfrage:** Verwenden Sie Batch-Abfragen, um [geplante Aufträge zu erstellen](../../api/scheduled-queries.md#create-a-new-scheduled-query), um Insights-Aggregattabellen zu generieren und so einen systematischen und automatisierten Ansatz bei der Datenverarbeitung sicherzustellen. Batch-Abfragen führen Abfragen aus `INSERT TABLE AS SELECT` und `CREATE TABLE AS SELECT`, um Daten zu bereinigen, zu formen, zu bearbeiten und anzureichern. Die Ergebnisse dieser Abfragen werden im Data Lake gespeichert.
1. **Laden aggregierter Einblicke:** Laden Sie die generierten aggregierten Einblicke in den beschleunigten Speicher und verwenden Sie SQL, um Abfragen zu testen, und stellen Sie die Genauigkeit und Effizienz des Datenabrufs sicher. Informationen dazu, wie Sie &quot;[stateless&quot;-Abfragen an den beschleunigten Speicher vornehmen](../../api/accelerated-queries.md), finden Sie in der Dokumentation.
1. **Zugriff und Integration:** Greifen Sie nahtlos auf die im beschleunigten Speicher gespeicherten Einblicke zu, indem Sie sie in Adobe Experience Platform [Benutzerdefinierte Dashboards](../../../dashboards/user-defined-dashboards.md) oder andere bevorzugte Business Intelligence-Tools (BI) integrieren. Diese Integrationen mit Clients von Drittanbietern ermöglichen ein kohärentes und intuitives Benutzererlebnis.

![Eine Infografik, die die vier Schritte zum Anpassen von Insights in Data Distiller veranschaulicht.](../../images/data-distiller/customizable-insights/steps-to-customizable-insights.png)

## Nächste Schritte

Durch Lesen dieses Dokuments verfügen Sie jetzt über ein besseres Verständnis der Anwendungsfälle, wesentlichen Funktionen und erforderlichen Schritte zur Entwicklung eines anpassbaren Einblicke-Dashboards mit Data Distiller. Weitere Informationen zum Erstellen von maßgeschneiderten Berichtsdatenmodellen finden Sie im Leitfaden zum [Reporting-Einblicke-Datenmodell](./reporting-insights-data-model.md) .
