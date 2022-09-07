---
keywords: Experience Platform; Startseite; beliebte Themen; Segmentierung; Segmentierung; Segmentierungsdienst; pql; PQL; Profile Query Language; Zeichenfolgenfunktionen; Zeichenfolge;
solution: Experience Platform
title: PQL-Zeichenfolgen-Funktionen
topic-legacy: developer guide
description: Profile Query Language (PQL) bietet Funktionen, die die Interaktion mit Zeichenfolgen vereinfachen.
exl-id: 9fd79d86-0802-4312-abce-f6ef5ba5bb34
source-git-commit: 1c9ed96cdbd9e670bd1f05467e33e8dab5bc2121
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 64%

---

# Zeichenfolgen-Funktionen

[!DNL Profile Query Language] (PQL) bietet Funktionen, die die Interaktion mit Zeichenfolgen vereinfachen. Weitere Informationen zu anderen PQL-Funktionen finden Sie im [[!DNL Profile Query Language] Übersicht](./overview.md).

## Ist wie

Mit der Funktion `like` wird bestimmt, ob eine Zeichenfolge einem angegebenen Muster entspricht.

**Format**

```sql
{STRING_1} like {STRING_2}
```

| Argument | Beschreibung |
| --------- | ----------- |
| `{STRING_1}` | Die Zeichenfolge, die überprüft werden soll. |
| `{STRING_2}` | Der Ausdruck, der mit der ersten Zeichenfolge übereinstimmen soll. Es werden zwei Sonderzeichen zum Erstellen eines Ausdrucks unterstützt: `%` und `_`. <ul><li>`%` wird verwendet, um 0 oder mehr Zeichen zu repräsentieren.</li><li>`_` wird verwendet, um genau ein Zeichen zu repräsentieren.</li></ul> |

**Beispiel**

Mit der folgenden PQL-Abfrage werden alle Städte abgerufen, die das Muster &quot;es&quot;enthalten.

```sql
city like "%es%"
```

## Beginnt mit

Mit der Funktion `startsWith` wird bestimmt, ob eine Zeichenfolge mit einer angegebenen Unterzeichenfolge beginnt.

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

Die folgende PQL-Abfrage bestimmt mit Groß-/Kleinschreibung, ob der Name der Person mit &quot;Joe&quot;beginnt.

```sql
person.name.startsWith("Joe")
```

## Beginnt nicht mit

Mit der Funktion `doesNotStartWith` wird bestimmt, ob eine Zeichenfolge nicht mit einer angegebenen Unterzeichenfolge beginnt.

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

Die folgende PQL-Abfrage ermittelt mit Groß-/Kleinschreibung, ob der Name der Person nicht mit &quot;Joe&quot;beginnt.

```sql
person.name.doesNotStartWith("Joe")
```

## Endet mit

Mit der Funktion `endsWith` wird bestimmt, ob eine Zeichenfolge mit einer angegebenen Unterzeichenfolge endet.

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

Die folgende PQL-Abfrage ermittelt mit Groß-/Kleinschreibung, ob die E-Mail-Adresse der Person auf &quot;.com&quot;endet.

```sql
person.emailAddress.endsWith(".com")
```

## Endet nicht mit

Mit der Funktion `doesNotEndWith` wird bestimmt, ob eine Zeichenfolge nicht mit einer angegebenen Unterzeichenfolge endet.

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

Die folgende PQL-Abfrage ermittelt mit Groß-/Kleinschreibung, ob die E-Mail-Adresse der Person nicht mit &quot;.com&quot;endet.

```sql
person.emailAddress.doesNotEndWith(".com")
```

## Enthält

Mit der Funktion `contains` wird bestimmt, ob eine Zeichenfolge eine angegebene Unterzeichenfolge enthält.

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

Die folgende PQL-Abfrage ermittelt mit Groß-/Kleinschreibung, ob die E-Mail-Adresse der Person die Zeichenfolge &quot;2010@gm&quot;enthält.

```sql
person.emailAddress.contains("2010@gm")
```

