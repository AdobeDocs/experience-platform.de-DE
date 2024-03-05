---
title: context
description: Automatisch Geräte-, Umgebungs- oder Standortdaten erfassen.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 13%

---

# `context`

Die `context` -Eigenschaft ist ein Array von Zeichenfolgen, die bestimmen, was das Web SDK automatisch erfassen kann. Diese Daten können zwar einen großen Wert bieten, es kann jedoch von Vorteil sein, einige dieser Daten wegzulassen, damit Sie die Datenschutzrichtlinien Ihres Unternehmens einhalten können.

## Kontextbegriffe und XDM-Elemente

Wenn Sie einen bestimmten Kontextschlüsselwort angeben, füllt das Web SDK automatisch alle zugehörigen XDM-Elemente. Wenn Sie ein bestimmtes XDM-Element weglassen und andere zulassen möchten, können Sie Werte mithilfe von [`onBeforeEventSend`](onbeforeeventsend.md). Wenn Sie mehrere Ereignisse auf einer Seite senden, enthält das Web SDK diese Felder auf jeder `SendEvent` aufrufen.

### Web

Die `"web"` erfasst Informationen über die aktuelle Seite.

| Dimension | Beschreibung | XDM-Pfad | Beispielwert |
| --- | --- | --- | --- |
| „Seiten-URL“ | Die URL der aktuellen Seite. | `xdm.web.webPageDetails.URL` | `https://example.com/index.html` |
| Referrer-URL | Die URL der zuvor besuchten Seite. | `xdm.web.webReferrer.URL` | `http://example.org/linkedpage.html` |

{style="table-layout:auto"}

### Gerät

Die `"device"` erfasst Informationen über das Gerät des Benutzers.

| Dimension | Beschreibung | XDM-Pfad | Beispielwert |
| --- | --- | --- | --- |
| Bildschirmhöhe | Die Bildschirmhöhe in Pixel. | `xdm.device.screenHeight` | `900` |
| Bildschirmbreite | Die Bildschirmbreite in Pixel. | `xdm.device.screenWidth` | `1440` |
| Bildschirmausrichtung | Die Ausrichtung des Bildschirms. | `xdm.device.screenOrientation` | `landscape` oder `portrait` |

{style="table-layout:auto"}

### Umgebung

Die `"environment"` erfasst Informationen zum Browser des Benutzers.

| Dimension | Beschreibung | XDM-Pfad | Beispielwert |
| --- | --- | --- | --- |
| Umgebungstyp | Die Art der Umgebung, in der das Erlebnis auftauchte. Das Web SDK setzt dieses Feld immer auf `browser`. | `xdm.environment.type` | `browser` |
| Viewport-Höhe | Die Höhe des Inhaltsbereichs des Browsers in Pixel. | `xdm.environment.browserDetails.viewportHeight` | `679` |
| Viewport-Breite | Die Breite des Inhaltsbereichs des Browsers in Pixel. | `xdm.environment.browserDetails.viewportWidth` | `642` |

{style="table-layout:auto"}

### Ortskontext

Die `"placeContext"` erfasst Informationen zum Standort des Benutzers.

| Dimension | Beschreibung | XDM-Pfad | Beispielwert |
| --- | --- | --- | --- |
| Ortszeit | Lokaler Zeitstempel für den Endbenutzer in vereinfachtem erweiterten [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6) Format. | `xdm.placeContext.localTime` | `YYYY-08-07T15:47:17.129-07:00` |
| Lokaler Zeitzonenversatz | Die Anzahl der Minuten, die der Benutzer von GMT versetzt wird. | `xdm.placeContext.localTimezoneOffset` | `360` |

{style="table-layout:auto"}

### Hohe Entropie-Client-Hinweise

Die `"highEntropyUserAgentHints"` erfasst detaillierte Informationen zum Gerät des Benutzers. Diese Daten sind im HTTP-Header der an Adobe gesendeten Anfrage enthalten. Nachdem die Daten im Edge-Netzwerk eintreffen, füllt das XDM-Objekt den entsprechenden XDM-Pfad. Wenn Sie den entsprechenden XDM-Pfad in der `sendEvent` aufrufen, hat er Vorrang vor dem HTTP-Header-Wert.

