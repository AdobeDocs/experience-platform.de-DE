---
title: Versionshinweise zur Google-Datenschicht-Erweiterung
description: Die neuesten Versionshinweise für die Google Data Layer Tag-Erweiterung in Adobe Experience Platform.
exl-id: 740b6e3a-d469-475d-9523-03b0b48b11c8
source-git-commit: 0b9fa104777f21fc9bc893784ae3155d887a48d2
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 1%

---

# Versionshinweise zur Google Data Layer-Erweiterung

## Version 1.0.4

* Öffentliche Beta-Version der Erweiterung.

## Version 1.0.6

* Es wurde eine Aktion hinzugefügt, mit der die Datenschicht auf den berechneten Status zurückgesetzt wird.
* Es wurden Fehler im Datenelement behoben, die das Abrufen von Werten aus dem berechneten Status verhinderten.

## Version 1.1.1

Eine wichtige Verbesserung- und Fehlerbehebungsversion, die aus dem Beta-Test-Feedback resultiert.

* Behebung eines Problems, bei dem ein leeres Datenelement der Google-Datenschichterweiterung, das in einer Nicht-Datenschichtregel verwendet wird (z. B. Bibliothek geladen), das Datenschichtobjekt und nicht den berechneten Status zurückgab.
* Behebung eines Problems, bei dem der berechnete Status der Datenschicht nicht vom Helfer in Ereignissen zum Zeitpunkt der Ereignisauslösung, sondern zum Zeitpunkt der Regelausführung übergeben wurde.
* Fügt dem Datenelementdialogfeld einen Umschalter hinzu, mit dem Benutzer auswählen können, ob nur Werte aus Ereignissen zurückgegeben werden sollen.
* Behebung eines Problems, bei dem der Ereignisverlauf nicht korrekt von Regel-Ereignis-Listenern erfasst wurde.
* Geringfügige Verbesserungen der Code-Klarheit.

## Version 1.2.0

* Fügt eine Aktion hinzu, um über ein Multifield-Dialogfeld mit Schlüssel-Wert an die Datenschicht zu pushen.
* Behebung eines Fehlers, durch den das Laden der Erweiterung verhindert wurde, wenn Tags synchron bereitgestellt wurden.
* Behebt einen Fehler, der beim Speichern eines Datenelements unter bestimmten Umständen einen Fehler verursachte.
* Fügt dem Ereignisdialogfeld eine Dokumentation hinzu, in der die Verwendung des Tags-Ereignisobjekts erläutert wird.
* Fügt eine Warnung über endlose Schleifen zum Ereignisdialogfeld hinzu.
