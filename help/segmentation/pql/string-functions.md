---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Zeichenfolgen-Funktionen
topic: developer guide
translation-type: tm+mt
source-git-commit: 6a0a9b020b0dc89a829c557bdf29b66508a10333
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 13%

---


# Zeichenfolgen-Funktionen

[!DNL Profile Query Language] (PQL) Angebot Funktionen, um die Interaktion mit Zeichenfolgen zu vereinfachen. Weiterführende Informationen zu anderen PQL-Funktionen finden Sie in der [Übersicht zu Profil Query Language](./overview.md).

## like

Mit der `like` Funktion wird bestimmt, ob eine Zeichenfolge einem angegebenen Muster entspricht.

**Format**

```sql
{STRING_1} like {STRING_2}
```

| Argument | Beschreibung |
| --------- | ----------- |
| `{STRING_1}` | Die Zeichenfolge, die überprüft werden soll. |
| `{STRING_2}` | Der Ausdruck, der mit der ersten Zeichenfolge übereinstimmen soll. Es werden zwei Sonderzeichen zum Erstellen eines Ausdrucks unterstützt: `%` und `_`. <ul><li>`%` wird verwendet, um 0 oder mehr Zeichen zu repräsentieren.</li><li>`_` wird verwendet, um genau ein Zeichen zu repräsentieren.</li></ul> |

**Beispiel**

Die folgende PQL-Abfrage ruft alle Städte mit dem Muster &quot;es&quot;ab.

```sql
city like "%es%"
```

## Beginnt mit

Mit der `startsWith` Funktion wird bestimmt, ob eine Zeichenfolge mit einer angegebenen Unterzeichenfolge Beginn.

**Format**

```sql
{STRING_1}.startsWith({STRING_2}, {BOOLEAN})
```

| Argument | Beschreibung |
| --------- | ----------- |
| `{STRING_1}` | Die Zeichenfolge, die überprüft werden soll. |
| `{STRING_2}` | Die Zeichenfolge, nach der in der ersten Zeichenfolge gesucht werden soll. |
| `{BOOLEAN}` | Ein optionaler Parameter, mit dem bestimmt wird, ob bei der Prüfung die Groß-/Kleinschreibung beachtet wird. Standardmäßig ist dies auf true festgelegt. |

**Beispiel**

Die folgende PQL-Abfrage bestimmt bei Beachtung der Groß-/Kleinschreibung, ob der Name der Person mit &quot;Joe&quot;Beginn.

```sql
person.name.startsWith("Joe")
```

## Beginnt nicht mit

Mit der `doesNotStartWith` Funktion wird bestimmt, ob eine Zeichenfolge nicht mit einer angegebenen Unterzeichenfolge Beginn.

**Format**

```sql
{STRING_1}.doesNotStartWith({STRING_2}, {BOOLEAN})
```

| Argument | Beschreibung |
| --------- | ----------- |
| `{STRING_1}` | Die Zeichenfolge, die überprüft werden soll. |
| `{STRING_2}` | Die Zeichenfolge, nach der in der ersten Zeichenfolge gesucht werden soll. |
| `{BOOLEAN}` | Ein optionaler Parameter, mit dem bestimmt wird, ob bei der Prüfung die Groß-/Kleinschreibung beachtet wird. Standardmäßig ist dies auf true festgelegt. |

**Beispiel**

Die folgende PQL-Abfrage bestimmt bei Beachtung der Groß-/Kleinschreibung, ob der Personenname nicht mit &quot;Joe&quot;Beginn.

```sql
person.name.doesNotStartWith("Joe")
```

## Endet mit

Mit der `endsWith` Funktion wird bestimmt, ob eine Zeichenfolge mit einer angegebenen Unterzeichenfolge endet.

**Format**

```sql
{STRING_1}.endsWith({STRING_2}, {BOOLEAN})
```

| Argument | Beschreibung |
| --------- | ----------- |
| `{STRING_1}` | Die Zeichenfolge, die überprüft werden soll. |
| `{STRING_2}` | Die Zeichenfolge, nach der in der ersten Zeichenfolge gesucht werden soll. |
| `{BOOLEAN}` | Ein optionaler Parameter, mit dem bestimmt wird, ob bei der Prüfung die Groß-/Kleinschreibung beachtet wird. Standardmäßig ist dies auf true festgelegt. |

**Beispiel**

Die folgende PQL-Abfrage bestimmt unter Berücksichtigung der Groß-/Kleinschreibung, ob die E-Mail-Adresse der Person mit &quot;.com&quot;endet.

```sql
person.emailAddress.endsWith(".com")
```

## Endet nicht mit

Mit der `doesNotEndWith` Funktion wird bestimmt, ob eine Zeichenfolge nicht mit einer angegebenen Unterzeichenfolge endet.

**Format**

```sql
{STRING_1}.doesNotEndWith({STRING_2}, {BOOLEAN})
```

| Argument | Beschreibung |
| --------- | ----------- |
| `{STRING_1}` | Die Zeichenfolge, die überprüft werden soll. |
| `{STRING_2}` | Die Zeichenfolge, nach der in der ersten Zeichenfolge gesucht werden soll. |
| `{BOOLEAN}` | Ein optionaler Parameter, mit dem bestimmt wird, ob bei der Prüfung die Groß-/Kleinschreibung beachtet wird. Standardmäßig ist dies auf true festgelegt. |

