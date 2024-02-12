---
keywords: Experience Platform;Profil;Echtzeit-Kundenprofil;Fehlerbehebung;API;Einheitliches Profil;Einheitliches Profil;Profil;RTCP;XDM-Diagramme
title: Benutzerdefinierte Barrierefreiheitslösungen für Experience Platform
type: Documentation
description: Erfahren Sie mehr über die benutzerdefinierten Barrierefreiheitslösungen in der Benutzeroberfläche von Adobe Experience Platform.
exl-id: cb5ad99e-8a95-4c9e-aae6-1d0036ecf052
source-git-commit: 2cf28acb5b0ddb4965b2d5120333659e0ac460bf
workflow-type: tm+mt
source-wordcount: '1663'
ht-degree: 92%

---

# Benutzerdefinierte Barrierefreiheitslösungen für Experience Platform

Adobe Experience Platform wird kontinuierlich verbessert, um die Bedürfnisse aller Arten von Benutzern zu erfüllen und die weltweiten Standards einzuhalten, die Einzelanwender mit visuellen, auditiven, Mobilitäts- oder anderen Beeinträchtigungen einschließen. In diesem Dokument werden benutzerdefinierte Barrierefreiheitslösungen innerhalb der Benutzeroberfläche von Experience Platform beschrieben.

## Übersicht über Startseite und Benutzeroberfläche

Die Benutzeroberfläche von Experience Platform erfüllt die erforderlichen Kontrastverhältnisse für Standardtext, Grafiken und Benutzeroberflächenkomponenten. Die Farben der Benutzeroberfläche wurden ebenfalls so ausgewählt, dass sie die Barrierefreiheit für alle Benutzer unterstützen, auch für Benutzer mit visuellen Beeinträchtigungen.

Auf viele Elemente der Benutzeroberfläche von Platform, die mit dem Mauszeiger angeklickt oder bearbeitet werden können, kann auch mit der Tastatur zugegriffen werden. Dazu gehören die linke Navigation, Video-Player, Tabellen und mehr.

Experience Platform strebt die Einhaltung internationaler Barrierefreiheitsstandards an, einschließlich der Web Content Accessibility Guidelines 2.1 Level A und Level AA sowie der Web-Standards der Web Accessibility Initiative – Accessible Rich Internet Applications (WAI-ARIA).

![Die Startseite der Adobe Experience Platform-Benutzeroberfläche.](images/homepage.png)

## Linke Navigation

Die linke Navigation in der Experience Platform-Benutzeroberfläche ist über die Tastatur zugänglich und bietet im normalen, Hover- und Auswahlstatus Farbkontraste, die den Barrierefreiheitsstandards entsprechen.

Vom Startbildschirm aus können Benutzer durch die Tabulatortaste die linke Navigation erreichen. Durch Auswählen von **Umschalt- + Tabulatortaste** wird der Benutzer zum Startbildschirm zurückgeleitet.

![Die linke Navigation.von Experience Platform.](images/left-navigation-select.png)

Wenn die linke Navigation im Fokus ist, bringt die **Tabulatortaste** den Benutzer zur Interaktion mit Erweitern und Reduzieren. Die Möglichkeit zum Erweitern oder Reduzieren der linken Navigation wird mit der **Eingabetaste** aktiviert.

![Die linke Navigation von Experience Platform in reduziertem Zustand.](images/left-navigation-collapse.png)

Wenn der linke Navigationsbereich im Fokus ist, erlauben es die Pfeiltasten nach oben und unten, zu jedem Element in dem Navigationsbereich zu navigieren, wobei ein kontinuierlicher Zyklus durchlaufen wird (mit anderen Worten, der Fokus ändert sich erst, wenn der Benutzer den linken Navigationsbereich verlässt). Der Fokus wird für Navigationselemente angezeigt, wenn diese ausgewählt sind. Die aktuelle Auswahl wird mit hervorgehobenen Text im Fettdruck angezeigt. Bei Auswahl eines Elements des linken Navigationsbereichs wird durch Drücken der **Eingabetaste** das ausgewählte UI-Element im rechten Bereich geöffnet. Der Fokus bleibt jedoch im linken Navigationsbereich, bis der Benutzer mit der Tabulatortaste davon weg navigiert.

![Der linke Navigationsbereich von Experience Platform mit ausgewählten Quellen.](images/left-navigation-sources.png)

Einige Funktionen in Platform sind nicht für alle Benutzer aktiviert. Diese Elemente werden in der Navigation angezeigt, können jedoch nicht ausgewählt werden. Beim Navigieren mit der Tastatur werden diese Elemente während der Pfeiltasten-Navigation übersprungen und können nicht mit der **Eingabetaste** ausgewählt werden.

