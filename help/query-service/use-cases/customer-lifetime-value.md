---
title: Verfolgen Sie Datensignale, um den Lebenszeitwert Ihrer Kunden zu generieren
description: Dieses Handbuch bietet eine umfassende Demonstration der Verwendung von Data Distiller und benutzerdefinierten Dashboards mit Real-time Customer Data Platform zur Messung und Visualisierung des Kundenlebenszeitwerts.
exl-id: c74b5bff-feb2-4e21-9ee4-1e0973192570
source-git-commit: ddf886052aedc025ff125c03ab63877cb049583d
workflow-type: tm+mt
source-wordcount: '1263'
ht-degree: 7%

---

# Verfolgen Sie Datensignale, um den Lebenszeitwert Ihrer Kunden zu generieren

Sie können Real-time Customer Data Platform verwenden, um den Kunden-Lebenszeitwert (CLV) zu verfolgen und diese Metrik mit benutzerdefinierten Dashboards zu visualisieren. Mithilfe von Data Distiller und benutzerdefinierten Dashboards können Sie messen, wie wertvoll ein Kunde für Ihr Unternehmen über die gesamte Beziehung hinweg ist. Wenn Sie den CLV kennen, können Sie die Strategien Ihres Unternehmens entwickeln, um neue Kunden zu gewinnen, während Sie die bestehenden beibehalten und die Gewinnmargen beibehalten.

Die folgende Infografik zeigt den Zyklus von Datenerfassung, -bearbeitung, -analyse und -aktivierung, der leistungsstarke Daten generiert, um Ihre Marketing-Kampagnen zu verbessern.

![Die Roundtrip-Infografik der Daten von Beobachtung über Analyse bis hin zu Aktion.](../images/use-cases/infographic-use-case-cycle.png)

Dieser End-to-End-Anwendungsfall zeigt, wie Datensignale erfasst und geändert werden können, um das abgeleitete Attribut für den Kundenlebenszeitwert zu berechnen. Diese abgeleiteten Datensätze können dann auf Ihre Real-Time CDP-Profildaten angewendet werden und stehen für die Verwendung mit benutzerdefinierten Dashboards zur Verfügung, um ein Dashboard für die Einsichtsanalyse zu erstellen. Über Data Distiller können Sie das Real-Time CDP-Insights-Datenmodell erweitern und die von CLV abgeleiteten Datensätze und Dashboard-Insights verwenden, um eine neue Audience zu erstellen und sie für ein gewünschtes Ziel zu aktivieren. Diese leistungsstarken Zielgruppen können dann für Ihre nächste Marketing-Kampagne verwendet werden.

Dieser Leitfaden soll Ihnen dabei helfen, Ihr Kundenerlebnis besser zu verstehen, indem Datensignale über wichtige Touchpoints hinweg gemessen werden, die CLV unterstützen, und einen ähnlichen Anwendungsfall in Ihrer Umgebung implementieren. Der gesamte Prozess wird in der folgenden Abbildung zusammengefasst.

![Eine Infografik der allgemeinen Schritte, die zur Nutzung des Kundenlebenszeitwerts erforderlich sind.](../images/use-cases/implementation-steps.png)

## Erste Schritte {#getting-started}

Dieses Handbuch setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Abfrage-](../home.md): Bietet eine Benutzeroberfläche und eine RESTful-API, in der Sie SQL-Abfragen verwenden können, um Ihre Daten zu analysieren und anzureichern.
* [Segmentierungs-](../../segmentation/home.md): Ermöglicht das Generieren von Zielgruppen aus Ihren Echtzeit-Kundenprofildaten.

## Voraussetzungen

Für dieses Handbuch müssen Sie die [Data Distiller](../data-distiller/overview.md) SKU als Teil Ihres Paketangebots haben. Wenn Sie sich nicht sicher sind, ob Sie über diese verfügen, wenden Sie sich an Ihren Adobe-Support-Mitarbeiter.

## Erstellen eines abgeleiteten Datensatzes {#create-derived-dataset}

Der erste Schritt bei der Erstellung Ihrer CLV besteht darin, einen abgeleiteten Datensatz aus den Datensignalen zu erstellen, die von Benutzeraktionen erfasst werden. Dieser spezielle Anwendungsfall wird in einem separaten Dokument über ein Treueprogramm für Fluggesellschaften erfasst. Informationen dazu, wie Sie mit dem [-Service dezilbasierte abgeleitete Datensätze für die Verwendung mit Ihren Profildaten erstellen, finden Sie im Handbuch ](./deciles-use-case.md) . Ausführliche Beispiele und Erläuterungen finden Sie im Dokument, in dem die folgenden Schritte erläutert werden:

