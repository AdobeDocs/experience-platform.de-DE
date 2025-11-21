---
title: Versionshinweise zum Adobe Experience Platform Web-SDK
description: Die neuesten Versionshinweise für Adobe Experience Platform Web-SDK.
keywords: Adobe Experience Platform Web SDK;Experience Platform Web SDK;Web SDK;Versionshinweise;
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
source-git-commit: 466938163cc4f453c40da3709f556a53be334728
workflow-type: tm+mt
source-wordcount: '2585'
ht-degree: 58%

---


# Versionshinweise zu Web SDK

In diesem Dokument werden die Versionshinweise für das Adobe Experience Platform Web SDK behandelt.
Die neuesten Versionshinweise zur Web SDK-Tag-Erweiterung finden Sie in den [Versionshinweisen zur Tag-Erweiterung für Web SDK](../tags/extensions/client/web-sdk/web-sdk-ext-release-notes.md).

## Version 2.30.0 – Donnerstag, 24. September 2025

**Neue Funktionen**

- Die Anzeige von Push-Benachrichtigungen wird nun unterstützt.

## Version 2.29.0 – Freitag, 4. September 2025

**Neue Funktionen**

- Unterstützung für die Erfassung von Adobe Advertising-Daten für Adobe Journey Analytics wurde hinzugefügt
- Unterstützung für die Aufzeichnung von Push-Abonnementdetails in den Benutzerprofilen hinzugefügt.

**Fehlerbehebungen und Verbesserungen**

- Es wurde ein Problem behoben, bei dem Konfigurationsüberschreibungsabschnitte zusammengeführt anstatt ersetzt wurden.
- Fehlerkorrektur - Die Link-Sammlung sendet jetzt den gesamten Dokumentinhalt als Link-Name.
- Es wurde ein Problem behoben, bei dem bestimmte Vorschläge nicht erneut gerendert werden konnten.

## Version 2.28.1 – Freitag, 31. Juli 2025

**Fehlerbehebungen und Verbesserungen**

- Es wurde ein Problem behoben, das die Ausführung benutzerdefinierter Builds verhinderte.

## Version 2.28.0 – Freitag, 24. Juli 2025

**Neue Funktionen**

- Es wurde Unterstützung für Adobe Journey Optimizer-Disqualifikationsregeln hinzugefügt.

**Fehlerbehebungen und Verbesserungen**

