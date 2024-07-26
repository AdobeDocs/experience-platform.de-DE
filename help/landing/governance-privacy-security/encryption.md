---
title: Datenverschlüsselung in Adobe Experience Platform
description: Erfahren Sie, wie Daten im Transit und im Ruhezustand in Adobe Experience Platform verschlüsselt werden.
exl-id: 184b2b2d-8cd7-4299-83f8-f992f585c336
source-git-commit: f0b9d414d7b08015478c132de6910629d86c9cf9
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 8%

---

# Datenverschlüsselung in Adobe Experience Platform

Adobe Experience Platform ist ein leistungsstarkes und erweiterbares System, das Kundenerlebnisdaten über Unternehmenslösungen hinweg zentralisiert und standardisiert. Alle von Platform verwendeten Daten werden während der Übertragung und im Ruhezustand verschlüsselt, um Ihre Daten sicher zu halten. In diesem Dokument werden die Verschlüsselungsprozesse von Platform auf hoher Ebene beschrieben.

Das folgende Prozessflussdiagramm zeigt, wie Experience Platform Daten erfasst, verschlüsselt und beibehält:

![Ein Diagramm, das zeigt, wie Daten von Experience Platform erfasst, verschlüsselt und persistiert werden.](../images/governance-privacy-security/encryption/flow.png)

## Durchfuhrdaten {#in-transit}

