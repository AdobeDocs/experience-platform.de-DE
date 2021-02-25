---
keywords: Experience Platform;Profil;Echtzeit-Profil von Kunden;Fehlerbehebung;API
title: Beispiel-PQL-Ausdruck für berechnete Attribute
topic: guide
type: Dokumentation
description: Berechnete Attribute sind Funktionen, mit denen Daten auf Ereignis-Ebene in Attribute auf Profil-Ebene Aggregat werden. Diese Funktionen erfordern die Verwendung gültiger PQL-Ausdruck (Profil Abfrage Language). In diesem Handbuch werden einige der am häufigsten verwendeten PQL-Ausdruck für berechnete Attribute vorgestellt.
translation-type: tm+mt
source-git-commit: 92533f732cc14b57d2a0a34ce9afe99554f9af04
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 2%

---


# (Alpha) Beispiel-PQL-Ausdruck für berechnete Attribute

>[!IMPORTANT]
>
>Die Funktion für berechnete Attribute ist derzeit alphanumerisch und steht nicht allen Benutzern zur Verfügung. Die Dokumentation und Funktionalität können sich ändern.

In Adobe Experience Platform sind berechnete Attribute Funktionen, mit denen Daten auf Ereignis-Ebene in Attribute auf Profil-Ebene Aggregat werden. Diese Funktionen werden automatisch berechnet, sodass sie für die Segmentierung, Aktivierung und Personalisierung verwendet werden können. Jedes berechnete Attribut wird mit grundlegenden Informationen wie Name und Beschreibung, der Schema-Klasse und dem Pfad zum Feld, in dem der Wert gespeichert werden soll, sowie einem Ausdruck definiert, dessen berechneter Wert der Wert ist, den Sie im berechneten Attribut speichern möchten.

Die Ausdruck, die in berechneten Attributen verwendet werden, werden mit der XDM-kompatiblen Abfrage [!DNL Profile Query Language] (PQL) erstellt, die die Definition und Ausführung von Abfragen für Kundendaten in Echtzeit unterstützt.

Berechnete Attribute unterstützen derzeit die folgenden Funktionen: sum, count, min, max und boolean. In diesem Handbuch werden einige der am häufigsten verwendeten PQL-Ausdruck erläutert, die Sie beim Definieren Ihrer eigenen berechneten Attribute für Ihr Unternehmen verwenden können. Weitere Informationen zu PQL und Links zu zusätzlichen Formatierungsrichtlinien und Beispielen unterstützter Abfragen finden Sie unter [PQL overview](../../segmentation/pql/overview.md).

## Streaming-Ausdruck

Die folgende Tabelle enthält Informationen zu häufig verwendeten Ausdrücken der Abfrage, die im Streaming-Modus unterstützt werden.

