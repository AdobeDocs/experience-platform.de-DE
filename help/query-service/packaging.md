---
title: Query Service-Paketierung
description: Im folgenden Dokument wird die Bündelung der für den Abfrage-Service verfügbaren Funktionen und Produkte beschrieben und die Unterschiede zwischen Ad-hoc- und Batch-Abfragen hervorgehoben.
exl-id: ba472d9e-afe6-423d-9abd-13ecea43f04f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 5%

---

# Packaging des Abfrage-Services

In diesem Dokument werden die verschiedenen Arten von Paketierungs- und Abfrageausführungsfunktionen beschrieben, die im Abfrage-Service verfügbar sind.

Der Abfrage-Service von Adobe Experience Platform kann basierend auf den Abfragemustern, die ausgeführt werden können, in zwei Funktionen unterteilt werden:

- **Ad-hoc** Abfragen sind SQL-Abfragen, mit denen aufgenommene Datensätze zur Überprüfung, Validierung, Experimentierung usw. untersucht werden. Diese Abfragen schreiben keine Daten zurück in den Data Lake von Experience Platform.
- **Batch-Abfragen** sind SQL-Abfragen, die zur Nachbearbeitung aufgenommener Datensätze verwendet werden. Diese Abfragen bereinigen, formen, bearbeiten und reichern Daten an, deren Ergebnisse zurück in den Data Lake von Experience Platform geschrieben werden. Diese Abfragen können als Batch-Vorgänge geplant, verwaltet und überwacht werden.

Query Service-Funktionen sind in den folgenden Produkten und Add-ons enthalten:

- **Experience Platform-basierte Anwendungen** (Adobe Real-Time Customer Data Platform, Adobe Customer Journey Analytics und Adobe Journey Optimizer): Der Zugriff auf den Abfrage-Service zum Ausführen von Ad-hoc-Abfragen wird von Anfang an für jede Variante und Ebene von Experience Platform-basierten Anwendungen bereitgestellt.
- **[!DNL Data Distiller]** (Add-on-Paket, das mit Adobe Real-Time CDP, Customer Journey Analytics und Adobe Journey Optimizer erworben werden kann): Der Zugriff auf den Abfrage-Service zum Ausführen von Batch-Abfragen wird mit [!DNL Data Distiller] bereitgestellt.

## Berechtigungen {#entitlements}

In der folgenden Tabelle sind die wichtigsten Berechtigungen für den Abfrage-Service basierend auf ihrer Verpackung aufgeführt:

