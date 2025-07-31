---
title: Versionshinweise zur Adobe Experience Platform Web SDK-Erweiterung
description: Adobe Experience Platform Web SDK – Tag-Erweiterung
exl-id: 91de8c91-023a-45b6-9f67-ac75ee471e50
source-git-commit: 54c609ec995ac8e48c1c6441390b205bfb5a01cc
workflow-type: tm+mt
source-wordcount: '2825'
ht-degree: 63%

---


# Versionshinweise zur Web SDK-Erweiterung

In diesem Dokument werden die Versionshinweise für die Adobe Experience Platform Web SDK-Tag-Erweiterung behandelt. Die neuesten Versionshinweise zu SDK finden Sie in den [Versionshinweisen zu Experience Platform Web SDK](/help/web-sdk/release-notes.md).

## Version 2.31.1 – Freitag, 31. Juli 2025

- Es wurde ein Problem behoben, das die Ausführung benutzerdefinierter Builds verhinderte.
- Enthält [Version 2.28.1](../../../../web-sdk/release-notes.md#2-28-1) des Adobe Experience Platform Web SDK.

## Version 2.31.0 – Freitag, 24. Juli 2025

**Neue Funktionen**

- Enthält [Version 2.28.0](../../../../web-sdk/release-notes.md#2-28-0) des Adobe Experience Platform Web SDK.

**Fehlerbehebungen und Verbesserungen**

- Es wurde ein Problem behoben, bei dem ein Fehler ausgegeben wird, wenn eine Datenstrom-Überschreibung über ein Datenelement aktiviert wird.
- Es wurde ein Problem behoben, bei dem leere `idSyncContainerId`-Überschreibungen einen Fehler auslösten.
- Beim Auflösen von Mediendatenelementen ist jetzt das Ereignisobjekt eingeschlossen.

**Bekannte Probleme**

- Nach der Veröffentlichung der Version 2.31.0 wurde ein Problem mit dem Build-Prozess [Benutzerdefinierte Komponenten](/help/web-sdk/install/create-custom-build.md) festgestellt. Während benutzerdefinierte Builds weiterhin funktionieren, sind alle Komponenten derzeit im Build enthalten, was unabhängig von der Komponentenauswahl zu einem Paket in voller Größe führt. Eine Lösung für dieses Problem wird derzeit entwickelt. Wenn Sie sich zur Minimierung der Build-Größe auf die Auswahl benutzerdefinierter Komponenten verlassen, wird empfohlen, auf eine zukünftige Version zu warten.


## Version 2.30.1 – Mittwoch, 27. Mai 2025

**Fehlerbehebungen und Verbesserungen**

- Es wurde ein Problem behoben, bei dem die Ansicht Variable aktualisieren abstürzte, wenn für eine Organisation keine Standard-Sandbox festgelegt war.

## Version 2.30.0 – Donnerstag, 21. Mai 2025

**Neue Funktionen**

- Sie können jetzt ein Datenelement angeben, wenn Sie Drittanbieter-Cookies aktivieren.
- Es wurden Clear-Schaltflächen zu Code-Feldern hinzugefügt.
- Enthält [Version 2.27.0](../../../../web-sdk/release-notes.md#2-27-0) des Adobe Experience Platform Web SDK.

**Fehlerbehebungen und Verbesserungen**

- Es wurde eine Validierung hinzugefügt, um zu verhindern, dass die Einstellung `onBeforeLinkClickSend` wird, wenn die Ereignisgruppierung aktiviert ist.

## Version 2.29.1 – Freitag, 8. Mai 2025

**Fehlerbehebungen und Verbesserungen**

- Es wurde ein Problem behoben, bei dem Einstellungen nicht gespeichert wurden, wenn nach der Bearbeitung sofort auf „Speichern“ geklickt wurde.

## Version 2.29.0 – Donnerstag, 5. März 2025

**Neue Funktionen**

- Sie können jetzt benutzerdefinierte Web-SDK-Builds erstellen und die benötigten Komponenten über die Benutzeroberfläche der Tag-Erweiterung auswählen. Dies kann zu kleineren Builds führen, indem nicht verwendete Komponenten ausgeschlossen werden. Weitere Informationen finden Sie in der Dokumentation [Erstellen eines benutzerdefinierten Web-SDK-Builds](web-sdk-extension-configuration.md#custom-build).
- Enthält [Version 2.26.0](../../../../web-sdk/release-notes.md#2-26-0) des Adobe Experience Platform Web SDK.

**Fehlerbehebungen und Verbesserungen**

- Eine elegante Handhabung fehlender Datenelemente in Aktionen vom Typ [Variable aktualisieren](action-types.md#update-variable) wurde hinzugefügt. Zuvor wurde beim Bearbeiten einer Aktion „Variable aktualisieren“ mit einem fehlenden Datenelement eine Fehlermeldung angezeigt. Jetzt können Sie ein anderes Datenelement auswählen und alle Einstellungen für die Aktion „Variable aktualisieren“ werden weiterhin angewendet. Datenelemente können fehlen, wenn sie gelöscht oder eine Tags-Eigenschaft dupliziert wird.
- Das Öffnen einer neuen Registerkarte mit der Aktion [Umleiten mit Identität](action-types.md#redirect-with-identity) wird nun unterstützt. Bei Verwendung der Aktion wird jetzt das `target` des Anker-Tags verwendet, wenn der Browser umgeleitet wird.
- Es wurde ein Problem behoben, bei dem Adobe Audience Manager in Konfigurationsüberschreibungen nicht deaktiviert werden konnte.

## Version 2.28.0 – Freitag, 23. Januar 2025

**Fehlerbehebungen und Verbesserungen**

- Es wurde ein Problem behoben, bei dem Überschreibungen des ID-Synchronisierungs-Containers nicht festgelegt werden konnten, ohne Audience Manager zu aktivieren.
- Es wurde ein Problem behoben, bei dem Überschreibungen der Datenstromkonfiguration beim Upgrade auf die neueste Version deaktiviert wurden.
- Es wurde ein Problem behoben, bei dem Benutzer die Einstellungen für die automatische Klicksammlung von Target nicht speichern konnten.

**Neue Funktionen**

- Es wurde eine neue Funktion hinzugefügt, mit der Sie zwischen technischen Namen und Anzeigenamen im XDM-Objekt wechseln können.
- Enthält [Version 2.25.0](../../../../web-sdk/release-notes.md#2-25-0) des Adobe Experience Platform Web SDK.

## Version 2.27.0 – Freitag, 31. Oktober 2024

**Neue Funktionen**

- [Datenstromüberschreibungen](../web-sdk/web-sdk-extension-configuration.md#datastream-overrides) enthalten jetzt Einstellungen zum Deaktivieren von Experience Cloud-Lösungen und Adobe Experience Platform-Services.
- Sie können jetzt [Datenstrom-Überschreibungen](../web-sdk/web-sdk-extension-configuration.md) für Mediensitzungen erstellen.

Enthält Version 2.24.0 des Adobe Experience Platform Web SDK.

## Version 2.26.1 – Freitag, 19. September 2024

**Fehlerbehebungen und Verbesserungen**

- Es wurde ein Problem behoben, bei dem Cookies bei der lokalen Ausführung der Web-SDK nicht korrekt geschrieben wurden.

Enthält Version 2.23.0 des Adobe Experience Platform Web SDK.

## Version 2.26.0 – Freitag, 22. August 2024

**Neue Funktionen**

- Überwachungs-Hook `triggered` Ereignis hinzugefügt.
- [Geführte Ereignisse](action-types.md#instance), [Standardpersonalisierung anfordern](action-types.md#personalization), [Regelsatzelemente abonnieren](event-types.md#subscribe-ruleset-items) und [Regelsätze auswerten](action-types.md#evaluate-rulesets) sind jetzt allgemein verfügbar.

**Fehlerbehebungen und Verbesserungen**

- Es wurde ein Problem behoben, bei dem duplizierte Variablendatenelemente einander überschreiben konnten.
- Bei Verwendung des [Standardpersonalisierung anfordern](action-types.md#personalization) geführten Ereignisses sind visuelle Personalisierungsentscheidungen jetzt automatisch aktiviert.

Enthält Version 2.22.0 des Adobe Experience Platform Web SDK.

## Version 2.25.0 – Freitag, 18. Juli 2024

**Neue Funktionen**

- Unterstützung für das automatische Tracking der Personalisierung in Adobe Journey Optimizer wurde hinzugefügt.
- Es wurden neue Einstellungen zur Verwaltung der verbesserten Klick-Sammlung eingeführt.

Enthält Version 2.21.1 des Adobe Experience Platform Web SDK.

## Version 2.24.0 – Donnerstag, 5. Juni 2024

**Fehlerbehebungen und Verbesserungen**

- Fehlerkorrektur - Beim Ändern der Erweiterungskonfiguration tritt jetzt kein Fehler mehr auf, wenn Konfigurationsüberschreibungen definiert sind.
- Zulassen, dass leere Werte für Ping-Intervalle der Mediensammlung festgelegt werden.
- Fehlerkorrektur - Beim Ändern einer Aktion vom Typ Variable aktualisieren tritt jetzt kein Fehler mehr auf.
- Zurücksetzen des ID-Synchronisierungs-Containers in Überschreibungen der Konfiguration zulassen.

Enthält Version 2.20.0 des Adobe Experience Platform Web SDK.

## Version 2.23.1 – Mittwoch, 28. Mai 2024

**Neue Funktionen**

- Es wurde Unterstützung für die [`Streaming Media Collection`](web-sdk-extension-configuration.md#streaming-media) in der Erweiterungskonfiguration hinzugefügt.
- Die [`Send Media Event`](action-types.md#send-media-event) Aktion für die [!DNL Streaming Media Collection] wurde hinzugefügt.
- Das [`Media: Quality of Experience`](data-element-types.md#quality-experience) Datenelement für die [!DNL Streaming Media Collection] wurde hinzugefügt.

Enthält Version 2.20.0 des Adobe Experience Platform Web SDK.

**Fehlerbehebungen und Verbesserungen**

- Fehlerkorrektur - Bei der Suche nach Datenelementen in der Aktion [Variable aktualisieren](action-types.md#update-variable) tritt jetzt kein Fehler mehr auf.
- Ereignistypen [!UICONTROL Media] aus den Ereignistypen entfernt, die zur Verwendung in der `sendEvent`-Aktion vorgeschlagen wurden.

## Version 2.22.0 – Samstag, 3. Mai 2024

**Neue Funktionen**

- Erweitern eines variablen Datenelements zur Unterstützung von Datenobjekten.
- Die Aktion „Variable aktualisieren“ unterstützt jetzt das Ändern von Passthrough-Adobe Analytics-, Adobe Audience Manager- und Adobe Target-Daten.

Enthält Version 2.19.2 des Adobe Experience Platform Web SDK.

## Version 2.21.4 – Donnerstag, 10. Januar 2024

**Fehlerbehebungen und Verbesserungen**

- Es wurde ein Problem behoben, bei dem das Speichern von Konfigurations-Überschreibungen ohne alle 3 Umgebungen die Erweiterungs-Benutzeroberfläche abstürzen ließ.
- Es wurde ein Problem behoben, bei dem das Kontrollkästchen Vorhandenen Wert löschen beim Bearbeiten einer Aktion vom Typ Variable aktualisieren nicht angezeigt wurde.

Enthält Version 2.19.2 des Adobe Experience Platform Web SDK.

## Version 2.21.3 – Samstag, 10. November 2023

Enthält Version 2.19.1 des Adobe Experience Platform Web SDK.

**Fehlerbehebungen und Verbesserungen**

- Es wurde ein Problem behoben, bei dem das in `Send event complete` Ereignissen verfügbare Vorschläge-Array immer leer war.

## Version 2.21.2 – Donnerstag, 1. November 2023

**Neue Funktionen**

- `Request default personalization` Option zum Senden einer Ereignisaktion hinzugefügt.
- Unterstützung für die Ereignisse des oberen und unteren Ende der Seite in der Aktion „Ereignis senden“ wurde hinzugefügt.
- `Apply propositions` Aktion hinzugefügt.
- `Evaluate rulesets` Aktion und `Subscribe ruleset items` Ereignis für In-App-Nachrichten hinzugefügt.
- `Decision context` zur Aktion „Ereignis senden“ hinzugefügt.

**Fehlerbehebungen und Verbesserungen**

- Enthält Version 2.19.0 des Adobe Experience Platform Web SDK.

## Version 2.20.3 – Mittwoch, 8. August 2023

**Fehlerbehebungen und Verbesserungen**

- Es wurde ein Problem behoben, bei dem Datenelemente nicht im Feld ID-Synchronisierungs-Container-ID-Überschreibung gespeichert werden konnten.

## Version 2.20.1 – Freitag, 3. August 2023

**Fehlerbehebungen und Verbesserungen**

- Die Validierung gespeicherter Einstellungen zum Überschreiben des Datenstroms wurde verbessert.

## Version 2.20.0 – Dienstag, 31. Juli 2023

**Neue Funktionen**

- Unterstützung für [Überschreibungen der Datenstrom-ID pro Befehl](../../../../datastreams/overrides.md) hinzugefügt.

**Fehlerbehebungen und Verbesserungen**

- Veraltete `edgeConfigId` zugunsten von `datastreamId` in der SDK-Konfiguration.
- Mehrere Verbesserungen des Benutzererlebnisses für die Datenstromkonfiguration heben die Benutzeroberfläche auf.

## Version 2.19.0 – 21. Juni 2023

- Das Datenelement **[!UICONTROL Variable]** und die Aktionen **[!UICONTROL Variable aktualisieren]** sind jetzt allgemein verfügbar.

## Version 2.18.0 – 18. Mai 2023

- Enthält Version 2.17.0 des Adobe Experience Platform Web SDK.

## Version 2.17.0 – 25. April 2023

**Neue Funktionen**

- Enthält Version 2.16.0 des Adobe Experience Platform Web SDK.
- Es wurde Unterstützung für [Überschreibungen der Datenstromkonfiguration](/help/datastreams/overrides.md) hinzugefügt.
- Der Option `datasetId` des Befehls `sendEvent` wurde ein Hinweis hinzugefügt, dass sie veraltet ist.

**Fehlerbehebungen und Verbesserungen**

- Es wurde ein Problem behoben, durch das beim Scrollen in Safari die Datenstromauswahl geschlossen wurde.

## Version 2.16.1 – 14. April 2023

- Es wurde ein Problem mit XDM-Objekt- und -Variablen-Datenelementen behoben, durch das die Auswahl eines Schemas aus einer nicht standardmäßigen Sandbox verhindert wurde.

## Version 2.16.0 – 30. März 2023

**Neue Funktionen**

- (Beta) Aktion **[!UICONTROL Variable aktualisieren]** und Datenelement **[!UICONTROL Variable]** hinzugefügt.
- Konfiguration hinzugefügt für Callback-Funktion [`onBeforeLinkClickSend`](/help/web-sdk/commands/configure/onbeforelinkclicksend.md).

**Fehlerbehebungen und Verbesserungen**

- Es wurde ein Problem behoben, das dazu führte, dass das Klicken auf Elemente in einem Anker-Tag nicht funktionierte, wenn die Aktion **[!UICONTROL Umleiten mit Identität]** verwendet wurde.
- Es wurde ein Problem behoben, bei dem XDM-Objektdatenelemente nicht funktionierten, wenn nur ein Schema vorhanden war.
- Enthält Version 2.15.0 des Adobe Experience Platform Web SDK.

## Version 2.15.1 – 26. Januar 2023

- Es wurde ein Problem behoben, bei dem Benutzende ohne Zugriff auf Datenströme die Erweiterungskonfiguration nicht bearbeiten konnten.
- Es wurde Unterstützung für Oberflächen im Rahmen der Aktion `sendEvent` hinzugefügt.

Enthält Version 2.14.0 des Adobe Experience Platform Web SDK.

## Version 2.14.1 – 13. Oktober 2022

- Es wurde ein Problem behoben, bei dem die ID aus dem Experience Cloud-ID-Service vom Web SDK nicht berücksichtigt wird.

Enthält Version 2.13.1 der Adobe Experience Platform Web SDK-Bibliothek.

## Version 2.14.0 – 28. September 2022

- Es wurde eine neue `targetMigrationEnabled`-Konfiguration hinzugefügt, die eine vollständige seitenweise Migration ermöglicht.
- Es wurde eine Antwort-Aktion zum Anwenden hinzugefügt, um hybride Server-Client-Implementierungen zu ermöglichen.
- Es wurde eine Kontextoption für Benutzeragent-Client-Hinweise für hohe Entropie hinzugefügt.

Enthält Version 2.13.0 der Adobe Experience Platform Web SDK-Bibliothek.

## Version 2.13.0 – 29. Juni 2022

- Die Sortierreihenfolge numerischer Eigenschaften im XDM-Objekt-Datenelement wurde korrigiert, z. B. bei eVars.

Enthält Version 2.12.0 der Adobe Experience Platform Web SDK-Bibliothek.

## Version 2.12.0 – 13. Juni 2022

- Das Datenelement `identityMap` wurde so aktualisiert, dass die Namespace-Optionen basierend auf den in den Erweiterungseinstellungen definierten Sandboxes aufgefüllt werden.
- Die Aktion **[!UICONTROL Umleiten mit Identität]** wurde hinzugefügt, um eine Domain-übergreifende Identitätsfreigabe zu ermöglichen.
- Es wurden Dokumentations-Links zur Aktion `sendEvent` hinzugefügt.
- Die Bibliothek der React Spectrum-Benutzeroberfläche wurde aktualisiert.
- Es wurden verschiedene Verbesserungen an der Benutzeroberfläche vorgenommen.

Enthält Version 2.11.0 der Adobe Experience Platform Web SDK-Bibliothek.

## Version 2.11.2 – 3. Mai 2022

Enthält Version 2.10.1 der Adobe Experience Platform Web SDK-Bibliothek.

## Version 2.11.1 – 22. April 2022

- Ein fehlerhafter Konfigurationsbefehl aus Version 2.11.0 wurde korrigiert.

Enthält Version 2.10.0 der Adobe Experience Platform Web SDK-Bibliothek.

## Version 2.11.0 – 22. April 2022

- die Performance der Tags-Benutzeroberfläche wurde verbessert.
- Sandbox-Selektoren wurden zur Datenstrom-Erweiterungskonfiguration hinzugefügt.

Enthält Version 2.10.0 der Adobe Experience Platform Web SDK-Bibliothek.

## Version 2.10.0 – 10. März 2022

- Der Code-Ausschnitt zur Vorab-Ausblendung, der auf der Konfigurationsseite kopiert werden kann, wurde aktualisiert, um mit dem aktualisierten Adobe Target VEC-Editor verwendet werden zu können.

Enthält Version 2.9.0 der Adobe Experience Platform Web SDK-Bibliothek.

## Version 2.9.0 – 19. Januar 2022

Enthält Version 2.8.0 der Adobe Experience Platform Web SDK-Bibliothek.

## Version 2.8.0 – 26. Oktober 2021

Enthält Version 2.7.0 der Adobe Experience Platform Web SDK-Bibliothek.

- Weitere Informationen aus der Edge Network sind im Ereignis „Versandereignis abgeschlossen“ verfügbar, einschließlich `inferences` und `destinations`. Das Format dieser Eigenschaften kann sich ändern, da diese Funktionen derzeit als Teil einer Beta eingeführt werden.

## Version 2.7.3 – 7. September 2021

Enthält Version 2.6.4 der Adobe Experience Platform Web SDK-Bibliothek.

- Es wird nicht mehr vor der Einstellung von `container.buildInfo.environment.` gewarnt.

## Version 2.7.0 – 16. August 2021

Enthält Version 2.6.3 der Adobe Experience Platform Web SDK-Bibliothek.

- Bei Verwendung des Datenelementtyps „Identitätszuordnung“ werden Kennungen, deren IDs in Werte aufgelöst werden, bei denen es sich um nicht ausgefüllte Zeichenfolgen handelt, jetzt automatisch aus der Identitätszuordnung entfernt.
- Es wurde ein Fehler behoben, der bei dem Versuch auftrat, ein Datenelement mit dem Datenelementtyp „XDM-Objekt“ zu speichern, wenn kein Schema ausgewählt war.
- Die Typografie der Benutzeroberfläche wurde verbessert.

## Version 2.6.2 – 4. August 2021

Enthält Version 2.6.2 der Adobe Experience Platform Web SDK-Bibliothek.

## Version 2.6.1 – 29. Juli 2021

Enthält Version 2.6.1 der Adobe Experience Platform Web SDK-Bibliothek.

## Version 2.6.0 – 27. Juli 2021

Enthält Version 2.6.0 der Adobe Experience Platform Web SDK-Bibliothek.

- Labels, Beschreibungen und Fehlermeldungen mit dem Begriff „Edge-Konfiguration“ wurden gemäß der neuesten Adobe Experience Platform-Terminologie so geändert, dass stattdessen der Begriff „Datenstrom“ verwendet wird.
- In der Erweiterungskonfigurationsansicht wurde Unterstützung für die Verarbeitung einer großen Anzahl von Datenströmen und Datenstromumgebungen hinzugefügt.
- In der XDM-Objekt-Datenelementansicht wurde Unterstützung für die Verarbeitung einer großen Anzahl von Schemata hinzugefügt.
- Es wurde der Ereignistyp „Versandereignis abgeschlossen“ hinzugefügt, mit dem eine Regel ausgeführt werden kann, nachdem ein Ereignis an den Server gesendet und eine Antwort empfangen wurde. Zusätzliche Dokumentation wird in Kürze verfügbar sein.
- Der Ereignistyp „Entscheidungen erhalten“ wird nicht mehr unterstützt. Verwenden Sie stattdessen den Ereignistyp „Versandereignis abgeschlossen“.
- Die Benutzeroberfläche und die Fehlerbehandlung wurden allgemein verbessert.

## Version 2.5.0 – 1. Juni 2021

Enthält Version 2.5.0 der Adobe Experience Platform Web SDK-Bibliothek.

- Der Aktion „Ereignis senden“ wurde ein Feld `data` hinzugefügt. In der kommenden Dokumentation wird beschrieben, wie dies in bestimmten Szenarien verwendet werden kann.
- In der XDM-Objekt-Datenelementansicht wurde ein Problem behoben, bei dem ein Fehler ausgegeben wurde, wenn Benutzende Zugriff auf Adobe Experience Platform-Sandboxes hatten, aber nicht auf die als Standard für das Unternehmen konfigurierte Sandbox.
- In der XDM-Objekt-Datenelementansicht wurde ein Problem behoben, bei dem ein erforderliches Schemafeld als ungültig angesehen wurde, selbst wenn das übergeordnete Objekt keine Werte umfasste.

## Version 2.4.0 – 9. März 2021

Enthält Version 2.4.0 der Adobe Experience Platform Web SDK-Bibliothek.

- Ein Kontrollkästchen [ „Dokument wird ](/help/web-sdk/commands/sendevent/documentunloading.md)&quot; wurde der Benutzeroberfläche für die Aktion „Ereignis senden“ hinzugefügt.
- Es wurde Unterstützung für eine `out`-Option beim [Konfigurieren des Standardeinverständnisses](/help/web-sdk/commands/configure/defaultconsent.md) hinzugefügt, wodurch alle Ereignisse ignoriert werden, bis das Einverständnis eingeht (die vorhandene `pending`-Option stellt Ereignisse in die Warteschlange und sendet sie, sobald das Einverständnis eingeht).
- Dem Feld für das Standardeinverständnis wurde eine QuickInfo hinzugefügt.
- Es wurde Unterstützung für den Adobe Consent 2.0-Standard bei Verwendung des [`setConsent`](/help/web-sdk/commands/setconsent.md)-Befehls hinzugefügt.
- In der Benutzeroberfläche für das XDM-Objekt-Datenelement wird jetzt eine passendere Fehlermeldung angezeigt, wenn das Zugriffstoken der Benutzenden ungültig ist oder nicht ordnungsgemäß bereitgestellt wurde.
- Es wurde ein ursprungsübergreifender Fehler behoben (was sich nicht auf die Nutzung der Erweiterung auswirkt), der beim Anzeigen eines XDM-Objekt-Datenelements in der Developer Console für den Browser eingeblendet wurde.

## Version 2.3.0 – 4. November 2020

Enthält Version 2.3.0 der Adobe Experience Platform Web SDK-Bibliothek.

- Unterstützung für die Verwendung eines Datenelements beim Konfigurieren des Standardeinverständnisses hinzugefügt.
- Es wurde die Möglichkeit hinzugefügt, mit dem XDM-Objektdatenelementtyp nach XDM-Schemata zu suchen.
- Es wurde das Klonen von XDM-Daten im Aktionstyp „Ereignis senden“ hinzugefügt, um sicherzustellen, dass spätere Änderungen am XDM-Datenobjekt nicht in der Anfrage übernommen werden.

## Version 2.2.0 – 1. Oktober 2020

- Wenn Kundinnen oder Kunden versuchten, ein XDM-Objekt aus Sandbox-Schemata zu erstellen, traten Authentifizierungsprobleme auf. Die API, die Experience Platform aufruft, ist jetzt über Umgebungen informiert, sodass Benutzenden nur die Schemata präsentiert werden, auf die sie Zugriff haben, um sie zu bearbeiten.
- Bei Verwendung des Datenelements `identityMap` werden die Namespaces jetzt vorab in einer Dropdown-Liste ausgefüllt, sodass Sie dies nicht manuell tun müssen.
- Die Benutzeroberfläche für das Datenelement `xdmObject` wurde überarbeitet. In der neuen Benutzeroberfläche können Sie sehen, welche Felder ausgefüllt wurden, ohne jedes Element im Objekt eingeben zu müssen.

## Version 2.1.1 – 26. August 2020

- Behebung eines Problems, bei dem Adobe Experience Platform-Sandboxen in der XDM-Objekt-Ansicht fehlerhaft angezeigt wurden. Wenn bei Verwendung dieser Erweiterungsversion die erwartete Sandbox nicht in der Liste angezeigt wird, sollte sich der Benutzer an den Adobe Experience Platform-Administrator wenden, um sicherzustellen, dass die Zugriffsberechtigungen korrekt festgelegt sind.

## Version 2.1.0 – 5. August 2020

- Grundlegende Änderung: Die Aktion `syncIdentity` wurde entfernt; die Übergabe dieser IDs erfolgt jetzt über die Aktion `sendEvent`. Deaktivieren Sie ggf. bestehende Regeln, die diese Aktion verwenden, bevor Sie ein Upgrade der Erweiterung vornehmen.
- Aktualisierung auf Alloy Version 2.1.0 ([Versionshinweise](/help/web-sdk/release-notes.md))
- Unterstützung für den IAB 2.0-Standard für Einwilligungen in der Aktion `setConsent`.
- Unterstützung für das Überschreiben der Datensatz-ID in der Aktion `sendEvent`.
- Neues Datenelement vom Typ `IdentityMap`. Über dieses kann der Eintrag `identityMap` im nun aktivierten XDM-Objektdatenelement sowie in der Aktion `setConsent` ausgefüllt werden.
- Unterstützung für das Übergeben einer Identitätszuordnung bzw. „identityMap“ in der Aktion `setConsent`.
- Unterstützung für die Auswahl einer Experience Platform-Sandbox im XDM-Objekt-Datenelement.

## Version 1.0.0 – 26. Mai 2020

- Unterstützung für das Auswählen der Umgebung über den Konfigurations-Service.

## Version 0.1.2 – 4. Mai 2020

- `configId` wurde in `edgeConfigId` umbenannt.
- `viewStart` wurde in `renderDecisions` umbenannt und standardmäßig auf „false“ eingestellt. Bei der Einstellung „true“ werden Personalisierungsangebote abgerufen und automatisch gerendert.
- Änderungen im Zusammenhang mit `Get Decisions`:
   - Der Befehl `getDecisions` wurde entfernt.
   - Dem `sendEvent`-Befehl wurde die Option `scopes` hinzugefügt. Entscheidungen werden in der aufgelösten Zusage `sendEvent` zurückgegeben.
   - Es wurde ein integrierter `__view__`-Bereich hinzugefügt, der dafür sorgt, dass ganzseitige Angebote zurückgegeben werden. (VEC-Angebote in Target zum Beispiel.)
Diese Entscheidungen werden nur dann vom `sendEvent`-Befehl zurückgegeben, wenn `renderDecisions` auf „false“ gesetzt ist.
   - Es wurde ein `Decisions Received`-Ereignis hinzugefügt, das ausgelöst wird, wenn Entscheidungen verfügbar werden.
- Mehrere Personalisierungsbenachrichtigungen wurden unter einem einzigen Server-Aufruf kombiniert.
- Es wurde ein Problem mit der Ereignis-Merge-ID behoben, das jedes Mal zurückgesetzt wurde, wenn das Datenelement referenziert wurde.
- Die Aktion `setCustomerIds` wurde in `syncIdentity` umbenannt.
- Es wurde ein `getIdentity`-Befehl hinzugefügt. Dieser kann derzeit nur über benutzerdefinierten Code genutzt werden.
- Durch Aktivierung der Debugging-Funktion mit `_satellite` wird jetzt das Debugging im Adobe Experience Platform Web SDK aktiviert.
- Jetzt werden eingegebene Werte im XDM-Objekt unterstützt: Boolesche, Zahlen und Dezimalzahlen.

## Version 0.0.10 – 16. März 2020

- Die Konzepte von „Opt-in“ und „Opt-out“ wurden unter `Consent` vereint und ein neuer `setConsent`-Befehl wurde hinzugefügt.
- Ein neues Datenelement vom Typ `XDM Object` wurde hinzugefügt, das die Zuordnung von JavaScript/JSON zu XDM ermöglicht.

## Version 0.0.7 – 18. Februar 2020

- Die Optionen idSyncContainerId, datasetId, schemaId, urlDestinationsEnabled und cookieDestinationsEnabled wurden entfernt.
- Unterstützung für Bindestriche im Optionswert edgeDomain wurde hinzugefügt.
- Während der ID-Migration gestellte Anfragen werden an den demdex-Endpunkt gesendet, um die domänenübergreifende Identifizierung zu verbessern, wenn kein demdex-Cookie gesetzt wurde.
- Bei der ID-Migration gestellte Anfragen erwarten immer eine Antwort, um sicherzustellen, dass Identitäts-Cookies gesetzt werden.
- Beim Ausführen eines ungültigen Befehls wird eine Liste mit gültigen Befehlsnamen in der Konsole protokolliert.
- Es wurde ein Kontrollkästchen zum Umschalten der Unterstützung von Drittanbieter-Cookies zur Tag-Erweiterung hinzugefügt. Dadurch werden Aufrufe von demdex.net deaktiviert.

## Version 0.0.5 – 20. Dezember 2019

- Activity Tracker-Konfigurationen wurden zur Tag-Erweiterung hinzugefügt
- Anzeigen von EventType und EventMergeId beim Ereignisbefehl
- Es wurde eine onBeforeEventSend-Konfiguration zur Tag-Erweiterung hinzugefügt.
- Es wurde eine edgeBasePath-Konfiguration zur Tag-Erweiterung hinzugefügt.

## Version 0.0.3 – 25. November 2019

- Neue Felder „Merge-ID“ und „Typ“ bei der Aktion „Ereignis senden“. Die Merge-ID wird im XDM-Schema mit `xdm.eventMergeID` gemappt und der Typ wird im XDM-Schema mit `xdm.eventType` gemappt.

## Version 0.0.2 – 18. November 2019

- Erstmalige Veröffentlichung
