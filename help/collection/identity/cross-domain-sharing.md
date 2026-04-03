---
title: Identität domänenübergreifend freigeben
description: Pflegen Sie die Identitätskontinuität über Domains hinweg, deren Eigentümer Ihr Unternehmen ist, um die Personalisierung und das Reporting zu verbessern.
source-git-commit: bf0bb72777cacd822fd6e887ac3ef71764784214
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# Identität domänenübergreifend freigeben

Wenn Besucher zwischen Domains wechseln, deren Eigentümer Ihr Unternehmen ist, behält jede Domain standardmäßig ihre eigene Besucheridentität bei. Ohne eine explizite Übergabe wird ein Besucher, der von einer Ihrer Domains auf eine andere klickt, als neue, unbekannte Person auf der Ziel-Site behandelt. Dieser Implementierungstyp ermöglicht die Berichterstellung für Fragmente und den Neustart der Personalisierung.

Die Domain-übergreifende Identitätsfreigabe löst dieses Problem, indem ein `adobe_mc` Abfragezeichenfolgenparameter an die Ziel-URL angehängt wird, wenn ein Besucher auf einen Link klickt oder umgeleitet wird. Dieser Parameter enthält die [Experience Cloud ID (ECID) des Besuchers](./overview.md) Ihre Organisations-ID und einen Zeitstempel. Wenn die Zielseite mit einem gültigen `adobe_mc` geladen wird, liest die Web-SDK die Seite automatisch und wendet die weitergegebene Identität auf die erste Edge Network-Anfrage an, sodass beide Domains denselben Besucher haben. Der `adobe_mc` läuft nach fünf Minuten ab, sodass die Zielseite nach der Umleitung sofort geladen werden muss.

In diesem Anwendungsbeispiel wird die gemeinsame Nutzung von Identitäten zwischen Websites in verschiedenen Domains behandelt. Wenn Sie die Identität von einer Mobile App an eine WebView- oder mobile Web-Seite übergeben möchten, verwenden Sie stattdessen [Freigabe von Mobile-zu-Web](./mobile-to-web.md).

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Ihre Implementierung die folgenden Anforderungen erfüllt:

* **Web SDK**: [Web SDK](/help/collection/js/js-overview.md) Version **2.11.0 oder höher** oder die Tag-Erweiterung „Web SDK&quot; ist sowohl auf der Quell- als auch auf der Zieldomäne installiert.
* **Matching-Konfiguration**: Alle teilnehmenden Domains verwenden bei der Konfiguration der Web-SDK denselben [`orgId`](../js/commands/configure/orgid.md).
* **URL-Steuerung**: Ihr Code steuert die Links oder Umleitungen zwischen Domains, sodass Sie Abfragezeichenfolgenparameter an die Ziel-URL anhängen können.

## Domain-übergreifende Freigabe implementieren

Sie müssen die Identitätsfreigabe für jede Domain konfigurieren, die bei einer domänenübergreifenden Übergabe als Quelle dient. Wenn Besucher in beiden Richtungen zwischen zwei Domains navigieren können, konfigurieren Sie beide Domains als Quellen.

>[!BEGINTABS]

>[!TAB JavaScript-Bibliothek]

Verwenden Sie den Befehl [`appendIdentityToUrl`](/help/collection/js/commands/appendidentitytourl.md) , um den `adobe_mc` an ausgehende Links anzuhängen. Im folgenden Beispiel werden Klicks auf Ankerelemente überwacht und Identitäten an alle Links angehängt, die auf eine gewünschte Domain verweisen:

```js
document.addEventListener("click", event => {
  // Check if the click was a link
  const anchor = event.target.closest("a");
  if (!anchor || !anchor.href) return;

  // Check if the link points to a domain you want to share identity with
  const url = new URL(anchor.href);
  if (!url.hostname.endsWith(".example.com") && !url.hostname.endsWith(".example.org")) return;

  // Append the identity to the URL, then navigate
  event.preventDefault();
  alloy("appendIdentityToUrl", { url: anchor.href }).then(result => {
    window.open(result.url, anchor.target || "_self");
  });
});
```

>[!TAB Web SDK-Tag-Erweiterung]

Verwenden Sie die Aktion [**[!UICONTROL Redirect with identity]**](/help/tags/extensions/client/web-sdk/actions/redirect-with-identity.md) , um den `adobe_mc` an ausgehende Links anzuhängen. Sie können eine Regel mit den folgenden Bedingungen erstellen, um das gewünschte Verhalten zu erzielen:

1. **Ereignis**: Legen Sie die Erweiterung auf **[!UICONTROL Core]** und den Ereignistyp auf **[!UICONTROL Click]** fest. Geben Sie unter **[!UICONTROL Elements matching the CSS selector]** `a[href]` ein.
2. **Bedingung**: Setzen Sie die Erweiterung auf **[!UICONTROL Core]** und den Bedingungstyp auf **[!UICONTROL Value Comparison]**. Legen Sie **[!UICONTROL Left Operand]** auf `%this.hostname%`, **[!UICONTROL Operator]** auf **[!UICONTROL Matches Regex]** und **[!UICONTROL Right Operand]** auf einen regulären Ausdruck fest, der Ihren Ziel-Domains entspricht (z. B. `example\.com$|example\.org$`).
3. **Aktion**: Legen Sie die Erweiterung auf **[!UICONTROL Adobe Experience Platform Web SDK]** und den Aktionstyp auf **[!UICONTROL Redirect with identity]** fest.

>[!ENDTABS]

## Identität in der Ziel-Domain empfangen

Für die Ziel-Domain ist kein zusätzlicher Code erforderlich. Wenn die Web-SDK auf der Seite vorhanden ist und die URL einen gültigen `adobe_mc` enthält, extrahiert die SDK die ECID automatisch und wendet sie bei der ersten Edge Network-Anfrage auf die Identitätszuordnung des Besuchers an.

Stellen Sie sicher, dass die Ziel-Domain die folgenden Bedingungen erfüllt:

* Die Tag-Erweiterung „Web SDK&quot; oder „Web SDK&quot; wird mit derselben [`orgId`](../js/commands/configure/orgid.md) wie die Quelldomäne installiert und konfiguriert. Sie können die JavaScript-Bibliothek und die Web-SDK-Tag-Erweiterung synonym zwischen Domains verwenden, sofern diese denselben `orgId` gemeinsam haben.
* Die Seite lädt und sendet ihre erste Edge Network-Anfrage innerhalb **fünf Minuten** nach der Umleitung, bevor der `adobe_mc` abläuft.
