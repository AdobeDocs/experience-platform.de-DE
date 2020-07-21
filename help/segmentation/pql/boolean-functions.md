---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Boolesche Funktionen
topic: developer guide
translation-type: tm+mt
source-git-commit: 6a0a9b020b0dc89a829c557bdf29b66508a10333
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 21%

---


# Boolesche Funktionen

Boolesche Funktionen werden verwendet, um eine boolesche Logik für verschiedene Elemente in [!DNL Profile Query Language] (PQL) durchzuführen.  Weiterführende Informationen zu anderen PQL-Funktionen finden Sie in der [Übersicht zu Profil Query Language](./overview.md).

## Und

Die `and` Funktion wird verwendet, um eine logische Verbindung zu erstellen.

**Format**

```sql
{QUERY} and {QUERY}
```

**Beispiel**

Die folgende PQL Abfrage wird alle Menschen mit Heimat als Kanada und Geburtsjahr von 1985.

```sql
homeAddress.countryISO = "CA" and person.birthYear = 1985
```

## Oder

Die `or` Funktion wird verwendet, um eine logische Trennung zu erzeugen.

**Format**

```sql
{QUERY} or {QUERY}
```

**Beispiel**

Die folgende PQL Abfrage wird alle Menschen mit Heimat als Kanada oder Geburtsjahr von 1985.

```sql
homeAddress.countryISO = "CA" or person.birthYear = 1985
```

## Nicht

Die Funktion `not` (oder `!`) dient zur Erstellung einer logischen Negation.

**Format**

```sql
not ({QUERY})
!({QUERY})
```

**Beispiel**

Die folgende PQL-Abfrage gibt alle Menschen zurück, die ihr Heimatland nicht als Kanada haben.

```sql
not (homeAddress.countryISO = "CA")
```

## Wenn

Die `if` Funktion wird zum Auflösen eines Ausdrucks verwendet, je nachdem, ob eine angegebene Bedingung wahr ist.

**Format**

```sql
if ({TEST_EXPRESSION}, {TRUE_EXPRESSION}, {FALSE_EXPRESSION})
```

| Argument | Beschreibung |
| --------- | ----------- |
| `{TEST_EXPRESSION}` | Der boolesche Ausdruck, der getestet wird. |
| `{TRUE_EXPRESSION}` | Der Ausdruck, dessen Wert verwendet wird, wenn `{TEST_EXPRESSION}` true lautet. |
| `{FALSE_EXPRESSION}` | Der Ausdruck, dessen Wert verwendet wird, wenn `{TEST_EXPRESSION}` false lautet. |

**Beispiel**

In der folgenden PQL-Abfrage wird der Wert so eingestellt, `1` als wäre das Heimatland Kanada und `2` das Heimatland nicht Kanada.

```sql
if (homeAddress.countryISO = "CA", 1, 2)
```

## Nächste Schritte

Jetzt, da Sie von booleschen Funktionen erfahren haben, können Sie sie in Ihren PQL-Abfragen verwenden. Weiterführende Informationen zu anderen PQL-Funktionen finden Sie in der [Übersicht zu Profil Query Language](./overview.md).
