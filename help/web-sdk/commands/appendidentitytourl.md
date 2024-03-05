---
title: appendIdentityToUrl
description: Sie können personalisierte Erlebnisse zwischen Apps, Web und domänenübergreifend genauer bereitstellen.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---

# `appendIdentityToUrl`

Die `appendIdentityToUrl` -Befehl können Sie der URL eine Benutzer-ID als Abfragezeichenfolge hinzufügen. Mit dieser Aktion können Sie die Identität eines Besuchers zwischen Domänen übertragen, wodurch doppelte Besucherzahlen für Datensätze verhindert werden, die sowohl Domänen als auch Kanäle enthalten. Sie ist in Web SDK-Versionen 2.11.0 oder höher verfügbar.

Die generierte und an die URL angehängte Abfragezeichenfolge lautet `adobe_mc`. Wenn das Web SDK keine ECID finden kann, wird die `/acquire` -Endpunkt zu erstellen.

>[!NOTE]
>
>Wenn keine Zustimmung erteilt wurde, wird die URL aus dieser Methode unverändert zurückgegeben. Dieser Befehl wird sofort ausgeführt. Er wartet nicht auf eine Aktualisierung der Zustimmung.

## Anhängen der Identität an URL mithilfe der Web SDK-Erweiterung

Das Anhängen einer Identität an eine URL erfolgt als Aktion innerhalb einer Regel in der Adobe Experience Platform-Oberfläche für Datenerfassungs-Tags.

1. Anmelden bei [experience.adobe.com](https://experience.adobe.com) mit Ihren Adobe ID-Anmeldedaten.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Regeln]** und wählen Sie dann die gewünschte Regel aus.
1. under [!UICONTROL Aktionen], wählen Sie eine vorhandene Aktion aus oder erstellen Sie eine Aktion.
1. Legen Sie die [!UICONTROL Erweiterung] Dropdown-Feld zu **[!UICONTROL Adobe Experience Platform Web SDK]** und legen Sie die [!UICONTROL Aktionstyp] nach **[!UICONTROL Umleiten mit Identität]**.
1. Klicks **[!UICONTROL Änderungen beibehalten]** und führen Sie dann Ihren Veröffentlichungs-Workflow aus.

Dieser Befehl wird normalerweise mit einer bestimmten Regel verwendet, die auf Klicks prüft und die gewünschten Domänen überprüft.

+++ Regelereigniskriterien

Trigger, wenn ein Anker-Tag `href` -Eigenschaft angeklickt wird.

* **[!UICONTROL Erweiterung]**: Core
* **[!UICONTROL Ereignistyp]**: Klicken
* **[!UICONTROL Wenn der Benutzer auf]**: Spezifische Elemente
* **[!UICONTROL Elemente, die mit der CSS-Auswahl übereinstimmen]**: `a[href]`

![Regelereignis](../assets/id-sharing-event-configuration.png)

+++

++ + Regelbedingung

Trigger nur auf gewünschten Domänen.

* **[!UICONTROL Logiktyp]**: Normal
* **[!UICONTROL Erweiterung]**: Core
* **[!UICONTROL Bedingungstyp]**: Wertvergleich
* **[!UICONTROL Linke Opera]**: `%this.hostname%`
* **[!UICONTROL Operator]**: Entspricht Regex
* **[!UICONTROL Rechter Operand]**: Ein regulärer Ausdruck, der den gewünschten Domänen entspricht. Beispiel: `adobe.com$|behance.com$`

![Regelbedingung](../assets/id-sharing-condition-configuration.png)

+++

++ + Regelaktion

Hängen Sie die Identität an die URL an.

* **[!UICONTROL Erweiterung]**: Adobe Experience Platform Web SDK
* **[!UICONTROL Aktionstyp]**: Umleitung mit Identität

![Regelaktion](../assets/id-sharing-action-configuration.png)

+++

## Identität an URL mithilfe der Web SDK-JavaScript-Bibliothek anhängen

Führen Sie die `appendIdentityToUrl` -Befehl mit einer URL als Parameter. Die Methode gibt eine URL zurück, an die die Kennung als Abfragezeichenfolge angehängt ist.

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

Wenn Sie sich für [Antworten verarbeiten](command-responses.md) mit diesem Befehl, enthält das Antwortobjekt **`url`**, die neue URL mit Identitätsdaten, die als Abfragezeichenfolgenparameter hinzugefügt werden.
