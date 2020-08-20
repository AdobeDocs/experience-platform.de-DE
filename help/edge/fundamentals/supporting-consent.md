---
title: Unterstützen von Zustimmung
seo-title: Unterstützen der Zustimmungseinstellung des Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie mit dem Experience Platform Web SDK die Zustimmungseinstellungen unterstützen.
seo-description: Erfahren Sie, wie Sie mit dem Experience Platform Web SDK die Zustimmungseinstellungen unterstützen.
keywords: consent;defaultConsent;default consent;setConsent;Profile Privacy Mixin;Experience Event Privacy Mixin;Privacy Mixin;
translation-type: tm+mt
source-git-commit: 8c256b010d5540ea0872fa7e660f71f2903bfb04
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 62%

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

## Voreinstellungen für die Übermittlung von Zustimmungen über Adobe Standard

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

## Übermittlung von Voreinstellungen für die Zustimmung über den IAB-TCF-Standard

Das SDK unterstützt die Aufzeichnung von Voreinstellungen für die Zustimmung eines Benutzers, die über den IAB-Standard (Interactive Advertising Bureau Europe) Transparency and Consent Framework (TCF) bereitgestellt werden. Die Zeichenfolge für die Einwilligung kann mit demselben Befehl setConsent wie oben festgelegt werden:

```javascript
alloy("setConsent", {
    consent: [{
      standard: "IAB TCF",
      version: "2.0",
      value: "CO1Z4yuO1Z4yuAcABBENArCsAP_AAH_AACiQGCNX_T5eb2vj-3Zdt_tkaYwf55y3o-wzhhaIse8NwIeH7BoGP2MwvBX4JiQCGBAkkiKBAQdtHGhcCQABgIhRiTKMYk2MjzNKJLJAilsbe0NYCD9mnsHT3ZCY70--u__7P3fAwQgkwVLwCRIWwgJJs0ohTABCOICpBwCUEIQEClhoACAnYFAR6gAAAIDAACAAAAEEEBAIABAAAkIgAAAEBAKACIBAACAEaAhAARIEAsAJEgCAAVA0JACKIIQBCDgwCjlACAoAAAAA.YAAAAAAAAAAA",
      gdprApplies: true
    }]
});
```

Wenn die Zustimmung auf diese Weise festgelegt wird, wird das einheitliche Profil mit den Informationen zur Zustimmung aktualisiert. Damit dies funktioniert, muss das Profil XDM Schema das [Profil Privacy Mixin](https://github.com/adobe/xdm/blob/master/docs/reference/context/profile-privacy.schema.md)enthalten. Beim Senden von Ereignissen müssen die IAB-Einwilligungsinformationen manuell zum Ereignis xdm-Objekt hinzugefügt werden. Das SDK enthält nicht automatisch die Informationen zur Einwilligung in die Ereignis. Um die Einwilligungsinformationen in Ereignissen zu senden, muss das [Experience Ereignis Privacy Mixin](https://github.com/adobe/xdm/blob/master/docs/reference/context/experienceevent-privacy.schema.md) dem Experience Ereignis Schema hinzugefügt werden.

## Senden beider Standards in einer Anforderung

Das SDK unterstützt auch das Senden von mehr als einem Einwilligungsobjekt in einer Anforderung.

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "1.0",
      value: {
        general: "in"
      }
    },{
      standard: "IAB TCF",
      version: "2.0",
      value: "CO1Z4yuO1Z4yuAcABBENArCsAP_AAH_AACiQGCNX_T5eb2vj-3Zdt_tkaYwf55y3o-wzhhaIse8NwIeH7BoGP2MwvBX4JiQCGBAkkiKBAQdtHGhcCQABgIhRiTKMYk2MjzNKJLJAilsbe0NYCD9mnsHT3ZCY70--u__7P3fAwQgkwVLwCRIWwgJJs0ohTABCOICpBwCUEIQEClhoACAnYFAR6gAAAIDAACAAAAEEEBAIABAAAkIgAAAEBAKACIBAACAEaAhAARIEAsAJEgCAAVA0JACKIIQBCDgwCjlACAoAAAAA.YAAAAAAAAAAA",
      gdprApplies: true
    }]
});
```

## Beständigkeit der Voreinstellungen für die Zustimmung

Nachdem Sie dem SDK mithilfe des `setConsent`-Befehls Benutzereinstellungen mitgeteilt haben, behält das SDK die Voreinstellungen des Nutzers in einem Cookie bei. Wenn der Benutzer das nächste Mal Ihre Website im Browser lädt, ruft das SDK diese beibehaltenen Voreinstellungen ab und verwendet sie, um zu bestimmen, ob Ereignis an die Adobe gesendet werden können. Es ist nicht erforderlich, den `setConsent`-Befehl erneut auszuführen, außer um eine Änderung der Voreinstellungen des Nutzers mitzuteilen, was jederzeit möglich ist.

## Synchronisieren von Identitäten beim Festlegen der Zustimmung

Wenn die Standardgenehmigung aussteht, kann die &quot;setConsent&quot; die erste Anforderung sein, die ausgeht und Identität festlegt. Aus diesem Grund kann es wichtig sein, Identitäten bei der ersten Anforderung zu synchronisieren. Die Identitätskarte kann wie beim Befehl &quot;sendEvent&quot;dem Befehl &quot;setConsent&quot;hinzugefügt werden. Siehe [Abrufen der Experience Cloud-ID](./identity.md)

