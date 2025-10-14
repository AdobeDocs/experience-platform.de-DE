---
title: Versionshinweise für die Adobe Analytics-Erweiterung
description: Aktuelle Versionshinweise für die Tag-Erweiterung „Adobe Analytics“ in Adobe Experience Platform.
exl-id: 3c7b4ec0-4b81-4ef4-b15f-6ad102525840
source-git-commit: 5f4e157a39bf927b3821931d55f968862b2ed16d
workflow-type: tm+mt
source-wordcount: '1524'
ht-degree: 70%

---

# Adobe Analytics-Erweiterung – Versionshinweise

Im Folgenden finden Sie eine Liste der Versionshinweise für die Adobe Analytics-Tag-Erweiterung.

>[!NOTE]
>
>Die Analytics-Tag-Erweiterung wird oft als Reaktion auf Aktualisierungen der [AppMeasurement JavaScript Library aktualisiert](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=de). Einzelheiten zu den unten genannten spezifischen Versionen finden [&#128279;](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=de) in den AppMeasurement-Versionshinweisen.

## 28. Oktober 2024

**Adobe Analytics-Erweiterung 1.9.6**

**Funktionen**:

* Eine neue Funktion wurde hinzugefügt, mit der Benutzende eine JSON-Version der Aktion „Variablen festlegen[&#x200B; anzeigen und &#x200B;](https://experienceleague.adobe.com/de/docs/experience-platform/tags/extensions/client/analytics/overview#set-variables) können. Die Adobe Web SDK-Erweiterung enthält auch eine Aktion zum [Ausfüllen einer Analytics-Variablen](https://experienceleague.adobe.com/de/docs/experience-platform/tags/extensions/client/web-sdk/data-element-types) durch Bereitstellung von JSON. Durch Kopieren von JSON-Daten aus der AA-Erweiterung in die Web SDK-Erweiterung können migrierende Kunden einfach mehrere Einstellungen gleichzeitig übertragen, anstatt jede Variable manuell hinzuzufügen.

## 12. August 2024

**Adobe Analytics-Erweiterung 1.9.5**

**Funktionen**:

* Auf [AppMeasurement auf Version 2.27.0 aktualisiert](https://github.com/adobe/appmeasurement/releases/tag/v2.27.0).

## 4. März 2024

**Adobe Analytics-Erweiterung 1.9.4**

**Funktionen**:

* Auf [AppMeasurement auf Version 2.26.0 aktualisiert](https://github.com/adobe/appmeasurement/releases/tag/v2.26.0).

## 15. September 2023

**Adobe Analytics-Erweiterung 1.9.3**

**Funktionen**:

* Auf [AppMeasurement auf Version 2.25.0 aktualisiert](https://github.com/adobe/appmeasurement/releases/tag/v2.25.0).


## 19. Juli 2023

**Adobe Analytics-Erweiterung 1.9.2**

**Funktionen**:

* Aktualisierung auf [AppMeasurement v2.24.0](https://github.com/adobe/appmeasurement/releases/tag/v2.24.0).
* Es wurde eine optionale Konfiguration (`decodeLinkParameters` Standard-`false`) hinzugefügt, die Link-URLs decodiert, die doppelbyte-codierte Zeichen enthalten.

**Fehlerbehebungen**:

* Es wurde eine zusätzliche Fehlerbehandlung für Browser mit fehlerhaften APIs [&#x200B; hohe Entropie (Benutzeragenten](https://experienceleague.adobe.com/docs/analytics/technotes/client-hints.html?lang=de)Client-Hinweise) hinzugefügt.
* Die Kopfzeile [POST &#x200B;](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/POST) Inhaltstyp wurde geändert, sodass sie standardmäßig `x-www-form-urlencoded` verwendet wird.

## 23. September 2022

**Adobe Analytics-Erweiterung 1.9.**

**Funktionen**:

* Auf AppMeasurement v2.23.0 aktualisiert.
* Die Erweiterung kann jetzt Client[Hinweise mit hoher Entropie erfassen, &#x200B;](https://developer.mozilla.org/en-US/docs/Web/HTTP/Client_hints#user-agent_client_hints) von der neuesten AppMeasurement-Version unterstützt wird.

## 28. Februar 2022

**Adobe Analytics-Erweiterung 1.9.0**

**Fehlerbehebungen**:

* Einige Debug-Anweisungen in AppMeasurement wurden entfernt.

## Dienstag, 29. November 2021

**Adobe Analytics-Erweiterung 1.8.**

**Fehlerbehebungen**:

* AppMeasurement wurde auf Version 2.22.3 aktualisiert.

## 16. September 2021

**Adobe Analytics-Erweiterung 1.8.7**

**Fehlerbehebungen**:

* AppMeasurement wurde auf Version 2.22.2 aktualisiert.
* Nicht mehr unterstützte Umgebung „buildInfo.environment“ entfernt

## 24. August 2021

**Adobe Analytics-Erweiterung 1.8.6**

**Fehlerbehebungen**:

* [AppMeasurement wurde auf Version 2.22.1 aktualisiert](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=de).
* Der Fallback-linkName wurde aktualisiert und spiegelt nun die Activity Map-Logik statt der Verwendung von innerHTML wider.

## 6. August 2020

**Adobe Analytics-Erweiterung 1.8.5**

**Fehlerbehebungen**:

* In den Einstellungen für das AAM-Modul wurde der falsche Cookie-Name festgelegt, wenn das entsprechende Feld leer gelassen wurde. Dieser Fehler wurde nun behoben.

**Funktionen**:

* AppMeasurement wurde aktualisiert auf [Version 2.22.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=de).
* Geringfügige Änderung an der Benutzeroberfläche: Die zusätzliche Einstellung wird jetzt in einem Accordion konsolidiert angezeigt anstatt in einem Kontrollkästchen.

## 2. Juni 2020

**Adobe Analytics-Erweiterung 1.8.4**

**Fehlerbehebungen**:

* Es wurde ein Fehler behoben, durch den die Warenkorbereignisse (prodView, scAdd, scView usw.) nicht im Ereignis-Dropdown-Menü angezeigt wurden. All diese Optionen sollten jetzt aus der Dropdown-Liste ausgewählt werden können.

**Funktionen**:

* Sie können nun die Activity Map in der Erweiterung deaktivieren, ohne dass benutzerdefinierter Code verwendet werden muss. Die Activity Map wird als separates Modul geladen (ähnlich wie das AAM-Modul) und kann bei Bedarf deaktiviert werden.
* Die Benutzeroberfläche wurde durch Minimierung von Hierarchievariablen und anderen Optionen bereinigt.
* Es wurde ein Feld zum Einstellen von Kauf-IDs in der Benutzeroberfläche für die Erweiterungskonfiguration hinzugefügt.

## 10. März 2020

**Adobe Analytics-Erweiterung 1.8.3**

**Fehlerbehebungen**:

* Es wurde ein Fehler behoben, der sich auf die Regelkonfiguration auswirkte und einen Fehler auslöste, wenn Sie versuchten, Variablen festzulegen, während Sie eine benutzerdefinierte Bibliothek verwendeten und Ihre Report Suites nicht in Analytics konfiguriert worden waren.
* Beim Erstellen einer eVar trat ein Fehler auf, durch den nicht die Option zum „Duplizieren von“ einer Prop oder umgekehrt angezeigt wurde. Dieses Problem wurde nun behoben, sodass das Verhalten dem in früheren Versionen entspricht.

**Funktionen**:

* [AppMeasurement wurde auf Version 2.20.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=de) aktualisiert.

## 2. März 2020

**Adobe Analytics-Erweiterung 1.8.2**

**Fehlerbehebungen**:

* Es wurde ein Problem behoben, bei dem eine falsche Syntax für numerische Ereignisse und serialisierte Währung verwendet wurde.

**Funktionen**:

* [AppMeasurement wurde auf Version 2.18.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=de) aktualisiert.
* DIL-Bibliothek im Audience Manager-Modul wurde auf Version 9.4 aktualisiert.
* Länge der Eingabefelder in der Erweiterung wurde erhöht.
* eVars und Props in den Erweiterungs- und Aktionskonfigurationen zeigen jetzt den Anzeigenamen von Analytics an.
* Im Abschnitt „Cookies“ der Erweiterungskonfiguration wurde ein Kontrollkästchen hinzugefügt, mit dem Sie sichere Cookies schreiben können.
* Dem Audience Manager-Modul wurden drei neue Konfigurationen hinzugefügt. Es wurde eine Einstellung hinzugefügt, mit der die Protokollierung, URL-Ziele und Cookie-Ziele aktiviert werden können.

## 13. November 2019

**Adobe Analytics-Erweiterung 1.8.**

**Fehlerbehebungen**:

* Es wurde ein Fehler behoben, durch den Premium-eVar und -Props nicht gespeichert wurden.

## 1. November 2019

**Adobe Analytics-Erweiterung 1.8.0**

**Fehlerbehebungen**:

* Es wurde ein Fehler behoben, durch den manche Kunden keine Report Suite-Optionen in der Dropdown-Liste sehen konnten
* Es wurde ein Fehler behoben, durch den manche Variablen bei der Verwendung von ECID nicht korrekt eingestellt wurden

**Funktionen**:

* Numerische Sortierung von eVar, Props und Ereignissen in der Erweiterungsansicht
* Änderungen am Backend-Schema zur Unterstützung von Magento-Kontextdaten

## 6. September 2019

**Adobe Analytics-Erweiterung 1.7.8**

**Fehlerbehebungen**:

* Ein Fehler wurde behoben, durch den Benutzer in der Dropdown-Liste keine Report Suite-Optionen sehen konnten
* Ein Fehler wurde behoben, durch den Ereignisse nicht korrekt ausgelöst wurden

## 5. September 2019

**Adobe Analytics-Erweiterung 1.7.7**

**Funktionen**:

* AppMeasurement wurde auf Version 2.17 aktualisiert.
* Zielgruppen-Management-Modul wurde aktualisiert, sodass es jetzt DIL 9.3 unterstützt.
* Feldbreiten wurden aktualisiert, um mehr Platz zur Verfügung zu stellen

**Fehlerbehebungen**:

* Ein Fehler wurde beim Festlegen der Opt-in-/Opt-out-Option behoben
* Ein Fehler wurde behoben, durch den Variablen bei der Verwendung von ECID nicht richtig festgelegt wurden

## 18. Juli 2019

**Adobe Analytics-Erweiterung 1.7.6**

**Funktionen**:

* Aktualisierung der Adobe Analytics-Erweiterung für die Unterstützung von DIL 9.2 für Audience Manager

* Aktualisierung der Erweiterung zur Unterstützung von [AppMeasurement 2.15.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=de#version-2.15.0)
* Das folgende Kontrollkästchen wurde entfernt, da es nicht mehr unterstützt wird: „Hängen Sie den Destination Publishing IFRAME nicht an das DOM an oder lösen Sie Ziele aus“

## 4. Juni 2019

**Adobe Analytics-Erweiterung 1.7.5**

**Funktionen**:

* Aktualisierung der Adobe Analytics-Erweiterung auf [AppMeasurement 2.14.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=de#version-2.14.0), die unter anderem ein bekanntes clearVars-Problem behebt
* Hinzufügung eines Exchange-Links zur Erweiterung. Der Exchange-Listeneintrag kann über die Option „Erweiterungsinfo“ im Dropdown-Menü aufgerufen werden.

**Fehlerbehebungen**:

* Behebung eines Fehlers in der Benutzeroberfläche, durch den die falsche eVar aus einer Liste gelöscht wurde
* Behebung eines Fehlers, durch den bei dem Versuch, mehrere Report Suites hinzuzufügen, ein SSL-Tracking-Server erforderlich war. Wenn mehrere Report Suites hinzugefügt werden, ist ein Tracking-Server erforderlich, das SSL-Tracking-Serverfeld ist jedoch optional.

## 15. April 2019

**Adobe Analytics-Erweiterung 1.7.4**

**Fehlerbehebungen**:

* Zurücksetzung der Erweiterung, nachdem ein Fehler in AppMeasurement 2.13.0 gefunden wurde. Die Version verursachte ein Problem, bei dem die ECID nicht gesendet wurde. Wenn Sie also 1.7.3 installiert haben, empfehlen wir ein Upgrade auf 1.7.4, um dieses Problem zu vermeiden. Beachten Sie, dass clearVars fortgesetzt wird, bis eine aktualisierte Version von AppMeasurement veröffentlicht wird

## 12. April 2019

**Adobe Analytics-Erweiterung 1.7.3**

**Fehlerbehebungen**:

* Aktualisierung der Adobe Analytics-Erweiterung auf AppMeasurement 2.13.0, die unter anderem ein bekanntes clearVars-Problem behebt.

## 21. März 2019

**Adobe Analytics-Erweiterung 1.7.2**

**Funktionen**:

* Aktualisierung der Adobe Analytics-Erweiterung auf DIL 9.1.
* Aktualisierung der Adobe Analytics-Erweiterung auf AppMeasurement 2.12.
* Aktualisierung der Adobe Analytics-Erweiterung auf React-Spectrum.
* Beim Konfigurieren Ihrer Report Suites auf der Konfigurationsseite wird jetzt ein Dropdown-Menü für alle Report Suites in Ihrem Unternehmen angezeigt, damit Sie die gewünschte Report Suite einfacher auswählen können.

## 7. März 2019

**Adobe Analytics-Erweiterung 1.7.1**

**Fehlerbehebungen**:

* Zurücksetzung der Erweiterung auf Version 1.6, nachdem ein Fehler in Version 1.7 gefunden wurde.

## 11. Februar 2019

**Adobe Analytics-Erweiterung 1.6**

**Funktionen**:

* Aktualisierung der Adobe Analytics-Erweiterung auf DIL 9.0. Diese Version unterstützt die Anmeldung.
* Aktualisierung der Adobe Analytics-Erweiterung auf AppMeasurement 2.11, um Opt-in zu unterstützen.

**Fehlerbehebungen**:

* Behebung eines Konflikts mit dem Prototyp-JS. Die Analytics-Erweiterung unterstützt jetzt standardmäßige prototype.js-Bibliotheken.

## 9. November 2018

**Adobe Analytics-Erweiterung 1.5.1**

**Fehlerbehebungen**:

* Herabstufung des DIL-Moduls auf Version 7.0, um ein Problem zu beheben, bei dem Analysesignale nicht ausgelöst wurden.

## 5. November 2018

**Adobe Analytics-Erweiterung 1.5**

**Funktionen**:

* Aktualisierung der Adobe Analytics-Erweiterung, um DIL 8.0 in Audience Manager zu unterstützen.
* Unterteilung des Felds „Serialisieren von Wert“ in zwei Felder: „Ereignis-ID“ und „Ereigniswert“. Dadurch wird das Problem behoben, durch das statt der Serialisierung eines Ereignisses ein Wert zugewiesen wird
   * Bitte beachten: Wenn Sie das aktuelle Feld verwenden, um eine ID mithilfe einer Zeichenfolge hinzuzufügen (z. B. Event7=3:abc123), müssen Sie Ihre Eingabe aktualisieren, um die ID im Feld „Ereignis-ID“ wiederzugeben

**Fehlerbehebungen**:

* Behebung eines Fehlers, durch den der Währungscode nicht ordnungsgemäß ausgefüllt werden konnte

## 11. Oktober 2018

**Adobe Analytics-Erweiterung 1.4**

**Funktionen**:

* Migration des Tracking-Cookie-Namens in die Erweiterungskonfiguration.

**Fehlerbehebungen**:

* Behebung eines Fehlers, sodass festgelegte Variablen nicht abstürzen, wenn kein trackerProperties-Objekt verfügbar ist.

## 5. Juni 2018

**Adobe Analytics-Erweiterung 1.3**

**Funktionen**:

* Aktualisierung der Adobe Analytics-Erweiterung zur Unterstützung von AppMeasurement 2.9.
* Hinzufügung der Funktion „Tracker global zugänglich machen“ in der Adobe Analytics-Erweiterung, wodurch der Tracker unter `windows.s` global geladen werden kann.

**Fehlerbehebungen**:

* Behebung eines Fehlers, durch den die Listenansicht beim Zurückkehren aus der Detailansicht zurückgesetzt wurde
* Behebung einiger Fehler, um das Laden von Ressourcen in der Revisionsauswahl zu verbessern
* Behebung eines Fehlers, durch den s.events von mehreren Regeln in der Adobe Analytics-Erweiterung überschrieben wurden.

## 20. März 2018

**Adobe Analytics-Erweiterung 1.2**

**Funktionen**:

* Aktualisierung von AppMeasurement.js auf Version 2.8.0.
* Fügt Unterstützung für Server-seitige Weiterleitung hinzu

## 8. Februar 2018

**Adobe Analytics-Erweiterung 1.**

**Funktionen**:

* Aktualisierung von AppMeasurement auf Version 2.6.
* Der initialisierte Analytics-Tracker wird jetzt über ein freigegebenes Modul in der Adobe Experience Platform-Tag-Erweiterung offengelegt, sodass andere Erweiterungen Code zur Interaktion mir ihr enthalten können.

**Fehlerbehebungen**:

* Behebung eines Fehlers in der Adobe Analytics-Erweiterung, durch den die Meldung „Fehler: fehlende Report Suite-ID bei AppMeasurement-Initialisierung“ in der Browserkonsole angezeigt wurde.