![Abschnitte des linken Navigationsbereichs von Experience Platform, die für den Benutzer nicht aktiviert sind, können nicht ausgewählt werden.](images/left-navigation-sections-disabled.png)

## Dialogfeld „Eingebettetes Video“

Videos können in Experience Platform über die Tastaturnavigation angezeigt werden, indem ein verfügbarer Video-Link hervorgehoben und ausgewählt wird. Dadurch wird ein eingebettetes Videodialogfeld in der Platform-Benutzeroberfläche geöffnet.

![Ein blauer Rahmen wird um ein ausgewähltes Element herum angezeigt, um anzugeben, dass es sich im Fokus befindet.](images/profile-overview-tab.png)

## Tastaturzugriff für das Videodialogfeld

Die Navigation im eingebetteten Videodialogfeld ist auch über die Tastatur möglich. In der folgenden Tabelle wird die vollständige Tastaturnavigation beschrieben, die für das eingebettete Videodialogfeld verfügbar ist.

| Dialogelement | Tastaturzugriff | Beschreibung |
|---|---|---|
| Wiedergabe und Pause | Tabulatortaste<br/>Leertaste | Verwenden Sie die **Tabulatortaste**, um den Fokus auf die Wiedergabeschaltfläche zu legen. Durch Drücken der **Leertaste** beginnt die Videowiedergabe oder sie wird pausiert. |
| Scrubber | Tabulatortaste<br/>Nach links<br/>Nach rechts | Während das Video wiedergegeben wird, verwenden Sie die **Tabulatortaste**, um den Scrubber zu fokussieren. Wenn der Scrubber im Fokus ist, springt durch Drücken der Tasten **Nach links oder Nach rechts** die Videowiedergabe um 5 Sekunden vorwärts bzw. zurück. |
| Stummschaltung | Tabulatortaste<br/>Leertaste | Verwenden Sie die **Tabulatortaste**, um den Fokus auf das Element „Stummschaltung“ zu setzen. Verwenden Sie die **Leertaste**, um die Stummschaltung für die Videowiedergabe zu aktivieren oder zu deaktivieren. |
| Volumen | Tabulatortaste<br/>Nach links<br/>Nach rechts | Verwenden Sie die **Tabulatortaste**, um den Lautstärkepegel zu steuern. Mit den Tasten **Nach links bzw. Nach rechts** wird die Lautstärke erhöht bzw. verringert. |
| [!UICONTROL Untertitel] | Tabulatortaste<br/>Eingabetaste<br/>Nach oben<br/>Nach unten | **Tabulatortaste** zu [!UICONTROL Untertiteln]. Verwenden Sie die **Eingabetaste**, um das Menü zu öffnen, und die Tasten **Nach oben und Nach unten**, um eine Sprache für Untertitel auszuwählen. Bestätigen Sie Ihre Auswahl mit der **Eingabetaste**. |
| [!UICONTROL Qualität] | Tabulatortaste<br/>Eingabetaste<br/>Nach oben<br/>Nach unten | Verwenden Sie die **Tabulatortaste**, um das Element [!UICONTROL Qualität] in den Fokus zu bringen. Verwenden Sie die **Eingabetaste**, um das Menü zu öffnen, und die Tasten **Nach oben bzw. Nach unten**, um die Videoqualität auszuwählen. Bestätigen Sie Ihre Auswahl mit der **Eingabetaste**. |
| Vollbild | Tabulatortaste<br/>Leertaste oder Eingabetaste<br/>Esc | Verwenden Sie die **Tabulatortaste**, um das Vollbildelement zu fokussieren. Verwenden Sie die **Leertaste oder Eingabetaste**, um die Vollbildansicht zu aktivieren. **Esc** beendet den Vollbildmodus. |
| Schließen | Tabulatortaste<br/>Leertaste oder Eingabetaste | Verwenden Sie die **Tabulatortaste**, um die Schaltfläche „Schließen“ in den Fokus zu bringen. Verwenden Sie die **Leertaste oder Eingabetaste**, um das Videodialogfeld zu verlassen. |

>[!NOTE]
>
>Während der Wiedergabe können Sie jederzeit die Esc-Taste verwenden, um das eingebettete Videodialogfeld zu schließen.

![Das eingebettete Videodialogfeld mit Zahlen zur Identifizierung von Tastaturnavigationselementen.](images/video-dialog.png)

## Drag-and-Drop von Dateien

