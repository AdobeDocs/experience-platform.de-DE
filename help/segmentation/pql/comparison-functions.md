---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Vergleichsfunktionen
topic: developer guide
translation-type: tm+mt
source-git-commit: 92f92f480f29f7d6440f4e90af3225f9a1fcc3d0
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 10%

---


# Vergleichsfunktionen

Vergleichsfunktionen werden verwendet, um zwischen verschiedenen Ausdrücken und Werten zu vergleichen, zurückzugeben `true` oder `false` entsprechend. Weitere Informationen zu anderen PQL-Funktionen finden Sie in der [Profil Abfrage Language-Übersicht](./overview.md).

## Gleich

Die Funktion `=` (gleich) prüft, ob ein Wert oder Ausdruck mit einem anderen Wert oder Ausdruck übereinstimmt.

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

Die Funktion `!=` (nicht gleich) prüft, ob ein Wert oder Ausdruck **nicht** mit einem anderen Wert oder Ausdruck übereinstimmt.

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

## Niedriger als

Mit der Vergleichsfunktion `<` (kleiner als) wird überprüft, ob der erste Wert kleiner als der zweite ist.

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

Mit der Vergleichsfunktion `<=` (kleiner oder gleich) wird überprüft, ob der erste Wert kleiner oder gleich dem zweiten Wert ist.

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

Jetzt, da Sie von den Vergleichsfunktionen erfahren haben, können Sie sie in Ihren PQL-Abfragen verwenden. Weitere Informationen zu anderen PQL-Funktionen finden Sie in der [Profil Abfrage Language-Übersicht](./overview.md).
