---
title: PrehidingStyle
description: Erstellen Sie eine CSS-Definition, mit der personalisierte Inhalte geladen werden können, ohne dass sie flackern.
exl-id: 3693542a-69d3-4ad8-bea4-4cabf7d80563
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# `prehidingStyle`

Mit der `prehidingStyle` Eigenschaft können Sie einen CSS-Selektor definieren, um personalisierte Inhalte bis zum Laden auszublenden. Diese Eigenschaft ist bei synchronen Web-SDK-Implementierungen hilfreich, um Flackern zu vermeiden. Adobe empfiehlt die Verwendung des [Snippets zum Vorab-Ausblenden](../../personalization/manage-flicker.md) für asynchrone Web SDK-Implementierungen.

Die in dieser Eigenschaft definierten CSS-Selektoren beginnen mit dem Ausblenden von Inhalten, wenn Sie den ersten [`sendEvent`](../sendevent/overview.md) auf einer Seite ausführen. Inhalte werden beim Empfang einer Antwort von Adobe eingeblendet, die normalerweise personalisierte Inhalte enthält. Inhalte werden auch eingeblendet, wenn der `sendEvent`-Befehl fehlschlägt oder eine Zeitüberschreitung auftritt.

Wenn Sie sowohl `prehidingStyle` als auch den Code-Ausschnitt zum Vorab-Ausblenden in Ihre Implementierung aufnehmen, hat der Code-Ausschnitt zum Vorab-Ausblenden Vorrang vor dieser Konfigurationseigenschaft.

## Vorab-Ausblenden des Stils mit der Tag-Erweiterung „Web SDK&quot;

Klicken Sie beim **[!UICONTROL der Tag]**&#x200B;[ Erweiterung auf die Schaltfläche „Vorab-Ausblendungsstil bereitstellen](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei ](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** und klicken Sie dann auf **[!UICONTROL Konfigurieren]** auf der Karte [!UICONTROL Adobe Experience Platform Web SDK].
1. Scrollen Sie nach unten zum Abschnitt [!UICONTROL Personalization] und klicken Sie dann auf die Schaltfläche **[!UICONTROL Vorab-Ausblendstil]**.
1. Diese Schaltfläche öffnet ein modales Fenster mit einem CSS-Editor. Fügen Sie den gewünschten CSS-Selektor- und Deklarationsblock ein und klicken Sie dann auf **[!UICONTROL Speichern]**, um das modale Fenster zu schließen.
1. Klicken **[!UICONTROL unter]** auf „Speichern“ und veröffentlichen Sie Ihre Änderungen.

## Vorab-Ausblenden des Stils mit der Web SDK JavaScript-Bibliothek

Legen Sie die `prehidingStyle` beim Ausführen des `configure`-Befehls fest. Wenn Sie diese Eigenschaft beim Konfigurieren der Web-SDK auslassen, wird beim Ausführen des ersten `sendEvent` auf einer Seite nichts ausgeblendet. Legen Sie diesen Wert auf den gewünschten CSS-Selektor und Deklarationsblock für synchron geladene Bibliotheken fest.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  prehidingStyle: "#container { opacity: 0 !important }"
});
```
