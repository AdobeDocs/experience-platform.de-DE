---
title: Tracking von Datensignalen zur Generierung Ihres Kundenlebenszeitwerts
description: Dieses Handbuch bietet eine umfassende Demonstration zur Verwendung von Data Distiller und benutzerdefinierten Dashboards mit Real-time Customer Data Platform zur Messung und Visualisierung des Kundenlebenszeitwerts.
exl-id: c74b5bff-feb2-4e21-9ee4-1e0973192570
source-git-commit: e0af1f0110ceb514a5b249c42a05bf780ea834c6
workflow-type: tm+mt
source-wordcount: '1263'
ht-degree: 7%

---

# Tracking von Datensignalen zur Generierung Ihres Kundenlebenszeitwerts

Sie können Real-time Customer Data Platform verwenden, um den Kundenlebenszeitwert (CLV) zu verfolgen und diese Metrik mit benutzerdefinierten Dashboards zu visualisieren. Mithilfe von Data Distiller und benutzerdefinierten Dashboards können Sie messen, wie wertvoll ein Kunde für Ihr Unternehmen in der gesamten Beziehung ist. Die Kenntnis des CLV kann Ihnen dabei helfen, die Strategien Ihres Unternehmens zu entwickeln, um neue Kunden zu gewinnen und gleichzeitig die bestehenden zu behalten und Gewinnspannen zu halten.

Die folgende Infografik zeigt den Zyklus der Datenerfassung, -bearbeitung, -analyse und -nutzung, der leistungsstarke Daten zur Verbesserung Ihrer Marketing-Kampagnen generiert.

![Die Rundreise informiert über Daten von Beobachtung über Analyse bis zum Handeln.](../images/use-cases/infographic-use-case-cycle.png)

Dieser durchgängige Anwendungsfall zeigt, wie Datensignale erfasst und geändert werden können, um das abgeleitete Attribut für den Kundenlebenszeitwert zu berechnen. Diese abgeleiteten Datensätze können dann auf Ihre Real-Time CDP-Profildaten angewendet werden und können mit benutzerdefinierten Dashboards verwendet werden, um ein Dashboard für die Insight-Analyse zu erstellen. Über Data Distiller können Sie das Real-Time CDP Insight-Datenmodell erweitern und mithilfe der von CLV abgeleiteten Datensätze und Dashboard-Einblicke eine neue Zielgruppe erstellen und für ein gewünschtes Ziel aktivieren. Diese leistungsstarken Zielgruppen können dann zur Unterstützung Ihrer nächsten Marketing-Kampagne verwendet werden.

Dieses Handbuch soll Ihnen dabei helfen, Ihr Kundenerlebnis besser zu verstehen, indem Sie Datensignale über wichtige Touchpoints hinweg messen, die CLV steuern und einen ähnlichen Anwendungsfall in Ihrer Umgebung implementieren. Der gesamte Prozess wird in der Abbildung unten zusammengefasst.

![Eine Infografik der umfassenden Schritte, die zur Nutzung des Lebenszeitwerts von Kunden erforderlich sind.](../images/use-cases/implementation-steps.png)

## Erste Schritte {#getting-started}

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Query Service](../home.md): Bietet eine Benutzeroberfläche und eine RESTful-API, mit der Sie SQL-Abfragen zur Analyse und Anreicherung Ihrer Daten verwenden können.
* [Segmentierungsdienst](../../segmentation/home.md): Ermöglicht das Generieren von Zielgruppen aus Ihren Echtzeit-Kundenprofildaten.

## Voraussetzungen

Für dieses Handbuch benötigen Sie die [Data Distiller](../data-distiller/overview.md) SKU als Teil Ihres Paketangebots. Wenden Sie sich an Ihren Adobe-Kundenbetreuer, wenn Sie sich nicht sicher sind, ob Sie über dieses Angebot verfügen.

## abgeleiteten Datensatz erstellen {#create-derived-dataset}

Der erste Schritt bei der Erstellung Ihrer CLV besteht darin, einen abgeleiteten Datensatz aus den von Benutzeraktionen erfassten Datensignalen zu erstellen. Dieser besondere Anwendungsfall wird in einem separaten Dokument über ein Treueprogramm für Fluggesellschaften erfasst. Weitere Informationen finden Sie im Handbuch . [Verwenden Sie Query Service , um dezimalbasierte abgeleitete Datensätze für die Verwendung mit Ihren Profildaten zu erstellen.](./deciles-use-case.md). Vollständige Beispiele und Erläuterungen zu den folgenden Schritten finden Sie im Dokument:

