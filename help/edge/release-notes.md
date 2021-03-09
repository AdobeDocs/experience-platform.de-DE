---
title: Versionshinweise zum Adobe Experience Platform Web-SDK
description: Die neuesten Versionshinweise für Adobe Experience Platform Web-SDK.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;Versionshinweise
translation-type: tm+mt
source-git-commit: b0e6d1f7cf7302bb3a7403bb18dfd8b7489d583e
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 6%

---


# Versionshinweise

## Version 2.4.0

* Das SDK kann jetzt [als npm-Paket](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html) installiert werden.
* Es wurde Unterstützung für eine `out`-Option hinzugefügt, wenn [die Standardgenehmigung](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent) konfiguriert wird. Dadurch werden alle Ereignis bis zum Erhalt der Einwilligung gelöscht (die bestehende `pending`-Option setzt Ereignis in Warteschlange und sendet sie, sobald die Einwilligung eingegangen ist).
* Der Rückruf [onBeforeEventSend](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#onbeforeeventsend) kann jetzt verwendet werden, um zu verhindern, dass ein Ereignis gesendet wird.
* Beim Senden von Ereignissen zu personalisierten Inhalten, die gerendert oder angeklickt werden, wird nun ein XDM-Mixin anstelle von `meta.personalization` verwendet.
* Der Befehl [getIdentity](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html#retrieving-the-visitor-id) gibt jetzt die ID des Randbereichs neben der Identität zurück.
* Warnungen und Fehler, die vom Server empfangen wurden, wurden verbessert und werden in einer angemesseneren Weise behandelt.
* Unterstützung für [2.0-Standard der Adobe](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard) hinzugefügt.
* Voreinstellungen für die Zustimmung werden nach Erhalt in lokaler Datenspeicherung gehasht und gespeichert, um eine optimierte Integration zwischen CMPs, Platform Web SDK und Platform Edge Network zu ermöglichen. Wenn Sie die Voreinstellungen für die Zustimmung erfassen, empfehlen wir Ihnen jetzt, bei jedem Laden der Seite `setConsent` anzurufen.
* Es wurden zwei [Überwachungshinweise](https://github.com/adobe/alloy/wiki/Monitoring-Hooks), `onCommandResolved` und `onCommandRejected` hinzugefügt.
* Fehlerbehebung: Ereignisse für Interaktionsbenachrichtigungen zu Personalisierungen enthalten Informationen zu derselben Aktivität, wenn ein Benutzer zu einer neuen einseitigen App-Ansicht, zurück zur ursprünglichen Ansicht und auf ein Element klickt, das für die Konvertierung infrage kommt.
* Fehlerbehebung: Wenn für das erste vom SDK gesendete Ereignis `documentUnloading` `true` festgelegt wurde, wird [`sendBeacon`](https://developer.mozilla.org/de-DE/docs/Web/API/Navigator/sendBeacon) verwendet, um das Ereignis zu senden, was zu einem Fehler bei einer nicht eingerichteten Identität führt.

## Version 2.3.0

* Neue nonce-Unterstützung, um strengere Content-Sicherheitsrichtlinien zu ermöglichen.
* Unterstützung der Personalisierung für Einzelseitenanwendungen hinzugefügt.
* Verbesserte Kompatibilität mit anderen On-Page-JavaScript-Code, der `window.console`-APIs überschreiben kann.
* Fehlerbehebung: `sendBeacon` wurde nicht verwendet, wenn `documentUnloading` auf `true` gesetzt wurde oder wenn Link-Klicks automatisch verfolgt wurden.
* Fehlerbehebung: Ein Link wird nicht automatisch verfolgt, wenn das Ankerelement HTML-Inhalt enthält.
* Fehlerbehebung: Bestimmte Browserfehler, die eine schreibgeschützte `message`-Eigenschaft enthalten, wurden nicht ordnungsgemäß verarbeitet, was dazu führte, dass dem Kunden ein anderer Fehler angezeigt wurde.
* Fehlerbehebung: Wenn das SDK in einem iframe ausgeführt wird, wird ein Fehler ausgegeben, wenn die HTML-Seite des iframe aus einer anderen Subdomäne stammt als die HTML-Seite des übergeordneten Fensters.

## Version 2.2.0

* Fehlerbehebung: Das Opt-in-Objekt hinderte Alloy daran, Aufrufe durchzuführen, wenn `idMigrationEnabled` `true` ist.
* Fehlerbehebung: Achten Sie auf Anforderungen, die Angebot zur Personalisierung zurückgeben, um ein flackerndes Problem zu vermeiden.

## Version 2.1.0

* Entfernen Sie den Befehl `syncIdentity` und unterstützen Sie die Übergabe dieser IDs im Befehl `sendEvent`.
* Unterstützung von IAB 2.0 Consent Standard.
* Unterstützung der Weitergabe zusätzlicher IDs im Befehl `setConsent`.
* Support Außerkraftsetzen von `datasetId` im Befehl `sendEvent`
* Unterstützung für zulässige Monitore ([Mehr lesen](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* Übergeben Sie `environment: browser` in die Kontextdaten der Implementierung.
