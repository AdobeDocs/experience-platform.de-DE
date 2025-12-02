---
title: Personalisierung
description: Rendern verschiedener Inhalte für verschiedene Benutzer und Erstellen eines personalisierten Erlebnisses für sie.
exl-id: 4bd370c8-8d8d-469e-9666-b5b6d0e3a660
source-git-commit: 54cd49bc1e6f23e3fb6d539274ea16d36ea21386
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 0%

---

# `personalization`

Das `personalization`-Objekt konfiguriert, welche Personalisierungsentscheidungen (Angebote oder Vorschläge) angefordert werden und wie sie in der Anfrage und Antwort verarbeitet werden. Dies ist besonders bei Adobe Target- oder Adobe Journey Optimizer-Implementierungen nützlich, da es die treibende Kraft ist, mit der Sie die angezeigten Inhalte pro Benutzerin bzw. Benutzer anpassen können.

```js
alloy("sendEvent", {
  personalization: {
    decisionScopes: ["hero-banner"],
    surfaces: ["web://example.com"],
    schemas: ["https://ns.adobe.com/personalization/dom-action"],
    sendDisplayEvent: true,
    sendDisplayNotifications: true,
    includePendingDisplayNotifications: true,
    defaultPersonalizationEnabled: false
  },
  renderDecisions: true,
  xdm: adobeDataLayer.getState(reference)
});
```

Das `personalization`-Objekt enthält die folgenden Eigenschaften:

## `personalization.decisionScopes`

Die `decisionScopes`-Eigenschaft ist ein Array von Zeichenfolgen, das die Web-SDK anweist, Personalisierungsentscheidungen abzurufen und zurückzugeben. Jedes Element im Array identifiziert einen Speicherort, einen Kontext oder eine logische Platzierung, an dem personalisierte Inhalte gewünscht werden.

Diese Eigenschaft ist nützlich, wenn Sie explizit personalisierte Inhalte für bestimmte Bereiche oder Komponenten einer Seite abrufen möchten. Dies ist besonders nützlich bei Single Page Applications, für die möglicherweise andere Angebote erforderlich sind, wenn sich die Navigation oder Ansicht der Benutzenden ändert. Sie können diese Eigenschaft auch verwenden, um die Leistung zu optimieren, indem Sie nur Angebote für die Benutzeroberflächenelemente abrufen, die für den Benutzer relevant sind.

```js
personalization: {
  decisionScopes: ["hero-banner", "cart-offer"]
}
```

In Adobe Target wird jeder Entscheidungsumfang einer Mbox oder Aktivität zugeordnet. In Adobe Journey Optimizer ist jeder Entscheidungsumfang entscheidungsbasierten Web-Content-Platzierungen oder -Kampagnen zugeordnet. In Offer Decisioning werden die Entscheidungsumfänge den Angeboten oder Vorschlägen zugeordnet, die der Besucher erhalten soll.

