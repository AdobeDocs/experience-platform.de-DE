---
title: Versionshinweise zur Core-Erweiterung
description: Aktuelle Versionshinweise zur Core-Erweiterung in Adobe Experience Platform.
exl-id: a049b2d5-7a00-435d-bcc7-112658a53a1e
source-git-commit: 0955646164269d868be5161a117c6e12dbd9a4cb
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Core-Erweiterung – Versionshinweise

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../../term-updates.md).

## 29. März 2023

v3.4.1

* Fügt neue webnative Delegationsereignisse hinzu:
   * Keydown
   * KeyUp
* Fügt die Möglichkeit hinzu, mit vielen Werten (&quot;Weitere hinzufügen&quot;-Optionen) gegen die folgenden Delegaten zu testen:
   * Ereignisse
      * Änderung
   * Bedingungen
      * Cookie
      * Landing Page
      * Query String Parameter
      * Traffic-Quelle
      * Variable
* Ändert den &quot;events/EntersViewport&quot;-Delegaten für die Verwendung der [Schnittstellenbeobachter-API](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API) anstelle der manuellen Erkennung von Elementen, die in den Viewport gelangen.
* Entfernt Code, der DTM-Cookies zu LocalStorage migriert hat.
* Protokolliert eine Warnung auf der Konsole, wenn die LocalStorage- und SessionStorage-APIs nicht verfügbar sind.

## 4. Januar 2022

v3.3.0

