---
title: Debugging im Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie die Debugging-Funktionen im Web SDK der Experience Platform umschalten.
keywords: Debugging von Web SDK;Debugging;Konfigurieren;Befehl;Debugging-Befehl;edgeConfigId;setDebug;debugEnabled;Debuggen;
exl-id: 4e893af8-a48e-48dc-9737-4c61b3355f03
source-git-commit: 0f671a967a67761e0cfef6fa0d022e3c3790c2d8
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 73%

---

# Debugging

Wenn das Debugging aktiviert ist, gibt das SDK Meldungen an die Browser-Konsole aus, die beim Debugging Ihrer Implementierung und beim Verständnis des Verhaltens des SDK hilfreich sein können. Das Debuggen führt auch zu einer Server-seitigen synchronen Überprüfung der Daten, die für das von Ihnen konfigurierte Schema erfasst werden.

Das Debuggen ist standardmäßig deaktiviert, kann jedoch auf drei verschiedene Arten aktiviert werden:

* `configure`-Befehl
* `setDebug`-Befehl
* Abfragezeichenfolge-Parameter

## Debugging mit dem Befehl „Konfigurieren“ aktivieren

Aktivieren Sie beim Konfigurieren des SDK mit dem `configure`-Befehl das Debugging, indem Sie die `debugEnabled`-Option auf `true` einstellen.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```

>[!TIP]
>
>Dies ermöglicht das Debugging für alle Nutzer der Web-Seite und nicht nur für Ihren persönlichen Browser.

## Debugging mit dem Befehl „Debuggen“ aktivieren

Schalten Sie das Debugging wie folgt mit einem separaten `debug`-Befehl um:

```javascript
alloy("setDebug", {
  "enabled": true
});
```

Wenn Sie es vorziehen, keinen Code auf Ihrer Web-Seite zu ändern oder keine Protokollmeldungen für alle Nutzer Ihrer Website zu erstellen, ist dies besonders nützlich, da Sie den `debug`-Befehl jederzeit in der JavaScript-Konsole Ihres Browsers ausführen können.

## Debugging mit einem Abfragezeichenfolgen-Parameter aktivieren

Aktivieren Sie das Debugging, indem Sie einen `alloy_debug`-Abfragezeichenfolgen-Parameter wie folgt auf `true` oder `false` einstellen:

```HTTP
http://example.com/?alloy_debug=true
```

Ähnlich wie der `debug`-Befehl ist dies besonders hilfreich, wenn Sie keinen Code auf Ihrer Web-Seite ändern möchten oder keine Protokollmeldungen für alle Nutzer Ihrer Website erstellen möchten, da Sie beim Laden der Web-Seite in Ihrem Browser den Abfragezeichenfolgen-Parameter festlegen können.

## Priorität und Dauer

Wenn das Debugging über den `debug`-Befehl oder den Abfragezeichenfolgen-Parameter festgelegt wird, setzt er alle `debug`-Optionen, die im `configure`-Befehl eingestellt sind, außer Kraft. In diesen beiden Fällen bleibt das Debugging auch für die Dauer der Sitzung aktiviert. Wenn Sie also das Debugging mit dem Debugging-Befehl oder dem Abfragezeichenfolgen-Parameter aktivieren, bleibt es aktiviert, bis einer der folgenden Schritte ausgeführt wird:

* Beenden der Sitzung
* Sie führen den `debug`-Befehl aus
* Sie legen den Abfragezeichenfolgen-Parameter erneut fest

## Abrufen von Bibliotheksinformationen

Es ist oft hilfreich, auf einige Details hinter der Bibliothek zuzugreifen, die Sie in Ihre Website geladen haben. Führen Sie dazu den `getLibraryInfo`-Befehl wie folgt aus:

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
});
```

Derzeit enthält das bereitgestellte `libraryInfo`-Objekt die folgenden Eigenschaften:

* `version` Dies ist die Version der geladenen Bibliothek. Wenn die Version der Bibliothek, die geladen wird, beispielsweise 1.0.0 wäre, wäre der Wert `1.0.0`. Wenn die Bibliothek innerhalb der Adobe Experience Platform Launch-Erweiterung (mit dem Namen &quot;AEP Web SDK&quot;) ausgeführt wird, ist die Version die Bibliotheksversion und die Platform launch-Erweiterungsversion mit einem &quot;+&quot;-Zeichen verbunden. Wenn beispielsweise die Bibliotheksversion 1.0.0 und die Platform launch-Erweiterung 1.2.0 wäre, wäre der Wert `1.0.0+1.2.0`.
