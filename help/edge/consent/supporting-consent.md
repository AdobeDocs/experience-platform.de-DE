---
title: Unterstützende Voreinstellungen für die Zustimmung des Kunden mit dem Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie die Voreinstellungen für die Zustimmung mit dem Adobe Experience Platform Web SDK unterstützen.
keywords: approval;defaultConsent;default approval;setConsent;Profil Privacy field group;Experience Ereignis Privacy field group;Privacy field group;
exl-id: 647e4a84-4a66-45d6-8b05-d78786bca63a
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 32%

---

# Unterstützende Voreinstellungen für die Kundengenehmigung

Um die Privatsphäre Ihres Nutzers zu respektieren, sollten Sie die Zustimmung des Nutzers einholen, bevor Sie dem SDK die Verwendung benutzerspezifischer Daten für bestimmte Zwecke gestatten. Das SDK erlaubt es derzeit nur Nutzern, alle Zwecke ein- oder auszuschalten, in Zukunft möchte Adobe jedoch eine genauere Kontrolle über bestimmte Zwecke ermöglichen.

Wenn der Nutzer sich für alle Zwecke anmeldet, darf das SDK die folgenden Aufgaben ausführen:

* Senden an und Empfangen von Daten von Adobe-Servern.
* Lesen und Schreiben von Cookies oder Elementen der Web-Datenspeicherung.

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
>Befehle werden nur im Arbeitsspeicher in die Warteschlange gestellt. Sie werden nicht beim Laden der Seite gespeichert.

Wenn Sie keine Ereignis erfassen möchten, die vor dem Festlegen der Anmeldevoreinstellungen des Benutzers aufgetreten sind, können Sie `"defaultConsent": "out"` während der SDK-Konfiguration weiterleiten. Der Versuch, Befehle auszuführen, die von den Anmeldevoreinstellungen des Benutzers abhängen, hat keine Auswirkungen, bis Sie die Anmeldevoreinstellungen des Benutzers an das SDK übermittelt haben.

>[!NOTE]
>
>Derzeit unterstützt das SDK nur einen einzigen, ganz oder gar keinen Zweck. Obwohl wir planen, eine stabilere Reihe von Zielen oder Kategorien zu entwickeln, die den verschiedenen Adobe-Funktionen und -Produktangeboten entsprechen, bietet die aktuelle Implementierung nur die Alles-oder-Nichts-Methode zur Teilnahme.  Dies gilt nur für Adobe Experience Platform [!DNL Web SDK]- und NICHT für andere JavaScript-Bibliotheken der Adobe.

An dieser Stelle möchten Sie den Nutzer vielleicht bitten, sich irgendwo in Ihrer Benutzeroberfläche anzumelden. Sobald die Benutzereinstellungen erfasst wurden, teilen Sie diese Voreinstellungen dem SDK mit.

## Voreinstellungen für die Übermittlung von Zustimmungen über den Adobe Experience Platform Standard

Das SDK unterstützt die Versionen 1.0 und 2.0 des Adobe Experience Platform-Zustimmungsstandards. Die 1.0- und 2.0-Standards unterstützen derzeit nur die automatische Durchsetzung einer &quot;Alles oder Nichts&quot;-Präferenz. Der 1.0-Standard wird zugunsten des 2.0-Standards eingestellt. Der 2.0-Standard ermöglicht es Ihnen, zusätzliche Voreinstellungen für die Zustimmung hinzuzufügen, die zur manuellen Durchsetzung der Einwilligung verwendet werden können.

### Verwenden der Adobe-Standardversion 2.0

Wenn Sie Adobe Experience Platform verwenden, müssen Sie eine Schema-Feldgruppe zum Datenschutz in Ihr Profil-Schema einbeziehen. Weitere Informationen zur Adobe-Standardversion 2.0 finden Sie unter [Verwaltung, Datenschutz und Sicherheit in Adobe Experience Platform](../../landing/governance-privacy-security/overview.md). Sie können Daten innerhalb des Wertobjekts unten hinzufügen, die dem Schema des Felds `consents` der Feldgruppe &quot;Profil und Voreinstellungen&quot;entsprechen.

