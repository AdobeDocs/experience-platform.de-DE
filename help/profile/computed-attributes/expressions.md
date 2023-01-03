---
keywords: Experience Platform; Profil; Echtzeit-Kundenprofil; Fehlerbehebung; API
title: Beispiel-PQL-Ausdrücke für berechnete Attribute
topic-legacy: guide
type: Documentation
description: Berechnete Attribute sind Funktionen, mit denen Daten auf Ereignisebene in Attribute auf Profilebene aggregiert werden. Diese Funktionen erfordern die Verwendung gültiger PQL-Ausdrücke (Profile Query Language). In diesem Handbuch werden einige der am häufigsten verwendeten PQL-Ausdrücke für berechnete Attribute vorgestellt.
exl-id: 7c80e2d3-919a-47f9-a59f-833a70f02a8f
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 4%

---

# (Alpha) Beispiel-PQL-Ausdrücke für berechnete Attribute

>[!IMPORTANT]
>
>Die Funktion für berechnete Attribute ist derzeit alphanumerisch und steht nicht allen Benutzern zur Verfügung. Dokumentation und Funktionalitäten können sich ändern.

In Adobe Experience Platform sind berechnete Attribute Funktionen zum Aggregieren von Daten auf Ereignisebene in Profilattributen. Diese Funktionen werden automatisch berechnet, sodass sie für die Segmentierung, Aktivierung und Personalisierung verwendet werden können. Jedes berechnete Attribut wird mit grundlegenden Informationen wie einem Namen und einer Beschreibung, der Schemaklasse und dem Pfad zum Feld, in dem der Wert gespeichert werden soll, sowie einem Ausdruck definiert, dessen berechneter Wert dem Wert entspricht, den Sie im berechneten Attribut speichern möchten.

Die in berechneten Attributen verwendeten Ausdrücke werden mithilfe von [!DNL Profile Query Language] (PQL), eine Experience-Datenmodell (XDM)-konforme Abfragesprache, die die Definition und Ausführung von Abfragen für Echtzeit-Kundenprofildaten unterstützt.

Berechnete Attribute unterstützen derzeit die folgenden Funktionen: sum, count, min, max, and boolean. In diesem Handbuch werden einige der am häufigsten verwendeten PQL-Ausdrücke vorgestellt, die Sie beim Definieren Ihrer eigenen berechneten Attribute für Ihr Unternehmen verwenden können. Weitere Informationen zu PQL und Links zu zusätzlichen Formatierungsrichtlinien und Beispielen unterstützter Abfragen finden Sie unter [PQL-Übersicht](../../segmentation/pql/overview.md).

## Streaming-Ausdrücke

Die folgende Tabelle enthält Details zu häufig verwendeten Abfrageausdrücken, die im Streaming-Modus unterstützt werden.

