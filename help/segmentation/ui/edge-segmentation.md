---
keywords: Experience Platform; Startseite; beliebte Themen; Kantensegmentierung; Segmentierung; Segmentierungsdienst; Segmentierungsdienst; Benutzerhandbuch; Streaming-Edge;
solution: Experience Platform
title: UI-Anleitung zur Edge-Segmentierung
topic-legacy: ui guide
description: Bei der Edge-Segmentierung können Segmente in Platform sofort am Rand ausgewertet werden, was Anwendungsfälle für die Personalisierung derselben Seite und der nächsten Seite ermöglicht.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: 95ffd09b81b49c8c7d65695a2fbc0fcd97b12c9e
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 1%

---

# Handbuch zur Benutzeroberfläche für Edge-Segmentierung

>[!NOTE]
>
>Die Edge-Segmentierung ist jetzt allgemein für alle Platform-Benutzer verfügbar. Wenn Sie während der Beta-Phase Kantensegmente erstellt haben, sind diese Segmente weiterhin funktionsfähig.

Mit der Edge-Segmentierung können Segmente in Adobe Experience Platform sofort ausgewertet werden. [am Rand](../../edge/home.md), wodurch dieselben Anwendungsfälle für die Personalisierung der Seite und der nächsten Seite aktiviert werden.

>[!IMPORTANT]
>
> Die Edge-Daten werden an einem Edge-Server-Speicherort gespeichert, der am nächsten zum Erfassungsort liegt, und können an einem anderen Speicherort als dem als Hub (oder Prinzipal) für das Adobe Experience Platform-Rechenzentrum bezeichnet werden.
>
> Darüber hinaus berücksichtigt die Edge-Segmentierungsmodul nur Anforderungen an den Edge, an dem **one** mit Primärkennzeichnung versehene Identität, die mit nicht Edge-basierten primären Identitäten konsistent ist.

## Kantensegmentierungs-Abfragetypen

Derzeit können nur ausgewählte Abfragetypen mit Kantensegmentierung ausgewertet werden. Die folgenden Abschnitte enthalten eine Liste von Abfragetypen, die mit der Kantensegmentierung ausgewertet werden können und die derzeit nicht unterstützt werden.

### Unterstützte Abfragetypen {#query-types}

Eine Abfrage kann mit Kantensegmentierung ausgewertet werden, wenn sie eines der in der folgenden Tabelle aufgeführten Kriterien erfüllt.

>[!NOTE]
>
>Wenn die Abfrage mit einem der Abfragetypen in der folgenden Tabelle übereinstimmt, wird sie automatisch mithilfe der Kantensegmentierung ausgewertet. Das System bestimmt diese Fähigkeit automatisch anhand des Abfrageausdrucks.