Wenn sich der Benutzer anmeldet, führen Sie den Befehl `setConsent` mit der Erfassungseinstellung `y` wie folgt aus:

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

Im Uhrzeitfeld sollte angegeben werden, wann der Benutzer seine Voreinstellungen für die Zustimmung zuletzt aktualisiert hat. Wenn der Benutzer Opt-out, führen Sie den Befehl `setConsent` aus, wobei die Erfassungseinstellung auf `n` wie folgt eingestellt ist:

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

>[!NOTE]
>
>Nachdem sich ein Benutzer abgemeldet hat, können Sie mit dem SDK nicht festlegen, dass die Benutzer die Zustimmung einholen auf `y` setzen.

### Verwenden der Adobe-Standardversion 1.0

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

>[!NOTE]
>
>Nachdem sich ein Nutzer abgemeldet hat, ist es im SDK nicht möglich, die Nutzerzustimmung auf `in` einzustellen.

## Übermittlung von Präferenzen für die Zustimmung über den IAB-TCF-Standard

Das SDK unterstützt die Aufzeichnung von Voreinstellungen für die Zustimmung eines Benutzers, die über den IAB-Standard (Interactive Advertising Bureau Europe) Transparency and Consent Framework (TCF) bereitgestellt werden. Die Zeichenfolge für die Einwilligung kann mit demselben Befehl wie oben festgelegt werden:`setConsent`

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

Wenn die Einwilligung auf diese Weise festgelegt wird, wird das Echtzeit-Profil des Kunden mit den Einwilligungsinformationen aktualisiert. Damit dies funktioniert, muss das Profil-XDM-Schema die Feldgruppe [Profil Privacy Schema](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md) enthalten. Beim Senden von Ereignissen müssen die IAB-Einwilligungsinformationen manuell zum Ereignis-XDM-Objekt hinzugefügt werden. Das SDK enthält nicht automatisch die Informationen zur Einwilligung in die Ereignis. Um die Informationen zur Einwilligung in Ereignissen zu senden, muss die Feldgruppe [Experience Ereignis Privacy](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/experience-event/experienceevent-privacy.schema.md) dem Experience Ereignis-Schema hinzugefügt werden.

## Senden mehrerer Standards in einer Anforderung

Das SDK unterstützt auch das Senden von mehr als einem Einwilligungsobjekt in einer Anforderung.

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

Nachdem Sie dem SDK mithilfe des `setConsent`-Befehls Benutzereinstellungen mitgeteilt haben, behält das SDK die Voreinstellungen des Nutzers in einem Cookie bei. Wenn der Benutzer das nächste Mal Ihre Website im Browser lädt, ruft das SDK diese beibehaltenen Voreinstellungen ab und verwendet sie, um zu bestimmen, ob Ereignis an die Adobe gesendet werden können.

Sie müssen die Benutzereinstellungen unabhängig speichern, um den Dialog zur Genehmigung mit den aktuellen Voreinstellungen anzeigen zu können. Es gibt keine Möglichkeit, die Benutzereinstellungen aus dem SDK abzurufen. Um sicherzustellen, dass die Benutzereinstellungen mit dem SDK synchronisiert bleiben, können Sie bei jedem Laden der Seite den Befehl `setConsent` aufrufen. Das SDK führt nur dann einen Server-Aufruf durch, wenn sich die Voreinstellungen geändert haben.

## Synchronisieren von Identitäten während der Einrichtung der Zustimmung

Wenn die Standardgenehmigung aussteht oder ausfällt, kann `setConsent` die erste Anforderung sein, die ausgeht und Identität festlegt. Aus diesem Grund kann es wichtig sein, Identitäten bei der ersten Anforderung zu synchronisieren. Die Identitätskarte kann wie beim Befehl `setConsent` hinzugefügt werden. `sendEvent` Siehe [Abrufen der Experience Cloud-ID](../identity/overview.md)
