---
title: Verwenden von Adobe Target mit dem Platform Web SDK
description: Erfahren Sie, wie Sie personalisierte Inhalte mit dem Experience Platform Web SDK mit Adobe Target rendern
keywords: Target; adobe target; activity.id; experience.id; renderDecisions; DecisionScopes; Vorabausblenden von Snippet; VEC; Form-Based Experience Composer; xdm; Zielgruppen; Entscheidungen; Umfang; Schema;
exl-id: 021171ab-0490-4b27-b350-c37d2a569245
source-git-commit: c3d66e50f647c2203fcdd5ad36ad86ed223733e3
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 3%

---

# Verwenden von Adobe Target mit dem Platform Web SDK

Adobe Experience Platform [!DNL Web SDK] kann in Adobe Target verwaltete personalisierte Erlebnisse für den Webkanal bereitstellen und rendern. Sie können einen WYSIWYG-Editor namens [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC) oder eine nicht visuelle Schnittstelle, den [Form-Based Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html), verwenden, um Aktivitäten und Personalisierungserlebnisse zu erstellen, zu aktivieren und bereitzustellen.

Die folgenden Funktionen wurden getestet und werden derzeit in Target unterstützt:

* A/B-Tests
* A4T-Impressions- und Konversionsberichte
* Automated Personalization
* Erlebnis-Targeting
* Multivarianz-Tests
* Native Target-Impressions- und Konversionsberichte
* VEC-Unterstützung

## Aktivieren von Adobe Target

Gehen Sie wie folgt vor, um [!DNL Target] zu aktivieren:

1. Aktivieren Sie Target in Ihrem [datastream](../../fundamentals/datastreams.md) mit dem entsprechenden Clientcode.
1. Fügen Sie Ihren Ereignissen die Option `renderDecisions` hinzu.

Anschließend können Sie optional auch die folgenden Optionen hinzufügen:

* `decisionScopes`: Rufen Sie bestimmte Aktivitäten ab (nützlich für Aktivitäten, die mit dem formularbasierten Composer erstellt wurden), indem Sie diese Option zu Ihren Ereignissen hinzufügen.
* [Vorabausblenden von Snippets](../manage-flicker.md): Blenden Sie nur bestimmte Teile der Seite aus.

## Verwenden von Adobe Target VEC

Um VEC mit einer Platform Web SDK-Implementierung zu verwenden, installieren und aktivieren Sie entweder die VEC Helper-Erweiterung [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) oder [Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak).

## VEC-Aktivitäten automatisch rendern

Das Adobe Experience Platform Web SDK kann Ihre Erlebnisse, die über den VEC von Adobe Target definiert wurden, automatisch im Internet für Ihre Benutzer rendern. Um dem Adobe Experience Platform Web SDK anzuzeigen, dass VEC-Aktivitäten automatisch gerendert werden sollen, senden Sie ein Ereignis mit `renderDecisions = true`:

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

Der formularbasierte Experience Composer ist eine nicht visuelle Benutzeroberfläche, die zum Konfigurieren von A/B-Tests, [!DNL Experience Targeting]-, Automated Personalization- und Recommendations-Aktivitäten mit verschiedenen Antworttypen wie JSON, HTML, Image usw. nützlich ist. Je nach dem von Adobe Target zurückgegebenen Antworttyp oder der von Ihnen zurückgegebenen Entscheidung kann Ihre Kerngeschäftslogik ausgeführt werden. Um Entscheidungen für Ihre formularbasierten Composer-Aktivitäten abzurufen, senden Sie ein Ereignis mit allen &quot;decisionScopes&quot;, für die Sie eine Entscheidung abrufen möchten.

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

`decisionScopes` definiert Abschnitte, Orte oder Teile Ihrer Seiten, in denen Sie ein personalisiertes Erlebnis rendern möchten. Diese `decisionScopes` sind anpassbar und benutzerdefiniert. Bei aktuellen [!DNL Target]-Kunden werden `decisionScopes` auch als &quot;Mboxes&quot;bezeichnet. In der [!DNL Target]-Benutzeroberfläche wird `decisionScopes` als &quot;Speicherorte&quot;angezeigt.

## Der Bereich `__view__`

Das Adobe Experience Platform Web SDK bietet Funktionen, mit denen Sie VEC-Aktionen abrufen können, ohne sich bei der Wiedergabe der VEC-Aktionen für Sie auf das SDK verlassen zu müssen. Senden Sie ein Ereignis mit `__view__` , das als `decisionScopes` definiert ist.

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

## Zielgruppen in XDM

Beim Definieren von Zielgruppen für Ihre Target-Aktivitäten, die über das Adobe Experience Platform Web SDK bereitgestellt werden, muss [XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=de) definiert und verwendet werden. Nachdem Sie XDM-Schemas, Klassen und Schemafeldgruppen definiert haben, können Sie eine Target-Zielgruppenregel erstellen, die durch XDM-Daten für das Targeting definiert wird. In Target werden XDM-Daten im Audience Builder als benutzerdefinierter Parameter angezeigt. Das XDM wird mit Punktnotation serialisiert (z. B. `web.webPageDetails.name`).

Wenn Sie Target-Aktivitäten mit vordefinierten Zielgruppen haben, die benutzerdefinierte Parameter oder ein Benutzerprofil verwenden, werden diese nicht korrekt über das SDK bereitgestellt. Statt benutzerdefinierte Parameter oder das Benutzerprofil zu verwenden, müssen Sie stattdessen XDM verwenden. Es gibt jedoch native Zielgruppen-Targeting-Felder, die über das Adobe Experience Platform Web SDK unterstützt werden und keine XDM erfordern. Diese Felder sind in der Target-Benutzeroberfläche verfügbar, für die kein XDM erforderlich ist:

* Ziel-Bibliothek
* Geo
* Netzwerk
* Operating System
* Seiten der Site
* Browser
* Traffic-Quellen
* Zeitrahmen

## Terminologie

__Entscheidungen:__ In  [!DNL Target] korrelieren Entscheidungen mit dem Erlebnis, das aus einer Aktivität ausgewählt wird.

__Schema:__ Das Schema einer Entscheidung ist der Angebotstyp in  [!DNL Target].

__Anwendungsbereich:__ Der Anwendungsbereich der Entscheidung. In [!DNL Target] ist der Umfang die mBox. Die globale mBox ist der Bereich `__view__` .

__XDM:__ Das XDM wird in Punktnotation serialisiert und dann  [!DNL Target] als mBox-Parameter eingefügt.
