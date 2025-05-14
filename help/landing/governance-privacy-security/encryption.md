---
title: Datenverschlüsselung in Adobe Experience Platform
description: Erfahren Sie, wie Daten bei der Übertragung und im Ruhezustand in Adobe Experience Platform verschlüsselt werden.
exl-id: 184b2b2d-8cd7-4299-83f8-f992f585c336
source-git-commit: f6eaba4c0622318ba713c562ba0a4c20bba02338
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 6%

---

# Datenverschlüsselung in Adobe Experience Platform

Adobe Experience Platform ist ein leistungsstarkes und erweiterbares System, das Kundenerlebnisdaten über Unternehmenslösungen hinweg zentralisiert und standardisiert. Alle von Experience Platform verwendeten Daten werden während der Übertragung und im Ruhezustand verschlüsselt, um Ihre Daten zu schützen. In diesem Dokument werden die Verschlüsselungsprozesse von Experience Platform auf einer allgemeinen Ebene beschrieben.

Das folgende Prozessflussdiagramm veranschaulicht, wie Experience Platform Daten aufnimmt, verschlüsselt und persistiert:

![Ein Diagramm, das veranschaulicht, wie Daten von Experience Platform aufgenommen, verschlüsselt und gespeichert werden.](../images/governance-privacy-security/encryption/flow.png)

## Daten werden übertragen {#in-transit}

Alle Daten, die zwischen Experience Platform und externen Komponenten übertragen werden, werden über sichere, verschlüsselte Verbindungen mit HTTPS ([ v1.2) ](https://datatracker.ietf.org/doc/html/rfc5246).

Im Allgemeinen werden Daten auf drei Arten in Experience Platform importiert:

- [Datenerfassung](../../collection/home.md) Funktionen ermöglichen es Websites und mobilen Apps, Daten zum Staging und zur Vorbereitung für die Aufnahme an Experience Platform Edge Network zu senden.
- [Source-Connectoren](../../sources/home.md) Streamen von Daten direkt aus Adobe Experience Cloud-Programmen und anderen Unternehmensdatenquellen an Experience Platform.
- Nicht-Adobe-ETL-Tools (Extract, Transform, Load) senden Daten zur Nutzung an [Batch-Aufnahme](../../ingestion/batch-ingestion/overview.md)API).

