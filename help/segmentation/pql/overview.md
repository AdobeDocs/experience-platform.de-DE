---
solution: Experience Platform
title: Übersicht zu Profile Query Language (PQL)
description: Dieses Handbuch bietet einen allgemeinen Überblick über PQL, einschließlich Formatierungsrichtlinien und PQL-Beispielausdrücken.
exl-id: 4f7ab50e-89a3-42db-b74a-c6f2d86c9bcb
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: ht
source-wordcount: '706'
ht-degree: 100%

---

# Übersicht zu [!DNL Profile Query Language] (PQL)

[!DNL Profile Query Language] (PQL) ist eine [!DNL Experience Data Model] (XDM)-konforme Abfragesprache, die die Definition und Ausführung von Segmentierungsabfragen für [!DNL Real-Time Customer Profile]-Daten unterstützt.

Dieses Handbuch bietet einen allgemeinen Überblick über PQL, einschließlich Formatierungsrichtlinien und PQL-Beispielausdrücken.

## Formatierung von PQL-Abfragen

PQL-Abfragen haben die folgende Signatur:

```sql
({INPUT_PARAMETER_1}, {INPUT_PARAMETER_2}, ...) => {RESULT_TYPE}
```

Der Eingabeparameter kann ein einfaches Primitiv sein, z. B. ein boolescher Wert, eine Zeichenfolge oder ein komplexerer Typ wie ein Objekt, ein Array oder eine Zuordnung.

Es gibt drei verschiedene Möglichkeiten, auf Eingabeparameter innerhalb eines PQL-Ausdrucks zu verweisen:

### Impliziter Verweis auf den ersten Parameter

Da sich der erste Parameter immer im Kontext befindet, kann im folgenden Beispiel ein direkter Eigenschaftsverweis (`homeAddress`) darauf erfolgen.

```sql
homeAddress.stateProvince = workAddress.stateProvince
```

### Expliziter Verweis auf den ersten Parameter

Im folgenden Beispiel bezieht sich `$1` auf den ersten Parameter. Daher verweist `$2` auf den zweiten Parameter usw.

```sql
$1.homeAddress.stateProvince = $1.homeAddress.stateProvince
```

### Verwendung benannter Variablen unter Verwendung der Lambda-Notation

Im folgenden Beispiel ist `Profile` ein Variablenname, der vom Abfrageautor ausgewählt werden kann.

```sql
(Profile) => Profile.homeAddress.stateProvince = Profile.workAddress.stateProvince
```

## PQL-Literale

PQL unterstützt die folgenden Literaltypen:

| Literal | Definition | Beispiel |
| ------- | ---------- | ------- |
| Zeichenfolge | Ein Datentyp, der aus Zeichen besteht, die von doppelten Anführungszeichen umgeben sind. | `"pizza"`, `"jobs"`, `"antidisestablishmentarianism"` |
| Boolesch | Ein Datentyp, der entweder „true“ oder „false“ ist. | `true`, `false` |
| Ganzzahl | Ein Datentyp, der eine ganze Zahl darstellt. Sie kann positiv, negativ oder null sein. | `-201`, `0`, `412` |
| Double | Ein Datentyp, der eine beliebige reale Zahl darstellt. Sie kann positiv, negativ oder null sein. | `-51.24`, `3.14`, `0.6942058` |
| Datum | Ein Datentyp, mit dem Datumswerte basierend auf Jahr, Monat und Tag als Ganzzahlparameter erstellt werden können. Das Format lautet `date(year, month, day)`. | `date(2020, 3, 14)` |
| Array | Ein Datentyp, der aus einer Gruppe anderer Literalwerte besteht. Zur Gruppierung werden eckige Klammern und Kommas verwendet, um zwischen verschiedenen Werten zu trennen. <br> **Hinweis:** Sie können nicht direkt auf die Eigenschaften von Elementen in einem Array zugreifen. Wenn Sie also auf eine Eigenschaft in einem Array zugreifen müssen, wird `select X from array where X.item = ...` als Methode unterstützt. <br> PQL reserviert das Wort `xEvent`, um auf ein Array von Erlebnisereignissen zu verweisen, die mit einem Profil verknüpft sind. | `[1, 4, 7]`, `["US", "CA"]` |
| Relative Zeitverweise | Reservierte Wörter, die verwendet werden können, um Zeitstempel und Zeitintervallverweise zu bilden. <ul><li>now, today, yesterday, tomorrow</li><li>this, last, next</li><li>before, after, from</li><li>millisecond(s), second(s), minute(s), hour(s), day(s), week(s), month(s), year(s), decade(s), century/centuries, millennium/millennia</li></ul> | `X.timestamp occurs before today`, `X.timestamp occurs last month`, `X.timestamp occurs <= 3 days before now` |

