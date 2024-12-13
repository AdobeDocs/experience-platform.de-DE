---
solution: Experience Platform
title: Handbuch zur Benutzeroberfläche für Edge-Segmentierung
description: Erfahren Sie, wie Sie die Edge-Segmentierung nutzen können, um Segmentdefinitionen in Platform direkt auszuwerten und so Anwendungsfälle für die Personalisierung auf derselben und der nächsten Seite zu ermöglichen.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: e6e9abc7ffe27a2ff9c4ccf4ca243cabdae3d631
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 81%

---

# Handbuch zur Benutzeroberfläche für Edge-Segmentierung

>[!NOTE]
>
>Die Edge-Segmentierung ist jetzt allgemein für alle Benutzenden von Platform verfügbar. Wenn Sie während der Beta-Phase Edge-Segmentdefinitionen erstellt haben, sind diese Segmentdefinitionen weiterhin funktionsfähig.

Bei der Edge-Segmentierung werden Segmente in Adobe Experience Platform sofort [am Edge](../../web-sdk/home.md) ausgewertet, was Anwendungsfälle für die Personalisierung derselben Seite und der nächsten Seite ermöglicht.

>[!IMPORTANT]
>
> Die Edge-Daten werden an dem Edge-Server-Standort gespeichert, der am nächsten zum Erfassungsort liegt. Sie können auch an einem anderen Speicherort als dem als Hub (oder Prinzipal) für das Adobe Experience Platform-Rechenzentrum festgelegten gespeichert werden.
>
> Außerdem wird die Edge-Segmentierungs-Engine nur Edge-Anfragen berücksichtigen, wenn **eine** primär markierte Identität vorhanden ist, was im Einklang mit nicht-Edge-basierten primären Identitäten steht.

## Abfragetypen für Edge-Segmentierungen {#query-types}

Derzeit können nur ausgewählte Abfragetypen mithilfe der Edge-Segmentierung ausgewertet werden. Die folgenden Abschnitte enthalten eine Liste von Abfragetypen, die mit der Edge-Segmentierung ausgewertet werden können und die aktuell nicht unterstützt werden.

Eine Abfrage kann mithilfe der Edge-Segmentierung ausgewertet werden, wenn sie eines der in der folgenden Tabelle aufgeführten Kriterien erfüllt.

>[!NOTE]
>
>Wenn die Abfrage einem der Abfragetypen in der folgenden Tabelle entspricht, wird sie automatisch mithilfe der Edge-Segmentierung ausgewertet. Das System bestimmt diese Fähigkeit automatisch anhand des Abfrageausdrucks.

| Abfragetyp | Details |
| ---------- | ------- |
| Einzelnes Ereignis | Jede Segmentdefinition, die auf ein einzelnes eingehendes Ereignis ohne Zeitbeschränkung verweist. |
| Einzelnes Ereignis innerhalb eines relativen Zeitfensters | Jede Segmentdefinition, die auf ein einzelnes eingehendes Ereignis verweist. |
| Einzelnes Ereignis mit einem Zeitfenster | Jede Segmentdefinition, die auf ein einzelnes eingehendes Ereignis mit einem Zeitfenster verweist. |
| Nur Profil | Jede Segmentdefinition, die nur auf ein Profilattribut verweist. |
| Einzelnes Ereignis mit einem Profilattribut innerhalb eines relativen Zeitfensters von weniger als 24 Stunden | Jede Segmentdefinition, die auf ein einzelnes eingehendes Ereignis mit einem oder mehreren Profilattributen verweist und innerhalb eines relativen Zeitfensters von weniger als 24 Stunden auftritt. |
| Segment von Segmenten | Jede Segmentdefinition, die eine oder mehrere Batch- oder Streaming-Segmentdefinitionen enthält. **Hinweis:** Wenn das Segment von Segmenten mit **Batch**-Segmentdefinitionen verwendet wird, kann es **24 Stunden**, bis eine Profildisqualifizierung erfolgt. Wenn das Segment von Segmenten mit **Streaming**-Segmentdefinitionen verwendet wird, erfolgt die Profildisqualifizierung auf Streaming-Weise. |
| Mehrere Ereignisse mit einem Profilattribut | Jede Segmentdefinition, die **innerhalb der letzten 24 Stunden** auf mehrere Ereignisse verweist und (optional) ein oder mehrere Profilattribute hat. |

Im folgenden Szenario wird eine Segmentdefinition **nicht** für die Edge-Segmentierung aktiviert:

- Die Segmentdefinition umfasst eine Kombination aus einem einzelnen Ereignis und einem `inSegment`-Ereignis.
   - Wenn die im Ereignis `inSegment` enthaltene Segmentdefinition jedoch nur ein Profil ist, **wird** die Segmentdefinition für die Edge-Segmentierung aktiviert.
- Die Segmentdefinition verwendet „Jahr ignorieren“ als Teil ihrer Zeitbeschränkungen.

## Nächste Schritte

In diesem Handbuch wird erläutert, wie Segmentdefinitionen mithilfe der Edge-Segmentierung in Adobe Experience Platform ausgewertet werden. Weitere Informationen zur Verwendung der Experience Platform-Benutzeroberfläche finden Sie im [Benutzerhandbuch zur Segmentierung](./overview.md). Weitere Informationen zum Ausführen ähnlicher Aktionen und zum Arbeiten mit Segmentdefinitionen mithilfe von Experience Platform-APIs finden Sie im [Handbuch zur API für die Edge-Segmentierung](../api/edge-segmentation.md).

## Anhang

Im folgenden Abschnitt finden Sie häufig gestellte Fragen zur Edge-Segmentierung:

### Wie lange dauert es, bis eine Segmentdefinition im Edge Network verfügbar ist?

Es dauert bis zu einer Stunde, bis eine Segmentdefinition im Edge Network verfügbar ist.