| Beschreibung | PQL-Ausdruck | Eingabetyp:<br/>Profil- oder Erlebnisereignis (EE)[]) | Ergebnistyp |
|---|---|---|---|
| Anzahl der Bilddownloads in den letzten sieben Tagen. | xEvent[(Zeitstempel tritt &lt; 7 Tage vor dem Zeitpunkt auf) und eventType=&quot;download&quot; und contentType = &quot;image&quot;].count() | Profil und EE[] | Ganzzahl |
| Summe der Kundenausgaben für Sportartikel in den letzten sieben Tagen. | xEvent[(Zeitstempel tritt &lt; 7 Tage vor dem Zeitpunkt auf) und eventType=&quot;transaction&quot; und category = &quot;sporting products&quot;].sum(commerce.order.priceTotal) | Profil und EE[] | Ganzzahl oder Double |
| Durchschnittliche Kundenausgaben für Sportartikel in den letzten sieben Tagen.<br/><br/>**Hinweis:** Erfordert die Erstellung von drei berechneten Attributen. | **ca1:** xEvent[(Zeitstempel tritt &lt; 7 Tage vor dem Zeitpunkt auf) und eventType=&quot;transaction&quot; und category = &quot;sporting products&quot;].sum(commerce.order.priceTotal)<br/><br/>**ca2:** xEvent[(Zeitstempel tritt &lt; 7 Tage vor dem Zeitpunkt auf) und eventType=&quot;transaction&quot; und category = &quot;sporting products&quot;].count()<br/><br/>**ca3:** ca1/ca2 | Profil und EE[] | Double |
| Hat der Kunde in den letzten sieben Tagen mehr als 100 USD für Sportartikel ausgegeben?<br/><br/>**Hinweis:** Erfordert die Erstellung von zwei berechneten Attributen. | **ca1:** xEvent[(Zeitstempel tritt &lt; 7 Tage vor dem Zeitpunkt auf) und eventType=&quot;transaction&quot; und category = &quot;sporting products&quot;].sum(commerce.order.priceTotal)<br/><br/>**ca2:** ca1 > 100 | Profil und EE[] | Boolesch |
| Hat der Kunde in den letzten sieben Tagen einen Kauf getätigt? | chain(xEvent, timestamp, [A: WHAT(eventType = &quot;transaction&quot;) WHEN(&lt; 7 Tage vorher)]) | Profil und EE[] | Boolesch |
| Niedrigste Ausgaben für Sportartikel in den letzten sieben Tagen. | xEvent[(Zeitstempel tritt &lt; 7 Tage vor dem Zeitpunkt auf) und eventType=&quot;transaction&quot; und category = &quot;sporting products&quot;].min(commerce.order.priceTotal) | Profil und EE[] | Ganzzahl oder Double |
| Höchste Ausgaben für Sportartikel in den letzten sieben Tagen. | xEvent[(Zeitstempel tritt &lt; 7 Tage vor dem Zeitpunkt auf) und eventType=&quot;transaction&quot; und category = &quot;sporting products&quot;].max(commerce.order.priceTotal) | Profil und EE[] | Ganzzahl oder Double |
| Anzahl der Downloads jedes heruntergeladenen Produkts in den letzten sieben Tagen, indiziert nach Produkt. | xEvent[(Zeitstempel tritt &lt; 7 Tage vor dem aktuellen Datum auf) und eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.count())) | Profil und EE[] | Zuordnung[Zeichenfolge, Ganzzahl] |
| Summe der numerischen Eigenschaft über Downloads der heruntergeladenen Produkte in den letzten 7 Tagen, indiziert nach Produkt. | xEvent[(Zeitstempel tritt &lt; 7 Tage vor dem aktuellen Datum auf) und eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal))) | Profil und EE[] | Zuordnung[Zeichenfolge, Ganzzahl] oder Landkarte[Zeichenfolge, Doppelt] |
| Durchschnitt der numerischen Eigenschaft gegenüber den Downloads der heruntergeladenen Produkte in den letzten 7 Tagen, indiziert nach Produkt.<br/><br/>**Hinweis:** Erfordert die Erstellung von drei berechneten Attributen. | **ca1:** xEvent[(Zeitstempel tritt &lt; 7 Tage vor dem aktuellen Datum auf) und eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal)))<br/><br/>**ca2:** xEvent[(Zeitstempel tritt &lt; 7 Tage vor dem aktuellen Datum auf) und eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.count()))<br/><br/>**ca3:** ca2 / ca1 | Profil und EE[] | Zuordnung[Zeichenfolge, Doppelt] |
| Mindestens numerische Eigenschaft gegenüber Downloads jedes heruntergeladenen Produkts in den letzten 7 Tagen, indiziert nach Produkt. | xEvent[(Zeitstempel tritt &lt; 7 Tage vor dem aktuellen Datum auf) und eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.min(commerce.order.priceTotal))) | Profil und EE[] | Zuordnung[Zeichenfolge, Ganzzahl] oder Landkarte[Zeichenfolge, Doppelt] |
| Maximale numerische Eigenschaft über Downloads der heruntergeladenen Produkte in den letzten 7 Tagen, indiziert nach Produkt. | xEvent[(Zeitstempel tritt &lt; 7 Tage vor dem aktuellen Datum auf) und eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.max(commerce.order.priceTotal))) | Profil und EE[] | Zuordnung[Zeichenfolge, Ganzzahl] oder Landkarte[Zeichenfolge, Doppelt] |
| Numerischer Ausdruck für ein Profil, nicht auf Ereignisse verweisen. | if(person.gender = &quot;female&quot;, 60, 65) | Profil | Ganzzahl oder Double |
| Boolescher Ausdruck für das Profil, nicht auf Ereignisse verweisen. | person.birthYear >= 2000 | Profil | Boolesch |
| Zeichenfolgenausdruck im Profil, nicht auf Ereignisse verweisen. | if(homeAddress.countryCode in [&quot;US&quot;,&quot;MX&quot;,&quot;CA&quot;], &quot;NA&quot;, &quot;ROW&quot;) | Profil | Zeichenfolge |

## Batch-Ausdrücke

Die folgende Tabelle enthält Details zu Abfrageausdrücken, die nur im Batch-Modus verfügbar sind, was bedeutet, dass sie derzeit nicht im Streaming verfügbar sind.

| Beschreibung | PQL-Ausdruck | Eingabetyp:<br/>Profil- oder Erlebnisereignis (EE)[]) | Ergebnistyp |
|---|---|---|---|
| Gibt an, ob die Summe numerischer Ausdrücke gegenüber Produktdownloads in den letzten 7 Tagen 100, indiziert nach Produkt, überschreitet. | xEvent[(Zeitstempel tritt &lt; 7 Tage vor dem aktuellen Datum auf) und eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal) > 100)) | Profil und EE[] | Zuordnung[Zeichenfolge, Boolesch] |
| Gibt an, ob der Durchschnitt numerischer Ausdrücke gegenüber Produktdownloads in den letzten 7 Tagen 100, indexiert nach Produkt, überschreitet. | xEvent[(Zeitstempel tritt &lt; 7 Tage vor dem aktuellen Datum auf) und eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.average(commerce.order.priceTotal) > 100)) | Profil und EE[] | Zuordnung[Zeichenfolge, Boolesch] |
| Akkumulation verschiedener Metriken für jedes heruntergeladene Produkt in den letzten 7 Tagen, indiziert nach Produkt. | xEvent[(Zeitstempel tritt &lt; 7 Tage vor dem aktuellen Datum auf) und eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, {&quot;count&quot;: G.count(), &quot;sum&quot;: G.sum(commerce.order.priceTotal)}) | Profil und EE[] | Zuordnung[Zeichenfolge, Objekt] wobei Objekt ein benutzerdefinierter XDM-Typ ist |
