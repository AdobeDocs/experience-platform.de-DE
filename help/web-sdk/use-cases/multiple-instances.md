---
title: Verwenden mehrerer SDK-Web-Instanzen
description: Erfahren Sie, wie Sie mit mehreren Experience Platform Web SDK-Eigenschaften interagieren.
keywords: Multiple Properties
exl-id: e07afb0d-3490-414f-bc9c-f71bc04fe664
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 64%

---

# Verwenden mehrerer SDK-Web-Instanzen

Es gibt bestimmte Fälle, in denen Sie mit zwei verschiedenen Eigenschaften auf derselben Seite interagieren möchten. Zu diesen Fällen gehören:

* Firmen, die übernommen wurden und an der Integration ihrer Websites arbeiten
* Datenaustausch-Beziehungen zwischen mehreren Firmen
* Kunden, die neue Adobe-Lösungen testen und ihre vorhandene Implementierung nicht stören möchten

Mit dem SDK können Sie für jede Eigenschaft eine separate Instanz erstellen, indem Sie dem Array im Basis-Code einen weiteren Namen hinzufügen. Das folgende Beispiel stellt zwei Namen bereit: `titanium` und `copper`.

```html
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["titanium", "copper"]);
</script>
<script src="alloy.js" async></script>
```

Daher erstellt das Skript zwei Instanzen des SDK. Die globale Funktion für die Interaktion mit der ersten Instanz heißt `titanium` und die globale Funktion für die Interaktion mit der zweiten Instanz heißt `copper`.

Durch Erstellen von zwei separaten Instanzen kann jede für eine andere Eigenschaft konfiguriert werden. Jegliche Kommunikation oder Datenpersistenz, die aufgrund der Interaktion mit `titanium` auftritt, wird von `copper` isoliert.

Im folgenden Beispiel können Sie Befehle mit jeder Instanz ausführen:

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

Achten Sie darauf, den `configure`-Befehl für jede Instanz auszuführen, bevor Sie andere Befehle auf derselben Instanz ausführen.

>[!IMPORTANT]
>
>Um Konflikte mit Cookies zu vermeiden, muss jede Web SDK-Instanz über eine eigene eindeutige `datastreamId` und eine eigene eindeutige `orgId` verfügen.
