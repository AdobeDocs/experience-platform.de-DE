---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;boolean functions;boolean;
solution: Experience Platform
title: Boolesche Funktionen
topic: developer guide
description: Boolesche Funktionen werden verwendet, um eine Boolesche Logik für verschiedene Elemente in Profil Abfrage Language (PQL) auszuführen.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 14%

---


# Boolesche Funktionen

Boolesche Funktionen werden verwendet, um eine boolesche Logik für verschiedene Elemente in [!DNL Profile Query Language] (PQL) durchzuführen.  More information about other PQL functions can be found in the [[!DNL Profile Query Language] overview](./overview.md).

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

Jetzt, da Sie von booleschen Funktionen erfahren haben, können Sie sie in Ihren PQL-Abfragen verwenden. Weitere Informationen zu anderen PQL-Funktionen finden Sie in [Profil Query Language – Übersicht](./overview.md).
