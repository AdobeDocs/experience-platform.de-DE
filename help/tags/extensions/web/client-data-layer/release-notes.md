---
title: Versionshinweise für die Adobe Client-Datenschicht-Erweiterung
description: Die neuesten Versionshinweise für die Adobe Client-Datenschicht-Tag-Erweiterung in Adobe Experience Platform.
source-git-commit: 8dfb7bdc16d0654ee1d76dc5f5af50938b122d33
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 100%

---

# Versionshinweise zur Adobe Client-Datenschicht-Erweiterung

## Version 2.0.2

* Laden der ACDL-Core-Bibliothek (Version 2.0.2)
* In Version 2.0.0 der ACDL-Core-Bibliothek wurde die Möglichkeit zur Nutzung von event.beforeState und event.afterState entfernt. Daher haben wir diese Objekte so geändert, dass immer leere Objekte zurückgegeben werden. Implementierungen, die auf diese Funktionen angewiesen sind, müssen beim Wechsel auf diese Version aktualisiert werden.

## Version 1.1.3

* Laden der ACDL-Core-Bibliothek (Version 1.1.3)

## Version 1.1.2

Die Erweiterung stellt bei der ersten Version die folgenden Funktionen bereit:

* Laden der ACDL-Core-Bibliothek (Version 1.1.1)
* Umbenennen der Adobe-Datenschicht
* Ereignisse:
   * Überwachen aller Ereignisse
   * Überwachen aller gepushten Daten
   * Überwachen eines bestimmten gepushten Ereignisses
   * Alle Ereignisse können in verschiedenen Umfängen überwacht werden
* Datenelemente:
   * Berechneter Status: Globaler oder spezifischer Status
   * Datenschichtgröße
* Aktionen:
   * Zurücksetzen der Datenschichtgröße (unter Beibehaltung des aktuellen berechneten Status)
   * Pushen eines Objekts an die Datenschicht
