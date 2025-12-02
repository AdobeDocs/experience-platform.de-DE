---
title: Vorschläge anwenden
description: Vorschläge rendern in Single-Page Applications ohne Inkrementierung von Metriken.
source-git-commit: 217282135bcd750740f4d3f8c6e17a0b8f9578bd
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 1%

---

# Vorschläge anwenden

Mit dem Aktionstyp **[!UICONTROL Apply propositions]** können Sie Vorschläge in Single-Page Applications rendern, ohne die Metriken zu inkrementieren. Dieser Aktionstyp ist nützlich bei der Arbeit mit Einzelseitenanwendungen, bei denen Teile der Seite erneut gerendert werden, wodurch möglicherweise bereits auf die Seite angewendete Personalisierungen überschrieben werden.

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei &#x200B;](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Rules]** und wählen Sie dann die gewünschte Regel aus.
1. Wählen Sie unter [!UICONTROL Actions] eine vorhandene Aktion aus oder erstellen Sie eine Aktion.
1. Legen Sie das Dropdown-Feld [!UICONTROL Extension] auf **[!UICONTROL Adobe Experience Platform Web SDK]** und dann den [!UICONTROL Action type] auf **[!UICONTROL Apply propositions]** fest.

![Experience Platform Tags-Benutzeroberfläche mit dem Aktionstyp „Vorschläge anwenden“](../assets/apply-propositions.png)

## Anwendungsfälle

Sie können diesen Aktionstyp für verschiedene Anwendungsfälle verwenden, z. B.:

1. **Rendern von Mbox HTML-Angeboten**. Vorschläge, die explizit über einen Bereich oder eine Oberfläche von einer **[!UICONTROL Send event]** Aktion angefordert werden, werden nicht automatisch gerendert. Sie können den Aktionstyp **[!UICONTROL Apply propositions]** verwenden, um Web SDK mitzuteilen, wo sie gerendert werden sollen, indem Sie die Vorschlagsmetadaten angeben.
2. **Rendern der Angebote für eine Ansicht auf einer Einzelseitenanwendung**. Wenn beim Rendern eines Ansichtsänderungsereignisses die Analysedaten noch nicht bereit sind, können Sie die **[!UICONTROL Apply propositions]** Aktion verwenden, um die Ansichtsvorschläge oben auf der Seite zu rendern. Siehe [Ereignisse oben und unten auf der Seite (Zweite Seitenansicht - Option 2)](/help/collection/use-cases/personalization/top-bottom-page-events.md) für weitere Details. Um dies zu verwenden, geben Sie einen **[!UICONTROL View name]** in das Formular ein.
3. **Vorschläge neu rendern**. Wenn Ihre Site ein Framework wie React verwendet, um Inhalte erneut zu rendern, müssen Sie möglicherweise die Personalisierung erneut anwenden. In solchen Fällen können Sie den Aktionstyp **[!UICONTROL Apply propositions]** verwenden, um dies zu tun.

Dieser Aktionstyp sendet kein Anzeigeereignis für gerenderte Vorschläge. Es verfolgt gerenderte Vorschläge, damit sie in nachfolgenden **[!UICONTROL Send event]**-Aufrufen einbezogen werden können.

## Verfügbare Felder

Dieser Aktionstyp unterstützt die folgenden Felder:

* **[!UICONTROL Instance]**: Die SDK-Instanz, für die die Aktion gilt. Dieses Dropdown-Menü ist deaktiviert, wenn Ihre Implementierung eine einzige SDK-Instanz verwendet.
* **[!UICONTROL Propositions]**: Ein Array von Vorschlagsobjekten, die Sie erneut rendern möchten.
* **[!UICONTROL View name]**: Der Name der zu rendernden Ansicht.
* **[!UICONTROL Proposition metadata]**: Ein Objekt, das bestimmt, wie HTML-Angebote angewendet werden können. Sie können diese Informationen entweder über das Formular oder über ein Datenelement bereitstellen. Sie enthält die folgenden Eigenschaften:
   * **[!UICONTROL Scope]**
   * **[!UICONTROL Selector]**
   * **[!UICONTROL Action type]**
