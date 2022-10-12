---
keywords: Experience Platform; Abfrage; Query Service; Fehlerbehebung; Limits; Richtlinien; Limit;
title: Limits für Query Service
description: Dieses Dokument enthält Informationen zu Nutzungsbeschränkungen für Query Service-Daten, die Ihnen bei der Optimierung Ihrer Abfrageverwendung helfen.
exl-id: 1ad5dcf4-d048-49ff-97e3-07040392b65b
source-git-commit: e40a9fb0149e194de693a98e5d185860a255b5c4
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 7%

---

# Limits für Query Service

Limits sind Schwellenwerte, die die Datennutzung und Systemnutzung, Leistungsoptimierung und Vermeidung von Fehlern oder unerwarteten Ergebnissen in Adobe Experience Platform lenken.

Dieses Dokument enthält standardmäßige Nutzungsbeschränkungen für Query Service-Daten, mit denen Sie die Systemleistung bei der Abfrage von Daten im Zusammenhang mit Ihren Lizenzberechtigungen optimieren können.

## Voraussetzungen

Bevor Sie mit diesem Dokument fortfahren, sollten Sie die wichtigsten Definitionen und Funktionen von Query Service kennen. Sie werden nachfolgend beschrieben:

* **Ad-hoc-Abfragen**: Für die Ausführung `SELECT` Abfragen zum Erkunden, Experimentieren und Validieren von Daten, in denen die Ergebnisse der Abfragen vorliegen **nicht gespeichert werden** auf dem See.

* **Batch-Abfragen**: Für die Ausführung `INSERT TABLE AS SELECT` und `CREATE TABLE AS SELECT` Abfragen zum Bereinigen, Gestalten, Bearbeiten und Anreichern von Daten. Die Ergebnisse dieser Abfragen **gespeichert werden** auf dem See. Die Metrik zur Messung des Verbrauchs dieser Funktion ist die Berechnung der Stunden.

* **Query Service-Benutzer**: Query Service-Benutzer, die in Ihrer aktuellen Lizenz für Customer Journey Analytics, Adobe Real-time Customer Data Platform und/oder Adobe Journey Optimizer bereitgestellt werden, können auch mit Data Distiller verwendet werden. Query Service-Benutzer werden zwischen Funktionen freigegeben.

* **Ad-hoc-Benutzer**: Ad-hoc-Benutzer führen Ad-hoc-Abfragen aus.

* **Batch-Benutzer**: Batch-Benutzer sind diejenigen, die Batch-Abfragen ausführen.

* **Reporting-API**: Eine API zum Ausführen von Datenabruf-Aufrufen (intern oder extern). Erweiterte Berichtsdatenmodelle werden aus den nativen Berichtsdatenmodellen in Adobe Experience Platform abgeleitet, z. B. dem Real-Time CDP Dashboards-Datenmodell.

Die folgende Abbildung fasst zusammen, wie Query Service-Funktionen derzeit zusammengefasst und lizenziert sind:

![Ein Diagramm zur Erläuterung der Verteilung und Verpackung von Query Service-Funktionen im Zusammenhang mit der Lizenzierung.](./images/guardrails/query-capabilities.png)

## Arten von Beschränkungen

In diesem Dokument gibt es zwei Arten von Standardbeschränkungen:

* **Softlimit**: Sie können jedoch über eine weiche Grenze hinausgehen, bieten Softlimits jedoch eine empfohlene Richtlinie für die Systemleistung.

* **Hardbounce**: Eine feste Begrenzung bietet ein absolutes Maximum.

>[!NOTE]
>
>Die in diesem Dokument beschriebenen Standardbeschränkungen werden ständig verbessert. Achten Sie regelmäßig auf Updates.

## Limits bei der Primären Entitätsleistung

Die folgenden Tabellen enthalten die empfohlenen Limits und Beschreibungen für die Ausführung von Abfragen bei Verwendung eines bestimmten Abfragemusters.

**Ad-hoc-Abfragen**

| Beschränkung | Limit | Begrenzungstyp | Beschreibung |
|---|---|---|---|
| Maximale Ausführungsdauer | 10 Minuten | Hard | Dies definiert die maximale Ausgabedauer für eine Ad-hoc-SQL-Abfrage. Wenn Sie die Zeitbeschränkung zum Zurückgeben eines Ergebnisses überschreiten, wird der Fehlercode 53400 ausgegeben. |
| Gleichzeitige Query Service-Benutzer | <ul><li>Wie in der Produktbeschreibung der Anwendung angegeben.</li><li>+5 (mit jedem zusätzlichen Ad-hoc-Abfrage-Benutzer-Add-On-Paket gekauft)</li></ul> | Hard | Dadurch wird definiert, wie viele Benutzer Sitzungen für eine bestimmte Organisation gleichzeitig erstellen können. Wenn die gleichzeitige Beschränkung überschritten wird, erhält der Benutzer eine `Session Limit Reached` Fehler. |
| Abfragegleichzeitigkeit | <ul><li>Wie in der Produktbeschreibung der Anwendung angegeben.</li><li>+1 (mit jedem zusätzlichen erworbenen Ad-hoc-Abfragebenutzer-Add-on-SKU-Paket)</li></ul> | Hard | Dadurch wird definiert, wie viele Abfragen für eine bestimmte Organisation gleichzeitig ausgeführt werden können. Wenn die gleichzeitige Beschränkung überschritten wird, werden die Abfragen in die Warteschlange gestellt. |
| Client-Connector und Ergebnisausgabegrenze | Client Connector<ul><li>Query UI (100 Zeilen)</li><li>Drittanbieter-Client (50.000)</li><li>[!DNL PostgresSQL] Client (50.000)</li></ul> | Hard | Das Ergebnis einer Abfrage kann auf folgende Weise empfangen werden:<ul><li>Benutzeroberfläche von Query Service</li><li>Drittanbieter-Client</li><li>[!DNL PostgresSQL] client</li></ul>Hinweis: Durch das Hinzufügen einer Begrenzung zur Ausgabenanzahl können Ergebnisse schneller zurückgegeben werden. Beispielsweise `LIMIT 5`, `LIMIT 10` und so weiter. |
| Über zurückgegebene Ergebnisse | Client-Benutzeroberfläche | K. A. | Dadurch wird definiert, wie die Ergebnisse den Benutzern zur Verfügung gestellt werden. |

