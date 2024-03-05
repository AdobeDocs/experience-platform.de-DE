---
title: clickCollectionEnabled
description: Bestimmen Sie, ob Link-Klickdaten automatisch erfasst werden.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---


# `clickCollectionEnabled`

Die `clickCollectionEnabled` -Eigenschaft ist ein boolescher Wert, der bestimmt, ob das Web SDK automatisch Verknüpfungsdaten erfasst. Diese Eigenschaft ist nützlich, wenn Sie Linkdaten lieber manuell verfolgen möchten.

Wenn diese Option nicht deaktiviert ist, werden die folgenden XDM-Elemente automatisch mit Daten aufgefüllt:

* `xdm.web.webInteraction.name`
* `xdm.web.webInteraction.type`
* `xdm.web.webInteraction.URL`

## Automatische Linktracking-Logik

Das Web SDK verfolgt alle Klicks auf `<a>` und `<area>` HTML-Elemente, wenn keine `onClick` -Attribut. Klicks werden mit einem [erfassen](https://www.w3.org/TR/uievents/#capture-phase) Klicken Sie auf Ereignis-Listener, der an das Dokument angehängt ist. Wenn auf einen gültigen Link geklickt wird, wird die folgende Logik in der richtigen Reihenfolge ausgeführt:

1. Wenn der Link Kriterien erfüllt, die auf Werten in [`downloadLinkQualifier`](downloadlinkqualifier.md)oder wenn der Link eine `download` HTML-Attribut, `xdm.web.webInteraction.type` auf `"download"`.
1. Wenn die Zieldomäne des Links von der aktuellen `window.location.hostname`, `xdm.web.webInteraction.type` auf `"exit"`.
1. Wenn der Link sich nicht für `"download"` oder `"exit"`, `xdm.web.webInteraction.type` auf `"other"`.

In allen Fällen `xdm.web.webInteraction.name` auf die Textbeschriftung des Links festgelegt ist und `xdm.web.webInteraction.URL` auf die Link-Ziel-URL eingestellt ist. Wenn Sie den Linknamen auch auf die URL setzen möchten, können Sie dieses XDM-Feld mit [`onBeforeLinkClickSend`](onbeforelinkclicksend.md).

## Automatisches Linktracking mit der Web SDK-Tag-Erweiterung aktivieren

Wählen Sie die **[!UICONTROL Aktivieren der Klickdatenerfassung]** Kontrollkästchen, wenn [Konfigurieren der Tag-Erweiterung](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Anmelden bei [experience.adobe.com](https://experience.adobe.com) mit Ihren Adobe ID-Anmeldedaten.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** Klicken Sie auf **[!UICONTROL Konfigurieren]** auf [!UICONTROL Adobe Experience Platform Web SDK] Karte.
1. Scrollen Sie nach unten zum [!UICONTROL Datenerfassung] und wählen Sie das Kontrollkästchen aus. **[!UICONTROL Aktivieren der Klickdatenerfassung]**.
1. Klicks **[!UICONTROL Speichern]** und veröffentlichen Sie dann Ihre Änderungen.

## Automatisches Linktracking mit der JavaScript-Bibliothek des Web SDK aktivieren

Legen Sie die `clickCollectionEnabled` boolean beim Ausführen der `configure` Befehl. Wenn Sie diese Eigenschaft beim Konfigurieren des Web SDK weglassen, wird standardmäßig `true`. Setzen Sie diesen Wert auf `false` wenn Sie die manuelle Einstellung `xdm.web.webInteraction.type` und `xdm.web.webInteraction.value`.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "clickCollectionEnabled": false
});
```
