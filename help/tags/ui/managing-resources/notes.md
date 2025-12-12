---
title: Anmerkungen
description: Erfahren Sie, wie Sie Tag-Ressourcen in Adobe Experience Platform mit Textanmerkungen versehen können.
exl-id: 14d6b6a1-3bd0-4181-8181-e6b35c197a44
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 99%

---

# Anmerkungen

Anmerkungen sind Kommentare in Textform, die Sie bestimmten Tag-Ressourcen in Adobe Experience Platform hinzufügen können. Die folgenden Ressourcen können mit Anmerkungen versehen werden:

* Erweiterungen
* Datenelemente
* Regeln
* Regelkomponenten
* Bibliotheken
* Eigenschaften

Anmerkungen können bis zu 512 Unicode-Zeichen enthalten.

Anmerkungen sind Kommentare, die sich nicht auf das Verhalten der Ressourcen auswirken, denen sie hinzugefügt werden. Sie sind nicht in benutzerdefinierten Bibliotheken enthalten. Anmerkungen können für folgende Zwecke verwendet werden:

* Hintergrundinformationen zu einer Ressource bereitstellen
* Aufgabenliste für künftige Verbesserungen
* Weiterleiten von Ratschlägen zur Ressourcenverwendung an andere Benutzer
* Anweisungen an andere Team-Mitglieder weitergeben
* Verlaufskontext aufzeichnen
* Zur Erinnerung daran, was eine Ressource tut, warum sie so aufgebaut ist oder wo sie genutzt wird

## Anmerkungen erstellen

Ressourcen, in denen Anweisungen erstellt werden können, weisen eine schmale Leiste auf der rechten Bildschirmseite auf. Diese Leiste enthält ein Symbol für Anmerkungen. Auf diesem Symbol ist die aktuelle Anzahl der Anmerkungen zu sehen, die mit der Ressource verknüpft sind.

Wählen Sie **[!UICONTROL Notes]** aus, um die rechte Leiste mit den Anmerkungen einzublenden. (Die neuesten Anmerkungen sind darin als erste aufgeführt.)  Um eine neue Anmerkung hinzuzufügen, geben Sie deren Text in das Feld oben ein und klicken Sie auf **[!UICONTROL Add Note]**.

## Sonstiges

* Anmerkungen in Tag-Ressourcen entsprechen dem Verhalten von Anmerkungen in DTM. Sie sind nicht veränderlich und können nicht bearbeitet oder gelöscht werden.
* Bei der Anzeige älterer Revisionen einer Ressource werden nur die Anmerkungen angezeigt, die vor dem `created_at` Datum der Revision erstellt wurden.
* Wenn Sie eine Ressource löschen, werden auch alle mit der Ressource verknüpften Anmerkungen gelöscht.
