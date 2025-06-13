---
title: Aktualisierung der Segmentierungs-Eignungskriterien
description: Erfahren Sie mehr über die Aktualisierungen der Segmentierungs-Eignungskriterien, die sich auf die Arten von Zielgruppen auswirken, die mithilfe von Streaming und Edge-Segmentierung ausgewertet werden können.
hide: true
hidefromtoc: true
exl-id: c91c0f75-9bc8-4fa7-9d27-9b07d0ea560c
source-git-commit: 6935cee30adb59d52db6c6fed7036f81b54edd52
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 4%

---

# Aktualisierung der Segmentierungseignungskriterien

>[!IMPORTANT]
>
>Alle vorhandenen Segmentdefinitionen, die derzeit mithilfe von Streaming oder Edge-Segmentierung ausgewertet werden, funktionieren weiterhin wie bisher, es sei denn, sie werden bearbeitet oder aktualisiert.

Ab dem 20. Mai 2025 werden drei Aktualisierungen vorgenommen, die sich auf die Segmentierungseignung auswirken.

1. Berechtigter Regelsatz
2. Zeitfenster-Eignung
3. Einschließen von Batch-Daten in Streaming-Zielgruppen
4. Aktive Zusammenführungsrichtlinien

## Regelsatz {#ruleset}

Alle **neuen oder bearbeiteten** Segmentdefinitionen, die den folgenden Regelsätzen entsprechen **werden nicht mehr** Streaming- oder Edge-Segmentierung ausgewertet. Stattdessen werden sie mithilfe der Batch-Segmentierung ausgewertet.

- Ein einzelnes Ereignis mit einem Zeitfenster von mehr als 24 Stunden
   - Aktivieren Sie eine Zielgruppe mit allen Profilen, die sich eine Web-Seite in den letzten 3 Tagen angesehen haben.
- Ein einzelnes Ereignis ohne Zeitfenster
   - Aktivieren Sie eine Zielgruppe mit allen Profilen, die eine Web-Seite angesehen haben.

## Zeitfenster {#time-window}

Um eine Zielgruppe mit Streaming-Segmentierung auszuwerten **muss sie** einem Zeitfenster von 24 Stunden eingeschränkt sein.

## Einschließen von Batch-Daten in Streaming-Zielgruppen {#include-batch-data}

Vor diesem Update konnten Sie eine Definition für Streaming-Zielgruppen erstellen, die sowohl Batch- als auch Streaming-Datenquellen kombinierte. Mit der neuesten Aktualisierung wird jedoch die Erstellung einer Zielgruppe mit sowohl Batch- als auch Streaming-Datenquellen mithilfe der Batch-Segmentierung ausgewertet.

Wenn Sie eine Segmentdefinition mit Streaming- oder Edge-Segmentierung auswerten müssen, die dem aktualisierten Regelsatz entspricht, müssen Sie explizit einen Batch und einen Streaming-Regelsatz erstellen und sie mithilfe von Segmenten kombinieren. Dieser Batch **Regelsatz** auf einem Profilschema basieren.

Angenommen, Sie haben zwei Zielgruppen, von denen eine die Profilschemadaten und die andere die Ereignisschemadaten enthält:

| Zielgruppe | Schema | Typ der Quelle | Query definition | Zielgruppen-ID |
| -------- | ------ | ----------- | ---------------- | ----------- |
| Einwohner Kaliforniens | Profil | Batch-Quelle | Wohnsitz ist in the state of California | `e3be6d7f-1727-401f-a41e-c296b45f607a` |
| Letzte Kassengänge | Erlebnisereignis | Streaming-Quelle | Hat mindestens einen Checkout in den letzten 24 Stunden | `9e1646bb-57ff-4309-ba59-17d6c5bab6a1` |

Wenn Sie die Batch-Komponente in Ihrer Streaming-Zielgruppe verwenden möchten, müssen Sie einen Verweis auf die Batch-Zielgruppe anhand des Segments von Segmenten erstellen.

Ein Beispielregelsatz, der die beiden Zielgruppen kombiniert, würde also wie folgt aussehen:

```
inSegment("e3be6d7f-1727-401f-a41e-c296b45f607a") and 
CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("commerce.checkouts", false)) 
WHEN(<= 24 hours before now)])
```

Die resultierende Zielgruppe *wird* mithilfe der Streaming-Segmentierung ausgewertet, da sie die Zugehörigkeit der Batch-Zielgruppe durch Verweis auf die Komponente für die Batch-Zielgruppe nutzt.

Wenn Sie jedoch zwei Zielgruppen mit Ereignisdaten kombinieren möchten, **Sie die beiden Ereignisse nicht** kombinieren. Sie müssen beide Zielgruppen erstellen und dann eine weitere Zielgruppe erstellen, die `inSegment` verwendet, um auf diese beiden Zielgruppen zu verweisen.

Angenommen, Sie haben zwei Zielgruppen, wobei beide Zielgruppen Erlebnisereignis-Schemadaten enthalten:

| Zielgruppe | Schema | Typ der Quelle | Query definition | Zielgruppen-ID |
| -------- | ------ | ----------- | ---------------- | ----------- |
| Letzte Abbrüche | Erlebnisereignis | Batch-Quelle | Hat mindestens ein Abbruchereignis in den letzten 48 Stunden | `7deb246a-49b4-4687-95f9-6316df049948` |
| Letzte Kassengänge | Erlebnisereignis | Streaming-Quelle | Hat mindestens einen Checkout in den letzten 24 Stunden | `9e1646bb-57ff-4309-ba59-17d6c5bab6a1` |

In diesem Fall müssten Sie wie folgt eine dritte Zielgruppe erstellen:

```
inSegment("7deb246a-49b4-4687-95f9-6316df049948") and inSegment("9e1646bb-57ff-4309-ba59-17d6c5bab6a1")
```

>[!IMPORTANT]
>
>Alle vorhandenen Segmentdefinitionen, die mit den Regelsätzen übereinstimmen, bleiben mithilfe von Streaming oder Edge-Segmentierung ausgewertet, bis sie bearbeitet werden.
>
>Darüber hinaus bleiben alle vorhandenen Segmentdefinitionen, die derzeit die anderen Bewertungskriterien für Streaming oder Edge-Segmentierung erfüllen, mit Streaming- oder Edge-Segmentierung bewertet.

## Zusammenführungsrichtlinie {#merge-policy}

Alle **neuen oder bearbeiteten** Segmentdefinitionen, die für Streaming oder Edge-Segmentierung qualifiziert **müssen** in der Zusammenführungsrichtlinie „Active on Edge&quot; festgelegt sein.

Wenn kein aktiver Zusammenführungsrichtliniensatz festgelegt ist, müssen Sie [Zusammenführungsrichtlinie konfigurieren](../profile/merge-policies/ui-guide.md#configure) und sie so einstellen, dass sie im Randbereich aktiv ist.
