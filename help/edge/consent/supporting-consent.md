---
title: Unterstützen von Voreinstellungen für die Kundeneinwilligung mit dem Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie Zustimmungsvoreinstellungen mit dem Adobe Experience Platform Web SDK unterstützen.
keywords: consent; defaultConsent; Standardzustimmung; setConsent; Profildatenschutzfeldgruppe; Erlebnisereignis-Datenschutzfeldgruppe; Datenschutzfeldgruppe;
exl-id: 647e4a84-4a66-45d6-8b05-d78786bca63a
source-git-commit: 16c8972333fa67fa2e308445f4ad6282510370d1
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 31%

---

# Unterstützen von Zustimmungsvoreinstellungen von Kunden

Um die Privatsphäre Ihres Nutzers zu respektieren, sollten Sie die Zustimmung des Nutzers einholen, bevor Sie dem SDK die Verwendung benutzerspezifischer Daten für bestimmte Zwecke gestatten. Das SDK erlaubt es derzeit nur Nutzern, alle Zwecke ein- oder auszuschalten, in Zukunft möchte Adobe jedoch eine genauere Kontrolle über bestimmte Zwecke ermöglichen.

Wenn der Nutzer sich für alle Zwecke anmeldet, darf das SDK die folgenden Aufgaben ausführen:

* Senden an und Empfangen von Daten von Adobe-Servern.
* Cookies oder Elemente des Webspeichers lesen und schreiben.

Wenn der Nutzer sich von allen Zwecken abmeldet, führt das SDK keine dieser Aufgaben aus.

## Konfigurieren der Zustimmung

Standardmäßig ist der Nutzer für alle Zwecke angemeldet. Um zu verhindern, dass das SDK die oben genannten Aufgaben ausführt, bevor der Nutzer sich anmeldet, müssen Sie `"defaultConsent": "pending"` während der SDK-Konfiguration wie folgt weiterleiten:

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "imsOrgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": "pending"
});
```

Wenn die Standardzustimmung für den allgemeinen Zweck auf „Ausstehend“ eingestellt ist, führt der Versuch, Befehle auszuführen, die von den Nutzeranmeldeeinstellungen (z. B. `sendEvent`-Befehl) abhängen, dazu, dass der Befehl innerhalb des SDK in die Warteschlange gestellt wird. Diese Befehle werden erst verarbeitet, nachdem Sie die Nutzeranmeldeeinstellungen an das SDK übermittelt haben.

>[!NOTE]
>
>Befehle werden nur im Speicher in die Warteschlange gestellt. Sie werden nicht über Seitenladevorgänge hinweg gespeichert.

Wenn Sie keine Ereignisse erfassen möchten, die vor dem Festlegen der Opt-in-Voreinstellungen des Benutzers aufgetreten sind, können Sie `"defaultConsent": "out"` während der SDK-Konfiguration. Der Versuch, Befehle auszuführen, die von den Anmeldeeinstellungen des Benutzers abhängen, hat keine Auswirkungen, bis Sie dem SDK die Opt-in-Voreinstellungen des Benutzers mitgeteilt haben.

>[!NOTE]
>
>Derzeit unterstützt das SDK nur einen einzigen &quot;all&quot;oder &quot;Nichts&quot;-Zweck. Obwohl wir planen, eine stabilere Reihe von Zielen oder Kategorien zu entwickeln, die den verschiedenen Adobe-Funktionen und -Produktangeboten entsprechen, bietet die aktuelle Implementierung nur die Alles-oder-Nichts-Methode zur Teilnahme.  Dies gilt nur für Adobe Experience Platform [!DNL Web SDK] und NICHT anderen JavaScript-Bibliotheken der Adobe.

An dieser Stelle möchten Sie den Nutzer vielleicht bitten, sich irgendwo in Ihrer Benutzeroberfläche anzumelden. Sobald die Benutzereinstellungen erfasst wurden, teilen Sie diese Voreinstellungen dem SDK mit.

## Voreinstellungen für die Übermittlung von Zustimmungen über den Adobe Experience Platform-Standard

Das SDK unterstützt die Versionen 1.0 und 2.0 des Adobe Experience Platform-Zustimmungsstandards. Derzeit unterstützen die 1.0- und 2.0-Standards nur die automatische Durchsetzung einer &quot;Alles oder Nichts&quot;-Zustimmungsvoreinstellung. Der 1,0-Standard wird schrittweise zugunsten des 2,0-Standards eingestellt. Mit dem 2.0-Standard können Sie zusätzliche Zustimmungsvoreinstellungen hinzufügen, mit denen die Zustimmungsvoreinstellung manuell erzwungen werden kann.

### Verwenden der Adobe-Standardversion 2.0

Wenn Sie Adobe Experience Platform verwenden, müssen Sie eine Datenschutzschema-Feldergruppe in Ihr Profilschema aufnehmen. Siehe [Governance, Datenschutz und Sicherheit in Adobe Experience Platform](../../landing/governance-privacy-security/overview.md) für weitere Informationen zur Adobe Standard Version 2.0. Sie können Daten innerhalb des value -Objekts hinzufügen, die dem Schema des `consents` des [!UICONTROL Einverständnis und Voreinstellungen] Profilfeldgruppe.

Wenn sich der Benutzer anmeldet, führen Sie die `setConsent` -Befehl, wobei die Sammlungsvoreinstellung auf `y` wie folgt:

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: {
        collect: {
          val: "y"
        },
        metadata: {
          time: "2021-03-17T15:48:42-07:00"
        }
      }
    }]
});
```

