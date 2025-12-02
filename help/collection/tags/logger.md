---
title: logger
description: Gibt beim Debuggen Informationen an die Browser-Konsole aus.
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 1%

---

# `logger`

Das `_satellite.logger`-Objekt enthält Methoden, mit denen Sie Diagnose- oder Informationsmeldungen an die Browser-Konsole ausgeben können, wenn [Debugging](../use-cases/debugging.md) aktiviert ist. Wenn das Debugging nicht aktiviert ist, bewirken alle `logger`-Methodenaufrufe nichts.

Mit diesen Methoden können Entwickler, technische Marketing-Experten und Tester leicht erkennen, welche Trigger wann in einer Tag-Eigenschaft vorhanden sind. Da diese Konsolenmeldungen nur angezeigt werden, wenn der Debugging-Modus aktiviert ist, können Sie `logger` Meldungen in -Bereitstellungen der Produktion überlassen, ohne die Browser-Konsole der Besucher Ihrer Site zu beeinträchtigen.

```ts
readonly _satellite.logger: {
  debug(...args: unknown[]): void;
  log(...args: unknown[]): void;
  info(...args: unknown[]): void;
  warn(...args: unknown[]): void;
  error(...args: unknown[]): void;
}
```

>[!TIP]
>
>Frühere Versionen des Tag-Objekts `_satellite.notify()` verwendet. Die `notify()` ist zugunsten von `_satellite.logger` veraltet.

## Methoden

Alle `_satellite.logger` werden bei aktiviertem Debugging an die entsprechende JavaScript-`console.*` weitergeleitet. Die meisten `console` Argumente oder Objekte werden mithilfe von `_satellite.logger` unterstützt:

| Methode | Weiterleiten an | Empfohlene Verwendungszwecke |
|---|---|---|
| `_satellite.logger.debug()` | `console.debug()` | Ausführliche Diagnose; bei einigen Browsern ist möglicherweise eine ausführliche Protokollierung erforderlich, um sie anzuzeigen. |
| `_satellite.logger.log()` | `console.log()` | Allgemeine Nachrichten. |
| `_satellite.logger.info()` | `console.info()` | Allgemeine Informationsveranstaltungen. |
| `_satellite.logger.warn()` | `console.warn()` | Wiederherstellbare Probleme. Der Konsoleneintrag ist gelb hervorgehoben. |
| `_satellite.logger.error()` | `console.error()` | Fehler. Der Konsoleneintrag ist rot hervorgehoben. Adobe empfiehlt die Verwendung von `error` für Stacks. |

```js
// First enable debugging mode
_satellite.setDebug(true);

// Logs a debug message
_satellite.logger.debug('Verbose diagnostic event');

// Logs a generic message
_satellite.logger.log('Example');

// Logs an informational message with mixed arguments
_satellite.logger.info('Rule triggered', 42, { ruleId: 'R123' }, ['a', 'b']);

// Logs a warning message
_satellite.logger.warn('Data element does not contain a value');

// Logs an error message with stack
_satellite.logger.error(new Error('Required extension not found'));
```

## Konsolenausgabe

In allen Meldungen der Konsolenausgabe stellt die Bibliothek Folgendes voran:

* **🚀**: Hilft Ihnen bei der einfachen Erkennung, welche Konsolenmeldungen von Ihrer Tag-Implementierung stammen.
* **\[Herkunft\]**: Der Name der Regel, Aktion, Erweiterung oder des Datenelements, von dem das Protokoll stammt. Wenn Sie eine Logger-Methode außerhalb Ihrer Implementierung aufrufen (z. B. über die Browser-Konsole), wird `[Custom Script]` verwendet.
* **Nachrichtenausgabe**: Die Nachrichtenausgabe, die beim Aufrufen der Methode enthalten ist.

>[!NOTE]
>
>Browser-Formatierungstoken wie `%c`, `%s` und `%d` werden nicht angewendet, da der Logger das `🚀 [Origin]` Präfix anwendet.
