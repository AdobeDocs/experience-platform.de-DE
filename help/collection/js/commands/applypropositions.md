---
title: applyPropositions
description: Vorschläge erneut rendern, die bereits mit sendEvent gerendert wurden.
exl-id: 6b79f334-4ea6-4ba4-8640-d35b7f90df98
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# `applyPropositions`

Mit dem Befehl `applyPropositions` können Sie Vorschläge, die bereits mit dem Befehl [`sendEvent`](sendevent/overview.md) gerendert wurden, erneut rendern. Dieser Befehl ist nützlich, wenn Sie mit Einzelseitenanwendungen arbeiten, in denen Teile der Seite erneut gerendert werden, wodurch möglicherweise bereits auf die Seite angewendete Personalisierungen überschrieben werden.

Dieser Befehl unterstützt die folgenden Felder:

* **Vorschläge**: Ein Array von Vorschlagsobjekten, die Sie erneut rendern möchten.
* **Ansichtsname**: Der Name der zu rendernden Ansicht. Die Anzeigebenachrichtigungen für diese Entscheidungen werden zwischengespeichert und können mit der Option `sendEvent` in einen nachfolgenden `personalization.includeRenderedPropositions`-Befehl eingefügt werden.
* **Meta-**: Ein Objekt, das bestimmt, wie HTML-Angebote angewendet werden können. Sie enthält die folgenden Eigenschaften:
   * Anwendungsbereich
   * Selektor
   * Aktionstyp

Führen Sie den `applyPropositions` Befehl aus, wenn Sie Ihre konfigurierte Instanz der Web-SDK aufrufen. Das -Objekt, das Konfigurationsoptionen enthält, unterstützt die folgenden Felder:

* **`propositions`**: Ein Array von Vorschlagsobjekten, die Sie erneut rendern möchten. Dieses Objekt wird in der Regel nicht verwendet, da das `propositionScopes` normalerweise bestimmt, welche Bereiche oder Oberflächen Sie erneut rendern möchten.
* **`metadata`**: Legt fest, wie HTML-Angebote angewendet werden. Es ist eine Zuordnung, bei der der Schlüssel ein Bereich oder eine Oberfläche ist und der Wert ein Objekt ist, das die Schlüssel `selector` und `actionType` enthält.
   * `selector`: Eine Zeichenfolge, die einen CSS-Selektor enthält, auf den die HTML angewendet werden soll.
   * `actionType`: Die Aktion, die mit der HTML durchgeführt werden soll. Gültige Werte sind `setHtml`, `replaceHtml` und `appendHtml`.
* **`viewName`**: Der Name der Ansicht, die in einer Einzelseitenanwendung gerendert werden soll. Die Anzeigebenachrichtigungen für diese Entscheidungen werden zwischengespeichert und können mit `sendEvent` in einen nachfolgenden `personalization.includeRenderedPropositions`-Befehl eingefügt werden.

```js
alloy("applyPropositions",{
  "propositions": [],
  "metadata": {},
  "viewName": ""
});
```

## Anwenden von Vorschlägen mithilfe der Tag-Erweiterung „Web SDK&quot;

Die diesem Befehl entsprechende Web SDK-Tag-Erweiterung ist die [**[!UICONTROL Apply propositions]**](/help/tags/extensions/client/web-sdk/actions/apply-propositions.md).
