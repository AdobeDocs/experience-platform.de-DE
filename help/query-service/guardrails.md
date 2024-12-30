---
keywords: Experience Platform;Abfrage;Abfrage-Service;Fehlerbehebung;Leitplanken;Richtlinien;Limit;
title: Leitplanken für Query Service
description: Dieses Dokument enthält Informationen zu Nutzungsbeschränkungen für Abfrage-Service-Daten, die Sie bei der Optimierung der Verwendung Ihrer Abfrage unterstützen.
exl-id: 1ad5dcf4-d048-49ff-97e3-07040392b65b
source-git-commit: 5d6b70e397a252e037589c3200053ebcb7eb8291
workflow-type: tm+mt
source-wordcount: '1181'
ht-degree: 4%

---

# Leitplanken für Query Service

Leitplanken sind Schwellenwerte, die die Daten- und Systemnutzung steuern, die Leistungsoptimierung optimieren und Fehler oder unerwartete Ergebnisse in Adobe Experience Platform vermeiden.
Dieses Dokument enthält standardmäßige Nutzungsbeschränkungen für Abfrage-Service-Daten, mit denen Sie die Systemleistung bei der Abfrage von Daten im Zusammenhang mit Ihren Lizenzierungsberechtigungen optimieren können.

>[!IMPORTANT]
>
>Überprüfen Sie zusätzlich zu dieser Seite mit Leitplanken Ihre Lizenzberechtigungen in Ihrem Kundenauftrag und [ entsprechenden ](https://helpx.adobe.com/de/legal/product-descriptions.html)Produktbeschreibung) die tatsächlichen Nutzungsbeschränkungen.

## Voraussetzungen

Bevor Sie mit diesem Dokument fortfahren, sollten Sie über gute Kenntnisse der wichtigsten Definitionen und Funktionen des Abfrage-Service verfügen. Sie werden nachfolgend beschrieben:

* **Ad-hoc-Abfragen**: Zum Ausführen `SELECT` Abfragen, um Daten zu untersuchen, zu experimentieren und zu validieren, bei denen die Ergebnisse der Abfragen **nicht gespeichert)** Data Lake.

* **Batch-Abfragen**: Zum Ausführen von `INSERT TABLE AS SELECT` und `CREATE TABLE AS SELECT` Abfragen zum Bereinigen, Gestalten, Bearbeiten und Anreichern von Daten. Die Ergebnisse dieser Abfragen **werden** Data Lake gespeichert. Die Metrik zur Messung der Nutzung dieser Funktion ist die Anzahl der Rechenstunden.

* **Query Service-Benutzer**: Abfrage-Service-Benutzer, die in Ihrer aktuellen Lizenz für Customer Journey Analytics, Adobe Real-time Customer Data Platform und/oder Adobe Journey Optimizer bereitgestellt werden, können auch mit Data Distiller verwendet werden. Query Service-Benutzer werden von den -Funktionen gemeinsam genutzt.

* **Ad-hoc-**: Ad-hoc-Benutzer sind diejenigen, die Ad-hoc-Abfragen ausführen.

* **Batch-Benutzer**: Batch-Benutzer sind diejenigen, die Batch-Abfragen ausführen.

* **Reporting-API**: Eine API für Datenabruf-Aufrufe (intern oder extern). Erweiterte Berichtsdatenmodelle werden von den nativen Berichtsdatenmodellen in Adobe Experience Platform abgeleitet, z. B. vom Real-Time CDP Dashboards -Datenmodell.

Die folgende Abbildung fasst zusammen, wie die Abfrage-Service-Funktionen derzeit verpackt und lizenziert werden:

## Schutzmechanismen-Typen

In diesem Dokument gibt es zwei Arten von Standardbeschränkungen:

| Art der Leitplanke | Beschreibung |
|----------|---------|
| **Leistungs-Schutzmaßnahme (weiches Limit)** | Die Leistung betreffende Leitplanken sind Nutzungsbeschränkungen, die sich auf den Umfang Ihrer Anwendungsfälle beziehen. Beim Überschreiten der Leistungsleitplanken kann es zu Leistungseinbußen und Latenzzeiten kommen. Adobe ist nicht für eine solche Leistungsbeeinträchtigung verantwortlich. Kunden, die ständig eine Leistungsschutzmaßnahme überschreiten, können sich dafür entscheiden, zusätzliche Kapazität zu lizenzieren, um eine Leistungsbeeinträchtigung zu vermeiden. |
| **Vom System erzwungene Leitplanken (feste Grenze)** | Systemerzwungene Leitplanken werden von der Real-Time CDP-Benutzeroberfläche oder -API erzwungen. Dies sind Beschränkungen, die Sie nicht überschreiten können, da die Benutzeroberfläche und die API Sie daran hindern oder einen Fehler zurückgeben. |

