---
title: Aktualisierung der Segmentierungs-Eignungskriterien
description: Erfahren Sie mehr über die Aktualisierungen der Segmentierungs-Eignungskriterien, die sich auf die Arten von Zielgruppen auswirken, die mithilfe von Streaming und Edge-Segmentierung ausgewertet werden können.
hide: true
hidefromtoc: true
exl-id: c91c0f75-9bc8-4fa7-9d27-9b07d0ea560c
source-git-commit: e6deed1fe52a0a852f521100171323f0de23295b
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---

# Aktualisierung der Segmentierungseignungskriterien

Ab dem 23. Mai 2025 werden zwei Aktualisierungen vorgenommen, die sich auf die Segmentierungseignung auswirken.

1. Abfragetypen für Streaming- und Edge-Segmentierung
2. Zusammenführungsrichtlinien für Streaming und Edge-Segmentierung

## Abfragetypen

Alle **neuen oder bearbeiteten** Segmentdefinitionen, die den folgenden Abfragetypen entsprechen **werden nicht mehr** Streaming- oder Edge-Segmentierung ausgewertet. Stattdessen werden sie mithilfe der Batch-Segmentierung ausgewertet.

- Ein einzelnes Ereignis mit einem Zeitfenster von mehr als 24 Stunden
   - Aktivieren Sie eine Zielgruppe mit allen Profilen, die sich eine Web-Seite in den letzten 3 Tagen angesehen haben.
- Ein einzelnes Ereignis ohne Zeitfenster
   - Aktivieren Sie eine Zielgruppe mit allen Profilen, die eine Web-Seite angesehen haben.

Wenn Sie eine Segmentdefinition mit Streaming- oder Edge-Segmentierung auswerten müssen, die dem aktualisierten Abfragetyp entspricht, können Sie explizit eine Batch- und Streaming-Abfrage erstellen und sie mithilfe von Segmenten kombinieren.

Wenn Sie beispielsweise eine Zielgruppe mit allen Profilen aktivieren müssen, die in den letzten 3 Tagen eine Web-Seite mithilfe der Streaming-Segmentierung aufgerufen haben, können Sie die folgenden Abfragen erstellen:

- Q1 (Streaming): Alle Profile, die sich eine Web-Seite in den letzten 24 Stunden angesehen haben
- Q2 (Batch): Alle Profile, die in den letzten 3 Tagen eine Web-Seite angesehen haben

Sie können sie dann kombinieren, indem Sie sich auf Q1 oder Q2 beziehen.

Wenn Sie eine Zielgruppe mit allen Profilen aktivieren müssen, die eine Web-Seite angesehen haben, können Sie die folgenden Abfragen erstellen:

- Q3 (Streaming): Alle Profile, die sich eine Web-Seite in den letzten 24 Stunden angesehen haben
- Q4 (Batch): Alle Profile, die eine Web-Seite angesehen haben.

Sie können sie dann kombinieren, indem Sie sich auf Q3 oder Q4 beziehen.

>[!IMPORTANT]
>
>Alle vorhandenen Segmentdefinitionen, die mit den Abfragetypen übereinstimmen, bleiben mithilfe von Streaming oder Edge-Segmentierung ausgewertet, bis sie bearbeitet werden.
>
>Darüber hinaus bleiben alle vorhandenen Segmentdefinitionen, die derzeit die anderen Bewertungskriterien für Streaming oder Edge-Segmentierung erfüllen, mit Streaming- oder Edge-Segmentierung bewertet.

## Zusammenführungsrichtlinie

Alle **neuen oder bearbeiteten** Segmentdefinitionen, die für Streaming oder Edge-Segmentierung qualifiziert **müssen** in der Zusammenführungsrichtlinie „Active on Edge&quot; festgelegt sein.

Alle vorhandenen Segmentdefinitionen, die mithilfe von Streaming oder Edge-Segmentierung ausgewertet werden, funktionieren weiterhin wie bisher.
