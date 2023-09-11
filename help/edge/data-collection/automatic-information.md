---
title: Automatisch erfasste Informationen
description: Eine Übersicht über die Daten, die das Adobe Experience Platform Web SDK automatisch erfasst.
source-git-commit: 89b981104e3cbe597d1556484f4365866bf2a11d
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 32%

---

# Automatisch erfasste Informationen

Das Adobe Experience Platform Web SDK erfasst automatisch einige Informationen standardmäßig. Wenn Ihr Unternehmen diese Daten nicht automatisch erfassen möchte, können Sie die `context` in der [`configure` command](../fundamentals/configuring-the-sdk.md).

Aus der `context` -Array sind nicht in der Datenerfassung enthalten. Wenn die Variable `context` -Array ist im `configure` angegeben ist, werden alle Daten in der unten stehenden Tabelle automatisch erfasst.

| Name | Beschreibung | `context` Array-Keyword | XDM-Pfad | Beispielwert |
| --- | --- | --- | --- | --- |
| Bildschirmhöhe | Die Bildschirmhöhe in Pixel. | `device` | `events[].xdm.device.screenHeight` | `900` |
| Bildschirmbreite | Die Bildschirmbreite in Pixel. | `device` | `events[].xdm.device.screenWidth` | `1440` |
| Bildschirmausrichtung | Die Ausrichtung des Bildschirms. | `device` | `events[].xdm.device.screenOrientation` | `landscape` oder `portrait` |
| Umgebungstyp | Die Art der Umgebung, in der das Erlebnis auftauchte. Adobe Experience Platform Web SDK setzt dieses Feld immer auf `browser`. | `environment` | `events[].xdm.environment.type` | `browser` |
| Viewport-Höhe | Die Höhe des Inhaltsbereichs des Browsers in Pixel. | `environment` | `events[].xdm.environment.browserDetails.viewportHeight` | `679` |
| Viewport-Breite | Die Breite des Inhaltsbereichs des Browsers in Pixel. | `environment` | `events[].xdm.environment.browserDetails.viewportWidth` | `642` |
| SDK-Name | Die SDK-ID. Dieses Feld verwendet einen URI, um die Eindeutigkeit der Kennungen zu verbessern, die von verschiedenen Software-Bibliotheken bereitgestellt werden. Bei Verwendung der eigenständigen Bibliothek lautet der Wert `https://ns.adobe.com/experience/alloy`. Wenn die Bibliothek als Teil der Tag-Erweiterung verwendet wird, lautet der Wert `https://ns.adobe.com/experience/alloy+reactor`. | | `events[].xdm.implementationDetails.name` | `https://ns.adobe.com/experience/alloy` |
| SDK-Version | Wenn die eigenständige Bibliothek verwendet wird, ist der Wert die Bibliotheksversion. Wenn die Bibliothek als Teil der Tag-Erweiterung verwendet wird, ist der Wert eine Verkettung der Bibliotheksversion und Tag-Erweiterungsversion. | | `events[].xdm.implementationDetails.version` | `2.1.0+2.1.3` |
| Umgebung | Die Umgebung, in der die Daten erfasst wurden. Adobe Experience Platform Web SDK setzt dieses Feld immer auf `browser`. | | `events[].xdm.implementationDetails.environment` | `browser` |
| Ortszeit | Lokaler Zeitstempel für den Endnutzer im vereinfachten erweiterten ISO-Format [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6). | `placeContext` | `events[].xdm.placeContext.localTime` | `YYYY-08-07T15:47:17.129-07:00` |
| Lokaler Zeitzonenversatz | Anzahl der Minuten, die der Benutzer von GMT versetzt wird. | `placeContext` | `events[].xdm.placeContext.localTimezoneOffset` | `360` |
| Zeitstempel | Der UTC-Zeitstempel für den Endbenutzer im vereinfachten erweiterten ISO-Format [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6). | Immer eingeschlossen | `events[].xdm.timestamp` | `YYYY-08-07T22:47:17.129Z` |
| URL der aktuellen Seite | Die URL der aktuellen Seite. | `web` | `events[].xdm.web.webPageDetails.URL` | `https://example.com/index.html` |
| Referrer-URL | Die URL der zuvor besuchten Seite. | `web` | `events[].xdm.web.webReferrer.URL` | `http://example.org/linkedpage.html` |

{style="table-layout:auto"}
