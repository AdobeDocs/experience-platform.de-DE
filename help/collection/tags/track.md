---
title: track()
description: Trigger einer Direktaufruf-Regel.
source-git-commit: a36e5af39f904370c1e97a9ee1badad7a2eac32e
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 2%

---

# `track()`

Mit der `_satellite.track()` Methode können Sie einen Trigger für eine [Direktaufrufregel“ &#x200B;](/help/tags/extensions/client/core/overview.md#direct-call-event).

>[!IMPORTANT]
>
>Adobe betrachtet `_satellite.track()` als **veraltete Implementierungsmethode**. Obwohl es immer noch vollständig unterstützt wird, empfiehlt Adobe dringend, modernere Implementierungsverfahren zu verwenden, z. B. die [Adobe Client-Datenschicht](/help/tags/extensions/client/client-data-layer/overview.md), die der empfohlene Ansatz für neue Implementierungen ist.
>
>Wenn Sie `_satellite.track()` auf Ihrer Site verwenden möchten, **Sie jeden Aufruf**, damit Ihre Site nicht eng an die Tag-Bibliothek gekoppelt ist. Wenn die Tag-Eigenschaft nicht überwacht wird, führt das zukünftige Entfernen dazu, dass alle Verweise auf das `_satellite`-Objekt Fehler auslösen.

```ts
_satellite.track(identifier: string, detail?: unknown ): void;
```

Wenn Sie `_satellite.track()` mithilfe der in der Tags-Benutzeroberfläche konfigurierten Kennung aufrufen, wird diese Regel sofort ausgelöst. Der Aufruf dieser Methode dient nur als Regelereignis. Die Bedingungen der Regel gelten weiterhin, bevor die Regelaktionen ausgeführt werden. Mehrere Direktaufrufregeln können dieselbe Kennung verwenden, sodass Sie alle diese Regeln gleichzeitig mit einem einzigen `_satellite.track()`-Aufruf in Trigger bringen können. Jede ausgelöste Regel prüft vor der Ausführung einer Aktion weiterhin ihre eigenen Bedingungen, selbst wenn mehrere Regeln dieselbe Kennung aufweisen.

## Verfügbare Felder

Die `_satellite.track()`-Methode unterstützt zwei Argumente:

| Name | Typ | Erforderlich | Beschreibung |
|---|---|---|---|
| **`identifier`** | `string` | Ja | Die Kennung der Direktaufrufregel. Diese Kennung wird beim Konfigurieren der Regel in der Tags-Benutzeroberfläche festgelegt. |
| **`detail`** | `unknown` | Nein | Eine optionale Payload mit beliebigen Informationen. Beim Konfigurieren einer Regel können Sie mithilfe von `event.detail` (benutzerdefinierter Code) oder `%event.detail%` (Textfelder, die die Datenelementnotation unterstützen) auf die Payload zugreifen. |

```js
// Trigger rules with the identifier 'example'
if (window._satellite?.track) {
  _satellite.track('example');
}

// Trigger a direct call rule with an optional payload that your tag rule can use
_satellite.track('contact_submit', { name: 'John Doe' });
// When configuring the rule, access the payload field using:
// event.detail.name (custom code block) or
// %event.detail.name% (data element)
```
