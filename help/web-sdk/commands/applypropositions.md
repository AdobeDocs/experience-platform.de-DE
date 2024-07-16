---
title: applyPropositions
description: Rendern Sie Vorschläge erneut, die bereits mit sendEvent gerendert wurden.
exl-id: 6b79f334-4ea6-4ba4-8640-d35b7f90df98
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# `applyPropositions`

Mit dem Befehl `applyPropositions` können Sie Vorschläge erneut rendern, die bereits mit dem Befehl [`sendEvent`](sendevent/overview.md) gerendert wurden. Dieser Befehl ist beim Arbeiten mit Einzelseitenanwendungen nützlich, bei denen Teile der Seite erneut gerendert werden, wodurch möglicherweise bereits auf die Seite angewendete Personalisierungen überschrieben werden.

Dieser Befehl unterstützt die folgenden Felder:

* **Vorschläge**: Ein Array von Vorschlagsobjekten, die Sie erneut rendern möchten.
* **Name der Ansicht**: Der Name der Ansicht, die gerendert werden soll. Die Anzeigebenachrichtigungen für diese Entscheidungen werden zwischengespeichert und können mithilfe der Option `personalization.includePendingDisplayNotifications` in einen nachfolgenden `sendEvent` -Befehl aufgenommen werden.
* **Metadaten**: Ein Objekt, das bestimmt, wie HTML-Angebote angewendet werden können. Sie enthält die folgenden Eigenschaften:
   * Anwendungsbereich
   * Selektor
   * Aktionstyp

## Anwenden von Vorschlägen mithilfe der Web SDK-Tag-Erweiterung

Das Anwenden von Vorschlägen erfolgt als Aktion innerhalb einer Regel in der Adobe Experience Platform-Oberfläche für Datenerfassungs-Tags.

1. Melden Sie sich mit Ihren Adobe ID-Anmeldedaten bei [experience.adobe.com](https://experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Regeln]** und wählen Sie dann die gewünschte Regel aus.
1. Wählen Sie unter [!UICONTROL Aktionen] eine vorhandene Aktion aus oder erstellen Sie eine Aktion.
1. Setzen Sie das Dropdown-Feld [!UICONTROL Erweiterung] auf **[!UICONTROL Adobe Experience Platform Web SDK]** und legen Sie den Aktionstyp] auf **[!UICONTROL Vorschläge anwenden]** fest.[!UICONTROL 
1. Legen Sie die gewünschten Felder auf der rechten Seite fest.
1. Klicken Sie auf **[!UICONTROL Änderungen beibehalten]** und führen Sie dann Ihren Veröffentlichungs-Workflow aus.

## Anwenden von Vorschlägen mithilfe der Web SDK JavaScript-Bibliothek

Führen Sie den Befehl `applyPropositions` aus, wenn Sie Ihre konfigurierte Instanz des Web SDK aufrufen. Das Objekt, das Konfigurationsoptionen enthält, unterstützt die folgenden Felder:

* **`propositions`**: Ein Array von Vorschlagsobjekten, die Sie erneut rendern möchten. Dieses Objekt wird in der Regel nicht verwendet, da das Feld `propositionScopes` normalerweise bestimmt, welche Bereiche oder Oberflächen Sie erneut rendern möchten.
* **`metadata`**: Bestimmt, wie HTML-Angebote angewendet werden. Dies ist eine Zuordnung, bei der der Schlüssel ein Bereich oder eine Oberfläche ist und der Wert ein Objekt ist, das die Schlüssel `selector` und `actionType` enthält.
   * `selector`: Eine Zeichenfolge, die einen CSS-Selektor enthält, in dem die HTML angewendet werden soll.
   * `actionType`: Die Aktion, die mit der HTML ausgeführt werden soll. Gültige Werte sind `setHtml`, `replaceHtml` und `appendHtml`.
* **`viewName`**: Der Name der Ansicht, die in einer Einzelseitenanwendung dargestellt werden soll. Die Anzeigenbenachrichtigungen für diese Entscheidungen werden zwischengespeichert und können mit `personalization.includePendingDisplayNotifications` in einen nachfolgenden `sendEvent`-Befehl aufgenommen werden.

```js
alloy("applyPropositiions",{
  "propositions": [],
  "metadata": {},
  "viewName": ""
});
```
