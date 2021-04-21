---
keywords: Experience Platform;Home;beliebte Themen;Segmentierung;Segmentierung;Segmentierungsdienst;pql;PQL;Sprache der Profil-Abfrage;Datums- und Uhrzeitfunktionen;Datenzeitfunktionen;Datenzeit;Datum;Uhrzeit;
solution: Experience Platform
title: Datums- und Uhrzeitfunktionen für PQL
topic-legacy: developer guide
description: Datums- und Uhrzeitfunktionen werden zur Durchführung von Datums- und Uhrzeitvorgängen in Profil Abfrage Language (PQL) verwendet.
exl-id: 8cbffcb6-1c25-454f-8f02-eca602318e5e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 7%

---

# Datums- und Uhrzeitfunktionen

Datums- und Uhrzeitfunktionen werden verwendet, um Datums- und Uhrzeitvorgänge für Werte innerhalb von [!DNL Profile Query Language] (PQL) durchzuführen. Weitere Informationen zu anderen PQL-Funktionen finden Sie im [[!DNL Profile Query Language] overview](./overview.md).

## Aktueller Monat

Die Funktion `currentMonth` gibt den aktuellen Monat als Ganzzahl zurück.

**Format**

```sql
currentMonth()
```

**Beispiel**

Die folgende PQL-Abfrage prüft, ob der Geburtsmonat der Person der aktuelle Monat ist.

```sql
person.birthMonth = currentMonth()
```

## Monat

Die Funktion `getMonth` gibt den Monat als Ganzzahl basierend auf einem angegebenen Zeitstempel zurück.

**Format**

```sql
{TIMESTAMP}.getMonth()
```

**Beispiel**

Die folgende PQL-Abfrage überprüft, ob der Geburtsmonat der Person im Juni liegt.

```sql
person.birthdate.getMonth() = 6
```

## Aktuelles Jahr

Die Funktion `currentYear` gibt das aktuelle Jahr als Ganzzahl zurück.

**Format**

```sql
currentYear()
```

**Beispiel**

Die folgende PQL-Abfrage prüft, ob das Produkt im laufenden Jahr verkauft wurde.

```sql
product.saleYear = currentYear()
```

## Jahr

Die Funktion `getYear` gibt das Jahr als Ganzzahl basierend auf einem angegebenen Zeitstempel zurück.

**Format**

```sql
{TIMESTAMP}.getYear()
```

**Beispiel**

Die folgende PQL-Abfrage überprüft, ob das Geburtsjahr der Person in den Jahren 1991, 1992, 1993, 1994 oder 1995 zurückgeht.

```sql
person.birthday.getYear() in [1991, 1992, 1993, 1994, 1995]
```

## Aktueller Tag des Monats

Die Funktion `currentDayOfMonth` gibt den aktuellen Tag des Monats als Ganzzahl zurück.

**Format**

```sql
currentDayOfMonth()
```

**Beispiel**

Die folgende PQL-Abfrage prüft, ob der Geburtstag der Person mit dem aktuellen Monatsdatum übereinstimmt.

```sql
person.birthDay = currentDayOfMonth()
```

## Monatstag abrufen

Die Funktion `getDayOfMonth` gibt den Tag als Ganzzahl basierend auf einem bestimmten Zeitstempel zurück.

**Format**

```sql
{TIMESTAMP}.getDayOfMonth()
```

**Beispiel**

Die folgende PQL-Abfrage überprüft, ob der Artikel innerhalb der ersten 15 Tage des Monats verkauft wurde.

```sql
product.sale.getDayOfMonth() <= 15
```

## Occurs

Die Funktion `occurs` vergleicht die angegebene Zeitstempelfunktion mit einem bestimmten Zeitraum.

**Format**

Die Funktion `occurs` kann in einem der folgenden Formate geschrieben werden:

```sql
{TIMESTAMP} occurs {COMPARISON} {INTEGER} {TIME_UNIT} {DIRECTION} {TIME}
{TIMESTAMP} occurs {DIRECTION} {TIME}
{TIMESTAMP} occurs (on) {TIME}
{TIMESTAMP} occurs between {TIME} and {TIME}
```

| Argument | Beschreibung |
| --------- | ----------- |
| `{COMPARISON}` | Ein Vergleichsoperator. Kann eine der folgenden Operatoren sein: `>`, `>=`, `<`, `<=`, `=`, `!=`. Weitere Informationen zu den Vergleichsfunktionen finden Sie im Dokument [Vergleichsfunktionen](./comparison-functions.md). |
| `{INTEGER}` | Eine nicht negative Ganzzahl. |
| `{TIME_UNIT}` | Eine Zeiteinheit. Kann eines der folgenden Wörter sein: `millisecond(s)`, `second(s)`, `minute(s)`, `hour(s)`, `day(s)`, `week(s)`, `month(s)`, `year(s)`, `decade(s)`, `century`, `centuries`, `millennium`, `millennia`. |
| `{DIRECTION}` | Eine Präposition, die beschreibt, wann das Datum mit dem Datum zu vergleichen ist. Kann eines der folgenden Wörter sein: `before`, `after`, `from`. |
| `{TIME}` | Kann ein Zeitstempelliteral (`today`, `now`, `yesterday`, `tomorrow`), eine relative Zeiteinheit (eine von `this`, `last` oder `next` gefolgt von einer Zeiteinheit) oder ein Zeitstempelattribut sein. |

>[!NOTE]
>
>Die Verwendung des Wortes `on` ist optional. Es ist vorhanden, um die Lesbarkeit für einige Kombinationen zu verbessern, z. B. `timestamp occurs on date(2019,12,31)`.

**Beispiel**

Die folgende PQL-Abfrage überprüft, ob der Artikel in der letzten Woche verkauft wurde.

```sql
product.saleDate occurs last week
```

Die folgende PQL-Abfrage überprüft, ob ein Artikel zwischen dem 8. Januar 2015 und dem 1. Juli 2017 verkauft wurde.

```sql
product.saleDate occurs between date(2015, 1, 8) and date(2017, 7, 1)
```

## Jetzt

`now` ist ein reserviertes Wort, das den Zeitstempel der PQL-Ausführung darstellt.

**Beispiel**

Die folgende PQL-Abfrage überprüft, ob ein Artikel genau drei Stunden zuvor verkauft wurde.

```sql
product.saleDate occurs = 3 hours before now
```

## Heute

`today` ist ein reserviertes Wort, das den Zeitstempel des Beginns der Ausführung von PQL darstellt.

**Beispiel**

Die folgende PQL-Abfrage prüft, ob der Geburtstag einer Person vor drei Tagen erfolgte.

```sql
person.birthday occurs = 3 days before today
```

## Nächste Schritte

Jetzt, da Sie Informationen zu Datums- und Uhrzeitfunktionen erhalten haben, können Sie diese in Ihren PQL-Abfragen verwenden. Weitere Informationen zu anderen PQL-Funktionen finden Sie in [Profil Query Language – Übersicht](./overview.md).
