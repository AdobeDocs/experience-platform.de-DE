---
title: Interaktion mit mehreren Eigenschaften
seo-title: Adobe Experience Platform Web SDK Interaktion mit mehreren Eigenschaften
description: Erfahren Sie, wie Sie mit mehreren Experience Platform Web SDK-Eigenschaften interagieren.
seo-description: Erfahren Sie, wie Sie mit mehreren Experience Platform Web SDK-Eigenschaften interagieren.
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (Beta) Interaktion mit mehreren Eigenschaften

>[!IMPORTANT]
>
>Das Adobe Experience Platform Web SDK befindet sich derzeit in der Betaphase und steht nicht allen Benutzern zur Verfügung. Dokumentation und Funktionalität können sich ändern.

Es gibt bestimmte Fälle, in denen Sie mit zwei verschiedenen Eigenschaften auf derselben Seite interagieren möchten. Dazu gehören:

* Firmen, die erworben wurden und an der Integration ihrer Websites arbeiten
* Datenaustausch-Beziehungen zwischen mehreren Firmen
* Kunden, die neue Adobe-Lösungen testen und ihre vorhandene Implementierung nicht stören möchten

Mit dem SDK können Sie für jede Eigenschaft eine separate Instanz erstellen, indem Sie dem Array im Basiscode einen weiteren Namen hinzufügen. Im folgenden Beispiel haben wir zwei Namen angegeben, `mycustomname1` und `mycustomname2`.

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname1", "mycustomname2"]);
</script>
<script src="alloy.js" async></script>
```

Daher erstellt das Skript zwei Instanzen des SDK. Die globale Funktion für die Interaktion mit der ersten Instanz wird benannt `mycustomname1` und die globale Funktion für die Interaktion mit der zweiten Instanz wird benannt `mycustomname2`.

Durch Erstellen von zwei separaten Instanzen kann jede für eine andere Eigenschaft konfiguriert werden. Jede Kommunikations- oder Datenpersistenz, die durch Interaktion mit dem Server auftritt, `mycustomname1` wird isoliert von `mycustomname2` und umgekehrt gehalten.

Im obigen Beispiel können Sie Befehle wie folgt mit jeder der Instanzen ausführen:

```javascript
mycustomname1("configure", {
  "configId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg"
});

mycustomname1("event", {
  "data": {
    "key": "value"
  }
});

mycustomname2("configure", {
  "configId": "f46e981f-fd03-4bdd-a9d9-73ce4447f870",
  "orgId": "ADB3NUMBERSANDLETTERS2@AdobeOrg"
});

mycustomname2("event", {
  "data": {
    "key": "value"
  }
});
```

Achten Sie darauf, den `configure` Befehl für jede Instanz auszuführen, bevor Sie andere Befehle auf derselben Instanz ausführen.

## Einschränkungen

Um Konflikte mit Cookies zu vermeiden, kann nur eine Instanz des Adobe Experience Platform Web SDK auf einer Seite eine bestimmte Instanz aufweisen `configId`.  Ebenso kann nur eine Instanz des Adobe Experience Platform Web SDK eine bestimmte Instanz haben `orgId`.
