---
title: Verwenden von Adobe Target mit dem Platform Web SDK
description: Erfahren Sie, wie Sie personalisierte Inhalte mit dem Experience Platform Web SDK mit Adobe Target rendern
keywords: Target; adobe target; activity.id; experience.id; renderDecisions; DecisionScopes; Vorabausblenden von Snippet; VEC; Form-Based Experience Composer; xdm; Zielgruppen; Entscheidungen; Umfang; Schema; Systemdiagramm; Diagramm
exl-id: 021171ab-0490-4b27-b350-c37d2a569245
source-git-commit: 930756b4e10c42edf2d58be16c51d71df207d1af
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 6%

---

# Verwenden von [!DNL Adobe Target] mit [!DNL Platform Web SDK]

[!DNL Adobe Experience Platform] [!DNL Web SDK] kann personalisierte Erlebnisse bereitstellen und rendern, die in  [!DNL Adobe Target] dem Webkanal verwaltet werden. Sie können einen WYSIWYG-Editor namens [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC) oder eine nicht visuelle Schnittstelle, den [Form-Based Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html), verwenden, um Aktivitäten und Personalisierungserlebnisse zu erstellen, zu aktivieren und bereitzustellen.

>[!IMPORTANT]
>
>Die [Adobe Target-Dokumentation](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/aep-implementation/aep-web-sdk.html?lang=en) enthält Themen mit spezifischen Informationen zum Platform Web SDK, da sie sich auf Target-Funktionen bezieht.

Die folgenden Funktionen wurden getestet und werden derzeit in [!DNL Target] unterstützt:

