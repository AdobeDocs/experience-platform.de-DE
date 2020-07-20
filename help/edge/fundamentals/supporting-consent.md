---
title: Unterstützen von Zustimmung
seo-title: Unterstützen der Zustimmungseinstellung des Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie mit dem Experience Platform Web SDK die Zustimmungseinstellungen unterstützen.
seo-description: Erfahren Sie, wie Sie mit dem Experience Platform Web SDK die Zustimmungseinstellungen unterstützen.
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 96%

---


# Unterstützende Zustimmung

Um die Privatsphäre Ihres Nutzers zu respektieren, sollten Sie die Zustimmung des Nutzers einholen, bevor Sie dem SDK die Verwendung benutzerspezifischer Daten für bestimmte Zwecke gestatten. Das SDK erlaubt es derzeit nur Nutzern, alle Zwecke ein- oder auszuschalten, in Zukunft möchte Adobe jedoch eine genauere Kontrolle über bestimmte Zwecke ermöglichen.

Wenn der Nutzer sich für alle Zwecke anmeldet, darf das SDK die folgenden Aufgaben ausführen:

* Senden an und Empfangen von Daten von Adobe-Servern.
* Cookies oder Elemente der Web-Datenspeicherung lesen und schreiben (mit Ausnahme der Beibehaltung der Anmeldevoreinstellungen des Nutzers).

Wenn der Nutzer sich von allen Zwecken abmeldet, führt das SDK keine dieser Aufgaben aus.

## Konfigurieren der Zustimmung

Standardmäßig ist der Nutzer für alle Zwecke angemeldet. Um zu verhindern, dass das SDK die oben genannten Aufgaben ausführt, bevor der Nutzer sich anmeldet, müssen Sie `"defaultConsent": { "general": "pending" }` während der SDK-Konfiguration wie folgt weiterleiten:

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "imsOrgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": { "general": "pending" }
});
```

Wenn die Standardzustimmung für den allgemeinen Zweck auf „Ausstehend“ eingestellt ist, führt der Versuch, Befehle auszuführen, die von den Nutzeranmeldeeinstellungen (z. B. `event`-Befehl) abhängen, dazu, dass der Befehl innerhalb des SDK in die Warteschlange gestellt wird. Diese Befehle werden erst verarbeitet, nachdem Sie die Nutzeranmeldeeinstellungen an das SDK übermittelt haben.

An dieser Stelle möchten Sie den Nutzer vielleicht bitten, sich irgendwo in Ihrer Benutzeroberfläche anzumelden. Sobald die Benutzereinstellungen erfasst wurden, teilen Sie diese Voreinstellungen dem SDK mit.

## Voreinstellungen für die Übermittlung von Zustimmungen

Wenn sich der Nutzer anmeldet, führen Sie den `setConsent`-Befehl mit der `general`-Option, die auf `in` eingestellt ist, wie folgt aus:

```javascript
alloy("setConsent", {
    consent: [{ 
      standard: "Adobe",
      version: "1.0",
      value: { 
        general: "in" 
      }
    }]
});
```

Da der Nutzer jetzt angemeldet ist, werden alle zuvor in die Warteschlange gestellten Befehle vom SDK ausgeführt. Zukünftige Befehle, die vom Nutzer abhängen, werden _nicht_ in die Warteschlange gestellt und stattdessen sofort ausgeführt.

Wenn der Nutzer sich entscheidet, sich abzumelden, führen Sie den `setConsent`-Befehl wie folgt aus, während die `general`-Option auf `out` eingestellt ist:

```javascript
alloy("setConsent", {
    consent: [{ 
      standard: "Adobe",
      version: "1.0",
      value: { 
        general: "out" 
      }
    }]
});
```

>[!NOTE]
>
>Nachdem sich ein Nutzer abgemeldet hat, ist es im SDK nicht möglich, die Nutzerzustimmung auf `in` einzustellen.

Da der Nutzer sich für eine Abmeldung entschieden hat, werden Promises, die von zuvor in die Warteschlange gestellten Befehlen zurückgegeben wurden, abgelehnt. Zukünftige Befehle, die von der Anmeldung des Nutzers abhängen, geben Promises zurück, die in ähnlicher Weise abgelehnt werden. Weitere Informationen zum Umgang mit oder zur Unterdrückung von Fehlern finden Sie unter [Befehle ausführen](executing-commands.md).

>[!NOTE]
>
>Derzeit unterstützt das SDK nur den `general`-Zweck. Obwohl wir planen, eine stabilere Reihe von Zielen oder Kategorien zu entwickeln, die den verschiedenen Adobe-Funktionen und -Produktangeboten entsprechen, bietet die aktuelle Implementierung nur die Alles-oder-Nichts-Methode zur Teilnahme.  This only applies to the Adobe Experience Platform [!DNL Web SDK] and NOT other Adobe JavaScript libraries.

## Beständigkeit der Zustimmungseinstellungen

Nachdem Sie dem SDK mithilfe des `setConsent`-Befehls Benutzereinstellungen mitgeteilt haben, behält das SDK die Voreinstellungen des Nutzers in einem Cookie bei. Wenn der Nutzer das nächste Mal Ihre Website im Browser lädt, ruft das SDK diese beibehaltenen Voreinstellungen ab und verwendet sie. Es ist nicht erforderlich, den `setConsent`-Befehl erneut auszuführen, außer um eine Änderung der Voreinstellungen des Nutzers mitzuteilen, was jederzeit möglich ist.