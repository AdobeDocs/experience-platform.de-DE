---
title: Datenverschlüsselung in Adobe Experience Platform
topic-legacy: data protection
description: Erfahren Sie, wie Daten im Transit und im Ruhezustand in Adobe Experience Platform verschlüsselt werden.
exl-id: 184b2b2d-8cd7-4299-83f8-f992f585c336
source-git-commit: d99a9081edc483831d56af3d838b67d9aba25bea
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 5%

---

# Datenverschlüsselung in Adobe Experience Platform

Adobe Experience Platform ist ein leistungsstarkes und erweiterbares System, das Kundenerlebnisdaten über Unternehmenslösungen hinweg zentralisiert und standardisiert. Alle von Platform verwendeten Daten werden während der Übertragung und im Ruhezustand verschlüsselt, um Ihre Daten sicher zu halten. In diesem Dokument werden die Verschlüsselungsprozesse von Platform auf hoher Ebene beschrieben.

Das folgende Prozessflussdiagramm zeigt, wie Daten erfasst, verschlüsselt und persistiert werden von [!DNL Experience Platform]:

![](../images/governance-privacy-security/encryption/flow.png)

## Durchfuhrdaten {#in-transit}

Alle Daten, die zwischen Platform und einer externen Komponente übertragen werden, werden über sichere, verschlüsselte Verbindungen mithilfe von HTTPS übertragen [TLS v1.2](https://datatracker.ietf.org/doc/html/rfc5246).

Im Allgemeinen werden Daten auf drei Arten in Platform importiert:

* [Datenerfassung](../../collection/home.md) -Funktionen ermöglichen es Websites und mobilen Anwendungen, Daten zum Staging und zur Vorbereitung auf die Aufnahme an das Platform Edge Network zu senden.
* [Quell-Connectoren](../../sources/home.md) Daten direkt aus Adobe Experience Cloud-Anwendungen und anderen Datenquellen für Unternehmen an Platform streamen.
* Nicht-Adobe-ETL-Tools (Extrahieren, Transformieren, Laden) senden Daten an die [Batch-Aufnahme-API](../../ingestion/batch-ingestion/overview.md) für den Verbrauch.

Nach dem Einbringen der Daten in das System und [im Ruhezustand verschlüsselt](#at-rest)kann sie dann durch Platform-Dienste angereichert und wie folgt aus dem System herausgezogen werden:

* [Ziele](../../destinations/home.md) ermöglichen es Ihnen, Daten für Adobe Apps und Partneranwendungen zu aktivieren.
* Native Platform-Anwendungen wie [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=de) und [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=de) kann auch die Daten nutzen.

## Ruhezeiten {#at-rest}

Daten, die von Platform erfasst und verwendet werden, werden im Data Lake gespeichert, einem hochgradig granularen Datenspeicher, der alle vom System verwalteten Daten enthält, unabhängig von Herkunft oder Dateiformat. Alle im Data Lake gespeicherten Daten werden verschlüsselt, gespeichert und in einem isolierten [[!DNL Microsoft Azure Data Lake] Speicherung](https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) -Instanz, die für Ihre Organisation eindeutig ist.

Weitere Informationen dazu, wie ruhende Daten in Azure Data Lake Storage verschlüsselt werden, finden Sie in der [offizielle Azure-Dokumentation](https://learn.microsoft.com/en-us/azure/storage/common/storage-service-encryption).

## Nächste Schritte

Dieses Dokument bietet einen allgemeinen Überblick darüber, wie Daten in Platform verschlüsselt werden. Weitere Informationen zu Sicherheitsverfahren in Platform finden Sie in der Übersicht unter [Governance, Datenschutz und Sicherheit](./overview.md) auf der Experience League oder sehen Sie sich die [Whitepaper zur Plattformsicherheit](https://www.adobe.com/content/dam/cc/en/security/pdfs/AEP_SecurityOverview.pdf).
