---
title: clickCollectionEnabled
description: Erfahren Sie, wie Sie das Web SDK so konfigurieren, dass festgestellt wird, ob Link-Klick-Daten automatisch erfasst werden.
source-git-commit: 660d4e72bd93ca65001092520539a249eae23bfc
workflow-type: tm+mt
source-wordcount: '371'
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

Aktivieren Sie das Kontrollkästchen **[!UICONTROL Klick-Datenerfassung aktivieren]** bei der Konfiguration der Tag-Erweiterung [.](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)

1. Melden Sie sich mit Ihren Adobe ID-Anmeldedaten bei [experience.adobe.com](https://experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** und klicken Sie dann auf der Karte [!UICONTROL Adobe Experience Platform Web SDK] auf **[!UICONTROL Konfigurieren]** .
1. Scrollen Sie nach unten zum Abschnitt [!UICONTROL Datenerfassung] und aktivieren Sie dann das Kontrollkästchen **[!UICONTROL Klick-Datenerfassung aktivieren]** .
1. Klicken Sie auf **[!UICONTROL Speichern]** und veröffentlichen Sie dann Ihre Änderungen.

## Automatisches Linktracking mit der Web SDK JavaScript-Bibliothek aktivieren {#library}

Legen Sie den booleschen Wert `clickCollectionEnabled` fest, wenn Sie den Befehl `configure` ausführen. Wenn Sie diese Eigenschaft beim Konfigurieren des Web SDK weglassen, wird standardmäßig `true` verwendet. Setzen Sie diesen Wert auf `false` , wenn Sie `xdm.web.webInteraction.type` und `xdm.web.webInteraction.value` manuell festlegen möchten.

```js
alloy(configure, {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: false
});
```