| Berechtigung für Abfrage-Service | In Experience Platform-basierten Anwendungen verpackt | Verpackt mit [!DNL Data Distiller] |
|---|---|---|
| Unterstütztes Abfragemuster | Nur Ad-hoc-Abfragen | Batch-Abfrage |
| Anwendungsfall unterstützt | <ul><li>&#x200B;</li><li>Datenerkennung&#x200B;</li><li>Datenvalidierung</li><li>Experimentieren</li></ul> | <ul><li>Reinigung</li><li>Formgebung</li><li>Bearbeitung</li><li>bereichernd</li></ul> |
| Unterstützte Semantik | <ul><li>SELECT queries</li></ul> | <ul><li>CTAS- und ITAS-Abfragen</li></ul> |
| Maximale Ausführungszeit | 10 Minuten | 24 Stunden |
| Lizenzmetrik | **Benutzerparallelität abfragen**: <ul><li>1 gleichzeitiger Benutzer (Real-Time CDP, Adobe Journey Optimizer)&#x200B;</li><li>5 gleichzeitige Benutzer (Customer Journey Analytics)&#x200B;</li></ul> **gleichzeitige Abfrage**: <ul><li>1 gleichzeitige Abfrage (alle Programme) wird ausgeführt&#x200B;</li></ul> **Sie können ein zusätzliches Add-on für Ad-hoc** Abfragen für Benutzer erwerben, um Ihre autorisierte Ad-hoc-Abfrageberechtigung zu erhöhen. <ul><li>+5 zusätzliche gleichzeitige Benutzer pro Pack</li><li>+1 zusätzliche gleichzeitige Abfrage pro Pack</li></ul> | **Stunden**: <ul><li>Variable (Bereich basierend auf Ihrer Programmberechtigung)</li></ul> **Stunden berechnen** ist ein Maß für die Zeit, die die Abfrage-Service-Engine zum Lesen, Verarbeiten und Zurückschreiben von Daten in den Data Lake benötigt, wenn eine Batch-Abfrage ausgeführt wird. <br>Mit der Data Distiller SKU erhalten Sie auch eine zusätzliche Gleichzeitigkeit von Benutzenden und Abfragen, die für die Ausführung von Ad-hoc-Abfragen verwendet werden kann.  Die Data Distiller SKU umfasst:<br><ul><li>+5 zusätzliche gleichzeitige Benutzer</li><li>+1 zusätzliche gleichzeitige Abfrage</li></ul> |
| Beschleunigte Abfrage- und Reporting-Nutzung | Nein | Ja - Mit gleichzeitigen beschleunigten Abfragen können Sie Daten aus dem beschleunigten Speicher lesen und in Ihren Dashboards anzeigen. Eine dedizierte Berechtigung zum Speichern von Berichtsmodellen und Datensätzen im beschleunigten Speicher wird ebenfalls bereitgestellt. |
| Data-Lake-Speicherkapazität | Ihre gesamten Speicherberechtigungen hängen von Ihren plattformbasierten Anwendungslizenzen ab. Zum Beispiel Real-Time CDP, AJO, CJA und so weiter. | Ja - Es wird eine zusätzliche Speicherberechtigung bereitgestellt, um Ihre Roh- und abgeleiteten Datensätze für Distiller-Anwendungsfälle über ein siebentägiges Datenablaufdatum hinaus beizubehalten.<br>Ihre Data-Lake-Speicherkapazität wird in Terabyte (TB) gemessen und hängt von der Menge der erworbenen Rechenstunden ab. Weitere Informationen finden Sie in der Produktbeschreibung . |
| Freibetrag für Datenexporte | Ihre gesamte Exportberechtigung hängt von Ihren plattformbasierten Anwendungslizenzen ab. Zum Beispiel Real-Time CDP, AJO, CJA und so weiter. | Ja - Es wird eine zusätzliche Exportberechtigung bereitgestellt, um den Export abgeleiteter Datensätze zu ermöglichen, die mit Data Distiller erstellt wurden.<br>Ihre jährliche Datenexportzulage wird in Terabyte (TB) gemessen und hängt von der Menge der von Ihnen erworbenen Rechenstunden ab. Weitere Einzelheiten finden Sie in der Produktbeschreibung. |
| Benutzeroberfläche zur Abfrageausführung | <ul><li>Benutzeroberfläche von Query Service</li><li>Client-Benutzeroberfläche von Drittanbietern</li><li>[!DNL PostgresSQL] Client-Benutzeroberfläche</li></ul> | <ul><li>Benutzeroberfläche von Query Service </li><li>Client-Benutzeroberfläche von Drittanbietern</li><li>[!DNL PostgresSQL] Client-Benutzeroberfläche</li><li>REST-APIs</li></ul> |
| Über zurückgegebene Abfrageergebnisse | Client-Benutzeroberfläche | Abgeleiteter Datensatz im Data Lake gespeichert |
| Ergebnisgrenze | <ul><li>Benutzeroberfläche von Query Service - Die Anzahl der Ausgabezeilen kann ([ einer Benutzeroberflächeneinstellung konfiguriert) ](./ui/user-guide.md#result-count) zwischen 50 und 500 Zeilen eingestellt werden.</li><li>Drittanbieter-Clients - 50.000</li><li>[!DNL PostgresSQL] Client - 50.000</li></ul> | CTAS- und ITAS-Abfragen generieren nur Erfolgsmeldungen, da die Abfrageausgabe in abgeleiteten Datensätzen gespeichert wird. |
| Kapazität des Datensatzes lesen | Ja | Ja |
| Datensatzkapazität schreiben | Nein | Ja |
| Geplante Kapazität | Nein | Ja |
| Überwachungskapazität | Ja | Ja |
| Setup-Kapazität des Warnhinweises abfragen | Nein | Ja |

{style="table-layout:auto"}

## Zugangssteuerung {#access-control}

Die Zugriffssteuerung für Experience Platform wird über die [Adobe Admin Console verwaltet](https://adminconsole.adobe.com/) wobei Produktprofile Benutzende mit Berechtigungen und Sandboxes verknüpfen. Weiterführende Informationen dazu finden Sie unter [Zugangssteuerung – Übersicht](../access-control/home.md).

Detaillierte Anweisungen [ Anfordern des Zugriffs auf die Produktprofilberechtigungen finden Sie in den Dokumenten ](../access-control/ui/permissions.md)Berechtigungen für ein Produktprofil verwalten[&#128279;](../access-control/ui/users.md) und Benutzer für ein Produktprofil verwalten

### Relevante Query Service-Berechtigungen {#query-service-permissions}

Um den Abfrage-Service verwenden zu können, muss die **[!DNL Manage Queries]** in Admin Console aktiviert sein. Mit dieser Berechtigung können Benutzer Ad-hoc- und Batch-Abfragen ausführen.

In der folgenden Tabelle sind die Auswirkungen der [!DNL Manage Queries] Berechtigung aufgeführt:

| Berechtigung | Funktion |
|---|---|
| [!DNL Manage Queries] (ohne Schreibberechtigung) | Ermöglicht den Zugriff zum Ausführen von Ad-hoc-Abfragen |
| [!DNL Manage Queries] (mit Schreibberechtigung für Daten) | Ermöglicht den Zugriff zum Ausführen von Batch-Abfragen |

{style="table-layout:auto"}

### Relevante SQL Insights-Berechtigungen {#sql-insights-permissions}

Um Data Distiller [SQL Insights](./data-distiller/sql-insights/overview.md) innerhalb von Dashboards zu erstellen, **die folgenden Berechtigungen** Admin Console aktiviert werden.

| Berechtigung | Funktion |
|---|---|
| [!DNL View Custom Dashboard] | Bietet Ansichtszugriff auf benutzerdefinierte Dashboards |
| [!DNL Manage Custom Dashboard] | Bietet Verwaltungszugriff für benutzerdefinierte Dashboards |

{style="table-layout:auto"}

## Sandbox-Unterstützung {#sandbox-support}

Sandboxes sind virtuelle Partitionen innerhalb einer einzelnen Instanz von Experience Platform. Jede Experience Platform-Instanz unterstützt mehrere Produktions- und Nicht-Produktions-Sandboxes, von denen jede eine eigene Bibliothek mit Experience Platform-Ressourcen verwaltet. Nicht-Produktions-Sandboxes ermöglichen es Ihnen, Funktionen zu testen, Experimente durchzuführen und benutzerdefinierte Konfigurationen vorzunehmen, ohne dass sich dies auf Ihre Produktions-Sandboxes auswirkt. Weitere Informationen zu Sandboxes finden Sie unter [Sandbox-Übersicht](../sandboxes/home.md). Alle Berechtigungen für den Abfrage-Service werden für alle Sandboxes freigegeben.

## Nächste Schritte

Durch das Lesen dieses Dokuments sollten Sie ein besseres Verständnis der verschiedenen Pakettypen und Abfrageausführungsfunktionen haben, die im Abfrage-Service verfügbar sind. Weitere Informationen zum Abfrage-Service, z. B. bekannte branchenspezifische Anwendungsfälle, finden Sie unter [Dokumentation zu Anwendungsfällen](./use-cases/abandoned-browse.md). Weitere allgemeine Informationen finden Sie unter [Query Service - Übersicht](./home.md).