- Fehlerkorrektur - Im [Media Analytics-Tracker](commands/getmediaanalyticstracker.md) akzeptiert die `length`-Eigenschaft des Medienobjekts jetzt korrekt ungültige Datentypen.
- Verbesserte [Identitätsverwaltung](identity/overview.md) Fehlerbehandlung, um die Versprechensablehnung ordnungsgemäß zu verarbeiten, wenn die Identitätssuche fehlschlägt.
- Es wurde ein Problem behoben[&#x200B; bei dem &#x200B;](personalization/rendering-personalization-content.md)Personalisierungsinhalt) mit HTML-Inhaltselementen nicht gerendert werden konnten und ein Fehler im Zusammenhang mit einer fehlenden `renderStatusHandler` auftrat.
- Activity Map (URL[Sammlung) wurde korrigiert](commands/configure/clickcollectionenabled.md) um Nicht-HTTP-URLs ordnungsgemäß zu verarbeiten.

**Bekannte Probleme**

- Der [benutzerdefinierte Build](/help/web-sdk/install/create-custom-build.md)-Prozess mit `npx @adobe/alloy` funktioniert derzeit nicht wie erwartet in Version 2.28.0. Alle Komponenten sind unabhängig von den ausgewählten Modulen im generierten Build enthalten. Dieses Problem hat keine Auswirkungen auf die standardmäßige JavaScript-Datei, die im CDN verfügbar ist. Es wird eine Fehlerbehebung durchgeführt.

## Version 2.27.0 – Mittwoch, 20. Mai 2025

**Fehlerbehebungen und Verbesserungen**

- Es wurde ein Problem mit In-App-Nachrichten behoben, bei dem der benutzerdefinierte Stil nicht korrekt angewendet wurde.
- hat das Format des Ereignisverlaufs geändert. Dadurch werden In-App-Nachrichten und Inhaltskarten erneut angezeigt, wenn die alten Verlaufsdaten gelöscht werden.
- Es wurde ein Problem behoben, bei dem Vorschläge in SPA-Anwendungsfällen erneut angewendet wurden.
- Es wurde ein Problem beim Klick-Tracking für Shadow-DOM-Elemente behoben.

## Version 2.26.0 – Donnerstag, 5. März 2025

**Neue Funktionen**

- Sie können jetzt das NPM-Paket von Web SDK verwenden, um benutzerdefinierte Web-SDK-Builds zu erstellen und nur die benötigten Bibliothekskomponenten auszuwählen. Dies führt zu einer geringeren Bibliotheksgröße und optimierten Ladezeiten. Weitere Informationen finden Sie in der Dokumentation [&#x200B; Erstellen eines benutzerdefinierten Web-SDK-Builds mit dem NPM-Paket &#x200B;](install/create-custom-build.md).
- Der [`getIdentity`](commands/getidentity.md)-Befehl liest jetzt automatisch die ECID direkt aus dem `kndctr`-Identitäts-Cookie. Wenn Sie `getIdentity` mit dem Namespace `ECID` aufrufen und bereits ein Identitäts-Cookie vorhanden ist, sendet Web SDK keine Anfrage mehr an die Edge Network, um die Identität abzurufen. Jetzt liest es die Identität aus dem Cookie.

**Fehlerbehebungen und Verbesserungen**

- Es wurde ein Problem behoben, bei dem `getIdentity` Befehle nach dem Senden eines `collect`-Aufrufs die Identität nicht zurückgaben.
- Es wurde ein Problem behoben, bei dem Personalisierungs-Umleitungen dazu führten, dass Inhalte flackerten, bevor die Umleitung stattfand.

## Version 2.25.0 – Freitag, 23. Januar 2025

**Behoben und Verbesserungen**

- Dem `setDebug`-Befehl wurde eine Optionsvalidierung hinzugefügt.
- Es wurde eine Warnung hinzugefügt, die angezeigt wird, wenn eine `onBeforeLinkClickSend`-Funktion oder ein Download-Link-Qualifizierer konfiguriert wird, wenn die Klick-Sammlung deaktiviert ist.
- Es wurde ein Problem behoben, bei dem gerenderte Vorschläge nicht in Anzeigebenachrichtigungen enthalten waren.

**Neue Funktionen**

- Es wurde ein Fallback auf die konfigurierte Edge-Domain implementiert, wenn Drittanbieter-Cookies aktiviert und Anfragen an adobedc.demdex.net blockiert werden.

## Version 2.24.1 – Samstag, 6. Dezember 2024

**Behoben und Verbesserungen**

- Es wurde ein Abhängigkeitsproblem im Zusammenhang mit der [Adobe Experience Platform-Regel](https://github.com/adobe/aepsdk-rulesengine-typescript/)Engine behoben, das in einigen Kundenintegrationen zu Fehlern führte. Für Web SDK ist jetzt die [Adobe Experience Platform-Regel](https://github.com/adobe/aepsdk-rulesengine-typescript/)Engine, Version 2.0.3 oder höher, erforderlich.

## Version 2.24.0 – Freitag, 31. Oktober 2024

**Neue Funktionen**

- [Datenstrom-Überschreibungen](../datastreams/overrides.md) werden jetzt beim Starten von Mediensitzungen unterstützt.

- Unterstützung für Adobe Target-Antwort-Token im Überwachungs[`onContentRendering`](monitoring-hooks.md#onContentRendering)Hook hinzugefügt.

**Fehlerbehebungen und Verbesserungen**

- Wenn mehrere In-App-Nachrichten zurückgegeben werden, wird nur die Nachricht mit der höchsten Priorität angezeigt. Die anderen werden als unterdrückt aufgezeichnet.
- Leere Datenstrom-Überschreibungen werden nicht mehr an die Edge Network gesendet, wodurch potenzielle Konflikte mit Server-seitigen Routing-Konfigurationen reduziert werden.
- Die folgenden Namen der Protokollnachrichtenkomponenten wurden umbenannt, um sie an andere Adobe-SDKs anzupassen:
   - `DecisioningEngine` wurde in `RulesEngine` umbenannt
   - `LegacyMediaAnalytics` wurde in `MediaAnalyticsBridge` umbenannt
   - `Privacy` wurde in `Consent` umbenannt
- Fehlerkorrektur - Beim Rendern von Standardinhaltelementen über [`applyPropositions`](../web-sdk/commands/applypropositions.md) tritt jetzt kein Fehler mehr auf.
- Ein CSS-Fehler in Aktionen zum Verschieben und Ändern der Größe von Adobe Target wurde behoben.
- Der `machineLearning` Schlüssel wurde aus [`sendEvent`](../web-sdk/commands/sendevent/overview.md) Antworten entfernt.

## Version 2.23.0 – Freitag, 19. September 2024

**Neue Funktionen**

- Unterstützung für das Anfordern der [CORE ID](identity/overview.md#tracking-coreid-web-sdk) im Befehl [getIdentity](commands/getidentity.md#get-identity-using-the-web-sdk-javascript-library) hinzugefügt.

**Fehlerbehebungen und Verbesserungen**

- Es wurde ein Problem behoben, bei dem Cookies bei der lokalen Ausführung der Web-SDK nicht korrekt geschrieben wurden.

## Version 2.22.0 – Freitag, 22. August 2024

**Neue Funktionen**

- Es wurde Unterstützung für Hooks zur Personalisierungsüberwachung hinzugefügt.

**Fehlerbehebungen und Verbesserungen**

- Die Unterstützung für Internet Explorer wurde entfernt, wodurch die Gzip-Größe der Bibliothek um 9 % verringert wurde.
- Es wurde ein Problem behoben, bei dem Activity Map-Link-Details nicht initialisiert wurden, wenn der `onInstanceConfigured` Monitor-Hook aufgerufen wurde.
- Es wurde ein Problem behoben, bei dem Cookie-Ziele nicht auf den richtigen Pfad eingestellt wurden.
- Es wurde ein Kundenproblem mit einem -Aufruf an behoben.
- Es wurde ein Problem behoben, bei dem eine ungültige URL-Codierung im `adobe_mc`-Parameter dazu führte, [sendEvent](commands/sendevent/overview.md)-Aufrufe fehlschlugen.

## Version 2.21.1 – Freitag, 18. Juli 2024

**Fehlerbehebungen und Verbesserungen**

- Fehlerkorrektur - Bei der Verwendung der NPM-Bibliothek tritt jetzt kein Build-Fehler mehr auf.

## Version 2.21.0 – Mittwoch, 16. Juli 2024

**Neue Funktionen**

- Unterstützung für die automatische Interaktionsverfolgung von Vorschlägen wurde hinzugefügt.
- Es wurde ein benutzerdefiniertes Build-Skript hinzugefügt, das eine alloy.js-Datei bereitstellt.
- Verbesserte Klick-Sammlung mit ActivityMap- und Ereignisgruppierungsunterstützung.

## Version 2.20.0 – Mittwoch, 21. Mai 2024

**Neue Funktionen**

- Es wurde Unterstützung für [Streaming Media Collection](../web-sdk/commands/configure/streamingmedia.md) hinzugefügt.

**Fehlerbehebungen und Verbesserungen**

- Es wurde ein Fehler behoben, der dazu führte, dass der Standardinhalt durch den Code-Ausschnitt zum Vorab-Ausblenden ausgeblendet wurde, wenn das Einverständnis abgelehnt wurde.

## Version 2.19.2 – Donnerstag, 10. Januar 2024

**Fehlerbehebungen und Verbesserungen**

- Es wurde ein Problem behoben, bei dem Identitätsfehler andere Fehler maskierten und Identitätsfehler in Warnungen änderten.
- Es wurde ein Problem behoben, bei dem Seitenaufrufe am Ende nie gesendet wurden, wenn der Seitenaufruf am Anfang war und `renderDecisions` auf `false` gesetzt war.
- Es wurde ein Problem behoben, bei dem Web SDK beim Lesen domänenübergreifender Identitäten mehrere `adobe_mc` Abfragezeichenfolgenparameter aufwies.

## Version 2.19.1 – Samstag, 10. November 2023

**Fehlerbehebungen und Verbesserungen**

- Es wurde ein Problem behoben, bei dem das Vorschläge-Array, das von `sendEvent` Aufrufen zurückgegeben wurde, immer leer war.

## Version 2.19.0 – Donnerstag, 1. November 2023

**Neue Funktionen**

- Unterstützung für das Rendern von In-App-Nachrichten von Adobe Journey Optimizer wurde hinzugefügt.
- Es wurde Unterstützung für [Ereignisse oben und unten auf der Seite](use-cases/top-bottom-page-events.md) hinzugefügt.
- Dem [`defaultPersonalizationEnabled`](commands/sendevent/personalization.md)-Befehl wurde `sendEvent` Option hinzugefügt, um das Anfordern des seitenweiten Bereichs und der Standardoberfläche zu steuern.

**Fehlerbehebungen und Verbesserungen**

- Kombinierte Personalisierung zeigt Ereignisse zusammen an, wenn mehrere Personalisierungstypen gerendert werden.
- Es wurde ein Problem behoben, bei dem bei den Ansichtsnamen einer Einzelseitenanwendung die Groß-/Kleinschreibung beachtet wurde.
- Es wurde ein Problem mit personalisierten Shadow-DOM-Angebotsselektoren behoben.

## Version 2.18.0 – 31. Juli 2023

**Neue Funktionen**

- Unterstützung für [Überschreibungen der Datenstrom-ID pro Befehl](../datastreams/overrides.md) hinzugefügt.

**Fehlerbehebungen und Verbesserungen**

- Es wurde ein Problem behoben, durch das Beenden-Links nicht qualifiziert werden konnten, da die Domain Teil der Abfrage war.
- Statt `edgeConfigId` wird jetzt `datastreamId` in der Web SDK-Konfiguration unterstützt.

## Version 2.17.0 – 17. Mai 2023

**Fehlerbehebungen und Verbesserungen**

- Das Web SDK kodiert jetzt die Zielwerte der Audience Manager-Cookies, ähnlich wie bei der [Data Integration Library (DIL)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=de).

## Version 2.16.0 – 25. April 2023

**Neue Funktionen**

- Es wurde Unterstützung für [Überschreibungen der Datenstromkonfiguration](../datastreams/overrides.md) hinzugefügt.

## Version 2.15.0 – 30. März 2023

**Neue Funktionen**

- Unterstützung für [`onBeforeLinkClickSend`](/help/web-sdk/commands/configure/onbeforelinkclicksend.md) Link-Klick-Rückruf hinzugefügt.
- Adobe Journey Optimizer-Klick-Tracking wird nun unterstützt.

**Fehlerbehebungen und Verbesserungen**

- Die Link-Erfassung enthält jetzt den Link-Namen und die Besucherregion.
- Konsolenfehler für fehlgeschlagene URL-Ziele wurde entfernt.

## Version 2.14.0 – 25. Januar 2023

- (Beta) Zusätzliche Unterstützung für Adobe Journey Optimizer-Oberflächen und Vorschläge.

**Fehlerbehebungen und Verbesserungen**

- Es wurde ein Problem mit benutzerspezifischen Adobe Target-VEC-Code-Aktionen behoben, bei denen sich der Code an einer anderen Stelle als bei [!DNL at.js] befand.
- Es wurde ein Problem behoben, bei dem die „Referer“-Kopfzeile in manchen Edge-Fällen nicht ordnungsgemäß auf Anforderungen an das Edge-Netzwerk festgelegt wurde.
- Es wurde ein Problem behoben, bei dem Eigenschaften von [Client-Hinweisen für Benutzeragenten- und -agentinnen](/help/web-sdk/use-cases/client-hints.md) auf einen falschen Typ eingestellt werden konnten.
- Es wurde ein Problem behoben, bei dem `placeContext.localTime` nicht mit dem Schema übereinstimmte.

## Version 2.13.1 – 13. Oktober 2022

- Es wurde ein Problem behoben, bei dem die Besuchermigration nicht funktionierte, wenn window.Visitor nach der Konfiguration definiert wurde. Dies ist insbesondere bei der Ausführung mit Adobe-Tags ein Problem.
- Es wurde ein Problem behoben, bei dem `device.screenWidth` und `device.screenHeight` in einigen Umgebungen als Zeichenfolgen gefüllt wurden.

## Version 2.13.0 – 28. September 2022

**Neue Funktionen**

- Es wurde Unterstützung für [seitenweise vollständige Migration](home.md#migrating-to-web-sdk) hinzugefügt. Das Adobe Target-Profil wird jetzt beibehalten, wenn Besuchende zwischen at.js- und Web SDK-Seiten wechseln.
- Es wurde konfigurierbare Unterstützung für [hohe Entropie bei Client-Hinweisen für Benutzeragenten](/help/web-sdk/use-cases/client-hints.md) hinzugefügt.
- Es wurde Unterstützung für den [`applyResponse`](/help/web-sdk/commands/applyresponse.md)-Befehl hinzugefügt. Dies ermöglicht die hybride Personalisierung über die [Edge Network-API](https://developer.adobe.com/data-collection-apis/docs/api/).
- QA-Modus-Links funktionieren jetzt über mehrere Seiten.

**Fehlerbehebungen und Verbesserungen**

- Es wurde ein Problem behoben, bei dem Metriken für Personalisierungs-Klick-Tracking nicht aktualisiert wurden, wenn das Linktracking deaktiviert war.
- Befehle für das Auslösen eines Validierungsfehlers, wenn unbekannte Optionen angegeben waren, wurden aktualisiert.
- Die `_experience.decisioning.propositionEventType`-Eigenschaft wird jetzt beim automatischen Senden von Anzeige- und Interaktions-Personalisierungsereignissen gefüllt.
- Es wurde eine duplizierte Namespace-Validierung für den `getIdentity`-Befehl hinzugefügt.
- Es wurde eine duplizierte Validierung des Entscheidungsumfangs für den `sendEvent`-Befehl hinzugefügt.

## Version 2.12.0 – 29. Juni 2022

- Ändern Sie die Anforderungen an das Edge-Netzwerk, um den `cluster`-Cookie-Standorthinweis als Teil der URL zu verwenden. Dadurch wird sichergestellt, dass Benutzende, die ihren Standort während der Sitzung ändern (z. B. über ein VPN oder durch Mobilgeräte usw.), denselben Edge erreichen und über dasselbe Personalisierungsprofil verfügen.
- Konvertieren Sie die konfigurierten Funktionen in der Befehlsantwort getLibraryInfo in eine Zeichenfolge.

## Version 2.11.0 – 13. Juni 2022

**Neue Funktionen**

- Sie können jetzt personalisierte Erlebnisse präziser bereitstellen, indem Sie Besucher-IDs zwischen mobilen Apps und mobilen Webinhalten sowie domänenübergreifend freigeben. Weitere Informationen finden Sie in der [spezifischen Dokumentation](identity/id-sharing.md).
- Sie können jetzt ein Vorschläge-Array von [!DNL Adobe Target] in Einzelseitenanwendungen rendern oder ausführen, ohne die Analysemetriken zu inkrementieren. Dadurch werden Berichtsfehler reduziert und die Analysegenauigkeit erhöht. Weitere Informationen finden Sie in der [spezifischen Dokumentation](personalization/rendering-personalization-content.md#applypropositions).
- Zusätzliche Informationen zum `getLibraryInfo`-Befehl, einschließlich verfügbarer Befehle und der endgültigen Konfiguration für die Instanz, wurden hinzugefügt.

**Fehlerbehebungen und Verbesserungen**

- Die Cookie-Einstellungen zur Verwendung von `sameSite="none"`- und `secure`-Markierungen auf [!DNL HTTPS]-Seiten wurden aktualisiert.
- Es wurde ein Problem behoben, bei dem personalisierter Inhalt bei Verwendung der `eq`-Pseudoauswahl nicht korrekt angewandt wurde.
- Es wurde ein Problem behoben, bei dem `localTimezoneOffset` zum Fehlschlagen der Experience Platform-Validierung führen konnte.

## Version 2.10.1 – 3. Mai 2022

- Es wurde ein Problem behoben, bei dem mehrere persistente iFrames für ID-Synchronisationen und Segmentziele erstellt wurden.

## Version 2.10.0 – 22. April 2022

- Verwenden Sie einen persistenten iFrame für alle ID-Synchronisierungen und Segmentziele.
- Es wurde ein Problem behoben, bei dem zusammengeführte Metrikvorschläge im `sendEvent`-Ergebnis dupliziert wurden.

## Version 2.9.0 – 10. März 2022

- Unterstützung für das Tracking von [!DNL control (default)] Adobe Target-Erlebnissen wurde hinzugefügt.
- Die Ansichtsänderungsereignisse für Einzelseitenanwendungen wurden optimiert. Die Anzeigebenachrichtigung ist jetzt beim Rendern personalisierter Erlebnisse im Ansichtsänderungsereignis enthalten.
- Die Konsolenwarnung wurde entfernt, wenn `eventType` nicht vorhanden ist.
- Es wurde ein Problem behoben, bei dem die `propositions`-Eigenschaft nur von einem `sendEvent`-Befehl zurückgegeben wurde, wenn Erlebnisse aus dem Cache angefordert oder abgerufen wurden. Die `propositions`-Eigenschaft wird jetzt immer als Array definiert.
- Es wurde ein Problem behoben, bei dem ausgeblendete Container nicht angezeigt wurden, wenn ein Fehler von der Edge Network zurückgegeben wurde.
- Es wurde ein Problem behoben, bei dem die Interaktionsereignisse in Adobe Target nicht gezählt wurden. Dieses Problem wurde behoben, indem der Ansichtsname unter web.webPageDetails.viewName zu XDM hinzugefügt wurde.
- Es wurden fehlerhafte Dokumentationslinks in Konsolenmeldungen behoben.

## Version 2.8.0 – 19. Januar 2022

- Unterstützung für Schatten-DOM-Selektoren für die Personalisierung.
- Die Ereignistypen für die Personalisierung wurden umbenannt. (`display` und `click` werden zu `decisioning.propositionDisplay` und `decisioning.propositionInteract`)
- Es wurde ein Problem behoben, bei dem HTML-Angebote mit Inline-Skript-Tags die Skript-Tags zweimal zur Seite hinzugefügt haben, obwohl das Skript nur einmal ausgeführt wurde.

## Version 2.7.0 – 26. Oktober 2021

- Zusätzliche Informationen aus der Edge Network werden im Rückgabewert von `sendEvent` verfügbar gemacht, einschließlich `inferences` und `destinations`. Das Format dieser Eigenschaften kann sich ändern, da diese Funktionen derzeit als Teil einer Beta eingeführt werden.

## Version 2.6.4 – 7. September 2021

- Es wurde ein Problem behoben, bei dem setHTML-Aktionen von Adobe Target, die auf das `head`-Element angewendet wurden, den gesamten `head`-Inhalt ersetzt haben. Jetzt werden setHTML-Aktionen, die auf das `head`-Element angewendet werden, so geändert, dass HTML angehängt wird.

## Version 2.6.3 – 16. August 2021

- Es wurde ein Problem behoben, bei dem Objekte, die nicht für die öffentliche Verwendung vorgesehen waren, über die aufgelöste Zusage aus dem `configure`-Befehl verfügbar gemacht wurden.

## Version 2.6.2 – 4. August 2021

- Es wurde ein Problem behoben, bei dem eine Warnung zur Einstellung von `result.decisions` (bereitgestellt vom `sendEvent`-Befehl) auch dann in der Konsole protokolliert wird, wenn die `result.decisions`-Eigenschaft nicht aufgerufen wurde. Beim Zugriff auf die `result.decisions`-Eigenschaft wird keine Warnung protokolliert, aber die Eigenschaft wird dennoch eingestellt.

## Version 2.6.1 – 29. Juli 2021

- Es wurde ein Problem behoben, bei dem beim Rendern der Personalisierung für eine Einzelseiten-App-Ansicht ohne Personalisierungsinhalt ein Fehler ausgegeben und die vom `sendEvent`-Befehl zurückgegebene Zusage zurückgewiesen wurde.

## Version 2.6.0 – 27. Juli 2021

- Bietet mehr Personalisierungsinhalte in der aufgelösten `sendEvent`-Zusage, einschließlich Adobe Target-Antwort-Token. Wenn der `sendEvent`-Befehl ausgeführt wird, wird eine Zusage zurückgegeben, die schließlich mit einem `result`-Objekt aufgelöst wird, das Informationen enthält, die vom Server empfangen wurden. Zuvor enthielt dieses Ergebnisobjekt eine Eigenschaft mit dem Namen `decisions`. Diese `decisions`-Eigenschaft wird nicht mehr unterstützt. Die neue Eigenschaft `propositions` wurde hinzugefügt. Diese neue Eigenschaft bietet Kundinnen und Kunden Zugriff auf mehr Personalisierungsinhalte, darunter [Antwort-Token](/help/web-sdk/personalization/adobe-target/accessing-response-tokens.md).

## Version 2.5.0 – Juni 2021 

- Unterstützung für Umleitungspersonalisierungsangebote wurde hinzugefügt.
- Automatisch erfasste Darstellungsfeldbreiten und -höhen, die negative Werte sind, werden nicht mehr an den Server gesendet.
- Wenn ein Ereignis durch Rückgabe von `false` von einem `onBeforeEventSend`-Rückruf abgebrochen wird, wird jetzt eine Meldung protokolliert.
- Es wurde ein Problem behoben, bei dem bestimmte XDM-Daten, die für ein einzelnes Ereignis vorgesehen waren, über mehrere Ereignisse hinweg einbezogen wurden.

## Version 2.4.0 – März 2021 

- SDK kann jetzt als NPM[Paket installiert &#x200B;](/help/web-sdk/install/npm.md).
- Es wurde Unterstützung für eine `out`-Option beim [Konfigurieren des Standardeinverständnisses](/help/web-sdk/commands/configure/defaultconsent.md) hinzugefügt, wodurch alle Ereignisse ignoriert werden, bis das Einverständnis eingeht (die vorhandene `pending`-Option stellt Ereignisse in die Warteschlange und sendet sie, sobald das Einverständnis eingeht).
- Der [`onBeforeEventSend`](/help/web-sdk/commands/configure/onbeforeeventsend.md)-Callback kann jetzt verwendet werden, um das Senden eines Ereignisses zu verhindern.
- Jetzt wird eine XDM-Schemafeldgruppe anstelle von `meta.personalization` verwendet, wenn Ereignisse über gerenderte oder angeklickte personalisierte Inhalte gesendet werden.
- Der Befehl [`getIdentity`](/help/web-sdk/commands/getidentity.md) gibt jetzt die ID der Edge-Region zusammen mit der Identität zurück.
- Die vom Server empfangenen Warnungen und Fehler wurden verbessert und werden nun auf besser geeignete Weise gehandhabt.
- Es wurde Unterstützung für Adobe Consent 2.0 Standard für den [`setConsent`](/help/web-sdk/commands/setconsent.md) hinzugefügt.
- Die Einverständnisvoreinstellungen werden bei Erhalt gehasht und im lokalen Speicher gespeichert, um eine optimierte Integration zwischen CMPs, Experience Platform Web SDK und Experience Platform Edge Network zu ermöglichen. Wenn Sie Einverständnisvoreinstellungen erfassen, empfehlen wir Ihnen jetzt, `setConsent` bei jedem Laden der Seite aufzurufen.
- Es wurden zwei [Überwachungs-Hooks](https://github.com/adobe/alloy/wiki/Monitoring-Hooks), `onCommandResolved` und `onCommandRejected`, hinzugefügt.
- Fehlerbehebung: Die Benachrichtigungsereignisse für Personalisierungsinteraktionen enthielten doppelte Informationen über dieselbe Aktivität, wenn Benutzende zu einer neuen Singe-Page-App-Ansicht navigiert haben, zur ursprünglichen Ansicht zurückgekehrt sind und dann auf ein für die Konversion qualifiziertes Element geklickt haben.
- Fehlerbehebung: Wenn beim ersten vom SDK gesendeten Ereignis `documentUnloading` auf `true` eingestellt war, wurde [`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon) zum Senden des Ereignisses verwendet, was zu einem Fehler in Bezug auf eine nicht hergestellte Identität führte.

## Version 2.3.0 – November 2020

- Es wurde Nonce-Unterstützung hinzugefügt, um strengere Richtlinien zur Inhaltssicherheit zu ermöglichen.
- Es wurde Personalisierungsunterstützung für Single-Page-Apps hinzugefügt.
- Die Kompatibilität mit anderem JavaScript-Code auf der Seite wurde verbessert, durch den `window.console`-APIs möglicherweise überschrieben werden.
- Fehlerbehebung: `sendBeacon` wurde nicht verwendet, wenn `documentUnloading` auf `true` eingestellt war oder Klicks auf Links automatisch verfolgt wurden.
- Fehlerbehebung: Ein Link wurde bei einem Ankerelement mit HTML-Inhalt nicht automatisch verfolgt.
- Fehlerbehebung: Bestimmte Browser-Fehler mit einer schreibgeschützten `message`-Eigenschaft wurden nicht ordnungsgemäß verarbeitet, sodass auf Kundenseite ein anderer Fehler angezeigt wurde.
- Fehlerbehebung: Bei SDK-Ausführung in einem iframe ist ein Fehler aufgetreten, wenn die HTML-Seite des iframe von einer anderen Subdomain als der HTML-Seite des übergeordneten Fensters stammte.

## Version 2.2.0 – Oktober 2020

- Fehlerbehebung: Das Opt-in-Objekt hinderte Web SDK daran, Aufrufe durchzuführen, wenn `idMigrationEnabled` `true` wurde.
- Fehlerbehebung: Machen Sie Web SDK auf Anfragen aufmerksam, die Personalisierungsangebote zurückgeben sollten, um ein flackerndes Problem zu verhindern.

## Version 2.1.0 – August 2020

- Der Befehl `syncIdentity` wurde entfernt, und die Übergabe dieser IDs an den Befehl `sendEvent` wird unterstützt.
- Es wurde Unterstützung für den IAB 2.0-Einverständnisstandard hinzugefügt.
- Es wurde Unterstützung für die Übergabe zusätzlicher IDs im Befehl `setConsent` hinzugefügt.
- Es wurde Unterstützung zum Außerkraftsetzen von `datasetId` im Befehl `sendEvent` hinzugefügt.
- Überwachungs-Hooks für Support [mehr dazu](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
- `environment: browser` wird nun in den Kontextdaten der Implementierungsdetails übergeben.
