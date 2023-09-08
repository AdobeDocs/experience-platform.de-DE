---
solution: Experience Platform
title: Handbuch zur Benutzeroberfläche für Edge-Segmentierung
description: Erfahren Sie, wie Sie die Edge-Segmentierung nutzen können, um Segmentdefinitionen in Platform direkt auszuwerten und so Anwendungsfälle für die Personalisierung auf derselben und der nächsten Seite zu ermöglichen.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: ht
source-wordcount: '932'
ht-degree: 100%

---

# Handbuch zur Benutzeroberfläche für Edge-Segmentierung

>[!NOTE]
>
>Die Edge-Segmentierung ist jetzt allgemein für alle Benutzenden von Platform verfügbar. Wenn Sie während der Beta-Phase Edge-Segmentdefinitionen erstellt haben, sind diese Segmentdefinitionen weiterhin funktionsfähig.

Bei der Edge-Segmentierung werden Segmente in Adobe Experience Platform sofort [am Edge](../../edge/home.md) ausgewertet, was Anwendungsfälle für die Personalisierung derselben Seite und der nächsten Seite ermöglicht.

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

| Abfragetyp | Details | Beispiel | PQL-Beispiel |
| ---------- | ------- | ------- | ----------- |
| Einzelnes Ereignis | Jede Segmentdefinition, die auf ein einzelnes eingehendes Ereignis ohne Zeitbeschränkung verweist. | Personen, die einen Artikel zum Warenkorb hinzugefügt haben. | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart")])` |
| Einzelprofil | Alle Segmentdefinitionen, die auf ein einzelnes „Nur-Profil“-Attribut verweisen | Personen, die in den USA leben. | `homeAddress.countryCode = "US"` |
| Einzelereignis, das auf ein Profil verweist | Jede Segmentdefinition, die ohne Zeitbeschränkung auf ein oder mehrere Profilattribute und ein einzelnes eingehendes Ereignis verweist. | Personen, die in den USA leben und die Homepage besucht haben. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")])` |
| Negiertes einzelnes Ereignis mit einem Profilattribut | Jede Segmentdefinition, die auf ein negiertes eingehendes Ereignis und ein oder mehrere Profilattribute verweist. | Personen, die in den USA leben und die Homepage **nicht** besucht haben. | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")]))` |
| Einzelnes Ereignis innerhalb eines Zeitfensters | Jede Segmentdefinition, die auf ein einzelnes eingehendes Ereignis innerhalb eines bestimmten Zeitraums verweist. | Personen, die die Homepage in den letzten 24 Stunden besucht haben. | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 8 days before now)])` |
| Einzelnes Ereignis mit einem Profilattribut innerhalb eines Zeitfensters | Jede Segmentdefinition, die innerhalb eines bestimmten Zeitraums auf ein oder mehrere Profilattribute und ein einzelnes eingehendes Ereignis verweist. | Personen, die in den USA leben und die die Homepage in den letzten 24 Stunden besucht haben. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 8 days before now)])` |
| Negiertes einzelnes Ereignis mit einem Profilattribut innerhalb eines Zeitfensters | Jede Segmentdefinition, die innerhalb eines Zeitraums auf ein oder mehrere Profilattribute und ein negiertes einzelnes eingehendes Ereignis verweist. | Personen, die in den USA leben und die Homepage in den letzten 24 Stunden **nicht** besucht haben. | `homeAddress.countryCode = "US" and not(chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 8 days before now)]))` |
| Häufigkeitsereignis innerhalb eines Zeitfensters von 24 Stunden | Jede Segmentdefinition, die auf ein Ereignis verweist, das innerhalb eines Zeitfensters von 24 Stunden eine bestimmte Anzahl von Malen stattfindet. | Personen, die die Homepage in den letzten 24 Stunden **mindestens** fünf Mal besucht haben. | `chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| Häufigkeitsereignis mit einem Profilattribut innerhalb eines Zeitfensters von 24 Stunden | Jede Segmentdefinition, die auf ein oder mehrere Profilattribute und ein Ereignis verweist, die innerhalb eines Zeitfensters von 24 Stunden eine bestimmte Anzahl von Malen stattfinden. | Personen aus den USA, die die Homepage in den letzten 24 Stunden **mindestens** fünf Mal besucht haben. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| Negiertes Häufigkeitsereignis mit einem Profil innerhalb eines Zeitfensters von 24 Stunden | Jede Segmentdefinition, die auf ein oder mehrere Profilattribute und ein negiertes Ereignis verweist, das innerhalb eines Zeitfensters von 24 Stunden eine bestimmte Anzahl von Malen stattfindet. | Personen, die die Homepage in den letzten 24 Stunden nicht **mehr** als fünf Mal besucht haben. | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] ))` |
| Mehrere eingehende Treffer innerhalb eines Zeitprofils von 24 Stunden | Jede Segmentdefinition, die auf mehrere Ereignisse verweist, die innerhalb eines Zeitfensters von 24 Stunden auftreten. | Personen, die innerhalb der letzten 24 Stunden die Homepage **oder** die Checkout-Seite besucht haben. | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| Mehrere Ereignisse mit einem Profil innerhalb eines 24-Stunden-Zeitfensters | Jede Segmentdefinition, die auf ein oder mehrere Profilattribute und mehrere Ereignisse verweist, die innerhalb eines Zeitfensters von 24 Stunden auftreten. | Personen aus den USA, die innerhalb der letzten 24 Stunden die Homepage **und** die Checkout-Seite besucht haben. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| Segment von Segmenten | Jede Segmentdefinition, die ein oder mehrere Batch- oder Streaming-Segmente enthält. | Personen, die in den USA leben und sich im Segment „vorhandenes Segment“ befinden. | `homeAddress.countryCode = "US" and inSegment("existing segment")` |
| Abfrage, die auf eine Zuordnung verweist | Jede Segmentdefinition, die auf eine Zuordnung von Eigenschaften verweist. | Personen, die ihrem Warenkorb auf der Grundlage externer Segmentdaten Elemente hinzugefügt haben. | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart") WHERE(externalSegmentMapProperty.values().exists(stringProperty="active"))])` |

Im folgenden Szenario wird eine Segmentdefinition **nicht** für die Edge-Segmentierung aktiviert:

- Die Segmentdefinition umfasst eine Kombination aus einem einzelnen Ereignis und einem `inSegment`-Ereignis.
   - Wenn die im Ereignis `inSegment` enthaltene Segmentdefinition jedoch nur ein Profil ist, **wird** die Segmentdefinition für die Edge-Segmentierung aktiviert.

## Nächste Schritte

In diesem Handbuch wird erläutert, wie Segmentdefinitionen mithilfe der Edge-Segmentierung in Adobe Experience Platform ausgewertet werden. Weitere Informationen zur Verwendung der Experience Platform-Benutzeroberfläche finden Sie im [Benutzerhandbuch zur Segmentierung](./overview.md). Weitere Informationen zum Ausführen ähnlicher Aktionen und zum Arbeiten mit Segmentdefinitionen mithilfe von Experience Platform-APIs finden Sie im [Handbuch zur API für die Edge-Segmentierung](../api/edge-segmentation.md).

## Anhang

Im folgenden Abschnitt finden Sie häufig gestellte Fragen zur Edge-Segmentierung:

### Wie lange dauert es, bis eine Segmentdefinition im Edge Network verfügbar ist?

Es dauert bis zu einer Stunde, bis eine Segmentdefinition im Edge Network verfügbar ist.
