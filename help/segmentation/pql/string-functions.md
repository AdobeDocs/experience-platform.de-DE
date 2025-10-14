---
solution: Experience Platform
title: PQL-Zeichenfolgen-Funktionen
description: Profile Query Language (PQL) bietet Funktionen, die die Interaktion mit Zeichenfolgen vereinfachen.
exl-id: 9fd79d86-0802-4312-abce-f6ef5ba5bb34
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 43%

---

# Zeichenfolgen-Funktionen

[!DNL Profile Query Language] (PQL) bietet Funktionen, die die Interaktion mit Zeichenfolgen vereinfachen. Weitere Informationen zu anderen PQL-Funktionen finden Sie in der [[!DNL Profile Query Language] Übersicht](./overview.md).

## Ist wie

Mit der Funktion `like` wird bestimmt, ob eine Zeichenfolge einem angegebenen Muster als Boolesch entspricht.

**Format**

```sql
{STRING_1} like {STRING_2}
```

| Argument | Beschreibung |
| --------- | ----------- |
| `{STRING_1}` | Die Zeichenfolge, die überprüft werden soll. |
| `{STRING_2}` | Der Ausdruck, der mit der ersten Zeichenfolge übereinstimmen soll. Es werden zwei Sonderzeichen zum Erstellen eines Ausdrucks unterstützt: `%` und `_`. <ul><li>`%` wird verwendet, um 0 oder mehr Zeichen zu repräsentieren.</li><li>`_` wird verwendet, um genau ein Zeichen zu repräsentieren.</li></ul> |

**Beispiel**

Die folgende PQL-Abfrage ruft alle Städte ab, die das Muster „es“ enthalten.

```sql
city like "%es%"
```

## Beginnt mit

Mit der Funktion `startsWith` wird bestimmt, ob eine Zeichenfolge mit einer angegebenen Unterzeichenfolge als Boolescher Wert beginnt.

**Format**

```sql
{STRING_1}.startsWith({STRING_2}, {BOOLEAN})
```

| Argument | Beschreibung |
| --------- | ----------- |
| `{STRING_1}` | Die Zeichenfolge, die überprüft werden soll. |
| `{STRING_2}` | Die Zeichenfolge, nach der in der ersten Zeichenfolge gesucht werden soll. |
| `{BOOLEAN}` | Ein optionaler Parameter, mit dem bestimmt wird, ob bei der Prüfung die Groß-/Kleinschreibung beachtet wird. Standardmäßig ist dies auf „true“ gesetzt. |

**Beispiel**

Die folgende PQL-Abfrage bestimmt bei Beachtung der Groß-/Kleinschreibung, ob der Name der Person mit „Joe“ beginnt.

```sql
person.name.startsWith("Joe")
```

## Beginnt nicht mit

Mit der Funktion `doesNotStartWith` wird bestimmt, ob eine Zeichenfolge nicht mit einer angegebenen Unterzeichenfolge als Boolescher Wert beginnt.

**Format**

```sql
{STRING_1}.doesNotStartWith({STRING_2}, {BOOLEAN})
```

| Argument | Beschreibung |
| --------- | ----------- |
| `{STRING_1}` | Die Zeichenfolge, die überprüft werden soll. |
| `{STRING_2}` | Die Zeichenfolge, nach der in der ersten Zeichenfolge gesucht werden soll. |
| `{BOOLEAN}` | Ein optionaler Parameter, mit dem bestimmt wird, ob bei der Prüfung die Groß-/Kleinschreibung beachtet wird. Standardmäßig ist dies auf „true“ gesetzt. |

**Beispiel**

Die folgende PQL-Abfrage bestimmt bei Beachtung der Groß-/Kleinschreibung, ob der Name der Person nicht mit „Joe“ beginnt.

```sql
person.name.doesNotStartWith("Joe")
```

## Endet mit

Mit der Funktion `endsWith` wird bestimmt, ob eine Zeichenfolge mit einer angegebenen Unterzeichenfolge als Boolescher Wert endet.

