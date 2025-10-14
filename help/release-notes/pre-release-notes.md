---
title: Hinweise zu Vorabversionen von Experience Platform
description: Eine Vorschau der neuesten Versionshinweise für Adobe Experience Platform.
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: 9cf809f8fd6e424b4dcd800c3d554e4eb0e337dc
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 16%

---

# Hinweise zu Vorabversionen von Adobe Experience Platform

>[!IMPORTANT]
>
>Dieses Dokument ist als **Vorschau** der Versionshinweise für den aktuellen Monat gedacht. Release-Elemente können sich ändern und in der endgültigen Version hinzugefügt oder entfernt werden.

>[!TIP]
>
>Versionshinweise zu anderen Adobe Experience Platform-Programmen finden Sie in der folgenden Dokumentation:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/de/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/de/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/releases/pre-release-notes)
>- [Komposition föderierter Zielgruppen](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/en/docs/real-time-cdp-collaboration/using/latest)

**Veröffentlichungsdatum: Oktober 2025**

Neue Funktionen und Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Warnhinweise](#alerts)
- [Ziele](#destinations)
- [Segmentierungs-Service](#segmentation-service)
- [Quellen](#sources)

## Warnhinweise {#alerts}

Mit Experience Platform können Sie ereignisbasierte Warnhinweise für verschiedene Experience Platform-Aktivitäten abonnieren. Sie können unterschiedliche Warnhinweisregeln über die Registerkarte [!UICONTROL Warnhinweise] in der Benutzeroberfläche von Experience Platform abonnieren. Zusätzlich können Sie auswählen, ob Warnhinweise in der Benutzeroberfläche oder über E-Mail-Benachrichtigungen angezeigt werden sollen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Warnhinweis bei Zielausfallrate | Für Ziele wurde ein neuer Warnhinweis hinzugefügt: **Zielausfallrate überschreitet Schwellenwert**. Dieser Warnhinweis benachrichtigt Sie, wenn die Anzahl fehlgeschlagener Datensätze während der Datenaktivierung den zulässigen Schwellenwert überschritten hat, sodass Sie schnell auf Aktivierungsprobleme reagieren können. |

{style="table-layout:auto"}

Weitere Informationen zu Warnhinweisen finden Sie im Abschnitt [[!DNL Observability Insights] Übersicht](../observability/home.md).

## Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Funktionen**

| Ziel | Beschreibung |
| --- | --- |
| [!DNL AdForm] | Verwenden Sie dieses Ziel, um Adobe Real-Time CDP-Zielgruppen zur Aktivierung basierend auf der Experience Cloud ID (ECID) und der ID Fusion von [!DNL AdForm] an [!DNL AdForm] zu senden. ID Fusion von [!DNL AdForm] ist ein Service zur ID-Auflösung, mit dem Sie Ihre First-Party-Zielgruppen basierend auf der Experience Cloud ID (ECID) aktivieren können. |
| `Amazon Ads` | Wir haben zusätzliche persönliche IDs hinzugefügt, die Unterstützung von `firstName`, `lastName`, `street`, `city`, `state`, `zip` und `country` bieten. Die Zuordnung dieser Felder als Zielidentitäten kann die Übereinstimmungsraten der Zielgruppen verbessern. |

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Unterstützung für [!DNL AES256] Server-seitige Verschlüsselung in [!DNL Amazon S3] Zielen | [!DNL Amazon S3]-Ziele unterstützen jetzt [!DNL AES256] Server-seitige Verschlüsselung und bieten somit eine erweiterte Sicherheit für Ihre exportierten Daten. Sie können diese Verschlüsselungsmethode beim Einrichten oder Aktualisieren Ihrer [!DNL Amazon S3]-Zielverbindungen konfigurieren, um sicherzustellen, dass Ihre Daten im Ruhezustand mithilfe von [!DNL AES256]-Verschlüsselungsalgorithmen nach Industriestandard verschlüsselt werden. Weitere Informationen finden Sie in der [[!DNL Amazon] Dokumentation](https://docs.aws.amazon.com/AmazonS3/latest/userguide/UsingEncryption.html). |
| [Verschiedene neue Ziele, die die Überwachung auf Zielgruppenebene unterstützen](../dataflows/ui/monitor-destinations.md#audience-level-view) | Die folgenden Ziele unterstützen jetzt die Überwachung auf Zielgruppenebene: <ul><li>[!DNL Airship Tags]</li><li>(API) [!DNL Salesforce Marketing Cloud]</li><li>[!DNL Marketo Engage]</li><li>[!DNL Microsoft Bing]</li><li>(v1) [!DNL Pega CDH Realtime Audience]</li><li>(v2) [!DNL Pega CDH Realtime Audience]</li><li>[!DNL Salesforce Marketing Cloud] Kontointeraktion</li><li>[!DNL The Trade Desk]</li></ul> |
| Fehlerbehebung bei Leitplanken für den Datensatzexport | Es wurde eine Korrektur für die Leitplanken für den Datensatzexport implementiert. Zuvor wurden einige Datensätze, die eine Zeitstempelspalte enthielten, aber _nicht_ auf dem XDM-Erlebnisereignis-Schema basierten, fälschlicherweise als Erlebnisereignis-Datensätze behandelt, was die Exporte auf ein 365-tägiges Lookback-Fenster beschränkte. Die dokumentierte 365-Tage-Lookback-Schutzmaßnahme gilt jetzt ausschließlich für Experience Events-Datensätze. Datensätze, die ein anderes Schema als das XDM-Erlebnisereignis-Schema verwenden, werden jetzt von der Leitplanke für 10 Milliarden Datensätze geregelt. Einige Kunden sehen möglicherweise höhere Exportzahlen für Datensätze, die fälschlicherweise unter das 365-tägige Lookback-Fenster fielen. Auf diese Weise können Sie Datensätze für prädiktive Workflows exportieren, die über ein langes Lookback-Fenster verfügen. Weitere Informationen finden Sie unter [Leitplanken für Datensatzexporte](../destinations/guardrails.md#dataset-exports). |
| Verbessertes Reporting auf Zielgruppenebene für Unternehmensziele | Verbesserte Berichtslogik auf Zielgruppenebene für Unternehmensziele. Nach dieser Version erhalten Kundinnen und Kunden genauere Zahlen für Zielgruppenberichte, die nur Zielgruppen enthalten, die für das ausgewählte Ziel relevant sind. Diese Anpassung der Überwachung stellt sicher, dass die Berichterstellung nur Zielgruppen umfasst, die dem Datenfluss zugeordnet sind, und bietet somit klarere Einblicke in die tatsächliche Datenaktivierung. Dies wirkt sich nicht auf die Menge der aktivierten Daten aus. Es handelt sich lediglich um eine Verbesserung der Überwachung zur Verbesserung der Reporting-Genauigkeit. |

Weitere Informationen finden Sie unter [Ziele - Übersicht](../destinations/home.md).

## Segmentierungs-Service {#segmentation-service}

[!DNL Segmentation Service] definiert eine bestimmte Teilmenge von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Zielgruppen können auf Datensatzdaten (z. B. demografische Informationen) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Überwachung der Streaming-Segmentierung | Die Echtzeitüberwachung für Streaming-Segmentierung bietet Transparenz in Bezug auf Metriken zur Bewertungsrate, Latenz und Datenqualität auf Sandbox-, Datensatz- und Zielgruppenebene. Dies unterstützt proaktive Warnhinweise und umsetzbare Einblicke, um Dateningenieuren dabei zu helfen, Kapazitätsverletzungen und Aufnahmeprobleme zu identifizieren. Zu den Überwachungsmetriken gehören Auswertungsrate, P95-Aufnahmelatenz sowie empfangene, ausgewertete, fehlgeschlagene und übersprungene Datensätze. Die Funktionen für Datensatz- und Zielgruppenansicht bieten umfassende Einblicke in neue qualifizierte und disqualifizierte Profile. |

Weitere Informationen finden Sie in der [[!DNL Segmentation Service] Übersicht](../segmentation/home.md).

## Quellen {#sources}

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue oder aktualisierte Quellen**

| Quelle | Beschreibung |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Talon.one] Quellen für Treuedaten | Verwenden Sie die [!DNL Talon.One], um Batch- und Streaming-Treueprogramm-Daten in Experience Platform aufzunehmen. Der Connector unterstützt das Streaming von Profildaten, Transaktionsdaten und Treuedaten, einschließlich der verdienten Punkte, eingelösten Punkte, abgelaufenen Punkte und Stufendaten. |

**Aktualisierte Quellen**

| Quelle | Beschreibung |
| --- | --- |
| Allgemeine Verfügbarkeit der [!DNL Google Ads] (nur API) | Die API-Version der [!DNL Google Ads] ist jetzt allgemein verfügbar. Die API-Dokumentation wurde aktualisiert und zeigt nun, dass die neueste Version `v21` ist. Experience Platform unterstützt alle Versionen v19 und höher. Die Benutzeroberflächenversion bleibt in der Beta-Phase und unterstützt nur eine einmalige Aufnahme. Verwenden Sie die API-Route, um die inkrementelle Datenaufnahme zu verwenden. |
| Unterstützung virtueller [!DNL Azure Event Hubs] | Adobe unterstützt jetzt explizit virtuelle Netzwerkverbindungen zu Azure Event Hubs, wodurch die Datenübertragung über private Netzwerke anstatt über öffentliche Netzwerke ermöglicht wird. Auf die Zulassungsliste setzen Kunden können mit Experience Platform VNet den Traffic von Event Hubs privat über das private Azure-Backbone routen und so erweiterte Sicherheit und Compliance für Workflows zur Datenaufnahme bieten. |

Weitere Informationen finden Sie unter [Quelle – Übersicht](../sources/home.md).
