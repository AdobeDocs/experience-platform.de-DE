---
title: Adobe Experience Platform Web SDK-Hilfe
seo-title: Adobe Experience Platform Web SDK-Hilfe
description: Erfahren Sie, was Adobe Experience Platform Web SDK ist und wie es verwendet werden kann.
seo-description: Kunden der Adobe Experience Cloud die Interaktion mit den verschiedenen Diensten in der Experience Cloud ermöglichen
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (Beta) Was ist Adobe Experience Platform Web SDK

>[!IMPORTANT]
>
>Das Adobe Experience Platform Web SDK befindet sich derzeit in der Betaphase und steht nicht allen Benutzern zur Verfügung. Dokumentation und Funktionalität können sich ändern.

Adobe Experience Platform Web SDK ist eine clientseitige JavaScript-Bibliothek, mit der Kunden der Adobe Experience Cloud mit den verschiedenen Diensten in der Experience Cloud interagieren können.

## SDKs ersetzt durch Adobe Experience Platform Web SDK

Adobe Experience Platform Web SDK ersetzt die folgenden SDKs:

* Besucher.js
* AppMeasurement.js
* AT.js
* DIL.js

Dies ist nicht nur ein Wrapper um vorhandene Bibliotheken herum. Es ist eine vollständige Umschreibung. Ihr Zweck ist es, Herausforderungen zu beenden, indem Tags in der richtigen Reihenfolge ausgelöst werden, die nicht mit den Versionshinweisen der Bibliothek übereinstimmen und die Abhängigkeitsverwaltung verbessert wird. Es handelt sich um eine neue Methode zur Implementierung der Experience Cloud.

Neben einer neuen Bibliothek gibt es einen neuen Endpunkt, der die HTTP-Anforderungen an Adobe-Lösungen optimiert. Zuvor sendete Besucher.js einen Sperraufruf an den Besucher-ID-Dienst und dann einen Aufruf an Adobe Zielgruppe, dann sandte DIL.js einen Aufruf an Adobe Audience Manager und schließlich schickte AppMeasurement.js einen Aufruf an Adobe Analytics. Diese neue Bibliothek und dieser Endpunkt können eine ID abrufen, ein Erlebnis für die Zielgruppe abrufen, Daten an Audience Manager senden und die Daten in einem einzigen Aufruf an die Adobe Experience Platform übergeben.