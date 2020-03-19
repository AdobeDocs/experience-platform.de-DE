---
title: Zustimmung
seo-title: Unterstützende Adobe Experience Platform Web SDK-Genehmigungsvoreinstellung
description: Erfahren Sie, wie Sie mit dem Experience Platform Web SDK die Voreinstellungen für die Zustimmung unterstützen.
seo-description: Erfahren Sie, wie Sie mit dem Experience Platform Web SDK die Voreinstellungen für die Zustimmung unterstützen.
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (Beta) Unterstützende Zustimmung

>[!IMPORTANT]
>
>Das Adobe Experience Platform Web SDK befindet sich derzeit in der Betaphase und steht nicht allen Benutzern zur Verfügung. Dokumentation und Funktionalität können sich ändern.

Um die Privatsphäre Ihres Benutzers zu respektieren, sollten Sie die Zustimmung des Benutzers einholen, bevor Sie dem SDK die Verwendung benutzerspezifischer Daten für bestimmte Zwecke gestatten. Das SDK erlaubt es derzeit nur Benutzern, alle Aufgaben zu Opt-in oder auszuschalten, in Zukunft hofft Adobe jedoch auf eine genauere Kontrolle über bestimmte Zwecke.

Wenn der Benutzer sich für alle Zwecke anmeldet, darf das SDK die folgenden Aufgaben ausführen:

* Senden Sie Daten an die Server von Adobe und von diesen.
* Cookies oder Elemente der Web-Datenspeicherung lesen und schreiben (mit Ausnahme der Beibehaltung der Anmeldevoreinstellungen des Benutzers).

Wenn der Benutzer sich von allen Zwecken abmeldet, führt das SDK keine dieser Aufgaben aus.

## Konfigurieren der Zustimmung

Standardmäßig ist der Benutzer für alle Zwecke aktiviert. Um zu verhindern, dass das SDK die oben genannten Aufgaben ausführt, bis der Benutzer sich anmeldet, müssen Sie die SDK-Konfiguration wie folgt `"defaultConsent": { "general": "pending" }` weiterleiten:

```javascript
alloy("configure", {
  "configId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "imsOrgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": { "general": "pending" }
});
```

Wenn die Standardgenehmigung für den allgemeinen Zweck auf &quot;Ausstehend&quot;festgelegt ist, führt der Versuch, Befehle auszuführen, die von den Benutzeroptionseinstellungen (z. B. dem `event` Befehl) abhängen, dazu, dass der Befehl innerhalb des SDK in die Warteschlange gestellt wird. Diese Befehle werden erst verarbeitet, nachdem Sie die Anmeldevoreinstellungen des Benutzers an das SDK übermittelt haben.

An dieser Stelle möchten Sie den Benutzer vielleicht bitten, irgendwo in Ihrer Benutzeroberfläche zu Opt-in. Sobald die Benutzereinstellungen erfasst wurden, teilen Sie diese Voreinstellungen dem SDK mit.

## Voreinstellungen für die Übermittlung von Genehmigungen

Wenn sich der Benutzer anmeldet, führen Sie den `setConsent` Befehl mit der `general` folgenden Option aus `in` :

```javascript
alloy("setConsent", {
  "general": "in"
});
```

Da der Benutzer jetzt angemeldet ist, werden alle zuvor in die Warteschlange gestellten Befehle vom SDK ausgeführt. Zukünftige Befehle, die vom Benutzer abhängen, werden _nicht_ in die Warteschlange gestellt und stattdessen sofort ausgeführt.

Wenn der Benutzer Opt-out möchte, führen Sie den `setConsent` Befehl mit der `general` folgenden Option aus `out` :

```javascript
alloy("setConsent", {
  "general": "out"
});
```

>[!NOTE]
>
>Nachdem sich ein Benutzer abgewählt hat, ist es im SDK nicht möglich, die Benutzereinwilligung festzulegen `in`.

Da der Benutzer sich für Opt-out entschieden hat, werden Versprechungen, die von zuvor in die Warteschlange gestellten Befehlen zurückgegeben wurden, abgelehnt. Zukünftige Befehle, die vom Benutzer abhängen, geben Versprechen zurück, die in ähnlicher Weise abgelehnt werden. Weitere Informationen zum Umgang mit oder zur Fehlerbehebung finden Sie unter [Ausführungsbefehle](executing-commands.md).

>[!NOTE]
>
>Derzeit unterstützt das SDK nur den `general` Zweck. Obwohl wir planen, eine stabilere Reihe von Zielen oder Kategorien zu entwickeln, die den verschiedenen Adobe-Funktionen und -Produktangeboten entsprechen, ist die aktuelle Implementierung eine Alles-oder-Nichts-Methode zur Teilnahme.  Dies gilt nur für das Adobe Experience Platform Web SDK und NICHT für andere Adobe JavaScript-Bibliotheken.

## Beständigkeit der Voreinstellungen für die Zustimmung

Nachdem Sie dem SDK mithilfe des `setConsent` Befehls Benutzereinstellungen mitgeteilt haben, behält das SDK die Voreinstellungen des Benutzers in einem Cookie bei. Wenn der Benutzer das nächste Mal Ihre Website im Browser lädt, ruft das SDK diese beibehaltenen Voreinstellungen ab und verwendet sie. Es ist nicht erforderlich, den `setConsent` Befehl erneut auszuführen, außer um eine Änderung der Voreinstellungen des Benutzers mitzuteilen, die Sie jederzeit vornehmen können.