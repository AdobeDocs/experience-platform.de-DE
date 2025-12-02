---
title: Personalization-Konfigurationseinstellungen
description: Konfigurieren Sie Personalisierungseinstellungen in der Tag-Erweiterung „Web SDK".
source-git-commit: 9f4ce2a3a8af72342683c859caa270662b161b7d
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 1%

---

# Personalization-Konfigurationseinstellungen

In diesem Konfigurationsabschnitt können Sie festlegen, wie Sie bestimmte Teile der Seite ausblenden möchten, während personalisierte Inhalte geladen werden. Wenn diese Einstellungen richtig konfiguriert sind, stellen Sie sicher, dass Ihre Besucher die richtigen personalisierten Inhalte sehen.

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei &#x200B;](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Extensions]** und wählen Sie **[!UICONTROL Configure]** auf der [!UICONTROL Adobe Experience Platform Web SDK] aus.
1. Scrollen Sie nach unten zum Abschnitt **[!UICONTROL Personalization]** .

![Bild mit den Personalisierungseinstellungen der Tag-Erweiterung „Web SDK&quot; in der Tags-Benutzeroberfläche](../assets/web-sdk-ext-personalization.png)

Die folgenden Optionen sind verfügbar:

## [!UICONTROL Migrate Target from at.js to the Web SDK]**

Verwenden Sie diese Option, damit der Web-SDK die veralteten `mbox` und `mboxEdgeCluster` Cookies lesen und schreiben kann, die von den Bibliotheken `at.js` 1.x oder 2.x verwendet werden. Mit dieser Einstellung bleiben Besucherprofile intakt, wenn Sie zwischen Seiten wechseln, die die Web-SDK oder `at.js` auf derselben Website verwenden. Wenn Sie `at.js` nirgendwo auf Ihrer Site implementiert haben, müssen Sie dieses Kontrollkästchen nicht aktivieren. Die JavaScript-Bibliothek, die diesem Kontrollkästchen entspricht, ist [`targetMigrationEnabled`](/help/collection/js/commands/configure/targetmigrationenabled.md).

## [!UICONTROL Prehiding style] {#prehiding-style}

Mit dem Stil-Editor zum Vorab-Ausblenden können Sie benutzerdefinierte CSS-Regeln definieren, um bestimmte Abschnitte einer Seite auszublenden. Wenn die Seite geladen wird, verwendet Web SDK diesen Stil, um die Abschnitte auszublenden, die personalisiert werden müssen, die Personalisierung abzurufen und dann die personalisierten Seitenabschnitte wieder aufzuheben. Dieser Workflow ermöglicht Besuchenden die Anzeige personalisierter Inhalte, ohne dass der Prozess des Personalisierungsabrufs im Laden oder Flackern zu sehen ist. Die JavaScript-Bibliothek, die diesem Code-Editor entspricht, ist [`prehidingStyle`](/help/collection/js/commands/configure/prehidingstyle.md).

## [!UICONTROL Prehiding snippet] {#prehiding-snippet}

Dieser Abschnitt ist keine direkte Konfigurationseinstellung, sondern ein praktischer Ort, an dem Sie Implementierungs-Code erhalten können. Implementieren Sie dieses Code-Ausschnitt zum Vorab-Ausblenden im `<head>`-Tag auf Ihrer Site, um den gewünschten Inhalt auszublenden, während die Web-SDK-Bibliothek geladen wird.

>[!IMPORTANT]
>
>Bei Verwendung des Ausschnitts zum Vorab-Ausblenden empfiehlt Adobe, dieselbe CSS-Regel zwischen dem Ausschnitt zum Vorab-Ausblenden und dem Stil zum Vorab-Ausblenden zu verwenden.

## [!UICONTROL Enable personalization storage]

Ein Kontrollkästchen, mit dem Web SDK Personalisierungsereignisse speichern kann. im lokalen Speicher des Browsers. Dies ist nützlich, wenn Sie verfolgen möchten, welche Erlebnisse der Besucher über Seitenladevorgänge hinweg gesehen hat.

## [!UICONTROL Auto click collection for Adobe Journey Optimizer]

Ein Dropdown-Menü, das bestimmt, wann die Web-SDK automatisch Klicks auf von Adobe Journey Optimizer zurückgegebene Inhalte erfasst.

* **[!UICONTROL Always]**: Sammeln Sie alle Interaktionen mit Vorschlägen.
* **[!UICONTROL Decorated elements only]**: Erfassen Sie nur Interaktionen zu Elementen mit `data-aep-click-label` oder `data-aep-click-token` HTML-Attributen.
* **[!UICONTROL Never]**: Interaktionen mit Vorschlägen werden nicht erfasst.

Die JavaScript-Bibliothek, die diesem Dropdown-Menü entspricht, ist [`autoCollectPropositionInteractions.AJO`](/help/collection/js/commands/configure/autocollectpropositioninteractions.md). Der Standardwert lautet [!UICONTROL Always].

## [!UICONTROL Auto click collection for Adobe Target]

Ein Dropdown-Menü, das bestimmt, wann die Web-SDK automatisch Klicks auf von Adobe Target zurückgegebene Inhalte erfasst.

* **[!UICONTROL Always]**: Sammeln Sie alle Interaktionen mit Vorschlägen.
* **[!UICONTROL Decorated elements only]**: Erfassen Sie nur Interaktionen zu Elementen mit `data-aep-click-label` oder `data-aep-click-token` HTML-Attributen.
* **[!UICONTROL Never]**: Interaktionen mit Vorschlägen werden nicht erfasst.

Die JavaScript-Bibliothek, die diesem Dropdown-Menü entspricht, ist [`autoCollectPropositionInteractions.TGT`](/help/collection/js/commands/configure/autocollectpropositioninteractions.md). Der Standardwert lautet [!UICONTROL Never].
