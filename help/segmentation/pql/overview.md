---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Profil Abfrage Language (PQL) - Übersicht
topic: developer guide
translation-type: tm+mt
source-git-commit: 6a0a9b020b0dc89a829c557bdf29b66508a10333
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 3%

---


# [!DNL Profile Query Language] (PQL) - Übersicht

[!DNL Profile Query Language] (PQL) ist eine [!DNL Experience Data Model] (XDM-)konforme Abfrage, die die Definition und Ausführung von Segmentierungsdaten für [!DNL Real-time Customer Profile] Daten unterstützt.

Dieser Leitfaden bietet einen allgemeinen Überblick über PQL, der Formatierungsrichtlinien enthält und PQL-Ausdrücke anzeigt.

## PQL-Abfrage formatieren

PQL-Abfragen haben folgende Unterschrift:

```sql
({INPUT_PARAMETER_1}, {INPUT_PARAMETER_2}, ...) => {RESULT_TYPE}
```

Der Eingabeparameter kann ein einfacher Primitiv sein, z. B. ein boolescher oder ein String, oder ein komplexerer Typ, z. B. ein Objekt, ein Array oder eine Map.

Es gibt **drei** verschiedene Möglichkeiten, auf Eingabeparameter innerhalb eines PQL-Ausdrucks zu verweisen:

### Impliziter Verweis auf den ersten Parameter

Im unten stehenden Beispiel kann, da der erste Parameter immer im Kontext steht, ein Eigenschaftsverweis (`homeAddress`) direkt darauf angewendet werden.

```sql
homeAddress.stateProvince = workAddress.stateProvince
```

### Explizite Bezugnahme auf den ersten Parameter

Im unten stehenden Beispiel `$1` bezieht sich auf den ersten Parameter. Daher `$2` würde auf den zweiten Parameter usw. verwiesen.

```sql
$1.homeAddress.stateProvince = $1.homeAddress.stateProvince
```

### Verwendung benannter Variablen unter Verwendung der Lambda-Notation

Im folgenden Beispiel `Profile` ist ein Variablenname aufgeführt, der vom Autor der Abfrage ausgewählt werden kann.

```sql
(Profile) => Profile.homeAddress.stateProvince = Profile.workAddress.stateProvince
```

## PQL-Literale

PQL unterstützt die folgenden Literaltypen:

| Literal | Definition | Beispiel |
| ------- | ---------- | ------- |
| Zeichenfolge | Ein Datentyp, der aus Zeichen besteht, die von Dubletten-Anführungszeichen umgeben sind. | `"pizza"`, `"jobs"`, `"antidisestablishmentarianism"` |
| Boolesch | Ein Datentyp, der entweder &quot;true&quot;oder &quot;false&quot;ist. | `true`, `false` |
| Ganzzahl | Ein Datentyp, der eine ganze Zahl darstellt. Es kann positiv, negativ oder null sein. | `-201`, `0`, `412` |
| Double | Ein Datentyp, der eine beliebige reale Zahl darstellt. Es kann positiv, negativ oder null sein. | `-51.24`, `3.14`, `0.6942058` |
| Datum | Ein Datentyp, der zum Erstellen von Daten basierend auf den Parametern Jahr, Monat und Tag als Ganzzahl verwendet werden kann. It is formatted as `date(year, month, day)` | `date(2020, 3, 14)` |
| Array | Ein Datentyp, der als Gruppe anderer Literalwerte zusammengesetzt ist. Es verwendet eckige Klammern zur Gruppierung und Kommas zur Trennung zwischen verschiedenen Werten. <br> **Hinweis:** Sie können nicht direkt auf Eigenschaften von Elementen in einem Array zugreifen. Wenn Sie also auf eine Eigenschaft in einem Array zugreifen müssen, wird die unterstützte Methode `select X from array where X.item = ...`verwendet. <br> PQL behält sich das Wort `xEvent` vor, auf eine Reihe von Erlebnis-Ereignissen zu verweisen, die mit einem Profil verknüpft sind. | `[1, 4, 7]`, `["US", "CA"]` |
| Relative Zeitreferenzen | Reservierte Wörter, die zum Erstellen von Zeitstempeln und Zeitintervallverweisen verwendet werden können. <ul><li>jetzt, heute, gestern, morgen</li><li>this, last, next</li><li>before, after, from</li><li>Millisekunde(n), Sekunde(n), Minute(n), Stunde(n), Tag(e), Woche(n), Monat(n), Jahr(e), Jahrzehnt(e), Jahrhundert/Jahrhunderte, Jahrtausend/Jahrtausend</li></ul> | `X.timestamp occurs before today`, `X.timestamp occurs last month`, `X.timestamp occurs <= 3 days before now` |


