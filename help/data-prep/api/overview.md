---
keywords: Experience Platform;Datenvorgabe;Datenvorbereitung API;Fehlerbehebung;API
title: Übersicht über die Datenvorgabe-API
topic-legacy: guide
description: Mit der Datenvorgabe-API können Sie programmgesteuert Zuordnungssätze und -funktionen erstellen, sodass Sie Ihre Daten zwischen Quell- und Ziel-Schemas transformieren können.
exl-id: 740944ae-93ba-4099-a65e-18d6b384c307
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 1%

---

# Handbuch zur Zuordnungs-Dienst-API

Data Prep ermöglicht es Datenentwicklern, Daten dem Experience Data Model (XDM) zuzuordnen, umzuformen und zu validieren. Die Datenvorgabe wird als &quot;Map&quot;-Schritt in den Datenaufnahmemechanismen einschließlich des CSV-Ingestion-Arbeitsablaufs angezeigt.

Die Zuordnungs-Dienst-API, auch als Data Prep-API bezeichnet, enthält mehrere der unten aufgeführten Endpunkte. Weitere Informationen zu erforderlichen Kopfzeilen, zum Lesen von Beispiel-API-Aufrufen und mehr finden Sie in den einzelnen Endpunkthandbüchern.[](./getting-started.md)

## Funktionen

Mit Zuordnungsfunktionen können Sie Ihre Daten zwischen Quell- und Ziel-Schemas transformieren. Sie können den `/languages/el`-Endpunkt verwenden, um Ihre Ausdruck zu validieren und eine Liste aller verfügbaren Zuordnungsfunktionen und -vorgänge zu erhalten.

Detaillierte Informationen zur Verwendung der Zuordnungssatzfunktionen finden Sie im Handbuch [Funktionen.](./functions.md)

## Zuordnungssatz

Zuordnungssätze können verwendet werden, um zu definieren, wie Daten in einem Quell-Schema denen eines Ziel-Schemas zugeordnet werden. Sie können den Endpunkt `/mappingSets` in der Datenvorgabe-API verwenden, um Zuordnungssätze programmgesteuert abzurufen, zu erstellen, zu aktualisieren und zu validieren.

Detaillierte Informationen zur Verwendung von Zuordnungssätzen finden Sie im Handbuch [Endpunkt des Zuordnungssatzes](./mapping-set.md).

## Nächste Schritte

Um mit dem Aufrufen der Zuordnungs-Dienst-API zu beginnen, lesen Sie bitte das Handbuch [Erste Schritte](./getting-started.md) und wählen Sie dann eine der Endpunktrichtlinien, um zu erfahren, wie die spezifischen Endpunkte verwendet werden.
