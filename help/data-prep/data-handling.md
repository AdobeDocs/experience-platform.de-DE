---
keywords: Experience Platform;Home;beliebte Themen;Map CSV;Map CSV-Datei;CSV-Datei zu xdm zuordnen;CSV zu xdm zuordnen;ui-Handbuch;Mapper;Zuordnung;Datenvorbereitung;Datenvorbereitung;Vorbereiten von Daten;
solution: Experience Platform
title: Umgang mit Datenformaten mit Data Prep
topic-legacy: overview
description: Dieses Dokument gibt einen Überblick darüber, wie verschiedene Datentypen in der Datenvorbereitung verarbeitet werden.
exl-id: 4ad253b7-3f83-48cd-9c46-8b5ba627c09e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 13%

---

# Umgang mit Datenformaten mit Data Prep

Data Prep kann mit verschiedenen Datenformaten, die in Adobe Experience Platform aufgenommen werden, problemlos umgehen. In diesem Dokument wird erläutert, wie verschiedene Datenformate mit Data Prep behandelt werden.

## Booleans {#booleans}

Wenn der Quelltyp eine Zeichenfolge ist und der Zielgruppe-Typ ein boolescher Typ ist, kann Data Prep den Wert automatisch analysieren und den Quellwert in einen booleschen Wert konvertieren.

Die Werte `y`, `yes`, `Y`, `YES`, `on`, `ON`, `true` und `TRUE` werden automatisch als `true` analysiert.

Die Werte `n`, `N`, `no`, `NO`, `off`, `OFF`, `false` und `FALSE` werden automatisch als `false` analysiert.

## Daten  {#dates}

Data Prep unterstützt Datumsfunktionen sowohl als Zeichenfolgen als auch als Datenzeitobjekte.

### Datumsformat

Die Funktion date konvertiert Zeichenfolgen und Datenzeitobjekte in ein mit ISO 8601 formatiertes ZonedDateTime-Objekt.

**Format**

```http
date({DATE}, {FORMAT}, {DEFAULT_DATE})
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{DATE}` | Erforderlich. Die Zeichenfolge, die das Datum darstellt. |
| `{FORMAT}` | Optional. Die Zeichenfolge, die das Format des Datums darstellt. Weitere Informationen zur Zeichenfolgenformatierung finden Sie im Abschnitt [Datums-/Uhrzeitformat-Zeichenfolge](#format). |
| `{DEFAULT_DATE}` | Optional. Das Standarddatum, das zurückgegeben wird, wenn das angegebene Datum null ist. |

Beispielsweise konvertiert der Ausdruck `date(orderDate, "yyyy-MM-dd")` den Wert `orderDate` von &quot;31. Dezember 2020&quot;in den Zeitwert &quot;2020-12-31&quot;.

### Datumsfunktion Konvertierungen

Wenn Zeichenfolgenfelder aus eingehenden Daten in Schemas mithilfe des Experience Data Model (XDM) Datumsfeldern zugeordnet werden, sollte das Datumsformat explizit erwähnt werden. Wenn nicht explizit erwähnt, versucht Data Prep, die Eingabedaten zu konvertieren, indem sie mit den folgenden Formaten übereinstimmen. Sobald ein passendes Format gefunden wurde, werden alle nachfolgenden Formate nicht mehr ausgewertet.

```console
"yyyy-MM-dd HH:mm:ssZ",
"yyyy-MM-dd HH:mm:ss.SSSZ",
"yyyy-MM-dd HH:mm:ss.SSS",
"yyyy-MM-dd'T'HH:mm:ss.SSSX",
"yyyy-MM-dd'T'HH:mm:ss'Z'",
"yyyy-MM-dd",
"yyyy/MM/dd",
"yyyy.MM.dd",
"yyyy-MMM-dd",
"yyyyMMdd",
"MM-dd-yyyy",
"MMddyyyy",
"M/dd/yyyy",
"dd.M.yyyy",
"M/dd/yyyy hh:mm:ss a",
"dd.M.yyyy hh:mm:ss a",
"dd.MMM.yyyy",
"dd-MMM-yyyy"
```

>[!IMPORTANT]
>
> Data Prep versucht, Zeichenfolgen so gut wie möglich in Datumswerte umzuwandeln. Diese Konversionen können jedoch zu unerwünschten Ergebnissen führen. Der Zeichenfolgenwert &quot;12112020&quot;entspricht beispielsweise dem Muster &quot;Tag&quot;, der Benutzer hat jedoch möglicherweise beabsichtigt, das Datum mit dem Muster &quot;ddMMyyy&quot;zu lesen. Daher sollten Benutzer explizit das Datumsformat für Zeichenfolgen erwähnen.

### Datums-/Uhrzeitformat-Zeichenfolgen {#format}

Die folgende Tabelle zeigt, welche Musterbuchstaben für Formatzeichenfolgen definiert werden. Beachten Sie, dass bei den Buchstaben die Groß- und Kleinschreibung beachtet wird.

| Symbol | Bedeutung | Präsentation | Beispiel |
| ------ | ------- | ------------ | ------- |
| G | Die Zeit | Text | AD; Anno Domini; A |
| Y | Jahr, basierend auf der ISO-Woche | Nummer | 1996; 96 |
| y | Das Jahr | Nummer | 2004; 04 |
| M/L | Monat des Jahres | Zahl/Text | 7; 07; Jul; Juli; J |
| w | Woche im Jahr | Nummer | 27 |
| W | Woche des Monats | Nummer | 3 |
| D | Tag des Jahres | Nummer | 189 |
| d | Tag des Monats | Nummer | 10 |
| F | Wochentag in einem Monat | Nummer | 2 |
| E | Name des Wochentags | Text | Dienstag; Tue |
| u | Wochentag als Zahl. 1 steht für Montag, ..., 7 steht für Sonntag | Nummer | 1 |
| a | AM-/PM-Marker | Text | PM |
| H | Stunde pro Tag (0-23) | Nummer | 0 |
| k | Stunde pro Tag (1-24) | Nummer | 24 |
| K | Stunde in AM/PM (0-11) | Nummer | 0 |
| h | Stunde in AM/PM (1-12) | Nummer | 12 |
| m | Minute in der Stunde | Nummer | 38 |
| s | Sekunde in der Minute | Nummer | 44 |
| S | Millisekunde | Nummer | 245 |
| z | Zeitzone | Allgemeine Zeitzone | Pacific Standard Time; PST; GMT-08:00 |
| Z | Zeitzone | RFC 822-Zeitzone | -0800 |
| X | Zeitzone | Zeitzone nach ISO 8601 | -08; -0800; -08:00 |
| V | Zeitzone-ID | Text | Amerika/Los_Angeles |
| O | Zeitzonenversatz | Text | GMT+8 |
| Q/q | Quartal des Jahres | Zahl/Text | 3; 03; Q3; 3. Quartal |
