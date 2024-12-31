---
title: Installieren von Web SDK mithilfe der JavaScript-Bibliothek
description: Referenzieren Sie die Web-SDK-Bibliothek mithilfe einer eigenständigen CDN-Datei.
exl-id: bacfe938-4326-48f6-a321-bd16970e77eb
source-git-commit: 9876390f7ba34c312f2ce4c00fe39e3ea1ef1ace
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Installieren von Web SDK mithilfe der JavaScript-Bibliothek

Eine Alternative zur Installation von Web SDK ohne [Verwendung der Tag-Erweiterung](extension.md) besteht darin, auf die JavaScript-Bibliothek zu verweisen, die auf einem CDN gehostet wird. Sie können direkt auf die Bibliothek verweisen oder sie herunterladen und in Ihrer eigenen Infrastruktur hosten. Es ist in minimierten und vollständigen Formaten verfügbar.

Die Web-SDK-Bibliothek ist über die folgende URL-Struktur verfügbar:

* **minifiziert**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.min.js`
* **Voll**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.js`

In den [Versionshinweisen](../release-notes.md) finden Sie die neueste Version, die in die URL aufgenommen werden soll. Beispielsweise ist die URL für die Vollversion der Version 2.19.1 `https://cdn1.adoberesources.net/alloy/2.19.1/alloy.js`.

## Hinzufügen des Codes

Fügen Sie den folgenden Codeblock so hoch wie möglich in das `<head>`-Tag Ihres HTML ein:

```html
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.19.1/alloy.min.js" async></script>
```

Dieser Code erstellt asynchron ein `alloy`-Objekt, mit dem Sie einen beliebigen Web-SDK-Befehl aufrufen können. Wenn Sie die Web-SDK synchron laden möchten, können Sie das `async`-Attribut in der letzten Zeile des Codeblocks entfernen. Das Entfernen des `async` verhindert, dass der Rest des HTML-Dokuments vom Browser analysiert und gerendert wird, bis die Bibliothek geladen und ausgeführt wird. Von dieser zusätzlichen Verzögerung vor der Anzeige primärer Inhalte für Benutzer wird normalerweise abgeraten, sie kann jedoch je nach den Anforderungen Ihres Unternehmens sinnvoll sein.
