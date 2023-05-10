---
title: Leistungsgarantien für die Edge Network Server-API
description: Erfahren Sie, wie Sie die Server-API in optimalen Leistungsgarantien verwenden.
keywords: Datenerfassung;Datenerfassung;Edge-Netzwerk;API;SAL;SLIT;Service-Level
exl-id: 063d0fbb-26d1-4727-9dea-8e7223b2173d
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 2%

---

# Leistungsgarantien für die Edge Network Server-API

## Übersicht {#overview}

Leistungsgarantien definieren Nutzungsbeschränkungen im Zusammenhang mit Anwendungsfällen Ihrer Server-API. Eine Überschreitung der in diesem Artikel beschriebenen Leistungsgarantien könnte zu einer Leistungsbeeinträchtigung führen.

Adobe ist nicht für Leistungsbeeinträchtigungen verantwortlich, die durch überschrittene Nutzungsbeschränkungen verursacht werden. Kunden, die die Leistungsgarantien konsequent überschreiten, können zusätzliche Verarbeitungskapazität anfordern, um eine Leistungsbeeinträchtigung zu vermeiden.

## Definitionen

* **Verfügbarkeit** wird für jedes fünfminütige Intervall als Prozentsatz der vom Experience Platform Edge Network verarbeiteten Anforderungen berechnet, die nicht fehlschlagen und sich ausschließlich auf die bereitgestellten Edge Network-APIs beziehen. Wenn ein Mandant in einem bestimmten Fünfminüterintervall keine Anforderungen gestellt hat, gilt dieses Intervall als zu 100 % verfügbar.
* **Monatlicher Uptime-Prozentsatz** für eine bestimmte Region wird als Durchschnitt der Verfügbarkeit für alle 5-minütigen Intervalle in einem Monat berechnet.
* Ein **Upstream** ist ein Dienst hinter dem Edge Network, der für einen bestimmten Datastream aktiviert ist, z. B. für die serverseitige Weiterleitung von Adoben, die Adobe Edge-Segmentierung oder Adobe Target.
* A **Anfrageeinheit** entspricht einem 8-KB-Fragment einer Anforderung und einem vorgelagerten für einen Datastream konfigurierten.
* A **Anfrage** ist eine einzige Nachricht, die von einer kundeneigenen Anwendung an die [!DNL Server API]. Eine Anforderung kann eine oder mehrere Anfrageeinheiten enthalten.
* Ein **error** ist eine Anforderung, die aufgrund eines Edge-Netzwerks fehlschlägt [Interner Dienstfehler](error-handling.md).

## Dienstbeschränkungen

Alle Datastreams erzwingen bestimmte Nutzungsbeschränkungen, die hauptsächlich steuern, wie viele Ereignisse gleichzeitig gesendet werden können, wie ihre Größe und die Anzahl der Upstream-Dienste, an die diese Anfragen weitergeleitet werden.

### Anfrageeinheiten

Alle Beschränkungen werden angewendet und normalisiert über eine **Anfrageeinheit (EVU)**, definiert als **8 KB-Fragment** einer Anfrage an einen in einem Datastream konfigurierten Upstream-Dienst.

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
| `/v2/collect` | 6.000 |


### HTTP-Anfragegrößenbeschränkung

| Payload-Format | Maximale Größe für eine Anforderung | Max. 8 KB Anforderungsfragmente |
| --- | --- | --- |
| JSON-Klartext | 64 KB | 8 |


>[!NOTE]
>
>Abhängig von der Payload selbst sind die binären Formate im Allgemeinen 20-40 % kompakter, sodass Sie mehr Daten als im Nur-Text-JSON-Format übertragen können. Wenden Sie sich an Ihren Kundenbetreuer, wenn Sie eine höhere Kapazität für Ihre Datenspeicher benötigen.
