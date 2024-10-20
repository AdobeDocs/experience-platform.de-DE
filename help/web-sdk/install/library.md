---
title: Installieren des Web SDK mithilfe der JavaScript-Bibliothek
description: Referenzieren Sie die Web SDK-Bibliothek mithilfe einer eigenständigen CDN-Datei.
exl-id: bacfe938-4326-48f6-a321-bd16970e77eb
source-git-commit: 9876390f7ba34c312f2ce4c00fe39e3ea1ef1ace
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Installieren des Web SDK mithilfe der JavaScript-Bibliothek

Eine Alternative zur Installation des Web SDK ohne [Verwendung der Tag-Erweiterung](extension.md) besteht darin, auf die auf einem CDN gehostete JavaScript-Bibliothek zu verweisen. Sie können die Bibliothek direkt referenzieren oder herunterladen und in Ihrer eigenen Infrastruktur hosten. Es ist in minimierten und vollständigen Formaten verfügbar.

Die Web SDK-Bibliothek ist mit der folgenden URL-Struktur verfügbar:

* **minified**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.min.js`
* **full**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.js`

In den [Versionshinweisen](../release-notes.md) finden Sie die neueste Version, die in die URL aufgenommen werden soll. Beispielsweise lautet die URL für die Vollversion von Version 2.19.1 `https://cdn1.adoberesources.net/alloy/2.19.1/alloy.js`.

## Code hinzufügen

Fügen Sie den folgenden Codeblock so weit wie möglich im Tag `<head>` Ihrer HTML hinzu:

```html
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.19.1/alloy.min.js" async></script>
```

Dieser Code erstellt asynchron ein `alloy` -Objekt, mit dem Sie einen beliebigen Web SDK-Befehl aufrufen können. Wenn Sie das Web SDK synchron laden möchten, können Sie das Attribut `async` in der letzten Zeile des Codeblocks entfernen. Wenn Sie das Attribut `async` entfernen, wird verhindert, dass der Rest des HTML-Dokuments vom Browser analysiert und gerendert wird, bis die Bibliothek geladen und ausgeführt wird. Diese zusätzliche Verzögerung vor der Anzeige von Primärinhalten für Benutzer wird in der Regel nicht empfohlen, kann jedoch je nach den Anforderungen Ihres Unternehmens sinnvoll sein.
