---
title: defaultConsent
description: Legen Sie die standardmäßige Methode zur Einverständniserfassung für Ihre Web-Eigenschaft fest.
exl-id: 2a22fa8b-a234-4d3e-9b55-c7482a928fe6
source-git-commit: bf0bb72777cacd822fd6e887ac3ef71764784214
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---


# `defaultConsent`

Die `defaultConsent`-Eigenschaft bestimmt, wie das Einverständnis zur Datenerfassung verarbeitet wird, bevor der [`setConsent`](../setconsent.md) aufgerufen wird. Diese Eigenschaft ist nützlich, wenn Sie nicht versehentlich Daten von Personen erfassen möchten, die in Bereichen wohnen, in denen vor der Datenerfassung ein Einverständnis erforderlich ist.

Wenn Sie einen Besucher haben, der nicht unter die Datenschutz-Grundverordnung (DSGVO) fällt, kann die standardmäßige Einwilligung auf `in` gesetzt werden. Für Besucher innerhalb der Gerichtsbarkeit der DSGVO kann das standardmäßige Einverständnis auf `pending` festgelegt werden. Ihre Consent Management Platform (CMP) kann die Region des Kunden erkennen und das Flag `gdprApplies` IAB TCF 2.0 bereitstellen. Diese Markierung kann verwendet werden, um das Standardeinverständnis festzulegen.

Legen Sie beim Ausführen des `defaultConsent`-Befehls die `configure`-Zeichenfolgeneigenschaft auf die gewünschte Einverständnisstufe fest. Bei dieser Eigenschaft wird zwischen Groß- und Kleinschreibung unterschieden und sie unterstützt nur die folgenden drei Werte: `"in"`, `"out"` und `"pending"`. Wenn Sie versuchen, einen anderen Wert zu verwenden, gibt die Bibliothek einen Fehler aus. Wenn im `configure`-Befehl nicht festgelegt, ist der Standardwert **`in`**.

>[!IMPORTANT]
>
>Der `defaultConsent` bleibt beim Laden der Seite nicht erhalten. Stellen Sie sicher, dass Sie jedes Mal, wenn Sie den `configure`-Befehl aufrufen, das gewünschte Standardeinverständnis festlegen. Im Gegensatz dazu wird das aufgelöste Einverständnis eines Besuchers (festgelegt durch [`setConsent`](../setconsent.md)) in einem Cookie gespeichert und automatisch auf nachfolgende Seitenladevorgänge angewendet.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  defaultConsent: "pending"
});
```

* **`in`**: Die Datenerfassung funktioniert normal, bis der Benutzer eine Abwahl trifft.
* **`out`**: Daten werden dauerhaft verworfen, bis sich der Benutzer anmeldet.
* **`pending`**: Daten werden lokal gespeichert, bis sich der Benutzer mithilfe des [`setConsent`](../setconsent.md)-Befehls anmeldet.

>[!NOTE]
>
>Obwohl Adobe plant, eine robustere Reihe von Zwecken oder Kategorien zu erstellen, die den Funktionen und Produktangeboten von Adobe entsprechen, ist die aktuelle Implementierung ein Alles-oder-Nichts-Ansatz für das Opt-in. Diese Einschränkung gilt nur für Web SDK und nicht für andere Adobe JavaScript-Bibliotheken.

## Verwenden von `defaultConsent` zusammen mit `setConsent` {#using-consent}

Bei der gemeinsamen Verwendung führen `defaultConsent` und `setConsent` je nach den konfigurierten Werten zu unterschiedlichen Datenerfassungs-, Cookie- und Identitätsergebnissen. Eine vollständige Interaktionstabelle finden [&#x200B; unter „Einverständnis und Identität &#x200B;](/help/collection/identity/consent.md#how-consent-affects-identity) Datenerfassung“.

## Festlegen des Standardeinverständnisses basierend auf `gdprApplies`

Einige CMPs bieten die Möglichkeit festzustellen, ob die Datenschutz-Grundverordnung (DSGVO) auf den Kunden anwendbar ist. Wenn Sie von einer Einwilligung für Kunden ausgehen möchten, für die die DSGVO nicht gilt, können Sie das `gdprApplies`-Flag in einem TCF-API-Aufruf verwenden. Beispiel:

```js
var alloyConfiguration = { ... };
window.__tcfapi('getTCData', 2, function (tcData, success) {
  if (success) {
    alloyConfiguration.defaultConsent = tcData.gdprApplies ? "pending" : "in";
    window.alloy("configure", alloyConfiguration);
  }
});
```

Im obigen Code-Block wird der Befehl `configure` aufgerufen, nachdem die `tcData` von der TCF-API abgerufen wurde. Wenn `gdprApplies` „true“ ist, wird das Standardeinverständnis auf `pending` festgelegt. Wenn `gdprApplies` den Wert „false“ hat, wird das Standardeinverständnis auf &quot;`in`&quot; festgelegt. Stellen Sie sicher, dass Sie die Variable `alloyConfiguration` mit Ihrer Konfiguration ausfüllen.

## Standardmäßiges Einverständnis mit der Tag-Erweiterung „Web SDK&quot;

Siehe [Einverständniseinstellungen](/help/tags/extensions/client/web-sdk/configure/consent.md) in der Dokumentation zur Web SDK-Tag-Erweiterung, um zu erfahren, wie Sie diese Aktionen mithilfe von Tags durchführen können.
