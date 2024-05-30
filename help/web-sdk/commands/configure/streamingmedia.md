---
title: streamingMedia
description: Konfigurieren Sie das Web SDK, um Daten im Zusammenhang mit der Mediennutzung in Ihren Web-Eigenschaften zu erfassen.
source-git-commit: c0cb244221215f78f9ef13d8a54a8799ab15df6c
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 6%

---


# `streamingMedia`

Die `streamingMedia` -Komponente können Sie Daten im Zusammenhang mit Mediensitzungen auf Ihrer Website erfassen.

Die erfassten Daten können Informationen zu Medienwiedergaben, Pausen, Beendigungen und anderen damit zusammenhängenden Ereignissen enthalten. Nach der Erfassung können Sie diese Daten an Adobe Experience Platform und/oder Adobe Analytics senden, um Berichte zu erstellen. Diese Funktion bietet eine umfassende Lösung zum Verfolgen und Verstehen des Verhaltens der Mediennutzung auf Ihrer Website.

## Voraussetzungen {#prerequisites}

So verwenden Sie die `streamingMedia` -Komponente des Web SDK müssen Sie die folgenden Voraussetzungen erfüllen:

* Stellen Sie sicher, dass Sie Zugriff auf Adobe Experience Platform und/oder Adobe Analytics haben.
* Sie müssen die Web SDK-Version 2.20.0 oder höher verwenden. Siehe [Übersicht über die Installation des Web SDK](../../install/overview.md) , um zu erfahren, wie Sie die neueste Version installieren.
* Aktivieren Sie die **[[!UICONTROL Media Analytics]](../../../datastreams/configure.md#advanced-options)** -Option für den verwendeten Datastream.
* Stellen Sie sicher, dass das von Ihrem Datastream verwendete Schema die Schemafelder für die Mediensammlung enthält.
* Konfigurieren Sie die Streaming-Medien-Funktion in der Web SDK-Konfiguration, wie auf dieser Seite gezeigt, entweder über das [Tag-Erweiterung](#tag-extension) oder durch [JavaScript-Bibliothek](#library).

## Konfigurieren von Streaming-Medien mithilfe der Web SDK-Tag-Erweiterung {#tag-extension}

Gehen Sie wie folgt vor, um Streaming-Medien in der Web SDK-Tag-Erweiterung zu konfigurieren.

1. Anmelden bei [experience.adobe.com](https://experience.adobe.com) mit Ihren Adobe ID-Anmeldedaten.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** Klicken Sie auf **[!UICONTROL Konfigurieren]** auf [!UICONTROL Adobe Experience Platform Web SDK] Karte.
1. Konfigurieren Sie die **[!UICONTROL Streaming-Medien]** -Einstellungen, wie im Abschnitt [Konfigurationsseite der Web SDK-Tag-Erweiterung](../../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#media-collection).

## Streaming-Medien mithilfe der Web SDK-JavaScript-Bibliothek konfigurieren {#library}

Verwenden Sie zum Konfigurieren von Streaming-Medien im Web SDK die unten beschriebenen Eigenschaften.

Beim Aufrufen der `configure` -Befehl, fügen Sie die `streamingMedia` -Objekt.

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
| `channel` | Zeichenfolge | Ja | Der Name des Kanals, in dem die Streaming-Mediensammlung erfolgt. Beispiel: `Video channel`. |
| `playerName` | Zeichenfolge | Ja | Der Name des Medienplayers. |
| `appVersion` | Zeichenfolge | Nein | Die Version der Medienplayer-Anwendung. |
| `mainPingInterval` | Ganzzahl | Nein | Häufigkeit der Pings für den Hauptinhalt in Sekunden. Der Standardwert lautet `10`. Die Werte können einen Bereich von `10` nach `50` Sekunden.  Wenn kein Wert angegeben ist, wird der Standardwert bei Verwendung von [automatisch verfolgte Sitzungen](../createmediasession.md#automatic). |
| `adPingInterval` | Ganzzahl | Nein | Häufigkeit der Pings für Anzeigeninhalte in Sekunden. Der Standardwert lautet `10`. Die Werte können einen Bereich von `1` nach `10` Sekunden. Wenn kein Wert angegeben ist, wird der Standardwert bei Verwendung von [automatisch verfolgte Sitzungen](../createmediasession.md#automatic). |
