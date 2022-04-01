---
title: Vereinbarungen und Ziele auf Dienstebene
description: Erfahren Sie, wie Sie die Authentifizierung für die Edge Network Server-API konfigurieren
seo-description: Learn how to configure authentication for the Edge Network Server API
keywords: Datenerfassung;Datenerfassung;Edge-Netzwerk;API;SAL;SLIT;Service-Level
hide: true
hidefromtoc: true
source-git-commit: 50a688e2f19f4fda2fc4cca823edb5886ad32bba
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 2%

---


# Schutzschilde

## Übersicht {#overview}

Die Adobe wird kommerziell verantwortungsvolle Anstrengungen unternehmen, um die [!DNL Server API] innerhalb eines monatlichen Betriebszeitanteils von mindestens 99,9 % für jede Region während eines monatlichen Abrechnungszyklus verfügbar sind.

## Definitionen

* **Verfügbarkeit** wird für jedes fünfminütige Intervall als Prozentsatz der vom Experience Adobe Experience Platform Edge Network verarbeiteten Anforderungen berechnet, die nicht fehlschlagen und sich ausschließlich auf die bereitgestellten Adobe Experience Platform Edge Network-APIs beziehen. Wenn ein Mandant in einem bestimmten Fünfminüterintervall keine Anforderungen gestellt hat, gilt dieses Intervall als zu 100 % verfügbar.
* **Monatlicher Uptime-Prozentsatz** für eine bestimmte Region wird als Durchschnitt der Verfügbarkeit für alle 5-minütigen Intervalle in einem Monat berechnet.
* Ein **Upstream** ist ein Dienst hinter dem Adobe Edge-Netzwerk, der für einen bestimmten Datastream aktiviert ist, z. B. Adobe Server Side Forwarding, Adobe Edge Segmentation oder Adobe Target.
* A **Anfrage** an die Server-API gesendet wird, ist als eine oder mehrere Anfrageeinheiten definiert.
* A **Anfrageeinheit** entspricht einem 8-KB-Fragment einer Anforderung und einem vorgelagerten für einen Datastream konfigurierten.
* Ein **error** ist eine Anforderung, die aufgrund eines Adobe Experience Platform Edge Network fehlschlägt [Interner Dienstfehler](error-handling.md).

## Interne Ziele

Adobe-Engineering-Teams setzen nahezu zeitnahe Telemetrie-, Monitoring- und Skalierungsverfahren ein, um die folgenden Ziele sicherzustellen:

* Weniger als 1 % der HTTP-Anforderungen gibt zurück `5xx` Fehler in den letzten fünf Minuten
* Weniger als 1 % der Upstream-Verbindungen geben in den letzten fünf Minuten einen Fehler zurück
* Jede Mandantenkapazität wird in weniger als 10 Minuten ab dem Zeitpunkt verdoppelt, an dem eine Beschränkung erreicht wird.

## Vertragsausschlüsse auf Dienstebene

Die oben beschriebene Service-Level-Verpflichtung gilt nicht für Fehler bei der Verfügbarkeit oder Leistung, die durch die folgenden Ereignisse verursacht werden:

* Faktoren außerhalb unserer angemessenen Kontrolle, einschließlich Internetzugang oder damit zusammenhängende Probleme außerhalb der Adobe-Infrastruktur.
* Jeder Missbrauch der [!DNL Server API], wie in den unten aufgeführten Beschränkungen definiert.

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
| `/v2/interact` | 4000 |
| `/v2/collect` | 6.000 |


### HTTP-Anfragegrößenbeschränkung

| Payload-Format | Maximale Größe für eine Anforderung | Max. 8 KB Anforderungsfragmente |
| --- | --- | --- |
| JSON-Klartext | 64 KB | 8 |


>[!NOTE]
>
>Abhängig von der Payload selbst sind die binären Formate im Allgemeinen 20-40 % kompakter, sodass Sie mehr Daten als im Nur-Text-JSON-Format übertragen können. Wenden Sie sich an Ihren Kundenbetreuer, wenn Sie eine höhere Kapazität für Ihre Datenspeicher benötigen.

