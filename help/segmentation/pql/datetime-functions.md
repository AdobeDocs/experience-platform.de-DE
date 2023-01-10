---
keywords: Experience Platform; Startseite; beliebte Themen; Segmentierung; Segmentierung; Segmentierungsdienst; pql; PQL; Profilabfragesprache; Datums- und Uhrzeitfunktionen; Datums-/Uhrzeitfunktionen; Datum; Uhrzeit;
solution: Experience Platform
title: PQL-Datums- und Uhrzeitfunktionen
description: Mit Datums- und Uhrzeitfunktionen können Datums- und Uhrzeitvorgänge für Werte in der Profile Query Language (PQL) durchgeführt werden.
exl-id: 8cbffcb6-1c25-454f-8f02-eca602318e5e
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 7%

---

# Datums- und Uhrzeitfunktionen

Mit den Datums- und Uhrzeitfunktionen können Sie Datums- und Uhrzeitvorgänge für Werte in [!DNL Profile Query Language] (PQL). Weitere Informationen zu anderen PQL-Funktionen finden Sie im [[!DNL Profile Query Language] Übersicht](./overview.md).

## Aktueller Monat

Die `currentMonth` gibt den aktuellen Monat als Ganzzahl zurück.

**Format**

```sql
currentMonth()
```

**Beispiel**

Die folgende PQL-Abfrage prüft, ob der Geburtsmonat der Person der aktuelle Monat ist.

```sql
person.birthMonth = currentMonth()
```

## Monat abrufen

Die `getMonth` gibt den Monat als Ganzzahl basierend auf einem angegebenen Zeitstempel zurück.

**Format**

```sql
{TIMESTAMP}.getMonth()
```

**Beispiel**

Die folgende PQL-Abfrage prüft, ob der Geburtsmonat der Person im Juni liegt.

```sql
person.birthdate.getMonth() = 6
```

## Aktuelles Jahr

Die `currentYear` gibt das aktuelle Jahr als Ganzzahl zurück.

**Format**

```sql
currentYear()
```

**Beispiel**

Die folgende PQL-Abfrage prüft, ob das Produkt im aktuellen Jahr verkauft wurde.

```sql
product.saleYear = currentYear()
```

## Jahr abrufen

Die `getYear` gibt das Jahr basierend auf einem angegebenen Zeitstempel als Ganzzahl zurück.

**Format**

```sql
{TIMESTAMP}.getYear()
```

**Beispiel**

Die folgende PQL-Abfrage prüft, ob das Geburtsjahr der Person in den Jahren 1991, 1992, 1993, 1994 oder 1995 zurückgeht.

```sql
person.birthday.getYear() in [1991, 1992, 1993, 1994, 1995]
```

## Aktueller Tag im Monat

Die `currentDayOfMonth` gibt den aktuellen Tag des Monats als Ganzzahl zurück.

**Format**

```sql
currentDayOfMonth()
```

**Beispiel**

Die folgende PQL-Abfrage prüft, ob der Geburtstag der Person mit dem aktuellen Tag des Monats übereinstimmt.

```sql
person.birthDay = currentDayOfMonth()
```

## Tag des Monats abrufen

Die `getDayOfMonth` gibt den Tag basierend auf einem angegebenen Zeitstempel als Ganzzahl zurück.

**Format**

```sql
{TIMESTAMP}.getDayOfMonth()
```

**Beispiel**

Die folgende PQL-Abfrage prüft, ob der Artikel innerhalb der ersten 15 Tage des Monats verkauft wurde.

```sql
product.sale.getDayOfMonth() <= 15
```

## Tritt auf

Die `occurs` vergleicht die angegebene Zeitstempelfunktion mit einem festen Zeitraum.

**Format**

Die `occurs` -Funktion kann mit einem der folgenden Formate geschrieben werden:

```sql
{TIMESTAMP} occurs {COMPARISON} {INTEGER} {TIME_UNIT} {DIRECTION} {TIME}
{TIMESTAMP} occurs {DIRECTION} {TIME}
{TIMESTAMP} occurs (on) {TIME}
{TIMESTAMP} occurs between {TIME} and {TIME}
```

| Argument | Beschreibung |
| --------- | ----------- |
| `{COMPARISON}` | Ein Vergleichsoperator. Kann einer der folgenden Operatoren sein: `>`, `>=`, `<`, `<=`, `=`, `!=`. Weitere Informationen zu den Vergleichsfunktionen finden Sie im [Dokument zu Vergleichsfunktionen](./comparison-functions.md). |
| `{INTEGER}` | Eine nicht negative Ganzzahl. |
| `{TIME_UNIT}` | Eine Zeiteinheit. Kann eines der folgenden Wörter sein: `millisecond(s)`, `second(s)`, `minute(s)`, `hour(s)`, `day(s)`, `week(s)`, `month(s)`, `year(s)`, `decade(s)`, `century`, `centuries`, `millennium`, `millennia`. |
| `{DIRECTION}` | Eine Präposition, die beschreibt, wann das Datum mit dem verglichen werden soll. Kann eines der folgenden Wörter sein: `before`, `after`, `from`. |
| `{TIME}` | Kann ein Zeitstempelliteral sein (`today`, `now`, `yesterday`, `tomorrow`), eine relative Zeiteinheit (eine von `this`, `last`oder `next` gefolgt von einer Zeiteinheit) oder einem Zeitstempelattribut. |

>[!NOTE]
>
>Verwendung des Wortes `on` ist optional. Es gibt eine Möglichkeit, die Lesbarkeit für einige Kombinationen zu verbessern, z. B. `timestamp occurs on date(2019,12,31)`.

**Beispiel**

Die folgende PQL-Abfrage prüft, ob der Artikel in der letzten Woche verkauft wurde.

```sql
product.saleDate occurs last week
```

Die folgende PQL-Abfrage prüft, ob ein Artikel zwischen dem 8. Januar 2015 und dem 1. Juli 2017 verkauft wurde.

```sql
product.saleDate occurs between date(2015, 1, 8) and date(2017, 7, 1)
```

## Jetzt

`now` ist ein reserviertes Wort, das den Zeitstempel der PQL-Ausführung darstellt.

**Beispiel**

Die folgende PQL-Abfrage prüft, ob ein Artikel genau drei Stunden zuvor verkauft wurde.

```sql
product.saleDate occurs = 3 hours before now
```

## Heute

`today` ist ein reserviertes Wort, das den Zeitstempel des Beginns des Tages der PQL-Ausführung darstellt.

**Beispiel**

Die folgende PQL-Abfrage prüft, ob der Geburtstag einer Person vor drei Tagen erfolgte.

```sql
person.birthday occurs = 3 days before today
```

## Nächste Schritte

Nachdem Sie sich mit Datums- und Uhrzeitfunktionen vertraut gemacht haben, können Sie diese nun in Ihren PQL-Abfragen verwenden. Weitere Informationen zu anderen PQL-Funktionen finden Sie in [Profil Query Language – Übersicht](./overview.md).