Im Zeitfeld sollte angegeben werden, wann der Benutzer seine Zustimmungseinstellungen zuletzt aktualisiert hat. Wenn der Benutzer sich entscheidet, sich abzumelden, führen Sie die `setConsent` -Befehl, wobei die Sammlungsvoreinstellung auf `n` wie folgt:

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: {
        collect: {
          val: "n"
        },
        metadata: {
          time: "2021-03-17T15:51:30-07:00"
        }
      }
    }]
});
```

### Verwendung des Adobe-Standards Version 1.0

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

## Übermittlung von Zustimmungsvoreinstellungen über den IAB TCF-Standard

Das SDK unterstützt die Aufzeichnung von Zustimmungsvoreinstellungen eines Benutzers, die über den IAB-Standard (Interactive Advertising Bureau Europe) Transparency and Consent Framework (TCF) bereitgestellt werden. Die Zustimmungszeichenfolge kann über denselben `setConsent` -Befehl wie oben gezeigt:

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

Wenn die Zustimmung auf diese Weise festgelegt wird, wird das Echtzeit-Kundenprofil mit den Zustimmungsinformationen aktualisiert. Damit dies funktioniert, muss das Profil-XDM-Schema die [Feldergruppe zum Profildatenschutzschema](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md). Beim Senden von Ereignissen müssen die IAB-Zustimmungsinformationen manuell zum Ereignis-XDM-Objekt hinzugefügt werden. Das SDK enthält die Zustimmungsinformationen nicht automatisch in die Ereignisse. Um die Zustimmungsinformationen in Ereignissen zu senden, muss die [Feldergruppe &quot;Erlebnisereignisdatenschutz&quot;](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/experience-event/experienceevent-privacy.schema.md) muss zum Schema Erlebnisereignis hinzugefügt werden.

## Senden mehrerer Standards in einer Anfrage

Das SDK unterstützt auch das Senden von mehr als einem Zustimmungsobjekt in einer Anfrage.

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: {
        collect: {
          val: "y"
        },
        metadata: {
          time: "2021-03-17T15:48:42-07:00"
        }
      }
    },{
      standard: "IAB TCF",
      version: "2.0",
      value: "CO1Z4yuO1Z4yuAcABBENArCsAP_AAH_AACiQGCNX_T5eb2vj-3Zdt_tkaYwf55y3o-wzhhaIse8NwIeH7BoGP2MwvBX4JiQCGBAkkiKBAQdtHGhcCQABgIhRiTKMYk2MjzNKJLJAilsbe0NYCD9mnsHT3ZCY70--u__7P3fAwQgkwVLwCRIWwgJJs0ohTABCOICpBwCUEIQEClhoACAnYFAR6gAAAIDAACAAAAEEEBAIABAAAkIgAAAEBAKACIBAACAEaAhAARIEAsAJEgCAAVA0JACKIIQBCDgwCjlACAoAAAAA.YAAAAAAAAAAA",
      gdprApplies: true
    }]
});
```

## Beständigkeit der Zustimmungseinstellungen

Nachdem Sie dem SDK mithilfe des `setConsent`-Befehls Benutzereinstellungen mitgeteilt haben, behält das SDK die Voreinstellungen des Nutzers in einem Cookie bei. Wenn der Benutzer das nächste Mal Ihre Website im Browser lädt, ruft das SDK diese beibehaltenen Voreinstellungen ab und verwendet sie, um zu bestimmen, ob Ereignisse an Adobe gesendet werden können oder nicht.

Sie müssen die Benutzereinstellungen unabhängig speichern, um das Dialogfeld &quot;Einverständnis&quot;mit den aktuellen Voreinstellungen anzeigen zu können. Es gibt keine Möglichkeit, die Benutzereinstellungen vom SDK abzurufen. Um sicherzustellen, dass die Benutzereinstellungen mit dem SDK synchronisiert bleiben, können Sie die `setConsent` bei jedem Laden der Seite. Das SDK führt nur dann einen Server-Aufruf durch, wenn sich die Voreinstellungen geändert haben.

## Synchronisieren von Identitäten beim Festlegen der Zustimmung

Wenn die Standardzustimmung aussteht oder nicht, wird die `setConsent` kann die erste Anfrage sein, die gesendet wird und Identität feststellt. Daher kann es wichtig sein, Identitäten bei der ersten Anfrage zu synchronisieren. Die Identitätszuordnung kann zu `setConsent` -Befehl wie auf der `sendEvent` Befehl. Siehe [Abrufen der Experience Cloud-ID](../identity/overview.md)
