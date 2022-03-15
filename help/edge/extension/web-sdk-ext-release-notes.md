---
title: Versionshinweise zur Adobe Experience Platform Web SDK-Erweiterung
description: Adobe Experience Platform Web SDK-Tag-Erweiterung
exl-id: 91de8c91-023a-45b6-9f67-ac75ee471e50
source-git-commit: bb06dd63de1a36d3e3d065a986f3d34f63783895
workflow-type: tm+mt
source-wordcount: '1290'
ht-degree: 48%

---

# Versionshinweise zur Adobe Experience Platform Web SDK-Erweiterung

In diesem Dokument werden die Versionshinweise für die Adobe Experience Platform Web SDK-Tag-Erweiterung behandelt. Die neuesten Versionshinweise zum SDK finden Sie in der [Versionshinweise zum Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html).

## Version 2.10.0 - 10. März 2022

* Aktualisieren Sie den Codeausschnitt zur Vorab-Ausblendung, der auf der Konfigurationsseite kopiert werden kann, um mit dem aktualisierten Adobe Target VEC-Editor zu funktionieren.

Enthält Version 2.9.0 der Adobe Experience Platform Web SDK-Bibliothek.

## Version 2.9.0 - 19. Januar 2022

Enthält Version 2.8.0 der Adobe Experience Platform Web SDK-Bibliothek.

## Version 2.8.0 - 26. Oktober 2021

Enthält Version 2.7.0 der Adobe Experience Platform Web SDK-Bibliothek.

* Weitere Informationen aus Experience Edge sind im Ereignis &quot;Ereignis abschließen senden&quot;verfügbar, einschließlich `inferences` und `destinations`. Das Format dieser Eigenschaften kann sich ändern, da diese Funktionen derzeit als Teil einer Beta-Version eingeführt werden. Weitere Informationen finden Sie unter [Tracking von Ereignissen.](../fundamentals/tracking-events.md)

## Version 2.7.3 - 7. September 2021

Enthält Version 2.6.4 der Adobe Experience Platform Web SDK-Bibliothek.

* Es gibt keine Warnung mehr zur Einstellung der Verwendung von `container.buildInfo.environment.`

## Version 2.7.0 - 16. August 2021

Enthält Version 2.6.3 der Adobe Experience Platform Web SDK-Bibliothek.

* Bei Verwendung des Datenelementtyps Identity Map werden IDs, deren IDs in Werte aufgelöst werden, die nicht ausgefüllte Zeichenfolgen sind, jetzt automatisch aus der Identitätszuordnung entfernt.
* Fehlerkorrektur - beim Versuch, ein Datenelement mit dem Datenelementtyp &quot;XDM-Objekt&quot;zu speichern, tritt kein Fehler mehr auf und es wurde kein Schema ausgewählt.
* Verbesserte Typografie der Benutzeroberfläche.

## Version 2.6.2 - 4. August 2021

Enthält Version 2.6.2 der Adobe Experience Platform Web SDK-Bibliothek.

## Version 2.6.1 - 29. Juli 2021

Enthält Version 2.6.1 der Adobe Experience Platform Web SDK-Bibliothek.

## Version 2.6.0 - 27. Juli 2021

Enthält Version 2.6.0 der Adobe Experience Platform Web SDK-Bibliothek.

* Beschriftungen, Beschreibungen und Fehlermeldungen, die den Begriff &quot;Edge-Konfiguration&quot;verwenden, wurden geändert, um den Begriff &quot;Datastream&quot;zur Anpassung an die neueste Adobe Experience Platform-Terminologie zu verwenden.
* In der Erweiterungskonfigurationsansicht wurde Unterstützung für die Verarbeitung einer großen Anzahl von Datastreams und Datastream-Umgebungen hinzugefügt.
* In der XDM Object -Datenelementansicht wurde Unterstützung für die Verarbeitung einer großen Anzahl von Schemas hinzugefügt.
* Es wurde der Ereignistyp &quot;Ereignis abschließen senden&quot;hinzugefügt, mit dem eine Regel ausgeführt werden kann, nachdem ein Ereignis an den Server gesendet und eine Antwort empfangen wurde. Weitere Dokumentationen werden in Kürze verfügbar sein.
* Der Ereignistyp Entscheidungen erhalten wird nicht mehr unterstützt. Verwenden Sie stattdessen den Ereignistyp &quot;Ereignis abschließen senden&quot;.
* Die Benutzeroberfläche und die Fehlerbehandlung wurden im Allgemeinen verbessert.

