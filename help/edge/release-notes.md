---
title: Versionshinweise zum Adobe Experience Platform Web-SDK
description: Die neuesten Versionshinweise für Adobe Experience Platform Web-SDK.
keywords: Adobe Experience Platform Web SDK; Platform Web SDK; Web SDK; Versionshinweise;
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
source-git-commit: 2be9d262a699861c01011c59358751e6406f3770
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 4%

---

# Versionshinweise

## Version 2.6.3 - 16. August 2021

* Es wurde ein Problem behoben, bei dem Objekte, die nicht für die öffentliche Verwendung vorgesehen waren, über das aufgelöste Promise des Befehls `configure` bereitgestellt wurden.

## Version 2.6.2 - 4. August 2021

* Es wurde ein Problem behoben, bei dem eine Warnung zur Einstellung von `result.decisions` (bereitgestellt vom `sendEvent`-Befehl) in der Konsole protokolliert wurde, selbst wenn nicht auf die `result.decisions`-Eigenschaft zugegriffen wurde. Beim Zugriff auf die Eigenschaft `result.decisions` wird keine Warnung protokolliert, die Eigenschaft wird jedoch weiterhin nicht mehr unterstützt.

## Version 2.6.1 - 29. Juli 2021

* Es wurde ein Problem behoben, bei dem beim Rendern der Personalisierung für eine Einzelseiten-App-Ansicht ohne Personalisierungsinhalt ein Fehler ausgegeben wurde und das vom Befehl `sendEvent` zurückgegebene Promise abgelehnt wurde.

## Version 2.6.0 - 27. Juli 2021

* Bietet mehr Personalisierungsinhalte im aufgelösten Versprechen `sendEvent`, einschließlich Adobe Target-Antwort-Token. Wenn der Befehl `sendEvent` ausgeführt wird, wird ein Promise zurückgegeben, das schließlich mit einem `result` -Objekt aufgelöst wird, das Informationen enthält, die vom Server empfangen wurden. Zuvor enthielt dieses Ergebnisobjekt eine Eigenschaft mit dem Namen `decisions`. Diese `decisions` -Eigenschaft wird nicht mehr unterstützt. Eine neue Eigenschaft, `propositions`, wurde hinzugefügt. Diese neue Eigenschaft bietet Kunden Zugriff auf mehr Personalisierungsinhalte, einschließlich [Antwort-Token](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/accessing-response-tokens.html).

## Version 2.5.0 - Juni 2021

* Unterstützung für Umleitungs-Personalisierungsangebote hinzugefügt.
* Automatisch erfasste Darstellungsfeldbreiten und -höhen, die negative Werte sind, werden nicht mehr an den Server gesendet.
* Wenn ein Ereignis durch Rückgabe von `false` aus einem `onBeforeEventSend` -Rückruf abgebrochen wird, wird jetzt eine Nachricht protokolliert.
* Es wurde ein Problem behoben, bei dem bestimmte XDM-Daten, die für ein einzelnes Ereignis vorgesehen waren, über mehrere Ereignisse hinweg einbezogen wurden.

## Version 2.4.0 - März 2021