{style=&quot;table-layout:auto&quot;}

**Batch-Abfragen**

| **Beschränkung** | **Limit** | **Begrenzungstyp** | **Beschreibung** |
|---|---|---|---|
| Maximale Ausführungsdauer | 24 Stunden | Hard | Dies definiert die maximale Ausführungszeit für eine Batch-SQL-Abfrage.<br>Die Verarbeitungszeit einer Abfrage hängt von der Menge der zu verarbeitenden Daten und der Komplexität der Abfrage ab. |
| Gleichzeitige Query Service-Benutzer für nicht geplanten Batch | <ul><li>Wie in der Produktbeschreibung der Anwendung angegeben.</li><li>+5 (mit jedem zusätzlichen Ad-hoc-Abfrage-Benutzer-Add-On-Paket gekauft)</li></ul> | Hard | Bei ungeplanten Batch-Abfragen (z. B. CTAS/ITAS-Abfragen im interaktiven Modus) wird dadurch definiert, wie viele Benutzer Sitzungen für eine bestimmte Organisation gleichzeitig erstellen können. Wenn die gleichzeitige Beschränkung überschritten wird, erhält der Benutzer eine `Session Limit Reached` Fehler. |
| Gleichzeitige Query Service-Benutzer für geplanten Batch | Keine Benutzerbeschränkung | K. A. | Geplante Batch-Abfragen sind asynchrone Aufträge, sodass keine Benutzerbegrenzung besteht. |
| Berechnungsstunden für die Batch-Datenverarbeitung | Wie im Adobe Experience Platform Intelligence Query Query Query Custom SKU Sales Order des Kunden angegeben | Soft | Dies definiert den Umfang der Rechenzeit pro Jahr, die ein Kunde zum Ausführen von Batch-Abfragen zum Scannen, Verarbeiten und Zurückschreiben von Daten in den Data Lake hat. |
| Abfragegleichzeitigkeit | Unterstützt | K. A. | Geplante Batch-Abfragen sind asynchrone Aufträge, daher werden gleichzeitige Abfragen unterstützt. |
| Client-Connector- und Ergebnisausgabegrenze | Client Connector<ul><li>Abfrage-Benutzeroberfläche (keine Obergrenze für Zeilen)</li><li>Drittanbieter-Client (keine Obergrenze für Zeilen)</li><li>[!DNL PostgresSQL] client (keine Obergrenze für Zeilen)</li><li>REST-APIs (keine Obergrenze für Zeilen)</li></ul> | Hard | Das Ergebnis einer Abfrage kann mithilfe der folgenden Methoden bereitgestellt werden:<ul><li>Kann als abgeleitete Datensätze gespeichert werden</li><li>Kann in die vorhandenen abgeleiteten Datensätze eingefügt werden</li></ul>Hinweis: Die Anzahl der Datensätze aus dem Abfrageergebnis ist nicht begrenzt. |
| Über zurückgegebene Ergebnisse | Datensatz | K. A. | Dadurch wird definiert, wie die Ergebnisse den Benutzern zur Verfügung gestellt werden. |

{style=&quot;table-layout:auto&quot;}

## Abfrage-beschleunigter Speicher {#query-accelerated-store}

Die folgende Tabelle enthält die empfohlenen Limits und eine Beschreibung für den Abfrage-beschleunigten Speicher.

| Beschränkung | Limit | Begrenzungstyp | Beschreibung |
|---|---|---|---|
| Abfragegleichzeitigkeit | 4 | Hard | Um sicherzustellen, dass Abfragen über aggregierte Daten über die Berichterstellungs-API (einschließlich Abfragen, die Datenmodelle wie die Echtzeit-Kundendatenmodelle verbessern) über die Ressourcen verfügen, die für eine effiziente Ausführung benötigt werden, verfolgt die Berichterstellungs-API die Ressourcenauslastung, indem sie jeder Abfrage Gleichzeitigkeitsfenster zuweist. Das System stellt Abfragen in eine Warteschlange und wartet, bis Zeitnischen für gleichzeitige Verwendung verfügbar sind oder sie aus dem Cache bereitgestellt werden können. Es stehen maximal vier gleichzeitige Abfragefenster zur Verfügung.<br>Wenn Sie über ein BI-Tool auf die Reporting-API zugreifen und mehr Parallelität benötigen, ist ein BI-Server erforderlich. |

{style=&quot;table-layout:auto&quot;}

## Nächste Schritte

Nach dem Lesen dieses Dokuments sollten Sie die Standardbeschränkungen für die Ausführung von Abfragen mit den verfügbaren Abfragemustern besser verstehen.

Weitere Informationen zu Query Service finden Sie in der folgenden Dokumentation:

* [Query Service-API](./api/getting-started.md)
* [Benutzeroberfläche von Query Service](./ui/overview.md)
