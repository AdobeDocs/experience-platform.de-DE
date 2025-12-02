---
title: Kontext
description: Automatische Erfassung von Geräte-, Umgebungs- oder Standortdaten.
exl-id: 911cabec-2afb-4216-b413-80533f826b0e
source-git-commit: c2564f1b9ff036a49c9fa4b9e9ffbdbc598a07a8
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 14%

---

# `context`

Die `context`-Eigenschaft ist ein Array von Zeichenfolgen, das bestimmt, was die Web-SDK automatisch erfassen kann. Diese Daten können zwar einen großen Wert bieten, doch das Auslassen einiger dieser Daten kann von Vorteil sein, damit Sie die Datenschutzrichtlinien Ihrer Organisation einhalten können.

## Kontextschlüsselwörter und XDM-Elemente

Wenn Sie ein bestimmtes Kontextschlüsselwort einbeziehen, füllt Web SDK automatisch alle zugehörigen XDM-Elemente. Wenn Sie ein bestimmtes XDM-Element auslassen möchten, während Sie andere zulassen, können Sie Werte mithilfe von [`onBeforeEventSend`](onbeforeeventsend.md) löschen. Wenn Sie mehrere Ereignisse auf einer Seite senden, enthält Web SDK diese Felder bei jedem `SendEvent`.

### Web

Das `"web"`-Schlüsselwort erfasst Informationen über die aktuelle Seite.

| Dimension | Beschreibung | XDM-Pfad | Beispielwert |
| --- | --- | --- | --- |
| „Seiten-URL“ | Die URL der aktuellen Seite. | `xdm.web.webPageDetails.URL` | `https://example.com/index.html` |
| Referrer-URL | Die URL der zuvor besuchten Seite. | `xdm.web.webReferrer.URL` | `http://example.org/linkedpage.html` |

### Gerät

Das `"device"`-Schlüsselwort erfasst Informationen über das Gerät des Benutzers.

| Dimension | Beschreibung | XDM-Pfad | Beispielwert |
| --- | --- | --- | --- |
| Bildschirmhöhe | Die Bildschirmhöhe in Pixel. | `xdm.device.screenHeight` | `900` |
| Bildschirmbreite | Die Bildschirmbreite in Pixel. | `xdm.device.screenWidth` | `1440` |
| Bildschirmausrichtung | Die Ausrichtung des Bildschirms. | `xdm.device.screenOrientation` | `landscape` oder `portrait` |

### Umgebung

Das `"environment"`-Schlüsselwort erfasst Informationen über den Browser des Benutzers.

| Dimension | Beschreibung | XDM-Pfad | Beispielwert |
| --- | --- | --- | --- |
| Umgebungstyp | Der Typ der Umgebung, in der das Erlebnis angezeigt wird. Web SDK legt dieses Feld immer auf `browser` fest. | `xdm.environment.type` | `browser` |
| Viewport-Höhe | Die Höhe des Inhaltsbereichs des Browsers in Pixel. | `xdm.environment.browserDetails.viewportHeight` | `679` |
| Viewport-Breite | Die Breite des Inhaltsbereichs des Browsers in Pixel. | `xdm.environment.browserDetails.viewportWidth` | `642` |

### Ortskontext

Das `"placeContext"`-Schlüsselwort erfasst Informationen zum Standort des Benutzers.

| Dimension | Beschreibung | XDM-Pfad | Beispielwert |
| --- | --- | --- | --- |
| Ortszeit | Lokaler Zeitstempel für den Endbenutzer im vereinfachten erweiterten [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6)Format. | `xdm.placeContext.localTime` | `YYYY-08-07T15:47:17.129-07:00` |
| Lokaler Zeitzonenversatz | Die Anzahl der Minuten, die die Benutzerin oder der Benutzer von GMT versetzt wird. | `xdm.placeContext.localTimezoneOffset` | `360` |
| Ländercode | Der Länder-Code des Endbenutzers. | `xdm.placeContext.geo.countryCode` | `US` |
| Bundesland | Der Bundesland-Provinzcode des Endbenutzers. | `xdm.placeContext.geo.stateProvince` | `CA` |
| Breitengrad | Der Breitengrad des Endbenutzerstandorts. | `xdm.placeContext.geo._schema.latitude` | `37.3307447` |
| Längengrad | Der Längengrad des Endbenutzerstandorts. | `xdm.placeContext.geo._schema.longitude` | `-121.8945965` |

### Zeitstempel

Das `"timestamp"`-Schlüsselwort erfasst Informationen zum Zeitstempel des Ereignisses. Dieser Kontext ist immer eingeschlossen und kann nicht entfernt werden.

| Dimension | Beschreibung | XDM-Pfad | Beispielwert |
| --- | --- | --- | --- |
| Zeitstempel des Ereignisses | UTC-Zeitstempel für den Endbenutzer im vereinfachten erweiterten [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6)-Format. | `xdm.timestamp` | `YYYY-08-07T22:47:17.129Z` |

### Implementierungsdetails

Das `implementationDetails`-Schlüsselwort erfasst Informationen über die SDK-Version, die zum Erfassen des Ereignisses verwendet wird.