## PQL-Funktionen

In der folgenden Tabelle sind die verschiedenen Kategorien unterstützter PQL-Funktionen aufgeführt, einschließlich Links zu weiteren Dokumentationen.

| Kategorie | Definition |
| -------- | ---------- |
| Boolesch | Wird verwendet, um boolesche Algebra in PQL zu implementieren. Weitere Informationen zu diesen Funktionen finden Sie im Dokument [zu booleschen Funktionen](./boolean-functions.md). |
| Vergleich | Dient zum Vergleich zwischen verschiedenen PQL-Elementen. Weitere Informationen zu diesen Funktionen finden Sie im Dokument [Vergleichsfunktionen](./comparison-functions.md). |
| Array, Liste und Satz | Wird für die Interaktion mit Arrays, Listen und Sets verwendet. Weitere Informationen zu diesen Funktionen finden Sie im Dokument [zu](./array-functions.md)Array-, Liste- und Set-Funktionen. |
| Zuordnung | Wird verwendet, um mit Karten zu interagieren. Weitere Informationen zu diesen Funktionen finden Sie im Dokument [Kartenfunktionen](./map-functions.md). |
| Zeichenfolge | Wird verwendet, um mit Zeichenfolgen zu interagieren. Weitere Informationen zu diesen Funktionen finden Sie im Dokument [Zeichenfolgen-Funktionen](./string-functions.md). |
| Arithmetisch | Dient zum Durchführen einer einfachen Arithmetik für PQL-Elemente. Weitere Informationen zu diesen Funktionen finden Sie im Dokument [Arithmetik-Funktionen](./arithmetic-functions.md) |
| Aggregation | Wird verwendet, um Ergebnisse eines Arrays zu einem einzelnen Ergebnis zu kombinieren. Weitere Informationen zu Aggregationsfunktionen finden Sie im Dokument [zu Aggregationsfunktionen](./aggregation-functions.md). |
| Datum und Uhrzeit | Wird in Verbindung mit Datums-, Uhrzeit- und Datenzeitobjekten verwendet. Weitere Informationen zu diesen Funktionen finden Sie im Dokument [zu Datums-/Uhrzeitfunktionen](./datetime-functions.md). |
| Filter | Dient zum Filtern von Daten in Arrays. Weitere Informationen zu diesen Funktionen finden Sie im Dokument [Filterfunktionen](./filter-functions.md). |
| Logische Quantoren | Wird verwendet, um Bedingungen in einem Array zu übernehmen. Weitere Informationen finden Sie im Dokument [zu logischen Quantifizierern](./logical-quantifiers.md). |
| Sonstiges | Funktionen, die nicht in eine der oben genannten Kategorien passen, finden Sie im Dokument [Verschiedene Funktionen](./misc-functions.md). |

## Nächste Schritte

Nachdem Sie nun gelernt haben, wie man es benutzt, können Sie PQL verwenden, wenn Sie Segmente erstellen und ändern. [!DNL Profile Query Language] For more information on segmentation, please read the [segmentation overview](../home.md).