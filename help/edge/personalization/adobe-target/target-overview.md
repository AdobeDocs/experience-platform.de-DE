---
title: Verwenden von Adobe Target mit dem Platform Web SDK
description: Erfahren Sie, wie Sie personalisierte Inhalte mit dem Experience Platform Web SDK mit Adobe Target wiedergeben
keywords: Zielgruppe;adobe-Zielgruppe;Aktivität.id;Experience.id;renderDecision;DecisionScopes;prehiding snippet;vec;Form-Based Experience Composer;xdm;Audiencen;Beschlüsse;Scope;Schema;
exl-id: 021171ab-0490-4b27-b350-c37d2a569245
source-git-commit: 20adb26fbd55302ac8005978968a0d69bdda8755
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 5%

---

# Verwenden von Adobe Target mit dem Platform Web SDK

Adobe Experience Platform [!DNL Web SDK] kann personalisierte Erlebnisse, die in Adobe Target verwaltet werden, für den Web-Kanal bereitstellen und rendern. Sie können einen WYSIWYG-Editor mit dem Namen [Visual Experience Composer](https://docs.adobe.com/content/help/en/target/using/experiences/vec/visual-experience-composer.html) (VEC) oder eine nicht visuelle Schnittstelle, den [Form-Based Experience Composer](https://docs.adobe.com/content/help/en/target/using/experiences/form-experience-composer.html), verwenden, um Ihre Aktivitäten und Personalisierungserlebnisse zu erstellen, zu aktivieren und bereitzustellen.

Die folgenden Funktionen wurden getestet und werden derzeit in der Zielgruppe unterstützt:

* A/B-Tests
* A4T Impression and Conversion Berichte
* Automated Personalization
* Erlebnis-Targeting
* Multivarianz-Tests
* Native Zielgruppe Impression and Conversion Berichte
* VEC-Unterstützung

## Aktivieren von Adobe Target

Gehen Sie wie folgt vor, um [!DNL Target] zu aktivieren:

1. Aktivieren Sie die Zielgruppe in Ihrem [datastream](../../fundamentals/datastreams.md) mit dem entsprechenden Clientcode.
1. hinzufügen Sie die Option `renderDecisions` zu Ihren Ereignissen.

Optional können Sie dann auch die folgenden Optionen hinzufügen:

* `decisionScopes`: Rufen Sie bestimmte Aktivitäten ab (nützlich für mit dem formularbasierten Composer erstellte Aktivitäten), indem Sie diese Option zu Ihren Ereignissen hinzufügen.
* [Ausblenden von Snippets](../manage-flicker.md) verhindern: Blenden Sie nur bestimmte Teile der Seite aus.

## Verwenden des Adobe Target VEC

Um VEC mit einer Platform Web SDK-Implementierung zu verwenden, installieren und aktivieren Sie entweder die VEC Helper Extension [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) oder [Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak).

## VEC-Aktivitäten automatisch rendern

Adobe Experience Platform Web SDK ist befugt, Ihre Erlebnisse, die über Adobe Target’s VEC im Web definiert werden, automatisch für Ihre Benutzer darzustellen. Um Adobe Experience Platform Web SDK anzuzeigen, dass VEC-Aktivitäten automatisch gerendert werden, senden Sie ein Ereignis mit `renderDecisions = true`:

```javascript
alloy
("sendEvent", 
  { 
  "renderDecisions": true, 
  "xdm": {
    "commerce": { 
      "order": {
        "purchaseID": "a8g784hjq1mnp3", 
         "purchaseOrderNumber": "VAU3123", 
         "currencyCode": "USD", 
         "priceTotal": 999.98 
         } 
      } 
    }
  }
);
```

## Verwenden des formularbasierten Composers

Der formularbasierte Experience Composer ist eine nicht visuelle Benutzeroberfläche, die zum Konfigurieren von A/B-Tests, [!DNL Experience Targeting]-, Automated Personalization- und Recommendations-Aktivitäten mit verschiedenen Antworttypen wie JSON, HTML, Image usw. nützlich ist. Abhängig vom Antworttyp oder der von Adobe Target zurückgegebenen Entscheidung kann Ihre Kerngeschäftslogik ausgeführt werden. Um Entscheidungen für Ihre formularbasierten Composer-Aktivitäten abzurufen, senden Sie ein Ereignis mit allen &quot;DecisionScopes&quot;, für die Sie eine Entscheidung abrufen möchten.

```javascript
alloy
  ("sendEvent", { 
    decisionScopes: [
      "foo", "bar"], 
      "xdm": {
        "commerce": { 
          "order": { 
            "purchaseID": "a8g784hjq1mnp3", 
            "purchaseOrderNumber": "VAU3123", 
            "currencyCode": "USD", 
            "priceTotal": 999.98 
          } 
        } 
      } 
    }
  );
```

## Entscheidungsbereiche

`decisionScopes` definiert Abschnitte, Orte oder Teile Ihrer Seiten, in denen Sie ein personalisiertes Erlebnis darstellen möchten. Diese `decisionScopes` sind anpassbar und benutzerdefiniert. Bei aktuellen [!DNL Target]-Kunden werden `decisionScopes` auch als &quot;mboxes&quot;bezeichnet. In der Benutzeroberfläche [!DNL Target] wird `decisionScopes` als &quot;Speicherorte&quot;angezeigt.

## Der Bereich `__view__`

Adobe Experience Platform Web SDK bietet Funktionen, mit denen Sie VEC-Aktionen abrufen können, ohne dabei auf das SDK zurückgreifen zu müssen, um die VEC-Aktionen für Sie wiederzugeben. Senden Sie ein Ereignis mit `__view__`, das als `decisionScopes` definiert ist.

```javascript
alloy("sendEvent", {
      "decisionScopes": ["__view__", "foo", "bar"], 
      "xdm": { 
        "web": { 
          "webPageDetails": { 
            "name": "Home Page"
          }
        } 
      }
    }
  ).then(function(results) {
    for (decision of results.decisions) {
      if (decision.decisionScope === "__view__") {
        console.log(decision.content)
      }
    }
  });
```

## Audiencen in XDM

Beim Definieren von Audiencen für Ihre Zielgruppe-Aktivitäten, die über Adobe Experience Platform Web SDK bereitgestellt werden, muss [XDM](https://docs.adobe.com/content/help/de-DE/experience-platform/xdm/home.html) definiert und verwendet werden. Nachdem Sie XDM-Schema, -Klassen und -Schema-Feldgruppen definiert haben, können Sie eine Zielgruppe-Audience erstellen, die von XDM-Daten für das Targeting definiert wird. Innerhalb der Zielgruppe werden XDM-Daten im Audience Builder als benutzerdefinierter Parameter angezeigt. Das XDM wird mit der Punktnotation serialisiert (z. B. `web.webPageDetails.name`).

Wenn Sie über Aktivitäten zur Zielgruppe mit vordefinierten Audiencen verfügen, die benutzerdefinierte Parameter oder ein benutzerdefiniertes Profil verwenden, werden diese nicht korrekt über das SDK bereitgestellt. Anstatt benutzerdefinierte Parameter oder das Profil zu verwenden, müssen Sie stattdessen XDM verwenden. Es gibt jedoch vordefinierte Audiencen-Targeting-Felder, die über das Adobe Experience Platform Web SDK unterstützt werden und keine XDM-Datei erfordern. Diese Felder sind in der Benutzeroberfläche der Zielgruppe verfügbar, für die kein XDM erforderlich ist:

* Ziel-Bibliothek
* Geo
* Netzwerk
* Operating System
* Seiten der Site
* Browser
* Traffic-Quellen
* Zeitrahmen

## Terminologie

__Entscheidungen:__ In  [!DNL Target]den Beschlüssen wird das Erlebnis, das aus einer Aktivität ausgewählt wurde, korreliert.

__Schema:__ Das Schema einer Entscheidung ist die Art des Angebots in  [!DNL Target].

__Anwendungsbereich:__ Der Anwendungsbereich des Beschlusses. In [!DNL Target] ist der Gültigkeitsbereich die mBox. Die globale mBox ist der Bereich `__view__`.

__XDM:__ Der XDM wird in Punktnotation serialisiert und dann  [!DNL Target] als mBox-Parameter eingefügt.
