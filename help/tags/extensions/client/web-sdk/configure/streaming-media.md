---
title: Konfigurationseinstellungen für Streaming-Medien
description: Passen Sie an, wie die Tag-Erweiterung „Web SDK" Streaming-Mediendaten erfasst.
source-git-commit: 46e5d007b27eaa67c9ee49e35a711424de383d68
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 4%

---

# Konfigurationseinstellungen für Streaming-Medien

Mit der Mediensammlungsfunktion können Sie Daten im Zusammenhang mit Mediensitzungen erfassen, z. B. Medienwiedergaben, Pausen, Beendigungen und andere verwandte Ereignisse. Nach der Erfassung können Sie diese Daten an Adobe Experience Platform oder Adobe Analytics senden, um Berichte zu generieren. Diese Funktion bietet eine umfassende Lösung zum Tracking und zum Verständnis des Medienkonsumverhaltens auf Ihrer Website.

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei ](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Extensions]** und wählen Sie **[!UICONTROL Configure]** auf der [!UICONTROL Adobe Experience Platform Web SDK] aus.
1. Scrollen Sie nach unten zum Abschnitt **[!UICONTROL Streaming media]** .

![Bild mit den Mediensammlungseinstellungen der Web-SDK-Tag-Erweiterung in der Tags-Benutzeroberfläche](../assets/media-collection.png)

## Voraussetzungen

Um die Streaming-Medienkomponente der Web-SDK verwenden zu können, müssen Sie die folgenden Voraussetzungen erfüllen:

* Stellen Sie sicher, dass Sie Zugriff auf Adobe Experience Platform oder Adobe Analytics haben.
* Aktivieren Sie die Option **[[!UICONTROL Media Analytics]](/help/datastreams/configure.md#advanced-options)** für den verwendeten Datenstrom.
* Stellen Sie sicher, dass das von Ihrem Datenstrom verwendete Schema die Schemafelder der Mediensammlung enthält.
* Konfigurieren Sie die Funktion für Streaming-Medien in der Tag-Erweiterung von Web SDK, wie auf dieser Seite gezeigt.

## [!UICONTROL Channel]

Der Name des Kanals, in dem die Mediensammlung stattfindet. Beispiel: `Video channel`. Jeder Zeichenfolgenwert ist gültig.

## [!UICONTROL Player Name]

Der Name des Medien-Players, den Ihre Eigenschaft für die Medienwiedergabe verwendet.

## [!UICONTROL Application Version]

Die Version der Media Player-Anwendung, die Ihre Eigenschaft für die Medienwiedergabe verwendet.

## [!UICONTROL Main ping interval]

Die Häufigkeit von Pings für den Hauptinhalt in Sekunden. Der Standardwert lautet `10`. Die Werte können zwischen `10` und `50` Sekunden liegen. Wenn kein Wert angegeben ist, wird der Standardwert bei der Verwendung von [automatisch verfolgten Sitzungen](/help/collection/js/commands/createmediasession.md#automatic) verwendet.

## [!UICONTROL Ad ping interval]

Die Häufigkeit von Pings für Anzeigeninhalte in Sekunden. Der Standardwert lautet `10`. Die Werte können zwischen `1` und `10` Sekunden liegen. Wenn kein Wert angegeben ist, wird der Standardwert bei der Verwendung von [automatisch verfolgten Sitzungen](/help/collection/js/commands/createmediasession.md#automatic) verwendet.