>[!TIP]
>
>Wenn Sie den globalen Umfang anfordern (oder blockieren) möchten, verwenden Sie [`defaultPersonalizationEnabled`](#personalizationdefaultpersonalizationenabled), anstatt ihn hier in `decisionScopes` anzugeben.

## `personalization.surfaces`

Die `surfaces`-Eigenschaft ist ein Array von [Oberflächen-URI](https://experienceleague.adobe.com/de/docs/journey-optimizer/using/channels/code-based-experience/configure-code-based-channel/code-based-surface#surface-uri)-Zeichenfolgen, die den Kanal, das Gerät oder den Kontext, für den die Personalisierung angefordert wird, manuell definieren. Sie ermöglichen es Ihnen, zwischen verschiedenen digitalen Erlebnissen wie Domains, Apps oder Geräteplattformen in Ihrem kanalübergreifenden Ökosystem zu unterscheiden. Standardmäßig leitet die Bibliothek die Standardoberfläche von der aktuellen Seite ab. Mit dieser Eigenschaft können Sie die automatisch abgeleitete Oberfläche für die aktuelle Seite überschreiben.

Diese Eigenschaft ist nützlich, wenn Sie die kanalübergreifende Personalisierung verwenden möchten, und Sie müssen unterscheiden, wie die Personalisierung zwischen verschiedenen Kanälen funktioniert. Damit können Sie unter derselben Adobe Experience Platform-Organisation separate Angebote für verschiedene Sites erstellen.

```js
personalization: {
  surfaces: ["web://example.com", "web://support.example.com/contact"]
}
```

Diese Eigenschaft wird in Adobe Journey Optimizer grundsätzlich verwendet, da sie mit in Journey Optimizer-Kampagnen eingerichteten Oberflächen und mit der Oberflächenverwaltung übereinstimmt.

## `personalization.schemas`

Die `schemas`-Eigenschaft ist ein Array von Schema-URI-Zeichenfolgen, die die von Edge Network angeforderten Arten von Personalisierungsinhalten filtern. Wenn Sie diese Eigenschaft festlegen, wird die Antwort, die Sie von Adobe erhalten, darauf beschränkt, nur Angebote einzuschließen, die den von Ihnen angegebenen Inhaltstypdefinitionen entsprechen. Wenn diese Option weggelassen wird, fordert die Bibliothek Angebote aller verfügbaren Schemata für die entsprechenden Bereiche oder Oberflächen an.

Diese Eigenschaft hilft bei der Optimierung der Antwortgröße und stellt sicher, dass Ihre Website oder Anwendung nur Angebotstypen erhält, die sie verarbeiten kann. Dies ist auch hilfreich, wenn es mit Single Page Applications verwendet wird, die personalisierte Inhalte auf eine bestimmte Weise rendern (z. B. nur mit DOM-Aktionen oder nur JSON-Objekten).

```js
personalization: {
  schemas: [
    "https://ns.adobe.com/personalization/dom-action",
    "https://ns.adobe.com/personalization/html-content-item"
  ]
}
```

Die folgenden Schema-URIs werden unterstützt:

* **`https://ns.adobe.com/personalization/dom-action`**: Angebote, die direkte DOM-Aktionen sind und normalerweise vom Visual Experience Composer in Adobe Target generiert werden. Sie enthalten Anweisungen zum automatischen Bearbeiten von Elementen auf der Seite ohne zusätzlichen Code. Dies ist der Standard für die automatisch gerenderte Web-Personalisierung.
* **`https://ns.adobe.com/personalization/html-content-item`**: Angebote, die unformatierten HTML enthalten, der als Zeichenfolge bereitgestellt wird. Bei Ihrer Implementierung wird dieser Inhalt normalerweise an der gewünschten Stelle auf der Seite eingefügt, sodass Sie mehr Kontrolle haben als bei DOM-Aktionen. Wird häufig für Banner, Ausschnitte oder modale Inhalte verwendet.
* **`https://ns.adobe.com/personalization/json-content-item`**: Als JSON-Objekt formatierte Angebote. Wird am häufigsten in API-basierten Implementierungen oder Frontends verwendet, die strukturierte Daten anstelle von HTML- oder DOM-Änderungen erwarten.
* **`https://ns.adobe.com/personalization/redirect-item`**: Angebote, die zu einer anderen URL umgeleitet werden. Wird verwendet, um den Benutzer basierend auf der Zielgruppenbestimmungs- oder Entscheidungslogik zu einer neuen Seite zu leiten, z. B. Landingpages oder Onboarding-Flüsse.
* **`https://ns.adobe.com/personalization/ruleset-item`**: Stellt einen Block von Geschäftslogik bereit, um eine Client-seitige Regel-Engine zu unterstützen. Enthält einen versionierten Regelsatz, der logische Bedingungen und Konsequenzen definiert (if/then Personalisierungslogik).
* **`https://ns.adobe.com/personalization/message/in-app`**: Speziell für In-App-Nachrichten von Adobe Journey Optimizer formatierte Angebote, die in der Regel als Modale, Banner, Popup-Fenster oder Überlagerungen gerendert werden.
* **`https://ns.adobe.com/personalization/message/content-card`**: Speziell für Adobe Journey Optimizer-Inhaltskarten formatierte Angebote, die für persistente oder Posteingangsähnliche Feeds in Web- oder Mobile Apps entwickelt wurden.
* **`https://ns.adobe.com/personalization/message/native-alert`**: Speziell für native Warnhinweise in Adobe Journey Optimizer formatierte Angebote, die plattformnative Benachrichtigungsdialoge auslösen.
* **`https://ns.adobe.com/personalization/measurement`**: Dient zur Nachverfolgung von Klicks und Interaktionen mit personalisierten Angeboten. Enthält keinen Inhalt, der gerendert werden kann.
* **`https://ns.adobe.com/personalization/eventHistoryOperation`**: Schema zur Änderung des Ereignisverlaufs eines Besuchers im lokalen Speicher. Wird intern von SDKs zum Tracking der Erlebnisse verwendet, die bereitgestellt oder blockiert wurden. Enthält keinen Inhalt, der gerendert werden kann.
* **`https://ns.adobe.com/personalization/default-content-item`**: Fallback- oder Standardinhalte, in der Regel wenn kein personalisiertes Angebot geeignet ist. Dadurch wird sichergestellt, dass nicht qualifizierte Benutzende weiterhin Inhalte erhalten, sodass das Erlebnis konsistent bleibt.

## `personalization.sendDisplayEvent`

Bei der `sendDisplayEvent`-Eigenschaft handelt es sich um einen booleschen Wert, der bestimmt, ob ein Anzeigebenachrichtigungsereignis automatisch an die Edge Network gesendet wird, unmittelbar nachdem personalisierte Inhalte auf der Seite gerendert wurden. Wenn ausgelassen, wird der Standardwert `true`. Legen Sie diese Variable auf `false` fest, wenn Sie nicht angeben möchten, dass personalisierte Inhalte für das Impression-Tracking gerendert wurden.

Der häufigste Anwendungsfall für das Festlegen dieser Variablen auf `false` besteht darin, einen anderen Befehl an eine andere Stelle in Ihrer Implementierung zu senden, die ein Anzeigeereignis kennzeichnet. Einige Implementierungen verfügen sowohl über Impression- als auch über Analytics-Ereignisse. Diese Eigenschaft gibt Ihnen die volle Kontrolle darüber, welche `sendEvent`-Befehle die Impressionen erhöhen.

```js
personalization: {
  sendDisplayEvent: true
}
```

>[!NOTE]
>
>Frühere Versionen von Web SDK (Version 2.12.0 und früher) verwenden stattdessen `sendDisplayNotifications`.

## `personalization.includePendingDisplayNotifications`

Die `includePendingDisplayNotifications`-Eigenschaft ist ein boolescher Wert, der steuert, ob ausstehende Anzeigebenachrichtigungen im aktuellen `sendEvent` enthalten sind. Ausstehende Anzeigebenachrichtigungen sind Impressionen für personalisierte Inhalte, die gerendert, aber noch nicht als Anzeigeereignis an Edge Network gemeldet wurden. Diese Eigenschaft ist bei der Verwendung von Einzelseitenanwendungen hilfreich, da das Rendern von personalisierten Inhalten und `sendEvent` möglicherweise asynchron erfolgt.

Der Standardwert für diese Eigenschaft ist `false`. Legen Sie diese Eigenschaft auf `true` fest, wenn Sie ausstehende Anzeigebenachrichtigungen per Batch löschen möchten, damit ihre Impressionen korrekt aufgezeichnet werden. Synchrone Implementierung, z. B. herkömmliche Websites, muss diese Eigenschaft normalerweise nicht festlegen.

```js
personalization: {
  includePendingDisplayNotifications: true
}
```

## `personalization.defaultPersonalizationEnabled`

Die `defaultPersonalizationEnabled`-Eigenschaft ist ein boolescher Wert, der Ihnen explizit die Kontrolle darüber gibt, wie die Web-SDK den standardmäßigen seitenweiten Personalisierungsbereich (`__view__`) und die Oberfläche für diesen `sendEvent` anfordert. Standardmäßig fordert Web SDK beim ersten `sendEvent` nach dem Laden einer Seite Angebote für den standardmäßigen seitenweiten Personalisierungsbereich und die zugehörigen Oberflächen an. Nachfolgende `sendEvent`-Befehle fordern keine Standardpersonalisierung an. Mit dieser Eigenschaft können Sie dieses Verhalten außer Kraft setzen. Dies ist nützlich bei Implementierungen von Einzelseiten-Apps, bei denen Sie beim Navigieren auf Ihrer Site die standardmäßige Personalisierung erneut anfordern können. Sie können diese Eigenschaft auch verwenden, wenn Sie ein Anzeigeereignis _nur_ senden möchten, ohne den Abruf von Angeboten zu duplizieren.

```js
personalization: {
  defaultPersonalizationEnabled: false
}
```

Diese Eigenschaft verwendet die folgende Logik, je nachdem, wie sie festgelegt ist:

* **Nicht festgelegt**: Standardpersonalisierung anfordern, wenn sie noch nicht angefordert wurde. Die Standardpersonalisierung wird normalerweise beim ersten `sendEvent` nach dem Laden einer Seite angefordert und dann bei nachfolgenden `sendEvent` auf derselben Seite nicht erneut angefordert. Durch Festlegen dieser Eigenschaft wird dieses Verhalten überschrieben.
* **`true`**: Fordern Sie explizit den Seitenumfang und die Standardoberfläche an, auch wenn dieser `sendEvent`-Befehl nicht der erste nach dem Laden einer Seite ist. Ideale Zeiten, um diese Eigenschaft auf `true` festzulegen, sind, wenn Sie eine standardmäßige Personalisierungsanfrage erzwingen müssen, z. B. in Szenarien mit Einzelseiten-Apps.
* **`false`**: Unterdrückt die Anfrage für den Seitenbereich und die Standardoberfläche explizit, auch wenn dieser `sendEvent`-Befehl der erste nach dem Laden einer Seite ist. Ideale Zeiten, um diese Eigenschaft auf `false` festzulegen, sind, wenn Sie möchten, dass ein bestimmter `sendEvent`-Befehl keine neuen Angebote anfordert und stattdessen nur Daten an Analytics sendet oder ein Anzeigeereignis sendet.

## Personalization-Komponenten, die die Tag-Erweiterung „Web SDK&quot; verwenden

Die Web SDK-Tag-Erweiterung, die dieser Eigenschaft entspricht, ist der [**[!UICONTROL Personalization]**](/help/tags/extensions/client/web-sdk/actions/send-event.md#personalization-fields) Abschnitt beim Konfigurieren einer [!UICONTROL Send event]-Aktion.
