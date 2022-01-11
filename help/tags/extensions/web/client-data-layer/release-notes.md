---
title: Versionshinweise für die Adobe Client-Datenschicht-Erweiterung
description: Aktuelle Versionshinweise für die Tag-Erweiterung „Adobe Client Data Layer“ in Adobe Experience Platform.
exl-id: 8fa3a210-6c85-4162-84cf-15c6e3cfcb9e
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: ht
source-wordcount: '164'
ht-degree: 100%

---

# Versionshinweise zur Erweiterung „Adobe Client Data Layer“

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
   * Berechneter Status: globaler oder spezifischer Status
   * Datenschichtgröße
* Aktionen:
   * Zurücksetzen der Datenschichtgröße (unter Beibehaltung des aktuellen berechneten Status)
   * Pushen eines Objekts an die Datenschicht
