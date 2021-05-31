---
title: Versionshinweise zur Adobe Experience Platform Web SDK-Erweiterung
description: Adobe Experience Platform Web SDK-Erweiterung in Adobe Experience Platform Launch
seo-description: Adobe Experience Platform Web SDK-Erweiterung in Adobe Experience Platform Launch
exl-id: 91de8c91-023a-45b6-9f67-ac75ee471e50
source-git-commit: c3d66e50f647c2203fcdd5ad36ad86ed223733e3
workflow-type: tm+mt
source-wordcount: '1130'
ht-degree: 78%

---

# Versionshinweise zur Adobe Experience Platform Web SDK-Erweiterung

In diesem Dokument werden die Versionshinweise für die Adobe Experience Platform Web SDK-Erweiterung für Adobe Experience Platform Launch behandelt. Die neuesten Versionshinweise zum SDK finden Sie in den [Versionshinweisen zum Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html).

## 9. März 2020

### Adobe Experience Platform Web-SDK 2.4.0

Enthält Version 2.4.0 der Adobe Experience Platform Web SDK-Bibliothek.

* Das Kontrollkästchen [&quot;document unloading&quot;](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api) wurde zur Benutzeroberfläche der Aktion &quot;Ereignis senden&quot;hinzugefügt.
* Unterstützung für eine `out`-Option bei der [Konfiguration der standardmäßigen Einwilligung](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent) hinzugefügt, die alle Ereignisse bis zum Erhalt der Einwilligung verlässt (die vorhandene `pending`-Option versetzt Ereignisse in die Warteschlange und sendet sie, sobald die Einwilligung eingeht).
* Dem standardmäßigen Einwilligungsfeld wurde eine QuickInfo hinzugefügt.
* Unterstützung für [Adobe Consent 2.0 Standard](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard) hinzugefügt.
* In der Benutzeroberfläche des XDM-Datenelements-Datenelements wird jetzt ein besserer Fehler angezeigt, wenn das Zugriffstoken des Benutzers ungültig oder nicht ordnungsgemäß bereitgestellt ist.
* Fehlerkorrektur - Es wurde ein ursprungsübergreifender Fehler behoben, der beim Anzeigen eines XDM-Objekt-Datenelements in der Browser-Entwicklerkonsole angezeigt wurde (was sich nicht auf den Vorgang der Erweiterung auswirkt).

## 4. November 2020

### Adobe Experience Platform Web-SDK 2.3.0

Enthält Version 2.3.0 der Adobe Experience Platform Web SDK-Bibliothek.

#### Funktionen

* Unterstützung für die Verwendung eines Datenelements beim Konfigurieren des Standardeinverständnisses hinzugefügt.
* Es wurde die Möglichkeit hinzugefügt, mit dem XDM-Objektdatenelementtyp nach XDM-Schemas zu suchen.
* Es wurde das Klonen von XDM-Daten im Aktionstyp „Ereignis senden“ hinzugefügt, um sicherzustellen, dass spätere Änderungen am XDM-Datenobjekt nicht in der Anfrage übernommen werden.

## 1. Oktober 2020

### Adobe Experience Platform Web-SDK 2.2.0

#### Fehlerkorrekturen

* Als Kunden versuchten, ein XDM-Objekt aus Sandbox-Schemas zu erstellen, traten Authentifizierungsprobleme auf. Die API, die Platform aufruft, ist jetzt über Umgebungen informiert, sodass Benutzern nur die Schemas angezeigt werden, auf die sie Zugriff haben, um sie zu bearbeiten.

#### Funktionen

* Bei Verwendung des Datenelements `identityMap` werden die Namespaces jetzt vorab in einer Dropdown-Liste ausgefüllt, sodass Sie dies nicht manuell tun müssen.
* Die Benutzeroberfläche für das Datenelement `xdmObject` wurde überarbeitet. In der neuen Benutzeroberfläche können Sie sehen, welche Felder ausgefüllt wurden, ohne jedes Element im Objekt eingeben zu müssen.


## 26. August 2020

### Adobe Experience Platform Web-SDK 2.1.1

#### Funktionen