{style="table-layout:auto"}

>[!NOTE]
>
>Die in diesem Dokument beschriebenen Standardbeschränkungen werden ständig verbessert. Achten Sie regelmäßig auf Updates.

## Leitplanken für die Leistung Primärer Entitäten

Die folgenden Tabellen enthalten die empfohlenen Leitplanken und Beschreibungen für die Ausführung von Abfragen bei Verwendung eines bestimmten Abfragemusters.

**Ad-hoc-Abfragen**

| Leitplanke | Limit | Art des Limits | Beschreibung |
|---|---|---|---|
| Maximale Ausführungszeit | 10 Minuten | Vom System erzwungene Leitplanken | Dies definiert die maximale Ausgabezeit für eine Ad-hoc-SQL-Abfrage. Wenn Sie das Zeitlimit für die Ausgabe eines Ergebnisses überschreiten, wird der Fehler-Code 53400. |
| Gleichzeitige Abfrage-Service-Benutzer | <ul><li>Wie in der Produktbeschreibung des Programms angegeben.</li><li>+5 (mit jedem zusätzlichen erworbenen Add-on-Paket für Ad-hoc-Abfragen von Benutzern)</li></ul> | Vom System erzwungene Leitplanken | Dadurch wird definiert, wie viele Benutzer gleichzeitig Sitzungen für eine bestimmte Organisation erstellen können. Wenn das Parallelitätslimit überschritten wird, wird ein `Session Limit Reached` Fehler angezeigt. |
| Parallelität von Abfragen | <ul><li>Wie in der Produktbeschreibung des Programms angegeben.</li><li>+1 (mit jedem zusätzlichen erworbenen Ad-hoc-Abfrage-Benutzer-Add-on-SKU-Paket)</li></ul> | Vom System erzwungene Leitplanken | Dadurch wird definiert, wie viele Abfragen gleichzeitig für eine bestimmte Organisation ausgeführt werden können. Wenn das Parallelitätslimit überschritten wird, werden die Abfragen in die Warteschlange gestellt. |
| Client-Connector und Ergebnisausgabe-Limit | Client-Connector<ul><li>Abfrage-Benutzeroberfläche (100 Zeilen)</li><li>Drittanbieter-Client (50.000)</li><li>[!DNL PostgresSQL] Client (50.000)</li></ul> | Vom System erzwungene Leitplanken | Das Ergebnis einer Abfrage kann wie folgt empfangen werden:<ul><li>Benutzeroberfläche von Query Service</li><li>Drittanbieter-Client</li><li>[!DNL PostgresSQL] Client</li></ul>Hinweis: Das Hinzufügen einer Begrenzung zur Ausgabeanzahl kann Ergebnisse schneller zurückgeben. Beispielsweise `LIMIT 5`, `LIMIT 10` und so weiter. |
| Ergebnisse zurückgegeben über | Client-Benutzeroberfläche | K. A. | Dadurch wird festgelegt, wie die Ergebnisse den Benutzern zur Verfügung gestellt werden. |

{style="table-layout:auto"}

**Batch-**

