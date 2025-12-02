---
title: _monitore
description: Hinzufügen von Ereignis-Listenern, um Ihre Tag-Implementierung zu debuggen.
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 1%

---

# `_monitors`

Mit dem `_satellite._monitors` können Sie Ereignis-Listener erstellen und benutzerdefinierten Code ausführen, wenn die Bibliothek eine ausgelöste Regel erkennt. Der Hauptzweck besteht darin, Sie beim Debuggen Ihrer Implementierung zu unterstützen, um sicherzustellen, dass die Regeln korrekt Trigger werden.

>[!IMPORTANT]
>
>Dieses Objekt dient nur Debugging-Zwecken. Binden Sie keine Produktionslogik an dieses Objekt. Die Verfügbarkeit von Eigenschaften oder Namen innerhalb dieses Objekts kann von Adobe jederzeit geändert werden.

```ts
_satellite._monitors?: {
  ruleTriggered(event: { rule: Rule }): void;
  ruleCompleted(event: { rule: Rule }): void;
  ruleConditionFailed(event: { rule: Rule; condition: Condition }): void;
}[];
```

Sie können die folgenden Ereignistypen überwachen:

## `ruleTriggered`

Diese Rückruffunktion wird ausgelöst, wenn ein Ereignis eine Regel vor der Verarbeitung der Bedingungen und Aktionen der Regel durch einen Trigger auslöst. Wenn diese Funktion Trigger aufweist, `ruleCompleted` oder `ruleConditionFailed` Trigger kurz danach (schließen sich gegenseitig aus).

## `ruleCompleted`

Die `ruleCompleted` Callback-Funktion wird nach dem `ruleTriggered` ausgelöst, wenn die Bedingungskriterien der Regel erfolgreich sind und alle Aktionen der Regel ausgeführt werden.

## `ruleConditionFailed`

Die Rückruffunktion &quot;`ruleConditionFailed`&quot; wird nach der `ruleTriggered` ausgelöst, wenn mindestens eine der Regelbedingungen fehlschlägt.

## `Rule`

Jede Rückruffunktion macht ein `Rule` verfügbar, das Informationen über die Regel selbst bereitstellt.

```ts
type Rule = {
  id: string;
  name: string;
  events: Event[]; // Rule-specific events
  conditions: Condition[]; // Rule-specific conditions
  actions: Action[]; // Rule-specific actions
}
```

| Name | Typ | Beschreibung |
|---|---|---|
| **`id`** | `string` | Die eindeutige Kennung der Regel. |
| **`name`** | `string` | Der Anzeigename der Regel. |
| **`events`** | `Event[]` | Ein Array von Ereignissen, die Sie zum Trigger der Regel konfiguriert haben. |
| **`conditions`** | `Condition[]` | Ein Array von Bedingungen, die zum Trigger der Regel konfiguriert wurden. |
| **`actions`** | `Action[]` | Ein Array von Aktionen, deren Ausführung konfiguriert wurde, wenn die Regel ausgelöst wird. |

## Beispiel

Fügen Sie dem HTML im `<head>`-Tag das folgende Codefragment hinzu, bevor Sie den Tag-Bibliothekslader aufrufen:

```html
<script>
  window._satellite ??= {};
  window._satellite._monitors ??= [];
  window._satellite._monitors.push({
    ruleTriggered(event) { console.log('Rule triggered', event.rule);},
    ruleCompleted(event) { console.log('Rule completed', event.rule);},
    ruleConditionFailed(event) { console.log('Rule condition failed', event.rule, event.condition);}
  });
</script>
<script src="https://assets.adobedtm.com/.../launch-EN...js" async></script>
```

Da die Tag-Bibliothek an dieser Stelle noch nicht auf der Seite geladen ist, wird das anfängliche `_satellite`-Objekt erstellt und ein Array auf der `_satellite._monitors` initialisiert. Das Skript fügt diesem Array dann ein Monitorobjekt hinzu.

Beachten Sie bei der Verwendung von Monitoren die folgenden Tipps:

* Beachten Sie, dass diese Debugmeldungen `console.log` anstelle von [`_satellite.logger`](logger.md) verwenden, da die Hooks erstellt werden, bevor die Tag-Bibliothek geladen wird.
* Obwohl das Codebeispiel alle drei Callback-Funktionen umfasst, sind sie keine erforderlichen Felder. Sie können beim Debuggen von Regeln auf Ihrer Site nur die gewünschten Erweiterungspunkte einbeziehen.
* Es sind mehrere Monitore zulässig, auch für dieselben Ereignisse. Wenn Sie mehrere Monitore für ein einzelnes Ereignis verwenden, ist die Anrufreihenfolge nicht garantiert.
* Stellen Sie sicher, dass Sie `_monitors` erstellen _bevor_ die Tag-Bibliothek laden. Wenn Sie diese Erweiterungspunkte erstellen, nachdem die Bibliothek geladen wurde, werden nur die ab diesem Zeitpunkt Trigger Regeln erfasst.
