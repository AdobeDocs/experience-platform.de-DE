---
title: Adobe Experience Platform Web SDK – Hilfe
seo-title: Adobe Experience Platform Web SDK – Hilfe
description: Erfahren Sie, was das Adobe Experience Platform Web SDK ist und wie es verwendet werden kann.
seo-description: Kunden von Adobe Experience Cloud die Interaktion mit den verschiedenen Diensten in der Experience Cloud ermöglichen.
translation-type: tm+mt
source-git-commit: f06c90d6248071894bd9929fbe1150e30c8e7385
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 41%

---


# Was ist das Adobe Experience Platform Web SDK

Adobe Experience Platform Web SDK ist eine clientseitige JavaScript-Bibliothek, mit der Kunden der Adobe Experience Cloud über das Adobe Experience Platform Edge Network mit den verschiedenen Diensten in der Experience Cloud interagieren können.

## Durch das Adobe Experience Platform Web SDK ersetzte SDKs

Das Adobe Experience Platform Web SDK ersetzt die folgenden SDKs:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Dies ist nicht nur ein Wrapper um vorhandene Bibliotheken. Es ist eine vollständige Umschreibung. Ihr Zweck ist es, Probleme wie das Auslösen von Tag in der richtigen Reihenfolge und inkonsistente Bibliotheksversionen zu lösen und eine verbesserte Abhängigkeitsverwaltung zu bieten. Es ist eine neue Methode zur Implementierung der Experience Cloud und es ist [Open Source](https://github.com/adobe/alloy)

Neben einer neuen Bibliothek gibt es einen neuen Endpunkt, der die HTTP-Abfragen an Adobe-Lösungen optimiert. Zuvor sendete Visitor.js einen Sperraufruf an den Besucher-ID-Dienst und dann einen Aufruf an Adobe Target, dann sandte DIL.js einen Aufruf an Adobe Audience Manager und schließlich schickte AppMeasurement.js einen Aufruf an Adobe Analytics. Diese neue Bibliothek und dieser Endpunkt können eine ID abrufen, ein Erlebnis für die Zielgruppe abrufen, Daten an Audience Manager senden und die Daten in einem einzigen Aufruf an die Adobe Experience Platform übergeben.

## Erste Schritte

Wir empfehlen Ihnen dringend, [sich unsere Anleitung](getting-started/quick-start-with-launch.md) zu den ersten Schritten für eine kurze Übung zu entnehmen.

Dieses Produkt entwickelt sich ständig und wächst, um immer mehr Anwendungsfälle zu unterstützen. Um auf dem neuesten Stand zu bleiben, besuchen wir unser [unterstütztes Einsatzfallbrett](https://github.com/adobe/alloy/projects/5). Wir halten dies auf dem neuesten Stand mit den derzeit unterstützten Anwendungsfällen und den Fällen, an denen wir arbeiten, um Ihnen die bestmöglichen Entscheidungen zu ermöglichen.

* __Anwendungsfälle, die noch nicht unterstützt__ werden - sind Anwendungsfälle, die auf unserem Fahrplan für die Zukunft liegen.
* __Anwendungsfälle noch nicht abgeschlossen__ - Dies sind die Anwendungsfälle, mit denen das Team derzeit arbeitet.
* __Unterstützte Anwendungsfälle__ - Dies sind die Anwendungsfälle, die unterstützt werden und heute funktionieren.
* __Nutzungsszenarien, die wir nicht unterstützen__ - dies sind die Anwendungsfälle, die wir beschlossen haben, nicht zu unterstützen.
