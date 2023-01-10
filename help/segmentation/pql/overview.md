---
keywords: Experience Platform; Startseite; beliebte Themen; PQL; pql; Profilabfragesprache
solution: Experience Platform
title: Profil Query Language (PQL) - Überblick
description: Dieses Handbuch bietet einen allgemeinen Überblick über PQL, einschließlich Formatierungsrichtlinien und Beispielausdrücken für PQLs.
exl-id: 4f7ab50e-89a3-42db-b74a-c6f2d86c9bcb
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 14%

---

# [!DNL Profile Query Language] (PQL) - Übersicht

[!DNL Profile Query Language] (PQL) ist eine [!DNL Experience Data Model] (XDM)-konforme Abfragesprache, die die Definition und Ausführung von Segmentierungsabfragen für [!DNL Real-Time Customer Profile] Daten.

Dieses Handbuch bietet einen allgemeinen Überblick über PQL, einschließlich Formatierungsrichtlinien und Beispielausdrücken für PQLs.

## PQL-Abfrageformatierung

PQL-Abfragen haben die folgende Signatur:

```sql
({INPUT_PARAMETER_1}, {INPUT_PARAMETER_2}, ...) => {RESULT_TYPE}
```

Der Eingabeparameter kann ein einfaches Primitiv sein, z. B. ein boolescher Wert, eine Zeichenfolge oder ein komplexerer Typ, z. B. ein Objekt, ein Array oder eine Zuordnung.

Es gibt drei verschiedene Möglichkeiten, auf Eingabeparameter im Text eines PQL-Ausdrucks zu verweisen:

### Impliziter Verweis auf den ersten Parameter

Da sich der erste Parameter immer im Kontext befindet, wird im folgenden Beispiel eine Eigenschaftsreferenz (`homeAddress`) können direkt an sie angefertigt werden.

```sql
homeAddress.stateProvince = workAddress.stateProvince
```

### Expliziter Verweis auf den ersten Parameter

Im folgenden Beispiel: `$1` bezieht sich auf den ersten Parameter. Daher `$2` auf den zweiten Parameter usw. verweisen.

```sql
$1.homeAddress.stateProvince = $1.homeAddress.stateProvince
```

### Verwendung benannter Variablen unter Verwendung der Lambda-Notation

Im folgenden Beispiel: `Profile` ist ein Variablenname, der vom Abfrageautor ausgewählt werden kann.

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
| Datum | Ein Datentyp, mit dem Datumswerte basierend auf Jahr, Monat und Tag als Ganzzahlparameter erstellt werden können. Sie ist formatiert als `date(year, month, day)` | `date(2020, 3, 14)` |
| Array | Ein Datentyp, der aus einer Gruppe anderer Literalwerte besteht. Zur Gruppierung werden eckige Klammern und Kommas verwendet, um zwischen verschiedenen Werten zu trennen. <br> **Hinweis:** Sie können nicht direkt auf die Eigenschaften von Elementen in einem Array zugreifen. Wenn Sie also auf eine Eigenschaft in einem Array zugreifen müssen, wird die unterstützte Methode `select X from array where X.item = ...`. <br> PQL behält sich das Wort vor `xEvent` , um ein Array von Erlebnisereignissen zu referenzieren, die mit einem Profil verknüpft sind. | `[1, 4, 7]`, `["US", "CA"]` |
| Relative Zeitreferenzen | Reservierte Wörter, die verwendet werden können, um Zeitstempel und Zeitintervallverweise zu bilden. <ul><li>jetzt, heute, gestern, morgen</li><li>dies, last, next</li><li>before, after, from</li><li>Millisekunde(n), Sekunde(n), Minute(n), Stunde(n), Tag(e), Woche(n), Monat(e), Jahr(e), Jahrzehnt(e), Jahrhundert/Jahrhunderte, Millenium/Millennium</li></ul> | `X.timestamp occurs before today`, `X.timestamp occurs last month`, `X.timestamp occurs <= 3 days before now` |


## PQL-Funktionen

In der folgenden Tabelle sind die verschiedenen Kategorien unterstützter PQL-Funktionen aufgeführt, einschließlich Links zu weiteren Dokumentationen mit weiteren Informationen.

| Kategorie | Definition |
| -------- | ---------- |
| Boolesch | Wird verwendet, um boolesche Algebra in PQL zu implementieren. Weitere Informationen zu diesen Funktionen finden Sie im [Dokument mit booleschen Funktionen](./boolean-functions.md). |
| Vergleich | Dient zum Vergleich zwischen verschiedenen PQL-Elementen. Weitere Informationen zu diesen Funktionen finden Sie im [Dokument zu Vergleichsfunktionen](./comparison-functions.md). |
| Array, Liste und Satz | Wird für die Interaktion mit Arrays, Listen und Sets verwendet. Weitere Informationen zu diesen Funktionen finden Sie im [Dokument zu Array-, List- und Set-Funktionen](./array-functions.md). |
| Zuordnung | Wird für die Interaktion mit Karten verwendet. Weitere Informationen zu diesen Funktionen finden Sie im [Dokument für Zuordnungsfunktionen](./map-functions.md). |
| Zeichenfolge | Wird zur Interaktion mit Zeichenfolgen verwendet. Weitere Informationen zu diesen Funktionen finden Sie im [Dokument mit Zeichenfolgen-Funktionen](./string-functions.md). |
| Objekt | Wird für die Interaktion mit Objekten verwendet. Weitere Informationen zu diesen Funktionen finden Sie im [Objektfunktionen-Dokument](./object-functions.md). |
| Arithmetisch | Wird verwendet, um grundlegende Berechnungen für PQL-Elemente durchzuführen. Weitere Informationen zu diesen Funktionen finden Sie im [Dokument mit arithmetischen Funktionen](./arithmetic-functions.md) |
| Aggregation | Wird verwendet, um Ergebnisse eines Arrays in einem einzelnen Ergebnis zu kombinieren. Weitere Informationen zu Aggregationsfunktionen finden Sie im [Dokument zu Aggregationsfunktionen](./aggregation-functions.md). |
| Datum und Uhrzeit | Wird zusammen mit Datums-, Uhrzeit- und Datum/Uhrzeit-Objekten verwendet. Weitere Informationen zu diesen Funktionen finden Sie im [Dokument zu Datums-/Uhrzeitfunktionen](./datetime-functions.md). |
| Filter | Dient zum Filtern von Daten innerhalb von Arrays. Weitere Informationen zu diesen Funktionen finden Sie im [Dokument mit Filterfunktionen](./filter-functions.md). |
| Logische Quantoren | Wird verwendet, um Bedingungen in einem Array zu erteilen. Weitere Informationen finden Sie im [Dokument zu logischen Quantifizierungen](./logical-quantifiers.md). |
| Sonstiges | Funktionen, die nicht in eine der oben genannten Kategorien passen, finden Sie im Abschnitt [Dokument zu verschiedenen Funktionen](./misc-functions.md). |

## Nächste Schritte

Jetzt, da Sie gelernt haben, [!DNL Profile Query Language]können Sie PQL beim Erstellen und Ändern von Segmenten verwenden. Weitere Informationen zur Segmentierung finden Sie im Abschnitt [Segmentierungsübersicht](../home.md).