In Experience Platform können Sie über die Tastatur auf alle Drag-and-Drop-Bereiche der Dateiauswahl zugreifen. Wenn Sie die **Tabulatortaste** verwenden, um **[!UICONTROL Dateien auswählen]** zu markieren, und diese Option über die **Eingabetaste oder Leertaste** auswählen, wird die Dateiauswahloberfläche des Betriebssystems aufgerufen.

Nachdem eine Datei hochgeladen wurde, können Sie über die Tastatur zum Symbol „Löschen“ navigieren, um die ausgewählte Datei zu entfernen und eine neue hochzuladen. Benutzer können über die **Tabulatortaste** zum Symbol „Löschen“ navigieren und diese Option über die **Eingabetaste oder Leertaste** auswählen. Nachdem die Datei entfernt wurde, ist die Option **[!UICONTROL Dateien auswählen]** automatisch im Fokus und kann ausgewählt werden.

Wenn die hochgeladene Datei nicht das richtige Format aufweist, wird ein Fehlersymbol mit einer Fehlermeldung angezeigt und die Schaltfläche **[!UICONTROL Dateien auswählen]** ist im Fokus und kann ausgewählt werden.

![Ein Drag-and-Drop-Bereich für Dateien mit einer Fehlermeldung und Fokus auf der Schaltfläche „Dateien auswählen“.](images/drag-and-drop.png)

Wenn Sie den Drag-and-Drop-Bereich mit der Maus auswählen, wird auch die Benutzeroberfläche für die Dateiauswahl aufgerufen. Alternativ kann ein Mausbenutzer eine Datei auswählen und auf den Bereich ziehen, um mit dem Upload zu beginnen.

![Ein Drag-and-Drop-Bereich für Dateien im Fokus, während ein Mausbenutzer eine Datei in den Bereich zieht.](images/drag-and-drop-mouse-over.png)

## Durchsuchen von Tabellen

Auf alle Tabellen in der Experience Platform-Benutzeroberfläche kann über die Tastatur zugegriffen werden. Das Durchsuchen und Interagieren mit Tabellenzeilen und -spalten ist über eine Reihe von Tastaturbefehlen möglich:

* Verwenden Sie in der Tabellenüberschrift die Taste **Nach unten**, um die Tabelle zu durchsuchen. Tabellenüberschriften können beim Navigieren über die **Tabulatortaste** ausgewählt werden. Außerdem können Sie die Sortierreihenfolge mit der **Leertaste** ändern.
* Mit den Tasten **Nach oben und Nach unten** können Sie nach oben und unten durch die Zeilen navigieren.
* Wenn eine Zeile ausgewählt oder im Fokus ist, können Sie über die **Eingabetaste** in der Zeile Details in der rechten Leiste aufrufen.
* Wenn eine Zeile ausgewählt oder im Fokus ist, verwenden Sie die **Pfeiltasten**, um durch sämtliche Elemente in der Zeile zu navigieren.
* Verwenden Sie die **Eingabetaste**, um ein Element in der Zeile auszuwählen. Benutzer mit Bildschirmlesehilfen werden benachrichtigt, wenn ein neues Fenster geöffnet werden muss.
* Beim Zoomen auf 200 % oder mehr können Sie die **Schieneninspektor** -Symbol, da die rechte Leiste reduziert wird, um mehr Anzeigeraum für die Tabelle bereitzustellen.

![Das Symbol für den Schieneninspektor im Fokus, wenn ein Benutzer auf 200 % zoomt.](images/rail-inspector.png)

### Barrierefreiheit beim Durchsuchen von Tabellen

| Tastaturzugriff | Beschreibung |
|---|---|
| Pos1 (Funktion + Nach links) | Führt den Benutzer, wenn die Zeile den Fokus hat, zum ersten Element in der Zeile |
| Ende (Funktion + Nach rechts) | Führt den Benutzer, wenn die Zeile den Fokus hat, zum letzten Element in der Zeile |
| Bild auf | Geht in der Tabelle zehn Zeilen nach oben (pro Seite) |
| Bild ab | Geht in der Tabelle zehn Zeilen nach unten (pro Seite) |
| Strg+Pos1 | Wechselt zur ersten Zeile in der Tabelle |
| Strg+Ende | Wechselt in der Tabelle zum ersten Wort pro Seite |

## Benutzeroberfläche des Schema-Editors

Die Benutzeroberfläche des Schema-Editors wird durch die folgenden Funktionen zugänglich gemacht:

* Der Schema-Editor unterstützt die Tastaturnavigation, einschließlich der Verwendung der **Tabulatortaste** zum Navigieren durch Benutzeroberflächenelemente.
* Durch Drücken der **Tabulatortaste** wird zum Suchfeld navigiert, dann in die Schemastruktur.
* Die Schemastruktur unterstützt die Verwendung der Pfeiltasten zum Navigieren durch die Benutzeroberfläche der Schemastruktur
   * Mit den Tasten **Nach oben und Nach unten** kann die Schemastruktur durchlaufen werden.
   * Mit den Tasten **Nach links und Nach rechts** können Knoten erweitert und reduziert werden oder es kann zwischen Inline-Aktionen in der Schemastruktur gewechselt werden.
* Die **Eingabetaste** aktiviert die einzelnen Knotendetails im Detailbereich auf der rechten Seite.
* Die Taste **Pos1** kehrt zum Anfang der Struktur zurück.
* Die Taste **Ende** navigiert zum unteren Ende der Struktur.
* Die Schemastruktur enthält auch ARIA-Beschriftungen für Bildschirmlesehilfen.

## Benutzeroberfläche von Segment Builder

Wenn Sie die Benutzeroberfläche von Segment Builder zum Erstellen und Bearbeiten von Segmenten in Experience Platform bzw. zur Interaktion mit diesen verwenden, verbessern die folgenden Funktionen die Barrierefreiheit:

* Auf die Benutzeroberfläche von Segment Builder kann über die Tastaturnavigation zugegriffen werden.
* Bildschirmlesehilfen sollten Markup-Tags für Überschriften erkennen und die Überschrift zusammen mit ihrer Ebene ankündigen.
* Andere Hilfstechnologien können die visuelle Anzeige einer Seite ändern, indem sie ordnungsgemäß codierte Überschriften verwenden, um eine Konturschrift oder eine alternative Ansicht anzuzeigen.

Sie können jetzt die linken und rechten Leisten der Arbeitsfläche des Segmentaufbaus reduzieren oder erweitern, um mehr Platz auf dem Bildschirm zu erhalten. Diese Funktion ist besonders hilfreich, da sie bei 200 % Zoom volle Funktionen bietet.

![Die Arbeitsfläche des Segmentaufbaus mit den Veröffentlichungs-Widgets der linken und rechten Leiste wird hervorgehoben.](images/left-right-rail-expandables.png)

## Abfrage-Service-Editor

Die folgenden Barrierefreiheitsfunktionen sind im Abfrage-Service-Editor verfügbar:

* Der Farbkontrast in der Benutzeroberfläche des Abfrage-Service-Editors entspricht den Regeln der Barrierefreiheit.
* Die Tastaturnavigation wird außerhalb der Editor-Benutzeroberfläche unterstützt. Die Editor-Benutzeroberfläche ist ein eingebetteter Code-Mirror.

>[!NOTE]
>
>Der Abfrage-Editor verarbeitet die **Registerkarte** -Schlüssel standardmäßig aus. Aufrufen **Registerkarte** -Funktion im Editor verwenden, müssen Sie die **Escape** und drücken Sie die **Registerkarte** direkt darauf folgen. Presse **Registerkarte** erneut verwenden, um den Fokus über den Editor hinaus zu verschieben.

## Registerkarte „Systemansicht“ in „Quellen und Ziele“

Beim Durchsuchen der **[!UICONTROL Systemansicht]** in „Quellen und Ziele“ verbessert die folgende Funktion die Barrierefreiheit:

* Drücken der **Tabulatortaste** setzt den Fokus auf die erste Quellverbindungskarte.
   * Drücken Sie die **Tabulatortaste** erneut, um den Fokus auf die Schaltfläche innerhalb der Karte zu setzen.
   * Wählen Sie die **Eingabetaste** aus, um die Aktions-Schaltfläche in der Karte zu aktivieren.
* Wenn Sie auf der Verbindungskarte die **Eingabetaste** auswählen, werden auch weitere Details in der rechten Leiste aktiviert
   * Wenn die rechte Leiste aktiviert ist, wird der Fokus auf diesen Bereich gesetzt. Drücken der **Tabulatortaste** setzt den Fokus auf **Schließen** für den Bereich der rechten Leiste. Wenn Sie die **Tabulatortaste** auswählen, wird der Fokus erneut durch den Bereich der rechten Leiste bewegt
   * Wenn mehr als eine Quellverbindungskarte vorhanden ist, können Sie mit der **Tabulatortaste** durch die Verbindungen navigieren.
   * Verwenden Sie die Tasten **Nach oben, Nach unten, Nach links, Nach rechts**, um durch die Liste der Quellen zu navigieren.
   * Wählen Sie die **Tabulatortaste** aus, um den Fokus auf den Bereich in der rechten Leiste zu legen.