| **Leitplanke** | **limit** | **Art des Limits** | **Beschreibung** |
|---|---|---|---|
| Maximale Ausführungszeit | 24 Stunden | Vom System erzwungene Leitplanken | Dies definiert die maximale Ausführungszeit für eine Batch-SQL-Abfrage.<br>Die Verarbeitungszeit einer Abfrage hängt vom zu verarbeitenden Datenvolumen und der Komplexität der Abfrage ab. |
| Gleichzeitige Query Service-Benutzer für nicht geplanten Batch | <ul><li>Wie in der Produktbeschreibung des Programms angegeben.</li><li>+5 (mit jedem zusätzlichen erworbenen Add-on-Paket für Ad-hoc-Abfragen von Benutzern)</li></ul> | Vom System erzwungene Leitplanken | Bei nicht geplanten Batch-Abfragen (z. B. CTAS-/ITAS-Abfragen im interaktiven Modus) definiert dies, wie viele Benutzer gleichzeitig Sitzungen für eine bestimmte Organisation erstellen können. Wenn das Parallelitätslimit überschritten wird, wird ein `Session Limit Reached` Fehler angezeigt. |
| Gleichzeitige Query Service-Benutzer für geplanten Batch | Keine Benutzerbegrenzung | K. A. | Geplante Batch-Abfragen sind asynchrone Aufträge, sodass es keine Benutzereinschränkung gibt. |
| Stunden für Batch-Datenverarbeitung | Wie im Adobe Experience Platform Intelligence Query Custom SKU-Kundenauftrag des Kunden angegeben | Leistungs-Schutzmaßnahme | Dies definiert die Berechnungszeit, die ein Kunde pro Jahr für die Ausführung von Batch-Abfragen zum Scannen, Verarbeiten und Zurückschreiben von Daten in den Data Lake verwenden darf. |
| Parallelität von Abfragen | Unterstützt | K. A. | Geplante Batch-Abfragen sind asynchrone Aufträge, daher werden gleichzeitige Abfragen unterstützt. |
| Client-Connector und Ergebnisausgabelimit | Client-Connector<ul><li>Abfrage-Benutzeroberfläche (keine Obergrenze für Zeilen)</li><li>Drittanbieter-Client (keine Obergrenze für Zeilen)</li><li>[!DNL PostgresSQL] Client (keine Obergrenze für Zeilen)</li><li>REST-APIs (keine Obergrenze für Zeilen)</li></ul> | Vom System erzwungene Leitplanken | Das Ergebnis einer Abfrage kann mithilfe der folgenden Methoden zur Verfügung gestellt werden:<ul><li>Kann als abgeleitete Datensätze gespeichert werden</li><li>Kann in die vorhandenen abgeleiteten Datensätze eingefügt werden</li></ul>Hinweis: Für die Anzahl der Einträge im Abfrageergebnis gibt es keine Obergrenze. |
| Ergebnisse zurückgegeben über | Datensatz | K. A. | Dadurch wird festgelegt, wie die Ergebnisse den Benutzern zur Verfügung gestellt werden. |

{style="table-layout:auto"}

## Abfrage-beschleunigte Speicherung {#query-accelerated-store}

Die nachstehende Tabelle enthält die empfohlenen Limits für Leitplanken und eine Beschreibung für den abfragebeschleunigten Speicher.

| Leitplanke | Limit | Art des Limits | Beschreibung |
|---|---|---|---|
| Parallelität von Abfragen | 4 | Vom System erzwungene Leitplanken | Um sicherzustellen, dass Abfragen zu aggregierten Daten über die Reporting-API (einschließlich Abfragen zur Verbesserung von Datenmodellen wie den Real-Time CDP-Datenmodellen) über die Ressourcen verfügen, die für eine effiziente Ausführung erforderlich sind, verfolgt die Reporting-API die Ressourcenauslastung, indem jeder Abfrage Slots für parallele Verarbeitung zugewiesen werden. Das System stellt Abfragen in eine Warteschlange und wartet, bis Parallelitätssteckplätze verfügbar sind oder sie aus dem Cache bereitgestellt werden können. Es stehen maximal vier gleichzeitige Abfrage-Slots zur Verfügung.<br>Wenn Sie über ein BI-Tool auf die Reporting-API zugreifen und mehr Gleichzeitigkeit benötigen, ist ein BI-Server erforderlich. |

{style="table-layout:auto"}

## Nächste Schritte

Nach dem Lesen dieses Dokuments sollten Sie die Standardbeschränkungen für die Ausführung von Abfragen mit den verfügbaren Abfragemustern besser verstehen.

In der folgenden Dokumentation finden Sie weitere Informationen zum Abfrage-Service:

* [Abfrage-Service-API](./api/getting-started.md)
* [Benutzeroberfläche von Query Service](./ui/overview.md)

In der folgenden Dokumentation finden Sie weitere Informationen zu anderen Experience Platform-Services-Leitplanken, zu End-to-End-Latenzinformationen und Lizenzinformationen aus den Produktbeschreibungsdokumenten von Real-Time CDP:

* [Real-Time CDP-Leitplanken](/help/rtcdp/guardrails/overview.md)
* [End-to-End-Latenzdiagramme](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) für verschiedene Experience Platform-Services.
* [Real-time Customer Data Platform (B2C Edition - Prime- und Ultimate-Pakete)](https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2P - Prime- und Ultimate-Pakete)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2B - Prime- und Ultimate-Pakete)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)