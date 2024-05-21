---
title: Datenverschlüsselung in Adobe Experience Platform
description: Erfahren Sie, wie Daten im Transit und im Ruhezustand in Adobe Experience Platform verschlüsselt werden.
exl-id: 184b2b2d-8cd7-4299-83f8-f992f585c336
source-git-commit: fd31d54339b8d87b80799a9c0fa167cc9a07a33f
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 0%

---

# Datenverschlüsselung in Adobe Experience Platform

Adobe Experience Platform ist ein leistungsstarkes und erweiterbares System, das Kundenerlebnisdaten über Unternehmenslösungen hinweg zentralisiert und standardisiert. Alle von Platform verwendeten Daten werden während der Übertragung und im Ruhezustand verschlüsselt, um Ihre Daten sicher zu halten. In diesem Dokument werden die Verschlüsselungsprozesse von Platform auf hoher Ebene beschrieben.

Das folgende Prozessflussdiagramm zeigt, wie Experience Platform Daten erfasst, verschlüsselt und beibehält:

![Ein Diagramm, das zeigt, wie Daten von Experience Platform erfasst, verschlüsselt und persistiert werden.](../images/governance-privacy-security/encryption/flow.png)

## Durchfuhrdaten {#in-transit}

Alle Daten, die zwischen Platform und einer externen Komponente übertragen werden, werden über sichere, verschlüsselte Verbindungen mithilfe von HTTPS übertragen [TLS v1.2](https://datatracker.ietf.org/doc/html/rfc5246).

Im Allgemeinen werden Daten auf drei Arten in Platform importiert:

- [Datenerfassung](../../collection/home.md) -Funktionen ermöglichen es Websites und mobilen Anwendungen, Daten zur Staging- und Aufnahmevorbereitung an das Platform-Edge Network zu senden.
- [Quell-Connectoren](../../sources/home.md) Daten direkt aus Adobe Experience Cloud-Anwendungen und anderen Datenquellen für Unternehmen an Platform streamen.
- Nicht-Adobe-ETL-Tools (Extract, Transform, Load) senden Daten an die [Batch-Aufnahme-API](../../ingestion/batch-ingestion/overview.md) für den Verbrauch.

Nach dem Einbringen der Daten in das System und [im Ruhezustand verschlüsselt](#at-rest), ergänzen und exportieren die Platform-Dienste die Daten wie folgt:

- [Ziele](../../destinations/home.md) ermöglichen es Ihnen, Daten für Adobe-Anwendungen und Partneranwendungen zu aktivieren.
- Native Platform-Anwendungen wie [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=de) und [Adobe Journey Optimizer](https://experienceleague.adobe.com/de/docs/journey-optimizer/using/ajo-home) kann auch die Daten nutzen.

### Unterstützung des mTLS-Protokolls {#mtls-protocol-support}

Sie können jetzt &quot;Mutual Transport Layer Security (mTLS)&quot;verwenden, um eine verbesserte Sicherheit bei ausgehenden Verbindungen zu HTTP-API-Zielen und benutzerdefinierten Aktionen in Adobe Journey Optimizer sicherzustellen. mTLS ist eine durchgängige Sicherheitsmethode für die gegenseitige Authentifizierung, mit der sichergestellt wird, dass beide Parteien, die Informationen teilen, diejenigen sind, die sie angeblich sind, bevor Daten freigegeben werden. mTLS umfasst einen zusätzlichen Schritt im Vergleich zu TLS, bei dem der Server auch das Zertifikat des Kunden anfordert und es auf dessen Ende überprüft.

#### mTLS in Adobe Journey Optimizer {#mtls-in-adobe-journey-optimizer}

In Adobe Journey Optimizer wird mTLS zusammen mit [benutzerdefinierte Aktionen](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions). Keine weiteren [Konfiguration für benutzerdefinierte Adobe Journey Optimizer-Aktionen](https://experienceleague.adobe.com/de/docs/journey-optimizer/using/configuration/configure-journeys/action-journeys/about-custom-action-configuration) ist von Ihrer Seite erforderlich, um mTLS zu aktivieren. Wenn der Endpunkt für eine benutzerdefinierte Aktion mTLS-fähig ist, ruft das System das Zertifikat aus dem Adobe Experience Platform-Keystore ab und stellt es automatisch an den -Endpunkt bereit (wie für mTLS-Verbindungen erforderlich).

Wenn Sie mTLS mit diesen Adobe Journey Optimizer- und Experience Platform-HTTP-API-Ziel-Workflows verwenden möchten, muss für die Serveradresse, die Sie in die Adobe Journey Optimizer-Benutzeroberfläche für Kundenaktionen oder die Benutzeroberfläche &quot;Ziele&quot;einfügen, die TLS-Protokolle deaktiviert und nur mTLS aktiviert sein. Wenn das TLS 1.2-Protokoll an diesem Endpunkt noch aktiviert ist, wird kein Zertifikat für die Client-Authentifizierung gesendet. Um mTLS mit diesen Workflows verwenden zu können, muss der &quot;Empfangs&quot;-Server-Endpunkt ein mTLS sein. **only** aktivierter Verbindungsendpunkt.

>[!IMPORTANT]
>
>In Ihrer benutzerdefinierten Aktion oder Ihrem Journey für Adobe Journey Optimizer ist keine zusätzliche Konfiguration erforderlich, um mTLS zu aktivieren. Dieser Vorgang erfolgt automatisch, wenn ein mTLS-fähiger Endpunkt erkannt wird. Die gebräuchlichen Namen (CN) und alternativen Namen des Betreffs (SAN) für jedes Zertifikat sind in der Dokumentation als Teil des Zertifikats verfügbar und können bei Bedarf als zusätzliche Ebene der Eigentümervalidierung verwendet werden.
>
>RFC 2818, veröffentlicht im Mai 2000, stellt die Verwendung des Felds &quot;Common Name&quot;(CN) in HTTPS-Zertifikaten zur Verifizierung des Subjektnamens ein. Stattdessen wird empfohlen, die Erweiterung &quot;Subject Alternative Name&quot;(SAN) des Typs &quot;DNS-Name&quot;zu verwenden.

### Zertifikate herunterladen {#download-certificates}

Wenn Sie die CN oder das SAN überprüfen möchten, um eine zusätzliche Validierung von Drittanbietern durchzuführen, können Sie die entsprechenden Zertifikate hier herunterladen:

- [Das öffentliche Adobe Journey Optimizer-Zertifikat](../images/governance-privacy-security/encryption/AJO-public-certificate.pem)
- [Das öffentliche Zertifikat des Zieldienstes](../images/governance-privacy-security/encryption/destinations-public-cert.pem).

## Ruhezeiten {#at-rest}

Daten, die von Platform erfasst und verwendet werden, werden im Data Lake gespeichert, einem hochgradig granularen Datenspeicher, der alle vom System verwalteten Daten enthält, unabhängig von Herkunft oder Dateiformat. Alle im Data Lake gespeicherten Daten werden verschlüsselt, gespeichert und in einem isolierten [[!DNL Microsoft Azure Data Lake] Speicherung](https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) -Instanz, die für Ihre Organisation eindeutig ist.

Weitere Informationen dazu, wie ruhende Daten in Azure Data Lake Storage verschlüsselt werden, finden Sie in der [offizielle Azure-Dokumentation](https://learn.microsoft.com/en-us/azure/storage/common/storage-service-encryption).

## Nächste Schritte

Dieses Dokument bietet einen allgemeinen Überblick darüber, wie Daten in Platform verschlüsselt werden. Weitere Informationen zu Sicherheitsverfahren in Platform finden Sie in der Übersicht unter [Governance, Datenschutz und Sicherheit](./overview.md) auf dem Experience League, oder schauen Sie sich die [Whitepaper zur Plattformsicherheit](https://www.adobe.com/content/dam/cc/en/security/pdfs/AEP_SecurityOverview.pdf).
