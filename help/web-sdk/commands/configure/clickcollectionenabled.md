---
title: clickCollectionEnabled
description: Erfahren Sie, wie Sie das Web SDK so konfigurieren, dass festgestellt wird, ob Link-Klick-Daten automatisch erfasst werden.
exl-id: e91b5bc6-8880-4884-87f9-60ec8787027e
source-git-commit: d3be2a9e75514023a7732a1c3460f8695ef02e68
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---

# `clickCollectionEnabled`

Die Eigenschaft `clickCollectionEnabled` ist ein boolescher Wert, der bestimmt, ob das Web SDK automatisch Verknüpfungsdaten erfasst. Wenn Sie diese Variable nicht festlegen, ist der Standardwert `true`, was bedeutet, dass die Linktracking-Daten standardmäßig automatisch erfasst werden. Das Festlegen dieser Eigenschaft auf `false` ist nützlich, wenn Sie Linkdaten lieber manuell verfolgen möchten.

Wenn `clickCollectionEnabled` aktiviert ist, werden die folgenden XDM-Elemente automatisch mit Daten aufgefüllt:

* `xdm.web.webInteraction.name`
* `xdm.web.webInteraction.type`
* `xdm.web.webInteraction.URL`

Interne Links, Downloadlinks und Exitlinks werden standardmäßig automatisch verfolgt, wenn dieser boolesche Wert aktiviert ist. Wenn Sie mehr Kontrolle über das automatische Linktracking wünschen, empfiehlt Adobe die Verwendung des Objekts [`clickCollection`](clickcollection.md) .

## Automatische Linktracking-Logik

Das Web SDK verfolgt alle Klicks auf HTML-Elemente `<a>` und `<area>`, wenn es kein `onClick` -Attribut aufweist. Klicks werden mit einem &quot;[Capture](https://www.w3.org/TR/uievents/#capture-phase)&quot;-Klickereignis erfasst, der an das Dokument angehängt ist. Wenn auf einen gültigen Link geklickt wird, wird die folgende Logik in der richtigen Reihenfolge ausgeführt:

1. Wenn der Link Kriterien erfüllt, die auf den Werten in [`downloadLinkQualifier`](downloadlinkqualifier.md) basieren, oder wenn der Link ein HTML-Attribut `download` enthält, wird `xdm.web.webInteraction.type` auf `"download"` gesetzt (wenn `clickCollection.downloadLinkEnabled` aktiviert ist).
1. Wenn die Zieldomäne des Links von der aktuellen `window.location.hostname` abweicht, wird `xdm.web.webInteraction.type` auf `"exit"` gesetzt (wenn `clickCollection.exitLinkEnabled` aktiviert ist).
1. Wenn der Link nicht für `"download"` oder `"exit"` qualifiziert ist, wird `xdm.web.webInteraction.type` auf `"other"` gesetzt.

In allen Fällen wird `xdm.web.webInteraction.name` auf die Textbeschriftung des Links und `xdm.web.webInteraction.URL` auf die Ziel-URL des Links festgelegt. Wenn Sie den Linknamen auch auf die URL setzen möchten, können Sie dieses XDM-Feld mithilfe des Rückrufs `filterClickDetails` im Objekt `clickCollection` überschreiben.

## Automatisches Linktracking mit der Web SDK-Tag-Erweiterung aktivieren {#tag-extension}

Diese Variable wird automatisch von der Tag-Erweiterung verwaltet. Sie müssen sie nicht explizit festlegen. Wenn beim [Konfigurieren der Tag-Erweiterung](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md) eine der folgenden Optionen ausgewählt ist, werden die entsprechenden Linktracking-Daten erfasst:

* [!UICONTROL Interne Link-Klicks abrufen]
* [!UICONTROL Externe Link-Klicks abrufen]
* [!UICONTROL Klicks auf Downloadlink abrufen]

Weitere Informationen finden Sie unter [`clickCollection`](clickcollection.md) .

## Automatisches Linktracking mit der Web SDK JavaScript-Bibliothek aktivieren {#library}

Legen Sie den booleschen Wert `clickCollectionEnabled` fest, wenn Sie den Befehl `configure` ausführen. Wenn Sie diese Eigenschaft beim Konfigurieren des Web SDK weglassen, wird standardmäßig `true` verwendet. Setzen Sie diesen Wert auf `false` , wenn Sie `xdm.web.webInteraction.type` und `xdm.web.webInteraction.value` manuell festlegen möchten.

```js
alloy(configure, {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: false
});
```