| Beschreibung | PQL-Ausdruck | Eingabetyp:<br/>Profil oder Erlebnis-Ereignis (EE[]) | Ergebnistyp |
|---|---|---|---|
| Anzahl der Downloads von Bildern in den letzten 7 Tagen. | xEvent[(Zeitstempel &lt; 7 Tage zuvor) und eventType=&quot;download&quot; und contentType = &quot;image&quot;].count() | Profil &amp; EE[] | Ganzzahl |
| Summe der Kundenausgaben für Sportartikel in den letzten 7 Tagen. | xEvent[(Zeitstempel &lt; 7 Tage vorher) und eventType=&quot;transaction&quot; und Kategorie = &quot;Sportartikel&quot;].sum(commerce.order.priceTotal) | Profil &amp; EE[] | Ganzzahl oder Dublette |
| Durchschnittliche Kundenausgaben für Sportartikel in den letzten 7 Tagen.<br/><br/>**Hinweis:** Erfordert die Erstellung von drei berechneten Attributen. | **ca1:** xEvent[(timestamp occur  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.sum(commerce.order.priceTotal)<br/><br/>**ca2:** xEvent[(timestamp occur  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.count()<br/><br/>**ca3:** ca1 / ca2]] | Profil &amp; EE[] | Double |
| Hat der Kunde in den letzten 7 Tagen mehr als 100 Dollar für Sportartikel ausgegeben?<br/><br/>**Hinweis:** Erfordert die Erstellung zweier berechneter Attribute. | **ca1:** xEvent[(Zeitstempel tritt auf  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.sum(commerce.order.priceTotal)<br/><br/>**ca2:** ca1 > 100] | Profil &amp; EE[] | Boolesch |
| Hat der Kunde in den letzten 7 Tagen einen Kauf getätigt? | chain(xEvent, timestamp, [A: WHAT(eventType = &quot;transaction&quot;) WHEN(&lt; 7 Tage zuvor)]) | Profil &amp; EE[] | Boolesch |
| Die geringsten Ausgaben der Benutzer für Sportartikel in den letzten 7 Tagen. | xEvent[(Zeitstempel &lt; 7 Tage vorher) und eventType=&quot;transaction&quot; und Kategorie = &quot;Sportartikel&quot;].min(commerce.order.priceTotal) | Profil &amp; EE[] | Ganzzahl oder Dublette |
| Höchste Benutzer verbringen in den letzten 7 Tagen Sportartikel. | xEvent[(Zeitstempel &lt; 7 Tage vorher) und eventType=&quot;transaction&quot; und Kategorie = &quot;Sportartikel&quot;].max(commerce.order.priceTotal) | Profil &amp; EE[] | Ganzzahl oder Dublette |
| Anzahl der Downloads jedes heruntergeladenen Produkts in den letzten 7 Tagen, nach Produkt indiziert. | xEvent[(Zeitstempel &lt; 7 Tage vorher) und eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.count()))) | Profil &amp; EE[] | Map[String, Integer] |
| Summe der numerischen Eigenschaft gegenüber den Downloads jedes heruntergeladenen Produkts in den letzten 7 Tagen, nach Produkt indiziert. | xEvent[(Zeitstempel &lt; 7 Tage vorher) und eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal)))) | Profil &amp; EE[] | Map[String, Integer] oder Map[String, Dublette] |
| Durchschnitt der numerischen Eigenschaft gegenüber den Downloads der heruntergeladenen Produkte in den letzten 7 Tagen, nach Produkt indiziert.<br/><br/>**Hinweis:** Erfordert die Erstellung von drei berechneten Attributen. | **ca1:** xEvent[(timestamp occur  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal)))<br/><br/>**ca2:** xEvent[(timestamp occur  &lt; 7=&quot;&quot; days=&quot;&quot; before=&quot;&quot; now=&quot;&quot;>.groupBy(product).map((K, G) => mapEntry(K, G.count())<br/><br/>**) ca3:** ca2 / ca1]] | Profil &amp; EE[] | Map[String, Dublette] |
| Minimum der numerischen Eigenschaft über Downloads jedes heruntergeladenen Produkts, in den letzten 7 Tagen indiziert nach Produkt. | xEvent[(Zeitstempel &lt; 7 Tage vorher) und eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.min(commerce.order.priceTotal)))) | Profil &amp; EE[] | Map[String, Integer] oder Map[String, Dublette] |
| Maximal numerische Eigenschaft über Downloads jedes heruntergeladenen Produkts in den letzten 7 Tagen, nach Produkt indiziert. | xEvent[(Zeitstempel &lt; 7 Tage vorher) und eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.max(commerce.order.priceTotal)))) | Profil &amp; EE[] | Map[String, Integer] oder Map[String, Dublette] |
| Numerischer Ausdruck auf Profil, nicht auf Ereignis verweisen. | if(person.gender = &quot;women&quot;, 60, 65) | Profil | Ganzzahl oder Dublette |
| Boolescher Ausdruck auf Profil, nicht auf Ereignis verweisen. | person.bornYear >= 2000 | Profil | Boolesch |
| String-Ausdruck auf Profil, nicht auf Ereignis verweisen. | if(homeAddress.countryCode in [&quot;US&quot;,&quot;MX&quot;,&quot;CA&quot;], &quot;NA&quot;, &quot;ROW&quot;) | Profil | Zeichenfolge |

## Batch-Ausdruck

Die folgende Tabelle enthält Details zu Ausdrücken der Abfrage, die nur im Stapelmodus verfügbar sind, d. h. sie sind derzeit nicht im Streaming verfügbar.

| Beschreibung | PQL-Ausdruck | Eingabetyp:<br/>Profil oder Erlebnis-Ereignis (EE[]) | Ergebnistyp |
|---|---|---|---|
| Gibt an, ob die Summe des numerischen Ausdrucks über die Produktdownloads in den letzten 7 Tagen 100 übersteigt (nach Produkt indiziert). | xEvent[(Zeitstempel &lt; 7 Tage vorher) und eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.sum(commerce.order.priceTotal) > 100)) | Profil &amp; EE[] | Map[String, Boolean] |
| Gibt an, ob der durchschnittliche numerische Ausdruck über die Produktdownloads in den letzten 7 Tagen 100 (produktspezifisch) übersteigt. | xEvent[(Zeitstempel &lt; 7 Tage vorher) und eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, G.average(commerce.order.priceTotal) > 100)) | Profil &amp; EE[] | Map[String, Boolean] |
| Kumulierung verschiedener Metriken für jedes heruntergeladene Produkt in den letzten 7 Tagen, nach Produkt indiziert. | xEvent[(Zeitstempel &lt; 7 Tage vorher) und eventType=&quot;download&quot;].groupBy(product).map((K, G) => mapEntry(K, {&quot;count&quot;: G.count(), &quot;sum&quot;: G.sum(commerce.order.priceTotal)) | Profil &amp; EE[] | Zuordnung[Zeichenfolge, Objekt], wobei Objekt ein benutzerdefinierter XDM-Typ ist |