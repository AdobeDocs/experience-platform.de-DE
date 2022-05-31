---
keywords: Experience Platform;Startseite;beliebte Themen;CSV zuordnen;CSV-Datei zuordnen;CSV-Datei zu xdm zuordnen;CSV zu xdm zuordnen;ui-Handbuch;Mapper;Zuordnung;Datenvorbereitung;Datenvorbereitung;Vorbereiten von Daten;
solution: Experience Platform
title: Verarbeiten von Datenformaten mit der Datenvorbereitung
topic-legacy: overview
description: In diesem Dokument erhalten Sie einen Überblick darüber, wie verschiedene Datentypen von der Datenvorbereitung verarbeitet werden.
exl-id: 4ad253b7-3f83-48cd-9c46-8b5ba627c09e
source-git-commit: 15afb221a3576b7a37ea02195549f246833b800d
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 98%

---

# Verarbeiten von Datenformaten mit der Datenvorbereitung

Datenvorbereitung kann verschiedene Datenformate, die in Adobe Experience Platform erfasst werden, zuverlässig verarbeiten. In diesem Dokument wird beschrieben, wie verschiedene Datenformate von der Datenvorbereitung verarbeitet werden.

## Boolesche Werte {#booleans}

Wenn der Quelltyp eine Zeichenfolge und der Zieltyp ein boolescher Wert ist, kann die Datenvorbereitung den Wert automatisch analysieren und den Quellwert in einen booleschen Wert konvertieren.

Die Werte `y`, `yes`, `Y`, `YES`, `on`, `ON`, `true` und `TRUE` werden so verarbeitet, dass sie automatisch zu `true` werden.

Die Werte `n`, `N`, `no`, `NO`, `off`, `OFF`, `false` und `FALSE` werden so verarbeitet, dass sie automatisch zu `false` werden.

## Daten {#dates}

Datenvorbereitung unterstützt Datumsfunktionen sowohl in Form von Zeichenfolgen als auch in Form von Datetime-Objekten.

### Datumsfunktion-Format

Die Datumsfunktion konvertiert Zeichenfolgen und Datetime-Objekte in ein nach ISO 8601 formatiertes ZonedDateTime-Objekt.

**Format**

```http
date({DATE}, {FORMAT}, {DEFAULT_DATE})
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{DATE}` | Erforderlich. Die Zeichenfolge, die das Datum darstellt. |
| `{FORMAT}` | Optional. Die Zeichenfolge, die das Format des Quelldatums darstellt. Weitere Informationen zur Zeichenfolgenformatierung finden Sie im Abschnitt zu [Zeichenfolgen im Datums-/Zeitformat](#format). |
| `{DEFAULT_DATE}` | Optional. Das Standarddatum, das zurückgegeben werden soll, wenn das angegebene Datum null ist. |

Der Ausdruck `date(orderDate, "yyyy-MM-dd")` konvertiert den Wert `orderDate` beispielsweise von „31. Dezember 2020“ in den Datetime-Wert „2020-12-31“.

### Konvertierungen von Datumsfunktionen

Wenn Zeichenfolgenfelder aus eingehenden Daten mithilfe des Experience-Datenmodells (XDM) Datumsfeldern in Schemas zugeordnet werden, sollte das Datumsformat explizit angegeben werden. Wenn es nicht explizit angegeben ist, versucht Datenvorbereitung, die Eingabedaten zu konvertieren, indem sie mit folgenden Formaten abgeglichen werden. Sobald ein passendes Format gefunden wurde, wird die Auswertung aller nachfolgenden Formate beendet.

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
> Datenvorbereitung versucht, Zeichenfolgen so gut wie möglich in Daten zu konvertieren. Solche Konversionen können jedoch zu unerwünschten Ergebnissen führen. Der Zeichenfolgenwert „12112020“ entspricht beispielsweise dem Muster „MMddyyyy“, der Benutzer hat jedoch ggf. beabsichtigt, dass das Datum dem Muster „ddMMyyyy“ folgt. Darum sollten Benutzer das Datumsformat für Zeichenfolgen explizit angeben.

### Zeichenfolgen im Datum/Zeit-Format {#format}

Die folgende Tabelle zeigt, welche Musterbuchstaben für Formatzeichenfolgen definiert sind. Beachten Sie, dass bei den Buchstaben die Groß- und Kleinschreibung beachtet wird.

| Symbol | Bedeutung | Präsentation | Beispiel |
| ------ | ------- | ------------ | ------- |
| G | Die Jahreszählung | Text | AD; Anno Domini, A |
| Y | Jahr, basierend auf der ISO-Woche | Zahl | 1996; 96 |
| y | Das Jahr | Zahl | 2004; 04 |
| M/L | Monat des Jahres | Zahl/Text | 7; 07; Jul; Juli; J |
| w | Woche im Jahr | Zahl | 27 |
| W | Woche des Monats | Zahl | 3 |
| D | Tag des Jahres | Zahl | 189 |
| d | Tag des Monats | Zahl | 10 |
| F | Wochentag in einem Monat | Zahl | 2 |
| E | Name des Wochentags | Text | Dienstag; Di |
| u | Wochentag als Zahl. 1 steht für Montag, ..., 7 steht für Sonntag | Zahl | 1 |
| a | AM/PM-Markierung | Text | PM |
| H | Uhrzeit (0-23) | Zahl | 0 |
| k | Uhrzeit (1-24) | Zahl | 24 |
| K | Uhrzeit in AM/PM (0-11) | Zahl | 0 |
| h | Uhrzeit in AM/PM (1-12) | Zahl | 12 |
| m | Minute in der Stunde | Zahl | 38 |
| s | Sekunde in der Minute | Zahl | 44 |
| S | Millisekunde | Zahl | 245 |
| z | Zeitzone | Allgemeine Zeitzone | Pacific Standard Time; PST; GMT-08:00 |
| Z | Zeitzone | RFC 822-Zeitzone | -0800 |
| X | Zeitzone | ISO 8601-Zeitzone | -08; -0800; -08:00 |
| V | Zeitzonen-ID | Text | America/Los_Angeles |
| O | Zeitzonenversatz | Text | GMT+8 |
| Q/q | Quartal des Jahres | Zahl/Text | 3; 03; Q3; 3. Quartal |

## Karten {#maps}

Karten werden derzeit nicht in [!DNL Data Prep].
