---
title: clickCollection
description: Einstellungen für Klick-Sammlungen optimieren.
exl-id: 5a128b4a-4727-4415-87b4-4ae87a7e1750
source-git-commit: d3be2a9e75514023a7732a1c3460f8695ef02e68
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# `clickCollection`

Das `clickCollection`-Objekt enthält mehrere Variablen, mit denen Sie automatisch erfasste Linkdaten steuern können. Verwenden Sie diese Variablen, wenn Sie Verknüpfungstypen aus der Datenerfassung ein- oder ausschließen möchten.

Dafür muss [`clickCollectionEnabled`](clickcollectionenabled.md) aktiviert sein.

Es wird ab Web SDK 2.25.0 unterstützt.

Die folgenden Variablen sind im `clickCollection`-Objekt verfügbar:

* **`clickCollection.internalLinkEnabled`**: Ein boolescher Wert, der bestimmt, ob Links innerhalb der aktuellen Domain automatisch verfolgt werden. Beispiel: `https://example.com/index.html` auf `https://example.com/product.html`.
* **`clickCollection.downloadLinkEnabled`**: Ein boolescher Wert, der basierend auf der [`downloadLinkQualifier`](downloadlinkqualifier.md)-Eigenschaft bestimmt, ob die Bibliothek Links verfolgt, die als Downloads qualifiziert sind.
* **`clickCollection.externalLinkEnabled`**: Ein boolescher Wert, der bestimmt, ob Links zu externen Domains automatisch verfolgt werden. Beispiel: `https://example.com` auf `https://example.net`.
* **`clickCollection.eventGroupingEnabled`**: Ein boolescher Wert, der bestimmt, ob die Bibliothek bis zur nächsten Seite wartet, um Linktracking-Daten zu senden. Wenn die nächste Seite geladen wird, kombinieren Sie die Linktracking-Daten mit dem Seitenladeereignis. Durch Aktivierung dieser Option wird die Anzahl der Ereignisse, die Sie an Adobe senden, reduziert. Wenn `internalLinkEnabled` deaktiviert ist, hat diese Variable keine Auswirkung.
* **`clickCollection.sessionStorageEnabled`**: Ein boolescher Wert, der bestimmt, ob Linktracking-Daten im Sitzungsspeicher und nicht in lokalen Variablen gespeichert werden. Wenn `internalLinkEnabled` oder `eventGroupingEnabled` deaktiviert sind, hat diese Variable keine Auswirkung.

  Adobe empfiehlt dringend, diese Variable zu aktivieren, wenn `eventGroupingEnabled` außerhalb von Single Page Applications verwendet wird. Wenn `eventGroupingEnabled` aktiviert ist, während `sessionStorageEnabled` deaktiviert ist, führt das Klicken auf eine neue Seite zum Verlust von Linktracking-Daten, da diese nicht im Sitzungsspeicher beibehalten werden. Da Single Page Applications normalerweise nicht zu einer neuen Seite navigieren, ist für SPA-Seiten kein Sitzungsspeicher erforderlich.
* **`filterClickDetails`**: Eine Rückruffunktion, die vollständige Steuerelemente für die von Ihnen erfassten Linktracking-Daten bereitstellt. Mit dieser Rückruffunktion können Sie das Senden von Linktracking-Daten ändern, verschleiern oder abbrechen. Dieser Rückruf ist nützlich, wenn Sie bestimmte Informationen auslassen möchten, z. B. persönlich identifizierbare Informationen in Links.

## Klicken Sie auf Sammlungseinstellungen mithilfe der Tag-Erweiterung „Web SDK&quot;

Wählen Sie beim Konfigurieren der Tag[Erweiterung eine der folgenden Optionen ](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md):

* [!UICONTROL Erfassen interner Links]
   * [!UICONTROL Optionen für die Ereignisgruppierung]:
      * [!UICONTROL Keine Ereignisgruppierung]
      * [!UICONTROL Ereignisgruppierung mithilfe des Sitzungsspeichers]
      * [!UICONTROL Ereignisgruppierung mithilfe eines lokalen Objekts]
* [!UICONTROL Erfassen externer Links]
* [!UICONTROL Downloadlinks erfassen]
* [!UICONTROL Filter - Klickeigenschaften]

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei ](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** und klicken Sie dann auf **[!UICONTROL Konfigurieren]** auf der Karte [!UICONTROL Adobe Experience Platform Web SDK].
1. Scrollen Sie nach unten zum Abschnitt [!UICONTROL Datenerfassung] und wählen Sie dann die gewünschten Einstellungen für Klick-Sammlungen aus.
1. Klicken Sie **[!UICONTROL Speichern]** und veröffentlichen Sie Ihre Änderungen.

Der Rückruf [!UICONTROL Eigenschaften filtern] öffnet einen benutzerdefinierten Code-Editor, mit dem Sie den gewünschten Code einfügen können. Innerhalb des Code-Editors haben Sie Zugriff auf die folgenden Variablen:

* **`content.clickedElement`**: Das angeklickte DOM-Element.
* **`content.pageName`**: Der Seitenname zum Zeitpunkt des Klicks.
* **`content.linkName`**: Der Name des angeklickten Links.
* **`content.linkRegion`**: Die Region des angeklickten Links.
* **`content.linkType`**: Der Link-Typ (Beenden, Herunterladen oder sonstiges).
* **`content.linkURL`**: Die Ziel-URL des angeklickten Links.
* **`return true`**: Sofort den Callback mit den aktuellen Variablenwerten beenden.
* **`return false`**: Sofort den Callback beenden und die Datenerfassung abbrechen.

Alle Variablen, die außerhalb von `content` definiert wurden, können verwendet werden, sind jedoch nicht in der Payload enthalten, die an Adobe gesendet wird.

## Klicken Sie auf Sammlungseinstellungen mithilfe der Web SDK JavaScript-Bibliothek

Legen Sie die gewünschten Variablen im `clickCollection` fest, wenn Sie den [`configure`](overview.md) Befehl ausführen. Wenn nicht festgelegt, hängen die Standardeinstellungen für dieses Objekt vom Wert von [`clickCollectionEnabled`](clickcollectionenabled.md) ab.

* `internalLinkEnabled`: stimmt überein mit `clickCollectionEnabled`
* `downloadLinkEnabled`: stimmt überein mit `clickCollectionEnabled`
* `externalLinkEnabled`: stimmt überein mit `clickCollectionEnabled`
* `eventGroupingEnabled`: Standardwert ist `false`; muss explizit aktiviert sein
* `sessionStorageEnabled`: Standardwert ist `false`; muss explizit aktiviert sein
* `filterClickDetails`: Enthält keine Funktion; muss explizit registriert werden

>[!TIP]
>Adobe empfiehlt, `eventGroupingEnabled` zu aktivieren, wenn `internalLinkEnabled` aktiviert ist, da dies die Anzahl der Ereignisse verringert, die für die vertragliche Nutzung zählen.

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
