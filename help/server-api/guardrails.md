---
title: Leitlinien für die Performance der Edge Network Server-API
description: Erfahren Sie, wie Sie die Server-API in Leitplanken für optimale Leistung verwenden.
exl-id: 063d0fbb-26d1-4727-9dea-8e7223b2173d
source-git-commit: 6414168c1deb047af30d8636ef8d61316f56aecf
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 5%

---


# Leitlinien für die Performance der Edge Network Server-API

## Übersicht {#overview}

Die Leistung betreffende Leitplanken definieren Nutzungsbeschränkungen für Ihre Server-API-Anwendungsfälle. Das Überschreiten der in diesem Artikel beschriebenen Leistungsschutzmechanismen kann zu Leistungseinbußen führen.

Adobe ist nicht für Leistungseinbußen verantwortlich, die durch Überschreitung von Nutzungsbeschränkungen verursacht werden. Kunden, die die Leistungsleitplanken konsequent überschreiten, können zusätzliche Verarbeitungskapazität anfordern, um eine Leistungsbeeinträchtigung zu vermeiden.

>[!IMPORTANT]
>
>Überprüfen Sie zusätzlich zu dieser Seite mit Leitplanken Ihre Lizenzberechtigungen in Ihrem Kundenauftrag und [ entsprechenden ](https://helpx.adobe.com/de/legal/product-descriptions.html)Produktbeschreibung) die tatsächlichen Nutzungsbeschränkungen.

Alle auf dieser Seite beschriebenen Leistungs-Schutzmechanismen gelten auf der Ebene der IMS-Organisation. Für Benutzende mit mehreren konfigurierten IMS-Organisationen unterliegt jede Organisation einzeln den unten stehenden Leistungsschutzmechanismen. Weitere Informationen zu ](../landing/glossary.md) finden Sie im [Experience Platform-Glossar[!DNL IMS Organizations].

## Definitionen

* **Verfügbarkeit** wird für jedes Fünf-Minuten-Intervall als Prozentsatz der vom Experience Platform-Edge Network verarbeiteten Anfragen berechnet, die nicht fehlerhaft sind und sich nur auf die bereitgestellten Edge Network-APIs beziehen. Wenn ein Mandant in einem bestimmten Fünf-Minuten-Intervall keine Anfragen gestellt hat, gilt dieses Intervall als 100 % verfügbar.
* **Monthly Uptime Percentage** für eine bestimmte Region wird als Durchschnitt der Verfügbarkeit für alle 5-Minuten-Intervalle in einem Monat berechnet.
* Ein **Upstream** ist ein Service hinter dem Edge Network, der für einen bestimmten Datenstrom aktiviert ist, z. B. Adobe-Server-seitige Weiterleitung, Adobe Edge-Segmentierung oder Adobe Target.
* Eine **Anfrageeinheit** entspricht einem 8 KB großen Fragment einer Anfrage und einem für einen Datenstrom vorkonfigurierten Fragment.
* Eine **Anfrage** ist eine einzelne Nachricht, die von einem kundeneigenen Programm an die [!DNL Server API] gesendet wird. Eine Anfrage kann eine oder mehrere Anfrageeinheiten enthalten.
* Ein **Fehler** ist jede Anfrage, die aufgrund eines Edge Networks [Interner Service-Fehler](error-handling.md) fehlschlägt.

## Service-Beschränkungen

Alle Datenströme erzwingen bestimmte Nutzungsbeschränkungen, die hauptsächlich steuern, wie viele Ereignisse gleichzeitig gesendet werden können, ihre Größe und die Anzahl der Upstream-Services, an die diese Anfragen weitergeleitet werden.

### Einheiten anfordern

Alle Limits werden über eine **Anfrageeinheit (RU)) angewendet und normalisiert** die als **8 KB-Fragment** einer Anfrage definiert ist, die an einen Upstream-Service gesendet wird, der in einem Datenstrom konfiguriert ist.

#### Beispiele

| Für jeden Datenstrom konfigurierte Upstreams | Durchschnittliche Anfragengröße | Einheiten anfordern |
| --- | --- | --- |
| 1 (Adobe-Plattform) | 8 KB (1 Fragment) | 1 |
| 2 (Adobe-Plattform, Adobe Target) | 8 KB (1 Fragment) | 2 |
| 2 (Adobe-Plattform, Adobe Target) | 16 KB (2 Fragmente) | 4 |
| 2 (Adobe-Plattform, Adobe Target) | 64 KB (8 Fragmente) | 16 |

### Limits für Anforderungseinheiten

Die nachstehende Tabelle zeigt die standardmäßigen Grenzwerte. Wenn Sie höhere Limits für Anfrageeinheiten benötigen, wenden Sie sich an Ihren Kundenbetreuer.

| Endpunkt | Anforderungseinheiten pro Sekunde |
| --- | --- |
| `/v2/interact` | 4.000 |
| `/v2/collect` | 6000 |

### Größenbeschränkung für HTTP-Anfragen

| Payload-Format | Maximale Größe einer Anfrage | Max. 8 KB Anfragefragmente |
| --- | --- | --- |
| JSON-Nur-Text | 64 KB | 8 |


>[!NOTE]
>
>Je nach Payload sind Binärformate im Allgemeinen 20-40 % kompakter, sodass Sie mehr Daten pushen können als in Nur-Text-JSON. Wenden Sie sich an Ihren Kundenbetreuer, wenn Sie eine höhere Kapazität für Ihre Datenströme benötigen.

## Nächste Schritte

In der folgenden Dokumentation finden Sie weitere Informationen zu anderen Experience Platform-Services-Leitplanken, zu End-to-End-Latenzinformationen und Lizenzinformationen aus den Produktbeschreibungsdokumenten von Real-Time CDP:

* [Real-Time CDP-Leitplanken](/help/rtcdp/guardrails/overview.md)
* [End-to-End-Latenzdiagramme](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) für verschiedene Experience Platform-Services.
* [Real-time Customer Data Platform (B2C Edition - Prime- und Ultimate-Pakete)](https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2P - Prime- und Ultimate-Pakete)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2B - Prime- und Ultimate-Pakete)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