**Beispiel**

Die folgende PQL-Abfrage bestimmt bei Beachtung der Groß-/Kleinschreibung, ob die E-Mail-Adresse der Person nicht mit &quot;.com&quot;endet.

```sql
person.emailAddress.doesNotEndWith(".com")
```

## „Enthält“

Mit der `contains` Funktion wird bestimmt, ob eine Zeichenfolge eine angegebene Unterzeichenfolge enthält.

**Format**

```sql
{STRING_1}.contains({STRING_2}, {BOOLEAN})
```

| Argument | Beschreibung |
| --------- | ----------- |
| `{STRING_1}` | Die Zeichenfolge, die überprüft werden soll. |
| `{STRING_2}` | Die Zeichenfolge, nach der in der ersten Zeichenfolge gesucht werden soll. |
| `{BOOLEAN}` | Ein optionaler Parameter, mit dem bestimmt wird, ob bei der Prüfung die Groß-/Kleinschreibung beachtet wird. Standardmäßig ist dies auf true festgelegt. |

**Beispiel**

Die folgende PQL-Abfrage bestimmt unter Berücksichtigung der Groß-/Kleinschreibung, ob die E-Mail-Adresse der Person die Zeichenfolge &quot;2010@gm&quot;enthält.

```sql
person.emailAddress.contains("2010@gm")
```

## Enthält nicht

Mit der `doesNotContain` Funktion wird bestimmt, ob eine Zeichenfolge keine angegebene Unterzeichenfolge enthält.

**Format**

```sql
{STRING_1}.doesNotContain({STRING_2}, {BOOLEAN})
```

| Argument | Beschreibung |
| --------- | ----------- |
| `{STRING_1}` | Die Zeichenfolge, die überprüft werden soll. |
| `{STRING_2}` | Die Zeichenfolge, nach der in der ersten Zeichenfolge gesucht werden soll. |
| `{BOOLEAN}` | Ein optionaler Parameter, mit dem bestimmt wird, ob bei der Prüfung die Groß-/Kleinschreibung beachtet wird. Standardmäßig ist dies auf true festgelegt. |

**Beispiel**

Die folgende PQL-Abfrage bestimmt unter Berücksichtigung der Groß-/Kleinschreibung, ob die E-Mail-Adresse der Person die Zeichenfolge &quot;2010@gm&quot;nicht enthält.

```sql
person.emailAddress.doesNotContain("2010@gm")
```

## Gleich

Mit der `equals` Funktion wird bestimmt, ob eine Zeichenfolge mit der angegebenen Zeichenfolge übereinstimmt.

**Format**

```sql
{STRING_1}.equals({STRING_2})
```

| Argument | Beschreibung |
| --------- | ----------- |
| `{STRING_1}` | Die Zeichenfolge, die überprüft werden soll. |
| `{STRING_2}` | Die mit der ersten Zeichenfolge zu vergleichende Zeichenfolge. |

**Beispiel**

Mit der folgenden PQL-Abfrage wird unter Berücksichtigung der Groß-/Kleinschreibung bestimmt, ob der Name der Person &quot;John&quot;lautet.

```sql
person.name.equals("John")
```

## Ungleich

Mit der `notEqualTo` Funktion wird bestimmt, ob eine Zeichenfolge nicht mit der angegebenen Zeichenfolge übereinstimmt.

**Format**

```sql
{STRING_1}.notEqualTo({STRING_2})
```

| Argument | Beschreibung |
| --------- | ----------- |
| `{STRING_1}` | Die Zeichenfolge, die überprüft werden soll. |
| `{STRING_2}` | Die mit der ersten Zeichenfolge zu vergleichende Zeichenfolge. |

**Beispiel**

Die folgende PQL-Abfrage bestimmt bei Beachtung der Groß-/Kleinschreibung, ob der Name der Person nicht &quot;John&quot;lautet.

```sql
person.name.notEqualTo("John")
```

## Stimmt überein mit

Mit der `matches` Funktion wird bestimmt, ob eine Zeichenfolge mit einem bestimmten regulären Ausdruck übereinstimmt. Weitere Informationen zu Übereinstimmungsmustern in regulären Ausdrücken finden Sie in [diesem Dokument](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html) .

**Format**

```sql
{STRING_1}.matches(STRING_2})
```

**Beispiel**

Die folgende PQL-Abfrage bestimmt, ob der Name der Person mit &quot;John&quot;Beginn, ohne dass die Groß-/Kleinschreibung beachtet wird.

```sql
person.name.matches("(?i)^John")
```

## Regelmäßiger Ausdruck

Die `regexGroup` Funktion wird verwendet, um spezifische Informationen basierend auf dem regulären Ausdruck zu extrahieren.

**Format**

```sql
{STRING}.regexGroup({EXPRESSION})
```

**Beispiel**

Die folgende PQL-Abfrage wird verwendet, um den Domänennamen aus einer E-Mail-Adresse zu extrahieren.

```sql
emailAddress.regexGroup("@(\w+)", 1)
```

## Nächste Schritte

Nachdem Sie nun von Zeichenfolgen-Funktionen Kenntnis erhalten haben, können Sie diese in Ihren PQL-Abfragen verwenden. Weiterführende Informationen zu anderen PQL-Funktionen finden Sie in der [Übersicht zu Profil Query Language](./overview.md).