* Behebung eines Problems, bei dem Adobe Experience Platform-Sandboxen in der XDM-Objekt-Ansicht fehlerhaft angezeigt wurden. Wenn bei Verwendung dieser Erweiterungsversion die erwartete Sandbox nicht in der Liste angezeigt wird, sollte sich der Benutzer an den Adobe Experience Platform-Administrator wenden, um sicherzustellen, dass die Zugriffsberechtigungen korrekt festgelegt sind.


## 5. August 2020

### Adobe Experience Platform Web-SDK 2.1.0

#### Funktionen

* Grundlegende Änderung: Die Aktion `syncIdentity` wurde entfernt; die Übergabe dieser IDs erfolgt jetzt über die Aktion `sendEvent`. Deaktivieren Sie ggf. bestehende Regeln, die diese Aktion verwenden, bevor Sie ein Upgrade der Erweiterung vornehmen.
* Aktualisierung auf Alloy Version 2.1.0 ([Versionshinweise](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html))
* Unterstützung für den IAB 2.0-Standard für Einwilligungen in der Aktion `setConsent`.
* Unterstützung für das Überschreiben der Datensatz-ID in der Aktion `sendEvent`.
* Neues Datenelement vom Typ `IdentityMap`. Über dieses kann der Eintrag `identityMap` im nun aktivierten XDM-Objektdatenelement sowie in der Aktion `setConsent` ausgefüllt werden.
* Unterstützung für das Übergeben einer Identitätszuordnung bzw. „identityMap“ in der Aktion `setConsent`.
* Unterstützung für die Auswahl einer Platform-Sandbox im XDM-Objektdatenelement.


## 26. Mai 2020

### Adobe Experience Platform Web-SDK 1.0.0

#### Funktionen

* Unterstützung für das Auswählen der Umgebung über den Konfigurations-Service.


## 4. Mai 2020

### Adobe Experience Platform Web-SDK 0.1.2

#### Funktionen

* `configId` wurde in `edgeConfigId` umbenannt.
* `viewStart` wurde in `renderDecisions` umbenannt und standardmäßig auf „false“ eingestellt. Bei der Einstellung „true“ werden Personalisierungsangebote abgerufen und automatisch gerendert.
* Änderungen im Zusammenhang mit `Get Decisions`:
   * Der Befehl `getDecisions` wurde entfernt.
   * Dem `sendEvent`-Befehl wurde die Option `scopes` hinzugefügt. Entscheidungen werden in der aufgelösten Zusage `sendEvent` zurückgegeben.
   * Es wurde ein integrierter `__view__`-Bereich hinzugefügt, der dafür sorgt, dass ganzseitige Angebote zurückgegeben werden. (z. B. VEC-Angebote in Target).
Diese Entscheidungen werden nur dann vom `sendEvent`-Befehl zurückgegeben, wenn `renderDecisions` mit „false“ festgelegt ist.
   * Es wurde ein `Decisions Received`-Ereignis hinzugefügt, das ausgelöst wird, wenn Entscheidungen verfügbar werden.
* Mehrere Personalisierungsbenachrichtigungen wurden unter einem einzigen Server-Aufruf kombiniert.
* Es wurde ein Problem mit der Ereignis-Merge-ID behoben, das jedes Mal zurückgesetzt wurde, wenn das Datenelement referenziert wurde.
* Die Aktion `setCustomerIds` wurde in `syncIdentity` umbenannt.
* Es wurde ein `getIdentity`-Befehl hinzugefügt. Dieser kann derzeit nur über benutzerdefinierten Code genutzt werden.
* Durch die Aktivierung von Debugging mit `_satellite` wird jetzt das Debugging im Adobe Experience Platform Web SDK aktiviert.
* Jetzt werden eingegebene Werte im XDM-Objekt unterstützt: Boolesche, Zahlen und Dezimalzahlen.

## 16. März 2020

### Adobe Experience Platform Web-SDK 0.0.10

#### Funktionen

* Die Konzepte von „Opt-in“ und „Opt-out“ wurden unter `Consent` vereint und ein neuer `setConsent`-Befehl wurde hinzugefügt.
* Ein neues Datenelement vom Typ `XDM Object` wurde hinzugefügt, das die Zuordnung von JavaScript/JSON zu XDM ermöglicht.

## 18. Februar 2020