**Format**

```sql
{STRING_1}.endsWith({STRING_2}, {BOOLEAN})
```

| Argument | Beschreibung |
| --------- | ----------- |
| `{STRING_1}` | Die Zeichenfolge, die überprüft werden soll. |
| `{STRING_2}` | Die Zeichenfolge, nach der in der ersten Zeichenfolge gesucht werden soll. |
| `{BOOLEAN}` | Ein optionaler Parameter, mit dem bestimmt wird, ob bei der Prüfung die Groß-/Kleinschreibung beachtet wird. Standardmäßig ist dies auf „true“ gesetzt. |

**Beispiel**

Die folgende PQL-Abfrage bestimmt bei Beachtung der Groß-/Kleinschreibung, ob die E-Mail-Adresse der Person mit &quot;.com“ endet.

```sql
person.emailAddress.endsWith(".com")
```

## Endet nicht mit

Mit der Funktion `doesNotEndWith` wird bestimmt, ob eine Zeichenfolge nicht mit einer angegebenen Unterzeichenfolge als Boolescher Wert endet.

**Format**

```sql
{STRING_1}.doesNotEndWith({STRING_2}, {BOOLEAN})
```

| Argument | Beschreibung |
| --------- | ----------- |
| `{STRING_1}` | Die Zeichenfolge, die überprüft werden soll. |
| `{STRING_2}` | Die Zeichenfolge, nach der in der ersten Zeichenfolge gesucht werden soll. |
| `{BOOLEAN}` | Ein optionaler Parameter, mit dem bestimmt wird, ob bei der Prüfung die Groß-/Kleinschreibung beachtet wird. Standardmäßig ist dies auf „true“ gesetzt. |

**Beispiel**

Die folgende PQL-Abfrage bestimmt bei Beachtung der Groß-/Kleinschreibung, ob die E-Mail-Adresse der Person nicht mit &quot;.com“ endet.

```sql
person.emailAddress.doesNotEndWith(".com")
```

## Enthält

Mit der Funktion `contains` wird bestimmt, ob eine Zeichenfolge eine angegebene Unterzeichenfolge als booleschen Wert enthält.

**Format**

```sql
{STRING_1}.contains({STRING_2}, {BOOLEAN})
```

| Argument | Beschreibung |
| --------- | ----------- |
| `{STRING_1}` | Die Zeichenfolge, die überprüft werden soll. |
| `{STRING_2}` | Die Zeichenfolge, nach der in der ersten Zeichenfolge gesucht werden soll. |
| `{BOOLEAN}` | Ein optionaler Parameter, mit dem bestimmt wird, ob bei der Prüfung die Groß-/Kleinschreibung beachtet wird. Standardmäßig ist dies auf „true“ gesetzt. |

**Beispiel**

Die folgende PQL-Abfrage bestimmt bei Beachtung der Groß-/Kleinschreibung, ob die E-Mail-Adresse der Person die Zeichenfolge &quot;2010@gm&quot; enthält.

```sql
person.emailAddress.contains("2010@gm")
```

## Enthält nicht

Mit der Funktion `doesNotContain` wird bestimmt, ob eine Zeichenfolge eine angegebene Unterzeichenfolge nicht als booleschen Wert enthält.

**Format**

```sql
{STRING_1}.doesNotContain({STRING_2}, {BOOLEAN})
```

| Argument | Beschreibung |
| --------- | ----------- |
| `{STRING_1}` | Die Zeichenfolge, die überprüft werden soll. |
| `{STRING_2}` | Die Zeichenfolge, nach der in der ersten Zeichenfolge gesucht werden soll. |
| `{BOOLEAN}` | Ein optionaler Parameter, mit dem bestimmt wird, ob bei der Prüfung die Groß-/Kleinschreibung beachtet wird. Standardmäßig ist dies auf „true“ gesetzt. |

**Beispiel**

