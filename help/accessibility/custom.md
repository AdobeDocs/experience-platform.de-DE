---
keywords: Experience Platform;Profil;Echtzeit-Kundenprofil;Fehlerbehebung;API;Einheitliches Profil;Einheitliches Profil;Profil;RTCP;XDM-Diagramme
title: Benutzerdefinierte Barrierefreiheitslösungen für Experience Platform
topic: Handbuch
type: Documentation
description: Erfahren Sie mehr über die benutzerdefinierten Barrierefreiheitslösungen in der Benutzeroberfläche von Adobe Experience Platform.
source-git-commit: 81db01c3e8d332e1fc8127d779c3a584bb498858
workflow-type: tm+mt
source-wordcount: '1532'
ht-degree: 1%

---


# Benutzerdefinierte Barrierefreiheitslösungen für Experience Platformen

Adobe Experience Platform wird kontinuierlich verbessert, um den Anforderungen aller Benutzertypen gerecht zu werden und den weltweiten Standards zu entsprechen, zu denen auch Personen mit Sehbehinderungen, Hörgeschäften, Mobilitäten oder anderen Beeinträchtigungen gehören. In diesem Dokument werden benutzerdefinierte Barrierefreiheitslösungen in der Benutzeroberfläche von Experience Platform beschrieben.

## Übersicht über Startseite und Benutzeroberfläche

Die Benutzeroberfläche der Experience Platform erfüllt die erforderlichen Kontrastverhältnisse für Standardtext-, Grafik- und Benutzeroberflächenkomponenten. Die Farben der Benutzeroberfläche wurden ebenfalls ausgewählt, um die Barrierefreiheit für alle Benutzer zu unterstützen, auch für Benutzer mit visuellen Behinderungen.

In Platform können Benutzeroberflächen-Elemente, die mit einem Zeiger angeklickt oder bearbeitet werden können, auch über eine Tastatur interagiert werden. Dazu gehören die linke Navigation, Videoplayer, Tabellen und mehr.

Experience Platform strebt die Einhaltung internationaler Barrierefreiheitsstandards an, einschließlich der Web Content Accessibility Guidelines 2.1 Level A und Level AA sowie der Web Accessibility Initiative - Accessible Rich Internet Applications (WAI-ARIA) Web Standards.

![Die Startseite der Adobe Experience Platform-Benutzeroberfläche.](images/homepage.png)

## Linke Navigation

Die linke Navigation in der Experience Platform-Benutzeroberfläche ist über die Tastatur zugänglich und bietet Farbkontrast in normalen, Hover- und Auswahlstatus, die den Barrierefreiheitsstandards entsprechen.

Auf dem Startbildschirm können Benutzer die Tabulatortaste zur linken Navigation drücken. Wenn Sie **Umschalt + Tab** auswählen, wird der Benutzer zum Startbildschirm zurückgeleitet.

![Die Experience Platform verließ die Navigation.](images/left-navigation-select.png)

Da die linke Navigation im Fokus ist, bringt **Tab** Benutzer zur Interaktion &quot;Erweitern und Reduzieren&quot;. Die Möglichkeit zum Erweitern oder Reduzieren der linken Navigation wird mit **Eingabetaste (Return)** aktiviert.

![Die Navigation links in der Experience Platform wurde reduziert.](images/left-navigation-collapse.png)

Wenn die linke Navigation im Fokus ist, navigieren die Nach-oben- und Nach-unten-Pfeiltasten zu jedem Element in der Navigation und der Zyklus kontinuierlich (d. h. der Fokus wechselt nicht weg, bis der Benutzer die linke Navigation mit der Tabulatortaste verlässt). Der Fokus wird für Navigationselemente angezeigt, wenn diese ausgewählt sind. Die aktuelle Auswahl wird mit einem hervorgehobenen und fett hervorgehobenen Text angezeigt. Bei Auswahl eines linken Navigationselements öffnet **Enter (Return)** das ausgewählte UI-Element im rechten Bereich. Der Fokus bleibt jedoch im linken Navigationsbereich, bis der Benutzer die Tabulatortaste loslässt.

![Die Experience Platform hat die Navigation mit den ausgewählten Quellen verlassen.](images/left-navigation-sources.png)

