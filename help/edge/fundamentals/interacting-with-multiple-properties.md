---
title: Interagieren mit mehreren Eigenschaften im Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie mit mehreren Experience Platform Web SDK-Eigenschaften interagieren.
keywords: multiple properties;configure;sendEvent;edgeConfigId;orgId;
translation-type: tm+mt
source-git-commit: b865b7fb940ca2d5f8b44f71eb58e62e3473f52d
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 68%

---


# Interagieren mit mehreren Eigenschaften

Es gibt bestimmte Fälle, in denen Sie mit zwei verschiedenen Eigenschaften auf derselben Seite interagieren möchten. Dazu gehören:

* Firmen, die übernommen wurden und an der Integration ihrer Websites arbeiten
* Datenaustausch-Beziehungen zwischen mehreren Firmen
* Kunden, die neue Adobe-Lösungen testen und ihre vorhandene Implementierung nicht stören möchten

Mit dem SDK können Sie für jede Eigenschaft eine separate Instanz erstellen, indem Sie dem Array im Basis-Code einen weiteren Namen hinzufügen. Im folgenden Beispiel werden die beiden Namen `mycustomname1` und `mycustomname2` angezeigt.

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

Durch Erstellen von zwei separaten Instanzen kann jede für eine andere Eigenschaft konfiguriert werden. Jede Kommunikations- oder Datenpersistenz, die durch Interaktion mit `mycustomname1` auftritt, wird von `mycustomname2` isoliert gehalten.

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

Um Konflikte mit Cookies zu vermeiden, kann nur eine Instanz von Adobe Experience Platform [!DNL Web SDK] innerhalb einer Seite ein bestimmtes `edgeConfigId` aufweisen. Ebenso kann nur eine Instanz von Adobe Experience Platform [!DNL Web SDK] ein bestimmtes `orgId` haben.
