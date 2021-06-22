---
keywords: Experience Platform;Profil;Echtzeit-Kundenprofil;Fehlerbehebung;API;Einheitliches Profil;Einheitliches Profil;Profil;RTCP;XDM-Diagramme
title: Allgemeine Funktionen zur Barrierefreiheit in Platform
topic: Handbuch
type: Documentation
description: Erfahren Sie mehr über die allgemeinen Barrierefreiheitsfunktionen, die von Adobe Experience Platform unterstützt werden, einschließlich Tastaturnavigation, Farbpaletten und Kontrast sowie Unterstützung durch Hilfstechnologien.
source-git-commit: 81db01c3e8d332e1fc8127d779c3a584bb498858
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 7%

---


# Barrierefreiheitsfunktionen in Experience Platform

Adobe Experience Platform möchte allen Personen barrierefreie und inklusive Funktionen bereitstellen, darunter auch Benutzern, die mit Hilfssystemen wie Spracherkennungssoftware und Bildschirmlesehilfen arbeiten. In diesem Dokument werden die allgemeinen Barrierefreiheitsfunktionen erläutert, die von Platform unterstützt werden, einschließlich Tastaturnavigation, semantische Struktur, ausreichender Kontrast zwischen Vordergrund- und Hintergrundelementen und Unterstützung für Hilfstechnologien.

## Hilfstechnologien

Benutzer mit Behinderungen verlassen sich häufig auf Hardware und Software, so genannte Hilfstechnologien, um auf digitale Inhalte zuzugreifen und Softwareprodukte zu verwenden. Adobe Experience Platform unterstützt verschiedene Arten von Hilfstechnologien (AT) wie Bildschirmlesehilfen, Zoom- und Spracherkennungssoftware. Befolgen Sie dazu die Best Practices für Barrierefreiheit, wie z. B. die Verwendung von semantischem Code, Textäquivalenten, Beschriftungen und ARIA. Interaktive Elemente in der Benutzeroberfläche der Experience Platform verwenden entsprechende Beschriftungen, barrierefreie Namen und Rollen, die sowohl ihren Zweck als auch ihren aktuellen Status identifizieren. Dadurch wird sichergestellt, dass Hilfstechnologien wie Bildschirmlesehilfen die Beschriftungen und andere Informationen für Benutzer auslesen können, damit sie problemlos mit den Anwendungssteuerelementen interagieren können.

## Tastaturzugriff

Experience Platform unterstützt die volle Barrierefreiheit der Tastatur.

Die folgenden Navigationselemente erleichtern die Zugänglichkeit:
* Die Tabulatortaste wechselt zwischen Benutzeroberflächenelementen, Abschnitten und Menügruppen.
* Pfeiltasten werden innerhalb von Menügruppen verschoben, um den Fokus auf einzelne aktive Elemente zu legen.
* Umschalt + Tab bewegt sich durch die Tab-Reihenfolge zurück.
* Die Tasten Rückgabe (Eingabetaste) und Leertaste aktivieren ausgewählte Elemente.
* Die Escape-Taste (ESC) dient als Abbrechen-Schaltfläche, um ein Dialogfeld zu schließen, wenn vorhanden.
* Experience Platform zeigt einen blauen Rahmen um ein ausgewähltes Element an, um einen klaren Hinweis darauf anzuzeigen, welches UI-Element derzeit den Fokus hat.

![Ein blauer Rahmen, der um ein ausgewähltes Element herum angezeigt wird und angibt, dass der Fokus angewendet wird.](images/profile-overview-tab.png)

## Farbpaletten und Kontrast

Experience Platform strebt die Konformität mit [WCAG 2.1 AA](https://www.w3.org/TR/WCAG/) an, einschließlich Anforderungen an den Farbkontrast. Die Experience Platform-Benutzeroberfläche bietet genügend Kontrast in der Anwendung, um Benutzern mit Sehschwäche oder Farbmangel ein barrierefreies Seherlebnis zu bieten.

![Die Farbpalette und der Kontrast, die auf der Startseite der Experience Platform-Benutzeroberfläche vorhanden sind.](images/homepage.png)

## Erforderliche Feldüberprüfung

Beim Hinzufügen von Daten, Erstellen von Schemata oder Definieren von Segmenten werden die erforderlichen Felder sowohl visuell, mit einem Sternchen neben der Textbeschriftung eines Felds als auch programmatisch angezeigt. Diese Felder werden bei der Eingabe von ungültigen Daten in die Trigger und beim Speichern geprüft. Wenn ein erforderliches Feld die Validierung nicht besteht, wird es rot mit einem Fehlersymbol gekennzeichnet und es wird auch eine schriftliche Beschreibung des zu behebenden Problems angezeigt.

![Schließen eines erforderlichen Felds, das die Validierung nicht bestanden hat. Das Feld wird rot angezeigt und ein Fehlersymbol wird angezeigt.](images/field-validation.png)