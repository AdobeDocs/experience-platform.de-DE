---
title: clickCollection
description: Einstellungen für Klick-Sammlungen optimieren.
exl-id: 5a128b4a-4727-4415-87b4-4ae87a7e1750
source-git-commit: 46c8748e9ab972705b8283c174c285e571acb2ed
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---

# `clickCollection`

Das `clickCollection`-Objekt enthält mehrere Variablen, mit denen Sie automatisch erfasste Linkdaten steuern können. Verwenden Sie diese Variablen, wenn Sie Verknüpfungstypen aus der Datenerfassung ein- oder ausschließen möchten. Sie wird ab Version 2.25.0 von Web SDK unterstützt.

Diese Variable erfordert Folgendes:

* [`clickCollectionEnabled`](clickcollectionenabled.md) muss aktiviert sein.
* Wenn Sie `clickCollection.filterClickDetails` verwenden, muss die veraltete Methode [`onBeforeLinkClickSend`](onbeforelinkclicksend.md) leer sein.
* Die Ereignis-Payload muss zu einem bestimmten Zeitpunkt während des Besuchs des Besuchers einen Wert in `xdm.web.webPageDetails.name` enthalten.

Wenn Ihre Implementierung nicht alle oben genannten Anforderungen erfüllt, hat dieses Objekt keine Auswirkungen.

Die folgenden Eigenschaften sind im `clickCollection`-Objekt verfügbar:

| Eigenschaft | Typ | Beschreibung |
| --- | --- | --- |
| **`internalLinkEnabled`** | `boolean` | Bestimmt, ob Links innerhalb der aktuellen Domain automatisch verfolgt werden. Beispielsweise würde `https://example.com/index.html` an `https://example.com/product.html` als interner Link betrachtet. |
| **`downloadLinkEnabled`** | `boolean` | Bestimmt, ob die Bibliothek Links verfolgt, die sich aufgrund der [`downloadLinkQualifier`](downloadlinkqualifier.md) Eigenschaft als Downloads qualifizieren. |
| **`externalLinkEnabled`** | `boolean` | Bestimmt, ob Links zu externen Domains automatisch verfolgt werden. Beispielsweise würde `https://example.com` an `https://example.net` als externer Link betrachtet. |
| **`eventGroupingEnabled`** | `boolean` | Legt fest, ob die Bibliothek bis zum nächsten Seitenansichtsereignis wartet, um Linktracking-Daten zu senden. Die -Bibliothek betrachtet ein Ereignis als „Seitenansicht“, wenn die folgenden Elemente in der Payload enthalten sind:<ul><li>`xdm.web.webPageDetails.name` enthält einen Zeichenfolgenwert</li><li>`xdm.web.webPageDetails.pageViews.value` ist größer als `0`</li></ul>Wenn das Ereignis „Seitenansicht“ geladen wird, kombiniert die Bibliothek gespeicherte Linktracking-Daten mit dem Rest der Daten in diesem Ereignis. Durch Aktivierung dieser Option wird die Gesamtzahl der Ereignisse reduziert, die Sie an Adobe senden. Wenn `internalLinkEnabled` deaktiviert ist, hat diese Variable keine Auswirkung. |
| **`sessionStorageEnabled`** | `boolean` | Bestimmt, ob Linktracking-Daten im Sitzungsspeicher statt in lokalen Variablen gespeichert werden. Wenn `internalLinkEnabled` oder `eventGroupingEnabled` deaktiviert sind, hat diese Variable keine Auswirkung.<br>Adobe empfiehlt dringend, diese Variable zu aktivieren, wenn `eventGroupingEnabled` außerhalb von Einzelseitenanwendungen verwendet wird. Wenn `eventGroupingEnabled` aktiviert ist, während `sessionStorageEnabled` deaktiviert ist, führt das Klicken auf eine neue Seite zum Verlust von Linktracking-Daten, da diese nicht im Sitzungsspeicher beibehalten werden. Da Single Page Applications normalerweise nicht zu einer neuen Seite navigieren, ist für SPA-Seiten kein Sitzungsspeicher erforderlich. |
| **`filterClickDetails`** | `function` | Eine Rückruffunktion, die vollständige Steuerelemente für die von Ihnen erfassten Linktracking-Daten bereitstellt. Mit dieser Rückruffunktion können Sie das Senden von Linktracking-Daten ändern, verschleiern oder abbrechen. Dieser Rückruf ist nützlich, wenn Sie bestimmte Informationen auslassen möchten, z. B. persönlich identifizierbare Informationen in Links. |

Wenn Sie dieses Objekt nicht im [`configure`](overview.md)-Befehl festlegen, hängen die Standardeinstellungen für dieses Objekt vom Wert von [`clickCollectionEnabled`](clickcollectionenabled.md) ab:

* `internalLinkEnabled`: stimmt überein mit `clickCollectionEnabled`
* `downloadLinkEnabled`: stimmt überein mit `clickCollectionEnabled`
* `externalLinkEnabled`: stimmt überein mit `clickCollectionEnabled`
* `eventGroupingEnabled`: Standardwert ist `false`; muss explizit aktiviert sein
* `sessionStorageEnabled`: Standardwert ist `false`; muss explizit aktiviert sein
* `filterClickDetails`: Enthält keine Funktion; muss explizit registriert werden

>[!TIP]
>
>Adobe empfiehlt, `eventGroupingEnabled` zu aktivieren, wenn `internalLinkEnabled` aktiviert ist, da dadurch die Anzahl der Ereignisse reduziert wird, die für die vertragliche Nutzung zählen.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: true,
  clickCollection: {
    internalLinkEnabled: true,
    downloadLinkEnabled: true,
    externalLinkEnabled: true,
    eventGroupingEnabled: true,
    sessionStorageEnabled: true,
    filterClickDetails: function(content) {
      // If the link is a clickable telephone number, anonymize it
      if(content.linkUrl?.includes("tel:")) {
        content.linkName = content.linkUrl = "Phone number";
      }
      // If the link is an email address, anonymize it
      if(content.linkUrl?.includes("mailto:")) {
        content.linkName = content.linkUrl = "Email address";
      }
    }
  }
});
```

## Konfigurieren der Klick-Sammlung für die Tag-Erweiterung „Web SDK&quot;

Diese Einstellungen können in der Tag-Erweiterung „Web SDK&quot; mithilfe der [Konfigurationseinstellungen für die Datenerfassung“ konfiguriert ](/help/tags/extensions/client/web-sdk/configure/data-collection.md).
