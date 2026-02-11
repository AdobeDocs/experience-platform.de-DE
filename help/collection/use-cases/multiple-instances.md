---
title: Verwenden mehrerer SDK-Web-Instanzen
description: Erfahren Sie, wie Sie mit mehreren Experience Platform Web SDK-Eigenschaften interagieren.
keywords: Multiple Properties
exl-id: e07afb0d-3490-414f-bc9c-f71bc04fe664
source-git-commit: 192739967e6b050bb04893ee7bab5119dd7f870c
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 23%

---

# Verwenden mehrerer SDK-Web-Instanzen

Es gibt bestimmte Fälle, in denen Sie mit zwei verschiedenen Eigenschaften auf derselben Seite interagieren möchten. Mögliche Szenarien sind:

* Firmen, die übernommen wurden und an der Integration ihrer Websites arbeiten
* Datenaustausch-Beziehungen zwischen mehreren Firmen
* Kunden, die neue Adobe-Lösungen testen und ihre bestehende Implementierung nicht stören möchten

Mit SDK können Sie für jede Eigenschaft eine separate Instanz erstellen, indem Sie dem Array im [Basis-Code) einen anderen Namen &#x200B;](../js/install/base-code.md). Das folgende Beispiel stellt zwei Namen bereit: `titanium` und `copper`.

```html
<!-- Base code -->
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
  (window,["titanium", "copper"]);
</script>

<!-- Load the Web SDK (JavaScript library loader or Tags embed code) -->
<!-- <script src=".../alloy.min.js" async></script> -->
<!-- <script src=".../launch-<ENV>.min.js" async></script> -->
```

Daher erstellt das Skript zwei globale Funktionen (`titanium` und `copper` im obigen Beispiel), die bei der Initialisierung der Bibliothek zu zwei SDK-Instanzen werden. Jede Instanz behält ihre eigene Konfiguration und ihren eigenen Status bei. Jeder Befehl, der `titanium` verwendet, wird von `copper` isoliert.

>[!TIP]
>
>Wenn Sie den Basis-Code mit Tags verwenden, stellen Sie sicher, dass alle von Ihnen festgelegten Instanznamen mit allen [SDK](/help/tags/extensions/client/web-sdk/configure/general.md)Instanznamen übereinstimmen, wenn Sie die Tag-Erweiterung konfigurieren.

Nach dem Benennungsmuster von `titanium` und `copper` as Web SDK-Instanzen können Sie Befehle unabhängig voneinander ausführen:

```javascript
titanium("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg"
});

titanium("sendEvent", {
  data: {
    key: "value"
  }
});

copper("configure", {
  datastreamId: "f46e981f-fd03-4bdd-a9d9-73ce4447f870",
  orgId: "ADB3NUMBERSANDLETTERS2@AdobeOrg"
});

copper("sendEvent", {
  data: {
    key: "value"
  }
});
```

Achten Sie darauf, den [`configure`](../js/commands/configure/overview.md)-Befehl für jede Instanz auszuführen, bevor Sie andere Befehle auf derselben Instanz ausführen.

>[!IMPORTANT]
>
>Um Konflikte mit Cookies zu vermeiden, muss jede Web SDK-Instanz über eine eigene eindeutige `datastreamId` und eine eigene eindeutige `orgId` verfügen.
