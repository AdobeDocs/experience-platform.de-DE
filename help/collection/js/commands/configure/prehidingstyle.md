---
title: PrehidingStyle
description: Erstellen Sie eine CSS-Definition, mit der personalisierte Inhalte geladen werden können, ohne dass sie flackern.
exl-id: 3693542a-69d3-4ad8-bea4-4cabf7d80563
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# `prehidingStyle`

Mit der `prehidingStyle` Eigenschaft können Sie einen CSS-Selektor definieren, um personalisierte Inhalte bis zum Laden auszublenden. Diese Eigenschaft ist bei synchronen Web-SDK-Implementierungen hilfreich, um Flackern zu vermeiden. Adobe empfiehlt die Verwendung des [Snippets zum Vorab-Ausblenden](/help/collection/use-cases/personalization/manage-flicker.md) für asynchrone Web-SDK-Implementierungen.

Die in dieser Eigenschaft definierten CSS-Selektoren beginnen mit dem Ausblenden von Inhalten, wenn Sie den ersten [`sendEvent`](../sendevent/overview.md) auf einer Seite ausführen. Inhalte werden beim Empfang einer Antwort von Adobe eingeblendet, die normalerweise personalisierte Inhalte enthält. Inhalte werden auch eingeblendet, wenn der `sendEvent`-Befehl fehlschlägt oder eine Zeitüberschreitung auftritt.

Wenn Sie sowohl `prehidingStyle` als auch den Code-Ausschnitt zum Vorab-Ausblenden in Ihre Implementierung aufnehmen, hat der Code-Ausschnitt zum Vorab-Ausblenden Vorrang vor dieser Konfigurationseigenschaft.

Legen Sie die `prehidingStyle` beim Ausführen des `configure`-Befehls fest. Wenn Sie diese Eigenschaft beim Konfigurieren der Web-SDK auslassen, wird beim Ausführen des ersten `sendEvent` auf einer Seite nichts ausgeblendet. Legen Sie diesen Wert auf den gewünschten CSS-Selektor und Deklarationsblock für synchron geladene Bibliotheken fest.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  prehidingStyle: "#container { opacity: 0 !important }"
});
```

## Vorab-Ausblenden des Stils mit der Tag-Erweiterung „Web SDK&quot;

Diese Einstellungen können in der Tag-Erweiterung „Web SDK&quot; mithilfe der [Personalization-Konfigurationseinstellungen konfiguriert ](/help/tags/extensions/client/web-sdk/configure/personalization.md).
