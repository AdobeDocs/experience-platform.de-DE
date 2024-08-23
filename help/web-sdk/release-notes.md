---
title: Versionshinweise zum Adobe Experience Platform Web-SDK
description: Die neuesten Versionshinweise für Adobe Experience Platform Web-SDK.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;Versionshinweise;
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
source-git-commit: 73a82825dd6c9ae97db76018df5462ab20c7d15e
workflow-type: tm+mt
source-wordcount: '1882'
ht-degree: 78%

---


# Versionshinweise

In diesem Dokument werden die Versionshinweise für das Adobe Experience Platform Web SDK behandelt.
Die neuesten Versionshinweise zur Web SDK-Tag-Erweiterung finden Sie in den [Versionshinweisen zur Tag-Erweiterung für Web SDK](../tags/extensions/client/web-sdk/web-sdk-ext-release-notes.md).

## Version 2.22.0 – Freitag, 22. August 2024

**Neue Funktionen**

- Es wurden Personalisierungsmonitore hinzugefügt.

**Fehlerbehebungen und Verbesserungen**

- Die Unterstützung für Internet Explorer wurde entfernt und die Größe der Bibliothek gzip um 9 % verringert.
- Es wurde ein Problem behoben, bei dem die Details des Activity Map-Links nicht initialisiert wurden, wenn der Erweiterungspunkt `onInstanceConfigured` für den Monitor aufgerufen wurde.
- Es wurde ein Problem behoben, bei dem Cookie-Ziele nicht auf den richtigen Pfad gesetzt wurden.
- Es wurde ein Kundenproblem behoben, das beim -Aufruf auftrat.
- Es wurde ein Problem behoben, bei dem eine ungültige URL-Kodierung im Parameter `adobe_mc` dazu führte, dass [sendEvent](commands/sendevent/overview.md) -Aufrufe fehlschlugen.

## Version 2.21.1 – Freitag, 18. Juli 2024

**Fehlerbehebungen und Verbesserungen**

- Fehlerkorrektur - bei der Verwendung der NPM-Bibliothek tritt kein Build mehr auf.

## Version 2.21.0 – Mittwoch, 16. Juli 2024

**Neue Funktionen**

- Unterstützung für das automatische Tracking von Vorschlagsinteraktionen hinzugefügt.
- Es wurde ein benutzerdefiniertes Build-Skript hinzugefügt, das eine Datei vom Typ &quot;legate.js&quot;bereitstellt.
- Verbesserte Klick-Sammlung mit Unterstützung für ActivityMap und Ereignisgruppierung.

## Version 2.20.0 – Mittwoch, 21. Mai 2024

**Neue Funktionen**

- Unterstützung für [Streaming-Mediensammlung](../web-sdk/commands/configure/streamingmedia.md) hinzugefügt.

**Fehlerbehebungen und Verbesserungen**

- Es wurde ein Fehler behoben, durch den der Standardinhalt vom Codeausschnitt zur Vorab-Ausblendung ausgeblendet wurde, wenn die Zustimmung abgelehnt wurde.

## Version 2.19.2 – Donnerstag, 10. Januar 2024

**Fehlerbehebungen und Verbesserungen**

- Es wurde ein Problem behoben, durch das Identitätsfehler andere Fehler maskierten und Identitätsfehler in Warnungen geändert wurden.
- Es wurde ein Problem behoben, durch das Seitenaufrufe am Ende nicht gesendet wurden, wenn der Seitenaufruf am Anfang war und `renderDecisions` auf `false` festgelegt war.
- Es wurde ein Problem behoben, bei dem das Web SDK domänenübergreifende Identitäten nicht gelesen hat, wenn mehrere `adobe_mc` Abfragezeichenfolgenparameter vorhanden waren.

## Version 2.19.1 – Samstag, 10. November 2023

**Fehlerbehebungen und Verbesserungen**

- Es wurde ein Problem behoben, bei dem das von `sendEvent` -Aufrufen zurückgegebene Vorschlagsarray immer leer war.

## Version 2.19.0 – Donnerstag, 1. November 2023

**Neue Funktionen**

- Unterstützung für das Rendern von In-App-Nachrichten aus Adobe Journey Optimizer hinzugefügt.
- Zusätzliche Unterstützung für [oben und unten von Seitenereignissen](use-cases/top-bottom-page-events.md).
- Dem Befehl `sendEvent` wurde die Option [`defaultPersonalizationEnabled`](commands/sendevent/personalization.md) hinzugefügt, um die Anforderung des seitenweiten Umfangs und der Standardoberfläche zu steuern.

**Fehlerbehebungen und Verbesserungen**

