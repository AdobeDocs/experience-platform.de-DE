---
title: StreamingMedia
description: Konfigurieren Sie die Web-SDK, um Daten zur Mediennutzung in Ihren Web-Eigenschaften zu erfassen.
exl-id: f7733619-d35e-43eb-ac90-052717310c39
source-git-commit: 57d42d88ec9a93744450a2a352590ab57d9e5bb7
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 6%

---

# `streamingMedia`

Mit der `streamingMedia`-Komponente können Sie Daten zu Mediensitzungen auf Ihrer Website erfassen.

Die erfassten Daten können Informationen zu Medienwiedergaben, Pausen, Beendigungen und anderen zugehörigen Ereignissen enthalten. Nach der Erfassung können Sie diese Daten an Adobe Experience Platform und/oder Adobe Analytics senden, um Berichte zu generieren. Diese Funktion bietet eine umfassende Lösung zum Tracking und zum Verständnis des Medienkonsumverhaltens auf Ihrer Website.

## Voraussetzungen {#prerequisites}

Um die `streamingMedia` von Web SDK verwenden zu können, müssen Sie die folgenden Voraussetzungen erfüllen:

* Stellen Sie sicher, dass Sie Zugriff auf Adobe Experience Platform und/oder Adobe Analytics haben.
* Sie müssen Web SDK Version 2.20.0 oder höher verwenden. Siehe [Web SDK-Installation - Übersicht](../../install/overview.md), um zu erfahren, wie Sie die neueste Version installieren.
* Aktivieren Sie **[[!UICONTROL Option]](../../../datastreams/configure.md#advanced-options)** Media Analytics) für den verwendeten Datenstrom.
* Stellen Sie sicher, dass das von Ihrem Datenstrom verwendete Schema die Schemafelder der Mediensammlung enthält.
* Konfigurieren Sie die Funktion für Streaming-Medien in der Web-SDK-Konfiguration, wie auf dieser Seite gezeigt, entweder über die [Tag-Erweiterung](#tag-extension) oder über die [JavaScript-Bibliothek](#library).

## Konfigurieren von Streaming-Medien mit der Tag-Erweiterung „Web SDK&quot; {#tag-extension}

Gehen Sie wie folgt vor, um Streaming-Medien in der Tag-Erweiterung „Web SDK&quot; zu konfigurieren.

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei ](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** und klicken Sie dann auf **[!UICONTROL Konfigurieren]** auf der Karte [!UICONTROL Adobe Experience Platform Web SDK].
1. Konfigurieren Sie die **[!UICONTROL Streaming Media]** wie auf der Seite [Konfiguration von Web SDK-Tag-Erweiterungen](../../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#media-collection) beschrieben.

## Konfigurieren von Streaming-Medien mit der Web SDK JavaScript-Bibliothek {#library}

Verwenden Sie zum Konfigurieren von Streaming-Medien in Web SDK die unten beschriebenen Eigenschaften.

Fügen Sie beim Aufrufen des `configure`-Befehls das `streamingMedia` hinzu.

```js
alloy("configure", {
    streamingMedia: {
        channel: "video channel",
        playerName: "test player",
        appVersion: "Media Analytics with Web SDK 2.20.0",
        mainPingInterval: 10,
        adPingInterval: 10
    }
});
```

| Eigenschaft | Typ | Erforderlich | Beschreibung |
|---------|----------|---------|---------|
| `channel` | Zeichenfolge | Ja | Der Name des Kanals, in dem die Streaming-Mediensammlung stattfindet. Beispiel: `Video channel`. |
| `playerName` | Zeichenfolge | Ja | Der Name des Medien-Players. |
| `appVersion` | Zeichenfolge | Nein | Die Version der Media Player-Anwendung. |
| `mainPingInterval` | Ganzzahl | Nein | Häufigkeit der Pings für den Hauptinhalt in Sekunden. Der Standardwert lautet `10`. Die Werte können zwischen `10` und `50` Sekunden liegen.  Wenn kein Wert angegeben ist, wird der Standardwert bei der Verwendung von [automatisch verfolgten Sitzungen](../createmediasession.md#automatic) verwendet. |
| `adPingInterval` | Ganzzahl | Nein | Häufigkeit der Pings für Anzeigeninhalte in Sekunden. Der Standardwert lautet `10`. Die Werte können zwischen `1` und `10` Sekunden liegen. Wenn kein Wert angegeben ist, wird der Standardwert bei der Verwendung von [automatisch verfolgten Sitzungen](../createmediasession.md#automatic) verwendet. |
