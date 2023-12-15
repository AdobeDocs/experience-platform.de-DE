---
title: Anpassbare Insights
description: Erfahren Sie mehr über die Anwendungsfälle, wichtigen Funktionen und erforderlichen Schritte zur Entwicklung eines anpassbaren Einblicke-Dashboards mit Data Distiller. Erfahren Sie, wie die anpassbare Insights-Funktion in Data Distiller die Transparenz verbessert und betriebliche Einblicke in verschiedene Dimensionen wie Profile, Zielgruppen, Kampagnen, Journey, Berechtigungen und Einverständniserklärungen erhält.
source-git-commit: 18c1d32bbc2732c38a9c37ee8fb9d36a23d4e515
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 5%

---

# Anpassbare Insights

Erstellen Sie maßgeschneiderte Berichtsdatenmodelle, um tiefere Einblicke zu gewinnen, Strategien zu optimieren und Analysen an bestimmte Geschäftsanforderungen anzupassen. Dazu nutzen Sie die anpassbaren Einblicke von Data Distiller. Verwenden Sie die Funktion &quot;Anpassbare Einblicke&quot;, um die Transparenz zu erhöhen und operative Einblicke aus Ihren Adobe Experience Platform-Daten über Dimensionen wie Profile, Zielgruppen, Kampagnen, Journey, Berechtigungen und Einverständniserklärungen hinweg zu gewinnen. Diese Funktion bietet eine vielseitige, adaptive Lösung, um die Berichtsdatenmodelle Ihres Unternehmens an Ihre spezifischen Geschäftsanforderungen anzupassen.

In diesem Dokument werden die Anwendungsfälle, grundlegenden Funktionen und erforderlichen Schritte zum Entwickeln eines anpassbaren Einblicke-Dashboards mit Data Distiller beschrieben.

## Voraussetzungen

In diesem Tutorial werden benutzerdefinierte Dashboards verwendet, um Daten aus Ihrem benutzerdefinierten Datenmodell innerhalb der Platform-Benutzeroberfläche zu visualisieren. Siehe [Dokumentation zu benutzerdefinierten Dashboards](../../../dashboards/user-defined-dashboards.md) , um mehr über diese Funktion zu erfahren.

## Erste Schritte