### Adobe Experience Platform Web-SDK 0.0.7

#### Funktionen

* Die Optionen idSyncContainerId, datasetId, schemaId, urlDestinationsEnabled und cookieDestinationsEnabled wurden entfernt.
* Unterstützung für Bindestriche im Optionswert edgeDomain wurde hinzugefügt.
* Während der ID-Migration gestellte Anfragen werden an den demdex-Endpunkt gesendet, um die domänenübergreifende Identifizierung zu verbessern, wenn kein demdex-Cookie gesetzt wurde.
* Bei der ID-Migration gestellte Anfragen erwarten immer eine Antwort, um sicherzustellen, dass Identitäts-Cookies gesetzt werden.
* Beim Ausführen eines ungültigen Befehls wird eine Liste mit gültigen Befehlsnamen in der Konsole protokolliert.
* Es wurde ein Kontrollkästchen zum Umschalten zwischen Drittanbieter-Cookie-Unterstützung und der Adobe Experience Platform Launch-Erweiterung hinzugefügt. Dadurch werden Aufrufe von demdex.net deaktiviert.

## 20. Dezember 2019

### Adobe Experience Platform Web-SDK 0.0.5

#### Funktionen

* Hinzufügen von Activity Tracker-Konfigurationen zur Platform Launch-Erweiterung
* Anzeigen von EventType und EventMergeId beim Ereignisbefehl
* Hinzufügen von onBeforeEventSend-Konfiguration zur Platform Launch-Erweiterung
* Hinzufügen von edgeBasePath-Konfiguration zur Platform Launch-Erweiterung

#### Aktualisierung auf Alloy Version 0.0.10, die die folgenden Änderungen enthält:

* Implementierung des Client-Speichers: Status- und Cookie-Logik auf den Server verschoben
* Anzeigen von EventType und EventMergeId beim Ereignisbefehl
* Verwenden von sendBeacon für Linktracking außer Exitlinks
* Erneute Einführung von ID-Synchronisierungen ohne Überprüfung des Ablaufs der Gültigkeit
* setCustomerIds-Befehl ohne Hashing-IDs auf Nicht-SSL-Seiten (http)
* Übergeben der APEX-Domäne an den Server, der beim Festlegen von Status/Cookies verwendet werden soll
* Abruf der ECID aus der Antwort mit einem neuen Handle-Typ
* Entfernen von Standardeinstellungen für Aktivierungs- und Identitätskonfigurationen
* Umbenennen und Verschieben von Abfrageoptionen in Meta
* Migration veralteter ECID

#### Fehlerkorrekturen

* Bei unerwartetem Status-Code wird der Antworttext für die Fehlermeldung geparst und formatiert
* Wird der Debugging-Befehl ausgeführt oder alloy_debug verwendet, wird er durch die Konfiguration überschrieben.

## 25. November 2019

### Adobe Experience Platform Web-SDK 0.0.3

#### Funktionen

* Neue Felder „Merge-ID“ und „Typ“ bei der Aktion „Ereignis senden“. Die Merge-ID wird im XDM-Schema mit `xdm.eventMergeID` gemappt und der Typ wird im XDM-Schema mit `xdm.eventType` gemappt.
* Verbesserte Fehlerbehebung und -berichterstellung
* Verwendung von `sendBeacon` für alle Links

#### Fehlerkorrekturen

* Es wurde ein Problem behoben, durch das das Debugging eines Abfragezeichenfolge-Parameters oder des Befehls `debug` nicht in der gesamten Sitzung beibehalten wurde.

## 18. November 2019

### Adobe Experience Platform Web-SDK 0.0.2

#### Funktionen

* Integration der Erweiterung
* ECID-Unterstützung ohne zusätzliche Bibliotheks- oder Netzwerkaufrufe
* Opt-in-Unterstützung
* Unterstützung beim Senden von XDM an Platform
* Unterstützung der Erstanbieterdomäne
* Automatische Erfassung des Browserkontexts
* Vollständig Open Source ([Erweiterung](https://github.com/adobe/reactor-extension-alloy), [SDK](https://github.com/adobe/reactor-extension-alloy))
* Detaillierte Protokollierung
* Möglichkeit, Fehler in der Produktion auszublenden.
