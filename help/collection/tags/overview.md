---
title: Satellitenobjektreferenz
description: Hier erfahren Sie mehr über das Client-seitige _satellite-Objekt und die verschiedenen Funktionen, die Sie damit in Tags ausführen können.
exl-id: f8b31c23-409b-471e-bbbc-b8f24d254761
source-git-commit: a36e5af39f904370c1e97a9ee1badad7a2eac32e
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 13%

---

# `_satellite` Objektverweis

Das `_satellite`-Objekt macht mehrere unterstützte Einstiegspunkte verfügbar, die Ihnen bei der Interaktion mit der auf Ihrer Site veröffentlichten Tag-Bibliothek helfen. Alle Tag-Bereitstellungen machen `_satellite` verfügbar, wenn das Lader-Tag korrekt implementiert ist. Es gibt mehrere primäre Anwendungsfälle für dieses Objekt:

* Verwendung in Ihrer Tag-Bibliothek in benutzerdefinierten Code-Blöcken, sodass Sie vollen Zugriff auf die Tag-Bibliothek selbst erhalten.
* Debuggen der bereitgestellten Implementierung in einer beliebigen Umgebung (Entwicklung, Staging oder Produktion)
* Direkte Implementierung auf Ihrer Website, sodass Sie den Trigger von Ereignissen oder Tag-Regeln vollständig steuern können. Für neue Implementierungen empfiehlt Adobe eine flexiblere Strategie, z. B. die [Adobe Client-Datenschicht](/help/tags/extensions/client/client-data-layer/overview.md).

>[!IMPORTANT]
>
>Wenn Sie `_satellite` über Ihren Site-Code aufrufen (z. B. `_satellite.track()`), **schützen Sie jeden Aufruf** sodass Ihre Site nicht eng mit der Tag-Bibliothek verknüpft ist.
>
>Die Verwendung von `_satellite` im benutzerdefinierten Code einer Tag-Eigenschaft oder lokal in Ihrer Browser-Konsole erfordert keinen Schutz.

## Häufige Anwendungsbeispiele

```js
// Read and write a temporary data element value
const region = _satellite.getVar('user_region');
_satellite.setVar('promo_code', code);

// Local debugging
_satellite.setDebug(true);
_satellite.logger.log('Rule evaluated');

// Manually trigger a rule configured in your tag property
if (window._satellite?.track) {
  _satellite.track('cart_add', { sku: '123', qty: 2 });
}
```
