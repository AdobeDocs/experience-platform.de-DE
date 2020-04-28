---
title: Adobe Experience Platform Web SDK – Hilfe
seo-title: Adobe Experience Platform Web SDK – Hilfe
description: Erfahren Sie, was das Adobe Experience Platform Web SDK ist und wie es verwendet werden kann.
seo-description: Kunden von Adobe Experience Cloud die Interaktion mit den verschiedenen Diensten in der Experience Cloud ermöglichen.
translation-type: tm+mt
source-git-commit: 5027ae2cd083631d7122346796ef93572c129d3f

---


# (Beta) Was ist das Adobe Experience Platform Web SDK

>[!IMPORTANT]
>
>Das Adobe Experience Platform Web SDK befindet sich derzeit in der Betaphase und steht nicht allen Nutzern zur Verfügung. Dokumentation und Funktionalität können sich ändern.

Adobe Experience Platform Web SDK ist eine clientseitige JavaScript-Bibliothek, mit der Kunden der Adobe Experience Cloud über das Adobe Experience Platform Edge Network mit den verschiedenen Diensten in der Experience Cloud interagieren können.

## Durch das Adobe Experience Platform Web SDK ersetzte SDKs

Das Adobe Experience Platform Web SDK ersetzt die folgenden SDKs:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Dies ist nicht nur ein Wrapper um vorhandene Bibliotheken. Es ist eine vollständige Umschreibung. Ihr Zweck ist es, Probleme wie das Auslösen von Tag in der richtigen Reihenfolge und inkonsistente Bibliotheksversionen zu lösen und eine verbesserte Abhängigkeitsverwaltung zu bieten. Es handelt sich um eine neue Methode zur Implementierung von Experience Cloud.

Neben einer neuen Bibliothek gibt es einen neuen Endpunkt, der die HTTP-Abfragen an Adobe-Lösungen optimiert. Zuvor sendete Visitor.js einen Sperraufruf an den Besucher-ID-Dienst und dann einen Aufruf an Adobe Target, dann sandte DIL.js einen Aufruf an Adobe Audience Manager und schließlich schickte AppMeasurement.js einen Aufruf an Adobe Analytics. Diese neue Bibliothek und dieser Endpunkt können eine ID abrufen, ein Erlebnis für die Zielgruppe abrufen, Daten an Audience Manager senden und die Daten in einem einzigen Aufruf an die Adobe Experience Platform übergeben.