* Erstellen Sie ein Schema, um Dezile-Bucketing zuzulassen.
* Verwenden Sie den Abfrage-Service, um Dezilen zu erstellen.
* Generieren von Dezildatensätzen.
* Aktivieren Sie das Schema zur Verwendung im Echtzeit-Kundenprofil.
* Erstellen Sie einen Identity-Namespace und markieren Sie ihn als primäre Kennung.
* Erstellen Sie eine Abfrage zur Berechnung von Dezilen über einen Lookback-Zeitraum.

## Erweitern des Insights-Datenmodells und Planen von Aktualisierungen {#extend-data-model-and-set-refresh-schedule}

Als Nächstes müssen Sie ein benutzerdefiniertes Datenmodell erstellen oder ein vorhandenes Adobe Real-Time CDP-Datenmodell erweitern, um mit Ihren CLV-Reporting-Insights interagieren zu können. Weitere Informationen finden Sie in der Dokumentation [ Erstellen eines Reporting-Insights-Datenmodells über den Abfrage-Service zur Verwendung mit beschleunigten Speicherdaten und benutzerdefinierten Dashboards](../data-distiller/sql-insights/reporting-insights-data-model.md#build-a-reporting-insights-data-model). Das Tutorial umfasst die folgenden Schritte:

* Erstellen Sie mit Data Distiller ein Modell für Reporting-Insights.
* Erstellen von Tabellen und Beziehungen und Auffüllen von Daten
* Abfragen des Reporting-Insights-Datenmodells.
* Erweitern Ihres Datenmodells mit dem Real-Time CDP Insights-Datenmodell.
* Erstellen Sie Dimensionstabellen, um Ihr Reporting-Insights-Modell zu erweitern.
* Abfragen Ihres erweiterten Reporting-Insights-Datenmodells mit beschleunigtem Speicher

Siehe die Dokumentation zum Insights-Datenmodell von Real-Time Customer Data Platform, um zu erfahren, wie Sie [Ihre SQL-Abfragevorlagen anpassen können, um Real-Time CDP-Berichte für Ihre Marketing- und KPI-Anwendungsfälle zu erstellen.](../../dashboards/data-models/cdp-insights-data-model-b2c.md).

Stellen Sie sicher, dass Sie einen Zeitplan festlegen, um Ihr benutzerdefiniertes Datenmodell regelmäßig zu aktualisieren. Dadurch wird sichergestellt, dass die Daten bei Bedarf als Teil der Aufnahme-Pipeline zurückgegeben werden und die benutzerdefinierten Dashboards gefüllt werden. Informationen zum Einrichten [ Zeitplans finden ](../ui/query-schedules.md#create-schedule) im Handbuch zum Planen von Abfragen .

## Erstellen eines Dashboards zur Erfassung von Insights {#build-a-custom-dashboard}

Nachdem Sie Ihr benutzerdefiniertes Datenmodell erstellt haben, können Sie Ihre Daten mit benutzerdefinierten Abfragen und benutzerdefinierten Dashboards visualisieren. Vollständige Anleitungen zum Erstellen eines benutzerdefinierten Dashboards finden Sie in der Übersicht [ benutzerdefinierten Dashboards ](../../dashboards/standard-dashboards.md). Das Handbuch zur Benutzeroberfläche enthält Details zu:

* Erstellen eines Widgets.
* Verwendung des Widget-Composers.

Beispiele für benutzerdefinierte CLV-Widgets, die Dezil-Buckets verwenden, finden Sie unten.

![Eine Sammlung benutzerdefinierter dezilbasierter CLTV-Widgets.](../images/use-cases/deciles-user-defined-dashboard.png)

## Erstellen und Aktivieren von leistungsstarken Zielgruppen {#create-and-activate-audiences}

Der nächste Schritt besteht darin, eine Segmentdefinition zu erstellen und Zielgruppen aus Ihren Echtzeit-Kundenprofildaten zu generieren. Informationen zum Erstellen und Aktivieren von Zielgruppen in Platform [ Sie im Handbuch zur Segment Builder](../../segmentation/ui/segment-builder.md)Benutzeroberfläche . Das Handbuch enthält Abschnitte zu folgenden Themen:

* Segmentdefinitionen mit einer Kombination aus Attributen, Ereignissen und vorhandenen Zielgruppen als Bausteinen erstellen.
* Verwenden Sie die Arbeitsfläche und Container des Regel-Builders, um die Reihenfolge zu steuern, in der die Segmentierungsregeln ausgeführt werden.
* Schätzungen der voraussichtlichen Zielgruppe anzeigen, sodass Sie Ihre Segmentdefinitionen nach Bedarf anpassen können.
* Alle Segmentdefinitionen für geplante Segmentierung aktivieren.
* Spezifische Segmentdefinitionen für Streaming-Segmentierung aktivieren.

Alternativ steht auch ein [Segment Builder-Video-Tutorial](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-segments.html) zur Verfügung, um weitere Informationen zu erhalten.

## Aktivieren Ihrer Audience für eine E-Mail-Kampagne {#activate-audience-for-campaign}

Nachdem Sie Ihre Zielgruppe erstellt haben, können Sie sie für ein Ziel aktivieren. Platform unterstützt eine Vielzahl von E-Mail-Service-Anbietern (ESPs), mit denen Sie Ihre E-Mail-Marketing-Aktivitäten verwalten können, z. B. E-Mail-Kampagnen zu Werbezwecken.

Unter [E-Mail-Marketing-Ziele - ](../../destinations/catalog/email-marketing/overview.md#connect-destination) finden Sie eine Liste der unterstützten Ziele, an die Sie Daten exportieren möchten (z. B. die Seite [Oracle Eloqua](../../destinations/catalog/email-marketing/oracle-eloqua-api.md)).

## Anzeigen der von Ihrer Kampagne zurückgegebenen Analysedaten {#post-campaign-data-analysis}

Die Daten aus Quellen können jetzt [inkrementell verarbeitet](../key-concepts/incremental-load.md) als Teil einer geplanten Aktualisierung Ihres Datenmodells im beschleunigten Datenspeicher. Alle Antwortereignisse von Kunden können direkt oder in Batches in Adobe Experience Platform aufgenommen werden. Ihr Datenmodell kann einmal oder mehrmals täglich aktualisiert werden, je nach Ihren Einstellungen oder Quell-Connectoren. Weitere Informationen finden [ in der ](../../ingestion/batch-ingestion/api-overview.md) zur Batch[Aufnahme-API oder ](../../ingestion/streaming-ingestion/overview.md) Streaming-Aufnahme .

Sobald Ihr Datenmodell aktualisiert wurde, liefern Ihre benutzerdefinierten Dashboard-Widgets aussagekräftige Signale, mit denen Sie den Kundenlebenszeitwert messen und visualisieren können.

![Ein benutzerdefiniertes Widget, mit dem die Anzahl der geöffneten E-Mails entsprechend ihrer Audience und E-Mail-Kampagne angezeigt wird.](../images/use-cases/post-activation-and-email-response-kpis.png)

Für Ihre benutzerdefinierte Analyse stehen verschiedene Visualisierungsoptionen zur Verfügung.

![Das Widget „Von Kampagnen-Buckets geöffnete E-Mails“.](../images/use-cases/email-opened-by-campaign-buckets.png)

Diese Erkenntnisse können Ihnen wiederum dabei helfen, Ihre Geschäftsstrategien für nachfolgende Kampagnen zu entwickeln.

![Eine Sammlung von vier benutzerdefinierten Widgets, die die Ergebnisse der E-Mail-Kampagne detailliert beschreiben.](../images/use-cases/example-widgets.png)

## Nächste Schritte

Durch das Lesen dieses Dokuments sollten Sie besser verstehen, wie Sie mit Real-time Customer Data Platform die Metrik des Kundenlebenszeitwerts (Customer Lifetime Value, CLV) verfolgen und visualisieren können. Um mehr über die vielen geschäftlichen Anwendungsfälle zu erfahren, die über Query Service und Experience Platform abgedeckt werden, sollten Sie die folgenden Dokumente lesen:

* [Ein Beispiel, das von Anfang bis Ende zeigt, wie vielseitig und vorteilhaft Query Service ist.](./abandoned-browse.md)
* [Verwendung des Abfrage-Service und des maschinellen Lernens zum Ermitteln und Filtern der Bot-Aktivität aus dem echten Online-Besucher-Traffic einer Website](./bot-filtering.md)
* [Erfahren Sie, wie Sie eine Übereinstimmung für Ihre Platform-Daten durchführen, die Ergebnisse aus mehreren Datensätzen kombiniert, indem Sie ungefähr mit einer Zeichenfolge Ihrer Wahl übereinstimmen.](./fuzzy-match.md)

<!-- "Data signals are actions taken by consumers while online that offer clues about intent that can be acted upon. This includes anything from visiting a website to filling out a change of address or clicking an ad."  -->

<!-- "Customer touchpoints are your brand's points of customer contact, from start to finish." -->
