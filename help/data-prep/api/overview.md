---
keywords: Experience Platform;Datenvorbereitung;Datenvorbereitungs-API;Fehlerbehebung;API
title: Datenvorbereitungs-API – Übersicht
description: Mit der Datenvorbereitungs-API können Sie programmatisch Zuordnungssätze und -funktionen erstellen, um Ihre Daten zwischen Quell- und Zielschemas zu konvertieren.
exl-id: 740944ae-93ba-4099-a65e-18d6b384c307
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 100%

---

# Handbuch zur Mapping Service-API

Die Datenvorbereitung ermöglicht es Dateningenieuren, Daten dem Experience-Datenmodell (XDM) zuzuordnen, umzuformen und zu validieren. Die Datenvorbereitung wird als „Map“-Schritt in den Datenaufnahmemechanismen, einschließlich des Workflows der CSV-Aufnahme, angezeigt.

Die Mapping Service-API, auch als Datenvorbereitungs-API bezeichnet, enthält verschiedene unten beschriebene Endpunkte. Weitere Informationen zu erforderlichen Kopfzeilen, zum Lesen von Beispiel-API-Aufrufen und mehr finden Sie in den einzelnen Endpunkthandbüchern sowie in den [Ersten Schritten](./getting-started.md).

## Funktionen

Mit Zuordnungssatzfunktionen können Sie Ihre Daten zwischen Quell- und Zielschemas konvertieren. Sie können den `/languages/el`-Endpunkt verwenden, um Ihre Ausdrücke zu validieren und eine Liste aller verfügbaren Zuordnungssatzfunktionen und -vorgänge abzurufen.

Ausführliche Informationen zur Verwendung von Zuordnungssatzfunktionen finden Sie im [Endpunkthandbuch zu Funktionen](./functions.md).

## Zuordnungssatz

Mit Zuordnungssätzen lässt sich definieren, wie Daten in einem Quellschema den Daten eines Zielschemas zugeordnet werden. Sie können den `/mappingSets`-Endpunkt in der Datenvorbereitungs-API verwenden, um Zuordnungssätze programmgesteuert abzurufen, zu erstellen, zu aktualisieren und zu validieren.

Ausführliche Informationen zur Verwendung von Zuordnungssätzen finden Sie im [Endpunkhandbuch zu Zuordnungssätzen](./mapping-set.md).

## Nächste Schritte

Um mit Aufrufen mit der Mapping Service-API zu beginnen, lesen Sie das Handbuch [Erste Schritte](./getting-started.md) und wählen Sie dann eins der Endpunkthandbücher aus, um zu erfahren, wie bestimmte Endpunkte verwendet werden.