| Dimension | Beschreibung | XDM-Pfad | Beispielwert |
| --- | --- | --- | --- |
| Name | Kennung des Software Development Kits (SDK). Dieses Feld verwendet einen URI, um die Eindeutigkeit der Kennungen zu verbessern, die von verschiedenen Software-Bibliotheken bereitgestellt werden. | `xdm.implementationDetails.name` | Wenn die eigenständige Bibliothek verwendet wird, wird der Wert `https://ns.adobe.com/experience/alloy`. Wenn die Bibliothek als Teil der Tag-Erweiterung verwendet wird, wird der Wert `https://ns.adobe.com/experience/alloy+reactor`. |
| Version | Die Version des Software Development Kit (SDK). | `xdm.implementationDetails.version` | Wenn die eigenständige Bibliothek verwendet wird, ist der Wert die Bibliotheksversion. Wenn die Bibliothek als Teil der Tag-Erweiterung verwendet wird, ist der Wert die Bibliotheksversion und die Tag-Erweiterungsversion, die mit einem `+` verbunden ist. Wenn beispielsweise die Bibliotheksversion `2.1.0` und die Tag-Erweiterungsversion `2.1.3` ist, würde der Wert `2.1.0+2.1.3`. |
| Umgebung | Die Umgebung, in der die Daten erfasst wurden. Dieses Feld ist bei Verwendung der JavaScript-Bibliothek immer auf `browser` festgelegt. | `xdm.implementationDetails.environment` | `browser` |

### Client-Hinweise mit hoher Entropie {#high-entropy-client-hints}

Das `"highEntropyUserAgentHints"`-Schlüsselwort erfasst detaillierte Informationen über das Gerät des Benutzers. Diese Daten sind im HTTP-Header der an Adobe gesendeten Anfrage enthalten. Nachdem die Daten an das Edge-Netzwerk gesendet wurden, füllt das XDM-Objekt den entsprechenden XDM-Pfad. Wenn Sie den entsprechenden XDM-Pfad in Ihrem `sendEvent`-Aufruf festlegen, hat dieser Vorrang vor dem HTTP-Header-Wert.

Wenn Sie bei der [ Ihres Datenstroms Gerätesuchen verwenden](/help/datastreams/configure.md) können Daten zugunsten von Gerätesuchwerten gelöscht werden. Einige Client-Hinweisfelder und Gerätesuchfelder können nicht im selben Treffer vorhanden sein.

| Eigenschaft | Beschreibung | HTTP-Kopfzeile | XDM-Pfad | Beispiel |
| --- | --- | --- | --- | --- |
| Betriebssystemversion | Die Version des Betriebssystems | `Sec-CH-UA-Platform-Version` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.platformVersion` | `10.15.7` |
| Architektur | Die zugrunde liegende CPU-Architektur. | `Sec-CH-UA-Arch` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.architecture` | `x86` |
| Gerätemodell | Der Name des verwendeten Geräts. | `Sec-CH-UA-Model` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.model` | `Intel Mac OS X 10_15_7` |
| Bitness | Die Anzahl der Bits, die von der zugrunde liegenden CPU-Architektur unterstützt werden. | `Sec-CH-UA-Bitness` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.bitness` | `64` |
| Browser-Anbieter | Das Unternehmen, das den Browser erstellt hat. Der Hinweis `Sec-CH-UA` niedrige Entropie erfasst auch dieses Element. | `Sec-CH-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.vendor` | `Google` |
| Browser-Name | Der verwendete Browser. Der Hinweis `Sec-CH-UA` niedrige Entropie erfasst auch dieses Element. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.brand` | `Chrome` |
| Browser-Version | Die Hauptversion des Browsers. Der Hinweis `Sec-CH-UA` niedrige Entropie erfasst auch dieses Element. Die genaue Browser-Version wird nicht automatisch erfasst. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.version` | `105` |

Weitere Informationen finden [ unter ](/help/collection/use-cases/client-hints.md)-Client-Hinweise für Benutzeragenten .

Legen Sie das `context` Array von Zeichenfolgen beim Ausführen des `configure`-Befehls fest. Wenn Sie diese Eigenschaft beim Konfigurieren der SDK weglassen, werden standardmäßig alle Kontextinformationen mit Ausnahme von `"highEntropyUserAgentHints"` erfasst. Legen Sie diese Eigenschaft fest, wenn Sie Client-Hinweise mit hoher Entropie erfassen möchten oder wenn Sie andere Kontextinformationen bei der Datenerfassung weglassen möchten. Zeichenfolgen können in beliebiger Reihenfolge eingefügt werden.

>[!NOTE]
>
>Wenn Sie alle Kontextinformationen erfassen möchten, einschließlich Client-Hinweisen mit hoher Entropie, müssen Sie jeden Wert in die `context` Array-Zeichenfolge aufnehmen. Beim standardmäßigen `context`-Wert werden `highEntropyUserAgentHints` ausgelassen und wenn Sie die `context`-Eigenschaft festlegen, werden bei allen ausgelassenen Werten keine Daten erfasst.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  context: ["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"]
});
```

## Erfassen von Kontextinformationen mithilfe der Tag-Erweiterung „Web SDK&quot;

Siehe [Kontexteinstellungen](/help/tags/extensions/client/web-sdk/configure/data-collection.md#context-settings) unter Datenerfassungskonfigurationseinstellungen in der Dokumentation zu Web SDK-Tag-Erweiterungen.
