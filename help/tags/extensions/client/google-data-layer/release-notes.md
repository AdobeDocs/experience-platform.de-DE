---
title: Versionshinweise zur Google-Datenschicht-Erweiterung
description: Aktuelle Versionshinweise für die Tag-Erweiterung "Google Data Layer“ in Adobe Experience Platform.
exl-id: 740b6e3a-d469-475d-9523-03b0b48b11c8
source-git-commit: c1bad7d5414e62f4d77f7d5903f4b2bf4d9081f8
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 5%

---

# Versionshinweise zur Google-Datenschicht-Erweiterung

## Version 1.0.4

* Öffentliche Beta-Version der Erweiterung.

## Version 1.0.6

* Hinzufügen einer Aktion zum Zurücksetzen der Datenschicht auf den berechneten Status.
* Behebung von Fehlern im Datenelement, die das Abrufen von Werten aus dem berechneten Status verhinderten.

## Version 1.1.1

Eine deutliche Verbesserung und Fehlerbehebung aufgrund des Feedbacks zu Betatests.

* Es wurde ein Problem behoben, bei dem ein leeres Datenschichterweiterungs-Datenelement der Google, das in einer Nicht-Datenschichtregel verwendet wird (z. B. Bibliothek geladen), das Datenschichtobjekt und nicht den berechneten Status zurückgab.
* Es wurde ein Problem behoben, bei dem der berechnete Status der Datenschicht nicht vom Helper in -Ereignissen zum Zeitpunkt der Ereignisauslösung, sondern zum Zeitpunkt der Regelausführung übergeben wurde.
* Fügt einen Umschalter zum Datenelementdialogfeld hinzu, mit dem Benutzende auswählen können, ob nur Werte aus Ereignissen zurückgegeben werden sollen.
* Es wurde ein Problem behoben, bei dem der Ereignisverlauf nicht korrekt von Regelereignis-Listenern erfasst wurde.
* Kleinere Verbesserungen der Code-Klarheit.

## Version 1.2.0

* Fügt eine Aktion hinzu, die mithilfe eines Schlüssel-Wert-Mehrfachfeld-Dialogfelds an die Datenschicht gepusht wird.
* Behebung eines Fehlers, der das Laden der Erweiterung verhinderte, wenn Tags synchron bereitgestellt wurden.
* Behebung eines Fehlers, der unter bestimmten Umständen zum Speichern eines Datenelements führte.
* Fügt dem Ereignisdialogfeld eine Dokumentation hinzu, in der die Verwendung des Tags-Ereignisobjekts erläutert wird.
* Fügt dem Ereignisdialogfeld eine Warnung zu Endlosschleifen hinzu.

## Version 1.2.2

* Fügt Unterstützung für gtag()-Google Analytics hinzu.
