---
title: Basiscode
description: Warteschlangenbefehle (Bootstrap), während die Datenerfassungsbibliothek asynchron geladen wird.
source-git-commit: 0a45b688243b17766143b950994f0837dc0d0b48
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# Basiscode

Der Basis-Code ermöglicht das Bootstrapping durch Einreihen von Befehlen in die Warteschlange, während Adobe Experience Platform Web SDK asynchron geladen wird. Nach Ausführung des Basis-Codes können Sie jeden Befehl wie [`configure`](../commands/configure/overview.md) oder [`sendEvent`](../commands/sendevent/overview.md) sofort aufrufen, ohne sich Gedanken über die Race-Bedingungen oder den Zeitpunkt des Ladevorgangs der Bibliothek machen zu müssen. Nach dem Laden von Web SDK werden Befehle aus der Warteschlange in der Reihenfolge „first-in“ und „first-out“ ausgeführt (in der Reihenfolge, in der sie sich in der Warteschlange befanden).

Befehle geben Promises zurück, auch wenn sie in die Warteschlange gestellt werden. Wenn ein Befehl in die Warteschlange gestellt wird, wird die Zusage nach Ausführung des Befehls aufgelöst oder zurückgewiesen, sobald das Laden der Web-SDK abgeschlossen ist. Wenn das Laden von Web SDK nie abgeschlossen wird (z. B. wenn die Bibliothek nicht geladen wird), bleiben Zusagen in der Warteschlange ausstehend.

## Hinzufügen des Basis-Codes

Platzieren Sie den Basis-Code so hoch wie möglich im `<head>`-Tag vor Skripten, die die Web-SDK aufrufen könnten.

```html
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
  (window,["alloy"]);
</script>
```

Laden Sie nach dem Hinzufügen des Basis-Codes die Web-SDK mit der von Ihnen ausgewählten Methode ([JavaScript](library.md)Bibliothekslader oder [Tags-Einbettungs-Code](/help/tags/extensions/client/web-sdk/getting-started.md)). Bei Tag-basierten Implementierungen wird der Basis-Code in der Web-SDK-Tag-Erweiterung 2.34.0 und höher unterstützt.

Dieser Basis **Code ist in** folgenden Szenarien nicht erforderlich:

* Bei synchronem Laden der JavaScript-Bibliothek Synchrone Ladeblöcke werden analysiert, während die Bibliothek abgerufen und ausgeführt wird.
* Bei Verwendung der Tag-Erweiterung erfolgen alle Aufrufe an die Web-SDK innerhalb von Tag-Regeln oder -Aktionen. Sie müssen nur dann den Basis-Code einbeziehen, wenn Ihre Implementierung außerhalb Ihrer Tags-Bibliothek auf die Web-SDK verweist. Die meisten Tag-Implementierungen rufen Web SDK normalerweise nicht außerhalb der Tag-Bibliothek auf, sodass die meisten Tag-Implementierungen keinen Basis-Code erfordern.

## Beispiele

In den Kommentaren in diesem Code-Beispiel wird der Zeitpunkt erläutert, zu dem Befehle in die Warteschlange gestellt und aufgelöst werden. Dieses Beispiel gilt sowohl für die JavaScript-Bibliothek als auch für die Tag-Erweiterung:

```html
<head>
  <script>
    // Calls made before the base code runs are not captured (alloy is not yet defined).
    // Always make sure that the base code runs before any attempt to call commands.
    // alloy("getLibraryInfo").then(console.log).catch(console.error);
  </script>

  <!-- Base code -->
  <script>
    !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
    []).push(o),n[o]=function(){var u=arguments;return new Promise(
    function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
    (window,["alloy"]);
  </script>

  <!-- Queued command -->
  <script>
    alloy("getLibraryInfo").then(result => {
      console.log("Queued call resolved:", result);
    }).catch(console.error);
  </script>

  <!-- Load the Web SDK using the JavaScript loader -->
  <script src="https://cdn1.adoberesources.net/alloy/<VERSION>/alloy.min.js" async></script>
  <!-- or the tag extension -->
  <!-- <script src=".../launch-<ENV>.min.js" async></script> -->

  <!-- Another call (queued if the library is still loading; immediate if it is ready) -->
  <script>
    alloy("getLibraryInfo").then(result => {
      console.log("Immediate call resolved:", result);
    }).catch(console.error);
  </script>
</head>
```

## SDK-Instanz umbenennen

Sie können die globale Funktion, die Sie aufrufen, umbenennen, indem Sie die letzte Zeile des Basis-Codes ändern. Änderung:

```js
(window,["alloy"]);
```

An:

```js
(window,["ingot"]);
```

Durch diese Änderung können Sie Befehle mit `ingot` anstelle von `alloy` aufrufen:

```js
ingot("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

## Mehrere SDK-Instanzen

Optional können Sie den Basis-Code verwenden, um mehr als eine SDK-Instanz auf einer Seite zu konfigurieren. Weitere [ finden Sie unter „Verwenden mehrerer Web](../../use-cases/multiple-instances.md)SDK-Instanzen“.
