---
solution: Experience Platform
title: Boolesche PQL-Funktionen
description: Boolesche Funktionen werden verwendet, um boolesche Logik für verschiedene Elemente in Profile Query Language (PQL) durchzuführen.
exl-id: 68a4a8cc-88ad-41b1-b9fc-c2b4ab7d0122
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 58%

---

# Boolesche Funktionen

Boolesche Funktionen werden verwendet, um eine boolesche Logik für verschiedene Elemente in [!DNL Profile Query Language] (PQL) durchzuführen.  Weitere Informationen zu anderen PQL-Funktionen finden Sie in der [[!DNL Profile Query Language] Übersicht](./overview.md) .

## Und

Mit der Funktion `and` wird ein logisches Bindewort als boolescher Wert erstellt.

**Format**

```sql
{QUERY} and {QUERY}
```

**Beispiel**

Die folgende PQL-Abfrage gibt alle Personen mit Wohnsitz in Kanada und dem Geburtsjahr 1985 zurück.

```sql
homeAddress.countryISO = "CA" and person.birthYear = 1985
```

## Oder

Mit der Funktion `or` wird eine logische Trennung als boolescher Wert erstellt.

**Format**

```sql
{QUERY} or {QUERY}
```

**Beispiel**

Die folgende PQL-Abfrage gibt alle Personen mit Wohnsitz in Kanada oder dem Geburtsjahr 1985 zurück.

```sql
homeAddress.countryISO = "CA" or person.birthYear = 1985
```

## Nicht

Die Funktion `not` (oder `!`) wird zur Erstellung einer logischen Negation verwendet.

**Format**

```sql
not ({QUERY})
!({QUERY})
```

**Beispiel**

Die folgende PQL-Abfrage gibt alle Menschen zurück, die keinen Wohnsitz in Kanada haben.

```sql
not (homeAddress.countryISO = "CA")
```

## Wenn 

Die Funktion `if` wird verwendet, um einen Ausdruck aufzulösen, je nachdem, ob eine angegebene Bedingung als boolescher Wert wahr ist.

**Format**

```sql
if ({TEST_EXPRESSION}, {TRUE_EXPRESSION}, {FALSE_EXPRESSION})
```

| Argument | Beschreibung |
| --------- | ----------- |
| `{TEST_EXPRESSION}` | Der geprüfte boolesche Ausdruck. |
| `{TRUE_EXPRESSION}` | Der Ausdruck, dessen Wert verwendet wird, wenn `{TEST_EXPRESSION}` „true“ ist. |
| `{FALSE_EXPRESSION}` | Der Ausdruck, dessen Wert verwendet wird, wenn `{TEST_EXPRESSION}` „false“ ist. |

**Beispiel**

Die folgende PQL-Abfrage setzt den Wert auf `1`, wenn der Wohnsitz in Kanada liegt, und auf `2`, wenn der Wohnsitz nicht in Kanada liegt.

```sql
if (homeAddress.countryISO = "CA", 1, 2)
```

## Nächste Schritte

Nachdem Sie sich mit booleschen Funktionen vertraut gemacht haben, können Sie diese nun in Ihren PQL-Abfragen verwenden. Weitere Informationen zu anderen PQL-Funktionen finden Sie in [Profil Query Language – Übersicht](./overview.md).
