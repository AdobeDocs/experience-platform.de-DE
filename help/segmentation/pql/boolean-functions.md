---
keywords: Experience Platform;Home;beliebte Themen;Segmentierung;Segmentierung;Segmentierungsdienst;pql;PQL;Profil-Abfrage-Sprache;Boolesche Funktionen;Boolescher Wert;
solution: Experience Platform
title: PQL Boolesche Funktionen
topic-legacy: developer guide
description: Boolesche Funktionen werden verwendet, um eine Boolesche Logik für verschiedene Elemente in Profil Abfrage Language (PQL) auszuführen.
exl-id: 68a4a8cc-88ad-41b1-b9fc-c2b4ab7d0122
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 12%

---

# Boolesche Funktionen

Boolesche Funktionen werden verwendet, um eine boolesche Logik für verschiedene Elemente in [!DNL Profile Query Language] (PQL) durchzuführen.  Weitere Informationen zu anderen PQL-Funktionen finden Sie im [[!DNL Profile Query Language] overview](./overview.md).

## Und

Die Funktion `and` wird zur Erstellung einer logischen Verbindung verwendet.

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

Die Funktion `or` wird verwendet, um eine logische Trennung zu erstellen.

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

Die Funktion `not` (oder `!`) wird zum Erstellen einer logischen Negation verwendet.

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

Die Funktion `if` wird verwendet, um einen Ausdruck aufzulösen, je nachdem, ob eine angegebene Bedingung wahr ist.

**Format**

```sql
if ({TEST_EXPRESSION}, {TRUE_EXPRESSION}, {FALSE_EXPRESSION})
```

| Argument | Beschreibung |
| --------- | ----------- |
| `{TEST_EXPRESSION}` | Der boolesche Ausdruck, der getestet wird. |
| `{TRUE_EXPRESSION}` | Der Ausdruck, dessen Wert verwendet wird, wenn `{TEST_EXPRESSION}` &quot;true&quot;ist. |
| `{FALSE_EXPRESSION}` | Der Ausdruck, dessen Wert verwendet wird, wenn `{TEST_EXPRESSION}` &quot;false&quot;ist. |

**Beispiel**

Die folgende PQL-Abfrage setzt den Wert auf `1`, wenn das Heimatland Kanada ist, und `2`, wenn das Heimatland nicht Kanada ist.

```sql
if (homeAddress.countryISO = "CA", 1, 2)
```

## Nächste Schritte

Jetzt, da Sie von booleschen Funktionen erfahren haben, können Sie sie in Ihren PQL-Abfragen verwenden. Weitere Informationen zu anderen PQL-Funktionen finden Sie in [Profil Query Language – Übersicht](./overview.md).
