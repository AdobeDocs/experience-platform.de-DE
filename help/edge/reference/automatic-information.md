---
title: Automatisch erfasste Informationen
seo-title: Informationen, die automatisch vom Adobe Experience Platform Web SDK erfasst werden
description: Beschreibung der einzelnen Informationen, die das Adobe Experience Cloud SDK automatisch erfasst
seo-description: Beschreibung der einzelnen Informationen, die das Adobe Experience Cloud SDK automatisch erfasst
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (Beta) Informationen automatisch erfasst

>[!IMPORTANT]
>
>Das Adobe Experience Platform Web SDK befindet sich derzeit in der Betaphase und steht nicht allen Benutzern zur Verfügung. Dokumentation und Funktionalität können sich ändern.

Das Adobe Experience Cloud-SDK sammelt eine Reihe von Informationen automatisch ohne spezielle Konfiguration. Diese Informationen können jedoch bei Bedarf mit der `context` Option im `configure` Befehl deaktiviert werden. [Siehe Konfigurieren des SDK](../fundamentals/configuring-the-sdk.md). Unten sehen Sie eine Liste dieser Informationen. Der Name in Klammern gibt die Zeichenfolge an, die beim Konfigurieren des Kontexts verwendet wird.

## Gerät (`device`)

Informationen zum Gerät. Dies umfasst keine Daten, die serverseitig von der Benutzeragenten-Zeichenfolge nachgeschlagen werden können.

### Bildschirmhöhe

| **Pfad in Nutzlast:** | **Beispiel:** |
| ---------------------------------- | ------------ |
| `events[].xdm.device.screenHeight` | `900` |

Die Höhe des Bildschirms in Pixel.

### Bildschirmausrichtung

| **Pfad in Nutzlast:** | **Mögliche Werte:** |
| --------------------------------------- | ------------------------- |
| `events[].xdm.device.screenOrientation` | `landscape` oder `portrait` |

Die Ausrichtung des Bildschirms.

### Bildschirmbreite

| **Pfad in Nutzlast:** | **Beispiel:** |
| --------------------------------- | ------------ |
| `events[].xdm.device.screenWidth` | `1440` |

Die Breite des Bildschirms (in Pixel).

## Umgebung (`environment`)

Details zur Browser-Umgebung.

### Umgebung

Browser

| **Pfad in Nutzlast:** | **Beispiel:** |
| ------------------------------- | ------------ |
| `events[].xdm.environment.type` | `browser` |

Die Art der Umgebung, mit der das Erlebnis aufgetaucht wurde. Das Adobe Experience Platform SDK for JavaScript wird immer eingestellt `browser`.

### Viewport-Höhe

| **Pfad in Nutzlast:** | **Beispiel:** |
| -------------------------------------------------------- | ------------ |
| `events[].xdm.environment.browserDetails.viewportHeight` | `679` |

Die Höhe des Inhaltsbereichs des Browsers (in Pixel).

### Viewport-Breite

| **Pfad in Nutzlast:** | **Beispiel:** |
| ------------------------------------------------------- | ------------ |
| `events[].xdm.environment.browserDetails.viewportWidth` | `642` |

Die Breite des Inhaltsbereichs des Browsers (in Pixel).

## Implementierungsdetails

Informationen zum SDK, das zum Erfassen des Ereignisses verwendet wird.

### Name

| **Pfad in Nutzlast:** | **Beispiel:** |
| ----------------------------------------- | --------------------------------------- |
| `events[].xdm.implementationDetails.name` | `https://ns.adobe.com/experience/alloy` |

Die Kennung des Software Development Kits (SDK).  Dieses Feld verwendet einen URI, um die Eindeutigkeit der Bezeichner zu verbessern, die von verschiedenen Softwarebibliotheken bereitgestellt werden.

### Version

| **Pfad in Nutzlast:** | **Beispiel:** |
| -------------------------------------------- | ------------ |
| `events[].xdm.implementationDetails.version` | `0.11.0` |

## Kontext platzieren (`placeContext`)

Informationen zum Speicherort des Endbenutzers.

### Ortszeit

| **Pfad in Nutzlast:** | **Beispiel:** |
| ------------------------------------- | ------------------------------- |
| `events[].xdm.placeContext.localTime` | `2019-08-07T15:47:17.129-07:00` |

Lokaler Zeitstempel für den Endbenutzer im vereinfachten erweiterten ISO-Format [ISO 8601](https://tools.ietf.org/html/rfc3339#section-5.6).

### Lokaler Zeitzonenversatz

| **Pfad in Nutzlast:** | **Beispiel:** |
| ----------------------------------------------- | ------------ |
| `events[].xdm.placeContext.localTimezoneOffset` | `360` |

Anzahl der Minuten, in denen der Benutzer vom GMT-Wert versetzt wird.

## Zeitstempel

| **Pfad in Nutzlast:** | **Beispiel:** |
| ------------------------ | -------------------------- |
| `events[].xdm.timestamp` | `2019-08-07T22:47:17.129Z` |

Der Zeitstempel des Ereignisses.  Dieser Teil des Kontexts kann nicht entfernt werden.

UTC-Zeitstempel für den Endbenutzer in vereinfachtem erweiterten ISO-Format [ISO 8601](https://tools.ietf.org/html/rfc3339#section-5.6).

## Webdetails (`web`)

Details zur Seite, auf der sich der Benutzer befindet.

### Aktuelle Seiten-URL

| **Pfad in Nutzlast:** | **Beispiel:** |
| ------------------------------------- | ------------------------------------ |
| `events[].xdm.web.webPageDetails.URL` | `https://somesite.com/somepage.html` |

Die URL der aktuellen Seite.

### Werber-URL

| **Pfad in Nutzlast:** | **Beispiel:** |
| ---------------------------------- | ----------------------------------------- |
| `events[].xdm.web.webReferrer.URL` | `http://somereferrer.com/linkedpage.html` |

Die URL der vorherigen besuchten Seite.
