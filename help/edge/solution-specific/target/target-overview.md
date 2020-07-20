---
title: 'Adobe Target und Adobe Experience Platform Web SDK. '
seo-title: Adobe Experience Platform Web SDK und Verwendung von Adobe Target
description: Erfahren Sie, wie Sie personalisierte Inhalte mit Experience Platform Web SDK mit Adobe Target rendern
seo-description: Erfahren Sie, wie Sie personalisierte Inhalte mit Experience Platform Web SDK mit Adobe Target rendern
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 5%

---


# [!DNL Target] Übersicht

Die Adobe Experience Platform [!DNL Web SDK] kann personalisierte Erlebnisse bereitstellen und rendern, die in Adobe Target für den Web-Kanal verwaltet werden. Sie können einen WYSIWYG-Editor, den so genannten [Visual Experience Composer](https://docs.adobe.com/content/help/en/target/using/experiences/vec/visual-experience-composer.html) (VEC), oder eine nicht visuelle Schnittstelle, den [Form-Based Experience Composer](https://docs.adobe.com/content/help/de-DE/target/using/experiences/form-experience-composer.html), verwenden, um Ihre Aktivitäten und Personalisierungserlebnisse zu erstellen, zu aktivieren und bereitzustellen.

## Adobe Target aktivieren

Zur Aktivierung [!DNL Target]müssen Sie folgende Schritte ausführen:

1. Aktivieren Sie die Aktivität.id- und Experience.id-Antwort-Token in der [!DNL Target] Benutzeroberfläche.

![Zielgruppe_Antwort_Token](../../solution-specific/target/assets/target_response_token.png)

1. Aktivieren Sie die Zielgruppe in Ihrer [Edge-Konfiguration](../../fundamentals/edge-configuration.md) mit dem entsprechenden Clientcode.
1. Hinzufügen Sie die `renderDecisions` Option auf Ihre Ereignis.

Dann können Sie optional auch:

* Hinzufügen Sie `decisionScopes` Ihre Ereignis an, um bestimmte Aktivitäten abzurufen (nützlich für Aktivitäten, die mit dem formularbasierten Composer erstellt wurden).
* Hinzufügen Sie das [Ausblendungsfragment](../../solution-specific/target/flicker-management.md) , um nur bestimmte Teile der Seite auszublenden.

## Verwenden des Adobe Target VEC

Mit dem SDK können Sie VEC normalerweise mit einer Ausnahme verwenden: Sie benötigen die [Zielgruppe VEC Helper Extension](https://docs.adobe.com/content/help/en/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) installiert und aktiv.

## VEC-Aktivitäten automatisch rendern

Das AEP Web SDK ist befugt, Ihre Erlebnisse, die über den VEC von Adobe Target im Web definiert werden, automatisch für Ihre Benutzer darzustellen. Um dem AEP Web SDK anzuzeigen, dass VEC-Aktivitäten automatisch gerendert werden sollen, senden Sie ein Ereignis mit `renderDecisions = true`:

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

Der formularbasierte Experience Composer ist eine nicht visuelle Benutzeroberfläche, die zum Konfigurieren von A/B-Tests, [!DNL Experience Targeting]automatisierter Personalisierung und Recommendations-Aktivitäten mit verschiedenen Antworttypen wie JSON, HTML, Image usw. nützlich ist. Abhängig vom Antworttyp oder der von Adobe Target zurückgegebenen Entscheidung kann Ihre Kerngeschäftslogik ausgeführt werden. Um Entscheidungen für Ihre formularbasierten Composer-Aktivitäten abzurufen, senden Sie ein Ereignis mit allen &quot;DecisionScopes&quot;, für die Sie eine Entscheidung abrufen möchten.

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

`decisionScopes` definiert Abschnitte, Orte oder Teile Ihrer Seiten, in denen Sie ein personalisiertes Erlebnis darstellen möchten. Diese `decisionScopes` sind benutzerdefiniert und anpassbar. Für aktuelle [!DNL Target] Kunden `decisionScopes` werden auch &quot;mboxes&quot;genannt. In der [!DNL Target] Benutzeroberfläche wird `decisionScopes` &quot;Speicherorte&quot;angezeigt.

## __Ansicht__ - Anwendungsbereich

AEP [!DNL Web SDK] bietet eine Funktion, mit der Sie VEC-Aktionen abrufen können, ohne sich auf AEP verlassen zu müssen, um die VEC-Aktionen für Sie [!DNL Web SDK] zu rendern. Senden Sie ein Ereignis mit der `__view__` Definition als `decisionScopes`.

```javascript
alloy("sendEvent", {
  decisionScopes: [“__view__”,"foo", "bar"], 
  "xdm": { 
    "web": { 
      "webPageDetails": { 
        "name": "Home Page"
       }
      } 
     }
    }
   ).then(results){
  for (decision of results.decisions){
     if(decision.decisionScope == "__view__")
       console.log(decision.content)
}
};
```

## Audiencen in XDM

Beim Definieren von Audiencen für Ihre Zielgruppe-Aktivitäten, die über das AEP Web SDK bereitgestellt werden, muss [XDM](https://docs.adobe.com/content/help/de-DE/experience-platform/xdm/home.html) definiert und verwendet werden. Nachdem Sie XDM-Schema, -Klassen und -Mixins definiert haben, können Sie eine Zielgruppe-Audience erstellen, die von XDM-Daten für das Targeting definiert wird. Innerhalb der Zielgruppe werden XDM-Daten im Audience Builder als benutzerdefinierter Parameter angezeigt. Das XDM wird mit der Punktnotation serialisiert (z. B. `web.webPageDetails.name`).

Wenn Sie über Aktivitäten zur Zielgruppe mit vordefinierten Audiencen verfügen, die benutzerdefinierte Parameter oder ein Profil verwenden, beachten Sie, dass diese nicht korrekt über das AEP Web SDK bereitgestellt werden. Anstatt benutzerdefinierte Parameter oder das Profil zu verwenden, müssen Sie stattdessen XDM verwenden. Es gibt jedoch vordefinierte Audiencen-Targeting-Felder, die über das AEP Web SDK unterstützt werden und keine XDM-Datei erfordern. Diese Felder stehen in der Benutzeroberfläche der Zielgruppe zur Verfügung, für die kein XDM erforderlich ist:

* Ziel-Bibliothek
* Geo
* Netzwerk
* Betriebssystem
* Seiten der Site
* Browser
* Traffic-Quellen
* Zeitrahmen

## Terminologie

__Entscheidungen__ - Diese entsprechen [!DNL Target]dem Erlebnis, das aus einer Aktivität ausgewählt wurde.

__Anwendungsbereich__ - Der Anwendungsbereich des Beschlusses. Das ist [!DNL Target]die mBox. Die globale mBox ist der `__view__` Anwendungsbereich.

__Schema__ - Das Schema einer Entscheidung ist die Art des Angebots in [!DNL Target].

__XDM__ - Der XDM wird in Punktnotation serialisiert und dann [!DNL Target] als mBox-Parameter eingefügt.