* Erstellen Sie ein Schema, das die Dezile-Bucketing ermöglicht.
* Verwenden Sie Query Service zum Erstellen von Dezimalstellen.
* Generieren von Dezimaldatensätzen.
* Aktivieren Sie das Schema zur Verwendung im Echtzeit-Kundenprofil.
* Erstellen Sie einen Identitäts-Namespace und markieren Sie ihn als primäre Kennung.
* Erstellen Sie eine Abfrage zur Berechnung der Dezimalzahlen über einen Lookback-Zeitraum.

## Erweitern des Insight-Datenmodells und Planen von Aktualisierungen {#extend-data-model-and-set-refresh-schedule}

Als Nächstes müssen Sie ein benutzerdefiniertes Datenmodell erstellen oder ein vorhandenes Adobe Real-Time CDP-Datenmodell erweitern, um mit Ihren CLV-Berichtseinblicken zu interagieren. Weitere Informationen finden Sie in der Dokumentation . [Erstellen eines Datenmodells mit Berichtseinblicken über Query Service zur Verwendung mit beschleunigten Speicherdaten und benutzerdefinierten Dashboards](../data-distiller/customizable-insights/reporting-insights-data-model.md#build-a-reporting-insights-data-model). Das Tutorial umfasst die folgenden Schritte:

* Erstellen Sie ein Modell für die Berichterstellung von Einblicken mit Data Distiller.
* Erstellen Sie Tabellen, Beziehungen und füllen Sie Daten aus.
* Abfragen des Reporting-Insight-Datenmodells.
* Erweitern Sie Ihr Datenmodell mit dem Real-Time CDP Insight-Datenmodell.
* Erstellen Sie Dimensionstabellen, um Ihr Reporting-Insights-Modell zu erweitern.
* Abfragen Ihres erweiterten Reporting-Insights-Datenmodells mit beschleunigtem Speicher

Siehe die Dokumentation zum Insights-Datenmodell von Real-Time Customer Data Platform, um zu erfahren, wie Sie [Ihre SQL-Abfragevorlagen anpassen können, um Real-Time CDP-Berichte für Ihre Marketing- und KPI-Anwendungsfälle zu erstellen.](../../dashboards/data-models/cdp-insights-data-model-b2c.md).

Stellen Sie sicher, dass Sie einen Zeitplan festlegen, um Ihr benutzerdefiniertes Datenmodell in einem normalen Cadence zu aktualisieren. Dadurch wird sichergestellt, dass die Daten bei Bedarf im Rahmen Ihrer Aufnahme-Pipeline zurückgesendet und Ihre benutzerdefinierten Dashboards gefüllt werden. Siehe [Planen von Abfragen](../ui/query-schedules.md#create-schedule) , um zu erfahren, wie Sie Ihren Zeitplan einrichten.

## Erstellen eines Dashboards zum Erfassen von Einblicken {#build-a-custom-dashboard}

Nachdem Sie Ihr benutzerdefiniertes Datenmodell erstellt haben, können Sie Ihre Daten mit benutzerdefinierten Abfragen und benutzerdefinierten Dashboards visualisieren. Umfassende Hinweise zur Verwendung finden Sie in der Übersicht über benutzerdefinierte Dashboards . [Erstellen eines benutzerdefinierten Dashboards](../../dashboards/user-defined-dashboards.md). Das UI-Handbuch enthält Details zu:

* So erstellen Sie ein Widget.
* Verwendung des Widget Composers.

Nachfolgend finden Sie Beispiele für benutzerdefinierte CLV-Widgets, die Dezimalgruppen verwenden.

![Eine Sammlung von benutzerdefinierten dezimalbasierten CLTV-Widgets.](../images/use-cases/deciles-user-defined-dashboard.png)

## Hochleistungszielgruppen erstellen und aktivieren {#create-and-activate-audiences}

Der nächste Schritt besteht darin, eine Segmentdefinition zu erstellen und Zielgruppen aus Ihren Echtzeit-Kundenprofildaten zu generieren. Weitere Informationen finden Sie im Handbuch zur Benutzeroberfläche von Segment Builder . [Erstellen und Aktivieren von Zielgruppen in Platform](../../segmentation/ui/segment-builder.md). Das Handbuch enthält Abschnitte zu folgenden Themen:

* Segmentdefinitionen mit einer Kombination aus Attributen, Ereignissen und vorhandenen Zielgruppen als Bausteinen erstellen.
* Verwenden Sie die Arbeitsfläche des Regel-Builders und Container, um die Reihenfolge zu steuern, in der die Segmentierungsregeln ausgeführt werden.
* Schätzungen der voraussichtlichen Zielgruppe anzeigen, sodass Sie Ihre Segmentdefinitionen nach Bedarf anpassen können.
* Alle Segmentdefinitionen für geplante Segmentierung aktivieren.
* Spezifische Segmentdefinitionen für Streaming-Segmentierung aktivieren.

Alternativ kann auch eine [Video-Tutorial zum Segment Builder](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-segments.html) für weitere Informationen verfügbar.

## Aktivieren der Audience für eine E-Mail-Kampagne {#activate-audience-for-campaign}

Sobald Sie Ihre Audience erstellt haben, können Sie sie für ein Ziel aktivieren. Platform unterstützt eine Vielzahl von E-Mail-Dienstanbietern (ESPs), mit denen Sie Ihre E-Mail-Marketing-Aktivitäten verwalten können, z. B. das Senden von Werbe-E-Mail-Kampagnen.

Überprüfen Sie die [Übersicht über E-Mail-Marketing-Ziele](../../destinations/catalog/email-marketing/overview.md#connect-destination) für eine Liste der unterstützten Ziele, in die Sie Daten exportieren möchten (z. B. die [Oracle Eloqua](../../destinations/catalog/email-marketing/oracle-eloqua-api.md) Seite).

## Anzeigen der zurückgegebenen Analysedaten aus Ihrer Kampagne {#post-campaign-data-analysis}

Die Daten aus Quellen können jetzt [inkrementell verarbeitet](../key-concepts/incremental-load.md) als Teil einer geplanten Aktualisierung Ihres Datenmodells im beschleunigten Datenspeicher. Alle Antwortereignisse von Kunden können bei ihrem Auftreten oder in Batches in Adobe Experience Platform aufgenommen werden. Ihr Datenmodell kann je nach Einstellungen oder Quell-Connectoren einmal oder mehrmals täglich aktualisiert werden. Siehe [Batch-Aufnahme-API - Übersicht](../../ingestion/batch-ingestion/api-overview.md) oder [Streaming-Erfassung - Übersicht](../../ingestion/streaming-ingestion/overview.md) für weitere Informationen.

Sobald Ihr Datenmodell aktualisiert wurde, stellen Ihre benutzerdefinierten Dashboard-Widgets aussagekräftige Signale bereit, mit denen Sie den Lebenszeitwert von Kunden messen und visualisieren können.

![Ein benutzerdefiniertes Widget, das die Anzahl der geöffneten E-Mails entsprechend ihrer Zielgruppe und E-Mail-Kampagne anzeigt.](../images/use-cases/post-activation-and-email-response-kpis.png)

Für Ihre benutzerdefinierte Analyse stehen verschiedene Visualisierungsoptionen zur Verfügung.

![Die E-Mail, die vom Widget Kampagnenkubel geöffnet wurde.](../images/use-cases/email-opened-by-campaign-buckets.png)

Diese Einblicke können Ihnen wiederum bei der Entwicklung Ihrer Geschäftsstrategien für nachfolgende Kampagnen helfen.

![Eine Sammlung von vier benutzerdefinierten Widgets, die die Ergebnisse der E-Mail-Kampagne detailliert beschreiben.](../images/use-cases/example-widgets.png)

## Nächste Schritte

Durch Lesen dieses Dokuments sollten Sie besser verstehen, wie Sie mit Real-time Customer Data Platform die CLV-Metrik (Customer Lifetime Value) verfolgen und visualisieren können. Um mehr über die vielen geschäftlichen Anwendungsfälle zu erfahren, die über Query Service und Experience Platform behandelt werden, sollten Sie die folgenden Dokumente lesen:

* [Ein durchgängiges Beispiel für einen abgebrochenen Browseranwendungsfall, der die Vielseitigkeit und Vorteile von Query Service demonstriert.](./abandoned-browse.md)
* [Verwendung von Query Service und maschinellem Lernen zur Bestimmung und Filterung von Bot-Aktivitäten anhand des echten Besucher-Traffics auf einer Online-Website](./bot-filtering.md)
* [So führen Sie eine Übereinstimmung mit Ihren Platform-Daten durch, bei der Ergebnisse aus mehreren Datensätzen kombiniert werden, indem Sie ungefähr eine Zeichenfolge Ihrer Wahl abgleichen.](./fuzzy-match.md)

<!-- "Data signals are actions taken by consumers while online that offer clues about intent that can be acted upon. This includes anything from visiting a website to filling out a change of address or clicking an ad."  -->

<!-- "Customer touchpoints are your brand's points of customer contact, from start to finish." -->
