---
title: Leitlinien für die Performance der Edge Network Server-API
description: Erfahren Sie, wie Sie die Server-API in optimalen Leistungsgarantien verwenden.
exl-id: 063d0fbb-26d1-4727-9dea-8e7223b2173d
source-git-commit: 6414168c1deb047af30d8636ef8d61316f56aecf
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 5%

---


# Leitlinien für die Performance der Edge Network Server-API

## Übersicht {#overview}

Leistungsgarantien definieren Nutzungsbeschränkungen im Zusammenhang mit Anwendungsfällen Ihrer Server-API. Eine Überschreitung der in diesem Artikel beschriebenen Leistungsgarantien könnte zu einer Leistungsbeeinträchtigung führen.

Adobe ist nicht für Leistungsbeeinträchtigungen verantwortlich, die durch überschrittene Nutzungsbeschränkungen verursacht werden. Kunden, die die Leistungsgarantien konsequent überschreiten, können zusätzliche Verarbeitungskapazität anfordern, um eine Leistungsbeeinträchtigung zu vermeiden.

>[!IMPORTANT]
>
>Überprüfen Sie Ihre Lizenzberechtigungen in Ihrem Kundenauftrag und die entsprechende [Produktbeschreibung](https://helpx.adobe.com/de/legal/product-descriptions.html) auf die tatsächlichen Nutzungsbeschränkungen zusätzlich zu dieser Limits-Seite.

Alle auf dieser Seite beschriebenen Leistungsgarantien gelten für die IMS-Organisation. Für Benutzer mit mehreren konfigurierten IMS-Organisationen unterliegt jede Organisation den nachstehenden Leistungsgarantien. Weitere Informationen zu [!DNL IMS Organizations] finden Sie im [Experience Platform-Glossar](../landing/glossary.md) .

## Definitionen

* **Verfügbarkeit** wird für jedes fünfminütige Intervall als Prozentsatz der vom Experience Platform-Edge Network verarbeiteten Anforderungen berechnet, die nicht fehlschlagen und sich ausschließlich auf die bereitgestellten Edge Network-APIs beziehen. Wenn ein Mandant in einem bestimmten Fünfminüterintervall keine Anforderungen gestellt hat, gilt dieses Intervall als zu 100 % verfügbar.
* **Monatlicher Uptime-Prozentsatz** für eine bestimmte Region wird als Durchschnitt der Verfügbarkeit für alle 5-Minuten-Intervalle in einem Monat berechnet.
* Ein **Upstream** ist ein Dienst hinter dem Edge Network, der für einen bestimmten Datastream aktiviert ist, z. B. Adobe Server Side Forwarding, Adobe Edge Segmentation oder Adobe Target.
* Eine **Anfrageeinheit** entspricht einem 8-KB-Fragment einer Anforderung und einem für einen Datastream vorkonfigurierten vorgelagerten Fragment.
* Eine **Anfrage** ist eine einzelne Nachricht, die von einer kundeneigenen Anwendung an die [!DNL Server API] gesendet wird. Eine Anforderung kann eine oder mehrere Anfrageeinheiten enthalten.
* Ein **error** ist eine Anforderung, die aufgrund eines Edge Networks [internal service error](error-handling.md) fehlschlägt.

## Dienstbeschränkungen

Alle Datastreams erzwingen bestimmte Nutzungsbeschränkungen, die hauptsächlich steuern, wie viele Ereignisse gleichzeitig gesendet werden können, wie ihre Größe und die Anzahl der Upstream-Dienste, an die diese Anfragen weitergeleitet werden.

### Anfrageeinheiten

Alle Beschränkungen werden über eine **Anfrageeinheit (RU)** angewendet und normalisiert, die als **8-KB-Fragment** einer Anforderung für einen in einem Datastream konfigurierten Upstream-Dienst definiert ist.

#### Beispiele

| Nach Datastream konfigurierte Upstreams | Durchschnittliche Anforderungsgröße | Anfrageeinheiten |
| --- | --- | --- |
| 1 (Adobe Platform) | 8 KB (1 Fragment) | 1 |
| 2 (Adobe Platform, Adobe Target) | 8 KB (1 Fragment) | 2 |
| 2 (Adobe Platform, Adobe Target) | 16 KB (2 Fragmente) | 4 |
| 2 (Adobe Platform, Adobe Target) | 64 KB (8 Fragmente) | 16 |

### Einschränkungen für Anfrageeinheiten

Die folgende Tabelle zeigt die Standardgrenzwerte. Wenden Sie sich an Ihren Kundenbetreuer, wenn Sie höhere Anforderungseinheiten benötigen.

| Endpunkt | Anforderungen von Einheiten pro Sekunde |
| --- | --- |
| `/v2/interact` | 4.000 |
| `/v2/collect` | 6000 |

### HTTP-Anfragegrößenbeschränkung

| Payload-Format | Maximale Größe für eine Anforderung | Max. 8 KB Anforderungsfragmente |
| --- | --- | --- |
| JSON-Klartext | 64 KB | 8 |


>[!NOTE]
>
>Abhängig von der Payload selbst sind die binären Formate im Allgemeinen 20-40 % kompakter, sodass Sie mehr Daten als im Nur-Text-JSON übertragen können. Wenden Sie sich an Ihren Kundenbetreuer, wenn Sie eine höhere Kapazität für Ihre Datenspeicher benötigen.

## Nächste Schritte

Weitere Informationen zu anderen Limits für Experience Platform-Services, End-to-End-Latenzinformationen und Lizenzinformationen aus Real-Time CDP Product Description-Dokumenten finden Sie in der folgenden Dokumentation:

* [Limits in Real-Time CDP](/help/rtcdp/guardrails/overview.md)
* [End-to-End-Latenzdiagramme](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) für verschiedene Experience Platform-Dienste.
* [Real-time Customer Data Platform (B2C Edition - Prime und Ultimate Packages)](https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2P - Prime- und Ultimate-Pakete)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2B - Prime- und Ultimate-Pakete)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
