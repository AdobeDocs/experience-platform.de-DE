---
title: Verwenden von Adobe Target mit dem Platform Web SDK
description: Erfahren Sie, wie Sie personalisierte Inhalte mit dem Experience Platform Web SDK mit Adobe Target rendern
keywords: Target; adobe target; activity.id; experience.id; renderDecisions; DecisionScopes; Vorabausblenden von Snippet; VEC; Form-Based Experience Composer; xdm; Zielgruppen; Entscheidungen; Umfang; Schema;
exl-id: 021171ab-0490-4b27-b350-c37d2a569245
source-git-commit: 202a77e4f9e8c7d5515ea0a5004b1c339f1d58ba
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 3%

---

# Verwenden von [!DNL Adobe Target] mit [!DNL Platform Web SDK]

[!DNL Adobe Experience Platform] [!DNL Web SDK] kann personalisierte Erlebnisse bereitstellen und rendern, die in  [!DNL Adobe Target] dem Webkanal verwaltet werden. Sie können einen WYSIWYG-Editor namens [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC) oder eine nicht visuelle Schnittstelle, den [Form-Based Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html), verwenden, um Aktivitäten und Personalisierungserlebnisse zu erstellen, zu aktivieren und bereitzustellen.

Die folgenden Funktionen wurden getestet und werden derzeit in [!DNL Target] unterstützt:

* [A/B-Tests](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html)
* [A4T-Impressions- und Konversionsberichte](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html)
* [Automated Personalization-Aktivitäten](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [Erlebnis-Targeting-Aktivitäten](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [Multivarianz-Tests (MVT)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html)
* [Native Target-Impressions- und Konversionsberichte](https://experienceleague.adobe.com/docs/target/using/reports/reports.html)
* [VEC-Unterstützung](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)

## Aktivieren von [!DNL Adobe Target]

Gehen Sie wie folgt vor, um [!DNL Target] zu aktivieren:

1. Aktivieren Sie [!DNL Target] in Ihrem [Datastream](../../fundamentals/datastreams.md) mit dem entsprechenden Clientcode.
1. Fügen Sie Ihren Ereignissen die Option `renderDecisions` hinzu.

Anschließend können Sie optional auch die folgenden Optionen hinzufügen:

* **`decisionScopes`**: Rufen Sie bestimmte Aktivitäten ab (nützlich für Aktivitäten, die mit dem formularbasierten Composer erstellt wurden), indem Sie diese Option zu Ihren Ereignissen hinzufügen.
* **[Vorabausblenden von Snippets](../manage-flicker.md)**: Blenden Sie nur bestimmte Teile der Seite aus.

## Verwenden von Adobe Target VEC

Um VEC mit einer [!DNL Platform Web SDK] -Implementierung zu verwenden, installieren und aktivieren Sie entweder die [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) oder die [Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC Helper-Erweiterung.

Weitere Informationen finden Sie unter [Visual Experience Composer Helper Extension](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) im *Adobe Target-Handbuch*.

## VEC-Aktivitäten automatisch rendern

Der [!DNL Adobe Experience Platform Web SDK] bietet die Möglichkeit, Ihre Erlebnisse, die über den VEC von [!DNL Adobe Target] definiert wurden, für Ihre Benutzer automatisch im Internet zu rendern. Um [!DNL Experience Platform Web SDK] anzuzeigen, dass VEC-Aktivitäten automatisch gerendert werden sollen, senden Sie ein Ereignis mit `renderDecisions = true`:

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

Der [Form-Based Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) ist eine nicht visuelle Schnittstelle, die für die Konfiguration von [!UICONTROL A/B-Tests], [!UICONTROL Erlebnis-Targeting], [!UICONTROL Automated Personalization] und [!UICONTROL Recommendations]-Aktivitäten mit verschiedenen Antworttypen nützlich ist, wie JSON, HTML, Bild, Bild, usw. Je nach dem von [!DNL Target] zurückgegebenen Antworttyp oder der von  zurückgegebenen Entscheidung kann Ihre Kerngeschäftslogik ausgeführt werden. Um Entscheidungen für Ihre formularbasierten Composer-Aktivitäten abzurufen, senden Sie ein Ereignis mit allen &quot;decisionScopes&quot;, für die Sie eine Entscheidung abrufen möchten.

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

`decisionScopes` Sie können Abschnitte, Orte oder Teile Ihrer Seiten definieren, in denen Sie ein personalisiertes Erlebnis rendern möchten. Diese `decisionScopes` sind anpassbar und benutzerdefiniert. Bei aktuellen [!DNL Target]-Kunden werden `decisionScopes` auch als &quot;Mboxes&quot;bezeichnet. In der [!DNL Target]-Benutzeroberfläche wird `decisionScopes` als &quot;Speicherorte&quot;angezeigt.

## Der Bereich `__view__`

Der [!DNL Experience Platform Web SDK] bietet Funktionen zum Abrufen von VEC-Aktionen, ohne dass das SDK die VEC-Aktionen für Sie rendern muss. Senden Sie ein Ereignis mit `__view__` , das als `decisionScopes` definiert ist.

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

Beim Definieren von Zielgruppen für Ihre [!DNL Target] -Aktivitäten, die über [!DNL Platform Web SDK] bereitgestellt werden, muss [XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=de) definiert und verwendet werden. Nachdem Sie XDM-Schemas, -Klassen und Schemafeldgruppen definiert haben, können Sie eine [!DNL Target]-Zielgruppenregel erstellen, die von XDM-Daten für das Targeting definiert wird. Innerhalb von [!DNL Target] werden XDM-Daten im [!UICONTROL Audience Builder] als benutzerdefinierter Parameter angezeigt. Das XDM wird mit Punktnotation serialisiert (z. B. `web.webPageDetails.name`).

Wenn Sie über [!DNL Target] -Aktivitäten mit vordefinierten Zielgruppen verfügen, die benutzerdefinierte Parameter oder ein Benutzerprofil verwenden, werden diese nicht korrekt über das SDK bereitgestellt. Statt benutzerdefinierte Parameter oder das Benutzerprofil zu verwenden, müssen Sie stattdessen XDM verwenden. Es gibt jedoch native Zielgruppen-Targeting-Felder, die über [!DNL Platform Web SDK] unterstützt werden und keine XDM erfordern. Diese Felder sind in der [!DNL Target]-Benutzeroberfläche verfügbar, für die kein XDM erforderlich ist:

* Ziel-Bibliothek
* Geo
* Netzwerk
* Operating System
* Seiten der Site
* Browser
* Traffic-Quellen
* Zeitrahmen

Weitere Informationen finden Sie unter [Kategorien für Zielgruppen](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-rules.html?lang=en) im *Adobe Target-Handbuch*.

### Einzelprofil-Update

Mit [!DNL Platform Web SDK] können Sie das Profil als Erlebnisereignis auf das Profil [!DNL Target] und auf das Profil [!DNL Platform Web SDK] aktualisieren.

Um ein [!DNL Target]-Profil zu aktualisieren, stellen Sie sicher, dass die Profildaten wie folgt übergeben werden:

* Unter `“data {“`
* Unter `“__adobe.target”`
* Präfix `“profile.”`, z. B. wie unten

| Schlüssel | Typ | Beschreibung |
| --- | --- | --- |
| `renderDecisions` | Boolesch | Weist die Personalisierungskomponente an, ob DOM-Aktionen interpretiert werden sollen |
| `decisionScopes` | Array `<String>` | Eine Liste der Bereiche, für die Entscheidungen abgerufen werden sollen |
| `xdm` | Objekt | In XDM formatierte Daten, die im Platform Web SDK als Erlebnisereignis landen |
| `data` | Objekt | Beliebige Schlüssel/Wert-Paare, die an [!DNL Target] -Lösungen unter der Zielklasse gesendet werden. |

Der typische [!DNL Platform Web SDK]-Code, der diesen Befehl verwendet, sieht wie folgt aus:

**`sendEvent`mit Profildaten**

```
alloy("sendEvent", {
   renderDecisions: true|false,
   xdm: { // Experience Event XDM data },
   data: { // Freeform stuff (event & profile) }
});
```

**Beispielcode**

```
alloy("sendEvent", {
  renderDecisions: true,
  xdm: {
    device: {
      screenWidth: 9999
    }
  },
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30
      }
    }
  }
}) 
.then(console.log);
```

## Terminologie

__Entscheidungen:__ In  [!DNL Target] korrelieren Entscheidungen mit dem Erlebnis, das aus einer Aktivität ausgewählt wird.

__Schema:__ Das Schema einer Entscheidung ist der Angebotstyp in  [!DNL Target].

__Anwendungsbereich:__ Der Anwendungsbereich der Entscheidung. In [!DNL Target] ist der Umfang die mBox. Die globale mBox ist der Bereich `__view__` .

__XDM:__ Das XDM wird in Punktnotation serialisiert und dann  [!DNL Target] als mBox-Parameter eingefügt.