## PQL-Funktionen

In der folgenden Tabelle sind die verschiedenen Kategorien unterstützter PQL-Funktionen aufgeführt, einschließlich Links zu weiterer Dokumentation mit zusätzlichen Informationen.

| Kategorie | Definition |
| -------- | ---------- |
| Boolesch | Wird verwendet, um boolesche Algebra in PQL zu implementieren. Weitere Informationen zu diesen Funktionen finden Sie im [Dokument zu booleschen Funktionen](./boolean-functions.md). |
| Vergleich | Wird für Vergleiche zwischen verschiedenen PQL-Elementen verwendet. Weitere Informationen zu diesen Funktionen finden Sie im [Dokument zu Vergleichsfunktionen](./comparison-functions.md). |
| Array, List und Set | Wird für die Interaktion mit Arrays, Listen und Sets verwendet. Weitere Informationen zu diesen Funktionen finden Sie im [Dokument zu Array-, List- und Set-Funktionen](./array-functions.md). |
| Zuordnung | Wird für die Interaktion mit Zuordnungen verwendet. Weitere Informationen zu diesen Funktionen finden Sie im [Dokument zu Zuordnungsfunktionen](./map-functions.md). |
| Zeichenfolge | Wird zur Interaktion mit Zeichenfolgen verwendet. Weitere Informationen zu diesen Funktionen finden Sie im [Dokument zu Zeichenfolgenfunktionen](./string-functions.md). |
| Objekt | Wird für die Interaktion mit Objekten verwendet. Weitere Informationen zu diesen Funktionen finden Sie im [Dokument zu Objektfunktionen](./object-functions.md). |
| Arithmetisch | Wird verwendet, um grundlegende Berechnungen für PQL-Elemente durchzuführen. Weitere Informationen zu diesen Funktionen finden Sie im [Dokument zu arithmetischen Funktionen](./arithmetic-functions.md) |
| Aggregation | Wird verwendet, um Ergebnisse eines Arrays zu einem einzelnen Ergebnis zu kombinieren. Weitere Informationen zu Aggregationsfunktionen finden Sie im [Dokument zu Aggregationsfunktionen](./aggregation-functions.md). |
| Datum und Uhrzeit | Wird zusammen mit Datums-, Uhrzeit- und Datum/Uhrzeit-Objekten verwendet. Weitere Informationen zu diesen Funktionen finden Sie im [Dokument zu Datums-/Uhrzeitfunktionen](./datetime-functions.md). |
| Filter | Wird zum Filtern von Daten innerhalb von Arrays verwendet. Weitere Informationen zu diesen Funktionen finden Sie im [Dokument zu Filterfunktionen](./filter-functions.md). |
| Logische Quantoren | Wird verwendet, um Bedingungen in einem Array durchzusetzen. Weitere Informationen finden Sie im [Dokument zu logischen Quantoren](./logical-quantifiers.md). |
| Sonstiges | Funktionen, die nicht in eine der oben genannten Kategorien passen, finden Sie im [Dokument zu sonstigen Funktionen](./misc-functions.md). |

## Nächste Schritte

Da Sie nun wissen, wie Sie [!DNL Profile Query Language] (PQL) verwenden, können Sie damit Segment-Definitionen erstellen und ändern. Weiterführende Informationen zur Segmentierung finden Sie in der [Segmentierungsübersicht](../home.md).
