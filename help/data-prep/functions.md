---
keywords: Experience Platform;home;popular topics;map csv;map csv file;map csv file;map csv file to xdm;map csv to xdm;ui guide;mapper;mapping;fields;mapping fields;mapping features;
solution: Experience Platform
title: Zuordnungsfunktionen für Datenvorbereitung
description: In diesem Dokument werden die mit der Datenvorbereitung verwendeten Zuordnungsfunktionen vorgestellt.
exl-id: e95d9329-9dac-4b54-b804-ab5744ea6289
source-git-commit: 830aa01828785a9ae4dea71078ee418fc510253c
workflow-type: tm+mt
source-wordcount: '6028'
ht-degree: 3%

---

# Funktionen zur Datenvorbereitung

Mit Datenvorbereitung-Funktionen können Werte basierend auf den in Quellfeldern eingegebenen Werten berechnet und berechnet werden.

## Felder

Ein Feldname kann eine beliebige gültige Kennung sein - eine unbegrenzte Sequenz von Unicode-Buchstaben und -Ziffern, beginnend mit einem Buchstaben, dem Dollarzeichen (`$`) oder dem Unterstrich (`_`). Bei Variablennamen wird auch zwischen Groß- und Kleinschreibung unterschieden.

Wenn ein Feldname dieser Konvention nicht entspricht, muss der Feldname mit `${}` umschlossen werden. Wenn der Feldname beispielsweise &quot;Vorname&quot;oder &quot;Vorname&quot;lautet, muss der Name wie `${First Name}` bzw. `${First\.Name}` umgebrochen werden.