* Ändert die [Trigger-Direktaufruf-Aktion](./overview.md#direct-call-action), damit Sie benutzerdefinierte Ereignisinformationen bereitstellen können, die an Direktaufrufregeln gesendet werden.

## 8. Oktober 2021

v3.2.2

* Korrigieren Sie das JSON-Schema für das Bedingungswert-Datenelement für alle verfügbaren Operatoren.
* Fehlerbehebung https://github.com/adobe/reactor-extension-core/issues/64.

## 23. September 2021

v3.2.1

* Es wurde ein Fehler behoben, bei dem die Initialisierung der Ansicht für Datenelemente mit bedingtem Wert nicht richtig funktionierte, wenn die Feldwerte 0 waren.

## 23. September 2021

v3.2.0

Die folgenden Änderungen wurden im Datenelement „Bedingter Wert“ eingeführt:

* Fügen Sie ein Kontrollkästchen für die bedingten und Fallback-Werte hinzu, damit der Benutzer auswählen kann, ob der zurückgegebene Wert „Undefiniert“ lauten soll.
* Zahlenwerte werden im Einstellungsobjekt als Zahlen dargestellt.
* Der bedingte Wert ist nicht mehr erforderlich, sodass er sich genauso verhalten kann wie der Fallback-Wert.

## 17. September 2021

v3.1.1

* Behebung eines JS-Fehlers, der verhinderte, dass die Ansicht für die Bedingung „Datumsbereich“ geladen werden konnte.

## 16. September 2021

v3.1.0

Neue Datenelemente wurden hinzugefügt:

* Zusammengeführtes Objekt - Wählen Sie mehrere Datenelemente aus, die jeweils ein Objekt bereitstellen sollen. Diese Objekte werden rekursiv zusammengeführt, um ein neues Objekt zu erzeugen.
* Bedingter Wert - Gibt einen von zwei Werten (conditionalValue oder fallbackValue) zurück, der auf dem Ergebnis des Vergleichs basiert.
* Laufzeitumgebung - Rückgabe einer der folgenden Launch-Umgebungsvariablen: Umgebungsstufe, Bibliothekserstellungsdatum, Eigenschaftsname, Eigenschafts-ID, Regelname, Regel-ID, Ereignistyp, Ereignisdetail-Payload, Direktaufruf-Identifikator.
* JavaScript-Tools - Wrapper für gängige JavaScript-Operationen: Grundlegende String-Manipulation (replace, substring, regex match, first and last index, split, slice), grundlegende Array-Operationen (slice, join, pop, shift) und grundlegende universelle Operationen (slice, length).
* Geräteattribute - Rückgabe von Geräteattributen wie Fenstergröße oder Bildschirmgröße.

## 11. August 2021

v3.0.0

* PDCL-6153: Unterstützt das zuverlässige Abrufen von vollständig qualifizierten URLs für zwischengespeicherte benutzerdefinierte Code-Aktionen.

Version 3.0.0 der Haupterweiterung ist mit Änderungen in [Version 27.2.0 der Turbine web runtime](https://github.com/adobe/reactor-turbine/releases/tag/v27.2.0) verknüpft, die es Benutzern ermöglichen, ihre Bibliothek in viele von Adobe verwaltete Host-Regionen zu laden, wenn das Unternehmen des Benutzers Premium CDN unterstützt.

Dieses Upgrade ist optional und abwärtskompatibel für Benutzer ohne Premium-CDN. Für Kunden, die Premium-CDN in ihrem Unternehmen aktiviert haben, ist es obligatorisch.

## 20. Mai 2021

v2.0.7

* Es wurde ein Problem behoben, durch das Mausinteraktionen auf Texteingaben nicht mehr ordnungsgemäß funktionierten.
* Die Verwendung der Bedingungen für Browser und Betriebssystem wird verworfen.

## 4. Mai 2021

v2.0.6

* Geringfügige Aktualisierung zur Korrektur von Symbolen, die bei einer Änderung der Bildschirmgröße verzerrt werden.

## 11. März 2021

v2.0.5

* Der Code in der Laufzeit-Auswertung für Ereignisse und Aktionen mit einer Verzögerungsoption, die jetzt Datenelementwerte unterstützt, die in Version 2.0.4 hinzugefügt werden, wurde aktualisiert, sodass nun Zeichenfolgen ordnungsgemäß in Zahlen umgewandelt werden.

## 9. März 2021

v2.0.4

* Unterstützung von Datenelementen für verschiedene Felder hinzugefügt – Die Unterstützung von Datenelementen wurde den folgenden Ereignissen hinzugefügt: „Zeit auf Seite“, „Betreten des Viewports“, „Hover“ und „Abgespielte Medienzeit“. Zusätzlich zu den folgenden Bedingungen: „Besuchszeit pro Site“ und „Vergleich von Werten“
* Fügt Unterstützung für das Standardverhalten von Strg/Befehlstaste+Klick und auch Mittelmausklick bei Verwendung der Linkverzögerung hinzu.
* **Die Linkverzögerung im Klickereignis wurde als „nicht mehr unterstützt“ gekennzeichnet.** – Weitere Informationen finden Sie im [Datenerfassungs-Blog](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/explainer-link-delay/ba-p/398403) für Adobe Experience Platform

## 6. Januar 2021

v1.9.0

* **Neue Aktion „Trigger Direct Call“** (Direktaufruf auslösen): Die Core-Erweiterung enthält jetzt einen neuen Aktionstyp namens `Trigger Direct Call`.  Dieser kann verwendet werden, um eine Direktaufrufregel über eine Aktion aus einer anderen Regel auszulösen. Er wird direkt der Methode `_satellite.track()` zugeordnet. Vielen Dank an [Jan Exner](https://twitter.com/jexner) für diesen Beitrag.

## 8. Dezember 2020

v1.8.4

* Es wurde ein Fehler behoben, durch den ein User CSP vorübergehend nicht löschen oder deaktivieren konnte.

## 28. Juli 2020

v1.8.3

* Es wurde ein Fehler behoben, durch den die CSP-Nonce beim Starten der Erweiterung nur einmal gelesen wurde, anstatt beim Aufruf der benutzerdefinierten Code-Aktion neu abgerufen zu werden.

## 13. Juli 2020

v1.8.2

* Es wurde ein Fehler behoben, durch den die Aktion für benutzerspezifischen Code einen Fehler für HTML-Code ausgab, der Token ohne Tag-Namen enthielt (z. B. Kommentare).

## 10. Juli 2020

v1.8.1

* Es wurde ein Fehler behoben, durch den benutzerdefinierte HTML-Entitäten innerhalb von Attributen von `script`- und `style`-Tags nicht korrekt dekodiert wurden, bevor sie auf die Seite geschrieben wurden.
* Es wurde ein Fehler behoben, der auftrat, wenn eine externe benutzerdefinierte Code-Aktion keinen Inhalt enthielt. Die externe Aktion für benutzerdefinierten Code ist die Aktion, die aus einer anderen Datei als der Bibliothek geladen wird (dies tritt auf, wenn das Ereignis, das die Regel auslöst, nicht libraryLoaded oder pageBottom ist).

## 6. Juli 2020

v1.8.0

* **Promises in benutzerspezifischem Code** – Bedingungen für benutzerspezifischen Code und JavaScript-Aktionen, die nicht global ausgeführt werden, können jetzt Promises zurückgeben.  Sie können sie verwenden, damit nachfolgende Bedingungen und Aktionen auf den Abschluss eines asynchronen Prozesses in Ihrem benutzerspezifischen Code warten, bevor Sie mit dem nächsten Element fortfahren.
* **Callbacks in Aktionen mit benutzerdefiniertem HTML-Code** – Sie können dasselbe in Aktionen mit benutzerdefiniertem HTML-Code erreichen, indem Sie die Callbacks `onCustomCodeSuccess()` und `onCustomCodeFailure()` verwenden.

Weitere Informationen finden Sie im [Referenzdokument zur Haupterweiterung](./overview.md) unter Bedingungen > Benutzerspezifischer Code und Aktionen > Benutzerspezifischer Code.

## 7. April 2020

v1.7.3

* **Vergrößerung der Textfeldlänge** – Texteingabefelder haben jetzt ein Flex-Layout, um die Bildschirmbreite des Benutzers besser zu nutzen und längeren Textzeichenfolgen mehr Platz zu geben.

## 1. November 2019

v1.7.0

* **Zugriff auf die `event`-Variable innerhalb des Datenelements für benutzerspezifischen Code** – Sie können jetzt auf das Ereignis in einem Datenelement für benutzerspezifischen Code verweisen, wenn es im Kontext einer Regel ausgeführt wird. Das -Objekt enthält nützliche Informationen zum Ereignis, das die Regel ausgelöst hat. Vielen Dank an [Stewart Schilling](https://twitter.com/sdi_stewart) für diesen Beitrag.

## 7. Oktober 2019

v1.6.2

* **Neuer Datenelement-Typ „Konstante“** – Die Core-Erweiterung enthält jetzt das neue Datenelement `Constant`.  Hiermit können Sie einen konstanten Wert speichern, der in verschiedenen Bedingungen, Aktionen oder benutzerdefiniertem Code referenziert wird. Vielen Dank an [Jan Exner](https://twitter.com/jexner) für diesen Beitrag.

## 11. September 2019

v1.6.1

* **Unterstützung von CSP mit einer Nonce** – Die Haupterweiterung hat jetzt einen optionalen Konfigurationsparameter. Sie können damit ein Datenelement hinzufügen, das eine Nonce referenziert. Falls konfiguriert, verwenden alle Inline-Skripte, die ein Tag zur Seite hinzufügt, die von Ihnen konfigurierte Nonce. Durch diese Änderung wird die Verwendung einer CSP mit einer Nonce unterstützt, sodass Launch-Skripte weiterhin in einer CSP-Umgebung geladen werden. Weitere Informationen zur Verwendung von Tags mit einer CSP finden Sie [hier](../../../ui/client-side/content-security-policy.md).

## 18. Juni 2019

v1.5.0

* **Direktaufruf-Protokollierung** – Die Browserprotokollierung für Direktaufrufregeln bietet jetzt zusätzliche Details, wenn sie passiert wird.

## 8. Mai 2019

v1.4.3

* **Eingabefelder** – Eingabefelder sind nun viel länger.
* **Benutzerdefiniertes Ereignis** – Der benutzerdefinierte Ereignistyp kann nun mit Ereignissen verwendet werden, die außerhalb des Fensters abgesendet werden.
* **Fehlerbehebung** – Behebung eines Fehlers, durch den die Wertvergleichsbedingung keinen 0-Wert enthalten konnte.
* **Fehlerbehebung** – Aktualisierung des Felds exchange\_url, sodass nun der Listeneintrag der Haupterweiterung in Adobe Exchange angezeigt wird.

## 8. Januar 2019

v1.4.2

* **Viewport-Aufruf-Ereignis** – Zuvor wurde das Viewport-Aufruf-Ereignis nur einmal pro Seite ausgelöst. Dieses Verhalten kann nun so konfiguriert werden, dass es jedes Mal ausgelöst wird, wenn das Element den Viewport aufruft.
* **Benutzerspezifisches Ereignis** – Benutzerspezifische Ereignisse können jetzt kontextbezogene Daten enthalten, die innerhalb von Bedingungen und Aktionen verwendet werden können.
* **Klickereignis** – Wenn Sie eine Link-Verzögerung im Klickereignis festlegen, wird es sich für nachkommende Elemente des Ankers und nicht nur für den Anker selbst registrieren.

## 8. November 2018

* **Option „Kohorte beibehalten“** – Die Option, eine Kohorte dauerhaft beizubehalten, wurde zur Sampling-Bedingung hinzugefügt. Dadurch wird die Beispielkohorte für einen Benutzer sitzungsübergreifend beibehalten oder beendet. Wenn beispielsweise das Kontrollkästchen „Kohorte beibehalten“ aktiviert ist und die Bedingung bei der ersten Ausführung für einen bestimmten Besucher „true“ zurückgibt, gibt sie in allen nachfolgenden Ausführungen der Bedingung für denselben Besucher ebenfalls „true“ zurück. Wenn das Kontrollkästchen „Kohorte beibehalten“ aktiviert ist und die Bedingung bei der ersten Ausführung für einen bestimmten Besucher „false“ zurückgibt, gibt sie gleichermaßen in allen nachfolgenden Ausführungen der Bedingung für denselben Besucher ebenfalls „false“ zurück.
* **Fehlerbehebung** – Es wurde ein Problem behoben, durch das eine Regel mithilfe eines Seitenende-Ereignisses und einer benutzerdefinierten Code-Aktion auf einer Seite, auf der Tags zwar synchron geladen, aber nicht ordnungsgemäß installiert wurden (kein Aufruf von `_satellite.pageBottom()`), Inhalte der Website gelöscht hat.
* **Fehlerbehebung** – Es wurde ein Problem behoben, bei dem Enters Viewport nicht funktionierte, wenn die Tag-Bibliothek asynchron geladen wurde und das Laden abgeschlossen wurde, nachdem das DOMContentLoaded-Ereignis des Browsers ausgelöst wurde.

## 24. Mai 2018

* **Funktion** – Hinzufügung einer Wertvergleichsbedingung. Dabei werden zwei Werte mit verschiedenen verfügbaren Operatoren verglichen. Dadurch wird die Funktionalität verschiedener älterer Bedingungen ersetzt, die viel zu spezifisch waren.
* **Funktion** – Hinzufügung einer „Max. Häufigkeit“-Bedingung, mit der Sie festlegen können, wie oft die Bedingung innerhalb eines Zeitraums oder Ereignisauftretens „true“ zurückgeben soll. Beispiele: 5 Mal pro Tag, 2 Mal pro Besuch.

## 11. April 2018

* **Funktion** – Datenelemente können nun auf andere Datenelemente verweisen.

## 20. März 2018

* **Fehlerbehebung** – Benutzerdefinierte Codefenster wiesen `document.write`-Fehler auf und wurden in asynchronen Implementierungen nicht ausgeführt
* **Fehlerbehebung** – Hauptmodule wurden nicht in einer Bibliothek eingeschlossen
* **Fehlerbehebung** – Probleme mit Mindest- und Höchstwerten im Datenelement „Zufällige Nummer“

## 10. Januar 2018

* **Funktion** – Datenelement „Zufällige Nummer“
* **Funktion** – Datenelement „Seiteninformationen“
* **Funktion** – Datumsbedingung
* **Funktion** – Sampling-Bedingung
