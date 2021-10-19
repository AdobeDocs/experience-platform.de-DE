---
keywords: Experience Platform;Home;beliebte Themen;Kantensegmentierung;Segmentierung;Segmentierungsdienst;Segmentierungsdienst;i-Leitfaden;Streaming-Kante;
solution: Experience Platform
title: Edge Segmentation UI Guide
topic-legacy: ui guide
description: Mit der Edge-Segmentierung können Segmente in der Plattform unmittelbar am Rand ausgewertet werden, sodass dieselben Anwendungsfälle für die Personalisierung der Seite und der nächsten Seite aktiviert werden.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: c89971668839555347e9b84c7c0a4ff54a394c1a
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 2%

---

# Edge Segmentation UI guide (Beta)

>[!IMPORTANT]
>
>Die Kantensegmentierung befindet sich derzeit in der Beta-Phase. Die Dokumentation und Funktionalität können sich ändern.

Mit der Edge-Segmentierung können Segmente in Adobe Experience Platform sofort ausgewertet werden. [am Rand](../../edge/home.md), die die gleiche Personalisierung der Seite und der nächsten Seite ermöglicht.

## Abfrage der Kantensegmentierung

Zurzeit können nur ausgewählte Abfragen mit Kantensegmentierung bewertet werden. Die folgenden Abschnitte enthalten eine Liste der Abfragen, die mit der Kantensegmentierung und den derzeit nicht unterstützten Typen bewertet werden können.

### Unterstützte Abfragen

Eine Abfrage kann mit Kantensegmentierung bewertet werden, wenn sie eines der in der folgenden Tabelle aufgeführten Kriterien erfüllt.

>[!NOTE]
>
>Wenn die Abfrage mit einem der in der folgenden Tabelle aufgeführten Typen von Abfragen übereinstimmt, wird sie automatisch mithilfe der Kantensegmentierung bewertet. Das System bestimmt diese Funktion automatisch anhand des Ausdrucks der Abfrage.

| Abfragetyp | Details | Beispiel |
| ---------- | ------- | ------- |
| Einzelnes Ereignis | Eine Segmentdefinition, die sich auf ein einzelnes eingehendes Ereignis ohne Zeitbeschränkung bezieht. | Personen, die dem Warenkorb ein Artikel hinzugefügt haben. |
| Einzelnes Ereignis, das sich auf ein Profil bezieht | Eine Segmentdefinition, die sich auf ein oder mehrere Profil-Attribute und ein einzelnes ankommendes Ereignis ohne Zeitbeschränkung bezieht. | Personen, die in den USA leben und die Homepage besucht haben. |
| Negatives einzelnes Ereignis mit einem Profil-Attribut | Eine Segmentdefinition, die sich auf ein negatives eintreffendes Ereignis und ein oder mehrere Profil-Attribute bezieht | Menschen, die in den USA leben und **nicht** besuchte die Homepage. |
| Einzelnes Ereignis innerhalb eines 24-Stunden-Fensters | Eine Segmentdefinition, die sich auf ein einzelnes ankommendes Ereignis innerhalb von 24 Stunden bezieht. | Personen, die die Homepage in den letzten 24 Stunden besucht haben. |
| Einzelnes Ereignis mit einem Profil-Attribut und einem 24-Stunden-Zeitfenster | Eine Segmentdefinition, die sich auf ein oder mehrere Profil-Attribute und ein negiertes einzelnes ankommendes Ereignis innerhalb von 24 Stunden bezieht. | Personen, die in den USA leben und die Homepage in den letzten 24 Stunden besucht haben. |
| Negiertes einzelnes Ereignis mit einem Profil-Attribut innerhalb eines 24-Stunden-Fensters | Eine Segmentdefinition, die sich auf ein oder mehrere Profil-Attribute und ein negiertes einzelnes ankommendes Ereignis innerhalb von 24 Stunden bezieht. | Menschen, die in den USA leben und **nicht** besuchte die Homepage in den letzten 24 Stunden. |
| Häufigkeitsangaben innerhalb eines 24-Stunden-Ereignisses | Eine Segmentdefinition, die sich auf ein Ereignis bezieht, das innerhalb eines Zeitfensters von 24 Stunden eine bestimmte Anzahl von Ereignissen aufweist. | Personen, die die Homepage besucht haben **mindestens** fünf Mal in den letzten 24 Stunden. |
| Ereignis der Häufigkeit mit einem Profil-Attribut innerhalb eines 24-Stunden-Fensters | Eine Segmentdefinition, die sich auf ein oder mehrere Profil-Attribute bezieht und ein Ereignis, das innerhalb eines Zeitfensters von 24 Stunden eine bestimmte Anzahl von Ereignissen aufnimmt. | Personen aus den USA, die die Homepage besucht haben **mindestens** fünf Mal in den letzten 24 Stunden. |
| Negatives Frequenzfenster mit einem Profil innerhalb eines 24-Stunden-Ereignisses | Eine Segmentdefinition, die sich auf ein oder mehrere Profil-Attribute und ein negiertes Ereignis bezieht, das innerhalb eines Zeitfensters von 24 Stunden eine bestimmte Anzahl von Ereignissen aufnimmt. | Personen, die die Startseite nicht besucht haben **mehr** in den letzten 24 Stunden mehr als fünf Mal. |
| Mehrere eingehende Treffer innerhalb eines Profils von 24 Stunden | Eine Segmentdefinition, die sich auf mehrere Ereignis bezieht, die innerhalb eines Zeitfensters von 24 Stunden auftreten. | Personen, die die Homepage besucht haben **oder** hat die Checkout-Seite innerhalb der letzten 24 Stunden besucht. |
| Mehrere Ereignisse mit einem Profil innerhalb eines 24-Stunden-Fensters | Eine Segmentdefinition, die sich auf ein oder mehrere Profil-Attribute und mehrere Ereignis bezieht, die innerhalb eines Zeitfensters von 24 Stunden auftreten. | Personen aus den USA, die die Homepage besucht haben **und** hat die Checkout-Seite innerhalb der letzten 24 Stunden besucht. |

## Nächste Schritte

In diesem Handbuch wird erläutert, wie Segmente mit der Segmentierung von Kanten auf Adobe Experience Platform bewertet werden. Weitere Informationen zur Verwendung der Experience Platform-Benutzeroberfläche finden Sie in der [Benutzerhandbuch für Segmentierung](./overview.md). Weitere Informationen zum Ausführen ähnlicher Aktionen und zum Arbeiten mit Segmenten mithilfe von Experience Platform-APIs finden Sie unter [Handbuch zur Edge-Segmentierungs-API](../api/edge-segmentation.md).