- Die kombinierte Personalisierung zeigt Ereignisse beim Rendern mehrerer Personalisierungstypen zusammen.
- Es wurde ein Problem behoben, bei dem bei Namen von Einzelseiten-Apps zwischen Groß- und Kleinschreibung unterschieden wurde.
- Es wurde ein Problem mit Shadow DOM-personalisierten Angebots-Selektoren behoben.

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
- Unterstützung für den Befehl [`applyResponse`](/help/web-sdk/commands/applyresponse.md) hinzugefügt. Dies ermöglicht die hybride Personalisierung über die [Edge Network Server-API](../server-api/overview.md).
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
- Es wurde ein Problem behoben, bei dem ausgeblendete Container nicht angezeigt wurden, wenn ein Fehler vom Edge Network zurückgegeben wurde.
- Es wurde ein Problem behoben, bei dem die Interaktionsereignisse in Adobe Target nicht gezählt wurden. Dieses Problem wurde behoben, indem der Ansichtsname unter web.webPageDetails.viewName zu XDM hinzugefügt wurde.
- Es wurden fehlerhafte Dokumentationslinks in Konsolenmeldungen behoben.

## Version 2.8.0 – 19. Januar 2022

- Unterstützung für Schatten-DOM-Selektoren für die Personalisierung.
- Die Ereignistypen für die Personalisierung wurden umbenannt. (`display` und `click` werden zu `decisioning.propositionDisplay` und `decisioning.propositionInteract`)
- Es wurde ein Problem behoben, bei dem HTML-Angebote mit Inline-Skript-Tags die Skript-Tags zweimal zur Seite hinzugefügt haben, obwohl das Skript nur einmal ausgeführt wurde.

## Version 2.7.0 – 26. Oktober 2021

- Stellen Sie zusätzliche Informationen aus dem Edge Network im Rückgabewert von `sendEvent` bereit, einschließlich `inferences` und `destinations`. Das Format dieser Eigenschaften kann sich ändern, da diese Funktionen derzeit im Rahmen einer Beta bereitgestellt werden.

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

- Das SDK kann jetzt als [NPM-Paket](/help/web-sdk/install/npm.md) installiert werden.
- Es wurde Unterstützung für eine `out`-Option beim [Konfigurieren des Standardeinverständnisses](/help/web-sdk/commands/configure/defaultconsent.md) hinzugefügt, wodurch alle Ereignisse ignoriert werden, bis das Einverständnis eingeht (die vorhandene `pending`-Option stellt Ereignisse in die Warteschlange und sendet sie, sobald das Einverständnis eingeht).
- Der Rückruf [`onBeforeEventSend`](/help/web-sdk/commands/configure/onbeforeeventsend.md) kann jetzt verwendet werden, um das Senden eines Ereignisses zu verhindern.
- Jetzt wird eine XDM-Schemafeldgruppe anstelle von `meta.personalization` verwendet, wenn Ereignisse über gerenderte oder angeklickte personalisierte Inhalte gesendet werden.
- Der Befehl [`getIdentity`](/help/web-sdk/commands/getidentity.md) gibt jetzt die ID des Edge-Bereichs neben der Identität zurück.
- Die vom Server empfangenen Warnungen und Fehler wurden verbessert und werden nun auf besser geeignete Weise gehandhabt.
- Adobe Consent 2.0-Standard für den Befehl [`setConsent`](/help/web-sdk/commands/setconsent.md) wird nun unterstützt.
- Die Einverständisvoreinstellungen werden bei Erhalt gehasht und im lokalen Speicher gespeichert, um eine optimierte Integration zwischen CMPs, dem Platform Web SDK und dem Platform Edge Network zu ermöglichen. Wenn Sie Einverständnisvoreinstellungen erfassen, empfehlen wir Ihnen jetzt, `setConsent` bei jedem Laden der Seite aufzurufen.
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

- Fehlerbehebung: Das Opt-in-Objekt hinderte das Web SDK daran, Aufrufe durchzuführen, wenn `idMigrationEnabled` `true` ist.
- Fehlerbehebung: Sorgen Sie dafür, dass das Web SDK über Anforderungen informiert wird, die Personalisierungsangebote zurückgeben sollen, um ein flackerndes Problem zu vermeiden.

## Version 2.1.0 – August 2020

- Der Befehl `syncIdentity` wurde entfernt, und die Übergabe dieser IDs an den Befehl `sendEvent` wird unterstützt.
- Es wurde Unterstützung für den IAB 2.0-Einverständnisstandard hinzugefügt.
- Es wurde Unterstützung für die Übergabe zusätzlicher IDs im Befehl `setConsent` hinzugefügt.
- Es wurde Unterstützung zum Außerkraftsetzen von `datasetId` im Befehl `sendEvent` hinzugefügt.
- Support-Überwachungs-Hooks ([mehr dazu](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
- `environment: browser` wird nun in den Kontextdaten der Implementierungsdetails übergeben.
