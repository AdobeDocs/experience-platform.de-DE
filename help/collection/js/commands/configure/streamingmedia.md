---
title: StreamingMedia
description: Konfigurieren Sie die Web-SDK, um Daten zur Mediennutzung in Ihren Web-Eigenschaften zu erfassen.
exl-id: f7733619-d35e-43eb-ac90-052717310c39
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 8%

---

# `streamingMedia`

Mit der `streamingMedia`-Komponente können Sie Daten zu Mediensitzungen auf Ihrer Website erfassen.

Die erfassten Daten können Informationen zu Medienwiedergaben, Pausen, Beendigungen und anderen zugehörigen Ereignissen enthalten. Nach der Erfassung können Sie diese Daten an Adobe Experience Platform oder Adobe Analytics senden, um Berichte zu generieren. Diese Funktion bietet eine umfassende Lösung zum Tracking und zum Verständnis des Medienkonsumverhaltens auf Ihrer Website.

## Voraussetzungen

Um die `streamingMedia`-Komponente von Web SDK verwenden zu können, müssen Sie die folgenden Voraussetzungen erfüllen:

* Stellen Sie sicher, dass Sie Zugriff auf Adobe Experience Platform oder Adobe Analytics haben.
* Sie müssen Web SDK Version 2.20.0 oder höher verwenden. Siehe [Web SDK-Installation - Übersicht](../../install/overview.md), um zu erfahren, wie Sie die neueste Version installieren.
* Aktivieren Sie die Option **[[!UICONTROL Media Analytics]](/help/datastreams/configure.md#advanced-options)** für den verwendeten Datenstrom.
* Stellen Sie sicher, dass das von Ihrem Datenstrom verwendete Schema die Schemafelder der Mediensammlung enthält.
* Konfigurieren Sie die Funktion für Streaming-Medien in der Web-SDK, wie auf dieser Seite dargestellt.

Fügen Sie beim Aufrufen des `configure`-Befehls das `streamingMedia` hinzu.

```js
alloy("configure", {
    streamingMedia: {
        channel: "Video channel",
        playerName: "Example player",
        appVersion: "Media Analytics with Web SDK 2.20.0",
        mainPingInterval: 10,
        adPingInterval: 10
    }
});
```

| Eigenschaft | Typ | Erforderlich | Beschreibung |
| --- | --- | --- | --- |
| **`channel`** | Zeichenfolge | Ja | Der Name des Kanals, in dem die Streaming-Mediensammlung stattfindet. Beispiel: `Video channel`. |
| **`playerName`** | Zeichenfolge | Ja | Der Name des Medien-Players. |
| **`appVersion`** | Zeichenfolge | Nein | Die Version der Media Player-Anwendung. |
| **`mainPingInterval`** | Ganzzahl | Nein | Häufigkeit der Pings für den Hauptinhalt in Sekunden. Der Standardwert lautet `10`. Die Werte können zwischen `10` und `50` Sekunden liegen.  Wenn kein Wert angegeben ist, wird der Standardwert bei der Verwendung von [automatisch verfolgten Sitzungen](../createmediasession.md#automatic) verwendet. |
| **`adPingInterval`** | Ganzzahl | Nein | Häufigkeit der Pings für Anzeigeninhalte in Sekunden. Der Standardwert lautet `10`. Die Werte können zwischen `1` und `10` Sekunden liegen. Wenn kein Wert angegeben ist, wird der Standardwert bei der Verwendung von [automatisch verfolgten Sitzungen](../createmediasession.md#automatic) verwendet. |

## Konfiguration von Streaming-Medien mit der Tag-Erweiterung „Web SDK&quot;

Diese Einstellungen können in der Tag-Erweiterung „Web SDK&quot; mithilfe von [Konfigurationseinstellungen für Streaming-Medien](/help/tags/extensions/client/web-sdk/configure/streaming-media.md) konfiguriert werden.