Einige Funktionen in Platform sind nicht für alle Benutzer aktiviert. Diese Elemente werden in der Navigation angezeigt, können jedoch nicht ausgewählt werden. Beim Navigieren mit einer Tastatur werden diese Elemente während der Pfeilnavigation übersprungen und können nicht mit **Eingabetaste (Return)** ausgewählt werden.

![Abschnitte der linken Navigationsleiste der Experience Platform, die für den Benutzer nicht aktiviert sind, können nicht ausgewählt werden.](images/left-navigation-sections-disabled.png)

## Dialogfeld &quot;Eingebettetes Video&quot;

Videos können in Experience Platform über die Tastaturnavigation angezeigt werden, um einen verfügbaren Videolink hervorzuheben und auszuwählen. Dadurch wird ein eingebettetes Videodialogfeld in der Platform-Benutzeroberfläche geöffnet.

![Ein blauer Rahmen, der um ein ausgewähltes Element herum angezeigt wird und angibt, dass der Fokus angewendet wird.](images/profile-overview-tab.png)

## Tastaturzugriff für das Video-Dialogfeld

Das eingebettete Videodialogfeld kann auch über die Tastatur navigiert werden. In der folgenden Tabelle wird die vollständige Tastaturnavigation beschrieben, die für das eingebettete Videodialogfeld verfügbar ist.

| Dialogelement | Tastaturzugriff | Beschreibung |
|---|---|---|
| Wiedergabe und Pause | Tab<br/>Leertaste | Verwenden Sie **Tab**, um den Fokus auf die Wiedergabeschaltfläche zu legen. **** Leertaste beginnt mit der Videowiedergabe und setzt die Videowiedergabe an. |
| Scrubber | Tab<br/>Linkspfeil<br/>Rechtspfeil | Wenn das Video wiedergegeben wird, verwenden Sie **Tab**, um den Scrubber zu fokussieren. Wenn der Scrubber im Fokus ist, überspringen die **Nach-links- und Nach-rechts-Pfeiltasten** die Videowiedergabe 5 Sekunden lang voraus bzw. zurück. |
| Stummschaltung | Tab<br/>Leertaste | Verwenden Sie **Tab**, um das Lautstärkepegel zu fokussieren. Verwenden Sie **Leertaste**, um die Videowiedergabe zu stummschalten oder zu deaktivieren. |
| Volumen | Tab<br/>Linkspfeil<br/>Rechtspfeil | Verwenden Sie **Tab**, um sich auf das Lautstärkepegel zu konzentrieren. **Nach-links- bzw. Nach-rechts-** Taste wird die Lautstärke nach oben bzw. unten verschoben. |
| [!UICONTROL Geschlossene Untertitel]  (&quot;cc&quot;) | Tab<br/>Enter<br/>Nach-oben-Pfeil<br/>Nach-unten-Pfeil | **** Element &quot; [!UICONTROL Geschlossene Untertitel] &quot;(&quot;cc&quot;). Verwenden Sie **Enter**, um das Menü zu öffnen, und **Nach-oben- und Nach-unten-Pfeiltasten**, um eine Sprache für Beschriftungen auszuwählen. **** Bestätigen Sie Ihre Auswahl. |
| [!UICONTROL Qualität] | Tab<br/>Enter<br/>Nach-oben-Pfeil<br/>Nach-unten-Pfeil | Verwenden Sie **Tab**, um das Element [!UICONTROL Qualität] zu fokussieren. Verwenden Sie **Enter**, um das Menü zu öffnen, und die **Nach-oben- und Nach-unten-Pfeiltasten**, um die Videoqualität auszuwählen. **** Bestätigen Sie Ihre Auswahl. |
| Vollbild | Registerkarte<br/>Leertaste oder Eingabetaste<br/>Escape | Verwenden Sie **Tab**, um das Vollbildelement zu fokussieren. Verwenden Sie **Leertaste oder Enter**, um die Vollbildansicht zu aktivieren. **Escape** (&quot;esc&quot;) beendet den Vollbildmodus. |
| Schließen | Registerkarte<br/>Leertaste oder Eingabetaste | Verwenden Sie **Tab**, um die Schließen-Schaltfläche zu fokussieren. Verwenden Sie die **Leertaste oder die Eingabetaste**-Taste, um das Videodialogfeld zu verlassen. |

