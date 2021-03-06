---
keywords: Experience Platform; Startseite; beliebte Themen; Segmentierung; Segmentierung; Segmentierungsdienst; pql; PQL; Profile Query Language; Vergleichsfunktionen; Vergleich;
solution: Experience Platform
title: PQL-Vergleichsfunktionen
topic-legacy: developer guide
description: Vergleichsfunktionen werden verwendet, um zwischen verschiedenen Ausdrücken und Werten zu vergleichen und "true"oder "false"entsprechend zurückzugeben.
exl-id: 15f106c7-b88b-4042-b925-703e2a309573
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 76%

---

# Vergleichsfunktionen

Vergleichsfunktionen werden verwendet, um zwischen verschiedenen Ausdrücken und Werten zu vergleichen und `true` oder `false` entsprechend zurückzugeben. Weitere Informationen zu anderen PQL-Funktionen finden Sie in der [[!DNL Profile Query Language] Übersicht](./overview.md).

## Gleich

Die Funktion `=` (gleich) prüft, ob ein Wert oder Ausdruck gleich einem anderen Wert oder Ausdruck ist.

**Format**

```sql
{EXPRESSION} = {VALUE}
```

**Beispiel**

Die folgende PQL-Abfrage prüft, ob das Land des Wohnsitzes Kanada ist.

```sql
homeAddress.countryISO = "CA"
```

## Ungleich

Die Funktion `!=` (ungleich) prüft, ob ein Wert oder Ausdruck **ungleich** einem anderen Wert oder Ausdruck ist.

**Format**

```sql
{EXPRESSION} != {VALUE}
```

**Beispiel**

Die folgende PQL-Abfrage prüft, ob das Land des Wohnsitzes nicht Kanada ist.

```sql
homeAddress.countryISO != "CA"
```

## Größer als

Mit der Funktion `>` (größer als) wird überprüft, ob der erste Wert größer als der zweite ist.

**Format**

```sql
{EXPRESSION} > {EXPRESSION} 
```

**Beispiel**

Die folgende PQL-Abfrage gibt Personen zurück, die weder im Januar noch im Februar Geburtstag haben.

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

Die folgende PQL-Abfrage gibt Personen zurück, die weder im Januar noch im Februar Geburtstag haben.

```sql
person.birthMonth >= 3
```

## Kleiner als

Mit der Vergleichsfunktion `<` (kleiner als) wird geprüft, ob der erste Wert kleiner als der zweite ist.

**Format**

```sql
{EXPRESSION} < {EXPRESSION} 
```

**Beispiel**

Die folgende PQL-Abfrage gibt Personen zurück, die im Januar Geburtstag haben.

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

Die folgende PQL-Abfrage gibt Personen zurück, die im Januar oder Februar Geburtstag haben.

```sql
person.birthMonth <= 2
```

## Nächste Schritte

Nachdem Sie sich mit den Vergleichsfunktionen vertraut gemacht haben, können Sie diese nun in Ihren PQL-Abfragen verwenden. Weitere Informationen zu anderen PQL-Funktionen finden Sie in [Profil Query Language – Übersicht](./overview.md).
