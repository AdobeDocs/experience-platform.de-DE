---
title: Versionshinweise zur Adobe Experience Platform Web SDK-Erweiterung
description: Adobe Experience Platform Web SDK – Tag-Erweiterung
exl-id: 91de8c91-023a-45b6-9f67-ac75ee471e50
source-git-commit: ba75669eeaef9fc023e7c33265ec1e5dbada9534
workflow-type: tm+mt
source-wordcount: '1757'
ht-degree: 96%

---


# Versionshinweise zur Adobe Experience Platform Web SDK-Erweiterung

In diesem Dokument werden die Versionshinweise für die Adobe Experience Platform Web SDK-Tag-Erweiterung behandelt. Die neuesten Versionshinweise zum SDK finden Sie in den [Versionshinweisen zum Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html?lang=de).

## Version 2.20.3 - 8. August 2023

**Fehlerbehebungen und Verbesserungen**

* Es wurde ein Problem behoben, bei dem Datenelemente nicht im Feld ID-Synchronisierungs-Container-ID-Überschreibung gespeichert werden konnten.

## Version 2.20.1 - 3. August 2023

**Fehlerbehebungen und Verbesserungen**

* Die Validierung gespeicherter Einstellungen zur Außerkraftsetzung von Datensätzen wurde verbessert.

## Version 2.20.0 - 31. Juli 2023

**Neue Funktionen**

* Hinzugefügte Unterstützung für [Überschreibungen der Datastream-ID pro Befehl](../../../../datastreams/overrides.md).

**Fehlerbehebungen und Verbesserungen**

* Veraltet `edgeConfigId` zugunsten von `datastreamId` in der SDK-Konfiguration.
* Die Benutzeroberfläche wird durch mehrere Verbesserungen des Benutzererlebnisses für die Datastream-Konfiguration außer Kraft gesetzt.

## Version 2.19.0 – 21. Juni 2023

* Das Datenelement **[!UICONTROL Variable]** und die Aktionen **[!UICONTROL Variable aktualisieren]** sind jetzt allgemein verfügbar.

## Version 2.18.0 – 18. Mai 2023

* Enthält Version 2.17.0 des Adobe Experience Platform Web SDK.

## Version 2.17.0 – 25. April 2023

**Neue Funktionen**

* Enthält Version 2.16.0 des Adobe Experience Platform Web SDK.
* Es wurde Unterstützung für [Überschreibungen der Datenstromkonfiguration](../../../../datastreams/overrides.md) hinzugefügt.
* Der Option `datasetId` des Befehls `sendEvent` wurde ein Hinweis hinzugefügt, dass sie veraltet ist.


**Fehlerbehebungen und Verbesserungen**

* Es wurde ein Problem behoben, durch das beim Scrollen in Safari die Datenstromauswahl geschlossen wurde.

## Version 2.16.1 – 14. April 2023

* Es wurde ein Problem mit XDM-Objekt- und -Variablen-Datenelementen behoben, durch das die Auswahl eines Schemas aus einer nicht standardmäßigen Sandbox verhindert wurde.

## Version 2.16.0 – 30. März 2023

**Neue Funktionen**

