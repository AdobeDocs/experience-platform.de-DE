---
title: clickCollection
description: Optimieren Sie die Einstellungen für die Klicksammlung.
exl-id: 5a128b4a-4727-4415-87b4-4ae87a7e1750
source-git-commit: d3be2a9e75514023a7732a1c3460f8695ef02e68
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# `clickCollection`

Das Objekt `clickCollection` enthält mehrere Variablen, mit denen Sie automatisch erfasste Linkdaten steuern können. Verwenden Sie diese Variablen, wenn Sie Link-Typen in die Datenerfassung einbeziehen oder daraus ausschließen möchten.

Dafür muss [`clickCollectionEnabled`](clickcollectionenabled.md) aktiviert sein.

Es wird auf Web SDK 2.25.0 oder höher unterstützt.

Die folgenden Variablen sind im Objekt `clickCollection` verfügbar:

* **`clickCollection.internalLinkEnabled`**: Ein boolescher Wert, der bestimmt, ob Links innerhalb der aktuellen Domäne automatisch verfolgt werden. Beispiel: `https://example.com/index.html` bis `https://example.com/product.html`.
* **`clickCollection.downloadLinkEnabled`**: Ein boolescher Wert, der bestimmt, ob die Bibliothek Links verfolgt, die basierend auf der Eigenschaft [`downloadLinkQualifier`](downloadlinkqualifier.md) als Downloads gelten.
* **`clickCollection.externalLinkEnabled`**: Ein boolescher Wert, der bestimmt, ob Links zu externen Domänen automatisch verfolgt werden. Beispiel: `https://example.com` bis `https://example.net`.
* **`clickCollection.eventGroupingEnabled`**: Ein boolescher Wert, der bestimmt, ob die Bibliothek auf die nächste Seite wartet, um Linktracking-Daten zu senden. Wenn die nächste Seite geladen wird, kombinieren Sie die Linktracking-Daten mit dem Seitenladeereignis. Durch Aktivierung dieser Option wird die Anzahl der Ereignisse reduziert, die Sie an Adobe senden. Wenn `internalLinkEnabled` deaktiviert ist, hat diese Variable keine Auswirkung.
* **`clickCollection.sessionStorageEnabled`**: Ein boolescher Wert, der bestimmt, ob Linktracking-Daten in der Sitzungsspeicherung statt in lokalen Variablen gespeichert werden. Wenn `internalLinkEnabled` oder `eventGroupingEnabled` deaktiviert sind, hat diese Variable keine Auswirkung.

  Adobe empfiehlt dringend, diese Variable zu aktivieren, wenn `eventGroupingEnabled` außerhalb von Einzelseitenanwendungen verwendet wird. Wenn `eventGroupingEnabled` aktiviert ist, während `sessionStorageEnabled` deaktiviert ist, führt das Klicken auf eine neue Seite zum Verlust von Linktracking-Daten, da sie im Sitzungsspeicher nicht beibehalten werden. Da Einzelseitenanwendungen normalerweise nicht zu einer neuen Seite navigieren, ist keine Sitzungsspeicherung für SPA Seiten erforderlich.
* **`filterClickDetails`**: Eine Callback-Funktion, die vollständige Kontrolle über von Ihnen erfasste Linktracking-Daten bietet. Mit dieser Rückruffunktion können Sie Linktracking-Daten ändern, verschleiern oder abbrechen. Dieser Rückruf ist nützlich, wenn Sie bestimmte Informationen weglassen möchten, z. B. persönlich identifizierbare Informationen innerhalb von Links.

## Klicken Sie auf die Sammlungseinstellungen mithilfe der Web SDK-Tag-Erweiterung

Wählen Sie eine der folgenden Optionen aus, wenn [die Tag-Erweiterung](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md) konfiguriert:

* [!UICONTROL Interne Links abrufen]
   * [!UICONTROL Optionen für die Ereignisgruppierung]:
      * [!UICONTROL Keine Ereignisgruppierung]
      * [!UICONTROL Ereignisgruppierung mithilfe des Sitzungsspeichers]
      * [!UICONTROL Ereignisgruppierung mit lokalem Objekt]
* [!UICONTROL Externe Links abrufen]
* [!UICONTROL Downloadlinks abrufen]
* [!UICONTROL Klickeigenschaften filtern]

1. Melden Sie sich mit Ihren Adobe ID-Anmeldedaten bei [experience.adobe.com](https://experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** und klicken Sie dann auf der Karte [!UICONTROL Adobe Experience Platform Web SDK] auf **[!UICONTROL Konfigurieren]** .
1. Scrollen Sie nach unten zum Abschnitt [!UICONTROL Datenerfassung] und wählen Sie dann die gewünschten Einstellungen für die Klicksammlung aus.
1. Klicken Sie auf **[!UICONTROL Speichern]** und veröffentlichen Sie dann Ihre Änderungen.

Der Rückruf [!UICONTROL Klickeigenschaften filtern] öffnet einen benutzerdefinierten Code-Editor, mit dem Sie den gewünschten Code einfügen können. Im Code-Editor haben Sie Zugriff auf die folgenden Variablen:

* **`content.clickedElement`**: Das DOM-Element, auf das geklickt wurde.
* **`content.pageName`**: Der Seitenname, an dem der Klick erfolgte.
* **`content.linkName`**: Der Name des angeklickten Links.
* **`content.linkRegion`**: Der Bereich des angeklickten Links.
* **`content.linkType`**: Der Typ des Links (Ausstieg, Download oder anderer).
* **`content.linkURL`**: Die Ziel-URL des angeklickten Links.
* **`return true`**: Beenden Sie den Rückruf sofort mit den aktuellen Variablenwerten.
* **`return false`**: Beenden Sie sofort den Rückruf und brechen Sie die Datenerfassung ab.

Alle Variablen, die außerhalb von `content` definiert sind, können verwendet werden, sind jedoch nicht in der Payload enthalten, die an Adobe gesendet wird.

## Klicken Sie auf Sammlungseinstellungen mithilfe der Web SDK JavaScript-Bibliothek.

Legen Sie die gewünschten Variablen im Objekt `clickCollection` fest, wenn Sie den Befehl [`configure`](overview.md) ausführen. Wenn nicht festgelegt, hängen die Standardeinstellungen für dieses Objekt vom Wert [`clickCollectionEnabled`](clickcollectionenabled.md) ab.

* `internalLinkEnabled`: Stimmt überein mit `clickCollectionEnabled`
* `downloadLinkEnabled`: Stimmt überein mit `clickCollectionEnabled`
* `externalLinkEnabled`: Stimmt überein mit `clickCollectionEnabled`
* `eventGroupingEnabled`: Der Standardwert ist `false`; muss explizit aktiviert sein.
* `sessionStorageEnabled`: Der Standardwert ist `false`; muss explizit aktiviert sein.
* `filterClickDetails`: Enthält keine Funktion; muss explizit registriert sein

>[!TIP]
>Adobe empfiehlt, `eventGroupingEnabled` zu aktivieren, wenn `internalLinkEnabled` aktiviert ist, da dadurch die Anzahl der Ereignisse verringert wird, die für die vertragliche Nutzung angerechnet werden.

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
