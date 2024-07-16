---
title: streamingMedia
description: Konfigurieren Sie das Web SDK, um Daten im Zusammenhang mit der Mediennutzung in Ihren Web-Eigenschaften zu erfassen.
exl-id: f7733619-d35e-43eb-ac90-052717310c39
source-git-commit: 57d42d88ec9a93744450a2a352590ab57d9e5bb7
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 6%

---

# `streamingMedia`

Mit der Komponente `streamingMedia` können Sie Daten im Zusammenhang mit Mediensitzungen auf Ihrer Website erfassen.

Die erfassten Daten können Informationen zu Medienwiedergaben, Pausen, Beendigungen und anderen damit zusammenhängenden Ereignissen enthalten. Nach der Erfassung können Sie diese Daten an Adobe Experience Platform und/oder Adobe Analytics senden, um Berichte zu erstellen. Diese Funktion bietet eine umfassende Lösung zum Verfolgen und Verstehen des Verhaltens der Mediennutzung auf Ihrer Website.

## Voraussetzungen {#prerequisites}

Um die Komponente `streamingMedia` des Web SDK zu verwenden, müssen Sie die folgenden Voraussetzungen erfüllen:

* Stellen Sie sicher, dass Sie Zugriff auf Adobe Experience Platform und/oder Adobe Analytics haben.
* Sie müssen die Web SDK-Version 2.20.0 oder höher verwenden. Informationen zur Installation der neuesten Version finden Sie in der [Übersicht zur Installation des Web SDK](../../install/overview.md) .
* Aktivieren Sie die Option **[[!UICONTROL Media Analytics]](../../../datastreams/configure.md#advanced-options)** für den verwendeten Datastream.
* Stellen Sie sicher, dass das von Ihrem Datastream verwendete Schema die Schemafelder für die Mediensammlung enthält.
* Konfigurieren Sie die Streaming-Medien-Funktion in der Web SDK-Konfiguration, wie auf dieser Seite gezeigt, entweder über die [Tag-Erweiterung](#tag-extension) oder über die [JavaScript-Bibliothek](#library).

## Konfigurieren von Streaming-Medien mithilfe der Web SDK-Tag-Erweiterung {#tag-extension}

Gehen Sie wie folgt vor, um Streaming-Medien in der Web SDK-Tag-Erweiterung zu konfigurieren.

1. Melden Sie sich mit Ihren Adobe ID-Anmeldedaten bei [experience.adobe.com](https://experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** und klicken Sie dann auf der Karte [!UICONTROL Adobe Experience Platform Web SDK] auf **[!UICONTROL Konfigurieren]** .
1. Konfigurieren Sie die Einstellungen für **[!UICONTROL Streaming-Medien]** wie auf der Konfigurationsseite für die [Web SDK-Tag-Erweiterung](../../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#media-collection) beschrieben.

## Streaming-Medien mithilfe der Web SDK JavaScript-Bibliothek konfigurieren {#library}

Verwenden Sie zum Konfigurieren von Streaming-Medien im Web SDK die unten beschriebenen Eigenschaften.

Fügen Sie beim Aufrufen des Befehls `configure` das Objekt `streamingMedia` hinzu.

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
| `mainPingInterval` | Ganzzahl | Nein | Häufigkeit der Pings für den Hauptinhalt in Sekunden. Der Standardwert lautet `10`. Die Werte können zwischen `10` und `50` Sekunden liegen.  Wenn kein Wert angegeben ist, wird der Standardwert bei Verwendung von [automatisch verfolgten Sitzungen](../createmediasession.md#automatic) verwendet. |
| `adPingInterval` | Ganzzahl | Nein | Häufigkeit der Pings für Anzeigeninhalte in Sekunden. Der Standardwert lautet `10`. Die Werte können zwischen `1` und `10` Sekunden liegen. Wenn kein Wert angegeben ist, wird der Standardwert bei Verwendung von [automatisch verfolgten Sitzungen](../createmediasession.md#automatic) verwendet. |
