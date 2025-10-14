---
title: applyPropositions
description: Vorschläge erneut rendern, die bereits mit sendEvent gerendert wurden.
exl-id: 6b79f334-4ea6-4ba4-8640-d35b7f90df98
source-git-commit: 4c7313afdce6645ab638b2998573e5a4f7c5de8f
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# `applyPropositions`

Mit dem Befehl `applyPropositions` können Sie Vorschläge, die bereits mit dem Befehl [`sendEvent`](sendevent/overview.md) gerendert wurden, erneut rendern. Dieser Befehl ist nützlich, wenn Sie mit Einzelseitenanwendungen arbeiten, in denen Teile der Seite erneut gerendert werden, wodurch möglicherweise bereits auf die Seite angewendete Personalisierungen überschrieben werden.

Dieser Befehl unterstützt die folgenden Felder:

* **Vorschläge**: Ein Array von Vorschlagsobjekten, die Sie erneut rendern möchten.
* **Ansichtsname**: Der Name der zu rendernden Ansicht. Die Anzeigebenachrichtigungen für diese Entscheidungen werden zwischengespeichert und können mit der Option `personalization.includeRenderedPropositions` in einen nachfolgenden `sendEvent`-Befehl eingefügt werden.
* **Metadaten**: Ein Objekt, das bestimmt, wie HTML-Angebote angewendet werden können. Sie enthält die folgenden Eigenschaften:
   * Anwendungsbereich
   * Selektor
   * Aktionstyp

## Anwenden von Vorschlägen mithilfe der Tag-Erweiterung „Web SDK&quot;

Das Anwenden von Vorschlägen wird als Aktion innerhalb einer Regel in der Benutzeroberfläche für Datenerfassungs-Tags von Adobe Experience Platform ausgeführt.

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei &#x200B;](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Regeln]** und wählen Sie dann die gewünschte Regel aus.
1. Wählen [!UICONTROL &#x200B; unter &quot;]&quot; eine vorhandene Aktion aus oder erstellen Sie eine Aktion.
1. Legen Sie [!UICONTROL &#x200B; Dropdown-Feld &#x200B;]Erweiterung“ auf **[!UICONTROL Adobe Experience Platform Web SDK]** fest und [!UICONTROL Aktionstyp] auf **[!UICONTROL Vorschläge anwenden]**.
1. Legen Sie die gewünschten Felder auf der rechten Seite fest.
1. Klicken Sie **[!UICONTROL Änderungen beibehalten]** und führen Sie dann den Veröffentlichungs-Workflow aus.

## Anwenden von Vorschlägen mithilfe der Web SDK JavaScript-Bibliothek

Führen Sie den `applyPropositions` Befehl aus, wenn Sie Ihre konfigurierte Instanz der Web-SDK aufrufen. Das -Objekt, das Konfigurationsoptionen enthält, unterstützt die folgenden Felder:

* **`propositions`**: Ein Array von Vorschlagsobjekten, die Sie erneut rendern möchten. Dieses Objekt wird in der Regel nicht verwendet, da das `propositionScopes` normalerweise bestimmt, welche Bereiche oder Oberflächen Sie erneut rendern möchten.
* **`metadata`**: Legt fest, wie HTML-Angebote angewendet werden. Es ist eine Zuordnung, bei der der Schlüssel ein Bereich oder eine Oberfläche ist und der Wert ein Objekt ist, das die Schlüssel `selector` und `actionType` enthält.
   * `selector`: Eine Zeichenfolge, die eine CSS-Auswahl zum Anwenden der HTML enthält.
   * `actionType`: Die Aktion, die mit der HTML ausgeführt werden soll. Gültige Werte sind `setHtml`, `replaceHtml` und `appendHtml`.
* **`viewName`**: Der Name der Ansicht, die in einer Einzelseitenanwendung gerendert werden soll. Die Anzeigebenachrichtigungen für diese Entscheidungen werden zwischengespeichert und können mit `personalization.includeRenderedPropositions` in einen nachfolgenden `sendEvent`-Befehl eingefügt werden.

```js
alloy("applyPropositions",{
  "propositions": [],
  "metadata": {},
  "viewName": ""
});
```
