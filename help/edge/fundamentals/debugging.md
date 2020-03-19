---
title: Debugging
seo-title: Debugging für Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie das Debugging von Experience Platform Web SDK umschalten
seo-description: Erfahren Sie, wie Sie das Debugging von Experience Platform Web SDK umschalten
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (Beta) Debugging

>[!IMPORTANT]
>
>Das Adobe Experience Platform Web SDK befindet sich derzeit in der Betaphase und steht nicht allen Benutzern zur Verfügung. Dokumentation und Funktionalität können sich ändern.

Wenn das Debugging aktiviert ist, gibt das SDK Meldungen an die Browser-Konsole aus, die beim Debugging Ihrer Implementierung und beim Verständnis des Verhaltens des SDK hilfreich sein können. Das Debuggen führt auch zu einer serverseitigen synchronen Überprüfung der Daten, die für das konfigurierte Schema erfasst werden.

Das Debuggen ist standardmäßig deaktiviert, kann jedoch auf drei verschiedene Arten umgeschaltet werden:

* `configure` command
* `debug` command
* enthält

## Debugging mit dem Befehl &quot;Konfigurieren&quot; umschalten

Aktivieren Sie beim Konfigurieren des SDK mit dem `configure` Befehl das Debugging, indem Sie die `debugEnabled` Option auf `true`.

```javascript
alloy("configure", {
  "configId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```

>[!Hint]
>Dies ermöglicht das Debugging für alle Benutzer der Webseite und nicht nur für Ihren persönlichen Browser.

## Debugging mit dem Befehl &quot;Debuggen&quot;umschalten

Schalten Sie das Debugging wie folgt mit einem separaten `debug` Befehl um:

```javascript
alloy("debug", {
  "enabled": true
});
```

Wenn Sie es vorziehen, keinen Code auf Ihrer Webseite zu ändern oder keine Protokollmeldungen für alle Benutzer Ihrer Website zu erstellen, ist dies besonders nützlich, da Sie den `debug` Befehl jederzeit in der JavaScript-Konsole Ihres Browsers ausführen können.

## Debugging mit einem Abfrage-Zeichenfolgenparameter umschalten

Schalten Sie das Debugging um, indem Sie einen `alloy_debug` Abfragen-Zeichenfolgenparameter auf `true` oder `false` wie folgt festlegen:

```HTTP
http://example.com/?alloy_debug=true
```

Ähnlich wie der `debug` Befehl ist dies besonders hilfreich, wenn Sie keinen Code auf Ihrer Webseite ändern möchten oder keine Protokollmeldungen für alle Benutzer Ihrer Website erstellen möchten, da Sie beim Laden der Webseite in Ihrem Browser den Abfrage-Zeichenfolgenparameter festlegen können.

## Priorität und Dauer

Wenn das Debugging über den `debug` Befehls- oder Abfragen-Zeichenfolgenparameter festgelegt wird, setzt er alle `debug` im `configure` Befehl festgelegten Optionen außer Kraft. In diesen beiden Fällen bleibt das Debugging auch während der Dauer der Sitzung umgeschaltet. Wenn Sie das Debugging mit dem Debugging-Befehl oder dem Abfrage-Zeichenfolgenparameter aktivieren, bleibt es aktiviert, bis einer der folgenden Schritte ausgeführt wird:

* Ende der Sitzung
* Sie führen den `debug` Befehl
* Sie legen den Abfrage-Zeichenfolgenparameter erneut fest
