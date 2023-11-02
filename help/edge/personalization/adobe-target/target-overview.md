---
title: Verwenden von Adobe Target mit dem Platform Web SDK
description: Erfahren Sie, wie Sie personalisierte Inhalte mit dem Experience Platform Web SDK mit Adobe Target rendern
keywords: Target; adobe target; activity.id; experience.id; renderDecisions; DecisionScopes; Vorabausblenden von Snippet; VEC; Form-Based Experience Composer; xdm; Zielgruppen; Entscheidungen; Umfang; Schema; Systemdiagramm; Diagramm
exl-id: 021171ab-0490-4b27-b350-c37d2a569245
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '1316'
ht-degree: 7%

---

# Verwenden [!DNL Adobe Target] mit dem [!DNL Platform Web SDK]

[!DNL Adobe Experience Platform] [!DNL Web SDK] kann personalisierte Erlebnisse bereitstellen und rendern, die in verwaltet werden [!DNL Adobe Target] zum Webkanal hinzu. Sie können einen WYSIWYG-Editor mit dem Namen [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC) oder einer nicht visuellen Benutzeroberfläche, der [Form-Based Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=de), um Ihre Aktivitäten und Personalisierungserlebnisse zu erstellen, zu aktivieren und bereitzustellen.

>[!IMPORTANT]
>
>Erfahren Sie, wie Sie Ihre Target-Implementierung mit dem [Migrieren von Target von at.js 2.x zum Platform Web SDK](https://experienceleague.adobe.com/docs/platform-learn/migrate-target-to-websdk/introduction.html?lang=de) Tutorial.
>
>Erfahren Sie, wie Sie Target zum ersten Mal mit der [Implementieren von Adobe Experience Cloud mit dem Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=de) Tutorial. Spezifische Informationen zu Target finden Sie im Tutorial-Abschnitt mit dem Titel [Target mit dem Platform Web SDK einrichten](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html).


Die folgenden Funktionen wurden getestet und werden derzeit in [!DNL Target]:

* [A/B-Tests](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html)
* [A4T-Impressions- und Konversionsberichte](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=de)
* [Automated Personalization-Aktivitäten](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [Erlebnis-Targeting-Aktivitäten](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [Multivarianz-Tests (MVT)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html)
* [Recommendations-Aktivitäten](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html)
* [Native Target-Impressions- und Konversionsberichte](https://experienceleague.adobe.com/docs/target/using/reports/reports.html)
* [VEC-Unterstützung](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)

## [!DNL Platform Web SDK] Systemdiagramm

Das folgende Diagramm hilft Ihnen, den Workflow von [!DNL Target] und [!DNL Platform Web SDK] Edge-Entscheidung.

![Abbildung der Adobe Target-Edge-Entscheidung mit dem Platform Web SDK](./assets/target-platform-web-sdk.png)

| Aufruf | Details |
| --- | --- |
| 1 | Das Gerät lädt die [!DNL Platform Web SDK]. Die [!DNL Platform Web SDK] sendet eine Anfrage mit XDM-Daten, der ID der Datastreams-Umgebung, übergebenen Parametern und der Kunden-ID (optional) an das Edge-Netzwerk. Seite (oder Container) ist vorab ausgeblendet. |
| 2 | Das Edge-Netzwerk sendet die Anfrage an die Edge-Dienste, um sie mit der Besucher-ID, der Zustimmung und anderen Besucherkontextinformationen wie Geolocation und gerätefreundlichen Namen anzureichern. |
| 3 | Das Edge-Netzwerk sendet die angereicherte Personalisierungsanforderung an die [!DNL Target] -Edge mit der Besucher-ID und den übergebenen Parametern. |
| 4 | Profilskripte werden ausgeführt und anschließend in [!DNL Target] Profilspeicherung. Der Profilspeicher ruft Segmente aus der [!UICONTROL Zielgruppenbibliothek] (z. B. Segmente, die von [!DNL Adobe Analytics], [!DNL Adobe Audience Manager], die [!DNL Adobe Experience Platform]). |
| 5 | Basierend auf URL-Anforderungsparametern und Profildaten, [!DNL Target] bestimmt, welche Aktivitäten und Erlebnisse dem Besucher für die aktuelle Seitenansicht und für künftige vorab abgerufene Ansichten angezeigt werden. [!DNL Target] sendet diese dann zurück an das Edge-Netzwerk. |
| 6 | a. Das Edge-Netzwerk sendet die Personalisierungsantwort zurück an die Seite, optional einschließlich der Profilwerte für eine zusätzliche Personalisierung. Personalisierte Inhalte auf der aktuellen Seite werden so schnell wie möglich bereitgestellt, ohne dass Standardinhalte aufflackern.<br>b. Personalisierte Inhalte für Ansichten, die als Ergebnis von Benutzeraktionen in einer Einzelseiten-App (SPA) angezeigt werden, werden zwischengespeichert und können sofort ohne zusätzlichen Server-Aufruf angewendet werden, wenn die Ansichten ausgelöst werden. <br>c. Das Edge-Netzwerk sendet die Besucher-ID und andere Werte in Cookies, z. B. Zustimmung, Sitzungs-ID, Identität, Cookie-Prüfung, Personalisierung usw. |
| 7 | Das Edge-Netzwerk nach vorne [!UICONTROL Analytics for Target] (A4T) Details (Aktivitäts-, Erlebnis- und Konversionsmetadaten) in die [!DNL Analytics] -Kante. |

## Aktivieren [!DNL Adobe Target]

Aktivieren [!DNL Target]führen Sie folgende Schritte aus:

1. Aktivieren [!DNL Target] in [datastream](../../../datastreams/overview.md) mit dem entsprechenden Clientcode.
1. Fügen Sie die `renderDecisions` -Option zu Ihren Ereignissen hinzufügen.

Anschließend können Sie optional auch die folgenden Optionen hinzufügen:

* **`decisionScopes`**: Rufen Sie bestimmte Aktivitäten ab (nützlich für Aktivitäten, die mit dem formularbasierten Composer erstellt wurden), indem Sie diese Option zu Ihren Ereignissen hinzufügen.
* **[Vorabausblenden eines Snippets](../manage-flicker.md)**: Blendet nur bestimmte Teile der Seite aus.

## Verwenden von Adobe Target VEC

So verwenden Sie VEC mit einer [!DNL Platform Web SDK] Implementierung, Installation und Aktivierung der [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) oder [Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC Helper-Erweiterung.

Weitere Informationen finden Sie unter [Visual Experience Composer Helper-Erweiterung](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) im *Adobe Target-Handbuch*.

## Rendern von personalisiertem Inhalt

Siehe [Rendern von Personalisierungsinhalten](../rendering-personalization-content.md) für weitere Informationen.

## Zielgruppen in XDM

Beim Definieren von Zielgruppen für Ihre [!DNL Target] Aktivitäten, die über die [!DNL Platform Web SDK], [XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html) müssen definiert und verwendet werden. Nachdem Sie XDM-Schemas, Klassen und Schemafeldgruppen definiert haben, können Sie eine [!DNL Target] Zielgruppenregel, die durch XDM-Daten für das Targeting definiert wird. Within [!DNL Target], werden XDM-Daten in der [!UICONTROL Audience Builder] als benutzerdefinierten Parameter. Das XDM wird mit Punktnotation serialisiert (z. B. `web.webPageDetails.name`).

Wenn Sie [!DNL Target] Aktivitäten mit vordefinierten Zielgruppen, die benutzerdefinierte Parameter oder ein Benutzerprofil verwenden, werden nicht korrekt über das SDK bereitgestellt. Statt benutzerdefinierte Parameter oder das Benutzerprofil zu verwenden, müssen Sie stattdessen XDM verwenden. Es werden jedoch native Zielgruppen-Targeting-Felder über die [!DNL Platform Web SDK] die kein XDM erfordern. Diese Felder sind im Abschnitt [!DNL Target] Benutzeroberfläche, die kein XDM erfordert:

* Ziel-Bibliothek
* Geo
* Netzwerk
* Operating System
* Seiten der Site
* Browser
* Traffic-Quellen
* Zeitrahmen

Weitere Informationen finden Sie unter [Kategorien für Zielgruppen](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-rules.html) im *Adobe Target-Handbuch*.

### Antwort-Token

Antwort-Token werden hauptsächlich zum Senden von Metadaten an Dritte wie Google, Facebook usw. verwendet. Antwort-Token werden im `meta` -Feld in `propositions` -> `items`. Im Folgenden finden Sie ein Beispiel:

```json
{
  "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI2NzM2IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
  "scope": "__view__",
  "scopeDetails": ...,
  "renderAttempted": true,
  "items": [
    {
      "id": "0",
      "schema": "https://ns.adobe.com/personalization/dom-action",
      "meta": {
        "experience.id": "0",
        "activity.id": "126736",
        "offer.name": "Default Content",
        "offer.id": "0"
      }
    }
  ]
}
```

Um die Antwort-Token zu erfassen, müssen Sie sich für `alloy.sendEvent` Versprechen, durchlaufen `propositions`
und extrahieren Sie Details aus `items` -> `meta`. Alle `proposition` hat eine `renderAttempted` boolesches Feld, das angibt, ob das `proposition` gerendert wurde oder nicht. Siehe Beispiel unten:

```js
alloy("sendEvent",
  {
    renderDecisions: true,
    decisionScopes: [
      "hero-container"
    ]
  }).then(result => {
    const { propositions } = result;

    // filter rendered propositions
    const renderedPropositions = propositions.filter(proposition => proposition.renderAttempted === true);

    // collect the item metadata that represents the response tokens
    const collectMetaData = (items) => {
      return items.filter(item => item.meta !== undefined).map(item => item.meta);
    }

    const pageLoadResponseTokens = renderedPropositions
      .map(proposition => collectMetaData(proposition.items))
      .filter(e => e.length > 0)
      .flatMap(e => e);
  });
  
```

Wenn das automatische Rendering aktiviert ist, enthält das Vorschlagsarray:

#### Beim Laden der Seite:

* Form-Based Composer-basiert `propositions` mit `renderAttempted` Markierung gesetzt auf `false`
* Visual Experience Composer-basierte Vorschläge mit `renderAttempted` Markierung gesetzt auf `true`
* Visual Experience Composer-basierte Vorschläge für eine Einzelseiten-Anwendungsansicht mit `renderAttempted` Markierung gesetzt auf `true`

#### On View - change (für zwischengespeicherte Ansichten):

* Visual Experience Composer-basierte Vorschläge für eine Einzelseiten-Anwendungsansicht mit `renderAttempted` Markierung gesetzt auf `true`

Wenn das automatische Rendering deaktiviert ist, enthält das Vorschlagsarray:

#### Beim Laden der Seite:

* Formularbasierter Composer basierend `propositions` mit `renderAttempted` Markierung gesetzt auf `false`
* Visual Experience Composer-basierte Vorschläge mit `renderAttempted` Markierung gesetzt auf `false`
* Visual Experience Composer-basierte Vorschläge für eine Einzelseiten-Anwendungsansicht mit `renderAttempted` Markierung gesetzt auf `false`

#### On View - change (für zwischengespeicherte Ansichten):

* Visual Experience Composer-basierte Vorschläge für eine Einzelseiten-Anwendungsansicht mit `renderAttempted` Markierung gesetzt auf `false`

### Einzelprofil-Update

Die [!DNL Platform Web SDK] ermöglicht die Aktualisierung des Profils auf [!DNL Target] und dem [!DNL Platform Web SDK] als Erlebnisereignis.

So aktualisieren Sie eine [!DNL Target] Profil erstellen, müssen Sie sicherstellen, dass die Profildaten mit Folgendem übergeben werden:

* Unter `"data {"`
* Unter `"__adobe.target"`
* Präfix `"profile."` z. B. wie folgt

| Schlüssel | Typ | Beschreibung |
| --- | --- | --- |
| `renderDecisions` | Boolesch | Weist die Personalisierungskomponente an, ob DOM-Aktionen interpretiert werden sollen |
| `decisionScopes` | Array `<String>` | Eine Liste der Bereiche, für die Entscheidungen abgerufen werden sollen |
| `xdm` | Objekt | In XDM formatierte Daten, die im Platform Web SDK als Erlebnisereignis landen |
| `data` | Objekt | Beliebige Schlüssel/Wert-Paare, die an gesendet werden [!DNL Target] Lösungen unter der Zielklasse. |

Typisch [!DNL Platform Web SDK] Code, der diesen Befehl verwendet, sieht wie folgt aus:

**`sendEvent`mit Profildaten**

```js
alloy("sendEvent", {
   renderDecisions: true|false,
   xdm: { // Experience Event XDM data },
   data: { // Freeform data }
});
```

**So senden Sie Profilattribute an Adobe Target:**

```js
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30
      }
    }
  }
});
```

## Empfehlungen anfordern

Die folgende Tabelle enthält [!DNL Recommendations] -Attribute und darüber, ob jede dieser Attribute über die [!DNL Platform Web SDK]:

| Kategorie | Attribut | Unterstützungsstatus |
| --- | --- | --- |
| Recommendations - Standardattribute der Entität | entity.id | Unterstützt |
|  | entity.name | Unterstützt |
|  | entity.categoryId | Unterstützt |
|  | entity.pageUrl | Unterstützt |
|  | entity.thumbnailUrl | Unterstützt |
|  | entity.message | Unterstützt |
|  | entity.value | Unterstützt |
|  | entity.inventory | Unterstützt |
|  | entity.brand | Unterstützt |
|  | entity.margin | Unterstützt |
|  | entity.event.detailsOnly | Unterstützt |
| Recommendations - Benutzerdefinierte Entitätsattribute | entity.yourCustomAttributeName | Unterstützt |
| Recommendations - Reservierte Mbox-/Seitenparameter | excludedIds | Unterstützt |
|  | cartIds | Unterstützt |
|  | productPurchasedId | Unterstützt |
| Seiten- oder Elementkategorie für Kategorieaffinität | user.categoryId | Unterstützt |

**So senden Sie Recommendations-Attribute an Adobe Target:**

```js
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "entity.id": "123",
        "entity.genre": "Drama"
      }
    }
  }
});
```

## Debugging

mboxTrace und mboxDebug werden nicht mehr unterstützt. Verwendung [[!DNL Platform Web SDK] Debugging](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/debugging.html).

## Terminologie

__Vorschläge:__ In [!DNL Target], korrelieren Vorschläge mit dem Erlebnis, das aus einer Aktivität ausgewählt wird.

__Schema:__ Das Schema einer Entscheidung ist der Angebotstyp in [!DNL Target].

__Umfang:__ Der Anwendungsbereich der Entscheidung. In [!DNL Target], ist der Bereich die mBox. Die globale mBox ist die `__view__` Umfang.

__XDM:__ Das XDM wird in Punktnotation serialisiert und dann in [!DNL Target] als mBox-Parameter.
