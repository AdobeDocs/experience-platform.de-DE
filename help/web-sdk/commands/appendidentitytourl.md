---
title: appendIdentityToUrl
description: Sie können personalisierte Erlebnisse zwischen Apps, Web und domänenübergreifend genauer bereitstellen.
exl-id: 09dd03bd-66d8-4d53-bda8-84fc4caadea6
source-git-commit: 153c5bae42c027c25a38a8b63070249d1b1a8f01
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 3%

---

# `appendIdentityToUrl`

Mit dem Befehl `appendIdentityToUrl` können Sie der URL eine Benutzer-ID als Abfragezeichenfolge hinzufügen. Mit dieser Aktion können Sie die Identität eines Besuchers zwischen Domänen übertragen, wodurch doppelte Besucherzahlen für Datensätze verhindert werden, die sowohl Domänen als auch Kanäle enthalten. Sie ist in Web SDK-Versionen 2.11.0 oder höher verfügbar.

Die generierte und an die URL angehängte Abfragezeichenfolge lautet `adobe_mc`. Wenn das Web SDK keine ECID finden kann, ruft es den `/acquire` -Endpunkt auf, um eine zu generieren.

>[!NOTE]
>
>Wenn keine Zustimmung erteilt wurde, wird die URL aus dieser Methode unverändert zurückgegeben. Dieser Befehl wird sofort ausgeführt. Er wartet nicht auf eine Aktualisierung der Zustimmung.

## Anhängen der Identität an URL mithilfe der Web SDK-Erweiterung {#extension}

Das Anhängen einer Identität an eine URL erfolgt als Aktion innerhalb einer Regel in der Adobe Experience Platform-Oberfläche für Datenerfassungs-Tags.

1. Melden Sie sich mit Ihren Adobe ID-Anmeldedaten bei [experience.adobe.com](https://experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Regeln]** und wählen Sie dann die gewünschte Regel aus.
1. Wählen Sie unter [!UICONTROL Aktionen] eine vorhandene Aktion aus oder erstellen Sie eine Aktion.
1. Setzen Sie das Dropdown-Feld [!UICONTROL Erweiterung] auf **[!UICONTROL Adobe Experience Platform Web SDK]** und setzen Sie den [!UICONTROL Aktionstyp] auf **[!UICONTROL Mit Identität umleiten]**.
1. Klicken Sie auf **[!UICONTROL Änderungen beibehalten]** und führen Sie dann Ihren Veröffentlichungs-Workflow aus.

Dieser Befehl wird normalerweise mit einer bestimmten Regel verwendet, die auf Klicks prüft und die gewünschten Domänen überprüft.

+++ Regelereigniskriterien

Trigger, wenn auf ein Anker-Tag mit der Eigenschaft `href` geklickt wird.

* **[!UICONTROL Erweiterung]**: Core
* **[!UICONTROL Ereignistyp]**: Klicken Sie auf
* **[!UICONTROL Wenn der Benutzer auf]** klickt: Bestimmte Elemente
* **[!UICONTROL Elemente, die mit dem CSS-Selektor übereinstimmen]**: `a[href]`

![Regelereignis](../assets/id-sharing-event-configuration.png)

+++

++ + Regelbedingung

Trigger nur auf gewünschten Domänen.

* **[!UICONTROL Logiktyp]**: Normal
* **[!UICONTROL Erweiterung]**: Core
* **[!UICONTROL Bedingungstyp]**: Wertvergleich
* **[!UICONTROL Left Operand]**: `%this.hostname%`
* **[!UICONTROL Operator]**: Entspricht Regex
* **[!UICONTROL Right Operand]**: Ein regulärer Ausdruck, der den gewünschten Domänen entspricht. Beispiel: `adobe.com$|behance.com$`

![Regelbedingung](../assets/id-sharing-condition-configuration.png)

+++

++ + Regelaktion

Hängen Sie die Identität an die URL an.

* **[!UICONTROL Erweiterung]**: Adobe Experience Platform Web SDK
* **[!UICONTROL Aktionstyp]**: Mit Identität umleiten

![Regelaktion](../assets/id-sharing-action-configuration.png)

+++

## Anhängen der Identität an URL mithilfe der Web SDK JavaScript-Bibliothek

Führen Sie den Befehl `appendIdentityToUrl` mit einer URL als Parameter aus. Die Methode gibt eine URL zurück, an die die Kennung als Abfragezeichenfolge angehängt ist.

```js
alloy("appendIdentityToUrl",document.location);
```

Sie können einen Ereignis-Listener für alle Klicks hinzufügen, die auf der Seite empfangen werden, und überprüfen, ob die URL mit den gewünschten Domänen übereinstimmt. Wenn dies der Fall ist, hängen Sie die Identität an die URL an und leiten Sie den Benutzer weiter.

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

Wenn Sie sich für [Antworten verarbeiten](command-responses.md) mit diesem Befehl entscheiden, enthält das Antwortobjekt **`url`**, die neue URL mit Identitätsdaten, die als Abfragezeichenfolgenparameter hinzugefügt werden.