Die Data Distiller SKU ist erforderlich, um ein benutzerdefiniertes Datenmodell für Ihre Reporting-Insights zu erstellen und um die Real-Time CDP-Datenmodelle zu erweitern, die angereicherte Platform-Daten enthalten. Siehe [Verpackung](../../packaging.md), [Limits](../../guardrails.md#query-accelerated-store), und  [Lizenz](../../data-distiller/license-usage.md) Dokumentation, die sich auf die Data Distiller SKU bezieht. Wenn Sie nicht über die Data Distiller-SKU verfügen, wenden Sie sich für weitere Informationen an Ihren Adobe-Kundenbetreuer.

## Anwendungsfälle für anpassbare Insights {#use-cases}

Im Folgenden finden Sie gängige Anwendungsfälle, die effektiv über anpassbare Insights in Data Distiller adressiert werden können.

### Transparenz der Profil- und Zielgruppennutzung {#usage-transparency}

**Herausforderung:** Aufschlüsseln der KPIs (Key Performance Indicators) nach bestimmten Kriterien wie Geschäftseinheiten, Treuestatus oder Customer Lifetime Value (CLTV).

**Anpassbare Insights-Lösung:** Data Distiller ermöglicht die Erweiterung der Berichtsdatenmodelle in Adobe Experience Platform und erleichtert damit [Hinzufügen benutzerdefinierter Profilattribute wie CLTV](../../use-cases/customer-lifetime-value.md) oder Treuestatus.

### Tracking von Einverständnisanomalien {#consent-anomaly-tracking}

**Herausforderung:** Anwenden von Zielgruppenüberschneidungen und der Größe von Trendzeilenberichten auf benutzerdefinierte Zustimmungsattribute für Kanäle wie E-Mail, SMS und Telefon.

**Anpassbare Insights-Lösung:** Das Berichtsdatenmodell kann erweitert werden, um Änderungen bei Zustimmungsvoreinstellungen im Laufe der Zeit zu verfolgen. Dazu gehört das Erstellen zusätzlicher Fakten- und Dimensionstabellen zum Trend von Zustimmungseinstellungen und -zeitplänen [inkrementelle Datenaktualisierung](../../key-concepts/incremental-load.md).

### Optimieren der Zielgruppensegmentierungsstrategie {#optimize-audience-segmentation-strategy}

**Herausforderung:** So integrieren Sie modellgenerierte Tendenzwerte für maschinelles Lernen (ML) in ihre KPI-Berichte für Zielgruppen.

**Anpassbare Insights-Lösung:** Data Distiller ermöglicht die Einbeziehung von [Tendenzwerte aus benutzerdefinierten ML-Modellen](../../use-cases/propensity-score.md), wodurch die Berechnung der aggregierten Werte auf Zielgruppenebene erleichtert wird. Diese Daten können dann zusammen mit standardmäßigen KPIs gemeldet werden.

### Zielgruppenerweiterung {#audience-expansion}

**Herausforderung:** So lassen sich mehr als nur Profilzahlen in Zielgruppenüberschneidungsberichten erfassen und zusätzliche demografische Daten oder Voreinstellungen erhalten, um Zielgruppenerweiterungsstrategien zu steuern.

**Anpassbare Insights-Lösung:** Durch Erweiterung des Berichtsdatenmodells können Benutzer zusätzliche Profilattribute einbinden, wodurch der Bericht zur Zielgruppenüberschneidung mit relevanten demografischen Daten und Voreinstellungen angereichert wird.

## Wichtige Funktionen zum Generieren von anpassbaren Insights {#key-capabilities}

In der folgenden Abbildung werden einige wichtige Funktionen zum Generieren von anpassbaren Insights hervorgehoben. Zu diesen Funktionen gehören:

1. **Datenvisualisierungen:** Einbeziehen visueller Elemente wie Trends und Balkendiagramme für eine umfassende Übersicht über Datentrends.
1. **Dashboard-Authoring:** Die Erstellung benutzerdefinierter Dashboards, die auf bestimmte Anwendungsfälle zugeschnitten sind, ermöglicht eine personalisiertere und zielgerichtetere Analyse.
1. **Flexible SQL-Datenmodellierung:** Verwenden Sie einen vielseitigen SQL-Datenmodellierungsansatz, der es Benutzern ermöglicht, verschiedene Datensätze nahtlos zu kombinieren und zu bearbeiten, wodurch die Anpassungsfähigkeit und Analysetiefe verbessert werden.
1. **Accelerated Store:** Implementierung eines beschleunigten Speichermechanismus, um aggregierte Einblicke effizient über SQL bereitzustellen und so einen optimierten und schnellen Zugriff auf wertvolle Informationen zu gewährleisten.
1. **BI-Verbindung:** Erleichterung der nahtlosen Integration mit gängigen Business Intelligence-Tools (BI), einschließlich Power BI, Tableau, Looker und Apache Superset. Diese Konnektivität stellt die Kompatibilität mit verschiedenen BI-Umgebungen sicher und bietet Anwendern die Flexibilität, ihr bevorzugtes Tool für detaillierte Analysen und Berichte zu verwenden.

![Visuelle Darstellungen der wichtigsten Funktionen von Data Distillers anpassbaren Insights.](../../images/data-distiller/customizable-insights/key-capabilities-of-customizable-insights.png)

## Schritte zum Erstellen von anpassbaren Insights {#steps-to-create}

Gehen Sie wie folgt vor, um in Data Distiller ein Dashboard mit anpassbaren Insights zu entwickeln.

1. **Ad-hoc-Abfrageerforschung:** Starten durch Ausführen von Ad-hoc `SELECT` Abfragen zur Erforschung von Rohdaten im Data Lake. Dies ermöglicht eine spontane, explorative Datenanalyse zum Experimentieren und Validieren von Daten, in denen die Ergebnisse der Abfragen nicht im Data Lake gespeichert sind.
1. **Nutzung der Batch-Abfrage:** Verwenden Sie Batch-Abfragen, um [Erstellen geplanter Aufträge](../../api/scheduled-queries.md#create-a-new-scheduled-query) für die Generierung von Insights-Aggregattabellen, wodurch ein systematischer und automatisierter Ansatz bei der Datenverarbeitung gewährleistet wird. Ausführung von Batch-Abfragen `INSERT TABLE AS SELECT` und `CREATE TABLE AS SELECT` Abfragen zum Bereinigen, Gestalten, Bearbeiten und Anreichern von Daten. Die Ergebnisse dieser Abfragen werden im Data Lake gespeichert.
1. **Aggregiertes Laden von Einblicken:** Laden Sie die generierten aggregierten Einblicke in den beschleunigten Speicher und verwenden Sie SQL, um Abfragen zu testen und die Genauigkeit und Effizienz des Datenabrufs sicherzustellen. Erfahren Sie mehr über [stateless Abfragen an den beschleunigten Speicher erstellen](../../api/accelerated-queries.md), siehe die Dokumentation.
1. **Zugriff und Integration:** Greifen Sie durch die Integration mit Adobe Experience Platform nahtlos auf die im beschleunigten Speicher gespeicherten Einblicke zu [Benutzerdefinierte Dashboards](../../../dashboards/user-defined-dashboards.md) oder anderen bevorzugten Business Intelligence-Tools (BI). Diese Integrationen mit Clients von Drittanbietern ermöglichen ein kohärentes und intuitives Benutzererlebnis.

![Eine Infografik, die die vier Schritte zum Anpassen von Insights in Data Distiller veranschaulicht.](../../images/data-distiller/customizable-insights/steps-to-customizable-insights.png)

## Nächste Schritte

Durch Lesen dieses Dokuments verfügen Sie jetzt über ein besseres Verständnis der Anwendungsfälle, wesentlichen Funktionen und erforderlichen Schritte zur Entwicklung eines anpassbaren Einblicke-Dashboards mit Data Distiller. Weitere Informationen zum Erstellen von maßgeschneiderten Berichtsdatenmodellen finden Sie unter [Leitfaden zum Reporting-Insights-Datenmodell](./reporting-insights-data-model.md).
