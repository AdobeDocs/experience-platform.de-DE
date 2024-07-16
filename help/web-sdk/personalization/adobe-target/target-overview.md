---
title: Adobe Target mit Web SDK für Personalisierung verwenden
description: Erfahren Sie, wie Sie personalisierte Inhalte mit dem Experience Platform Web SDK mit Adobe Target rendern
exl-id: 021171ab-0490-4b27-b350-c37d2a569245
source-git-commit: 69406293dce5fdfc832adff801f1991626dafae0
workflow-type: tm+mt
source-wordcount: '1345'
ht-degree: 3%

---

# Verwenden Sie [!DNL Adobe Target] und [!DNL Web SDK] für die Personalisierung

[!DNL Adobe Experience Platform] [!DNL Web SDK] kann personalisierte Erlebnisse, die in [!DNL Adobe Target] verwaltet werden, für den Webkanal bereitstellen und rendern. Sie können einen WYSIWYG-Editor namens [Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC) oder eine nicht visuelle Schnittstelle, den [formularbasierten Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=de), verwenden, um Aktivitäten und Personalisierungserlebnisse zu erstellen, zu aktivieren und bereitzustellen.

>[!IMPORTANT]
>
>Erfahren Sie, wie Sie Ihre Target-Implementierung mit dem Tutorial [Migration von Target von at.js 2.x zum Platform Web SDK](https://experienceleague.adobe.com/docs/platform-learn/migrate-target-to-websdk/introduction.html) in das Platform Web SDK migrieren.
>
>Erfahren Sie, wie Sie Target zum ersten Mal mit dem Tutorial [Adobe Experience Cloud mit Web SDK implementieren](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=de) implementieren. Spezifische Informationen zu Target finden Sie im Tutorial-Abschnitt mit dem Titel [Einrichten von Target mit Platform Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html) .


Die folgenden Funktionen wurden getestet und werden derzeit in [!DNL Target] unterstützt:

* [A/B-Tests](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html)
* [A4T-Impressions- und Konversionsberichte](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html)
* [Automated Personalization-Aktivitäten](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [Erlebnis-Targeting-Aktivitäten](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [Multivarianz-Tests (MVT)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html)
* [Recommendations-Aktivitäten](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html)
* [Native Target-Impressions- und Konversionsberichte](https://experienceleague.adobe.com/docs/target/using/reports/reports.html)
* [VEC-Unterstützung](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)

## [!DNL Web SDK] Systemdiagramm

Das folgende Diagramm veranschaulicht den Arbeitsablauf der Edge-Entscheidungsfindung von [!DNL Target] und [!DNL Web SDK].

![Diagramm der Adobe Target-Edge-Entscheidung mit dem Platform Web SDK](assets/target-platform-web-sdk-new.png)

| Aufruf | Details |
| --- | --- |
| 1 | Das Gerät lädt den [!DNL Web SDK]. Der [!DNL Web SDK] sendet eine Anfrage mit XDM-Daten, der ID der Datastreams-Umgebung, den übergebenen Parametern und der Kunden-ID (optional) an das Edge Network. Seite (oder Container) ist vorab ausgeblendet. |
| 2 | Das Edge Network sendet die Anfrage an die Edge-Dienste, um sie mit der Besucher-ID, der Zustimmung und anderen Besucherkontextinformationen wie Geolocation und gerätefreundlichen Namen anzureichern. |
| 3 | Das Edge Network sendet die angereicherte Personalisierungsanforderung mit der Besucher-ID und den übergebenen Parametern an den [!DNL Target] -Edge. |
| 4 | Profilskripte werden ausgeführt und dann in den [!DNL Target] -Profilspeicher eingespeist. Der Profilspeicher ruft Segmente aus der [!UICONTROL Zielgruppenbibliothek] ab (z. B. Segmente, die aus [!DNL Adobe Analytics], [!DNL Adobe Audience Manager] und dem [!DNL Adobe Experience Platform] freigegeben wurden). |
| 5 | Basierend auf URL-Anforderungsparametern und Profildaten bestimmt [!DNL Target], welche Aktivitäten und Erlebnisse für den Besucher für die aktuelle Seitenansicht und für künftige vorab abgerufene Ansichten angezeigt werden sollen. [!DNL Target] sendet dies dann zurück an das Edge Network. |
| 6 | a. Das Edge Network sendet die Personalisierungsantwort zurück an die Seite, optional einschließlich der Profilwerte für eine zusätzliche Personalisierung. Personalisierte Inhalte auf der aktuellen Seite werden so schnell wie möglich bereitgestellt, ohne dass Standardinhalte aufflackern.<br>b. Personalisierte Inhalte für Ansichten, die als Ergebnis von Benutzeraktionen in einer Einzelseiten-App (SPA) angezeigt werden, werden zwischengespeichert und können sofort ohne zusätzlichen Server-Aufruf angewendet werden, wenn die Ansichten ausgelöst werden. <br>c. Das Edge Network sendet die Besucher-ID und andere Werte in Cookies, z. B. Zustimmung, Sitzungs-ID, Identität, Cookie-Prüfung, Personalisierung. |
| 7 | Das Web SDK sendet die Benachrichtigung vom Gerät an das Edge Network. |
| 8 | Das Edge Network leitet [!UICONTROL Analytics for Target] (A4T)-Details (Aktivitäts-, Erlebnis- und Konversionsmetadaten) an den [!DNL Analytics] -Edge weiter. |

## Aktivieren von [!DNL Adobe Target]

Gehen Sie wie folgt vor, um [!DNL Target] zu aktivieren:

1. Aktivieren Sie [!DNL Target] in Ihrem [datastream](../../../datastreams/overview.md) mit dem entsprechenden Clientcode.
1. Fügen Sie Ihren Ereignissen die Option `renderDecisions` hinzu.

Anschließend können Sie optional auch die folgenden Optionen hinzufügen:

* **`decisionScopes`**: Rufen Sie bestimmte Aktivitäten ab (nützlich für Aktivitäten, die mit dem formularbasierten Composer erstellt wurden), indem Sie diese Option zu Ihren Ereignissen hinzufügen.
* **[Codeausschnitt vorab ausblenden](../manage-flicker.md)**: Blendet nur bestimmte Teile der Seite aus.

## Verwenden von Adobe Target VEC

Um VEC mit einer Implementierung vom Typ [!DNL Web SDK] zu verwenden, installieren und aktivieren Sie entweder die VEC Helper-Erweiterung [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) oder die VEC Helper-Erweiterung [Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) .

Weitere Informationen finden Sie unter [Visual Experience Composer Helper Extension](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) im *Adobe Target-Handbuch*.

## Rendern von personalisiertem Inhalt

Weitere Informationen finden Sie unter [Rendern von Personalisierungsinhalten](../rendering-personalization-content.md) .

## Zielgruppen in XDM

Beim Definieren von Zielgruppen für Ihre [!DNL Target] -Aktivitäten, die über [!DNL Web SDK] bereitgestellt werden, muss [XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=de) definiert und verwendet werden. Nachdem Sie XDM-Schemas, Klassen und Schemafeldgruppen definiert haben, können Sie eine [!DNL Target]-Zielgruppenregel erstellen, die von XDM-Daten für das Targeting definiert wird. Innerhalb von [!DNL Target] werden XDM-Daten im [!UICONTROL Audience Builder] als benutzerdefinierter Parameter angezeigt. Das XDM wird mit Punktnotation serialisiert (z. B. `web.webPageDetails.name`).

Wenn Sie über [!DNL Target] -Aktivitäten mit vordefinierten Zielgruppen verfügen, die benutzerdefinierte Parameter oder ein Benutzerprofil verwenden, werden diese nicht korrekt über das SDK bereitgestellt. Statt benutzerdefinierte Parameter oder das Benutzerprofil zu verwenden, müssen Sie stattdessen XDM verwenden. Es gibt jedoch native Zielgruppen-Targeting-Felder, die über die [!DNL Web SDK] unterstützt werden und keine XDM erfordern. Diese Felder sind in der Benutzeroberfläche von [!DNL Target] verfügbar, für die kein XDM erforderlich ist:

* Target-Bibliothek
* Geo
* Netzwerk
* Operating System
* Seiten der Site
* Browser
* Traffic-Quellen
* Zeitrahmen

Weitere Informationen finden Sie unter [Kategorien für Zielgruppen](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-rules.html) im *Adobe Target-Handbuch*.

### Antwort-Token

Antwort-Token werden verwendet, um Metadaten an Dritte wie Google oder Facebook zu senden. Antwort-Token werden zurückgegeben
im Feld `meta` innerhalb von `propositions` -> `items`. Im Folgenden finden Sie ein Beispiel:

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

Um die Antwort-Token zu sammeln, müssen Sie das `alloy.sendEvent`-Versprechen abonnieren, durch `propositions` navigieren und die Details aus `items` -> `meta` extrahieren.

Jede `proposition` hat ein boolesches Feld `renderAttempted`, das angibt, ob die `proposition` gerendert wurde oder nicht. Siehe Beispiel unten:

```js
alloy("sendEvent",
  {
    "renderDecisions": true,
    "decisionScopes": [
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

* Form-Based Composer based `propositions` , wobei die Markierung `renderAttempted` auf `false` gesetzt ist
* Visual Experience Composer-basierte Vorschläge mit `renderAttempted` -Markierung auf `true` gesetzt
* Visual Experience Composer-basierte Vorschläge für eine Einzelseiten-Anwendungsansicht mit `renderAttempted` -Markierung auf `true`

#### On View - change (für zwischengespeicherte Ansichten):

* Visual Experience Composer-basierte Vorschläge für eine Einzelseiten-Anwendungsansicht mit `renderAttempted` -Markierung auf `true`

Wenn das automatische Rendering deaktiviert ist, enthält das Vorschlagsarray:

#### Beim Laden der Seite:

* [!DNL Form-based Composer]-basiertes `propositions` mit `renderAttempted` -Markierung auf `false` gesetzt
* [!DNL Visual Experience Composer] basierte Vorschläge mit `renderAttempted` Markierung auf `false` gesetzt
* [!DNL Visual Experience Composer]-basierte Vorschläge für eine Einzelseiten-Anwendungsansicht, deren Markierung `renderAttempted` auf `false` gesetzt ist

#### On View - change (für zwischengespeicherte Ansichten):

* Visual Experience Composer-basierte Vorschläge für eine Einzelseiten-Anwendungsansicht mit der Markierung `renderAttempted`, die auf `false` gesetzt ist

### Einzelprofil-Update

Mit dem [!DNL Web SDK] können Sie das Profil als Erlebnisereignis auf das Profil [!DNL Target] und auf das Profil [!DNL Web SDK] aktualisieren.

Um ein [!DNL Target] -Profil zu aktualisieren, stellen Sie sicher, dass die Profildaten mit folgenden Werten übergeben werden:

* Unter `"data {"`
* Unter `"__adobe.target"`
* Präfix `"profile."`

| Schlüssel | Typ | Beschreibung |
| --- | --- | --- |
| `renderDecisions` | Boolesch | Weist die Personalisierungskomponente an, ob DOM-Aktionen interpretiert werden sollen |
| `decisionScopes` | Array `<String>` | Eine Liste der Bereiche, für die Entscheidungen abgerufen werden sollen |
| `xdm` | Objekt | In XDM formatierte Daten, die im Web SDK als Erlebnisereignis landen |
| `data` | Objekt | Beliebige Schlüssel/Wert-Paare, die unter der Zielklasse an [!DNL Target] -Lösungen gesendet werden. |

<!--Typical [!DNL Web SDK] code using this command looks like the following:-->

**Verzögern Sie das Speichern von Profil- oder Entitätsparametern, bis dem Endbenutzer Inhalt angezeigt wurde**

Um die Aufzeichnung von Attributen im Profil so lange zu verzögern, bis der Inhalt angezeigt wurde, setzen Sie in Ihrer Anfrage `data.adobe.target._save=false` .

Ihre Website enthält beispielsweise drei Entscheidungsbereiche, die drei Kategorielinks auf der Website entsprechen (Männer, Frauen und Kinder), und Sie möchten die Kategorie verfolgen, die der Benutzer schließlich besucht hat. Senden Sie diese Anfragen mit der Markierung `__save` , die auf `false` gesetzt ist, um zu vermeiden, dass die Kategorie zum Zeitpunkt der Inhaltsanforderung beibehalten wird. Nachdem der Inhalt visualisiert wurde, senden Sie die richtige Payload (einschließlich der `eventToken` und `stateToken`), damit die entsprechenden Attribute aufgezeichnet werden.

<!--Save profile or entity attributes by default with:

```js
alloy ( "sendEvent" , {
  renderDecisions : true,
  data : {
    __adobe : {
      target : {
        "__save" : true // Optional. __save=true is the default 
        "profile.gender" : "female",
        "profile.age" : 30,
        "entity.name" : "T-shirt",
        "entity.id" : "1234",
      }
    }
  }
} ) ; 
```
-->

Im folgenden Beispiel wird eine trackEvent-Meldung gesendet, Profilskripte ausgeführt, Attribute gespeichert und das Ereignis sofort aufgezeichnet.

```js
alloy ( "sendEvent" , {
  renderDecisions : true,
  data : {
    __adobe : {
      target : {
        "profile.gender" : "female",
        "profile.age" : 30,
        "entity.name" : "T-shirt" ,
        "entity.id" : "1234" ,
        "track": {
          "scopes": [ "mbox1", "mbox2"],
          "type": "display|click|..."
        }
      }
    }
  }
} ) ;
```

>[!NOTE]
>
>Wenn die Anweisung `__save` weggelassen wird, werden die Profil- und Entitätsattribute sofort gespeichert, so als ob die Anfrage ausgeführt wurde, selbst wenn der Rest der Anfrage ein Vorabruf der Personalisierung ist. Die Anweisung `__save` ist nur für Profil- und Entitätsattribute relevant. Wenn das track -Objekt vorhanden ist, wird die `__save` -Direktive ignoriert. Die Daten werden sofort gespeichert und die Benachrichtigung wird aufgezeichnet.

**`sendEvent`mit Profildaten**

```js
alloy("sendEvent", {
   renderDecisions: true|false,
   xdm: { // Experience Event XDM data },
   data: { // Freeform data }
});
```

**Senden von Profilattributen an Adobe Target:**

```js
alloy("sendEvent", {
  "renderDecisions": true,
  "data": {
    "__adobe": {
      "target": {
        "profile.gender": "female",
        "profile.age": 30
      }
    }
  }
});
```

## Empfehlungen anfordern

In der folgenden Tabelle sind die [!DNL Recommendations] -Attribute aufgeführt und es wird angezeigt, ob die einzelnen Attribute über die [!DNL Web SDK] unterstützt werden:

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

**Senden von Recommendations-Attributen an Adobe Target:**

```js
alloy("sendEvent", {
  "renderDecisions": true,
  "data": {
    "__adobe": {
      "target": {
        "entity.id": "123",
        "entity.genre": "Drama"
      }
    }
  }
});
```

## Debugging

mboxTrace und mboxDebug werden nicht mehr unterstützt. Verwenden Sie stattdessen die Methode [Web SDK debugging](/help/web-sdk/use-cases/debugging.md) .

## Terminologie

__Vorschläge:__ In [!DNL Adobe Target] korrelieren Vorschläge mit dem Erlebnis, das aus einer Aktivität ausgewählt wird.

__Schema:__ Das Schema einer Entscheidung ist der Angebotstyp in [!DNL Adobe Target].

__Umfang:__ Der Umfang der Entscheidung. In [!DNL Adobe Target] ist der Umfang die mBox. Die globale mBox ist der Bereich `__view__` .

__XDM:__ Das XDM wird in Punktnotation serialisiert und dann als mBox-Parameter in [!DNL Adobe Target] eingefügt.