Nachdem Daten in das System eingebracht und [im Ruhezustand verschlüsselt](#at-rest) reichern Experience Platform-Services die Daten auf folgende Weise an und exportieren sie:

- [Ziele](../../destinations/home.md) ermöglichen es Ihnen, Daten für Adobe-Programme und Partneranwendungen zu aktivieren.
- Native Experience Platform-Programme wie [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=de) und [Adobe Journey Optimizer](https://experienceleague.adobe.com/de/docs/journey-optimizer/using/ajo-home) können ebenfalls die Daten verwenden.

### mTLS-Protokoll-Unterstützung {#mtls-protocol-support}

Sie können jetzt Mutual Transport Layer Security (mTLS) verwenden, um erweiterte Sicherheit bei ausgehenden Verbindungen zum [HTTP-API-Ziel](../../destinations/catalog/streaming/http-destination.md) und Adobe Journey Optimizer [benutzerdefinierte Aktionen](https://experienceleague.adobe.com/de/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions) zu gewährleisten. mTLS ist eine End-to-End-Sicherheitsmethode zur gegenseitigen Authentifizierung, die sicherstellt, dass beide Parteien, die Informationen austauschen, auch die sind, die sie vorgeben zu sein, bevor die Daten ausgetauscht werden. mTLS umfasst einen zusätzlichen Schritt im Vergleich zu TLS, bei dem der Server auch das Zertifikat der Kundin bzw. des Kunden anfordert und überprüft, ob es gültig ist.

Wenn Sie Workflows für [Verwendung von mTLS mit benutzerdefinierten Aktionen von Adobe Journey Optimizer](https://experienceleague.adobe.com/de/docs/journey-optimizer/using/configuration/configure-journeys/action-journeys/about-custom-action-configuration) und Experience Platform-HTTP-API-Zielen verwenden möchten, müssen für die Serveradresse, die Sie in die Benutzeroberfläche für Kundenaktionen von Adobe Journey Optimizer oder die Benutzeroberfläche für Ziele einfügen, TLS-Protokolle deaktiviert und nur mTLS aktiviert sein. Wenn das TLS 1.2-Protokoll für diesen Endpunkt noch aktiviert ist, wird kein Zertifikat für die Client-Authentifizierung gesendet. Das bedeutet, dass Ihr Empfangs-Server-Endpunkt bei der Verwendung von mTLS mit diesen Workflows ein mTLS-**Verbindungsendpunkt** muss.

>[!IMPORTANT]
>
>In Ihrer benutzerdefinierten Aktion oder Ihrem HTTP-API-Ziel von Adobe Journey Optimizer ist keine zusätzliche Konfiguration erforderlich, um mTLS zu aktivieren. Dieser Vorgang erfolgt automatisch, wenn ein mTLS-aktivierter Endpunkt erkannt wird. Die Common Name (CN)- und Subject Alternative Names (SAN) für jedes Zertifikat finden Sie in der Dokumentation als Teil des Zertifikats und können als zusätzliche Ebene für die Eigentümervalidierung verwendet werden, wenn Sie dies wünschen.
>
>In RFC 2818, veröffentlicht im Mai 2000, wird die Verwendung des Felds „Common Name (CN)“ in HTTPS-Zertifikaten zur Überprüfung des Antragstellernamens nicht mehr unterstützt. Stattdessen wird empfohlen, die Erweiterung „Subject Alternative Name“ (SAN) des Typs „dns name“ zu verwenden.

### Herunterladen von Zertifikaten {#download-certificates}

>[!NOTE]
>
>Sie sind dafür verantwortlich sicherzustellen, dass Ihre Systeme ein gültiges öffentliches Zertifikat verwenden. Überprüfen Sie Ihre Zertifikate regelmäßig, insbesondere wenn das Ablaufdatum näher rückt. Verwenden Sie die API, um Zertifikate abzurufen und zu aktualisieren, bevor sie ablaufen.

Direkte Download-Links für öffentliche mTLS-Zertifikate werden nicht mehr bereitgestellt. Verwenden Sie stattdessen den [Endpunkt für öffentliche Zertifikate](../../data-governance/mtls-api/public-certificate-endpoint.md) um Zertifikate abzurufen. Dies ist die einzige unterstützte Methode für den Zugriff auf aktuelle öffentliche Zertifikate. Dadurch wird sichergestellt, dass Sie immer gültige, aktuelle Zertifikate für Ihre Integrationen erhalten.

Integrationen, die auf zertifikatbasierter Verschlüsselung basieren, müssen ihre Workflows aktualisieren, um den automatischen Zertifikatabruf mithilfe der API zu unterstützen. Wenn Sie statische Links oder manuelle Aktualisierungen verwenden, können abgelaufene oder widerrufene Zertifikate verwendet werden, was zu fehlgeschlagenen Integrationen führen kann.

#### Automatisierung des Zertifikatlebenszyklus {#certificate-lifecycle-automation}

Adobe automatisiert jetzt den Zertifikatlebenszyklus für mTLS-Integrationen, um die Zuverlässigkeit zu verbessern und Service-Unterbrechungen zu vermeiden. Öffentliche Zertifikate sind:

- Erneut veröffentlicht 60 Tage vor Ablauf der Gültigkeit.
- 30 Tage vor Ablauf widerrufen.

Diese Intervalle werden entsprechend den [ Richtlinien des CA/B-Forums weiter verkürzt](https://www.digicert.com/blog/tls-certificate-lifetimes-will-officially-reduce-to-47-days) mit dem Ziel, die Zertifikatlebensdauer auf maximal 47 Tage zu reduzieren.

Wenn Sie zuvor über Links auf dieser Seite Zertifikate heruntergeladen haben, aktualisieren Sie Ihren Prozess, um diese ausschließlich über die API abzurufen.

## Ruhende Daten {#at-rest}

Daten, die von Experience Platform aufgenommen und verwendet werden, werden im Data Lake gespeichert, einem hochgradig granularen Datenspeicher, der unabhängig von Herkunft oder Dateiformat alle vom System verwalteten Daten enthält. Alle im Data Lake persistierten Daten werden in einer für Ihre Organisation eindeutigen, isolierten [[!DNL Microsoft Azure Data Lake] Storage](https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction)-Instanz verschlüsselt, gespeichert und verwaltet.

Einzelheiten dazu, wie Data-at-Rest im Azure Data Lake Storage verschlüsselt werden, finden Sie in der [offiziellen Azure-Dokumentation](https://learn.microsoft.com/en-us/azure/storage/common/storage-service-encryption).

## Nächste Schritte

Dieses Dokument bietet einen allgemeinen Überblick darüber, wie Daten in Experience Platform verschlüsselt werden. Weitere Informationen zu Sicherheitsverfahren in Experience Platform finden Sie in der Übersicht zu [Governance, Datenschutz und Sicherheit](./overview.md) auf Experience League oder im [Experience Platform-Sicherheits-Whitepaper](https://www.adobe.com/content/dam/cc/en/security/pdfs/AEP_SecurityOverview.pdf).
