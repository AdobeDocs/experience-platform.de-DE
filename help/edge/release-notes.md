---
title: Versionshinweise zum Adobe Experience Platform Web-SDK
description: Die neuesten Versionshinweise für Adobe Experience Platform Web-SDK.
keywords: Adobe Experience Platform Web SDK; Platform Web SDK; Web SDK; Versionshinweise;
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
source-git-commit: 207fdd6d8a8dc27fa89798999734ba820f30fd54
workflow-type: tm+mt
source-wordcount: '1169'
ht-degree: 3%

---


# Versionshinweise

In diesem Dokument werden die Versionshinweise für das Adobe Experience Platform Web SDK behandelt.
Die neuesten Versionshinweise zur Web SDK-Tag-Erweiterung finden Sie in der [Versionshinweise zur Web SDK-Tag-Erweiterung](extension/web-sdk-ext-release-notes.md).

## Version 2.11.0 - 13. Juni 2022

**Neue Funktionen**

* Sie können jetzt personalisierte Erlebnisse genauer bereitstellen, indem Sie Besucher-IDs zwischen mobilen Apps und mobilen Webinhalten sowie domänenübergreifend freigeben. Siehe [dedizierte Dokumentation](identity/id-sharing.md) , um mehr zu erfahren.
* Sie können jetzt eine Reihe von Vorschlägen aus [!DNL Adobe Target] in Einzelseitenanwendungen, ohne die Analytics-Metriken zu erhöhen. Dadurch werden Berichtsfehler reduziert und die Analysegenauigkeit erhöht. Siehe [dedizierte Dokumentation](personalization/rendering-personalization-content.md#applypropositions) , um mehr zu erfahren.
* Zusätzliche Informationen zum `getLibraryInfo` -Befehl mit verfügbaren Befehlen und der endgültigen Konfiguration für die Instanz.

**Fehlerbehebungen und Verbesserungen**

* Die Cookie-Einstellungen zur Verwendung von `sameSite="none"` und `secure` Markierung auf [!DNL HTTPS] Seiten.
* Es wurde ein Problem behoben, bei dem personalisierter Inhalt bei Verwendung der Variablen `eq` Pseudo-Selektor.
* Es wurde ein Problem behoben, bei dem `localTimezoneOffset` konnte die Validierung der Experience Platform fehlschlagen.

## Version 2.10.1 - 3. Mai 2022

* Es wurde ein Problem behoben, bei dem mehrere beständige iFrames für ID-Synchronisationen und Segmentziele erstellt wurden.

## Version 2.10.0 - 22. April 2022

* Verwenden Sie einen beständigen iFrame für alle ID-Synchronisierungen und Segmentziele.
* Es wurde ein Problem behoben, bei dem zusammengeführte Metrikvorschläge im `sendEvent` Ergebnis.

## Version 2.9.0 - 10. März 2022

* Hinzugefügte Unterstützung für Tracking [!DNL control (default)] Adobe Target-Erlebnisse.
* Die Ansichtsänderungsereignisse für Einzelseitenanwendungen wurden optimiert. Die Benachrichtigung zur Anzeige ist jetzt beim Rendern personalisierter Erlebnisse in das Ansichtsänderungsereignis eingeschlossen.
* Konsolenwarnung wurde entfernt, wenn keine `eventType` vorhanden ist.
* Es wurde ein Problem behoben, bei dem die Variable `propositions` -Eigenschaft wurde nur von einer `sendEvent` -Befehl, wenn Erlebnisse aus dem Cache angefordert oder abgerufen wurden. Die `propositions` -Eigenschaft wird jetzt immer als Array definiert.
* Es wurde ein Problem behoben, bei dem ausgeblendete Container nicht angezeigt wurden, wenn ein Fehler von Adobe Experience Edge zurückgegeben wurde.
* Es wurde ein Problem behoben, bei dem die Interaktionsereignisse in Adobe Target nicht gezählt wurden. Dieses Problem wurde behoben, indem der Ansichtsname dem XDM unter web.webPageDetails.viewName hinzugefügt wurde.
* Es wurden fehlerhafte Dokumentationslinks in Konsolenmeldungen behoben.

## Version 2.8.0 - 19. Januar 2022

* Unterstützt Shadow-DOM-Selektoren für die Personalisierung.
* Die Ereignistypen für die Personalisierung wurden umbenannt. (`display` und `click` werden `decisioning.propositionDisplay` und `decisioning.propositionInteract`)
* Es wurde ein Problem behoben, bei dem HTML-Angebote mit Inline-Skript-Tags die Skript-Tags zweimal zur Seite hinzugefügt haben, obwohl das Skript nur einmal ausgeführt wurde.

## Version 2.7.0 - 26. Oktober 2021

* Zusätzliche Informationen aus Experience Edge im Rückgabewert von verfügbar machen `sendEvent`, einschließlich `inferences` und `destinations`. Das Format dieser Eigenschaften kann sich ändern, da diese Funktionen derzeit als Teil einer Beta-Version eingeführt werden. Weitere Informationen finden Sie unter [Tracking von Ereignissen.](fundamentals/tracking-events.md)

## Version 2.6.4 - 7. September 2021

* Es wurde ein Problem behoben, bei dem HTML Adobe Target-Aktionen auf die `head` -Element ersetzt wurde `head` Inhalt. Legen Sie jetzt HTML-Aktionen fest, die auf die `head` -Element geändert, um HTML anzuhängen.

## Version 2.6.3 - 16. August 2021

* Es wurde ein Problem behoben, bei dem Objekte, die nicht für die öffentliche Verwendung vorgesehen waren, über die aufgelöste Zusage aus dem `configure` Befehl.

## Version 2.6.2 - 4. August 2021

* Es wurde ein Problem behoben, bei dem eine Warnung zur Einstellung der `result.decisions` (gemäß `sendEvent` -Befehl) auch dann in der Konsole protokolliert werden, wenn die `result.decisions` nicht aufgerufen wurde. Beim Zugriff auf die `result.decisions` -Eigenschaft, aber die -Eigenschaft wird noch nicht unterstützt.

## Version 2.6.1 - 29. Juli 2021

* Es wurde ein Problem behoben, bei dem beim Rendern der Personalisierung für eine Einzelseiten-App-Ansicht ohne Personalisierungsinhalt ein Fehler ausgegeben wurde und das vom `sendEvent` zurückgewiesen werden.

## Version 2.6.0 - 27. Juli 2021

* Bietet mehr Personalisierungsinhalte im `sendEvent` aufgelöstes Versprechen, einschließlich Adobe Target-Antwort-Token. Wenn die `sendEvent` ausgeführt wird, wird ein Promise zurückgegeben, das schließlich mit einem `result` -Objekt, das Informationen enthält, die vom Server empfangen wurden. Zuvor enthielt dieses Ergebnisobjekt eine Eigenschaft mit dem Namen `decisions`. Diese `decisions` -Eigenschaft nicht mehr unterstützt. eine neue Eigenschaft, `propositions`wurde hinzugefügt. Diese neue Eigenschaft bietet Kunden Zugriff auf mehr Personalisierungsinhalte, darunter [Antwort-Token](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/accessing-response-tokens.html).

## Version 2.5.0 - Juni 2021

* Unterstützung für Umleitungs-Personalisierungsangebote hinzugefügt.
* Automatisch erfasste Darstellungsfeldbreiten und -höhen, die negative Werte sind, werden nicht mehr an den Server gesendet.
* Wenn ein Ereignis durch Rückgabe abgebrochen wird `false` von `onBeforeEventSend` -Rückruf, eine Nachricht wird nun protokolliert.
* Es wurde ein Problem behoben, bei dem bestimmte XDM-Daten, die für ein einzelnes Ereignis vorgesehen waren, über mehrere Ereignisse hinweg einbezogen wurden.

## Version 2.4.0 - März 2021

* Das SDK kann jetzt [als npm-Paket installiert](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html?lang=de).
* Hinzugefügte Unterstützung für eine `out` Option bei [Konfigurieren der Standardzustimmung](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent), wodurch alle Ereignisse gelöscht werden, bis die Zustimmung eingeht (die vorhandene `pending` -Option Ereignisse in die Warteschlange stellt und sie sendet, sobald die Zustimmung eingeht).
* Die [onBeforeEventSend-Rückruf](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#onbeforeeventsend) kann jetzt verwendet werden, um das Senden eines Ereignisses zu verhindern.
* Verwendet jetzt eine XDM-Schema-Feldergruppe anstelle von `meta.personalization` beim Senden von Ereignissen über die Wiedergabe oder das Klicken personalisierter Inhalte.
* Die [getIdentity-Befehl](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html#retrieving-the-visitor-id) gibt nun die ID der Edge-Region neben der Identität zurück.
* Die vom Server empfangenen Warnungen und Fehler wurden verbessert und werden entsprechend gehandhabt.
* Hinzugefügte Unterstützung für [Adobe Consent 2.0 standard](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard).
* Die Voreinstellungen für die Zustimmung werden bei Erhalt gehasht und im lokalen Speicher gespeichert, um eine optimierte Integration zwischen CMPs, dem Platform Web SDK und dem Platform Edge Network zu ermöglichen. Wenn Sie Zustimmungsvoreinstellungen erfassen, empfehlen wir Ihnen jetzt, `setConsent` bei jedem Laden der Seite.
* Zwei [Überwachungshooks](https://github.com/adobe/alloy/wiki/Monitoring-Hooks), `onCommandResolved` und `onCommandRejected`hinzugefügt.
* Fehlerbehebung: Die Interaktionsbenachrichtigungsereignisse enthalten doppelte Informationen über dieselbe Aktivität, wenn ein Benutzer zu einer neuen Einzelseiten-App-Ansicht zurückkehrt, zur ursprünglichen Ansicht zurückkehrt und auf ein Element geklickt hat, das für die Konversion qualifiziert ist.
* Fehlerbehebung: Wenn das erste vom SDK gesendete Ereignis `documentUnloading` auf `true`, [`sendBeacon`](https://developer.mozilla.org/de-DE/docs/Web/API/Navigator/sendBeacon) zum Senden des Ereignisses verwendet werden, was zu einem Fehler hinsichtlich einer nicht festzustellenden Identität führt.

## Version 2.3.0 - November 2020

* Nonce-Unterstützung wurde hinzugefügt, um strengere Richtlinien zur Inhaltssicherheit zu ermöglichen.
* Personalisierungsunterstützung für Einzelseitenanwendungen hinzugefügt.
* Verbesserte Kompatibilität mit anderen On-Page-JavaScript-Code, der möglicherweise überschrieben wird `window.console` APIs.
* Fehlerbehebung: `sendBeacon` wurde nicht verwendet, wenn `documentUnloading` auf `true` oder wenn Link-Klicks automatisch verfolgt wurden.
* Fehlerbehebung: Ein Link wird nicht automatisch verfolgt, wenn das Ankerelement HTML-Inhalt enthält.
* Fehlerbehebung: Bestimmte Browser-Fehler, die schreibgeschützt sind `message` -Eigenschaft nicht ordnungsgemäß verarbeitet wurden, was dazu führte, dass dem Kunden ein anderer Fehler angezeigt wurde.
* Fehlerbehebung: Wenn das SDK in einem iframe ausgeführt wird, tritt ein Fehler auf, wenn die HTML-Seite des iframe von einer anderen Subdomäne als der HTML-Seite des übergeordneten Fensters stammt.

## Version 2.2.0 - Oktober 2020

* Fehlerbehebung: Das Opt-in-Objekt hinderte Alloy an Aufrufen, wenn `idMigrationEnabled` is `true`.
* Fehlerbehebung: Machen Sie Alloy auf Anfragen aufmerksam, die Personalisierungsangebote zurückgeben sollen, um ein flackerndes Problem zu verhindern.

## Version 2.1.0 - August 2020

* Entfernen Sie die `syncIdentity` -Befehl und unterstützen die Übergabe dieser IDs in der `sendEvent` Befehl.
* Unterstützung für IAB 2.0 Consent Standard.
* Unterstützung für die Übergabe zusätzlicher IDs im `setConsent` Befehl.
* Unterstützung, die die `datasetId` im `sendEvent` Befehl.
* Alloy-Monitore unterstützen ([Mehr dazu](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* Pass `environment: browser` in der Implementierung finden Sie Kontextdaten.
