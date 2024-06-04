---
keywords: Experience Platform; Abfrage; Query Service; Fehlerbehebung; Limits; Richtlinien; Limit;
title: Limits für Query Service
description: Dieses Dokument enthält Informationen zu Nutzungsbeschränkungen für Query Service-Daten, die Ihnen bei der Optimierung Ihrer Abfrageverwendung helfen.
exl-id: 1ad5dcf4-d048-49ff-97e3-07040392b65b
source-git-commit: 5d6b70e397a252e037589c3200053ebcb7eb8291
workflow-type: tm+mt
source-wordcount: '1181'
ht-degree: 4%

---

# Limits für Query Service

Limits sind Schwellenwerte, die die Datennutzung und Systemnutzung, Leistungsoptimierung und Vermeidung von Fehlern oder unerwarteten Ergebnissen in Adobe Experience Platform lenken.
Dieses Dokument enthält standardmäßige Nutzungsbeschränkungen für Query Service-Daten, mit denen Sie die Systemleistung bei der Abfrage von Daten im Zusammenhang mit Ihren Lizenzberechtigungen optimieren können.

>[!IMPORTANT]
>
>Überprüfen Sie Ihre Lizenzberechtigungen in Ihrem Kundenauftrag und den entsprechenden [Produktbeschreibung](https://helpx.adobe.com/de/legal/product-descriptions.html) über die tatsächlichen Nutzungsbeschränkungen zusätzlich zu dieser Limits-Seite.

## Voraussetzungen

Bevor Sie mit diesem Dokument fortfahren, sollten Sie die wichtigsten Definitionen und Funktionen von Query Service kennen. Sie werden nachfolgend beschrieben:

* **Ad-hoc-Abfragen**: Für die Ausführung `SELECT` Abfragen zum Erkunden, Experimentieren und Validieren von Daten, in denen die Ergebnisse der Abfragen vorliegen **nicht gespeichert werden** auf dem Datensee.

* **Batch-Abfragen**: Für die Ausführung `INSERT TABLE AS SELECT` und `CREATE TABLE AS SELECT` Abfragen zum Bereinigen, Gestalten, Bearbeiten und Anreichern von Daten. Die Ergebnisse dieser Abfragen **gespeichert werden** auf dem Datensee. Die Metrik zur Messung des Verbrauchs dieser Funktion ist die Berechnung der Stunden.

* **Query Service-Benutzer**: Query Service-Benutzer, die in Ihrer aktuellen Lizenz für Customer Journey Analytics, Adobe Real-time Customer Data Platform und/oder Adobe Journey Optimizer bereitgestellt werden, können auch mit Data Distiller verwendet werden. Query Service-Benutzer werden zwischen Funktionen freigegeben.

* **Ad-hoc-Benutzer**: Ad-hoc-Benutzer sind Benutzer, die Ad-hoc-Abfragen ausführen.

* **Batch-Benutzer**: Batch-Benutzer sind diejenigen, die Batch-Abfragen ausführen.

* **Reporting-API**: Eine API für Datenabruf-Aufrufe (intern oder extern). Erweiterte Berichtsdatenmodelle werden aus den nativen Berichtsdatenmodellen in Adobe Experience Platform abgeleitet, z. B. dem Real-Time CDP Dashboards-Datenmodell.

Die folgende Abbildung fasst zusammen, wie Query Service-Funktionen derzeit zusammengefasst und lizenziert sind:

## Schutzarten

In diesem Dokument gibt es zwei Arten von Standardbeschränkungen:

| Schutztyp | Beschreibung |
|----------|---------|
| **Leistungsgarantie (weiche Begrenzung)** | Leistungsgarantien sind Nutzungsbeschränkungen, die sich auf das Scoping Ihrer Anwendungsfälle beziehen. Wenn Sie die Leistungsgarantien überschreiten, kann es zu Leistungseinbußen und Latenzzeiten kommen. Adobe ist nicht für eine solche Leistungsbeeinträchtigung verantwortlich. Kunden, die eine Leistungsgarantie konsequent überschreiten, können zusätzliche Kapazität lizenzieren, um Leistungsbeeinträchtigungen zu vermeiden. |
| **Systemerzwungene Limits (Hard Limit)** | Systemerzwungene Limits werden von der Real-Time CDP-Benutzeroberfläche oder -API erzwungen. Dies sind Beschränkungen, die Sie nicht überschreiten können, da die Benutzeroberfläche und API Sie davon abhält oder einen Fehler zurückgibt. |

{style="table-layout:auto"}

>[!NOTE]
>
>Die in diesem Dokument beschriebenen Standardbeschränkungen werden ständig verbessert. Achten Sie regelmäßig auf Updates.

## Limits bei der Primären Entitätsleistung

Die folgenden Tabellen enthalten die empfohlenen Limits und Beschreibungen für die Ausführung von Abfragen bei Verwendung eines bestimmten Abfragemusters.

**Ad-hoc-Abfragen**

| Leitplanke | Limit | Begrenzungstyp | Beschreibung |
|---|---|---|---|
| Maximale Ausführungsdauer | 10 Minuten | Systemerzwungene Limits | Dies definiert die maximale Ausgabedauer für eine Ad-hoc-SQL-Abfrage. Wenn Sie die Zeitbeschränkung zum Zurückgeben eines Ergebnisses überschreiten, wird der Fehlercode 53400 ausgegeben. |
| Gleichzeitige Query Service-Benutzer | <ul><li>Wie in der Produktbeschreibung der Anwendung angegeben.</li><li>+5 (mit jedem zusätzlichen Ad-hoc-Abfrage-Benutzer-Add-On-Paket gekauft)</li></ul> | Systemerzwungene Limits | Dadurch wird definiert, wie viele Benutzer Sitzungen für eine bestimmte Organisation gleichzeitig erstellen können. Wenn die gleichzeitige Beschränkung überschritten wird, erhält der Benutzer eine `Session Limit Reached` Fehler. |
| Abfrage-Parallelität | <ul><li>Wie in der Produktbeschreibung der Anwendung angegeben.</li><li>+1 (mit jedem zusätzlichen erworbenen Ad-hoc-Abfragebenutzer-Add-on-SKU-Paket)</li></ul> | Systemerzwungene Limits | Dadurch wird definiert, wie viele Abfragen für eine bestimmte Organisation gleichzeitig ausgeführt werden können. Wenn die gleichzeitige Beschränkung überschritten wird, werden die Abfragen in die Warteschlange gestellt. |
| Client-Connector und Ergebnisausgabegrenze | Client Connector<ul><li>Query UI (100 Zeilen)</li><li>Drittanbieter-Client (50.000)</li><li>[!DNL PostgresSQL] Client (50.000)</li></ul> | Systemerzwungene Limits | Das Ergebnis einer Abfrage kann auf folgende Weise empfangen werden:<ul><li>Benutzeroberfläche von Query Service</li><li>Drittanbieter-Client</li><li>[!DNL PostgresSQL] client</li></ul>Hinweis: Durch Hinzufügen einer Begrenzung zur Ausgabenanzahl können Ergebnisse schneller zurückgegeben werden. Beispielsweise `LIMIT 5`, `LIMIT 10` und so weiter. |
| Über zurückgegebene Ergebnisse | Client-Benutzeroberfläche | K. A. | Dadurch wird definiert, wie die Ergebnisse den Benutzern zur Verfügung gestellt werden. |

{style="table-layout:auto"}

**Batch-Abfragen**

| **Guardrail** | **Limit** | **Begrenzungstyp** | **Beschreibung** |
|---|---|---|---|
| Maximale Ausführungsdauer | 24 Stunden | Systemerzwungene Limits | Dies definiert die maximale Ausführungszeit für eine Batch-SQL-Abfrage.<br>Die Verarbeitungszeit einer Abfrage hängt von der Menge der zu verarbeitenden Daten und der Komplexität der Abfrage ab. |
| Gleichzeitige Query Service-Benutzer für nicht geplanten Batch | <ul><li>Wie in der Produktbeschreibung der Anwendung angegeben.</li><li>+5 (mit jedem zusätzlichen Ad-hoc-Abfrage-Benutzer-Add-On-Paket gekauft)</li></ul> | Systemerzwungene Limits | Bei ungeplanten Batch-Abfragen (z. B. CTAS/ITAS-Abfragen im interaktiven Modus) wird dadurch definiert, wie viele Benutzer Sitzungen für eine bestimmte Organisation gleichzeitig erstellen können. Wenn die gleichzeitige Beschränkung überschritten wird, erhält der Benutzer eine `Session Limit Reached` Fehler. |
| Gleichzeitige Query Service-Benutzer für geplanten Batch | Keine Benutzerbeschränkung | K. A. | Geplante Batch-Abfragen sind asynchrone Aufträge, sodass keine Benutzerbegrenzung besteht. |
| Berechnungsstunden für die Batch-Datenverarbeitung | Wie im Adobe Experience Platform Intelligence Query Query Query Custom SKU Sales Order des Kunden angegeben | Leistungsgarantie | Dies definiert den Umfang der Rechenzeit pro Jahr, die ein Kunde zum Ausführen von Batch-Abfragen zum Scannen, Verarbeiten und Zurückschreiben von Daten in den Data Lake hat. |
| Abfrage-Parallelität | Unterstützt | K. A. | Geplante Batch-Abfragen sind asynchrone Aufträge, daher werden gleichzeitige Abfragen unterstützt. |
| Client-Connector- und Ergebnisausgabegrenze | Client Connector<ul><li>Abfrage-Benutzeroberfläche (keine Obergrenze für Zeilen)</li><li>Drittanbieter-Client (keine Obergrenze für Zeilen)</li><li>[!DNL PostgresSQL] client (keine Obergrenze für Zeilen)</li><li>REST-APIs (keine Obergrenze für Zeilen)</li></ul> | Systemerzwungene Limits | Das Ergebnis einer Abfrage kann mithilfe der folgenden Methoden bereitgestellt werden:<ul><li>Kann als abgeleitete Datensätze gespeichert werden</li><li>Kann in die vorhandenen abgeleiteten Datensätze eingefügt werden</li></ul>Hinweis: Die Datensatzanzahl aus dem Abfrageergebnis ist nicht begrenzt. |
| Über zurückgegebene Ergebnisse | Datensatz | K. A. | Dadurch wird definiert, wie die Ergebnisse den Benutzern zur Verfügung gestellt werden. |

{style="table-layout:auto"}

## Abfrage-beschleunigter Speicher {#query-accelerated-store}

Die folgende Tabelle enthält die empfohlenen Limits und eine Beschreibung für den Abfrage-beschleunigten Speicher.

| Leitplanke | Limit | Begrenzungstyp | Beschreibung |
|---|---|---|---|
| Abfrage-Parallelität | 4 | Systemerzwungene Limits | Um sicherzustellen, dass Abfragen über aggregierte Daten über die Berichterstellungs-API (einschließlich Abfragen, die Datenmodelle wie die Real-Time CDP-Datenmodelle verbessern) über die Ressourcen verfügen, die für eine effiziente Ausführung benötigt werden, verfolgt die Berichterstellungs-API die Ressourcenauslastung durch Zuweisung von Zeitnischen für gleichzeitige Abfragen. Das System stellt Abfragen in eine Warteschlange und wartet, bis Zeitnischen für gleichzeitige Verwendung verfügbar sind oder sie aus dem Cache bereitgestellt werden können. Es stehen maximal vier gleichzeitige Abfragefenster zur Verfügung.<br>Wenn Sie über ein BI-Tool auf die Reporting-API zugreifen und mehr Parallelität benötigen, ist ein BI-Server erforderlich. |

{style="table-layout:auto"}

## Nächste Schritte

Nach dem Lesen dieses Dokuments sollten Sie die Standardbeschränkungen für die Ausführung von Abfragen mit den verfügbaren Abfragemustern besser verstehen.

Weitere Informationen zu Query Service finden Sie in der folgenden Dokumentation:

* [Query Service-API](./api/getting-started.md)
* [Benutzeroberfläche von Query Service](./ui/overview.md)

Weitere Informationen zu anderen Limits für Experience Platform-Services, End-to-End-Latenzinformationen und Lizenzinformationen aus Real-Time CDP Product Description-Dokumenten finden Sie in der folgenden Dokumentation:

* [Limits in Real-Time CDP](/help/rtcdp/guardrails/overview.md)
* [End-to-End-Latenzdiagramme](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) für verschiedene Experience Platform-Dienste.
* [Real-time Customer Data Platform (B2C Edition - Prime und Ultimate Packages)](https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2P - Prime und Ultimate Packages)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2B - Prime und Ultimate Packages)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)