>[!NOTE]
>
>Während der Wiedergabe kann jederzeit der Esc-Schlüssel (&quot;esc&quot;) verwendet werden, um das eingebettete Videodialogfeld zu schließen.

![Das eingebettete Videodialogfeld mit Zahlen zur Identifizierung von Tastaturnavigationselementen.](images/video-dialog.png)

## Drag &amp; Drop von Dateien

In Experience Platform können Sie über die Tastatur auf alle Drag &amp; Drop-Bereiche der Dateiauswahl zugreifen. Wenn Sie **Tab** verwenden, um **[!UICONTROL Dateien auswählen]** hervorzuheben, und **Enter oder Leertaste** verwenden, wird die Dateiauswahloberfläche des Betriebssystems aufgerufen.

Nachdem eine Datei hochgeladen wurde, kann über ein Löschsymbol über die Tastatur navigiert werden, um die ausgewählte Datei zu entfernen und eine neue hochzuladen. Benutzer können **Tab** verwenden, um sich auf das Löschsymbol zu konzentrieren, und **Eingabetaste oder Leertaste**, um es auszuwählen. Nachdem die Datei entfernt wurde, ist **[!UICONTROL Dateien auswählen]** automatisch im Fokus und kann ausgewählt werden.

Wenn die hochgeladene Datei nicht das richtige Format aufweist, wird ein Fehlersymbol mit einer Fehlermeldung angezeigt und die Schaltfläche **[!UICONTROL Dateien auswählen]** ist im Fokus und kann ausgewählt werden.

![Eine Drag &amp; Drop-Zone für Dateien mit einer Fehlermeldung und der Schaltfläche Dateien auswählen im Fokus.](images/drag-and-drop.png)

Wenn Sie die Drag &amp; Drop-Zone mit der Maus auswählen, wird auch die Benutzeroberfläche für die Dateiauswahl aufgerufen. Alternativ kann ein Mausbenutzer eine Datei auswählen und auf den Bereich ziehen, um mit dem Upload zu beginnen.

![Ein DateiDrag-and-Drop-Bereich im Fokus, während ein Mausbenutzer eine Datei in den Bereich zieht.](images/drag-and-drop-mouse-over.png)

## Tabellendurchsuchen

Auf alle Tabellen in der Experience Platform-Benutzeroberfläche kann über die Tastatur zugegriffen werden. Das Durchsuchen und Interagieren mit Tabellenzeilen und -spalten ist über eine Reihe von Tastaturbefehlen möglich:

* Verwenden Sie in der Tabellenüberschrift den **Abwärtspfeil**, um die Tabelle zu durchsuchen. Tabellenüberschriften können beim Navigieren über **Tab** ausgewählt werden. Außerdem können Sie die Sortierreihenfolge mit **Leertaste** ändern.
* **Nach-oben- und Nach-unten-** Tasten werden durch die Zeilen in der Tabelle nach oben und unten gerodet.
* Wenn eine Zeile ausgewählt oder im Fokus ist, werden mit **Enter** in der Zeile Details in der rechten Leiste bereitgestellt.
* Wenn eine Zeile ausgewählt oder im Fokus ist, verwenden Sie **Pfeiltasten**, um durch jedes Element in der Zeile zu navigieren.
* Verwenden Sie **Enter**, um ein Element in der Zeile auszuwählen. Benutzer mit Bildschirmlesehilfen werden benachrichtigt, wenn ein neues Fenster geöffnet werden muss.

### Barrierefreiheit der Tabelle durchsuchen

| Tastaturzugriff | Beschreibung |
|---|---|
| HOME (Funktion + Linkspfeil) | Führt Benutzer beim Fokussieren der Zeile zum ersten Element in der Zeile |
| END (Funktion + Pfeil nach rechts) | Wenn die Zeile zentriert ist, gelangen Benutzer zum letzten Element in der Zeile |
| Seite nach oben | Durchsucht zehn Zeilen in der Tabelle (pro Seite) |
| Seite nach unten | Durchläuft 10 Zeilen in der Tabelle (pro Seite) |
| Steuerung + HOME | Wechselt zur ersten Zeile in der Tabelle |
| Steuerung + Ende | Wechselt in Tabelle pro Seite zur ersten Arbeit |

