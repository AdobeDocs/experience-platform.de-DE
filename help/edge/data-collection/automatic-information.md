---
title: Automatisch erfasste Informationen
seo-title: Informationen, die automatisch vom Adobe Experience Platform Web SDK erfasst werden
description: Beschreibung der von Adobe Experience Cloud SDK automatisch erfassten Informationen
seo-description: Beschreibung der von Adobe Experience Cloud SDK automatisch erfassten Informationen
keywords: Informationen erfassen;Kontext;konfigurieren;Gerät;Bildschirmhöhe;Bildschirmausrichtung;Bildschirmbreite;Bildschirmbreite;Umgebung;ViewportHeight;Viewport-Höhe;Viewport-Breite;Viewport-Breite;Viewport-Breite;Browserdetails;Browserdetails;Implementierungsdetails;Name;Version;OrtContext;localTime;localTimeOffset;LocalTimeOffset Local TimeZone Offset;timestamp;web;url;webPageDetails;Webseitendetails;webReferrer;web Werber;landscape;portrait;
translation-type: tm+mt
source-git-commit: 0928dd3eb2c034fac14d14d6e53ba07cdc49a6ea
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 74%

---


# Automatisch erfasste Informationen

Adobe Experience Platform Web SDK sammelt eine Reihe von Informationen automatisch ohne spezielle Konfiguration. Diese Informationen können jedoch bei Bedarf mit der `context`-Option im `configure`-Befehl deaktiviert werden. Siehe [Konfigurieren des SDK](../fundamentals/configuring-the-sdk.md). Nachstehend eine Liste dieser Informationen. Der Name in Klammern gibt die Zeichenfolge an, die beim Konfigurieren des Kontexts verwendet wird.

## Gerät (`device`)

Informationen zum Gerät. Dies umfasst keine Daten, die Server-seitig von der Benutzeragenten-Zeichenfolge nachgeschlagen werden können.

### Bildschirmhöhe

| **Pfad in Payload:** | **Beispiel:** |
| ---------------------------------- | ------------ |
| `events[].xdm.device.screenHeight` | `900` |

Die Höhe des Bildschirms in Pixel.

### Bildschirmausrichtung

| **Pfad in Payload:** | **Mögliche Werte:** |
| --------------------------------------- | ------------------------- |
| `events[].xdm.device.screenOrientation` | `landscape` oder `portrait` |

Die Ausrichtung des Bildschirms.

### Bildschirmbreite

| **Pfad in Payload:** | **Beispiel:** |
| --------------------------------- | ------------ |
| `events[].xdm.device.screenWidth` | `1440` |

Die Breite des Bildschirms (in Pixel).

## Umgebung (`environment`)

Details zur Browser-Umgebung.

### Umgebungstyp

Browser

| **Pfad in Payload:** | **Beispiel:** |
| ------------------------------- | ------------ |
| `events[].xdm.environment.type` | `browser` |

Die Art der Umgebung, durch die das Erlebnis auftrat. Adobe Experience Platform Web SDK setzt dies immer auf `browser`.

### Viewport-Höhe

| **Pfad in Payload:** | **Beispiel:** |
| -------------------------------------------------------- | ------------ |
| `events[].xdm.environment.browserDetails.viewportHeight` | `679` |

Die Höhe des Inhaltsbereichs des Browsers (in Pixel).

### Viewport-Breite

| **Pfad in Payload:** | **Beispiel:** |
| ------------------------------------------------------- | ------------ |
| `events[].xdm.environment.browserDetails.viewportWidth` | `642` |

Die Breite des Inhaltsbereichs des Browsers (in Pixel).

## Implementierungsdetails

Informationen zum SDK, das zum Erfassen des Ereignisses verwendet wird.

### Name

| **Pfad in Payload:** | **Beispiel:** |
| ----------------------------------------- | --------------------------------------- |
| `events[].xdm.implementationDetails.name` | `https://ns.adobe.com/experience/alloy` |

Die Kennung des Software Development Kits (SDK).  Dieses Feld verwendet einen URI, um die Eindeutigkeit der Kennungen zu verbessern, die von verschiedenen Software-Bibliotheken bereitgestellt werden.

### Version

| **Pfad in Payload:** | **Beispiel:** |
| -------------------------------------------- | ------------ |
| `events[].xdm.implementationDetails.version` | `0.11.0` |

### Umgebung

| **Pfad in Payload:** | **Beispiel:** |
| ------------------------------------------------ | ------------ |
| `events[].xdm.implementationDetails.environment` | `browser` |


## Ortskontext (`placeContext`)

Informationen zum Standort des Endnutzers.

### Ortszeit

| **Pfad in Payload:** | **Beispiel:** |
| ------------------------------------- | ------------------------------- |
| `events[].xdm.placeContext.localTime` | `2019-08-07T15:47:17.129-07:00` |

Lokaler Zeitstempel für den Endnutzer im vereinfachten erweiterten ISO-Format [ISO 8601](https://tools.ietf.org/html/rfc3339#section-5.6).

### Lokaler Zeitzonenversatz

| **Pfad in Payload:** | **Beispiel:** |
| ----------------------------------------------- | ------------ |
| `events[].xdm.placeContext.localTimezoneOffset` | `360` |

Anzahl der Minuten, die der Nutzer von der GMT-Zeitzone versetzt ist.

## Zeitstempel

| **Pfad in Payload:** | **Beispiel:** |
| ------------------------ | -------------------------- |
| `events[].xdm.timestamp` | `2019-08-07T22:47:17.129Z` |

Der Zeitstempel des Ereignisses.  Diese Kontextinformation kann nicht entfernt werden.

UTC-Zeitstempel für den Endnutzer in vereinfachtem erweiterten ISO-Format [ISO 8601](https://tools.ietf.org/html/rfc3339#section-5.6).

## Web-Details (`web`)

Details zur Seite, auf der sich der Nutzer befindet.

### URL der aktuellen Seite

| **Pfad in Payload:** | **Beispiel:** |
| ------------------------------------- | ------------------------------------ |
| `events[].xdm.web.webPageDetails.URL` | `https://somesite.com/somepage.html` |

Die URL der aktuellen Seite.

### Referrer-URL

| **Pfad in Payload:** | **Beispiel:** |
| ---------------------------------- | ----------------------------------------- |
| `events[].xdm.web.webReferrer.URL` | `http://somereferrer.com/linkedpage.html` |

Die URL der zuvor besuchten Seite.
