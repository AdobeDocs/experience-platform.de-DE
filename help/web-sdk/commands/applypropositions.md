---
title: applyPropositions
description: Rendern Sie Vorschläge erneut, die bereits mit sendEvent gerendert wurden.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 1%

---


# `applyPropositions`

Die `applyPropositions` -Befehl können Sie Vorschläge erneut rendern, die bereits mit der [`sendEvent`](sendevent/overview.md) Befehl. Dieser Befehl ist beim Arbeiten mit Einzelseitenanwendungen nützlich, bei denen Teile der Seite erneut gerendert werden, wodurch möglicherweise bereits auf die Seite angewendete Personalisierungen überschrieben werden.

Dieser Befehl unterstützt die folgenden Felder:

* **Vorschläge**: Ein Array von Vorschlagsobjekten, die Sie erneut rendern möchten.
* **Anzeigename**: Der Name der anzuzeigenden Ansicht. Die Anzeigebenachrichtigungen für diese Entscheidungen werden zwischengespeichert und können in einer nachfolgenden `sendEvent` -Befehl mithilfe des `personalization.includePendingDisplayNotifications` -Option.
* **Metadaten**: Ein Objekt, das bestimmt, wie HTML-Angebote angewendet werden können. Sie enthält die folgenden Eigenschaften:
   * Anwendungsbereich
   * Selektor
   * Aktionstyp

## Anwenden von Vorschlägen mithilfe der Web SDK-Tag-Erweiterung

Das Anwenden von Vorschlägen erfolgt als Aktion innerhalb einer Regel in der Adobe Experience Platform-Oberfläche für Datenerfassungs-Tags.

1. Anmelden bei [experience.adobe.com](https://experience.adobe.com) mit Ihren Adobe ID-Anmeldedaten.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Regeln]** und wählen Sie dann die gewünschte Regel aus.
1. under [!UICONTROL Aktionen], wählen Sie eine vorhandene Aktion aus oder erstellen Sie eine Aktion.
1. Legen Sie die [!UICONTROL Erweiterung] Dropdown-Feld zu **[!UICONTROL Adobe Experience Platform Web SDK]** und legen Sie die [!UICONTROL Aktionstyp] nach **[!UICONTROL Vorschläge anwenden]**.
1. Legen Sie die gewünschten Felder auf der rechten Seite fest.
1. Klicks **[!UICONTROL Änderungen beibehalten]** und führen Sie dann Ihren Veröffentlichungs-Workflow aus.

## Vorschläge mithilfe der JavaScript-Bibliothek des Web SDK anwenden

Führen Sie die `applyPropositions` beim Aufruf Ihrer konfigurierten Instanz des Web SDK. Das Objekt, das Konfigurationsoptionen enthält, unterstützt die folgenden Felder:

* **`propositions`**: Ein Array von Vorschlagsobjekten, die Sie erneut rendern möchten. Dieses Objekt wird normalerweise nicht verwendet, da die Variable `propositionScopes` -Feld bestimmt normalerweise, welche Bereiche oder Oberflächen Sie erneut rendern möchten.
* **`metadata`**: Bestimmt, wie HTML-Angebote angewendet werden. Dies ist eine Zuordnung, bei der der Schlüssel ein Bereich oder eine Oberfläche ist und der Wert ein Objekt ist, das die Schlüssel enthält `selector` und `actionType`.
   * `selector`: Eine Zeichenfolge, die einen CSS-Selektor von enthält, auf den die HTML angewendet werden soll.
   * `actionType`: Die Aktion, die mit der HTML ausgeführt werden soll. Gültige Werte sind `setHtml`, `replaceHtml` und `appendHtml`.
* **`viewName`**: Der Name der Ansicht, die in einer Einzelseitenanwendung dargestellt werden soll. Die Anzeigebenachrichtigungen für diese Entscheidungen werden zwischengespeichert und können in einer nachfolgenden `sendEvent` -Befehl mit `personalization.includePendingDisplayNotifications`.

```js
alloy("applyPropositiions",{
  "propositions": [],
  "metadata": {},
  "viewName": ""
});
```