## Enthält nicht

Mit der Funktion `doesNotContain` wird bestimmt, ob eine Zeichenfolge eine angegebene Unterzeichenfolge nicht enthält.

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

Die folgende PQL-Abfrage ermittelt mit Groß-/Kleinschreibung, ob die E-Mail-Adresse der Person die Zeichenfolge &quot;2010@gm&quot;nicht enthält.

```sql
person.emailAddress.doesNotContain("2010@gm")
```

## Gleich

Mit der Funktion `equals` wird bestimmt, ob eine Zeichenfolge gleich der angegebenen Zeichenfolge ist.

**Format**

```sql
{STRING_1}.equals({STRING_2})
```

| Argument | Beschreibung |
| --------- | ----------- |
| `{STRING_1}` | Die Zeichenfolge, die überprüft werden soll. |
| `{STRING_2}` | Die mit der ersten Zeichenfolge zu vergleichende Zeichenfolge. |

**Beispiel**

Die folgende PQL-Abfrage bestimmt mit Groß-/Kleinschreibung, ob der Name der Person &quot;John&quot; lautet.

```sql
person.name.equals("John")
```

## Ungleich

Mit der Funktion `notEqualTo` wird bestimmt, ob eine Zeichenfolge nicht gleich der angegebenen Zeichenfolge ist.

**Format**

```sql
{STRING_1}.notEqualTo({STRING_2})
```

| Argument | Beschreibung |
| --------- | ----------- |
| `{STRING_1}` | Die Zeichenfolge, die überprüft werden soll. |
| `{STRING_2}` | Die mit der ersten Zeichenfolge zu vergleichende Zeichenfolge. |

**Beispiel**

Die folgende PQL-Abfrage ermittelt mit Groß-/Kleinschreibung, ob der Name der Person nicht &quot;John&quot;lautet.

```sql
person.name.notEqualTo("John")
```

## Stimmt überein mit

Mit der Funktion `matches` wird bestimmt, ob eine Zeichenfolge mit einem bestimmten regulären Ausdruck übereinstimmt. Weitere Informationen zu Übereinstimmungsmustern bei regulären Ausdrücken finden Sie in [diesem Dokument](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html).

**Format**

```sql
{STRING_1}.matches(STRING_2})
```

**Beispiel**

Die folgende PQL-Abfrage bestimmt, ohne die Groß-/Kleinschreibung zu beachten, ob der Name der Person mit &quot;John&quot;beginnt.

```sql
person.name.matches("(?i)^John")
```

>[!NOTE]
>
>Wenn Sie reguläre Ausdrucksfunktionen wie `\w`, **must** Escapezeichen für den umgekehrten Schrägstrich. Anstatt nur zu schreiben `\w`, müssen Sie einen zusätzlichen umgekehrten Schrägstrich einfügen und schreiben `\\w`.

## Gruppe regelmäßiger Ausdrücke

Die Funktion `regexGroup` wird verwendet, um spezifische Informationen basierend auf dem bereitgestellten regulären Ausdruck zu extrahieren.

**Format**

```sql
{STRING}.regexGroup({EXPRESSION})
```

**Beispiel**

Die folgende PQL-Abfrage wird verwendet, um den Domänennamen aus einer E-Mail-Adresse zu extrahieren.

```sql
emailAddress.regexGroup("@(\\w+)", 1)
```

>[!NOTE]
>
>Wenn Sie reguläre Ausdrucksfunktionen wie `\w`, **must** Escapezeichen für den umgekehrten Schrägstrich. Anstatt nur zu schreiben `\w`, müssen Sie einen zusätzlichen umgekehrten Schrägstrich einfügen und schreiben `\\w`.

## Nächste Schritte

Nachdem Sie sich mit Zeichenfolgen-Funktionen vertraut gemacht haben, können Sie sie in Ihren PQL-Abfragen verwenden. Weitere Informationen zu anderen PQL-Funktionen finden Sie in [Profil Query Language – Übersicht](./overview.md).