Alle Daten, die zwischen Platform und einer externen Komponente übertragen werden, werden über sichere, verschlüsselte Verbindungen mit HTTPS [TLS v1.2](https://datatracker.ietf.org/doc/html/rfc5246) durchgeführt.

Im Allgemeinen werden Daten auf drei Arten in Platform importiert:

- Mit den Funktionen zur [Datenerfassung](../../collection/home.md) können Websites und mobile Anwendungen Daten zum Staging und zur Vorbereitung auf die Erfassung an das Platform-Edge Network senden.
- [Source Connectors](../../sources/home.md) streamen Daten direkt von Adobe Experience Cloud-Anwendungen und anderen Unternehmensdatenquellen an Platform.
- Nicht-Adobe-ETL-Tools (Extract, Transform, Load) senden Daten zur Verwendung an die [Batch-Aufnahme-API](../../ingestion/batch-ingestion/overview.md).

Nachdem Daten in das System importiert und [im Rest](#at-rest) verschlüsselt wurden, reichern Platform-Dienste die Daten wie folgt an und exportieren sie:

- Mit [Zielen](../../destinations/home.md) können Sie Daten für Adobe-Anwendungen und Partneranwendungen aktivieren.
- Native Platform-Anwendungen wie [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=de) und [Adobe Journey Optimizer](https://experienceleague.adobe.com/de/docs/journey-optimizer/using/ajo-home) können auch die Daten verwenden.

### mTLS-Protokoll-Unterstützung {#mtls-protocol-support}

Sie können jetzt &quot;Mutual Transport Layer Security (mTLS)&quot;verwenden, um eine höhere Sicherheit bei ausgehenden Verbindungen mit dem [HTTP-API-Ziel](../../destinations/catalog/streaming/http-destination.md) und den benutzerdefinierten Aktionen](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions) von Adobe Journey Optimizer [sicherzustellen. mTLS ist eine End-to-End-Sicherheitsmethode zur gegenseitigen Authentifizierung, die sicherstellt, dass beide Parteien, die Informationen austauschen, auch die sind, die sie vorgeben zu sein, bevor die Daten ausgetauscht werden. mTLS umfasst einen zusätzlichen Schritt im Vergleich zu TLS, bei dem der Server auch das Zertifikat der Kundin bzw. des Kunden anfordert und überprüft, ob es gültig ist.

Wenn Sie mTLS mit benutzerdefinierten Adobe Journey Optimizer-Aktionen](https://experienceleague.adobe.com/de/docs/journey-optimizer/using/configuration/configure-journeys/action-journeys/about-custom-action-configuration) und Experience Platform-HTTP-API-Ziel-Workflows verwenden möchten, müssen für die Serveradresse, die Sie in die Adobe Journey Optimizer-Benutzeroberfläche für Kundenaktionen oder die Benutzeroberfläche &quot;Ziele&quot;einfügen, TLS-Protokolle deaktiviert und nur mTLS aktiviert sein. [ Wenn das TLS 1.2-Protokoll an diesem Endpunkt noch aktiviert ist, wird kein Zertifikat für die Client-Authentifizierung gesendet. Damit mTLS mit diesen Workflows verwendet werden kann, muss der &quot;Empfangs&quot;-Server-Endpunkt ein mTLS **only**-aktivierter Verbindungs-Endpunkt sein.

>[!IMPORTANT]
>
>In Ihrer benutzerdefinierten Aktion für Adobe Journey Optimizer oder Ihrem HTTP-API-Ziel ist keine zusätzliche Konfiguration erforderlich, um mTLS zu aktivieren. Dieser Prozess erfolgt automatisch, wenn ein mTLS-fähiger Endpunkt erkannt wird. Die gebräuchlichen Namen (CN) und alternativen Namen des Betreffs (SAN) für jedes Zertifikat sind in der Dokumentation als Teil des Zertifikats verfügbar und können bei Bedarf als zusätzliche Ebene der Eigentümervalidierung verwendet werden.
>
>RFC 2818, veröffentlicht im Mai 2000, stellt die Verwendung des Felds &quot;Common Name&quot;(CN) in HTTPS-Zertifikaten zur Verifizierung des Subjektnamens ein. Stattdessen wird empfohlen, die Erweiterung &quot;Subject Alternative Name&quot;(SAN) des Typs &quot;DNS-Name&quot;zu verwenden.

### Zertifikate herunterladen {#download-certificates}

>[!NOTE]
>
>Es liegt in Ihrer Verantwortung, das öffentliche Zertifikat auf dem neuesten Stand zu halten. Achten Sie darauf, dass Sie das Zertifikat regelmäßig überprüfen, zumal sein Ablaufdatum näher rückt. Sie sollten diese Seite mit einem Lesezeichen versehen, um die neueste Kopie in Ihrer Umgebung zu erhalten.

Wenn Sie die CN oder das SAN überprüfen möchten, um eine zusätzliche Validierung von Drittanbietern durchzuführen, können Sie die entsprechenden Zertifikate hier herunterladen:

- [Das öffentliche Adobe Journey Optimizer-Zertifikat](../images/governance-privacy-security/encryption/AJO-public-certificate.pem)
- [Das öffentliche Zertifikat des Zieldienstes ](../images/governance-privacy-security/encryption/destinations-public-cert.pem).

Sie können auch öffentliche Zertifikate sicher abrufen, indem Sie eine GET-Anfrage an den MTLS-Endpunkt senden. Weitere Informationen finden Sie in der Dokumentation zum [öffentlichen Zertifikatendpunkt](../../data-governance/mtls-api/public-certificate-endpoint.md) .

## Ruhezeiten {#at-rest}

Daten, die von Platform erfasst und verwendet werden, werden im Data Lake gespeichert, einem hochgradig granularen Datenspeicher, der alle vom System verwalteten Daten enthält, unabhängig von Herkunft oder Dateiformat. Alle im Data Lake persistenten Daten werden in einer isolierten [[!DNL Microsoft Azure Data Lake] Speicher](https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) -Instanz verschlüsselt, gespeichert und verwaltet, die für Ihr Unternehmen eindeutig ist.

Weitere Informationen dazu, wie ruhende Daten in Azure Data Lake Storage verschlüsselt werden, finden Sie in der [offiziellen Azure-Dokumentation](https://learn.microsoft.com/en-us/azure/storage/common/storage-service-encryption).

## Nächste Schritte

Dieses Dokument bietet einen allgemeinen Überblick darüber, wie Daten in Platform verschlüsselt werden. Weitere Informationen zu Sicherheitsverfahren in Platform finden Sie in der Übersicht zu [Governance, Datenschutz und Sicherheit](./overview.md) auf dem Experience League oder im Whitepaper [Plattformsicherheit](https://www.adobe.com/content/dam/cc/en/security/pdfs/AEP_SecurityOverview.pdf).
