---
title: appendIdentityToUrl
description: Präzisere Bereitstellung personalisierter Erlebnisse zwischen Apps, im Web und über Domains hinweg.
exl-id: 09dd03bd-66d8-4d53-bda8-84fc4caadea6
source-git-commit: 153c5bae42c027c25a38a8b63070249d1b1a8f01
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 3%

---

# `appendIdentityToUrl`

Mit dem Befehl `appendIdentityToUrl` können Sie der URL eine Benutzerkennung als Abfragezeichenfolge hinzufügen. Mit dieser Aktion können Sie die Identität eines Besuchers zwischen Domains übertragen und so doppelte Besucherzahlen für Datensätze verhindern, die sowohl Domains als auch Kanäle enthalten. Sie ist in Web SDK ab Version 2.11.0 verfügbar.

Die generierte und an die URL angehängte Abfragezeichenfolge wird `adobe_mc`. Wenn Web SDK keine ECID finden kann, ruft es den `/acquire`-Endpunkt auf, um eine zu generieren.

>[!NOTE]
>
>Wenn kein Einverständnis erteilt wurde, wird die URL von dieser Methode unverändert zurückgegeben. Dieser Befehl wird sofort ausgeführt und wartet nicht auf eine Aktualisierung des Einverständnisses.

## Anhängen von Identitäten an URLs mithilfe der Web SDK-Erweiterung {#extension}

Das Anhängen einer Identität an eine URL wird als Aktion innerhalb einer Regel in der Benutzeroberfläche „Tags der Datenerfassung“ von Adobe Experience Platform ausgeführt.

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei ](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Regeln]** und wählen Sie dann die gewünschte Regel aus.
1. Wählen [!UICONTROL  unter &quot;]&quot; eine vorhandene Aktion aus oder erstellen Sie eine Aktion.
1. Legen Sie das [!UICONTROL Erweiterung] Dropdown-Feld auf **[!UICONTROL Adobe Experience Platform Web SDK]** fest und legen Sie den [!UICONTROL Aktionstyp] auf **[!UICONTROL Umleiten mit Identität]** fest.
1. Klicken Sie **[!UICONTROL Änderungen beibehalten]** und führen Sie dann den Veröffentlichungs-Workflow aus.

Dieser Befehl wird normalerweise mit einer bestimmten Regel verwendet, die auf Klicks wartet und die gewünschten Domains prüft.

+++Kriterien für Regelereignisse

Trigger beim Klicken auf ein Anker-Tag mit einer `href`.

* **[!UICONTROL Erweiterung]**: Core
* **[!UICONTROL Ereignistyp]**: Klicken
* **[!UICONTROL Wenn der Benutzer auf klickt]**: Bestimmte Elemente
* **[!UICONTROL Elemente, die mit der CSS-Auswahl übereinstimmen]**: `a[href]`

![Regelereignis](../assets/id-sharing-event-configuration.png)

+++

+++Regelbedingung

Trigger nur auf den gewünschten Domains.

* **[!UICONTROL Logiktyp]**: Regulär
* **[!UICONTROL Erweiterung]**: Core
* **[!UICONTROL Bedingungstyp]**: Wertvergleich
* **[!UICONTROL Linker Operand]**: `%this.hostname%`
* **[!UICONTROL Operator]**: stimmt mit Regex überein
* **[!UICONTROL Rechter Operand]**: Ein regulärer Ausdruck, der den gewünschten Domains entspricht. Beispiel: `adobe.com$|behance.com$`

![Regelbedingung](../assets/id-sharing-condition-configuration.png)

+++

+++Regelaktion

Hängen Sie die Identität an die URL an.

* **[!UICONTROL Erweiterung]**: Adobe Experience Platform Web SDK
* **[!UICONTROL Aktionstyp]**: Mit Identität umleiten

![Regelaktion](../assets/id-sharing-action-configuration.png)

+++

## Anhängen von Identitäten an URLs mithilfe der Web SDK JavaScript-Bibliothek

Führen Sie den `appendIdentityToUrl` Befehl mit einer URL als Parameter aus. Die Methode gibt eine URL zurück, an die die Kennung als Abfragezeichenfolge angehängt wird.

```js
alloy("appendIdentityToUrl",document.location);
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
  alloy("appendIdentityToUrl", {url: anchor.href}).then(result => {document.location = result.url;});
});
```

## Antwortobjekt

Wenn Sie sich für [Handhabung von Antworten](command-responses.md) mit diesem Befehl entscheiden, enthält das Antwortobjekt **`url`**, die neue URL mit Identitätsinformationen, die als Abfragezeichenfolgenparameter hinzugefügt werden.
