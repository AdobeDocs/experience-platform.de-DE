---
title: Anmerkungen
description: Erfahren Sie, wie Sie Tag-Ressourcen in Adobe Experience Platform mit Textanmerkungen versehen können.
exl-id: 14d6b6a1-3bd0-4181-8181-e6b35c197a44
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 100%

---

# Anmerkungen

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Anmerkungen sind Kommentare in Textform, die Sie bestimmten Tag-Ressourcen in Adobe Experience Platform hinzufügen können. Die folgenden Ressourcen können mit Anmerkungen versehen werden:

* Erweiterungen
* Datenelemente
* Regeln
* Regel Komponenten
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

Wählen Sie **[!UICONTROL Anmerkungen]** aus, um die rechte Leiste zu erweitern und die Anmerkungen anzuzeigen, wobei die neuesten Anmerkungen oben stehen. Um eine neue Anmerkung hinzuzufügen, geben Sie deren Text in das Feld oben ein und klicken Sie auf **[!UICONTROL Anmerkung hinzufügen]**.

## Sonstiges

* Anmerkungen in Tag-Ressourcen entsprechen dem Verhalten von Anmerkungen in DTM. Sie sind nicht veränderlich und können nicht bearbeitet oder gelöscht werden.
* Bei der Anzeige älterer Revisionen einer Ressource werden nur die Anmerkungen angezeigt, die vor dem `created_at` Datum der Revision erstellt wurden.
* Wenn Sie eine Ressource löschen, werden auch alle mit der Ressource verknüpften Anmerkungen gelöscht.
