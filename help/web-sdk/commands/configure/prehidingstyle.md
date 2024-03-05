---
title: prehidingStyle
description: Erstellen Sie eine CSS-Definition, die das Laden personalisierter Inhalte ohne Flackern ermöglicht.
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# `prehidingStyle`

Die `prehidingStyle` -Eigenschaft können Sie einen CSS-Selektor definieren, um personalisierte Inhalte auszublenden, bis sie geladen werden. Diese Eigenschaft ist in synchronen Web SDK-Implementierungen nützlich, um Flackern zu vermeiden. Adobe empfiehlt die Verwendung der [Codeausschnitt vorab ausblenden](../../personalization/manage-flicker.md) für asynchrone Web SDK-Implementierungen.

Die in dieser Eigenschaft definierten CSS-Selektoren beginnen mit dem Ausblenden von Inhalten, wenn Sie die erste [`sendEvent`](../sendevent/overview.md) auf einer Seite. Der Inhalt wird beim Empfang einer Antwort von Adobe nicht ausgeblendet, die normalerweise personalisierte Inhalte enthält. Der Inhalt wird auch dann wieder eingeblendet, wenn die `sendEvent` fehlschlägt oder eine Zeitüberschreitung auftritt.

Wenn Sie beide `prehidingStyle` und dem Codeausschnitt zur Vorab-Ausblendung in Ihrer Implementierung hat das Codeausschnitt zur Vorab-Ausblendung Vorrang vor dieser Konfigurationseigenschaft.

## Vorab Ausblenden des Stils mithilfe der Web SDK-Tag-Erweiterung

Wählen Sie die **[!UICONTROL Vorab-Ausblendungsstil bereitstellen]** Schaltflächen beim [Konfigurieren der Tag-Erweiterung](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Anmelden bei [experience.adobe.com](https://experience.adobe.com) mit Ihren Adobe ID-Anmeldedaten.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Erweiterungen]** Klicken Sie auf **[!UICONTROL Konfigurieren]** auf [!UICONTROL Adobe Experience Platform Web SDK] Karte.
1. Scrollen Sie nach unten zum [!UICONTROL Personalisierung] und wählen Sie dann die Schaltfläche **[!UICONTROL Vorab-Ausblendungsstil bereitstellen]**.
1. Diese Schaltfläche öffnet ein modales Fenster mit einem CSS-Editor. Fügen Sie den gewünschten CSS-Selektor und Deklarationsbaustein ein und klicken Sie dann auf **[!UICONTROL Speichern]** , um das modale Fenster zu schließen.
1. Klicks **[!UICONTROL Speichern]** unter den Erweiterungsparametern und veröffentlichen Sie dann Ihre Änderungen.

## Vorab Ausblenden des Stils mithilfe der Web SDK-JavaScript-Bibliothek

Legen Sie die `prehidingStyle` Zeichenfolge beim Ausführen der `configure` Befehl. Wenn Sie diese Eigenschaft beim Konfigurieren des Web SDK weglassen, wird beim Ausführen des ersten `sendEvent` auf einer Seite. Legen Sie diesen Wert auf den gewünschten CSS-Selektor und Deklarationsblock für synchron geladene Bibliotheken fest.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "prehidingStyle": "#container { opacity: 0 !important }"
});
```