| Abfragetyp | Details | Beispiel | PQL-Beispiel |
| ---------- | ------- | ------- | ----------- |
| Einzelereignis | Jede Segmentdefinition, die auf ein einzelnes eingehendes Ereignis ohne Zeitbeschränkung verweist. | Personen, die einen Artikel zum Warenkorb hinzugefügt haben. | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart")])` |
| Einzelprofil | Alle Segmentdefinitionen, die auf ein einzelnes Attribut &quot;Nur Profil&quot;verweisen | Menschen, die in den USA leben. | `homeAddress.countryCode = "US"` |
| Einzelereignis, das ein Profil referenziert | Jede Segmentdefinition, die auf ein oder mehrere Profilattribute und ein einzelnes eingehendes Ereignis ohne Zeitbeschränkung verweist. | Personen, die in den USA leben und die Homepage besucht haben. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")])` |
| Negatives einzelnes Ereignis mit einem Profilattribut | Jede Segmentdefinition, die auf ein negatives eingehendes Ereignis und ein oder mehrere Profilattribute verweist. | Menschen, die in den USA leben und **not** besuchte die Homepage. | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")]))` |
| Einzelnes Ereignis innerhalb eines Zeitfensters | Jede Segmentdefinition, die auf ein einzelnes eingehendes Ereignis innerhalb eines bestimmten Zeitraums verweist. | Personen, die die Homepage in den letzten 24 Stunden besucht haben. | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 8 days before now)])` |
| Einzelnes Ereignis mit einem Profilattribut innerhalb eines Zeitfensters | Jede Segmentdefinition, die innerhalb eines bestimmten Zeitraums auf ein oder mehrere Profilattribute und ein einzelnes eingehendes Ereignis verweist. | Personen, die in den USA leben und die die Homepage in den letzten 24 Stunden besucht haben. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 8 days before now)])` |
| Negatives einzelnes Ereignis mit einem Profilattribut innerhalb eines Zeitfensters | Jede Segmentdefinition, die innerhalb eines Zeitraums auf ein oder mehrere Profilattribute und ein negiertes einzelnes eingehendes Ereignis verweist. | Menschen, die in den USA leben und **not** die Homepage in den letzten 24 Stunden besucht haben. | `homeAddress.countryCode = "US" and not(chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 8 days before now)]))` |
| Frequenzereignis innerhalb eines 24-Stunden-Zeitfensters | Jede Segmentdefinition, die auf ein Ereignis verweist, das innerhalb eines Zeitfensters von 24 Stunden eine bestimmte Anzahl von Malen stattfindet. | Besucher der Homepage **mindestens** fünf Mal in den letzten 24 Stunden. | `chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| Häufigkeitsereignis mit einem Profilattribut innerhalb eines 24-Stunden-Zeitfensters | Jede Segmentdefinition, die sich auf ein oder mehrere Profilattribute und ein Ereignis bezieht, die innerhalb eines Zeitfensters von 24 Stunden eine bestimmte Anzahl von Malen stattfinden. | Personen aus den USA, die die Homepage besucht haben **mindestens** fünf Mal in den letzten 24 Stunden. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| Umgekehrtes Frequenzereignis mit einem Profil innerhalb eines Zeitfensters von 24 Stunden | Jede Segmentdefinition, die auf ein oder mehrere Profilattribute und ein negiertes Ereignis verweist, das innerhalb eines Zeitfensters von 24 Stunden eine bestimmte Anzahl von Malen stattfindet. | Personen, die die Homepage nicht besucht haben **more** in den letzten 24 Stunden mehr als fünfmal. | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] ))` |
| Mehrere eingehende Treffer innerhalb eines Zeitprofils von 24 Stunden | Jede Segmentdefinition, die auf mehrere Ereignisse verweist, die innerhalb eines Zeitfensters von 24 Stunden auftreten. | Personen, die die Homepage besucht haben **oder** die Checkout-Seite innerhalb der letzten 24 Stunden besucht haben. | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| Mehrere Ereignisse mit einem Profil innerhalb eines 24-Stunden-Zeitfensters | Jede Segmentdefinition, die auf ein oder mehrere Profilattribute und mehrere Ereignisse verweist, die innerhalb eines Zeitfensters von 24 Stunden auftreten. | Personen aus den USA, die die Homepage besucht haben **und** die Checkout-Seite innerhalb der letzten 24 Stunden besucht haben. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| Segment von Segmenten | Jede Segmentdefinition, die einen oder mehrere Batch- oder Streaming-Segmente enthält. | Personen, die in den USA leben und sich im Segment &quot;vorhandenes Segment&quot;befinden. | `homeAddress.countryCode = "US" and inSegment("existing segment")` |
| Abfrage, die auf eine Zuordnung verweist | Jede Segmentdefinition, die auf eine Zuordnung von Eigenschaften verweist. | Personen, die ihrem Warenkorb auf der Grundlage externer Segmentdaten hinzugefügt haben. | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart") WHERE(externalSegmentMapProperty.values().exists(stringProperty="active"))])` |

## Nächste Schritte

In diesem Handbuch wird erläutert, wie Segmente mit Kantensegmentierung in Adobe Experience Platform ausgewertet werden. Weitere Informationen zur Verwendung der Experience Platform-Benutzeroberfläche finden Sie in der [Benutzerhandbuch zur Segmentierung](./overview.md). Weitere Informationen zum Ausführen ähnlicher Aktionen und zum Arbeiten mit Segmenten mithilfe von Experience Platform-APIs finden Sie unter [Handbuch zur Edge-Segmentierungs-API](../api/edge-segmentation.md).

## Anhang

Im folgenden Abschnitt finden Sie häufig gestellte Fragen zur Kantensegmentierung:

### Wie lange dauert es, bis ein Segment im Edge Network verfügbar ist?

Es dauert bis zu eine Stunde, bis ein Segment im Edge Network verfügbar ist.