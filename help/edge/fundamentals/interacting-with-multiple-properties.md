---
title: Interagieren mit mehreren Eigenschaften
seo-title: Adobe Experience Platform Web SDK – Interagieren mit mehreren Eigenschaften
description: Erfahren Sie, wie Sie mit mehreren Experience Platform Web SDK-Eigenschaften interagieren
seo-description: Erfahren Sie, wie Sie mit mehreren Experience Platform Web SDK-Eigenschaften interagieren
translation-type: tm+mt
source-git-commit: 7d4f364ebb9df1ce58481a35007ea75f86ab7825
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 100%

---


# Interagieren mit mehreren Eigenschaften

Es gibt bestimmte Fälle, in denen Sie mit zwei verschiedenen Eigenschaften auf derselben Seite interagieren möchten. Dazu gehören:

* Firmen, die übernommen wurden und an der Integration ihrer Websites arbeiten
* Datenaustausch-Beziehungen zwischen mehreren Firmen
* Kunden, die neue Adobe-Lösungen testen und ihre vorhandene Implementierung nicht stören möchten

Mit dem SDK können Sie für jede Eigenschaft eine separate Instanz erstellen, indem Sie dem Array im Basis-Code einen weiteren Namen hinzufügen. Im folgenden Beispiel haben wir zwei Namen angegeben, `mycustomname1` und `mycustomname2`.

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname1", "mycustomname2"]);
</script>
<script src="alloy.js" async></script>
```

Daher erstellt das Skript zwei Instanzen des SDK. Die globale Funktion für die Interaktion mit der ersten Instanz heißt `mycustomname1` und die globale Funktion für die Interaktion mit der zweiten Instanz heißt `mycustomname2`.

Durch Erstellen von zwei separaten Instanzen kann jede für eine andere Eigenschaft konfiguriert werden. Jede Kommunikations- oder Datenpersistenz, die durch die Interaktion mit `mycustomname1` auftritt, wird isoliert von `mycustomname2` gehalten und umgekehrt.

Im obigen Beispiel können Sie Befehle wie folgt mit jeder der Instanzen ausführen:

```javascript
mycustomname1("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg"
});

mycustomname1("sendEvent", {
  "data": {
    "key": "value"
  }
});

mycustomname2("configure", {
  "edgeConfigId": "f46e981f-fd03-4bdd-a9d9-73ce4447f870",
  "orgId": "ADB3NUMBERSANDLETTERS2@AdobeOrg"
});

mycustomname2("sendEvent", {
  "data": {
    "key": "value"
  }
});
```

Achten Sie darauf, den `configure`-Befehl für jede Instanz auszuführen, bevor Sie andere Befehle auf derselben Instanz ausführen.

## Einschränkungen

Um Konflikte mit Cookies zu vermeiden, kann nur eine Instanz des Adobe Experience Platform Web SDK auf einer Seite eine bestimmte `edgeConfigId` haben.  Ebenso kann nur eine Instanz des Adobe Experience Platform Web SDK eine bestimmte `orgId` haben.
