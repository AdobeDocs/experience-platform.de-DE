---
title: Installieren des Web SDK mithilfe der JavaScript-Bibliothek
description: Referenzieren Sie die Web SDK-Bibliothek mithilfe einer eigenständigen CDN-Datei.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# Installieren des Web SDK mithilfe der JavaScript-Bibliothek

Eine Option zur Installation des Web SDK besteht darin, auf die auf einem CDN gehostete JavaScript-Bibliothek zu verweisen. Sie können die Bibliothek direkt referenzieren oder herunterladen und in Ihrer eigenen Infrastruktur hosten. Es ist in minimierten und vollständigen Formaten verfügbar.

Die Web SDK-Bibliothek ist mit der folgenden URL-Struktur verfügbar:

* **Minimiert**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.min.js`
* **Voll**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.js`

Siehe [Versionshinweise](../release-notes.md) für die neueste Version, die in die URL aufgenommen werden soll. Beispielsweise lautet die URL für die Vollversion von Version 2.19.1 `https://cdn1.adoberesources.net/alloy/2.19.1/alloy.js`.

## Code hinzufügen

Fügen Sie den folgenden Codeblock so weit wie möglich in die `<head>` -Tag Ihrer HTML:

```html
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.19.1/alloy.min.js" async></script>
```

Dieser Code erstellt asynchron eine `alloy` -Objekt, mit dem Sie einen beliebigen Web SDK-Befehl aufrufen können. Wenn Sie das Web SDK synchron laden möchten, können Sie die `async` -Attribut in der letzten Zeile des Codeblocks. Entfernen der `async` -Attribut verhindert, dass der Rest des HTML-Dokuments vom Browser analysiert und gerendert wird, bis die Bibliothek geladen und ausgeführt wird. Diese zusätzliche Verzögerung vor der Anzeige von Primärinhalten für Benutzer wird in der Regel nicht empfohlen, kann jedoch je nach den Anforderungen Ihres Unternehmens sinnvoll sein.
