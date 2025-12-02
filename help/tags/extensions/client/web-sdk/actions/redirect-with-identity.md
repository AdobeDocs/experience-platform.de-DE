---
title: Mit Identität umleiten
description: Ermöglicht die Freigabe einer Besucherkennung über die Domains Ihres Unternehmens hinweg.
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 1%

---

# Mit Identität umleiten

Mit dem Aktionstyp &quot;**[!UICONTROL Redirect with identity]**&quot; können Sie eine Besucher-ID von der aktuellen Seite für eine andere Domain freigeben, der Ihr Unternehmen gehört. Es wurde für die Verwendung mit einem Klickereignis und einer Wertvergleichsbedingung entwickelt. Sie ähnelt funktionell dem Befehl [`appendIdentityToUrl`](/help/collection/js/commands/appendidentitytourl.md) in der JavaScript-Bibliothek.

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei &#x200B;](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Rules]** und wählen Sie dann die gewünschte Regel aus.
1. Wählen Sie unter [!UICONTROL Actions] eine vorhandene Aktion aus oder erstellen Sie eine Aktion.
1. Legen Sie das Dropdown-Feld [!UICONTROL Extension] auf **[!UICONTROL Adobe Experience Platform Web SDK]** und dann den [!UICONTROL Action type] auf **[!UICONTROL Redirect with identity]** fest.

## Anwendungsfälle

* **Domain-übergreifendes Identifizieren einer Person**: Wenn ein Besucher von einer Domain zu einer anderen klickt, die Ihrem Unternehmen gehört, können Sie diese Aktion verwenden, damit sie weiterhin als dieselbe Person betrachtet werden. Diese Identifizierungsmethode ist besonders nützlich, wenn Berichte vorhanden sind, die Daten aus mehreren Domains kombinieren, wodurch ein Überangebot an Besuchern verhindert wird.
* **Person von einer mobilen App zu einer Web-App identifizieren**: Wenn sich ein Besucher in Ihrer mobilen App befindet und auf einen Link zu Ihrer Web-App klickt, können Sie diese Aktion verwenden, damit Web SDK anerkennt, dass es sich um dieselbe Person handelt. Dieser Workflow ermöglicht ein konsistentes Erlebnis für die Berichterstellung und Personalisierung.

## Verfügbare Felder

* **[!UICONTROL Instance]**: Die SDK-Instanz, für die die Aktion gilt. Dieses Dropdown-Menü ist deaktiviert, wenn Ihre Implementierung eine einzige SDK-Instanz verwendet.
* **[!UICONTROL Datastream configuration overrides]**: Dieser Befehl unterstützt Überschreibungen der Datenstromkonfiguration, sodass Sie steuern können, welche Apps und Services diese Daten erhalten. Wenn Sie eine Überschreibung der Datenstromkonfiguration sowohl in einem einzelnen Befehl als auch in den Konfigurationseinstellungen der Tag-Erweiterung festlegen, hat der einzelne Befehl Vorrang. Weitere [&#x200B; finden Sie unter &#x200B;](../configure/configuration-overrides.md) der Datenstromkonfiguration .

## Beispielregel

Dieser Befehl wird normalerweise mit einer bestimmten Regel verwendet, die auf Klicks wartet und die gewünschten Domains prüft.

+++Kriterien für Regelereignisse

Trigger beim Klicken auf ein Anker-Tag mit einer `href`.

* **[!UICONTROL Extension]**: Core
* **[!UICONTROL Event type]**: Klicken
* **[!UICONTROL When the user clicks on]**: Spezifische Elemente
* **[!UICONTROL Elements matching the CSS selector]**: `a[href]`

![Regelereignis](../assets/id-sharing-event-configuration.png)

+++

+++Regelbedingung

Trigger nur auf den gewünschten Domains.

* **[!UICONTROL Logic type]**: normal
* **[!UICONTROL Extension]**: Core
* **[!UICONTROL Condition Type]**: Wertvergleich
* **[!UICONTROL Left Operand]**: `%this.hostname%`
* **[!UICONTROL Operator]**: Stimmt mit Regex überein
* **[!UICONTROL Right Operand]**: Ein regulärer Ausdruck, der den gewünschten Domains entspricht. Beispiel: `adobe.com$|behance.com$`

![Regelbedingung](../assets/id-sharing-condition-configuration.png)

+++

+++Regelaktion

Hängen Sie die Identität an die URL an.

* **[!UICONTROL Extension]**: Adobe Experience Platform Web SDK
* **[!UICONTROL Action Type]**: Mit Identität umleiten

![Regelaktion](../assets/id-sharing-action-configuration.png)

+++
