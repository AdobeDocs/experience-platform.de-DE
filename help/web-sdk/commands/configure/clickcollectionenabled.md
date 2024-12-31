---
title: clickCollectionEnabled
description: Erfahren Sie, wie Sie Web SDK so konfigurieren, dass festgestellt wird, ob Link-Klickdaten automatisch erfasst werden.
exl-id: e91b5bc6-8880-4884-87f9-60ec8787027e
source-git-commit: d3be2a9e75514023a7732a1c3460f8695ef02e68
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---

# `clickCollectionEnabled`

Die `clickCollectionEnabled`-Eigenschaft ist ein boolescher Wert, der bestimmt, ob die Web-SDK automatisch Linkdaten erfasst. Wenn Sie diese Variable nicht festlegen, lautet ihr Standardwert `true` , was bedeutet, dass Linktracking-Daten standardmäßig automatisch erfasst werden. Das Festlegen dieser Eigenschaft auf `false` ist nützlich, wenn Sie Linkdaten lieber manuell verfolgen möchten.

Wenn `clickCollectionEnabled` aktiviert ist, werden die folgenden XDM-Elemente automatisch mit Daten befüllt:

* `xdm.web.webInteraction.name`
* `xdm.web.webInteraction.type`
* `xdm.web.webInteraction.URL`

Interne Links, Downloadlinks und Exitlinks werden standardmäßig alle automatisch verfolgt, wenn dieser boolesche Wert aktiviert ist. Wenn Sie mehr Kontrolle über das automatische Linktracking erhalten möchten, empfiehlt Adobe die Verwendung des [`clickCollection`](clickcollection.md).

## Automatische Linktracking-Logik

Web SDK verfolgt alle Klicks auf `<a>` und `<area>` HTML-Elemente, wenn es kein `onClick` hat. Klicks werden mit einem [-](https://www.w3.org/TR/uievents/#capture-phase)-Listener erfasst, der an das Dokument angehängt ist. Wenn auf einen gültigen Link geklickt wird, wird die folgende Logik der Reihe nach ausgeführt:

1. Wenn die Relation Kriterien auf der Grundlage von Werten in [`downloadLinkQualifier`](downloadlinkqualifier.md) entspricht oder ein `download` HTML-Attribut enthält, wird `xdm.web.webInteraction.type` auf `"download"` gesetzt (wenn `clickCollection.downloadLinkEnabled` aktiviert ist).
1. Wenn sich die Ziel-Domain des Links vom aktuellen `window.location.hostname` unterscheidet, wird `xdm.web.webInteraction.type` auf `"exit"` gesetzt (wenn `clickCollection.exitLinkEnabled` aktiviert ist).
1. Wenn der Link weder für `"download"` noch für `"exit"` qualifiziert ist, wird `xdm.web.webInteraction.type` auf `"other"` gesetzt.

In allen Fällen ist `xdm.web.webInteraction.name` auf die Link-Textbeschriftung und `xdm.web.webInteraction.URL` auf die Link-Ziel-URL festgelegt. Wenn Sie den Link-Namen auch für die URL festlegen möchten, können Sie dieses XDM-Feld mit dem `filterClickDetails`-Callback im `clickCollection`-Objekt überschreiben.

## Aktivieren der automatischen Linkverfolgung mit der Tag-Erweiterung „Web SDK&quot; {#tag-extension}

Diese Variable wird automatisch von der Tag-Erweiterung verwaltet; Sie müssen sie nicht explizit festlegen. Wenn beim Konfigurieren [ Tag-Erweiterung eine der folgenden Optionen ausgewählt ](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md), werden die entsprechenden Linktracking-Daten erfasst:

* [!UICONTROL Erfassen interner Link-Klicks]
* [!UICONTROL Erfassen externer Link-Klicks]
* [!UICONTROL Klicks auf Download-Links erfassen]

Weitere Informationen finden Sie unter [`clickCollection`](clickcollection.md) .

## Aktivieren der automatischen Linkverfolgung mithilfe der Web SDK JavaScript-Bibliothek {#library}

Legen Sie beim Ausführen des `configure`-Befehls den booleschen Wert `clickCollectionEnabled` fest. Wenn Sie diese Eigenschaft beim Konfigurieren der Web-SDK auslassen, wird sie standardmäßig auf `true` gesetzt. Legen Sie diesen Wert auf `false` fest, wenn Sie `xdm.web.webInteraction.type` und `xdm.web.webInteraction.value` manuell festlegen möchten.

```js
alloy(configure, {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: false
});
```