## Version 2.5.0 - 1. Juni 2021

Enthält Version 2.5.0 der Adobe Experience Platform Web SDK-Bibliothek.

* Eine `data` an die Aktion Ereignis senden . In der kommenden Dokumentation wird beschrieben, wie dies in bestimmten Szenarien verwendet werden kann.
* In der Datenelementansicht &quot;XDM-Objekt&quot;wurde ein Problem behoben, bei dem ein Fehler ausgegeben wurde, wenn der Benutzer Zugriff auf Adobe Experience Platform-Sandboxes hatte, aber nicht auf die Sandbox, die als Standard für das Unternehmen konfiguriert wurde.
* In der Ansicht &quot;XDM Object data element&quot;wurde ein Problem behoben, bei dem ein erforderliches Schemafeld als ungültig angesehen wurde, selbst wenn das übergeordnete Objekt keine Werte enthielt.

## Version 2.4.0 - 9. März 2021

Enthält Version 2.4.0 der Adobe Experience Platform Web SDK-Bibliothek.

* Hinzugefügt [&quot;document unloading&quot;](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api) aktivieren, um die Benutzeroberfläche für die Aktion &quot;Ereignis senden&quot;zu aktivieren.
* Hinzugefügte Unterstützung für eine `out` Option bei [Konfigurieren der Standardzustimmung](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent) , wodurch alle Ereignisse gelöscht werden, bis die Zustimmung eingeht (die vorhandene `pending` -Option Ereignisse in die Warteschlange stellt und sie sendet, sobald die Zustimmung eingeht).
* Dem standardmäßigen Einwilligungsfeld wurde eine QuickInfo hinzugefügt.
* Hinzugefügte Unterstützung für [Adobe Consent 2.0 standard](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard).
* In der Benutzeroberfläche des XDM-Datenelements-Datenelements wird jetzt ein besserer Fehler angezeigt, wenn das Zugriffstoken des Benutzers ungültig oder nicht ordnungsgemäß bereitgestellt ist.
* Fehlerkorrektur - Es wurde ein ursprungsübergreifender Fehler behoben, der beim Anzeigen eines XDM-Objekt-Datenelements in der Browser-Entwicklerkonsole angezeigt wurde (was sich nicht auf den Vorgang der Erweiterung auswirkt).

## Version 2.3.0 - 4. November 2020

Enthält Version 2.3.0 der Adobe Experience Platform Web SDK-Bibliothek.

* Unterstützung für die Verwendung eines Datenelements beim Konfigurieren des Standardeinverständnisses hinzugefügt.
* Es wurde die Möglichkeit hinzugefügt, mit dem XDM-Objektdatenelementtyp nach XDM-Schemas zu suchen.
* Es wurde das Klonen von XDM-Daten im Aktionstyp „Ereignis senden“ hinzugefügt, um sicherzustellen, dass spätere Änderungen am XDM-Datenobjekt nicht in der Anfrage übernommen werden.

## Version 2.2.0 - 1. Oktober 2020

* Als Kunden versuchten, ein XDM-Objekt aus Sandbox-Schemas zu erstellen, traten Authentifizierungsprobleme auf. Die API, die Platform aufruft, ist jetzt über Umgebungen informiert, sodass Benutzern nur die Schemas angezeigt werden, auf die sie Zugriff haben, um sie zu bearbeiten.
* Bei Verwendung von `identityMap` -Datenelement verwenden, werden die Namespaces jetzt vorab in einer Dropdown-Liste ausgefüllt, sodass Sie dies nicht manuell eingeben müssen.
* Die Benutzeroberfläche für das Datenelement `xdmObject` wurde überarbeitet. In der neuen Benutzeroberfläche können Sie sehen, welche Felder ausgefüllt wurden, ohne jedes Element im Objekt eingeben zu müssen.

## Version 2.1.1 - 26. August 2020

