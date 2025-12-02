---
title: setDebug()
description: Aktivieren Sie das Debugging auf Ihrer Site über die Browser-Konsole.
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# `setDebug()`

Mit der `_satellite.setDebug()` Methode können Sie das [&#x200B; (Debugging](../use-cases/debugging.md) auf Ihrer Site aktivieren oder deaktivieren. Diese Methode soll lokal in Ihrer Browser-Konsole ausgeführt werden. Adobe rät davon ab, diese Methode innerhalb von Tag-Regeln aufzurufen.

```ts
_satellite.setDebug(enabled: boolean): void
```

* **`_satellite.setDebug(true);`**: Aktiviert [Debugging](../use-cases/debugging.md). Von der Tag-Bibliothek (einschließlich [`_satellite.logger`](logger.md)) generierte Nachrichten werden in Ihrer Browser-Konsole angezeigt.
* **`_satellite.setDebug(false);`**: Deaktiviert das Debugging. Von der Tag-Bibliothek generierte Konsolenmeldungen sind nicht sichtbar.

```js
// This console message does not appear because debug mode is not yet enabled
_satellite.logger.log('Example message');

// Enable debug mode
_satellite.setDebug(true);

// This console message appears in the console
_satellite.logger.info('Debug messages are now visible');

// Disable debug mode
_satellite.setDebug(false);

// This console message does not appear because debug mode is no longer enabled
_satellite.logger.warn('Incorrect rule trigger detected');
```

>[!NOTE]
>
>Nachrichten, die mit den nativen `console.log()` von JavaScript geschrieben wurden, sind für alle sichtbar, wenn DevTools geöffnet ist. Adobe empfiehlt, nach Möglichkeit [`_satellite.logger`](logger.md) zu verwenden.

## Persistenz des Debug-Modus

Beim Aufrufen dieser Methode verwendet der Debugmodus den folgenden Umfang:

* **Browser-Sitzung**: Der Debugging-Modus wird über Seitenladevorgänge hinweg beibehalten. Sie bleibt aktiviert, bis Sie die Browser-Sitzung beenden oder explizit deaktivieren.
* **Ursprungsbereich**: Der Debugging-Modus bleibt nur für dieselbe Site bestehen (Domain + Port + Protokoll).
* **Pro Browser-**: Der Debugging-Modus ist nicht profilübergreifend.

Andere Formen von [Debugging](../use-cases/debugging.md) können den Debugging-Modus mithilfe der Browser-Konsolenmethode beeinflussen und überschreiben.
