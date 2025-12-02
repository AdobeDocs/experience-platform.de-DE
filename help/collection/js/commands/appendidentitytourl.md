---
title: appendIdentityToUrl
description: Präzisere Bereitstellung personalisierter Erlebnisse zwischen Apps, im Web und über Domains hinweg.
exl-id: 09dd03bd-66d8-4d53-bda8-84fc4caadea6
source-git-commit: c2564f1b9ff036a49c9fa4b9e9ffbdbc598a07a8
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# `appendIdentityToUrl`

Mit dem Befehl `appendIdentityToUrl` können Sie der URL eine Benutzerkennung als Abfragezeichenfolge hinzufügen. Mit dieser Aktion können Sie die Identität eines Besuchers zwischen Domains übertragen und so doppelte Besucherzahlen für Datensätze verhindern, die sowohl Domains als auch Kanäle enthalten. Sie ist in Web SDK ab Version 2.11.0 verfügbar.

Die generierte und an die URL angehängte Abfragezeichenfolge wird `adobe_mc`. Wenn Web SDK keine ECID finden kann, ruft es den `/acquire`-Endpunkt auf, um eine zu generieren.

>[!NOTE]
>
>Wenn kein Einverständnis erteilt wurde, wird die URL von dieser Methode unverändert zurückgegeben. Dieser Befehl wird sofort ausgeführt und wartet nicht auf eine Aktualisierung des Einverständnisses.

Führen Sie den `appendIdentityToUrl` Befehl mit einer URL als Parameter aus. Die Methode gibt eine URL zurück, an die die Kennung als Abfragezeichenfolge angehängt wird.

```js
alloy("appendIdentityToUrl",
  {
    url: document.location.href
  }
);
```

Sie können einen Ereignis-Listener für alle auf der Seite empfangenen Klicks hinzufügen und überprüfen, ob die URL mit den gewünschten Domains übereinstimmt. Hängen Sie in diesem Fall die Identität an die URL an und leiten Sie den Benutzer weiter.

```js
document.addEventListener("click", event => {
  // Check if the click was a link
  const anchor = event.target.closest("a");
  if (!anchor || !anchor.href) return;

  // Check if the link points to the desired domain
  const url = new URL(anchor.href);
  if (!url.hostname.endsWith(".adobe.com") && !url.hostname.endsWith(".behance.com")) return;

  // Append the identity to the URL, then direct the user to the URL
  event.preventDefault();
  alloy("appendIdentityToUrl", {url: anchor.href}).then(result => { window.open(result.url, anchor.target || "_self"); });
});
```

Dieser Befehl unterstützt das [`edgeConfigOverrides`](configure/edgeconfigoverrides.md).

## Antwortobjekt

Beim [Verarbeiten von Antworten](command-responses.md) mit diesem Befehl enthält das Antwortobjekt **`url`**, die neue URL mit Identitätsinformationen, die als Abfragezeichenfolgenparameter hinzugefügt werden.

## Anhängen von Identitäten an URLs mithilfe der Tag-Erweiterung von Web SDK

Die diesem Befehl entsprechende Web SDK-Tag-Erweiterung ist die Aktion [Umleiten mit Identität](/help/tags/extensions/client/web-sdk/actions/redirect-with-identity.md).