* [A/B-Tests](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html)
* [A4T-Impressions- und Konversionsberichte](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=de)
* [Automated Personalization-Aktivitäten](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [Erlebnis-Targeting-Aktivitäten](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [Multivarianz-Tests (MVT)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html)
* [Recommendations-Aktivitäten](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html)
* [Native Target-Impressions- und Konversionsberichte](https://experienceleague.adobe.com/docs/target/using/reports/reports.html)
* [VEC-Unterstützung](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)

## [!DNL Platform Web SDK] Systemdiagramm

Das folgende Diagramm veranschaulicht den Arbeitsablauf der Edge-Entscheidungsfindung von [!DNL Target] und [!DNL Platform Web SDK].

![Abbildung der Adobe Target-Edge-Entscheidung mit dem Platform Web SDK](./assets/target-platform-web-sdk.png)

| Aufruf | Details |
| --- | --- |
| 1 | Das Gerät lädt [!DNL Platform Web SDK]. [!DNL Platform Web SDK] sendet eine Anfrage mit XDM-Daten, der DataStreams-Umgebungs-ID, den übergebenen Parametern und der Kunden-ID (optional) an das Edge-Netzwerk. Seite (oder Container) ist vorab ausgeblendet. |
| 2 | Das Edge-Netzwerk sendet die Anfrage an die Edge-Dienste, um sie mit der Besucher-ID, der Zustimmung und anderen Besucherkontextinformationen wie Geolocation und gerätefreundlichen Namen anzureichern. |
| 3 | Das Edge-Netzwerk sendet die angereicherte Personalisierungsanforderung an den [!DNL Target] -Edge mit der Besucher-ID und den übergebenen Parametern. |
| 4 | Profilskripte werden ausgeführt und dann in den Profilspeicher [!DNL Target] eingespeist. Der Profilspeicher ruft Segmente aus der [!UICONTROL Zielgruppenbibliothek] ab (z. B. Segmente, die von [!DNL Adobe Analytics], [!DNL Adobe Audience Manager], [!DNL Adobe Experience Platform] freigegeben wurden). |
| 5 | Basierend auf URL-Anforderungsparametern und Profildaten bestimmt [!DNL Target], welche Aktivitäten und Erlebnisse für den Besucher für die aktuelle Seitenansicht und für künftige vorab abgerufene Ansichten angezeigt werden sollen. [!DNL Target] sendet diese dann zurück an das Edge-Netzwerk. |
| 6 | a. Das Edge-Netzwerk sendet die Personalisierungsantwort zurück an die Seite, optional einschließlich der Profilwerte für eine zusätzliche Personalisierung. Personalisierte Inhalte auf der aktuellen Seite werden so schnell wie möglich bereitgestellt, ohne dass Standardinhalte aufflackern.<br>b. Personalisierte Inhalte für Ansichten, die als Ergebnis von Benutzeraktionen in einer Einzelseiten-App (SPA) angezeigt werden, werden zwischengespeichert und können sofort ohne zusätzlichen Server-Aufruf angewendet werden, wenn die Ansichten ausgelöst werden. <br>c. Das Edge-Netzwerk sendet die Besucher-ID und andere Werte in Cookies, z. B. Zustimmung, Sitzungs-ID, Identität, Cookie-Prüfung, Personalisierung usw. |
| 7 | Das Edge-Netzwerk leitet [!UICONTROL Analytics for Target] (A4T)-Details (Aktivitäts-, Erlebnis- und Konversionsmetadaten) an den [!DNL Analytics]-Edge weiter. |

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

## Rendern von personalisiertem Inhalt

Weitere Informationen finden Sie unter [Rendern von Personalisierungsinhalten](../rendering-personalization-content.md) .

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

### Antwort-Token

Antwort-Token werden hauptsächlich zum Senden von Metadaten an Dritte wie Google, Facebook usw. verwendet. Antwort-Token werden zurückgegeben
im Feld `meta` in `propositions` -> `items`. Hier finden Sie ein Beispiel:

```
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

Um die Antwort-Token zu erfassen, müssen Sie das `alloy.sendEvent`-Versprechen abonnieren, durch `propositions` iterieren
und extrahieren Sie die Details aus `items` -> `meta`. Jedes `proposition` hat ein boolesches `renderAttempted` -Feld.
gibt an, ob `proposition` gerendert wurde oder nicht. Siehe Beispiel unten:

```
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

* Form-Based Composer based `propositions` , wobei die `renderAttempted`-Markierung auf `false` gesetzt ist
* Visual Experience Composer-basierte Vorschläge mit `renderAttempted`-Markierung auf `true` gesetzt
* Visual Experience Composer-basierte Vorschläge für eine Einzelseiten-Anwendungsansicht mit der Markierung `renderAttempted`, die auf `true` gesetzt ist

#### On View - change (für zwischengespeicherte Ansichten):

* Visual Experience Composer-basierte Vorschläge für eine Einzelseiten-Anwendungsansicht mit der Markierung `renderAttempted`, die auf `true` gesetzt ist

Wenn das automatische Rendering deaktiviert ist, enthält das Vorschlagsarray:

#### Beim Laden der Seite:

* Form-Based Composer based `propositions` , wobei die `renderAttempted`-Markierung auf `false` gesetzt ist
* Visual Experience Composer-basierte Vorschläge mit `renderAttempted`-Markierung auf `false` gesetzt
* Visual Experience Composer-basierte Vorschläge für eine Einzelseiten-Anwendungsansicht mit der Markierung `renderAttempted`, die auf `false` gesetzt ist

#### On View - change (für zwischengespeicherte Ansichten):

* Visual Experience Composer-basierte Vorschläge für eine Einzelseiten-Anwendungsansicht mit der Markierung `renderAttempted`, die auf `false` gesetzt ist

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
   data: { // Freeform data }
});
```

**So senden Sie Profilattribute an Adobe Target:**

```
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

In der folgenden Tabelle sind die [!DNL Recommendations]-Attribute aufgeführt und es wird angezeigt, ob die einzelnen Attribute über [!DNL Platform Web SDK] unterstützt werden:

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

```
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "entity.id" : "123",
        "entity.genre" : "Drama"
      }
    }
  }
});
```

## Debugging

mboxTrace und mboxDebug werden nicht mehr unterstützt. Verwenden Sie [[!DNL Platform Web SDK] debugging](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/debugging.html).

## Terminologie

__Vorschläge:__ In  [!DNL Target]korrelieren Vorschläge mit dem Erlebnis, das aus einer Aktivität ausgewählt wird.

__Schema:__ Das Schema einer Entscheidung ist der Angebotstyp in  [!DNL Target].

__Anwendungsbereich:__ Der Anwendungsbereich der Entscheidung. In [!DNL Target] ist der Umfang die mBox. Die globale mBox ist der Bereich `__view__` .

__XDM:__ Das XDM wird in Punktnotation serialisiert und dann  [!DNL Target] als mBox-Parameter eingefügt.
