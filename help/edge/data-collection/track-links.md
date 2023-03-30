---
title: Verfolgen von Links mit dem Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie Linkdaten mit Experience Platform Web SDK an Adobe Analytics senden.
keywords: adobe analytics;analytics;sendEvent;s.t();s.tl();webPageDetails;pageViews;webInteraction;Web Interaction;Seitenansichten;Linktracking;Links;Link verfolgen;ClickCollection;ClickCollection;Sammlung;
exl-id: d5a1804c-8f91-4083-a46e-ea8f7edf36b6
source-git-commit: 04078a53bc6bdc01d8bfe0f2e262a28bbaf542da
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 1%

---

# Verfolgen von Links

Links können manuell festgelegt oder verfolgt werden [automatisch](#automaticLinkTracking). Manuelles Tracking erfolgt durch Hinzufügen der Details unter der `web.webInteraction` Teil des Schemas. Es gibt drei erforderliche Variablen:

* `web.webInteraction.name`
* `web.webInteraction.type`
* `web.webInteraction.linkClicks.value`

```javascript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webInteraction": {
        "linkClicks": {
            "value": 1
        },
        "name": "My Custom Link", // Name that shows up in the custom links report
        "URL": "https://myurl.com", // The URL of the link
        "type": "other" // values: other, download, exit
      }
    }
  }
});
```

Ab Version 2.15.0 erfasst das Web SDK die `region` des angeklickten HTML-Elements. Dadurch wird die [Activity Map](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/activity-map.html?lang=de) Berichtsfunktionen in Adobe Analytics.

Der Linktyp kann einen von drei Werten sein:

* **`other`:** Ein benutzerspezifischer Link
* **`download`:** Ein Downloadlink
* **`exit`:** Ein Exitlink

Diese Werte sind [automatisch zugeordnet](adobe-analytics/automatically-mapped-vars.md) in Adobe Analytics [konfiguriert](adobe-analytics/analytics-overview.md) um dies zu tun.

## Automatische Linktracking {#automaticLinkTracking}

Standardmäßig erfasst, markiert und erfasst das Web SDK Klicks auf qualifizierende Link-Tags. Klicks werden mit einem [erfassen](https://www.w3.org/TR/uievents/#capture-phase) Klicken Sie auf Ereignis-Listener, der an das Dokument angehängt ist.

Die automatische Linktracking kann deaktiviert werden durch [configuring](../fundamentals/configuring-the-sdk.md#clickCollectionEnabled) das Web SDK.

```javascript
clickCollectionEnabled: false
```

### Welche Tags qualifizieren sich für Linktracking?{#qualifyingLinks}

Automatische Linktracking für Anker `A` und `AREA` Tags. Diese Tags werden jedoch nicht für das Linktracking berücksichtigt, wenn sie eine angehängte `onclick` Handler.

### Wie werden Links beschriftet?{#labelingLinks}

Links werden als Downloadlink bezeichnet, wenn das Anker-Tag ein Download-Attribut enthält oder wenn der Link mit einer beliebten Dateierweiterung endet. Der Downloadlink-Qualifizierer kann [konfiguriert](../fundamentals/configuring-the-sdk.md) mit regulärem Ausdruck:

```javascript
downloadLinkQualifier: "\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"
```

Links werden als Exitlink bezeichnet, wenn sich die Zieldomäne des Links von der aktuellen unterscheidet `window.location.hostname`.

Links, die nicht als Download- oder Exitlink qualifiziert sind, werden als &quot;andere&quot;bezeichnet.

### Wie können Linktracking-Werte gefiltert werden?

Die mit dem automatischen Linktracking erfassten Daten können mithilfe einer [onBeforeEventSend-Rückruffunktion](../fundamentals/tracking-events.md#modifying-events-globally).

Das Filtern von Linktracking-Daten kann bei der Vorbereitung von Daten für Analytics-Berichte nützlich sein. Das automatische Linktracking erfasst sowohl den Linknamen als auch die Link-URL. In Analytics-Berichten hat der Linkname Vorrang vor der Link-URL. Wenn Sie die Link-URL melden möchten, muss der Linkname entfernt werden. Das folgende Beispiel zeigt eine `onBeforeEventSend` -Funktion, die den Linknamen für Downloadlinks entfernt:

```javascript
alloy("configure", {
  onBeforeEventSend: function(options) {
    if (options
      && options.xdm
      && options.xdm.web
      && options.xdm.web.webInteraction) {
        if (options.xdm.web.webInteraction.type === "download") {
          options.xdm.web.webInteraction.name = undefined;
        }
    }
  }
});
```

Ab Web SDK-Version 2.15.0 können die mit dem automatischen Linktracking erfassten Daten durch Bereitstellung einer [onBeforeLinkClickSend-Rückruffunktion](../fundamentals/configuring-the-sdk.md#onBeforeLinkClickSend).

Diese Rückruffunktion wird nur ausgeführt, wenn ein automatisches Link-Klick-Ereignis auftritt.

```javascript
alloy("configure", {
  onBeforeLinkClickSend: function(options) {
    if (options.xdm.web.webInteraction.type === "download") {
      options.xdm.web.webInteraction.name = undefined;
    }
  }
});
```

Beim Filtern von Linktracking-Ereignissen mithilfe des `onBeforeLinkClickSend` Befehl, Adobe empfiehlt, `false` für die Link-Klicks, die nicht verfolgt werden sollen. Bei jeder anderen Antwort sendet das Web SDK die Daten an das Edge-Netzwerk.


>[!NOTE]
>
>** Wenn beide `onBeforeEventSend` und `onBeforeLinkClickSend` Callback-Funktionen festgelegt sind, führt das Web SDK die `onBeforeLinkClickSend` Callback-Funktion zum Filtern und Erweitern des Link-Klickinteraktionsereignisses, gefolgt von der `onBeforeEventSend` Callback-Funktion.