* (Beta) Aktion **[!UICONTROL Variable aktualisieren]** und Datenelement **[!UICONTROL Variable]** hinzugefügt.
* Konfiguration hinzugefügt für Callback-Funktion [`onBeforeLinkClickSend`](../../../../edge/fundamentals/configuring-the-sdk.md#onBeforeLinkClickSend).

**Fehlerbehebungen und Verbesserungen**

* Es wurde ein Problem behoben, das dazu führte, dass das Klicken auf Elemente in einem Anker-Tag nicht funktionierte, wenn die Aktion **[!UICONTROL Umleiten mit Identität]** verwendet wurde.
* Es wurde ein Problem behoben, bei dem XDM-Objektdatenelemente nicht funktionierten, wenn nur ein Schema vorhanden war.
* Enthält Version 2.15.0 des Adobe Experience Platform Web SDK.


## Version 2.15.1 – 26. Januar 2023

* Es wurde ein Problem behoben, bei dem Benutzende ohne Zugriff auf Datenströme die Erweiterungskonfiguration nicht bearbeiten konnten.
* Es wurde Unterstützung für Oberflächen im Rahmen der Aktion `sendEvent` hinzugefügt.

Enthält Version 2.14.0 des Adobe Experience Platform Web SDK.


## Version 2.14.1 – 13. Oktober 2022

* Es wurde ein Problem behoben, bei dem die ID aus dem Experience Cloud-ID-Service vom Web SDK nicht berücksichtigt wird.

Enthält Version 2.13.1 der Adobe Experience Platform Web SDK-Bibliothek.

## Version 2.14.0 – 28. September 2022

* Es wurde eine neue `targetMigrationEnabled`-Konfiguration hinzugefügt, die eine vollständige seitenweise Migration ermöglicht.
* Es wurde eine Antwort-Aktion zum Anwenden hinzugefügt, um hybride Server-Client-Implementierungen zu ermöglichen.
* Es wurde eine Kontextoption für Benutzeragent-Client-Hinweise für hohe Entropie hinzugefügt.

Enthält Version 2.13.0 der Adobe Experience Platform Web SDK-Bibliothek.

## Version 2.13.0 – 29. Juni 2022

* Die Sortierreihenfolge numerischer Eigenschaften im XDM-Objekt-Datenelement wurde korrigiert, z. B. bei eVars.

Enthält Version 2.12.0 der Adobe Experience Platform Web SDK-Bibliothek.

## Version 2.12.0 – 13. Juni 2022

* Das Datenelement `identityMap` wurde so aktualisiert, dass die Namespace-Optionen basierend auf den in den Erweiterungseinstellungen definierten Sandboxes aufgefüllt werden.
* Die Aktion **[!UICONTROL Umleiten mit Identität]** wurde hinzugefügt, um eine Domain-übergreifende Identitätsfreigabe zu ermöglichen.
* Es wurden Dokumentations-Links zur Aktion `sendEvent` hinzugefügt.
* Die Bibliothek der React Spectrum-Benutzeroberfläche wurde aktualisiert.
* Es wurden verschiedene Verbesserungen an der Benutzeroberfläche vorgenommen.

Enthält Version 2.11.0 der Adobe Experience Platform Web SDK-Bibliothek.

## Version 2.11.2 – 3. Mai 2022

Enthält Version 2.10.1 der Adobe Experience Platform Web SDK-Bibliothek.

## Version 2.11.1 – 22. April 2022

* Ein fehlerhafter Konfigurationsbefehl aus Version 2.11.0 wurde korrigiert.

Enthält Version 2.10.0 der Adobe Experience Platform Web SDK-Bibliothek.

## Version 2.11.0 – 22. April 2022

* Die Leistung der Tags-Benutzeroberfläche wurde verbessert.
* Sandbox-Selektoren wurden zur Datenstrom-Erweiterungskonfiguration hinzugefügt.

Enthält Version 2.10.0 der Adobe Experience Platform Web SDK-Bibliothek.

## Version 2.10.0 – 10. März 2022

* Der Code-Ausschnitt zur Vorab-Ausblendung, der auf der Konfigurationsseite kopiert werden kann, wurde aktualisiert, um mit dem aktualisierten Adobe Target VEC-Editor verwendet werden zu können.

Enthält Version 2.9.0 der Adobe Experience Platform Web SDK-Bibliothek.

## Version 2.9.0 – 19. Januar 2022

Enthält Version 2.8.0 der Adobe Experience Platform Web SDK-Bibliothek.

## Version 2.8.0 – 26. Oktober 2021

Enthält Version 2.7.0 der Adobe Experience Platform Web SDK-Bibliothek.

* Weitere Informationen aus Experience Edge sind im Ereignis „Versandereignis abgeschlossen“ verfügbar, einschließlich `inferences` und `destinations`. Das Format dieser Eigenschaften kann sich ändern, da diese Funktionen derzeit als Teil einer Beta-Version eingeführt werden. Weitere Informationen finden Sie unter [Tracking von Ereignissen](../../../../edge/fundamentals/tracking-events.md).

## Version 2.7.3 – 7. September 2021

Enthält Version 2.6.4 der Adobe Experience Platform Web SDK-Bibliothek.

* Es wird nicht mehr vor der Einstellung von `container.buildInfo.environment.` gewarnt.

## Version 2.7.0 – 16. August 2021

Enthält Version 2.6.3 der Adobe Experience Platform Web SDK-Bibliothek.

* Bei Verwendung des Datenelementtyps „Identitätszuordnung“ werden Kennungen, deren IDs in Werte aufgelöst werden, bei denen es sich um nicht ausgefüllte Zeichenfolgen handelt, jetzt automatisch aus der Identitätszuordnung entfernt.
* Es wurde ein Fehler behoben, der bei dem Versuch auftrat, ein Datenelement mit dem Datenelementtyp „XDM-Objekt“ zu speichern, wenn kein Schema ausgewählt war.
* Die Typografie der Benutzeroberfläche wurde verbessert.

## Version 2.6.2 – 4. August 2021

Enthält Version 2.6.2 der Adobe Experience Platform Web SDK-Bibliothek.

## Version 2.6.1 – 29. Juli 2021

Enthält Version 2.6.1 der Adobe Experience Platform Web SDK-Bibliothek.

## Version 2.6.0 – 27. Juli 2021

Enthält Version 2.6.0 der Adobe Experience Platform Web SDK-Bibliothek.

* Kennzeichnungen, Beschreibungen und Fehlermeldungen mit dem Begriff „Edge-Konfiguration“ wurden gemäß der neuesten Adobe Experience Platform-Terminologie so geändert, dass stattdessen der Begriff „Datenstrom“ verwendet wird.
* In der Erweiterungskonfigurationsansicht wurde Unterstützung für die Verarbeitung einer großen Anzahl von Datenströmen und Datenstromumgebungen hinzugefügt.
* In der XDM-Objekt-Datenelementansicht wurde Unterstützung für die Verarbeitung einer großen Anzahl von Schemata hinzugefügt.
* Es wurde der Ereignistyp „Versandereignis abgeschlossen“ hinzugefügt, mit dem eine Regel ausgeführt werden kann, nachdem ein Ereignis an den Server gesendet und eine Antwort empfangen wurde. Zusätzliche Dokumentation wird in Kürze verfügbar sein.
* Der Ereignistyp „Entscheidungen erhalten“ wird nicht mehr unterstützt. Verwenden Sie stattdessen den Ereignistyp „Versandereignis abgeschlossen“.
* Die Benutzeroberfläche und die Fehlerbehandlung wurden allgemein verbessert.

## Version 2.5.0 – 1. Juni 2021

Enthält Version 2.5.0 der Adobe Experience Platform Web SDK-Bibliothek.

* Der Aktion „Ereignis senden“ wurde ein Feld `data` hinzugefügt. In der kommenden Dokumentation wird beschrieben, wie dies in bestimmten Szenarien verwendet werden kann.
* In der XDM-Objekt-Datenelementansicht wurde ein Problem behoben, bei dem ein Fehler ausgegeben wurde, wenn Benutzende Zugriff auf Adobe Experience Platform-Sandboxes hatten, aber nicht auf die als Standard für das Unternehmen konfigurierte Sandbox.
* In der XDM-Objekt-Datenelementansicht wurde ein Problem behoben, bei dem ein erforderliches Schemafeld als ungültig angesehen wurde, selbst wenn das übergeordnete Objekt keine Werte umfasste.

## Version 2.4.0 – 9. März 2021

Enthält Version 2.4.0 der Adobe Experience Platform Web SDK-Bibliothek.

* Ein Kontrollkästchen für [Dokument-Uploads](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=de#using-the-sendbeacon-api) wurde der Benutzeroberfläche für die Aktion „Ereignis senden“ hinzugefügt.
* Es wurde Unterstützung für eine `out`-Option beim [Konfigurieren des Standardeinverständnisses](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=de#default-consent) hinzugefügt, wodurch alle Ereignisse ignoriert werden, bis das Einverständnis eingeht (die vorhandene `pending`-Option stellt Ereignisse in die Warteschlange und sendet sie, sobald das Einverständnis eingeht).
* Dem Feld für das Standardeinverständnis wurde eine QuickInfo hinzugefügt.
* Es wurde Unterstützung für [Adobe Consent 2.0 Standard](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?lang=de#communicating-consent-preferences-via-the-adobe-standard) hinzugefügt.
* In der Benutzeroberfläche für das XDM-Objekt-Datenelement wird jetzt eine passendere Fehlermeldung angezeigt, wenn das Zugriffstoken der Benutzenden ungültig ist oder nicht ordnungsgemäß bereitgestellt wurde.
* Es wurde ein ursprungsübergreifender Fehler behoben (was sich nicht auf die Nutzung der Erweiterung auswirkt), der beim Anzeigen eines XDM-Objekt-Datenelements in der Developer Console für den Browser eingeblendet wurde.

## Version 2.3.0 – 4. November 2020

Enthält Version 2.3.0 der Adobe Experience Platform Web SDK-Bibliothek.

* Unterstützung für die Verwendung eines Datenelements beim Konfigurieren des Standardeinverständnisses hinzugefügt.
* Es wurde die Möglichkeit hinzugefügt, mit dem XDM-Objektdatenelementtyp nach XDM-Schemas zu suchen.
* Es wurde das Klonen von XDM-Daten im Aktionstyp „Ereignis senden“ hinzugefügt, um sicherzustellen, dass spätere Änderungen am XDM-Datenobjekt nicht in der Anfrage übernommen werden.

## Version 2.2.0 – 1. Oktober 2020

* Wenn Kundinnen oder Kunden versuchten, ein XDM-Objekt aus Sandbox-Schemata zu erstellen, traten Authentifizierungsprobleme auf. Die API, die Platform aufruft, ist jetzt über Umgebungen informiert, sodass Benutzenden nur die Schemata präsentiert werden, auf die sie zum Bearbeiten zugreifen können.
* Bei Verwendung des Datenelements `identityMap` werden die Namespaces jetzt vorab in einer Dropdown-Liste ausgefüllt, sodass Sie dies nicht manuell tun müssen.
* Die Benutzeroberfläche für das Datenelement `xdmObject` wurde überarbeitet. In der neuen Benutzeroberfläche können Sie sehen, welche Felder ausgefüllt wurden, ohne jedes Element im Objekt eingeben zu müssen.

## Version 2.1.1 – 26. August 2020

* Behebung eines Problems, bei dem Adobe Experience Platform-Sandboxen in der XDM-Objekt-Ansicht fehlerhaft angezeigt wurden. Wenn bei Verwendung dieser Erweiterungsversion die erwartete Sandbox nicht in der Liste angezeigt wird, sollte sich der Benutzer an den Adobe Experience Platform-Administrator wenden, um sicherzustellen, dass die Zugriffsberechtigungen korrekt festgelegt sind.

## Version 2.1.0 – 5. August 2020

* Grundlegende Änderung: Die Aktion `syncIdentity` wurde entfernt; die Übergabe dieser IDs erfolgt jetzt über die Aktion `sendEvent`. Deaktivieren Sie ggf. bestehende Regeln, die diese Aktion verwenden, bevor Sie ein Upgrade der Erweiterung vornehmen.
* Aktualisierung auf Alloy Version 2.1.0 ([Versionshinweise](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html?lang=de))
* Unterstützung für den IAB 2.0-Standard für Einwilligungen in der Aktion `setConsent`.
* Unterstützung für das Überschreiben der Datensatz-ID in der Aktion `sendEvent`.
* Neues Datenelement vom Typ `IdentityMap`. Über dieses kann der Eintrag `identityMap` im nun aktivierten XDM-Objektdatenelement sowie in der Aktion `setConsent` ausgefüllt werden.
* Unterstützung für das Übergeben einer Identitätszuordnung bzw. „identityMap“ in der Aktion `setConsent`.
* Es wurde Unterstützung für das Auswählen einer Platform-Sandbox im XDM-Objekt-Datenelement hinzugefügt.

## Version 1.0.0 – 26. Mai 2020

* Unterstützung für das Auswählen der Umgebung über den Konfigurations-Service.

## Version 0.1.2 – 4. Mai 2020

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
* Durch Aktivierung der Debugging-Funktion mit `_satellite` wird jetzt das Debugging im Adobe Experience Platform Web SDK aktiviert.
* Jetzt werden eingegebene Werte im XDM-Objekt unterstützt: Boolesche, Zahlen und Dezimalzahlen.

## Version 0.0.10 – 16. März 2020

* Die Konzepte von „Opt-in“ und „Opt-out“ wurden unter `Consent` vereint und ein neuer `setConsent`-Befehl wurde hinzugefügt.
* Ein neues Datenelement vom Typ `XDM Object` wurde hinzugefügt, das die Zuordnung von JavaScript/JSON zu XDM ermöglicht.

## Version 0.0.7 – 18. Februar 2020

* Die Optionen idSyncContainerId, datasetId, schemaId, urlDestinationsEnabled und cookieDestinationsEnabled wurden entfernt.
* Unterstützung für Bindestriche im Optionswert edgeDomain wurde hinzugefügt.
* Während der ID-Migration gestellte Anfragen werden an den demdex-Endpunkt gesendet, um die domänenübergreifende Identifizierung zu verbessern, wenn kein demdex-Cookie gesetzt wurde.
* Bei der ID-Migration gestellte Anfragen erwarten immer eine Antwort, um sicherzustellen, dass Identitäts-Cookies gesetzt werden.
* Beim Ausführen eines ungültigen Befehls wird eine Liste mit gültigen Befehlsnamen in der Konsole protokolliert.
* Es wurde ein Kontrollkästchen zum Umschalten der Unterstützung von Drittanbieter-Cookies zur Tag-Erweiterung hinzugefügt. Dadurch werden Aufrufe von demdex.net deaktiviert.

## Version 0.0.5 – 20. Dezember 2019

* Activity Tracker-Konfigurationen wurden zur Tag-Erweiterung hinzugefügt
* Anzeigen von EventType und EventMergeId beim Ereignisbefehl
* Es wurde eine onBeforeEventSend-Konfiguration zur Tag-Erweiterung hinzugefügt.
* Es wurde eine edgeBasePath-Konfiguration zur Tag-Erweiterung hinzugefügt.

## Version 0.0.3 – 25. November 2019

* Neue Felder „Merge-ID“ und „Typ“ bei der Aktion „Ereignis senden“. Die Merge-ID wird im XDM-Schema mit `xdm.eventMergeID` gemappt und der Typ wird im XDM-Schema mit `xdm.eventType` gemappt.

## Version 0.0.2 – 18. November 2019

* Erstmalige Veröffentlichung
