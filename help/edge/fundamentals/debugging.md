---
title: Debugging
seo-title: Adobe Experience Platform Web SDK – Debugging
description: Erfahren Sie, wie Sie das Debugging im Experience Platform Web SDK aktivieren
seo-description: Erfahren Sie, wie Sie das Debugging im Experience Platform Web SDK aktivieren
translation-type: tm+mt
source-git-commit: 31a527cb4ad1348262131f827c7e932404542c4b
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 100%

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
  "configId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```

>[!Hint]
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

Wenn das Debugging über den `debug`-Befehl oder den Abfragezeichenfolgen-Parameter festgelegt wird, setzt er alle `debug`-Optionen, die im `configure`-Befehl eingestellt sind, außer Kraft. In diesen beiden Fällen bleibt das Debugging auch während der Dauer der Sitzung umgeschaltet. Wenn Sie also das Debugging mit dem Debugging-Befehl oder dem Abfragezeichenfolgen-Parameter aktivieren, bleibt es aktiviert, bis einer der folgenden Schritte ausgeführt wird:

* Beenden der Sitzung
* Sie führen den `debug`-Befehl aus
* Sie legen den Abfragezeichenfolgen-Parameter erneut fest
