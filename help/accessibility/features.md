---
keywords: Experience Platform;Profil;Echtzeit-Kundenprofil;Fehlerbehebung;API;Einheitliches Profil;Einheitliches Profil;Profil;RTCP;XDM-Diagramme
title: Allgemeine Funktionen zur Barrierefreiheit in Platform
type: Documentation
description: Erfahren Sie mehr über die allgemeinen Funktionen zur Barrierefreiheit, die von Adobe Experience Platform unterstützt werden, einschließlich Tastaturnavigation, Farbpaletten und Kontrast sowie Unterstützung durch Hilfstechnologien.
exl-id: 4b7e2f2b-af51-4376-8a63-16c921cc7135
source-git-commit: 7b197f253aa5ce04a682040814cf749407154ebc
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 100%

---

# Funktionen zur Barrierefreiheit in Experience Platform

Adobe Experience Platform möchte allen Personen barrierefreie und inklusive Funktionen bereitstellen, darunter auch Benutzern, die mit Hilfssystemen wie Spracherkennungs-Software und Bildschirmlesehilfen arbeiten. In diesem Dokument werden die allgemeinen Funktionen zur Barrierefreiheit erläutert, die von Platform unterstützt werden, einschließlich Tastaturnavigation, semantischer Struktur, ausreichendem Kontrast zwischen Vordergrund- und Hintergrundelementen und Unterstützung für Hilfstechnologien.

## Hilfstechnologien

Benutzer mit Beeinträchtigungen verlassen sich häufig auf Hardware und Software, sogenannte Hilfstechnologien, um auf digitale Inhalte zuzugreifen und Software-Produkte zu verwenden. Adobe Experience Platform unterstützt verschiedene Arten von Hilfstechnologien wie Bildschirmlesehilfen, Zoom und Spracherkennungs-Software. Hierzu werden die Best Practices für Barrierefreiheit befolgt, beispielsweise die Verwendung von semantischem Code, Textäquivalenten, Beschriftungen und ARIA. Interaktive Elemente in der Benutzeroberfläche von Experience Platform verwenden entsprechende Beschriftungen, barrierefreie Namen und Rollen, die sowohl ihren Zweck als auch ihren aktuellen Status identifizieren. Dadurch wird sichergestellt, dass Hilfstechnologien wie Bildschirmlesehilfen die Beschriftungen und andere Informationen für Benutzer auslesen können, damit diese problemlos mit den Steuerelementen interagieren können.

## Tastaturzugriff

Experience Platform unterstützt die volle Barrierefreiheit der Tastatur.

Die folgenden Navigationselemente erleichtern die Zugänglichkeit:
* Die Tabulatortaste wechselt zwischen Benutzeroberflächenelementen, Abschnitten und Menügruppen.
* Mit den Pfeiltasten kann zwischen Elementen innerhalb von Menügruppen navigiert werden, um den Fokus auf einzelne aktive Elemente zu legen.
* Über die Tastenkombination „Umschalt+Tab“ werden die Registerkarten in umgekehrter Reihenfolge durchlaufen.
* Mit der Eingabetaste und Leertaste werden ausgewählte Elemente aktiviert.
* Die Esc-Taste dient zum Abbrechen und schließt ein vorhandenes Dialogfeld.
* Experience Platform zeigt einen blauen Rahmen um ein ausgewähltes Element an, um klar zu kennzeichnen, welches Element der Benutzeroberfläche derzeit im Fokus ist.

![Ein blauer Rahmen, der zur Kennzeichnung des Fokus um ein ausgewähltes Element angezeigt wird.](images/profile-overview-tab.png)

## Farbpaletten und Kontrast

Experience Platform strebt die Konformität mit [WCAG 2.1 AA](https://www.w3.org/TR/WCAG/) an, einschließlich der Anforderungen an den Farbkontrast. Die Experience Platform-Benutzeroberfläche bietet genügend Kontrast im Programm, um Benutzern mit Sehschwäche oder eingeschränkter farblicher Wahrnehmungsfähigkeit ein barrierefreies Seherlebnis zu bieten.

![Die Farbpalette und der Kontrast auf der Startseite der Experience Platform-Benutzeroberfläche.](images/homepage.png)

## Validierung von erforderlichen Feldern

Beim Hinzufügen von Daten, Erstellen von Schemata oder Definieren von Segmenten werden die erforderlichen Felder sowohl visuell, mit einem Sternchen neben der Textbeschriftung eines Felds, als auch programmatisch angezeigt. Bei diesen Feldern wird bei der Eingabe von ungültigen Daten und beim Speichern eine Validierung ausgelöst. Wenn die Validierung bei einem erforderlichen Feld nicht erfolgreich ist, wird das Feld mit einem Fehlersymbol und in roter Farbe gekennzeichnet. Zusätzlich wird auch eine schriftliche Beschreibung des zu behebenden Problems angezeigt.

![Detailansicht eines erforderlichen Felds, dessen Validierung nicht erfolgreich war. Das Feld erscheint in roter Farbe und ist mit einem Fehlersymbol gekennzeichnet.](images/field-validation.png)
