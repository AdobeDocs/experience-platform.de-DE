---
title: Aktualisierung der Segmentierungskriterien
description: Erfahren Sie mehr über die Aktualisierungen der Berechtigungskriterien für die Segmentierung, die sich auf die Arten von Zielgruppen auswirken, die mithilfe von Streaming und Kantensegmentierung bewertet werden können.
hide: true
hidefromtoc: true
source-git-commit: 0bbee2100ed6fdc0f40457965e195d07de6eb2a1
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---


# Aktualisierung der Segmentierungskriterien

Ab dem 24. September 2024 werden zwei Aktualisierungen vorgenommen, die sich auf die Eignung für die Segmentierung auswirken.

1. Abfragetypen für Streaming- und Edge-Segmentierung
2. Zusammenführungsrichtlinien für Streaming- und Edge-Segmentierung

## Abfragetypen

Alle **neuen oder bearbeiteten** Segmentdefinitionen, die den folgenden Abfragetypen entsprechen, werden **nicht mehr** mit Streaming- oder Kantensegmentierung ausgewertet. Stattdessen werden sie mithilfe der Batch-Segmentierung bewertet.

- Ein einzelnes Ereignis mit einem Zeitfenster von mehr als 24 Stunden
   - Aktivieren Sie eine Zielgruppe mit allen Profilen, die in den letzten 3 Tagen eine Webseite angesehen haben.
- Ein einzelnes Ereignis ohne Zeitfenster
   - Aktivieren Sie eine Zielgruppe mit allen Profilen, die eine Webseite angezeigt haben.

Wenn Sie eine Segmentdefinition mithilfe von Streaming oder Kantensegmentierung auswerten müssen, die dem aktualisierten Abfragetyp entspricht, können Sie explizit eine Batch- und Streaming-Abfrage erstellen und diese mithilfe eines Segmentsegments kombinieren.

Wenn Sie beispielsweise eine Zielgruppe mit allen Profilen aktivieren müssen, die in den letzten 3 Tagen eine Webseite mit Streaming-Segmentierung angesehen haben, können Sie die folgenden Abfragen erstellen:

- F1 (Streaming): Alle Profile, die in den letzten 24 Stunden eine Webseite angesehen haben
- F2 (Batch): Alle Profile, die in den letzten 3 Tagen eine Webseite angezeigt haben

Anschließend können Sie sie durch Verweis auf Q1 oder Q2 kombinieren.

Wenn Sie eine Zielgruppe mit allen Profilen aktivieren müssen, die eine Webseite angesehen haben, können Sie die folgenden Abfragen erstellen:

- F3 (Streaming): Alle Profile, die in den letzten 24 Stunden eine Webseite angesehen haben
- F4 (Batch): Alle Profile, die eine Webseite angezeigt haben.

Anschließend können Sie sie durch Verweis auf Q3 oder Q4 kombinieren.

>[!IMPORTANT]
>
>Alle vorhandenen Segmentdefinitionen, die mit den Abfragetypen übereinstimmen, werden mit Streaming oder Kantensegmentierung ausgewertet, bis sie bearbeitet werden.
>
>Darüber hinaus werden alle vorhandenen Segmentdefinitionen, die derzeit die anderen Kriterien zur Bewertung von Streaming- oder Edge-Segmentierung erfüllen, mit Streaming- oder Edge-Segmentierung ausgewertet.

## Zusammenführungsrichtlinie

Alle **neuen oder bearbeiteten** Segmentdefinitionen, die für Streaming- oder Kantensegmentierung **qualifiziert sind, müssen** in der Zusammenführungsrichtlinie &quot;Aktiv in Edge&quot;enthalten sein.

Alle vorhandenen Segmentdefinitionen, die mit Streaming oder Kantensegmentierung ausgewertet werden, funktionieren weiterhin wie bisher.