Die folgende PQL-Abfrage bestimmt bei Beachtung der Groß-/Kleinschreibung, ob die E-Mail-Adresse der Person die Zeichenfolge &quot;2010@gm&quot; nicht enthält.

```sql
person.emailAddress.doesNotContain("2010@gm")
```

## Gleich

Mit der Funktion `equals` wird bestimmt, ob eine Zeichenfolge gleich der angegebenen Zeichenfolge als Boolescher Wert ist.

**Format**

```sql
{STRING_1}.equals({STRING_2})
```

| Argument | Beschreibung |
| --------- | ----------- |
| `{STRING_1}` | Die Zeichenfolge, die überprüft werden soll. |
| `{STRING_2}` | Die mit der ersten Zeichenfolge zu vergleichende Zeichenfolge. |

**Beispiel**

Die folgende PQL-Abfrage bestimmt bei Beachtung der Groß-/Kleinschreibung, ob der Name der Person „John“ lautet.

```sql
person.name.equals("John")
```

## Ungleich

Mit der Funktion `notEqualTo` wird bestimmt, ob eine Zeichenfolge nicht gleich der angegebenen Zeichenfolge als boolescher Wert ist.

**Format**

```sql
{STRING_1}.notEqualTo({STRING_2})
```

| Argument | Beschreibung |
| --------- | ----------- |
| `{STRING_1}` | Die Zeichenfolge, die überprüft werden soll. |
| `{STRING_2}` | Die mit der ersten Zeichenfolge zu vergleichende Zeichenfolge. |

**Beispiel**

Die folgende PQL-Abfrage bestimmt bei Beachtung der Groß-/Kleinschreibung, ob der Name der Person nicht „John“ lautet.

```sql
person.name.notEqualTo("John")
```

## Stimmt überein mit

Mit der Funktion `matches` wird bestimmt, ob eine Zeichenfolge mit einem bestimmten regulären Ausdruck übereinstimmt. Weitere Informationen zu Übereinstimmungsmustern [&#x200B; regulären Ausdrücken finden Sie &#x200B;](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html) diesem Dokument als boolescher Wert.

**Format**

```sql
{STRING_1}.matches(STRING_2})
```

**Beispiel**

Die folgende PQL-Abfrage bestimmt, ob der Name der Person ohne Unterscheidung der Groß-/Kleinschreibung mit „John“ beginnt.

```sql
person.name.matches("(?i)^John")
```

>[!NOTE]
>
>Wenn Sie Funktionen für reguläre Ausdrücke wie `\w` verwenden, **müssen** den umgekehrten Schrägstrich auslassen. Anstatt nur `\w` zu schreiben, müssen Sie einen zusätzlichen umgekehrten Schrägstrich einfügen und `\\w` schreiben.

## Gruppe regelmäßiger Ausdrücke

Die Funktion `regexGroup` wird verwendet, um spezifische Informationen basierend auf dem regulären Ausdruck, der als Zeichenfolge bereitgestellt wird, zu extrahieren.

**Format**

```sql
{STRING}.regexGroup({EXPRESSION})
```

**Beispiel**

Die folgende PQL-Abfrage wird verwendet, um den Domain-Namen aus einer E-Mail-Adresse zu extrahieren.

```sql
emailAddress.regexGroup("@(\\w+)", 1)
```

>[!NOTE]
>
>Wenn Sie Funktionen für reguläre Ausdrücke wie `\w` verwenden, **müssen** den umgekehrten Schrägstrich auslassen. Anstatt nur `\w` zu schreiben, müssen Sie einen zusätzlichen umgekehrten Schrägstrich einfügen und `\\w` schreiben.

## Nächste Schritte

Nachdem Sie sich mit Zeichenfolgenfunktionen vertraut gemacht haben, können Sie diese in Ihren PQL-Abfragen verwenden. Weitere Informationen zu anderen PQL-Funktionen finden Sie in [Profil Query Language – Übersicht](./overview.md).
