---
title: clickCollectionEnabled
description: Erfahren Sie, wie Sie das Web SDK so konfigurieren, dass festgestellt wird, ob Link-Klick-Daten automatisch erfasst werden.
source-git-commit: 660d4e72bd93ca65001092520539a249eae23bfc
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---


# `clickCollectionEnabled`

Die `clickCollectionEnabled` -Eigenschaft ist ein boolescher Wert, der bestimmt, ob das Web SDK automatisch Verknüpfungsdaten erfasst. Wenn Sie diese Variable nicht festlegen, lautet der Standardwert `true` bedeutet, dass Linktracking-Daten standardmäßig automatisch erfasst werden. Festlegen dieser Eigenschaft auf `false` ist nützlich, wenn Sie Linkdaten lieber manuell verfolgen möchten.

Wann `clickCollectionEnabled` aktiviert ist, werden die folgenden XDM-Elemente automatisch mit Daten aufgefüllt:

* `xdm.web.webInteraction.name`
* `xdm.web.webInteraction.type`
* `xdm.web.webInteraction.URL`

Interne Links, Downloadlinks und Exitlinks werden standardmäßig automatisch verfolgt, wenn dieser boolesche Wert aktiviert ist. Wenn Sie mehr Kontrolle über das automatische Linktracking wünschen, empfiehlt Adobe die Verwendung der [`clickCollection`](clickcollection.md) -Objekt.

## Automatische Linktracking-Logik

Das Web SDK verfolgt alle Klicks auf `<a>` und `<area>` HTML-Elemente, wenn keine `onClick` -Attribut. Klicks werden mit einem [erfassen](https://www.w3.org/TR/uievents/#capture-phase) Klicken Sie auf Ereignis-Listener, der an das Dokument angehängt ist. Wenn auf einen gültigen Link geklickt wird, wird die folgende Logik in der richtigen Reihenfolge ausgeführt:

1. Wenn der Link Kriterien erfüllt, die auf Werten in [`downloadLinkQualifier`](downloadlinkqualifier.md)oder wenn der Link eine `download` HTML-Attribut, `xdm.web.webInteraction.type` auf `"download"` (if `clickCollection.downloadLinkEnabled` aktiviert ist).
1. Wenn die Zieldomäne des Links von der aktuellen `window.location.hostname`, `xdm.web.webInteraction.type` auf `"exit"` (if `clickCollection.exitLinkEnabled` aktiviert ist).
1. Wenn der Link sich nicht für `"download"` oder `"exit"`, `xdm.web.webInteraction.type` auf `"other"`.

In allen Fällen `xdm.web.webInteraction.name` auf die Textbeschriftung des Links festgelegt ist und `xdm.web.webInteraction.URL` auf die Link-Ziel-URL eingestellt ist. Wenn Sie den Linknamen auch auf die URL setzen möchten, können Sie dieses XDM-Feld mithilfe der `filterClickDetails` Callback in `clickCollection` -Objekt.

## Automatisches Linktracking mit der Web SDK-Tag-Erweiterung aktivieren {#tag-extension}

Wählen Sie die **[!UICONTROL Aktivieren der Klickdatenerfassung]** Kontrollkästchen, wenn [Konfigurieren der Tag-Erweiterung](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Anmelden bei [experience.adobe.com](https://experience.adobe.com) mit Ihren Adobe ID-Anmeldedaten.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** Klicken Sie auf **[!UICONTROL Konfigurieren]** auf [!UICONTROL Adobe Experience Platform Web SDK] Karte.
1. Scrollen Sie nach unten zum [!UICONTROL Datenerfassung] und wählen Sie das Kontrollkästchen aus. **[!UICONTROL Aktivieren der Klickdatenerfassung]**.
1. Klicks **[!UICONTROL Speichern]** und veröffentlichen Sie dann Ihre Änderungen.

## Automatisches Linktracking mit der Web SDK JavaScript-Bibliothek aktivieren {#library}

Legen Sie die `clickCollectionEnabled` boolean beim Ausführen der `configure` Befehl. Wenn Sie diese Eigenschaft beim Konfigurieren des Web SDK weglassen, wird standardmäßig `true`. Setzen Sie diesen Wert auf `false` wenn Sie `xdm.web.webInteraction.type` und `xdm.web.webInteraction.value` manuell.

```js
alloy(configure, {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: false
});
```
