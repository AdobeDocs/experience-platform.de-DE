---
keywords: Experience Platform;Home;beliebte Themen;Segmentierung;Segmentierung;Segmentierungsdienst;pql;PQL;Profil-Abfrage-Sprache;Vergleichsfunktionen;Vergleich;
solution: Experience Platform
title: PQL-Vergleichsfunktionen
topic: developer guide
description: Vergleichsfunktionen werden verwendet, um zwischen verschiedenen Ausdrücken und Werten zu vergleichen und "true"oder "false"entsprechend zurückzugeben.
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 14%

---


# Vergleichsfunktionen

Vergleichsfunktionen werden zum Vergleich zwischen verschiedenen Ausdrücken und Werten verwendet und geben `true` oder `false` entsprechend zurück. Weitere Informationen zu anderen PQL-Funktionen finden Sie im [[!DNL Profile Query Language] overview](./overview.md).

## Gleich

Die Funktion `=` (gleich) prüft, ob ein Wert oder Ausdruck gleich einem anderen Wert oder Ausdruck ist.

**Format**

```sql
{EXPRESSION} = {VALUE}
```

**Beispiel**

Die folgende PQL-Abfrage prüft, ob sich das Land mit der Heimatadresse in Kanada befindet.

```sql
homeAddress.countryISO = "CA"
```

## Ungleich

Die Funktion `!=` (nicht gleich) prüft, ob ein Wert oder Ausdruck **nicht** einem anderen Wert oder Ausdruck entspricht.

**Format**

```sql
{EXPRESSION} != {VALUE}
```

**Beispiel**

Die folgende PQL-Abfrage überprüft, ob das Land der Wohnadresse nicht in Kanada liegt.

```sql
homeAddress.countryISO != "CA"
```

## Größer als

Mit der Funktion `>` (Größer als) wird überprüft, ob der erste Wert größer als der zweite ist.

**Format**

```sql
{EXPRESSION} > {EXPRESSION} 
```

**Beispiel**

Die folgende PQL-Abfrage definiert Personen, deren Geburtstage nicht im Januar oder Februar liegen.

```sql
person.birthMonth > 2
```

## Größer oder gleich

Mit der Funktion `>=` (größer oder gleich) wird überprüft, ob der erste Wert größer oder gleich dem zweiten Wert ist.

**Format**

```sql
{EXPRESSION} >= {EXPRESSION} 
```

**Beispiel**

Die folgende PQL-Abfrage definiert Personen, deren Geburtstage nicht im Januar oder Februar liegen.

```sql
person.birthMonth >= 3
```

## Kleiner als

Mit der Vergleichsfunktion `<` (less than) wird geprüft, ob der erste Wert kleiner als der zweite ist.

**Format**

```sql
{EXPRESSION} < {EXPRESSION} 
```

**Beispiel**

Die folgende PQL-Abfrage definiert Personen, deren Geburtstag im Januar liegt.

```sql
person.birthMonth < 2
```

## Kleiner oder gleich

Mit der Vergleichsfunktion `<=` (kleiner oder gleich) wird geprüft, ob der erste Wert kleiner oder gleich dem zweiten Wert ist.

**Format**

```sql
{EXPRESSION} <= {EXPRESSION} 
```

**Beispiel**

Die folgende PQL-Abfrage definiert Personen, deren Geburtstag im Januar oder Februar liegt.

```sql
person.birthMonth <= 2
```

## Nächste Schritte

Jetzt, da Sie von den Vergleichsfunktionen erfahren haben, können Sie sie in Ihren PQL-Abfragen verwenden. Weitere Informationen zu anderen PQL-Funktionen finden Sie in [Profil Query Language – Übersicht](./overview.md).