Wenn Sie die Gerätesuche verwenden, wenn [Konfigurieren Ihres Datenspeichers](/help/datastreams/configure.md), können Daten zugunsten von Gerätesuchwerten gelöscht werden. Einige Clienthinweisfelder und Geräte-Suchfelder können nicht im selben Treffer vorhanden sein.

| Dimension | Beschreibung | HTTP-Header | XDM-Pfad | Beispielwert |
| --- | --- | --- | --- | --- |
| Version des Betriebssystems | Die Betriebssystemversion. | `Sec-CH-UA-Platform-Version` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.platformVersion` | |
| Architektur | Die zugrunde liegende CPU-Architektur. | `Sec-CH-UA-Arch` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.architecture` | |
| Gerätemodell | Der Name des verwendeten Geräts. | `Sec-CH-UA-Model` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.model` | |
| Bitness | Die Anzahl der Bit, die die zugrunde liegende CPU-Architektur unterstützt. | `Sec-CH-UA-Bitness` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.bitness` | |
| Browser-Anbieter | Das Unternehmen, das den Browser erstellt hat. Der niedrige Entropiehinweis `Sec-CH-UA` erfasst auch dieses Element. | `Sec-CH-UA-Full-Version-List` | | |
| Browsername | Der verwendete Browser. Der niedrige Entropiehinweis `Sec-CH-UA` erfasst auch dieses Element. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.brand` | |
| Browserversion | Die signifikante Version des Browsers. Der niedrige Entropiehinweis `Sec-CH-UA` erfasst auch dieses Element. Die genaue Browserversion wird nicht automatisch erfasst. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.version` | |

{style="table-layout:auto"}

## Erfassen von Kontextinformationen mithilfe der Web SDK-Tag-Erweiterung

Die Einstellung für Kontextinformationen ist eine Kombination aus Optionsfeldern und Kontrollkästchen, wenn [Konfigurieren der Tag-Erweiterung](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Jedes Kontrollkästchen wird einem Kontextschlüsselwort zugeordnet.

1. Anmelden bei [experience.adobe.com](https://experience.adobe.com) mit Ihren Adobe ID-Anmeldedaten.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** Klicken Sie auf **[!UICONTROL Konfigurieren]** auf [!UICONTROL Adobe Experience Platform Web SDK] Karte.
1. Scrollen Sie nach unten zum [!UICONTROL Datenerfassung] und wählen Sie entweder **[!UICONTROL Alle standardmäßigen Kontextinformationen]** oder **[!UICONTROL Spezifische Kontextdaten]**.
1. Wenn Sie **[!UICONTROL Spezifische Kontextdaten]** aktivieren Sie das Kontrollkästchen neben jedem gewünschten Kontextdatenelement.
1. Klicks **[!UICONTROL Speichern]** und veröffentlichen Sie dann Ihre Änderungen.

## Kontextdaten mit der JavaScript-Bibliothek des Web SDK erfassen

Legen Sie die `context` Zeichenfolgen-Array beim Ausführen der `configure` Befehl. Wenn Sie diese Eigenschaft beim Konfigurieren des SDK weglassen, werden alle Kontextinformationen außer `"highEntropyUserAgentHints"` wird standardmäßig erfasst. Legen Sie diese Eigenschaft fest, wenn Sie Client-Hinweise mit hoher Entropie erfassen möchten oder wenn Sie andere Kontextinformationen aus der Datenerfassung auslassen möchten. Zeichenfolgen können in beliebiger Reihenfolge eingefügt werden.

>[!NOTE]
>
>Wenn Sie alle Kontextinformationen, einschließlich Client-Hinweisen mit hoher Entropie, erfassen möchten, müssen Sie jeden Wert in die `context` Array-Zeichenfolge. Die Standardeinstellung `context` Wert omits `highEntropyUserAgentHints`und wenn Sie die `context` -Eigenschaft, werden keine Daten von ausgesetzten Werten erfasst.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "context": ["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"]
});
```
