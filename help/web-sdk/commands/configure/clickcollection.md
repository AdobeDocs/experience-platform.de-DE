---
title: clickCollection
description: Optimieren Sie die Einstellungen für die Klicksammlung.
source-git-commit: 660d4e72bd93ca65001092520539a249eae23bfc
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 0%

---


# `clickCollection`

Die `clickCollection` -Objekt enthält mehrere Variablen, mit denen Sie automatisch erfasste Linkdaten steuern können. Verwenden Sie diese Variablen, wenn Sie Link-Typen in die Datenerfassung einbeziehen oder daraus ausschließen möchten.

Sie erfordert [`clickCollectionEnabled`](clickcollectionenabled.md) aktiviert werden.

Es wird auf Web SDK 2.25.0 oder höher unterstützt.

Die folgenden Variablen sind im `clickCollection` -Objekt:

* **`clickCollection.internalLinkEnabled`**: Ein boolescher Wert, der bestimmt, ob Links innerhalb der aktuellen Domäne automatisch verfolgt werden. Beispiel: `https://example.com/index.html` nach `https://example.com/product.html`.
* **`clickCollection.downloadLinkEnabled`**: Ein boolescher Wert, der bestimmt, ob die Bibliothek Links verfolgt, die basierend auf der Variablen [`downloadLinkQualifier`](downloadlinkqualifier.md) -Eigenschaft.
* **`clickCollection.externalLinkEnabled`**: Ein boolescher Wert, der bestimmt, ob Links zu externen Domänen automatisch verfolgt werden. Beispiel: `https://example.com` nach `https://example.net`.
* **`clickCollection.eventGroupingEnabled`**: Ein boolescher Wert, der bestimmt, ob die Bibliothek auf die nächste Seite wartet, um Linktracking-Daten zu senden. Wenn die nächste Seite geladen wird, kombinieren Sie die Linktracking-Daten mit dem Seitenladeereignis. Durch Aktivierung dieser Option wird die Anzahl der Ereignisse reduziert, die Sie an Adobe senden. Wenn `internalLinkEnabled` deaktiviert ist, hat diese Variable keine Auswirkung.
* **`clickCollection.sessionStorageEnabled`**: Ein boolescher Wert, der bestimmt, ob Linktracking-Daten in der Sitzungsspeicherung statt in lokalen Variablen gespeichert werden. Wenn `internalLinkEnabled` oder `eventGroupingEnabled` deaktiviert sind, hat diese Variable keine Auswirkung.

  Adobe empfiehlt dringend, diese Variable zu aktivieren, wenn Sie `eventGroupingEnabled`. Wenn `eventGroupingEnabled` aktiviert ist, während `sessionStorageEnabled` deaktiviert ist, führt das Klicken auf eine neue Seite zum Verlust von Linktracking-Daten, da sie bei der Sitzungsspeicherung nicht beibehalten werden. Auch wenn es zulässig ist, die Option `sessionStorageEnabled` in Einzelseitenanwendungen ist es nicht ideal für SPA Seiten.
* **`filterClickDetails`**: Eine Callback-Funktion, die vollständige Kontrolle über von Ihnen erfasste Linktracking-Daten bietet. Mit dieser Rückruffunktion können Sie Linktracking-Daten ändern, verschleiern oder abbrechen. Dieser Rückruf ist nützlich, wenn Sie bestimmte Informationen weglassen möchten, z. B. persönlich identifizierbare Informationen innerhalb von Links.

## Klicken Sie auf die Sammlungseinstellungen mithilfe der Web SDK-Tag-Erweiterung

Wählen Sie die **[!UICONTROL Aktivieren der Klickdatenerfassung]** Kontrollkästchen, wenn [Konfigurieren der Tag-Erweiterung](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Wenn Sie dieses Kontrollkästchen aktivieren, werden die folgenden Optionen im Zusammenhang mit der Klicksammlung angezeigt:

* [!UICONTROL Interne Links]
   * [!UICONTROL Ereignisgruppierung aktivieren]
   * [!UICONTROL Sitzungsspeicher aktivieren]
* [!UICONTROL Externe Links]
* [!UICONTROL Downloadlinks]
* [!UICONTROL Klickeigenschaften filtern]

1. Anmelden bei [experience.adobe.com](https://experience.adobe.com) mit Ihren Adobe ID-Anmeldedaten.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** Klicken Sie auf **[!UICONTROL Konfigurieren]** auf [!UICONTROL Adobe Experience Platform Web SDK] Karte.
1. Scrollen Sie nach unten zum [!UICONTROL Datenerfassung] und wählen Sie das Kontrollkästchen aus. **[!UICONTROL Aktivieren der Klickdatenerfassung]**.
1. Wählen Sie die gewünschten Einstellungen für die Klicksammlung aus.
1. Klicks **[!UICONTROL Speichern]** und veröffentlichen Sie dann Ihre Änderungen.

Die [!UICONTROL Klickeigenschaften filtern] callback öffnet einen Editor für benutzerdefinierten Code, mit dem Sie den gewünschten Code einfügen können. Im Code-Editor haben Sie Zugriff auf die folgenden Variablen:

* **`content.clickedElement`**: Das angeklickte DOM-Element.
* **`content.pageName`**: Der Seitenname, an dem der Klick stattgefunden hat.
* **`content.linkName`**: Der Name des angeklickten Links.
* **`content.linkRegion`**: Der Bereich des angeklickten Links.
* **`content.linkType`**: Der Typ des Links (Ausstieg, Download oder anderer).
* **`content.linkURL`**: Die Ziel-URL des angeklickten Links.
* **`return true`**: Beenden Sie den Callback sofort mit den aktuellen Variablenwerten.
* **`return false`**: Beenden Sie den Callback sofort und brechen Sie die Datenerfassung ab.

Alle Variablen, die außerhalb von `content` kann verwendet werden, sind aber nicht in der Payload enthalten, die an Adobe gesendet wird.

## Klicken Sie auf Sammlungseinstellungen mithilfe der Web SDK JavaScript-Bibliothek.

Legen Sie die gewünschten Variablen innerhalb der `clickCollection` -Objekt beim Ausführen der [`configure`](overview.md) Befehl. Wenn nicht festgelegt, hängen die Standardeinstellungen für dieses Objekt vom Wert von [`clickCollectionEnabled`](clickcollectionenabled.md).

* `internalLinkEnabled`: Treffer `clickCollectionEnabled`
* `downloadLinkEnabled`: Treffer `clickCollectionEnabled`
* `externalLinkEnabled`: Treffer `clickCollectionEnabled`
* `eventGroupingEnabled`: Standardwert ist `false`; muss explizit aktiviert sein
* `sessionStorageEnabled`: Standardwert ist `false`; muss explizit aktiviert sein
* `filterClickDetails`: Enthält keine Funktion; muss explizit registriert sein.

>[!TIP]
>Adobe empfiehlt die Aktivierung `eventGroupingEnabled`, da dies dazu beiträgt, die Anzahl der Ereignisse zu reduzieren, die für die vertragliche Nutzung angerechnet werden.

```js
alloy("configure", {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
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
