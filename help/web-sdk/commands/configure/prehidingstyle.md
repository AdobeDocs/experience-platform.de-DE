---
title: prehidingStyle
description: Erstellen Sie eine CSS-Definition, die das Laden personalisierter Inhalte ohne Flackern ermöglicht.
exl-id: 3693542a-69d3-4ad8-bea4-4cabf7d80563
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# `prehidingStyle`

Mit der Eigenschaft `prehidingStyle` können Sie einen CSS-Selektor definieren, um personalisierte Inhalte auszublenden, bis sie geladen werden. Diese Eigenschaft ist in synchronen Web SDK-Implementierungen nützlich, um Flackern zu vermeiden. Adobe empfiehlt die Verwendung des [Codebeispiels zum Vorab-Ausblenden](../../personalization/manage-flicker.md) für asynchrone Web SDK-Implementierungen.

Die CSS-Selektoren, die Sie in dieser Eigenschaft definieren, fangen an, Inhalte auszublenden, wenn Sie den ersten [`sendEvent`](../sendevent/overview.md) -Befehl auf einer Seite ausführen. Der Inhalt wird beim Empfang einer Antwort von Adobe nicht ausgeblendet, die normalerweise personalisierte Inhalte enthält. Der Inhalt wird auch dann nicht ausgeblendet, wenn der Befehl `sendEvent` fehlschlägt oder eine Zeitüberschreitung auftritt.

Wenn Sie sowohl `prehidingStyle` als auch den Codeausschnitt zur Vorab-Ausblendung in Ihre Implementierung einbeziehen, hat das Codeausschnitt zur Vorab-Ausblendung Vorrang vor dieser Konfigurationseigenschaft.

## Vorab Ausblenden des Stils mithilfe der Web SDK-Tag-Erweiterung

Wählen Sie beim Konfigurieren der Tag-Erweiterung [ die Schaltfläche **[!UICONTROL Vorab-Ausblendestil bereitstellen](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md) aus.]**

1. Melden Sie sich mit Ihren Adobe ID-Anmeldedaten bei [experience.adobe.com](https://experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** und klicken Sie dann auf der Karte [!UICONTROL Adobe Experience Platform Web SDK] auf **[!UICONTROL Konfigurieren]** .
1. Scrollen Sie nach unten zum Bereich [!UICONTROL Personalization] und wählen Sie dann die Schaltfläche **[!UICONTROL Vorab-Ausblendestil bereitstellen]** aus.
1. Diese Schaltfläche öffnet ein modales Fenster mit einem CSS-Editor. Fügen Sie den gewünschten CSS-Selektor und Deklarationsblock ein und klicken Sie dann auf **[!UICONTROL Speichern]** , um das modale Fenster zu schließen.
1. Klicken Sie unter den Erweiterungseinstellungen auf **[!UICONTROL Speichern]** und veröffentlichen Sie dann Ihre Änderungen.

## Vorab Ausblenden des Stils mithilfe der Web SDK JavaScript-Bibliothek

Legen Sie die Zeichenfolge `prehidingStyle` fest, wenn Sie den Befehl `configure` ausführen. Wenn Sie diese Eigenschaft beim Konfigurieren des Web SDK auslassen, wird beim Ausführen des ersten `sendEvent` -Befehls auf einer Seite nichts ausgeblendet. Legen Sie diesen Wert auf den gewünschten CSS-Selektor und Deklarationsblock für synchron geladene Bibliotheken fest.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  prehidingStyle: "#container { opacity: 0 !important }"
});
```