## Benutzeroberfläche des Schema Editors

Die Benutzeroberfläche des Schema-Editors wird durch die folgenden Funktionen zugänglich gemacht:

* Der Schema Editor unterstützt die Tastaturnavigation, einschließlich der Verwendung von **Tab** zur Navigation durch Benutzeroberflächenelemente.
* **** Tabulatoren geben das Suchfeld ein und wechseln dann in die Schemastruktur.
* Die Schemastruktur unterstützt die Verwendung von Pfeiltasten zum Navigieren durch die Benutzeroberfläche der Schemastruktur
   * **Mithilfe von Nach-oben- und Nach-unten-** Pfeilern kann die Baumstruktur durchlaufen werden.
   * **Mit dem linken und rechten** Pfeil können Sie Knoten erweitern und reduzieren oder zwischen Inline-Aktionen in der Schemastruktur wechseln.
* **Enter (Return)** aktiviert die einzelnen Knotendetails im Detailbereich auf der rechten Seite.
* Der Schlüssel **Home** kehrt zum Anfang des Baums zurück.
* Der Schlüssel **End** navigiert zum unteren Ende des Baums.
* Die Schemastruktur enthält auch ARIA-Beschriftungen für Bildschirmlesehilfen.

## Benutzeroberfläche von Segment Builder

Wenn Sie die Segment Builder-Benutzeroberfläche zum Erstellen, Bearbeiten und Interagieren mit Segmenten in Experience Platform verwenden, verbessern die folgenden Funktionen die Barrierefreiheit:

* Auf die Segment Builder-Benutzeroberfläche kann über die Tastaturnavigation zugegriffen werden.
* Bildschirmlesehilfen sollten Markup-Tags für Überschriften erkennen und die Überschrift zusammen mit ihrer Ebene ankündigen.
* Andere Hilfstechnologien können die visuelle Anzeige einer Seite ändern, indem sie ordnungsgemäß kodierte Überschriften verwenden, um einen Umriss oder eine alternative Ansicht anzuzeigen.

## Query Service Editor

Die folgenden Barrierefreiheitsfunktionen sind im Abfragedienst-Editor verfügbar:

* Der Farbkontrast in der Benutzeroberfläche des Abfragedienst-Editors entspricht der Barrierefreiheit.
* Die Tastaturnavigation wird außerhalb der Editor-Benutzeroberfläche unterstützt. Die Editor-Benutzeroberfläche ist ein eingebetteter Code-Mirror.

## Registerkarte &quot;Systemansicht&quot;in &quot;Quellen und Ziele&quot;

Beim Durchsuchen der **[!UICONTROL Systemansicht]** in Quellen und Zielen verbessert die folgende Funktion die Barrierefreiheit:

* **** Tablet-Sets konzentrieren sich auf die erste Quell-Verbindungskarte
   * **** Drücken Sie die Tabulatortaste, um sich auf die Schaltfläche innerhalb der Karte zu konzentrieren.
   * Wählen Sie **Enter** aus, um die Aktionsaufruf-Schaltfläche in der Karte zu aktivieren.
* Wenn Sie auf der Verbindungskarte **Enter** auswählen, werden auch weitere Details in der rechten Leiste aktiviert
   * Wenn die rechte Leiste aktiviert ist, wird der Fokus auf diesen Bereich gesetzt. **** Tabs konzentrieren sich auf  **** Schließen für den rechten Schienenbereich. Wenn Sie **Tab** auswählen, wird der Fokus erneut durch das Bedienfeld in der rechten Leiste bewegt
   * Wenn mehr als eine Quellverbindungskarte vorhanden ist, durchläuft **Tab** die Verbindungen.
   * Verwenden Sie die **Pfeiltasten (oben, unten, links und rechts)**, um durch die Liste der Quellen zu navigieren.
   * Wählen Sie **Tab** aus, um den Fokus auf das Bedienfeld in der rechten Leiste festzulegen.