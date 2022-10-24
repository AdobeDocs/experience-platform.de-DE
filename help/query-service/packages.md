---
title: Query Service Packages
description: Im folgenden Dokument werden die für Query Service verfügbaren Funktionspakete und Produkte beschrieben und die Unterschiede zwischen Ad-hoc- und Batch-Abfragen hervorgehoben.
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '720'
ht-degree: 8%

---

# Query Service-Pakete

In diesem Dokument werden die verschiedenen Packaging- und Abfrageausführungsfunktionen beschrieben, die in Query Service verfügbar sind.

Adobe Experience Platform Query Service kann in zwei Funktionen unterteilt werden, die auf den auszuführenden Abfragemustern basieren:

- **Ad-hoc-Abfragen** sind SQL-Abfragen, mit denen erfasste Datensätze zur Überprüfung, Validierung, Experimentierung usw. untersucht werden. Diese Abfragen schreiben keine Daten zurück in den Platform Data Lake.
- **Batch-Abfragen** sind SQL-Abfragen, die zur Durchführung der Verarbeitung erfasster Datensätze nach der Erfassung verwendet werden. Diese Abfragen bereinigen, formen, manipulieren und anreichern Daten, deren Ergebnisse in den Platform Data Lake zurückgeschrieben werden. Diese Abfragen können als Batch-Aufträge geplant, verwaltet und überwacht werden.

Query Service-Funktionen werden mit den folgenden Produkten und Add-ons gepackt:

- **Plattformbasierte Anwendungen** (Adobe Real-time Customer Data Platform, Adobe Customer Journey Analytics und Adobe Journey Optimizer): Der Zugriff auf Query Service zum Ausführen von Ad-hoc-Abfragen wird von Anfang an für jede Variante und Ebene von Platform-basierten Anwendungen bereitgestellt.
- **[!DNL Data Distiller]** (Zusatzmodulpaket, das mit Adobe Real-Time CDP, Customer Journey Analytics und Adobe Journey Optimizer erworben werden kann): Zugriff auf Query Service zum Ausführen von Batch-Abfragen wird mit [!DNL Data Distiller].

In der folgenden Tabelle werden die wichtigsten Query Service-Berechtigungen basierend auf ihrer Verpackung aufgeführt:

| Berechtigung für Query Service | Mit Platform-basierten Anwendungen gepackt | Paket mit [!DNL Data Distiller] |
|---|---|---|
| Unterstütztes Abfragemuster | Nur Ad-hoc-Abfrage | Batch-Abfrage |
| Anwendungsfall unterstützt | <ul><li>&#x200B;</li><li>&#x200B;</li><li>Datenvalidierung</li><li>Experimentieren</li></ul> | <ul><li>Reinigung</li><li>Formatierung</li><li>Bearbeiten</li><li>Anreicherung</li></ul> |
| Unterstützte Semantik | <ul><li>Abfragen auswählen</li></ul> | <ul><li>CTAS- und ITAS-Abfragen</li></ul> |
| Maximale Ausführungszeit | 10 Minuten | 24 Stunden |
| Lizenzmetrik | **Query User Concurrency**: <ul><li>1 gleichzeitiger Benutzer (Real-Time CDP, Adobe Journey Optimizer) &#x200B;</li><li>5 gleichzeitige Benutzer (Customer Journey Analytics) &#x200B;</li></ul> **Abfragekonsistenz**: <ul><li>1 Abfrage mit gleichzeitiger Ausführung (alle Anwendungen) &#x200B;</li></ul> **Add-On für zusätzliche Ad-hoc-Abfragen für Benutzer des Packs** kann erworben werden, um die autorisierten Ad-hoc-Abfrageberechtigungen von Kunden zu erhöhen. <ul><li>+5 weitere gleichzeitige Benutzer pro Paket</li><li>+1 zusätzliche gleichzeitige Abfrage pro Paket</li></ul> | **Berechnungsstunden**: <ul><li>Variable (basierend auf den Anwendungsberechtigungen des Kunden)</li></ul> **Berechnungsstunden** ist ein Maß für die Zeit, die die Query Service-Engine benötigt, um Daten zu lesen, zu verarbeiten und in den Data Lake zurückzuschreiben, wenn eine Batch-Abfrage ausgeführt wird. |
| Oberfläche zur Ausführung von Abfragen | <ul><li>Benutzeroberfläche von Query Service</li><li>Client-Benutzeroberfläche von Drittanbietern</li><li>[!DNL PostgresSQL] Client-Benutzeroberfläche</li></ul> | <ul><li>Abfrage-Benutzeroberfläche </li><li>Client-Benutzeroberfläche von Drittanbietern</li><li>[!DNL PostgresSQL] Client-Benutzeroberfläche</li><li>REST-APIs</li></ul> |
| Abfrageergebnisse zurückgegeben über | Client-Benutzeroberfläche | Abgeleiteter Datensatz, der im Data Lake gespeichert ist |
| Ergebnisbegrenzung | <ul><li>Query UI - 100 Zeilen</li><li>Drittanbieter-Client - 50.000</li><li>[!DNL PostgresSQL] client - 50.000</li></ul> | <ul><li>Abfrage-Benutzeroberfläche (keine Obergrenze für Zeilen)</li><li>Drittanbieter-Clients (keine Obergrenze für Zeilen)</li><li>[!DNL PostgresSQL] client (keine Obergrenze für Zeilen)</li><li>REST-APIs (keine Obergrenze für Zeilen)</li></ul> |
| Datensatzkapazität lesen | Ja | Ja |
| Datensatzkapazität schreiben | Nein | Ja |
| Planungskapazität | Nein | Ja |
| Überwachungskapazität | Ja | Ja |
| Setup-Funktion für Abfragewarnungen | Nein | Ja |

