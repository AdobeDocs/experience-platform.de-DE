---
title: Mehrere Web SDK-Instanzen verwenden
description: Erfahren Sie, wie Sie mit mehreren Experience Platform Web SDK-Eigenschaften interagieren.
keywords: mehrere Eigenschaften;configure;sendEvent;edgeConfigId;orgId;
exl-id: e07afb0d-3490-414f-bc9c-f71bc04fe664
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 63%

---

# Mehrere Web SDK-Instanzen verwenden

Es gibt bestimmte Fälle, in denen Sie mit zwei verschiedenen Eigenschaften auf derselben Seite interagieren möchten. Zu diesen Fällen gehören:

* Firmen, die übernommen wurden und an der Integration ihrer Websites arbeiten
* Datenaustausch-Beziehungen zwischen mehreren Firmen
* Kunden, die neue Adobe-Lösungen testen und ihre vorhandene Implementierung nicht stören möchten

Mit dem SDK können Sie für jede Eigenschaft eine separate Instanz erstellen, indem Sie dem Array im Basis-Code einen weiteren Namen hinzufügen. Im folgenden Beispiel werden zwei Namen angegeben: `titanium` und `copper`.

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

Durch Erstellen von zwei separaten Instanzen kann jede für eine andere Eigenschaft konfiguriert werden. Jede Kommunikations- oder Datenpersistenz, die durch die Interaktion mit `titanium` wird isoliert von `copper`.

Im obigen Beispiel können Sie Befehle mit jeder Instanz ausführen:

```javascript
titanium("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg"
});

titanium("sendEvent", {
  "data": {
    "key": "value"
  }
});

copper("configure", {
  "edgeConfigId": "f46e981f-fd03-4bdd-a9d9-73ce4447f870",
  "orgId": "ADB3NUMBERSANDLETTERS2@AdobeOrg"
});

copper("sendEvent", {
  "data": {
    "key": "value"
  }
});
```

Achten Sie darauf, den `configure`-Befehl für jede Instanz auszuführen, bevor Sie andere Befehle auf derselben Instanz ausführen.

>[!IMPORTANT]
>
>Um Konflikte mit Cookies zu vermeiden, muss jede Web SDK-Instanz über eine eigene eindeutige `edgeConfigId` und ihre eigenen `orgId`.