* Behebung eines Problems, bei dem Adobe Experience Platform-Sandboxen in der XDM-Objekt-Ansicht fehlerhaft angezeigt wurden. Wenn bei Verwendung dieser Erweiterungsversion die erwartete Sandbox nicht in der Liste angezeigt wird, sollte sich der Benutzer an den Adobe Experience Platform-Administrator wenden, um sicherzustellen, dass die Zugriffsberechtigungen korrekt festgelegt sind.

## Version 2.1.0 - 5. August 2020

* Grundlegende Änderung: Die Aktion `syncIdentity` wurde entfernt; die Übergabe dieser IDs erfolgt jetzt über die Aktion `sendEvent`. Deaktivieren Sie ggf. bestehende Regeln, die diese Aktion verwenden, bevor Sie ein Upgrade der Erweiterung vornehmen.
* Aktualisierung auf Alloy Version 2.1.0 ([Versionshinweise](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html))
* Unterstützung für den IAB 2.0-Standard für Einwilligungen in der Aktion `setConsent`.
* Unterstützung für das Überschreiben der Datensatz-ID in der Aktion `sendEvent`.
* Neues Datenelement vom Typ `IdentityMap`. Über dieses kann der Eintrag `identityMap` im nun aktivierten XDM-Objektdatenelement sowie in der Aktion `setConsent` ausgefüllt werden.
* Unterstützung für das Übergeben einer Identitätszuordnung bzw. „identityMap“ in der Aktion `setConsent`.
* Unterstützung für die Auswahl einer Platform-Sandbox im XDM-Objektdatenelement.

## Version 1.0.0 - 26. Mai 2020

* Unterstützung für das Auswählen der Umgebung über den Konfigurations-Service.

## Version 0.1.2 - 4. Mai 2020

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
* Aktivieren von Debugging mithilfe von `_satellite` aktiviert jetzt das Debugging im Adobe Experience Platform Web SDK.
* Jetzt werden eingegebene Werte im XDM-Objekt unterstützt: Boolesche, Zahlen und Dezimalzahlen.

## Version 0.0.10 - 16. März 2020

* Die Konzepte von „Opt-in“ und „Opt-out“ wurden unter `Consent` vereint und ein neuer `setConsent`-Befehl wurde hinzugefügt.
* Ein neues Datenelement vom Typ `XDM Object` wurde hinzugefügt, das die Zuordnung von JavaScript/JSON zu XDM ermöglicht.

## Version 0.0.7 - 18. Februar 2020

* Die Optionen idSyncContainerId, datasetId, schemaId, urlDestinationsEnabled und cookieDestinationsEnabled wurden entfernt.
* Unterstützung für Bindestriche im Optionswert edgeDomain wurde hinzugefügt.
* Während der ID-Migration gestellte Anfragen werden an den demdex-Endpunkt gesendet, um die domänenübergreifende Identifizierung zu verbessern, wenn kein demdex-Cookie gesetzt wurde.
* Bei der ID-Migration gestellte Anfragen erwarten immer eine Antwort, um sicherzustellen, dass Identitäts-Cookies gesetzt werden.
* Beim Ausführen eines ungültigen Befehls wird eine Liste mit gültigen Befehlsnamen in der Konsole protokolliert.
* Es wurde ein Kontrollkästchen zum Umschalten zwischen Drittanbieter-Cookie-Unterstützung und der Tag-Erweiterung hinzugefügt. Dadurch werden Aufrufe von demdex.net deaktiviert.

## Version 0.0.5 - 20. Dezember 2019

* Hinzufügen von Activity Tracker-Konfigurationen zur Tag-Erweiterung
* Anzeigen von EventType und EventMergeId beim Ereignisbefehl
* Hinzufügen von onBeforeEventSend-Konfiguration zur Tag-Erweiterung
* Hinzufügen von edgeBasePath config zur Tag-Erweiterung

## Version 0.0.3 - 25. November 2019

* Neue Felder „Merge-ID“ und „Typ“ bei der Aktion „Ereignis senden“. Die Merge-ID wird im XDM-Schema mit `xdm.eventMergeID` gemappt und der Typ wird im XDM-Schema mit `xdm.eventType` gemappt.

## Version 0.0.2 - 18. November 2019

* Erstes Release
