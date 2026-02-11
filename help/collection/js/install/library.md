---
title: Installieren der Web SDK JavaScript-Bibliothek
description: Referenzieren Sie die Web-SDK-Bibliothek mithilfe einer eigenständigen CDN-Datei.
exl-id: bacfe938-4326-48f6-a321-bd16970e77eb
source-git-commit: 010192e91185c11d5454d4153913c06b90fe2122
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# Installieren der Web SDK JavaScript-Bibliothek

Wenn Sie sich gegen die Verwendung der [Web SDK-Tag-Erweiterung](/help/tags/extensions/client/web-sdk/overview.md) entscheiden, können Sie die Web-SDK installieren, indem Sie auf die eigenständige JavaScript-Bibliothek verweisen, die im CDN von Adobe gehostet wird. Sie können direkt auf die Bibliothek verweisen oder sie herunterladen und in Ihrer eigenen Infrastruktur hosten. Es ist in minimierten und vollständigen Formaten verfügbar.

Die Web-SDK-Bibliothek ist über die folgende URL-Struktur verfügbar:

* **minifiziert**: `https://cdn1.adoberesources.net/alloy/<VERSION>/alloy.min.js`
* **Voll**: `https://cdn1.adoberesources.net/alloy/<VERSION>/alloy.js`

In den [Versionshinweisen zu Web SDK](../release-notes.md) finden Sie die neueste Version, die in die URL aufgenommen werden soll. Beispielsweise ist die URL für die Vollversion der Version 2.19.1 `https://cdn1.adoberesources.net/alloy/2.19.1/alloy.js`.

## Hinzufügen des Basis-Codes und des Bibliotheksladers

Der hinzuzufügende Code besteht aus zwei Abschnitten:

* **Basis-Code**: Ermöglicht das Bootstrapping durch Einreihen von Befehlen in die Warteschlange, während der Web SDK asynchron geladen wird. Weitere Informationen finden [&#x200B; unter &#x200B;](base-code.md)-Code . Adobe empfiehlt die Verwendung des Basis-Codes beim asynchronen Laden der Bibliothek, um Wettlaufsituationen beim Aufrufen von Web-SDK-Befehlen beim Laden der Seite zu vermeiden.
* **Library Loader**: Lädt die vollständige JavaScript-Bibliothek.

Fügen Sie den folgenden Codeblock so hoch wie möglich im `<head>`-Tag vor Skripten hinzu, die möglicherweise die Web-SDK aufrufen:

```html
<!-- Base code -->
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<!-- Library loader -->
<script src="https://cdn1.adoberesources.net/alloy/<VERSION>/alloy.min.js" async></script>
```

Wenn Sie die Web-SDK synchron laden möchten, können Sie das `async`-Attribut beim Laden der Bibliothek entfernen. Das Entfernen des `async` blockiert das Parsen von HTML, während der Browser die Bibliothek abruft und ausführt. Von dieser zusätzlichen Verzögerung vor der Anzeige primärer Inhalte für Benutzer wird normalerweise abgeraten, sie kann jedoch je nach den Anforderungen Ihres Unternehmens sinnvoll sein.