* Das SDK kann jetzt [als NPM-Paket](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html?lang=de) installiert sein.
* Unterstützung für eine `out`-Option bei der [Konfiguration der standardmäßigen Einwilligung](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent) hinzugefügt, bei der alle Ereignisse bis zum Erhalt der Einwilligung gelöscht werden (die vorhandene `pending`-Option versetzt Ereignisse in die Warteschlange und sendet sie, sobald die Einwilligung eingeht).
* Der Rückruf [onBeforeEventSend](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#onbeforeeventsend) kann jetzt verwendet werden, um das Senden eines Ereignisses zu verhindern.
* Verwendet jetzt beim Senden von Ereignissen zu gerenderten oder angeklickten personalisierten Inhalten eine XDM-Schemafeldgruppe anstelle von `meta.personalization`.
* Der [getIdentity-Befehl](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html#retrieving-the-visitor-id) gibt jetzt die Edge-Regions-ID neben der Identität zurück.
* Die vom Server empfangenen Warnungen und Fehler wurden verbessert und werden entsprechend gehandhabt.
* Unterstützung für [Adobe Consent 2.0 Standard](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard) hinzugefügt.
* Die Voreinstellungen für die Zustimmung werden bei Erhalt gehasht und im lokalen Speicher gespeichert, um eine optimierte Integration zwischen CMPs, dem Platform Web SDK und dem Platform Edge Network zu ermöglichen. Wenn Sie Zustimmungsvoreinstellungen erfassen, empfehlen wir Ihnen jetzt, bei jedem Seitenladevorgang `setConsent` aufzurufen.
* Es wurden zwei [Monitoring-Hooks](https://github.com/adobe/alloy/wiki/Monitoring-Hooks), `onCommandResolved` und `onCommandRejected` hinzugefügt.
* Fehlerbehebung: Die Interaktionsbenachrichtigungsereignisse enthalten doppelte Informationen über dieselbe Aktivität, wenn ein Benutzer zu einer neuen Einzelseiten-App-Ansicht zurückkehrt, zur ursprünglichen Ansicht zurückkehrt und auf ein Element geklickt hat, das für die Konversion qualifiziert ist.
* Fehlerbehebung: Wenn das erste vom SDK gesendete Ereignis `documentUnloading` auf `true` gesetzt ist, wird [`sendBeacon`](https://developer.mozilla.org/de-DE/docs/Web/API/Navigator/sendBeacon) zum Senden des Ereignisses verwendet, was zu einem Fehler hinsichtlich einer nicht erstellten Identität führt.

## Version 2.3.0 - November 2020

* Nonce-Unterstützung wurde hinzugefügt, um strengere Richtlinien zur Inhaltssicherheit zu ermöglichen.
* Personalisierungsunterstützung für Einzelseitenanwendungen hinzugefügt.
* Verbesserte Kompatibilität mit anderen On-Page-JavaScript-Code, der möglicherweise `window.console`-APIs überschreibt.
* Fehlerbehebung: `sendBeacon` wurde nicht verwendet, wenn `documentUnloading` auf `true` gesetzt war oder wenn Link-Klicks automatisch verfolgt wurden.
* Fehlerbehebung: Ein Link wird nicht automatisch verfolgt, wenn das Ankerelement HTML-Inhalt enthält.
* Fehlerbehebung: Bestimmte Browser-Fehler, die eine schreibgeschützte `message` -Eigenschaft enthalten, wurden nicht ordnungsgemäß verarbeitet, was dazu führte, dass dem Kunden ein anderer Fehler angezeigt wurde.
* Fehlerbehebung: Wenn das SDK in einem iframe ausgeführt wird, tritt ein Fehler auf, wenn die HTML-Seite des iframe aus einer anderen Subdomäne stammt als die HTML-Seite des übergeordneten Fensters.

## Version 2.2.0 - Oktober 2020

* Fehlerbehebung: Das Opt-in-Objekt hinderte Alloy daran, Aufrufe durchzuführen, wenn `idMigrationEnabled` `true` ist.
* Fehlerbehebung: Machen Sie Alloy auf Anfragen aufmerksam, die Personalisierungsangebote zurückgeben sollen, um ein flackerndes Problem zu verhindern.

## Version 2.1.0 - August 2020

* Entfernen Sie den Befehl `syncIdentity` und unterstützen Sie die Übergabe dieser IDs im Befehl `sendEvent` .
* Unterstützung für IAB 2.0 Consent Standard.
* Unterstützung für die Übergabe zusätzlicher IDs im `setConsent`-Befehl.
* Unterstützung, die das `datasetId` im Befehl `sendEvent` überschreibt.
* Unterstützende Alloy-Monitore ([mehr dazu](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* Übergeben Sie `environment: browser` in die Kontextdaten der Implementierungsdetails.
