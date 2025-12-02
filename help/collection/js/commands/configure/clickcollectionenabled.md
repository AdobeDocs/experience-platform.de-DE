---
title: clickCollectionEnabled
description: Erfahren Sie, wie Sie Web SDK so konfigurieren, dass festgestellt wird, ob Link-Klickdaten automatisch erfasst werden.
exl-id: e91b5bc6-8880-4884-87f9-60ec8787027e
source-git-commit: 364b9adc406f732ea5ba450730397c4ce1bf03cf
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# `clickCollectionEnabled`

Die `clickCollectionEnabled`-Eigenschaft ist ein boolescher Wert, der bestimmt, ob die Web-SDK automatisch Linkdaten erfasst. Wenn Sie diese Variable nicht festlegen, lautet ihr Standardwert `true` , was bedeutet, dass Linktracking-Daten standardmäßig automatisch erfasst werden. Das Festlegen dieser Eigenschaft auf `false` ist nützlich, wenn Sie Linkdaten lieber manuell verfolgen möchten.

Wenn `clickCollectionEnabled` aktiviert ist, werden die folgenden XDM-Elemente automatisch mit Daten befüllt:

* `xdm.web.webInteraction.name`
* `xdm.web.webInteraction.type`
* `xdm.web.webInteraction.URL`

Interne Links, Downloadlinks und Exitlinks werden standardmäßig alle automatisch verfolgt, wenn dieser boolesche Wert aktiviert ist. Wenn Sie mehr Kontrolle über die automatische Linkverfolgung erhalten möchten, empfiehlt Adobe die Verwendung des [`clickCollection`](clickcollection.md).

## Automatische Linktracking-Logik

Web SDK verfolgt alle Klicks auf `<a>` und `<area>` HTML-Elemente, wenn es kein `onClick` hat. Klicks werden mit einem [-](https://www.w3.org/TR/uievents/#capture-phase)-Listener erfasst, der an das Dokument angehängt ist. Wenn auf einen gültigen Link geklickt wird, wird die folgende Logik der Reihe nach ausgeführt:

1. Wenn die Relation Kriterien auf der Grundlage von Werten in [`downloadLinkQualifier`](downloadlinkqualifier.md) entspricht oder ein `download` HTML-Attribut enthält, wird `xdm.web.webInteraction.type` auf `"download"` gesetzt (wenn `clickCollection.downloadLinkEnabled` aktiviert ist).
1. Wenn sich die Ziel-Domain des Links vom aktuellen `window.location.hostname` unterscheidet, wird `xdm.web.webInteraction.type` auf `"exit"` gesetzt (wenn `clickCollection.exitLinkEnabled` aktiviert ist).
1. Wenn der Link weder für `"download"` noch für `"exit"` qualifiziert ist, wird `xdm.web.webInteraction.type` auf `"other"` gesetzt.

In allen Fällen ist `xdm.web.webInteraction.name` auf die Link-Textbeschriftung und `xdm.web.webInteraction.URL` auf die Link-Ziel-URL festgelegt. Wenn Sie den Link-Namen auch für die URL festlegen möchten, können Sie dieses XDM-Feld mit dem `filterClickDetails`-Callback im `clickCollection`-Objekt überschreiben.

Legen Sie beim Ausführen des `clickCollectionEnabled`-Befehls den booleschen Wert `configure` fest. Wenn Sie diese Eigenschaft beim Konfigurieren der Web-SDK auslassen, wird sie standardmäßig auf `true` gesetzt. Legen Sie diesen Wert auf `false` fest, wenn Sie `xdm.web.webInteraction.type` und `xdm.web.webInteraction.value` manuell festlegen möchten.

```js
alloy(configure, {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: false
});
```

## Unterstützung für offene [!DNL Shadow DOM]

Web SDK unterstützt das automatische Klick-Tracking für Links in **Open Shadow-DOM**-Elementen.

Viele moderne Websites verwenden [Web-Komponenten](https://developer.mozilla.org/en-US/docs/Web/Web_Components) um wiederverwendbare und verkapselte Benutzeroberflächenelemente zu erstellen. Diese Komponenten verwenden häufig eine Technologie namens [**Shadow-DOM**](https://developer.mozilla.org/en-US/docs/Web/API/Web_components/Using_shadow_DOM), um ihre interne Struktur und ihre Stile vom Rest der Seite getrennt zu halten.

Es gibt zwei Arten von Shadow-DOM:

* **Open Shadow DOM:** Die interne Struktur ist für JavaScript verfügbar, das auf der Seite ausgeführt wird. Andere Skripte können mit dem Inhalt der Komponente interagieren oder ihn untersuchen.
* **Geschlossenes Shadow-DOM**: Die interne Struktur ist außerhalb der Komponente vor JavaScript verborgen, sodass sie für Tracking oder Manipulation nicht zugänglich ist.

Web SDK verfolgt Klicks auf `<a>` und `<area>` automatisch in **Open Shadow-DOMs**, genau wie bei Links im Hauptdokument. Dieses Tracking stellt sicher, dass Link-Klicks innerhalb von Web-Komponenten, die offene [!DNL Shadow DOM] verwenden, in Ihren Analytics-Daten enthalten sind. Klicks in **geschlossenen Shadow-DOMs** werden nicht verfolgt, da ihre interne Struktur vor JavaScript-Code verborgen ist, der außerhalb der Komponente ausgeführt wird.

## Aktivieren oder Deaktivieren der Klick-Sammlung für die Tag-Erweiterung „Web SDK&quot;

Siehe [Konfigurationseinstellungen für die Datenerfassung](/help/tags/extensions/client/web-sdk/configure/data-collection.md) in der Dokumentation zur Web SDK-Erweiterung, um zu erfahren, wie Sie diese Aktionen mithilfe von Tags durchführen können.