{style=&quot;table-layout:auto&quot;}

## Zugangssteuerung

Die Zugriffskontrolle für die Experience Platform wird über die [Adobe Admin Console](https://adminconsole.adobe.com/) wo Produktprofile Benutzer mit Berechtigungen und Sandboxes verknüpfen. Weiterführende Informationen dazu finden Sie unter [Zugangssteuerung – Übersicht](../access-control/home.md).

Um Query Service zu verwenden, muss die [!DNL Manage Queries] -Berechtigung muss in der Admin Console aktiviert sein. Mit dieser Berechtigung können Benutzer Ad-hoc- und Batch-Abfragen ausführen. Detaillierte Anweisungen zum Anfordern des Zugriffs auf das Produktprofil [!DNL Manage Queries] -Berechtigungen wurden im Abschnitt [Berechtigungen für ein Produktprofil verwalten](../access-control/ui/permissions.md) und [Benutzer für ein Produktprofil verwalten](../access-control/ui/users.md) Dokumente.

Nach dem Kauf der [!DNL Data Distiller] -Add-on, die [!DNL Write Dataset] muss erteilt werden. Diese Berechtigung ermöglicht [!DNL Data Distiller] -Benutzer, um Batch-Abfragen auszuführen.

In der folgenden Tabelle sind die Auswirkungen der [!DNL Manage Queries] Berechtigung:

| Berechtigung | Funktion |
|---|---|
| [!DNL Manage Queries] (ohne Schreibdatenberechtigung) | Ermöglicht Zugriff auf die Ausführung von Ad-hoc-Abfragen |
| [!DNL Manage Queries] (mit Schreibberechtigung für Daten) | Ermöglicht Zugriff auf die Ausführung von Batch-Abfragen |

{style=&quot;table-layout:auto&quot;}

## Sandbox-Unterstützung

Sandboxes sind virtuelle Partitionen innerhalb einer einzelnen Instanz von Experience Platform. Jede Platform-Instanz unterstützt mehrere Produktions- und Nicht-Produktions-Sandboxes, von denen jede eine eigene Bibliothek mit Platform-Ressourcen unterhält. Mit Nicht-Produktions-Sandboxes können Sie Funktionen testen, Experimente ausführen und benutzerdefinierte Konfigurationen vornehmen, ohne die Produktions-Sandboxes zu beeinträchtigen. Weiterführende Informationen finden Sie in der [Sandbox-Übersicht](../sandboxes/home.md). Alle Berechtigungen für Query Service werden für alle Sandboxes freigegeben.

## Nächste Schritte

Durch Lesen dieses Dokuments sollten Sie ein besseres Verständnis der verschiedenen in Query Service verfügbaren Packagetypen und Ausführungsfunktionen von Abfragen haben. Weitere Informationen zu Query Service, z. B. bekannten Anwendungsfällen in der Branche, finden Sie in der [Anwendungsfalldokumentation](./use-cases/abandoned-browse.md). Weitere allgemeine Informationen finden Sie unter [Query Service - Übersicht](./home.md).