>[!TIP]
>
>Wenn Sie mit Hierarchien arbeiten und ein untergeordnetes Attribut einen Punkt (`.`) enthält, müssen Sie einen Backslash (`\`) verwenden, um Sonderzeichen zu umgehen. Weitere Informationen finden Sie in der Anleitung zu [Maskieren von Sonderzeichen](home.md#escape-special-characters).

Wenn der Feldname **beliebig** der folgenden reservierten Schlüsselwörter ist, muss er mit `${}{}` umschlossen werden:

```console
new, mod, or, break, var, lt, for, false, while, eq, gt, div, not, null, continue, else, and, ne, true, le, if, ge, return, _errors, do, function, empty, size
```

Darüber hinaus enthalten reservierte Schlüsselwörter auch eine der auf dieser Seite aufgelisteten Zuordnungsfunktionen.

Auf Daten in Unterfeldern kann mithilfe der Punktnotation zugegriffen werden. Wenn beispielsweise ein `name` -Objekt vorhanden war, verwenden Sie `name.firstName`, um auf das Feld `firstName` zuzugreifen.

## Funktionsliste

In den folgenden Tabellen sind alle unterstützten Zuordnungsfunktionen aufgeführt, einschließlich Beispielausdrücke und der resultierenden Ausgaben.

### Zeichenfolgen-Funktionen {#string}

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Funktion | Beschreibung | Parameter | Aufbau | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| concat | Verkettet die angegebenen Zeichenfolgen. | <ul><li>STRING: Die verketteten Zeichenfolgen.</li></ul> | concat(STRING_1, STRING_2) | concat(&quot;Hi, &quot;, &quot;There&quot;, &quot;!&quot;) | `"Hi, there!"` |
| explode | Teilt die Zeichenfolge basierend auf einem Regex und gibt ein Array von Teilen zurück. Kann optional regex enthalten, um die Zeichenfolge zu teilen. Standardmäßig wird die Aufteilung in &quot;,&quot;aufgelöst. Die folgenden Trennzeichen **müssen** mit `\` maskieren: `+, ?, ^, \|, ., [, (, {, ), *, $, \` Wenn Sie mehrere Zeichen als Trennzeichen einschließen, wird das Trennzeichen als Trennzeichen mit mehreren Zeichen behandelt. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, die geteilt werden muss.</li><li>REGEX: *Optional* Der reguläre Ausdruck, der zum Aufteilen der Zeichenfolge verwendet werden kann.</li></ul> | explode(STRING, REGEX) | explode(&quot;Hallo, da!&quot;, &quot;&quot;) | `["Hi,", "there"]` |
| instr | Gibt die Position/den Index einer Unterzeichenfolge zurück. | <ul><li>EINGABE: **Erforderlich** Die Zeichenfolge, die gesucht wird.</li><li>SUBSTRING: **Erforderlich** Die Unterzeichenfolge, nach der in der Zeichenfolge gesucht wird.</li><li>START_POSITION: *Optional* Der Ort, an dem die Suche in der Zeichenfolge beginnen soll.</li><li>VORKOMMEN: *Optional* Das n-te Vorkommen, nach dem von der Startposition aus gesucht werden soll. Standardmäßig ist dies 1. </li></ul> | instr(INPUT, SUBSTRING, START_POSITION, OCCURRENCE) | instr(&quot;adobe.com&quot;, &quot;com&quot;) | 6 |
| replacestr | Ersetzt die Suchzeichenfolge, sofern sie in der ursprünglichen Zeichenfolge vorhanden ist. | <ul><li>EINGABE: **Erforderlich** Die Eingabezeichenfolge.</li><li>TO_FIND: **Erforderlich** Die Zeichenfolge, die in der Eingabe nachgeschlagen werden soll.</li><li>TO_REPLACE: **Erforderlich** Die Zeichenfolge, die den Wert in &quot;TO_FIND&quot;ersetzt.</li></ul> | replace(INPUT, TO_FIND, TO_REPLACE) | replacestr(&quot;This is a string re test&quot;, &quot;re&quot;, &quot;replace&quot;) | &quot;Dies ist ein string replace-Test&quot; |
| substr | Gibt eine Teilzeichenfolge einer angegebenen Länge zurück. | <ul><li>EINGABE: **Erforderlich** Die Eingabezeichenfolge.</li><li>START_INDEX: **Erforderlich** Der Index der Eingabezeichenfolge, in der die Teilzeichenfolge beginnt.</li><li>LÄNGE: **Erforderlich** Die Länge der Unterzeichenfolge.</li></ul> | substr(INPUT, START_INDEX, LENGTH) | substr(&quot;This is a substring test&quot;, 7, 8) | &quot;a subst&quot; |
| lower /<br>lcase | Konvertiert einen String in Kleinbuchstaben. | <ul><li>EINGABE: **Erforderlich** Die Zeichenfolge, die in Kleinbuchstaben konvertiert wird.</li></ul> | lower(INPUT) | lower(&quot;HeLLo&quot;)<br>lcase(&quot;HeLLo&quot;) | &quot;hello&quot; |
| upper /<br>ucase | Konvertiert einen String in Großbuchstaben. | <ul><li>EINGABE: **Erforderlich** Die Zeichenfolge, die in Großbuchstaben umgewandelt wird.</li></ul> | upper(INPUT) | upper(&quot;HeLLo&quot;)<br>ucase(&quot;HeLLo&quot;) | &quot;HELLO&quot; |
| split | Teilt eine Eingabezeichenfolge auf einem Trennzeichen. Das folgende Trennzeichen **muss** mit `\` maskieren: `\`. Wenn Sie mehrere Trennzeichen einschließen, wird die Zeichenfolge auf **beliebige** der in der Zeichenfolge vorhandenen Trennzeichen aufgeteilt. **Hinweis:** Diese Funktion gibt nur Indizes zurück, die nicht null sind, unabhängig davon, ob das Trennzeichen vorhanden ist. Wenn alle Indizes, einschließlich Nullen, im resultierenden Array erforderlich sind, verwenden Sie stattdessen die Funktion &quot;explode&quot;. | <ul><li>EINGABE: **Erforderlich** Die Eingabezeichenfolge, die geteilt werden soll.</li><li>SEPARATOR: **Erforderlich** Die Zeichenfolge, die zum Aufteilen der Eingabe verwendet wird.</li></ul> | split(INPUT, SEPARATOR) | split(&quot;Hello World&quot;, &quot;&quot;) | `["Hello", "world"]` |
| join | Verbindet eine Liste von Objekten mithilfe des Trennzeichens. | <ul><li>SEPARATOR: **Erforderlich** Die Zeichenfolge, die zum Verknüpfen der Objekte verwendet wird.</li><li>OBJEKTE: **Erforderlich** Ein Array von Zeichenfolgen, die verknüpft werden.</li></ul> | `join(SEPARATOR, [OBJECTS])` | `join(" ", to_array(true, "Hello", "world"))` | &quot;Hello World&quot; |
| lpad | Fügt die linke Seite einer Zeichenfolge mit der anderen angegebenen Zeichenfolge ein. | <ul><li>EINGABE: **Erforderlich** Die Zeichenfolge, die eingefügt werden soll. Diese Zeichenfolge kann null sein.</li><li>COUNT: **Erforderlich** Die Größe der Zeichenfolge, die eingefügt werden soll.</li><li>HINZUFÜGEN: **Erforderlich** Die Zeichenfolge, mit der die Eingabe aufgefüllt werden soll. Wenn null oder leer, wird es als einzelnes Leerzeichen behandelt.</li></ul> | lpad(INPUT, COUNT, PADDING) | lpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;yzyzybat&quot; |
| rpad | Fügt die rechte Seite einer Zeichenfolge mit der anderen angegebenen Zeichenfolge ein. | <ul><li>EINGABE: **Erforderlich** Die Zeichenfolge, die eingefügt werden soll. Diese Zeichenfolge kann null sein.</li><li>COUNT: **Erforderlich** Die Größe der Zeichenfolge, die eingefügt werden soll.</li><li>HINZUFÜGEN: **Erforderlich** Die Zeichenfolge, mit der die Eingabe aufgefüllt werden soll. Wenn null oder leer, wird es als einzelnes Leerzeichen behandelt.</li></ul> | rpad(INPUT, COUNT, PADDING) | rpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;batyzyzy&quot; |
| left | Ruft die ersten n Zeichen der angegebenen Zeichenfolge ab. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, für die Sie die ersten &quot;n&quot;-Zeichen erhalten.</li><li>COUNT: **Erforderlich** Die &quot;n&quot;-Zeichen, die Sie aus der Zeichenfolge abrufen möchten.</li></ul> | left(STRING, COUNT) | left(&quot;abcde&quot;, 2) | &quot;ab&quot; |
| right | Ruft die letzten n Zeichen der angegebenen Zeichenfolge ab. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, für die Sie die letzten &quot;n&quot;-Zeichen erhalten.</li><li>COUNT: **Erforderlich** Die &quot;n&quot;-Zeichen, die Sie aus der Zeichenfolge abrufen möchten.</li></ul> | right(STRING, COUNT) | right(&quot;abcde&quot;, 2) | &quot;de&quot; |
| ltrim | Entfernt den Leerraum am Anfang des Strings. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, aus der Sie den Leerraum entfernen möchten.</li></ul> | ltrim(STRING) | ltrim(&quot; hello&quot;) | &quot;hello&quot; |
| rtrim | Entfernt den Leerraum am Ende des Strings. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, aus der Sie den Leerraum entfernen möchten.</li></ul> | rtrim(STRING) | rtrim(&quot;hello &quot;) | &quot;hello&quot; |
| trim | Entfernt den Leerraum vom Anfang und vom Ende der Zeichenfolge. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, aus der Sie den Leerraum entfernen möchten.</li></ul> | trim(STRING) | trim(&quot; hello &quot;) | &quot;hello&quot; |
| ist gleich | Vergleicht zwei Zeichenketten, um sicherzustellen, dass sie gleich sind. Diese Funktion unterscheidet zwischen Groß- und Kleinschreibung. | <ul><li>STRING1: **Erforderlich** Die erste Zeichenfolge, die Sie vergleichen möchten.</li><li>STRING2: **Erforderlich** Die zweite Zeichenfolge, die Sie vergleichen möchten.</li></ul> | STRING1. &#x200B;equals( &#x200B; STRING2) | &quot;string1&quot;. &#x200B;equals &#x200B;(&quot;STRING1&quot;) | false |
| equalsIgnoreCase | Vergleicht zwei Zeichenketten, um sicherzustellen, dass sie gleich sind. Bei dieser Funktion wird zwischen Groß- und Kleinschreibung unterschieden: **nicht**. | <ul><li>STRING1: **Erforderlich** Die erste Zeichenfolge, die Sie vergleichen möchten.</li><li>STRING2: **Erforderlich** Die zweite Zeichenfolge, die Sie vergleichen möchten.</li></ul> | STRING1. &#x200B;equalsIgnoreCase &#x200B;(STRING2) | &quot;string1&quot;. &#x200B;equalsIgnoreCase &#x200B;(&quot;STRING1) | wahr |

{style="table-layout:auto"}

### Funktionen mit reguläreren Ausdrücken

| Funktion | Beschreibung | Parameter | Aufbau | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| extract_regex | Extrahiert basierend auf einem regulären Ausdruck Gruppen aus der Eingabezeichenfolge. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, aus der Sie die Gruppen extrahieren.</li><li>REGEX: **Erforderlich** Der reguläre Ausdruck, mit dem die Gruppe übereinstimmen soll.</li></ul> | extract_regex(STRING, REGEX) | extract_regex &#x200B;(&quot;E259,E259B_009,1_1&quot; &#x200B;, &quot;([^,]+),[^,]*,([^,]+)&quot;) | [&quot;E259,E259B_009,1_1&quot;, &quot;E259&quot;, &quot;1_1&quot;] |
| matches_regex | Überprüft, ob die Zeichenfolge mit dem eingegebenen regulären Ausdruck übereinstimmt. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, die Sie überprüfen, entspricht dem regulären Ausdruck.</li><li>REGEX: **Erforderlich** Der reguläre Ausdruck, mit dem Sie vergleichen.</li></ul> | matches_regex(STRING, REGEX) | matches_regex(&quot;E259,E259B_009,1_1&quot;, &quot;([^,]+),[^,]*,([^,]+)&quot;) | wahr |

{style="table-layout:auto"}

### Hashfunktionen {#hashing}

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Funktion | Beschreibung | Parameter | Aufbau | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| sha1 | Nimmt eine Eingabe und erzeugt einen Hash-Wert mit Secure Hash Algorithm 1 (SHA-1). | <ul><li>EINGABE: **Erforderlich** Der Klartext, der gehasht werden soll.</li><li>CHARSET: *Optional* Der Name des Zeichensatzes. Mögliche Werte sind UTF-8, UTF-16, ISO-8859-1 und US-ASCII.</li></ul> | sha1(INPUT, CHARSET) | sha1(&quot;my text&quot;, &quot;UTF-8&quot;) | c3599c11e47719df18a24 &#x200B; 48690840c5dfcce3c80 |
| sha256 | Nimmt eine Eingabe und erzeugt einen Hash-Wert mithilfe des Secure Hash Algorithm 256 (SHA-256). | <ul><li>EINGABE: **Erforderlich** Der Klartext, der gehasht werden soll.</li><li>CHARSET: *Optional* Der Name des Zeichensatzes. Mögliche Werte sind UTF-8, UTF-16, ISO-8859-1 und US-ASCII.</li></ul> | sha256(INPUT, CHARSET) | sha256(&quot;my text&quot;, &quot;UTF-8&quot;) | 7330d2b39ca35eaf4cb95fc846c21 &#x200B; ee6a39af698154a83a586ee270a0d372104 |
| sha512 | Nimmt eine Eingabe und erzeugt einen Hash-Wert mithilfe des Secure Hash Algorithm 512 (SHA-512). | <ul><li>EINGABE: **Erforderlich** Der Klartext, der gehasht werden soll.</li><li>CHARSET: *Optional* Der Name des Zeichensatzes. Mögliche Werte sind UTF-8, UTF-16, ISO-8859-1 und US-ASCII.</li></ul> | sha512(INPUT, CHARSET) | sha512(&quot;my text&quot;, &quot;UTF-8&quot;) | a3d7e45a0d9be5fd4e4b9a3b8c9c2163c21ef &#x200B; 708bf11b4232bb21d2a8704ada2cdcd7b367dd07 88a89 &#x200B; a5c908cfe377aceb1072a7b386b7d4fd2ff68a8fd24d16 |
| md5 | Nimmt eine Eingabe und erzeugt einen Hash-Wert mit MD5. | <ul><li>EINGABE: **Erforderlich** Der Klartext, der gehasht werden soll.</li><li>CHARSET: *Optional* Der Name des Zeichensatzes. Mögliche Werte sind UTF-8, UTF-16, ISO-8859-1 und US-ASCII. </li></ul> | md5(INPUT, CHARSET) | md5(&quot;my text&quot;, &quot;UTF-8&quot;) | d3b96ce8c9fb4 &#x200B; e9bd0198d03ba6852c7 |
| crc32 | Eine Eingabe verwendet einen CRC-Algorithmus (zyklische Redundanzprüfung), um einen 32-Bit-zyklischen Code zu erzeugen. | <ul><li>EINGABE: **Erforderlich** Der Klartext, der gehasht werden soll.</li><li>CHARSET: *Optional* Der Name des Zeichensatzes. Mögliche Werte sind UTF-8, UTF-16, ISO-8859-1 und US-ASCII.</li></ul> | crc32(INPUT, CHARSET) | crc32(&quot;my text&quot;, &quot;UTF-8&quot;) | 8df92e80 |

{style="table-layout:auto"}

### URL-Funktionen {#url}

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Funktion | Beschreibung | Parameter | Aufbau | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| get_url_protocol | Gibt das Protokoll aus der angegebenen URL zurück. Wenn die Eingabe ungültig ist, wird null zurückgegeben. | <ul><li>URL: **Erforderlich** Die URL, aus der das Protokoll extrahiert werden muss.</li></ul> | get_url_protocol &#x200B;(URL) | get_url_protocol(&quot;https://platform &#x200B; .adobe.com/home&quot;) | https |
| get_url_host | Gibt den Host der angegebenen URL zurück. Wenn die Eingabe ungültig ist, wird null zurückgegeben. | <ul><li>URL: **Erforderlich** Die URL, aus der der Host extrahiert werden muss.</li></ul> | get_url_host &#x200B;(URL) | get_url_host &#x200B;(&quot;https://platform &#x200B; .adobe.com/home&quot;) | platform.adobe.com |
| get_url_port | Gibt den Port der angegebenen URL zurück. Wenn die Eingabe ungültig ist, wird null zurückgegeben. | <ul><li>URL: **Erforderlich** Die URL, aus der der Port extrahiert werden muss.</li></ul> | get_url_port(URL) | get_url_port &#x200B;(&quot;sftp://example.com//home/ &#x200B; joe/employee.csv&quot;) | 22 |
| get_url_path | Gibt den Pfad der angegebenen URL zurück. Standardmäßig wird der vollständige Pfad zurückgegeben. | <ul><li>URL: **Erforderlich** Die URL, aus der der Pfad extrahiert werden muss.</li><li>FULL_PATH: *Optional* Ein boolescher Wert, der bestimmt, ob der vollständige Pfad zurückgegeben wird. Wenn der Wert auf &quot;false&quot;gesetzt ist, wird nur das Ende des Pfads zurückgegeben.</li></ul> | get_url_path &#x200B;(URL, FULL_PATH) | get_url_path &#x200B;(&quot;sftp://example.com// &#x200B; home/joe/employee.csv&quot;) | &quot;//home/joe/&#x200B; employee.csv&quot; |
| get_url_query_str | Gibt die Abfragezeichenfolge einer angegebenen URL als Zuordnung des Abfragezeichenfolgennamens und des Abfragezeichenfolgenwerts zurück. | <ul><li>URL: **Erforderlich** Die URL, von der Sie die Abfragezeichenfolge abrufen möchten.</li><li>ANCHOR: **Erforderlich** Bestimmt, was mit dem Anker in der Abfragezeichenfolge ausgeführt wird. Kann einer von drei Werten sein: &quot;keep&quot;, &quot;remove&quot;oder &quot;append&quot;.<br><br>Wenn der Wert &quot;keep&quot;ist, wird der Anker an den zurückgegebenen Wert angehängt.<br>Wenn der Wert &quot;remove&quot;ist, wird der Anker aus dem zurückgegebenen Wert entfernt.<br>Wenn der Wert &quot;append&quot;ist, wird der Anker als separater Wert zurückgegeben.</li></ul> | get_url_query_str &#x200B;(URL, ANCHOR) | get_url_query_str &#x200B;(&quot;foo://example.com:8042 &#x200B;/over/dahin?name= &#x200B; ferret#nose&quot;, &quot;keep&quot;)<br>get_url_query_str &#x200B;(&quot;foo://example.com:8042 &#x200B;/over/dahin?name= &#x200B; ferret#nose&quot;, &quot;remove&quot;)<br>get_url_query_str &#x200B;(&quot;foo://example.com:8042/over/then?name ferret#nose&quot;, &quot;append&quot;) | `{"name": "ferret#nose"}`<br>`{"name": "ferret"}`<br>`{"name": "ferret", "_anchor_": "nose"}` |
| get_url_encoded | Diese Funktion akzeptiert eine URL als Eingabe und ersetzt oder kodiert die Sonderzeichen durch ASCII-Zeichen. Weitere Informationen zu Sonderzeichen finden Sie in der [Liste der Sonderzeichen](#special-characters) im Anhang dieses Dokuments. | <ul><li>URL: **Erforderlich** Die Eingabe-URL mit Sonderzeichen, die Sie ersetzen oder durch ASCII-Zeichen kodieren möchten.</li></ul> | get_url_encoded(URL) | get_url_encoded(&quot;https</span>://example.com/partneralliance_asia-pacific_2022&quot;) | https%3A%2F%2Fexample.com%2Fpartneralliance_asia-pacific_2022 |
| get_url_decoded | Diese Funktion akzeptiert eine URL als Eingabe und dekodiert die ASCII-Zeichen in Sonderzeichen.  Weitere Informationen zu Sonderzeichen finden Sie in der [Liste der Sonderzeichen](#special-characters) im Anhang dieses Dokuments. | <ul><li>URL: **Erforderlich** Die Eingabe-URL mit ASCII-Zeichen, die Sie in Sonderzeichen dekodieren möchten.</li></ul> | get_url_decoded(URL) | get_url_decoded(&quot;https%3A%2F%2Fexample.com%2Fpartneralliance_asia-pacific_2022&quot;) | https</span>://example.com/partneralliance_asia-pacific_2022 |

{style="table-layout:auto"}

### Datums- und Uhrzeitfunktionen {#date-and-time}

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen. Weitere Informationen zur Funktion `date` finden Sie im Abschnitt &quot;Datumsangaben&quot;des Handbuchs zur Verarbeitung von [Datenformaten](./data-handling.md#dates).

| Funktion | Beschreibung | Parameter | Aufbau | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| now | Ruft die aktuelle Zeit ab. | | now() | now() | `2021-10-26T10:10:24Z` |
| Zeitstempel | Ruft die aktuelle Unix-Zeit ab. | | timestamp() | timestamp() | 1571850624571 |
| format | Formatiert das Eingabedatum in einem angegebenen Format. | <ul><li>DATUM: **Erforderlich** Das Eingabedatum, das Sie formatieren möchten, als ZonedDateTime-Objekt.</li><li>FORMAT: **Erforderlich** Das Format, in das das Datum geändert werden soll.</li></ul> | format(DATE, FORMAT) | format(2019-10-23T11:24:00+00:00, &quot;`yyyy-MM-dd HH:mm:ss`&quot;) | `2019-10-23 11:24:35` |
| dformat | Konvertiert einen Zeitstempel in eine Datums-Zeichenfolge in einem angegebenen Format. | <ul><li>TIMESTAMP: **Erforderlich** Der Zeitstempel, den Sie formatieren möchten. Dies wird in Millisekunden geschrieben.</li><li>FORMAT: **Erforderlich** Das Format, in das der Zeitstempel umgewandelt werden soll.</li></ul> | dformat(TIMESTAMP, FORMAT) | dformat(1571829875000, &quot;`yyyy-MM-dd'T'HH:mm:ss.SSSX`&quot;) | `2019-10-23T11:24:35.000Z` |
| date | Konvertiert eine Datums-Zeichenfolge in ein ZonedDateTime-Objekt (ISO 8601-Format). | <ul><li>DATUM: **Erforderlich** Die Zeichenfolge, die das Datum darstellt.</li><li>FORMAT: **Erforderlich** Die Zeichenfolge, die das Format des Quelldatums darstellt.**Hinweis:** Dies entspricht **nicht** dem Format, in das Sie die Datums-Zeichenfolge konvertieren möchten. </li><li>DEFAULT_DATE: **Erforderlich** Das zurückgegebene Standarddatum, wenn das angegebene Datum null ist.</li></ul> | date(DATE, FORMAT, DEFAULT_DATE) | date(&quot;2019-10-23 11:24&quot;, &quot;yyy-MM-dd HH:mm&quot;, now()) | `2019-10-23T11:24:00Z` |
| date | Konvertiert eine Datums-Zeichenfolge in ein ZonedDateTime-Objekt (ISO 8601-Format). | <ul><li>DATUM: **Erforderlich** Die Zeichenfolge, die das Datum darstellt.</li><li>FORMAT: **Erforderlich** Die Zeichenfolge, die das Format des Quelldatums darstellt.**Hinweis:** Dies entspricht **nicht** dem Format, in das Sie die Datums-Zeichenfolge konvertieren möchten. </li></ul> | date(DATE, FORMAT) | date(&quot;2019-10-23 11:24&quot;, &quot;yyy-MM-dd HH:mm&quot;) | `2019-10-23T11:24:00Z` |
| date | Konvertiert eine Datums-Zeichenfolge in ein ZonedDateTime-Objekt (ISO 8601-Format). | <ul><li>DATUM: **Erforderlich** Die Zeichenfolge, die das Datum darstellt.</li></ul> | date(DATE) | date(&quot;2019-10-23 11:24&quot;) | &quot;2019-10-23T11:24:00Z&quot; |
| date_part | Ruft die Datumsbereiche ab. Die folgenden Komponentenwerte werden unterstützt: <br><br>&quot;year&quot;<br>&quot;yyy&quot;<br>&quot;yy&quot;<br><br>&quot;quarter&quot;<br>&quot;qq&quot;<br>&quot;q&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;dayofyear&quot;<br>&quot;dy&quot;<br>&quot;y&quot;<br><br>&quot;day&quot; 13}&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;week&quot;<br>&quot;ww&quot;<br>&quot;w&quot;<br><br>&quot;week day&quot;<br>&quot;dw&quot;<br>&quot;w&quot;<br><br>&quot;hour&quot;<br>&quot;hh&quot;<br>&quot;hh24&quot;<br>&quot;hh12&quot;<br><br>&quot;minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;second&quot;<br>&quot;ss&quot;<br>&quot;s&quot;<br><br>&quot;millisecond&quot;<br>&quot;SSS&quot;<br> | <ul><li>KOMPONENTE: **Erforderlich** Eine Zeichenfolge, die den Teil des Datums darstellt. </li><li>DATUM: **Erforderlich** Das Datum im Standardformat.</li></ul> | date_part &#x200B;(COMPONENT, DATE) | date_part(&quot;MM&quot;, date(&quot;2019-10-17 11:55:12&quot;)) | 10 |
| set_date_part | Ersetzt eine Komponente an einem bestimmten Datum. Die folgenden Komponenten werden akzeptiert: <br><br>&quot;year&quot;<br>&quot;yyy&quot;<br>&quot;yy&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;hour&quot;<br>&quot;hh&quot;<br><br>&quot;minute&quot;<br>&quot;mi&quot;<br> &quot;n&quot;<br><br>&quot;second&quot;<br>&quot;ss&quot;<br>&quot;s&quot; | <ul><li>KOMPONENTE: **Erforderlich** Eine Zeichenfolge, die den Teil des Datums darstellt. </li><li>WERT: **Erforderlich** Der Wert, der für die Komponente für ein bestimmtes Datum festgelegt werden soll.</li><li>DATUM: **Erforderlich** Das Datum im Standardformat.</li></ul> | set_date_part &#x200B;(COMPONENT, VALUE, DATE) | set_date_part(&quot;m&quot;, 4, date(&quot;2016-11-09T11:44:44.797&quot;) | &quot;2016-04-09T11:44:44Z&quot; |
| make_date_time | Erstellt ein Datum aus Teilen. Diese Funktion kann auch mit make_timestamp ausgelöst werden. | <ul><li>JAHR: **Erforderlich** Das Jahr, bestehend aus vier Ziffern.</li><li>MONAT: **Erforderlich** Der Monat. Die zulässigen Werte sind 1 bis 12.</li><li>TAG: **Erforderlich** Der Tag. Die zulässigen Werte sind 1 bis 31.</li><li>STUNDE: **Erforderlich** Die Stunde. Die zulässigen Werte sind 0 bis 23.</li><li>MINUTE: **Erforderlich** Die Minute. Die zulässigen Werte sind 0 bis 59.</li><li>NANOSECOND: **Erforderlich** Die Nanosekundenwerte. Die zulässigen Werte sind 0 bis 999999999.</li><li>ZEITZONE: **Erforderlich** Die Zeitzone für die Datumszeit.</li></ul> | make_date_time &#x200B;(YEAR, MONTH, DAY, HOUR, MINUTE, SECOND, NANOSECOND, TIMEZONE) | make_date_time &#x200B;(2019, 10, 17, 11, 55, 12, 999, &quot;America/Los_Angeles&quot;) | `2019-10-17T11:55:12Z` |
| zone_date_to_utc | Konvertiert ein Datum in einer beliebigen Zeitzone in ein Datum in UTC. | <ul><li>DATUM: **Erforderlich** Das Datum, das Sie konvertieren möchten.</li></ul> | zone_date_to_utc &#x200B;(DATE) | `zone_date_to_utc&#x200B;(2019-10-17T11:55:&#x200B;12 PST` | `2019-10-17T19:55:12Z` |
| zone_date_to_zone | Konvertiert ein Datum aus einer Zeitzone in eine andere Zeitzone. | <ul><li>DATUM: **Erforderlich** Das Datum, das Sie konvertieren möchten.</li><li>ZONE: **Erforderlich** Die Zeitzone, in die Sie das Datum konvertieren möchten.</li></ul> | zone_date_to_zone &#x200B;(DATE, ZONE) | `zone_date_to_zone(now(), "Europe/Paris")` | `2021-10-26T15:43:59Z` |

{style="table-layout:auto"}

### Hierarchien - Objekte {#objects}

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Funktion | Beschreibung | Parameter | Aufbau | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| is_empty | Prüft, ob ein Objekt leer ist. | <ul><li>EINGABE: **Erforderlich** Das Objekt, das Sie überprüfen möchten, ist leer.</li></ul> | is_empty(INPUT) | `is_empty([1, null, 2, 3])` | false |
| arrays_to_object | Erstellt eine Liste von Objekten. | <ul><li>EINGABE: **Erforderlich** Eine Gruppierung von Schlüssel- und Array-Paaren.</li></ul> | arrays_to_object(INPUT) | `arrays_to_objects('sku', explode("id1\|id2", '\\\|'), 'price', [22.5,14.35])` | ```[{ "sku": "id1", "price": 22.5 }, { "sku": "id2", "price": 14.35 }]``` |
| to_object | Erstellt ein Objekt basierend auf den angegebenen flachen Schlüssel/Wert-Paaren. | <ul><li>EINGABE: **Erforderlich** Eine flache Liste von Schlüssel/Wert-Paaren.</li></ul> | to_object(INPUT) | to_object &#x200B;(&quot;firstName&quot;, &quot;John&quot;, &quot;lastName&quot;, &quot;Doe&quot;) | `{"firstName": "John", "lastName": "Doe"}` |
| str_to_object | Erstellt ein Objekt aus der Eingabezeichenfolge. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, die zum Erstellen eines Objekts analysiert wird.</li><li>VALUE_DELIMITER: *Optional* Das Trennzeichen, das ein Feld vom Wert trennt. Das Standardtrennzeichen ist `:`.</li><li>FIELD_DELIMITER: *Optional* Das Trennzeichen, das Feldwertpaare trennt. Das Standardtrennzeichen ist `,`.</li></ul> | str_to_object &#x200B;(STRING, VALUE_DELIMITER, FIELD_DELIMITER) **Hinweis**: Sie können die Funktion `get()` zusammen mit `str_to_object()` verwenden, um Werte für die Schlüssel in der Zeichenfolge abzurufen. | <ul><li>Beispiel 1: str_to_object(&quot;firstName - John ; lastName - ; - 123 345 7890&quot;, &quot;-&quot;, &quot;;&quot;)</li><li>Beispiel 2: str_to_object(&quot;firstName - John ; lastName - ; phone - 123 456 7890&quot;, &quot;-&quot;, &quot;;&quot;).get(&quot;firstName&quot;)</li></ul> | <ul><li>Beispiel 1:`{"firstName": "John", "lastName": "Doe", "phone": "123 456 7890"}`</li><li>Beispiel 2: &quot;John&quot;</li></ul> |
| contains_key | Überprüft, ob das Objekt in den Quelldaten vorhanden ist. **Hinweis:** Diese Funktion ersetzt die veraltete Funktion `is_set()`. | <ul><li>EINGABE: **Erforderlich** Der Pfad, der überprüft werden soll, wenn er in den Quelldaten vorhanden ist.</li></ul> | contains_key(INPUT) | contains_key(&quot;evars.evar.field1&quot;) | wahr |
| nullify | Legt den Wert des Attributs auf `null` fest. Dies sollte verwendet werden, wenn Sie das Feld nicht in das Zielschema kopieren möchten. | | nullify() | nullify() | `null` |
| get_keys | Analysiert die Schlüssel/Wert-Paare und gibt alle Schlüssel zurück. | <ul><li>OBJECT: **Required** Das Objekt, aus dem die Schlüssel extrahiert werden.</li></ul> | get_keys(OBJECT) | get_keys({&quot;book1&quot;: &quot;Pride and Prejustice&quot;, &quot;book2&quot;: &quot;1984&quot;}) | `["book1", "book2"]` |
| get_values | Analysiert die Schlüssel-Wert-Paare und gibt den Wert der Zeichenfolge basierend auf dem angegebenen Schlüssel zurück. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, die Sie analysieren möchten.</li><li>SCHLÜSSEL: **Erforderlich** Der Schlüssel, für den der Wert extrahiert werden muss.</li><li>VALUE_DELIMITER: **Erforderlich** Das Trennzeichen, das das Feld und den Wert voneinander trennt. Wenn entweder eine `null` oder eine leere Zeichenfolge angegeben wird, ist dieser Wert `:`.</li><li>FIELD_DELIMITER: *Optional* Das Trennzeichen zwischen Feld- und Wertpaaren. Wenn entweder eine `null` oder eine leere Zeichenfolge angegeben wird, ist dieser Wert `,`.</li></ul> | get_values(STRING, KEY, VALUE_DELIMITER, FIELD_DELIMITER) | get_values(\&quot;firstName - John , lastName - Cena , phone - 555 420 8692\&quot;, \&quot;firstName\&quot;, \&quot;-\&quot;, \&quot;,\&quot;) | John |
| map_get_values | Nimmt eine Zuordnung und eine Schlüsseleingabe. Wenn die Eingabe ein einzelner Schlüssel ist, gibt die Funktion den mit diesem Schlüssel verknüpften Wert zurück. Wenn die Eingabe ein Zeichenfolgen-Array ist, gibt die Funktion alle Werte zurück, die den bereitgestellten Schlüsseln entsprechen. Wenn die eingehende Zuordnung doppelte Schlüssel enthält, muss der Rückgabewert die Schlüssel deduplizieren und eindeutige Werte zurückgeben. | <ul><li>MAP: **Erforderlich** Die Eingabemap-Daten.</li><li>SCHLÜSSEL: **Erforderlich** Der Schlüssel kann eine einzelne Zeichenfolge oder ein String-Array sein. Wenn ein anderer primitiver Typ (Daten/Zahl) angegeben wird, wird er als Zeichenfolge behandelt.</li></ul> | get_values(MAP, KEY) | Im [Anhang](#map_get_values) finden Sie ein Codebeispiel. | |
| map_has_keys | Wenn ein oder mehrere Eingabeschlüssel angegeben sind, gibt die Funktion &quot;true&quot;zurück. Wenn ein Zeichenfolgen-Array als Eingabe bereitgestellt wird, gibt die Funktion beim ersten gefundenen Schlüssel &quot;true&quot;zurück. | <ul><li>MAP: **Erforderlich** Die Eingabemap-Daten</li><li>SCHLÜSSEL: **Erforderlich** Der Schlüssel kann eine einzelne Zeichenfolge oder ein String-Array sein. Wenn ein anderer primitiver Typ (Daten/Zahl) angegeben wird, wird er als Zeichenfolge behandelt.</li></ul> | map_has_keys(MAP, KEY) | Im [Anhang](#map_has_keys) finden Sie ein Codebeispiel. | |
| add_to_map | akzeptiert mindestens zwei Eingaben. Eine beliebige Anzahl von Karten kann als Eingaben bereitgestellt werden. Data Prep gibt eine einzelne Zuordnung zurück, die alle Schlüssel-Wert-Paare aus allen Eingaben enthält. Wenn ein oder mehrere Schlüssel wiederholt werden (in derselben Zuordnung oder über mehrere Maps hinweg), dedupliziert Data Prep die Schlüssel so, dass das erste Schlüssel-Wert-Paar in der Reihenfolge beibehalten wird, in der sie in der Eingabe übergeben wurden. | MAP: **Erforderlich** Die Eingabemap-Daten. | add_to_map(MAP 1, MAP 2, MAP 3, ...) | Im [Anhang](#add_to_map) finden Sie ein Codebeispiel. | |
| object_to_map (Syntax 1) | Verwenden Sie diese Funktion, um Map -Datentypen zu erstellen. | <ul><li>SCHLÜSSEL: **Erforderlich** Schlüssel müssen eine Zeichenfolge sein. Wenn andere Primitive-Werte wie Ganzzahlen oder Datumswerte angegeben werden, werden sie automatisch in Zeichenfolgen konvertiert und als Zeichenfolgen behandelt.</li><li>ANY_TYPE: **Erforderlich** bezieht sich auf jeden unterstützten XDM-Datentyp außer Maps.</li></ul> | object_to_map(KEY, ANY_TYPE, KEY, ANY_TYPE, ... ) | Im [Anhang](#object_to_map) finden Sie ein Codebeispiel. | |
| object_to_map (Syntax 2) | Verwenden Sie diese Funktion, um Map -Datentypen zu erstellen. | <ul><li>OBJEKT: **Erforderlich** Sie können ein eingehendes Objekt- oder Objekt-Array bereitstellen und auf ein Attribut innerhalb des Objekts als Schlüssel verweisen.</li></ul> | object_to_map(OBJECT) | Im [Anhang](#object_to_map) finden Sie ein Codebeispiel. |
| object_to_map (Syntax 3) | Verwenden Sie diese Funktion, um Map -Datentypen zu erstellen. | <ul><li>OBJEKT: **Erforderlich** Sie können ein eingehendes Objekt- oder Objekt-Array bereitstellen und auf ein Attribut innerhalb des Objekts als Schlüssel verweisen.</li></ul> | object_to_map(OBJECT_ARRAY, ATTRIBUTE_IN_OBJECT_TO_BE_USED_AS_A_KEY) | Im [Anhang](#object_to_map) finden Sie ein Codebeispiel. |

{style="table-layout:auto"}

Informationen zur Objektkopierfunktion finden Sie im Abschnitt [unter](#object-copy).

### Hierarchien - Arrays {#arrays}

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Funktion | Beschreibung | Parameter | Aufbau | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| coalesce | Gibt das erste Objekt zurück, das nicht null ist und sich in einem angegebenen Array befindet. | <ul><li>EINGABE: **Erforderlich** Das Array, von dem Sie das erste Objekt finden möchten, dessen Wert nicht null ist.</li></ul> | coalesce(INPUT) | coalesce(null, null, null, &quot;first&quot;, null, &quot;second&quot;) | &quot;first&quot; |
| first | Ruft das erste Element des angegebenen Arrays ab. | <ul><li>EINGABE: **Erforderlich** Das Array, von dem Sie das erste Element finden möchten.</li></ul> | first(INPUT) | first(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;1&quot; |
| last | Ruft das letzte Element des angegebenen Arrays ab. | <ul><li>EINGABE: **Erforderlich** Das Array, von dem Sie das letzte Element finden möchten.</li></ul> | last(INPUT) | last(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;3&quot; |
| add_to_array | Fügt Elemente am Ende des Arrays hinzu. | <ul><li>ARRAY: **Erforderlich** Das Array, dem Sie Elemente hinzufügen.</li><li>WERTE: Die Elemente, die an das Array angehängt werden sollen.</li></ul> | add_to_array &#x200B;(ARRAY, VALUES) | add_to_array &#x200B;([&#39;a&#39;, &#39;b&#39;], &#39;c&#39;, &#39;d&#39;) | [&#39;a&#39;, &#39;b&#39;, &#39;c&#39;, &#39;d&#39;] |
| join_arrays | Kombiniert die Arrays miteinander. | <ul><li>ARRAY: **Erforderlich** Das Array, dem Sie Elemente hinzufügen.</li><li>WERTE: Die Arrays, die an das übergeordnete Array angehängt werden sollen.</li></ul> | join_arrays &#x200B;(ARRAY, VALUES) | join_arrays &#x200B;([&#39;a&#39;, &#39;b&#39;], [&#39;c&#39;], [&#39;d&#39;, &#39;e&#39;]) | [&#39;a&#39;, &#39;b&#39;, &#39;c&#39;, &#39;d&#39;, &#39;e&#39;] |
| to_array | Nimmt eine Liste von Eingaben und konvertiert sie in ein Array. | <ul><li>INCLUDE_NULLS: **Erforderlich** Ein boolescher Wert, der angibt, ob Nullen in das Antwort-Array aufgenommen werden sollen oder nicht.</li><li>WERTE: **Erforderlich** Die Elemente, die in ein Array konvertiert werden sollen.</li></ul> | to_array &#x200B;(INCLUDE_NULLS, VALUES) | to_array(false, 1, null, 2, 3) | `[1, 2, 3]` |
| size_of | Gibt die Größe der Eingabe zurück. | <ul><li>EINGABE: **Erforderlich** Das Objekt, dessen Größe Sie ermitteln möchten.</li></ul> | size_of(INPUT) | `size_of([1, 2, 3, 4])` | 4 |
| upsert_array_append | Mit dieser Funktion werden alle Elemente im gesamten Eingabe-Array an das Ende des Arrays in Profil angehängt. Diese Funktion gilt für Aktualisierungen nur **1}.** Wenn diese Funktion im Kontext von Einfügen verwendet wird, gibt sie die Eingabe unverändert zurück. | <ul><li>ARRAY: **Erforderlich** Das Array, an das das Array im Profil angehängt werden soll.</li></ul> | update_array_append(ARRAY) | `upsert_array_append([123, 456])` | [123, 456] |
| upsert_array_replace | Diese Funktion wird verwendet, um Elemente in einem Array zu ersetzen. Diese Funktion gilt für Aktualisierungen nur **1}.** Wenn diese Funktion im Kontext von Einfügen verwendet wird, gibt sie die Eingabe unverändert zurück. | <ul><li>ARRAY: **Erforderlich** Das Array, das das Array im Profil ersetzen soll.</li></li> | upsert_array_replace(ARRAY) | `upsert_array_replace([123, 456], 1)` | [123, 456] |
| [!BADGE Nur Ziele]{type=Informative} array_to_string | Verbindet die Zeichenfolgendarstellungen der Elemente in einem Array mithilfe des angegebenen Trennzeichens. Wenn das Array mehrdimensional ist, wird es vor dem Verbinden reduziert. **Hinweis**: Diese Funktion wird in Zielen verwendet. Weitere Informationen finden Sie in der [Dokumentation](../destinations/ui/export-arrays-calculated-fields.md) . | <ul><li>SEPARATOR: **Erforderlich** Das Trennzeichen, das zum Verbinden der Elemente im Array verwendet wird.</li><li>ARRAY: **Erforderlich** Das Array, das verbunden wird (nach dem Reduzieren).</li></ul> | array_to_string(SEPARATOR, ARRAY) | `array_to_string(";", ["Hello", "world"])` | &quot;Hello;world&quot; |
| [!BADGE Nur Ziele]{type=Informative} filterArray* | Filtert das angegebene Array basierend auf einem Prädikat. **Hinweis**: Diese Funktion wird in Zielen verwendet. Weitere Informationen finden Sie in der [Dokumentation](../destinations/ui/export-arrays-calculated-fields.md) . | <ul><li>ARRAY: **Erforderlich** Das zu filternde Array</li><li>PRÄDIKATE: **Erforderlich** Die Eigenschaft, die auf jedes Element des angegebenen Arrays angewendet werden soll. | filterArray(ARRAY, PREDICATE) | `filterArray([5, -6, 0, 7], x -> x > 0)` | [5, 7] |
| [!BADGE Nur Ziele]{type=Informative} transformArray* | Wandelt das angegebene Array basierend auf einem Prädikat um. **Hinweis**: Diese Funktion wird in Zielen verwendet. Weitere Informationen finden Sie in der [Dokumentation](../destinations/ui/export-arrays-calculated-fields.md) . | <ul><li>ARRAY: **Erforderlich** Das zu transformierende Array.</li><li>PRÄDIKATE: **Erforderlich** Die Eigenschaft, die auf jedes Element des angegebenen Arrays angewendet werden soll. | transformArray(ARRAY, PREDICATE) | ` transformArray([5, 6, 7], x -> x + 1)` | [6, 7, 8] |
| [!BADGE Ziele only]{type=Informative} flattenArray* | Reduziert das angegebene (mehrdimensionale) Array in ein eindimensionales Array. **Hinweis**: Diese Funktion wird in Zielen verwendet. Weitere Informationen finden Sie in der [Dokumentation](../destinations/ui/export-arrays-calculated-fields.md) . | <ul><li>ARRAY: **Erforderlich** Das zu reduzierende Array.</li></ul> | flattenArray(ARRAY) | flattenArray([[&#39;a&#39;, &#39;b&#39;], [&#39;c&#39;, &#39;d&#39;]], [[&#39;e&#39;], [&#39;f&#39;]]) | [&#39;a&#39;, &#39;b&#39;, &#39;c&#39;, &#39;d&#39;, &#39;e&#39;, &#39;f&#39;] |

{style="table-layout:auto"}

### Hierarchien - Zuordnung {#map}

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Funktion | Beschreibung | Parameter | Aufbau | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| array_to_map | Diese Funktion akzeptiert ein Objekt-Array und einen Schlüssel als Eingabe und gibt eine Zuordnung des Schlüsselfelds mit dem Wert als Schlüssel und dem Array-Element als Wert zurück. | <ul><li>EINGABE: **Erforderlich** Das Objekt-Array, von dem Sie das erste Objekt finden möchten, dessen Wert nicht null ist.</li><li>SCHLÜSSEL: **Erforderlich** Der Schlüssel muss ein Feldname im Objekt-Array und das Objekt als Wert sein.</li></ul> | array_to_map(OBJECT[] INPUTS, KEY) | Lesen Sie den [Anhang](#object_to_map) für ein Codebeispiel. |
| object_to_map | Diese Funktion akzeptiert ein Objekt als Argument und gibt eine Zuordnung von Schlüssel-Wert-Paaren zurück. | <ul><li>EINGABE: **Erforderlich** Das Objekt-Array, von dem Sie das erste Objekt finden möchten, dessen Wert nicht null ist.</li></ul> | object_to_map(OBJECT_INPUT) | &quot;object_to_map(address), wobei die Eingabe &quot; + &quot;address: {line1 : \&quot;345 park ave\&quot;,line2: \&quot;bldg 2\&quot;,City : \&quot;san jose\&quot;,State : \&quot;CA\&quot;,type: \&quot;office\&quot;}&quot; ist | Gibt eine Zuordnung mit angegebenen Feld-Name- und Wert-Paaren zurück oder null, wenn die Eingabe null ist. Beispiel: `"{line1 : \"345 park ave\",line2: \"bldg 2\",City : \"san jose\",State : \"CA\",type: \"office\"}"` |
| to_map | Diese Funktion akzeptiert eine Liste von Schlüssel-Wert-Paaren und gibt eine Zuordnung von Schlüssel-Wert-Paaren zurück. | | to_map(OBJECT_INPUT) | &quot;to_map(\&quot;firstName\&quot;, \&quot;John\&quot;, \&quot;lastName\&quot;, \&quot;Doe\&quot;)&quot; | Gibt eine Zuordnung mit angegebenen Feld-Name- und Wert-Paaren zurück oder null, wenn die Eingabe null ist. Beispiel: `"{\"firstName\" : \"John\", \"lastName\": \"Doe\"}"` |

{style="table-layout:auto"}

### Logische Operatoren {#logical-operators}

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Funktion | Beschreibung | Parameter | Aufbau | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| decode | Bei einem Schlüssel und einer Liste mit Schlüsselwertpaaren, die als Array reduziert werden, gibt die Funktion den Wert zurück, wenn der Schlüssel gefunden wird, oder gibt einen Standardwert zurück, wenn er im Array vorhanden ist. | <ul><li>SCHLÜSSEL: **Erforderlich** Der zuzuordnende Schlüssel.</li><li>OPTIONS: **Erforderlich** Ein reduziertes Array von Schlüssel/Wert-Paaren. Optional kann ein Standardwert am Ende gesetzt werden.</li></ul> | decode(KEY, OPTIONS) | decode(stateCode, &quot;ca&quot;, &quot;California&quot;, &quot;pa&quot;, &quot;Pennsylvania&quot;, &quot;N/A&quot;) | Wenn der angegebene stateCode &quot;ca&quot;ist, &quot;California&quot;.<br>Wenn der angegebene stateCode &quot;pa&quot;, &quot;Pennsylvania&quot; ist.<br>Wenn der stateCode nicht mit dem folgenden übereinstimmt, &quot;K/A&quot;. |
| iif | Wertet einen bestimmten booleschen Ausdruck aus und gibt den angegebenen Wert basierend auf dem Ergebnis zurück. | <ul><li>AUSDRUCK: **Erforderlich** Der boolesche Ausdruck, der ausgewertet wird.</li><li>TRUE_VALUE: **Erforderlich** Der Wert, der zurückgegeben wird, wenn der Ausdruck &quot;true&quot;ergibt.</li><li>FALSE_VALUE: **Erforderlich** Der Wert, der zurückgegeben wird, wenn der Ausdruck &quot;false&quot;ergibt.</li></ul> | iif(EXPRESSION, TRUE_VALUE, FALSE_VALUE) | iif(&quot;s&quot;.equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;True&quot; |

{style="table-layout:auto"}

### Aggregation {#aggregation}

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Funktion | Beschreibung | Parameter | Aufbau | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| min | Gibt das Minimum der angegebenen Argumente zurück. Verwendet die natürliche Reihenfolge. | <ul><li>OPTIONS: **Erforderlich** Ein oder mehrere Objekte, die miteinander verglichen werden können.</li></ul> | min(OPTIONS) | min(3, 1, 4) | 1 |
| max | Gibt das Maximum der angegebenen Argumente zurück. Verwendet die natürliche Reihenfolge. | <ul><li>OPTIONS: **Erforderlich** Ein oder mehrere Objekte, die miteinander verglichen werden können.</li></ul> | max(OPTIONS) | max(3, 1, 4) | 4 |

{style="table-layout:auto"}

### Typkonvertierungen {#type-conversions}

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Funktion | Beschreibung | Parameter | Aufbau | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| to_bigint | Konvertiert einen String in einen BigInteger-Wert. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, die in einen BigInteger konvertiert werden soll.</li></ul> | to_bigint(STRING) | to_bigint &#x200B;(&quot;100000.34&quot;) | 1000000,34 |
| to_decimal | Konvertiert einen String in einen Double-String. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, die in ein Doppelt umgewandelt werden soll.</li></ul> | to_decimal(STRING) | to_decimal(&quot;20.5&quot;) | 20,5 |
| to_float | Konvertiert einen String in einen Float-Wert. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, die in einen Float-Wert konvertiert werden soll.</li></ul> | to_float(STRING) | to_float(&quot;12.3456&quot;) | 12,34566 |
| to_integer | Konvertiert eine Zeichenfolge in eine Ganzzahl. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, die in eine Ganzzahl konvertiert werden soll.</li></ul> | to_integer(STRING) | to_integer(&quot;12&quot;) | 12 |

{style="table-layout:auto"}

### JSON-Funktionen {#json}

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Funktion | Beschreibung | Parameter | Aufbau | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| json_to_object | Deserialisieren Sie den JSON-Inhalt aus der angegebenen Zeichenfolge. | <ul><li>STRING: **Erforderlich** Die zu deserialisierende JSON-Zeichenfolge.</li></ul> | json_to_object &#x200B;(STRING) | json_to_object &#x200B;({&quot;info&quot;:{&quot;firstName&quot;:&quot;John&quot;,&quot;lastName&quot;: &quot;Doe&quot;}) | Ein Objekt, das die JSON darstellt. |

{style="table-layout:auto"}

### Sondermaßnahmen {#special-operations}

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Funktion | Beschreibung | Parameter | Aufbau | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| uuid /<br>guid | Generiert eine Pseudo-Zufallskennung. | | uuid()<br>guid() | uuid()<br>guid() | 7c0267d2-bb74-4e1a-9275-3bf4fccda5f4<br>c7016dc7-3163-43f7-afc7-2e1c9c20633 |
| `fpid_to_ecid ` | Diese Funktion akzeptiert eine FPID-Zeichenfolge und konvertiert sie in eine ECID, die in Adobe Experience Platform- und Adobe Experience Cloud-Anwendungen verwendet werden soll. | <ul><li>STRING: **Erforderlich** Die FPID-Zeichenfolge, die in ECID konvertiert werden soll.</li></ul> | `fpid_to_ecid(STRING)` | `fpid_to_ecid("4ed70bee-b654-420a-a3fd-b58b6b65e991")` | `"28880788470263023831040523038280731744"` |

{style="table-layout:auto"}

### Benutzeragenten-Funktionen {#user-agent}

Jede der in der folgenden Tabelle enthaltenen Benutzeragenten-Funktionen kann einen der folgenden Werte zurückgeben:

* Telefon - Ein Mobilgerät mit kleinem Bildschirm (allgemein &lt; 7&quot;)
* Mobile : Ein Mobilgerät, das noch nicht identifiziert wurde. Bei diesem Mobilgerät kann es sich um einen eReader, ein Tablet, ein Telefon, eine Uhr usw. handeln.

Weitere Informationen zu Gerätefeldwerten finden Sie in der [Liste der Gerätefeldwerte](#device-field-values) im Anhang dieses Dokuments.

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Funktion | Beschreibung | Parameter | Aufbau | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| ua_os_name | Extrahiert den Betriebssystemnamen aus der Benutzeragenten-Zeichenfolge. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragenten-Zeichenfolge.</li></ul> | ua_os_name &#x200B;(USER_AGENT) | ua_os_name &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 wie Mac OS X) AppleWebKit/534.46 (KHTML, wie Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS |
| ua_os_version_major | Extrahiert die Hauptversion des Betriebssystems aus der Zeichenfolge des Benutzeragenten. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragenten-Zeichenfolge.</li></ul> | ua_os_version_major &#x200B;(USER_AGENT) | ua_os_version_major &#x200B; s(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 wie Mac OS X) AppleWebKit/534.46 (KHTML, wie Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | IOS 5 |
| ua_os_version | Extrahiert die Betriebssystemversion aus der Zeichenfolge des Benutzeragenten. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragenten-Zeichenfolge.</li></ul> | ua_os_version &#x200B;(USER_AGENT) | ua_os_version &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 wie Mac OS X) AppleWebKit/534.46 (KHTML, wie Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1.1 |
| ua_os_name_version | Extrahiert den Namen und die Version des Betriebssystems aus der Zeichenfolge des Benutzeragenten. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragenten-Zeichenfolge.</li></ul> | ua_os_name_version &#x200B;(USER_AGENT) | ua_os_name_version &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 wie Mac OS X) AppleWebKit/534.46 (KHTML, wie Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5.1.1 |
| ua_agent_version | Extrahiert die Agentenversion aus der Benutzeragenten-Zeichenfolge. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragenten-Zeichenfolge.</li></ul> | ua_agent_version &#x200B;(USER_AGENT) | ua_agent_version &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 wie Mac OS X) AppleWebKit/534.46 (KHTML, wie Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5,1 |
| ua_agent_version_major | Extrahiert den Namen des Agenten und die Hauptversion aus der Zeichenfolge des Benutzeragenten. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragenten-Zeichenfolge.</li></ul> | ua_agent_version_major &#x200B;(USER_AGENT) | ua_agent_version_major &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 wie Mac OS X) AppleWebKit/534.46 (KHTML, wie Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari 5 |
| ua_agent_name | Extrahiert den Agentennamen aus der Benutzeragenten-Zeichenfolge. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragenten-Zeichenfolge.</li></ul> | ua_agent_name &#x200B;(USER_AGENT) | ua_agent_name &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 wie Mac OS X) AppleWebKit/534.46 (KHTML, wie Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari |
| ua_device_class | Extrahiert die Geräteklasse aus der Benutzeragenten-Zeichenfolge. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragenten-Zeichenfolge.</li></ul> | ua_device_class &#x200B;(USER_AGENT) | ua_device_class &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 wie Mac OS X) AppleWebKit/534.46 (KHTML, wie Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Telefon |

{style="table-layout:auto"}

### Analytics-Funktionen {#analytics}

>[!NOTE]
>
>Sie dürfen nur die folgenden Analysefunktionen für WebSDK- und Adobe Analytics-Datenflüsse verwenden.

| Funktion | Beschreibung | Parameter | Aufbau | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| aa_get_event_id | Extrahiert die Ereignis-ID aus einer Analytics-Ereignis-Zeichenfolge. | <ul><li>EVENT_STRING: **Erforderlich** Die kommagetrennte Analytics-Ereigniszeichenfolge.</li><li>EVENT_NAME: **Erforderlich** Der Ereignisname, aus dem extrahiert und die ID abgerufen werden soll.</li></ul> | aa_get_event_id(EVENT_STRING, EVENT_NAME) | aa_get_event_id(&quot;event101=5:123456,scOpen&quot;, &quot;event101&quot;) | 123456 |
| aa_get_event_value | Extrahiert den Ereigniswert aus einer Analytics-Ereigniszeichenfolge. Wenn der Ereigniswert nicht angegeben ist, wird 1 zurückgegeben. | <ul><li>EVENT_STRING: **Erforderlich** Die kommagetrennte Analytics-Ereigniszeichenfolge.</li><li>EVENT_NAME: **Erforderlich** Der Ereignisname, aus dem ein Wert extrahiert werden soll.</li></ul> | aa_get_event_value(EVENT_STRING, EVENT_NAME) | aa_get_event_value(&quot;event101=5:123456,scOpen&quot;, &quot;event101&quot;) | 5 |
| aa_get_product_categories | Extrahiert die Produktkategorie aus einer Analytics-Produktzeichenfolge. | <ul><li>PRODUCTS_STRING: **Erforderlich** Die Analytics-Produktzeichenfolge.</li></ul> | aa_get_product_categories(PRODUCTS_STRING) | aa_get_product_categories(&quot;;Beispielprodukt 1;1;3.50,Beispielkategorie 2;Beispielprodukt 2;1;5.99&quot;) | [null,&quot;Beispielkategorie 2&quot;] |
| aa_get_product_names | Extrahiert den Produktnamen aus einer Analytics-Produktzeichenfolge. | <ul><li>PRODUCTS_STRING: **Erforderlich** Die Analytics-Produktzeichenfolge.</li></ul> | aa_get_product_names(PRODUCTS_STRING) | aa_get_product_names(&quot;;Beispielprodukt 1;1;3.50,Beispielkategorie 2;Beispielprodukt 2;1;5.99&quot;) | [&quot;Beispiel Produkt 1&quot;,&quot;Beispiel Produkt 2&quot;] |
| aa_get_product_quantity | Extrahiert die Mengen aus einer Analytics-Produktzeichenfolge. | <ul><li>PRODUCTS_STRING: **Erforderlich** Die Analytics-Produktzeichenfolge.</li></ul> | aa_get_product_quantity(PRODUCTS_STRING) | aa_get_product_quantity(&quot;;Beispielprodukt 1;1;3.50,Beispielkategorie 2;Beispielprodukt 2&quot;) | [&quot;1&quot;, null] |
| aa_get_product_price | Extrahiert den Preis aus einer Analytics-Produktzeichenfolge. | <ul><li>PRODUCTS_STRING: **Erforderlich** Die Analytics-Produktzeichenfolge.</li></ul> | aa_get_product_price(PRODUCTS_STRING) | aa_get_product_price(&quot;;Beispiel für Produkt 1;1;3.50,Beispielkategorie 2;Beispielprodukt 2&quot;) | [&quot;3.50&quot;, null] |
| aa_get_product_event_values | Extrahiert Werte für das benannte Ereignis aus der Produktzeichenfolge als Zeichenfolgen-Array. | <ul><li>PRODUCTS_STRING: **Erforderlich** Die Analytics-Produktzeichenfolge.</li><li>EVENT_NAME: **Erforderlich** Der Ereignisname, aus dem Werte extrahiert werden sollen.</li></ul> | aa_get_product_event_values(PRODUCTS_STRING, EVENT_NAME) | aa_get_product_event_values(&quot;;Beispielprodukt 1;1;4.20;event1=2.3\|event2=5:1,;Beispielprodukt 2;1;4.20;event1=3\|event2=2:2&quot;, &quot;event1&quot;) | [&quot;2.3&quot;, &quot;3&quot;] |
| aa_get_product_evars | Extrahiert die eVar-Werte für das benannte Ereignis aus der Produktzeichenfolge als Zeichenfolgen-Array. | <ul><li>PRODUCTS_STRING: **Erforderlich** Die Analytics-Produktzeichenfolge.</li><li>EVAR_NAME: **Erforderlich** Der zu extrahierende eVar.</li></ul> | aa_get_product_evars(PRODUCTS_STRING, EVENT_NAME) | aa_get_product_evars(&quot;;Beispielprodukt;1;6.69;;eVar1=Merchandising-Wert&quot;, &quot;eVar1&quot;) | [&quot;Merchandising-Wert&quot;] |

{style="table-layout:auto"}

<!-- | aa_get_product_events | Extracts a named event from the products string as an array of objects. | <ul><li>PRODUCTS_STRING: **Required** The Analytics products string.</li><li>EVENT_NAME: **Required** The event name to extract values from.</li></ul> | aa_get_product_events(PRODUCTS_STRING, EVENT_NAME) | aa_get_product_events(";Example product 1;1;4.20;event1=2.3\|event2=5:1,;Example product 2;1;4.20;event1=3\|event2=2:2", "event2") | [`{"id": "1","value", "5"}`, `{"id": "2","value", "1"}`] |
| aa_get_product_event_ids | Extracts the IDs for the named event from the products string as an array of strings. | <ul><li>PRODUCTS_STRING: **Required** The Analytics products string.</li><li>EVENT_NAME: **Required** The event name to extract values from.</li></ul> | aa_get_product_event_ids(PRODUCTS_STRING, EVENT_NAME) | aa_get_product_event_ids(";Example product 1;1;4.20;event1=2.3\|event2=5:1,;Example product 2;1;4.20;event1=3\|event2=2:2", "event2") | ["1", "2"] | -->

### Objektkopie {#object-copy}

>[!TIP]
>
>Die Funktion zum Kopieren von Objekten wird automatisch angewendet, wenn ein Objekt in der Quelle einem Objekt in XDM zugeordnet wird. Benutzer müssen keine weiteren Aktionen durchführen.

Sie können die Funktion zum Kopieren von Objekten verwenden, um Attribute eines Objekts automatisch zu kopieren, ohne Änderungen an der Zuordnung vorzunehmen. Wenn Ihre Quelldaten beispielsweise folgende Struktur aufweisen:

```json
address{
        line1: 4191 Ridgebrook Way,
        city: San Jose,
        state: California
        }
```

und eine XDM-Struktur von:

```json
addr{
    addrLine1: 4191 Ridgebrook Way,
    city: San Jose,
    state: California
    }
```

Anschließend wird die Zuordnung zu:

```json
address -> addr
address.line1 -> addr.addrLine1
```

Im obigen Beispiel werden die Attribute `city` und `state` ebenfalls automatisch zur Laufzeit erfasst, da das Objekt `address` `addr` zugeordnet ist. Wenn Sie ein `line2` -Attribut in der XDM-Struktur erstellen und Ihre Eingabedaten auch ein `line2` im `address` -Objekt enthalten, werden sie auch automatisch erfasst, ohne dass die Zuordnung manuell geändert werden muss.

Um sicherzustellen, dass die automatische Zuordnung funktioniert, müssen die folgenden Voraussetzungen erfüllt sein:

* Übergeordnete Objekte sollten zugeordnet werden;
* Neue Attribute müssen im XDM-Schema erstellt worden sein.
* Neue Attribute sollten über übereinstimmende Namen im Quellschema und im XDM-Schema verfügen.

Wenn eine der Voraussetzungen nicht erfüllt ist, müssen Sie das Quellschema mithilfe von data prep manuell dem XDM-Schema zuordnen.

## Anhang

Im Folgenden finden Sie weitere Informationen zur Verwendung der Zuordnungsfunktionen für die Datenvorbereitung

### Sonderzeichen {#special-characters}

Die nachstehende Tabelle enthält eine Liste der reservierten Zeichen und der zugehörigen kodierten Zeichen.

| Reserviertes Zeichen | Kodiertes Zeichen |
| --- | --- |
| space | %20 |
| ! | %21 |
| &quot; | %22 |
| # | %23 |
| $ | %24 |
| % | %25 |
| &amp; | %26 |
| &#39; | %27 |
| ( | %28 |
| ) | %29 |
| * | %2A |
| + | %2B |
| , | %2C |
| / | %2F |
| : | %3A |
|   | %3B |
| &lt; | %3C |
| = | %3D |
| > | %3E |
| ? | %3F |
| @ | %40 |
| [ | %5B |
| | | %5C |
| ] | %5D |
| ^ | %5E |
| ` | %60 |
| ~ | %7E |

{style="table-layout:auto"}

### Gerätefeldwerte {#device-field-values}

Die nachstehende Tabelle enthält eine Liste der Gerätefeldwerte und der zugehörigen Beschreibungen.

| Gerät | Beschreibung |
| --- | --- |
| Desktop | Ein Desktop- oder Laptop-Gerät. |
| Anonymisiert | Ein anonymes Gerät. In einigen Fällen handelt es sich um `useragents`, die von einer Anonymisierungssoftware geändert wurden. |
| Unbekannt | Ein unbekanntes Gerät. Dabei handelt es sich normalerweise um `useragents` , die keine Informationen über das Gerät enthalten. |
| Mobile | Ein Mobilgerät, das noch nicht identifiziert wurde. Bei diesem Mobilgerät kann es sich um einen eReader, ein Tablet, ein Telefon, eine Uhr usw. handeln. |
| Tablette | Ein Mobilgerät mit einem großen Bildschirm (normalerweise > 7&quot;). |
| Telefon | Ein Mobilgerät mit kleinem Bildschirm (normalerweise &lt; 7&quot;). |
| Watch | Ein Mobilgerät mit einem winzigen Bildschirm (normalerweise &lt; 2&quot;). Diese Geräte dienen normalerweise als zusätzlicher Bildschirm für Geräte vom Typ Telefon/Tablet. |
| Erweiterte Realität | Ein Mobilgerät mit AR-Funktionen. |
| Virtuelle Realität | Ein Mobilgerät mit VR-Funktionen. |
| eReader | Ein Gerät, das einem Tablet ähnelt, in der Regel jedoch einen [!DNL eInk] -Bildschirm aufweist. |
| Set-Top-Box | Ein angeschlossenes Gerät, das die Interaktion über einen TV-Bildschirm ermöglicht. |
| TV | Ein Gerät, das der Set-Top-Box ähnelt, aber in den Fernseher integriert ist. |
| Hauseinheit | Ein (normalerweise großes) Haushaltsgerät, wie ein Kühlschrank. |
| Spielekonsole | Ein festes Gaming-System wie ein [!DNL Playstation] oder ein [!DNL XBox]. |
| Handheld Game Console | Ein mobiles Gaming-System wie ein [!DNL Nintendo Switch]. |
| Stimme | Ein stimmgesteuertes Gerät wie ein [!DNL Amazon Alexa] oder ein [!DNL Google Home]. |
| Auto | Ein fahrzeugbasierter Browser. |
| Robot | Roboter, die eine Website besuchen. |
| Robot Mobile | Roboter, die eine Website besuchen, aber angeben, dass sie als mobiler Besucher angesehen werden sollen. |
| Robot Imitator | Roboter, die eine Website besuchen, so tun, als wären sie Roboter wie [!DNL Google], aber sie sind es nicht. **Hinweis**: In den meisten Fällen handelt es sich bei Roboterimmitatoren tatsächlich um Roboter. |
| Cloud | Eine Cloud-basierte Anwendung. Das sind weder Roboter noch Hacker, aber es sind Anwendungen, die eine Verbindung herstellen müssen. Dazu gehören [!DNL Mastodon] -Server. |
| Hacker | Dieser Gerätewert wird verwendet, wenn Skripterstellung in der Zeichenfolge `useragent` erkannt wird. |

{style="table-layout:auto"}

### Code-Beispiele {#code-samples}

#### map_get_values {#map-get-values}

+++Auswählen zum Anzeigen des Beispiels

```json
 example = "map_get_values(book_details,\"author\") where input is : {\n" +
        "    \"book_details\":\n" +
        "    {\n" +
        "        \"author\": \"George R. R. Martin\",\n" +
        "        \"price\": 17.99,\n" +
        "        \"ISBN\": \"ISBN-978-0553801477\"\n" +
        "    }\n" +
        "}",
      result = "{\"author\": \"George R. R. Martin\"}"
```

+++

#### map_has_keys {#map_has_keys}

+++Auswählen zum Anzeigen des Beispiels

```json
 example = "map_has_keys(book_details,\"author\")where input is : {\n" +
        "    \"book_details\":\n" +
        "    {\n" +
        "        \"author\": \"George R. R. Martin\",\n" +
        "        \"price\": 17.99,\n" +
        "        \"ISBN\": \"ISBN-978-0553801477\"\n" +
        "    }\n" +
        "}",
      result = "true"
```

+++

#### add_to_map {#add_to_map}

+++Auswählen zum Anzeigen des Beispiels

```json
example = "add_to_map(book_details, book_details2) where input is {\n" +
        "    \"book_details\":\n" +
        "    {\n" +
        "        \"author\": \"George R. R. Martin\",\n" +
        "        \"price\": 17.99,\n" +
        "        \"ISBN\": \"ISBN-978-0553801477\"\n" +
        "    }\n" +
        "}" +
        "{\n" +
        "    \"book_details2\":\n" +
        "    {\n" +
        "        \"author\": \"Neil Gaiman\",\n" +
        "        \"price\": 17.99,\n" +
        "        \"ISBN\": \"ISBN-0-380-97365-0\"\n" +
        "        \"publisher\": \"William Morrow\"\n" +
        "    }\n" +
        "}",
      result = "{\n" +
        "    \"book_details\":\n" +
        "    {\n" +
        "        \"author\": \"George R. R. Martin\",\n" +
        "        \"price\": 17.99,\n" +
        "        \"ISBN\": \"ISBN-978-0553801477\"\n" +
        "        \"publisher\": \"William Morrow\"\n" +
        "    }\n" +
        "}",
      returns = "A new map with all elements from map and addends"
```

+++

#### object_to_map {#object_to_map}

**Syntax 1**

+++Auswählen zum Anzeigen des Beispiels

```json
example = "object_to_map(\"firstName\", \"John\", \"lastName\", \"Doe\")",
result = "{\"firstName\" : \"John\", \"lastName\": \"Doe\"}"
```

+++

**Syntax 2**

+++Auswählen zum Anzeigen des Beispiels

```json
example = "object_to_map(address) where input is " +
  "address: {line1 : \"345 park ave\",line2: \"bldg 2\",City : \"san jose\",State : \"CA\",type: \"office\"}",
result = "{line1 : \"345 park ave\",line2: \"bldg 2\",City : \"san jose\",State : \"CA\",type: \"office\"}"
```

+++

**Syntax 3**

+++Auswählen zum Anzeigen des Beispiels

```json
example = "object_to_map(addresses,type)" +
        "\n" +
        "[\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City\": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"home\"\n" +
        "    },\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City \": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"work\"\n" +
        "    },\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City \": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"office\"\n" +
        "    }\n" +
        "]" ,
result = "{\n" +
        "    \"home\":\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City\": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"home\"\n" +
        "    },\n" +
        "    \"work\":\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City \": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"work\"\n" +
        "    },\n" +
        "    \"office\":\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City \": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"office\"\n" +
        "    }\n" +
        "}" 
```

+++

#### array_to_map {#array_to_map}

+++Auswählen zum Anzeigen des Beispiels

```json
example = "array_to_map(addresses, \"type\") where addresses is\n" +
  "\n" +
  "[\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City\": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"home\"\n" +
  "    },\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City \": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"work\"\n" +
  "    },\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City \": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"office\"\n" +
  "    }\n" +
  "]" ,
result = "{\n" +
  "    \"home\":\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City\": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"home\"\n" +
  "    },\n" +
  "    \"work\":\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City \": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"work\"\n" +
  "    },\n" +
  "    \"office\":\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City \": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"office\"\n" +
  "    }\n" +
  "}",
returns = "Returns a map with given field name and value pairs or null if input is null"
```

+++

