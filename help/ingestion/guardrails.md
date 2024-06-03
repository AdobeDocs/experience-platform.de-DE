---
keywords: Experience Platform;Fehlerbehebung;Leitplanken;Richtlinien;
title: Schutzmaßnahmen bei der Datenaufnahme
description: Erfahren Sie mehr über Limits für die Datenerfassung in Adobe Experience Platform.
exl-id: f07751cb-f9d3-49ab-bda6-8e6fec59c337
source-git-commit: cdc5bb01ef6de8134c6ad4ef6601a748571bf86f
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 52%

---

# Schutzmaßnahmen bei der Datenaufnahme

>[!IMPORTANT]
>
>Limits für die Batch- und Streaming-Erfassung werden auf Organisationsebene und nicht auf Sandbox-Ebene berechnet. Das bedeutet, dass Ihre Datennutzung pro Sandbox an die gesamte Berechtigung zur Lizenznutzung gebunden ist, die Ihrer gesamten Organisation entspricht. Darüber hinaus ist die Datennutzung in Entwicklungs-Sandboxes auf 10 % Ihrer Gesamtprofile beschränkt. Weitere Informationen zur Lizenzverwendungsberechtigung finden Sie im Abschnitt [Best Practices für das Datenmanagement - Handbuch](../landing/license-usage-and-guardrails/data-management-best-practices.md).

Leitplanken sind Schwellenwerte, die Anhaltspunkte für die Daten- und Systemnutzung, die Performance-Optimierung und die Vermeidung von Fehlern oder unerwarteten Ergebnissen in Adobe Experience Platform bieten. Leitplanken können sich auf Ihre Nutzung oder Verwendung von Daten und Verarbeitung im Zusammenhang mit Ihren Lizenzierungsberechtigungen beziehen.

Dieses Dokument enthält Anleitungen zu Schutzmaßnahmen bei der Datenaufnahme in Adobe Experience Platform.

## Schutzmaßnahmen bei der Batch-Aufnahme

In der folgenden Tabelle sind Schutzmaßnahmen aufgeführt, die bei der Verwendung der [Batch-Aufnahme-API](./batch-ingestion/overview.md) oder von Quellen zu beachten sind:

| Art der Aufnahme | Leitlinien | Anmerkungen |
| --- | --- | --- |
| Data-Lake-Aufnahme mithilfe der Batch-Aufnahme-API | <ul><li>Mit der Batch-Aufnahme-API können Sie bis zu 20 GB Daten pro Stunde in den Data Lake aufnehmen.</li><li>Die maximale Anzahl von Dateien pro Batch beträgt 1.500.</li><li>Die maximale Batch-Größe beträgt 100 GB.</li><li>Die maximale Anzahl von Eigenschaften oder Feldern pro Zeile beträgt 10.000.</li><li>Die maximale Anzahl der Batches pro Minute und anwendender Person beträgt 138.</li></ul> | |
| Data-Lake-Aufnahme mithilfe von Batch-Quellen | <ul><li>Sie können mit Batch-Aufnahme-Quellen wie [!DNL Azure Blob], [!DNL Amazon S3] und [!DNL SFTP] bis zu 200 GB Daten pro Stunde in den Data Lake aufnehmen.</li><li>Die Batch-Größe sollte zwischen 256 MB und 100 GB liegen. Dies gilt sowohl für unkomprimierte als auch für komprimierte Daten. Wenn komprimierte Daten im Data Lake unkomprimiert sind, gelten diese Einschränkungen.</li><li>Die maximale Anzahl von Dateien pro Batch beträgt 1.500.</li><li>Die Mindestgröße einer Datei oder eines Ordners beträgt 1 Byte. Es ist nicht möglich, Dateien oder Ordner mit der Größe 0 Byte zu erfassen.</li></ul> | Lesen Sie die [Quellen - Übersicht](../sources/home.md) für einen Katalog von Quellen, die Sie für die Datenerfassung verwenden können. |
| Batch-Aufnahme in Profil | <ul><li>Die maximale Größe einer Datensatzklasse beträgt 100 KB (fest).</li><li>Die maximale Größe einer ExperienceEvent-Klasse beträgt 10 KB (hart).</li></ul> | |
| Anzahl der täglich aufgenommenen Profil- oder ExperienceEvent-Batches | **Die maximale Anzahl von Profil- oder ExperienceEvent-Batches, die pro Tag aufgenommen werden, beträgt 90.** Das bedeutet, dass die Gesamtanzahl der pro Tag aufgenommenen Profil- und ExperienceEvent-Batches 90 nicht überschreiten darf. Das Aufnehmen zusätzlicher Batches beeinträchtigt die System-Performance. | Dies ist ein weiches Limit. Es ist möglich, über ein weiches Limit hinauszugehen, jedoch stellen weiche Limits einen empfohlenen Richtwert für die System-Performance dar. |

## Schutzmaßnahmen bei der Streaming-Aufnahme

Lesen Sie die [Streaming-Erfassung - Übersicht](./streaming-ingestion/overview.md) für Informationen zu Limits für die Streaming-Erfassung.

## Limits für Streaming-Quellen

In der folgenden Tabelle sind die bei der Verwendung von Streaming-Quellen zu berücksichtigenden Limits aufgeführt:

| Art der Aufnahme | Leitlinien | Anmerkungen |
| --- | --- | --- |
| Streaming-Quellen | <ul><li>Die maximale Datensatzgröße beträgt 1 MB, wobei die empfohlene Größe bei 10 KB liegt.</li><li>Streaming-Quellen unterstützen bei der Aufnahme in den Data Lake zwischen 4.000 und 5.000 Anfragen pro Sekunde. Dies gilt für beide neu erstellten Quellverbindungen zusätzlich zu den bestehenden Quellverbindungen. **Hinweis**: Es kann bis zu 30 Minuten dauern, bis die Streaming-Daten vollständig im Data Lake verarbeitet sind.</li><li>Streaming-Quellen unterstützen maximal 1.500 Anfragen pro Sekunde bei der Aufnahme von Daten in Profil- oder Streaming-Segmentierung.</li></ul> | Streaming-Quellen wie [!DNL Kafka], [!DNL Azure Event Hubs] und [!DNL Amazon Kinesis] verwenden nicht die Route des [!DNL Data Collection Core Service] (DCCS) und können unterschiedliche Durchsatzbeschränkungen aufweisen. In der [Quellenübersicht](../sources/home.md) finden Sie einen Katalog der Quellen, die Sie für die Datenaufnahme verwenden können. |

## Nächste Schritte

Weitere Informationen zu anderen Limits für Experience Platform-Services, End-to-End-Latenzinformationen und Lizenzinformationen aus Real-Time CDP Product Description-Dokumenten finden Sie in der folgenden Dokumentation:

* [Limits in Real-Time CDP](/help/rtcdp/guardrails/overview.md)
* [End-to-End-Latenzdiagramme](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) für verschiedene Experience Platform-Dienste.
* [Real-time Customer Data Platform (B2C Edition - Prime und Ultimate Packages)](https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2P - Prime und Ultimate Packages)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2B - Prime und Ultimate Packages)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
