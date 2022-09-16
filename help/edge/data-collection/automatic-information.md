---
title: Automatisch erfasste Informationen im Adobe Experience Platform Web SDK
description: Eine Übersicht über die einzelnen Informationen, die das Adobe Experience Platform SDK automatisch erfasst.
keywords: Informationen erfassen;Kontext;Konfigurieren;Gerät;Bildschirmhöhe;Bildschirmhöhe;Bildschirmausrichtung;Bildschirmausrichtung;Bildschirmbreite;Bildschirmbreite;Umgebung;ViewportHeight;Viewport-Höhe;ViewportWidth;Viewport-Breite;Browserdetails;Browserdetails;Implementierungsdetails;Implementierungsdetails;Name;Version;Ortszeit;localTime;localZoneOffset;local Zeitzonenversatz;Zeitstempel;Web;url;webPageDetails;Web-Seitendetails;webReferrer;Web Referrer;landscape;Hochformat;
exl-id: 901df786-df36-4986-9c74-a32d29c11b71
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 59%

---

# Automatisch erfasste Informationen

Das Adobe Experience Platform Web SDK sammelt eine Reihe von Informationen automatisch ohne spezielle Konfiguration. Diese Informationen können jedoch bei Bedarf mit der `context`-Option im `configure`-Befehl deaktiviert werden. Siehe [Konfigurieren des SDK](../fundamentals/configuring-the-sdk.md). Nachstehend eine Liste dieser Informationen. Der Name in Klammern gibt die Zeichenfolge an, die beim Konfigurieren des Kontexts verwendet wird.

## Gerät (`device`)

Informationen zum Gerät. Dies umfasst keine Daten, die Server-seitig von der Benutzeragenten-Zeichenfolge nachgeschlagen werden können.

### Bildschirmhöhe

| **Pfad in Payload:** | **Beispiel:** |
| ---------------------------------- | ------------ |
| `events[].xdm.device.screenHeight` | `900` |

Die Höhe des Bildschirms (in Pixel).

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

Die Art der Umgebung, in der das Erlebnis auftauchte. Adobe Experience Platform Web SDK setzt dies immer auf `browser`.

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

Die Kennung des Software Development Kits (SDK).  Dieses Feld verwendet einen URI, um die Eindeutigkeit der Kennungen zu verbessern, die von verschiedenen Software-Bibliotheken bereitgestellt werden. Wenn die eigenständige Bibliothek verwendet wird, lautet der Wert `https://ns.adobe.com/experience/alloy`. Wenn die Bibliothek als Teil der Tag-Erweiterung verwendet wird, lautet der Wert `https://ns.adobe.com/experience/alloy+reactor`.

### Version

| **Pfad in Payload:** | **Beispiel:** |
| -------------------------------------------- | ------------ |
| `events[].xdm.implementationDetails.version` | `0.11.0` |

Wenn die eigenständige Bibliothek verwendet wird, ist der Wert einfach die Bibliotheksversion. Wenn die Bibliothek als Teil der Tag-Erweiterung verwendet wird, ist dies die Bibliotheksversion und die Tag-Erweiterungsversion mit einem &quot;+&quot;verbunden. Wenn die Bibliotheksversion beispielsweise 2.1.0 wäre und die Tag-Erweiterungsversion 2.1.3 wäre, wäre der Wert `2.1.0+2.1.3`.

### Umgebung

| **Pfad in Payload:** | **Beispiel:** |
| ------------------------------------------------ | ------------ |
| `events[].xdm.implementationDetails.environment` | `browser` |

Die Umgebung, in der die Daten erfasst wurden. Dies ist immer auf `browser`.

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
