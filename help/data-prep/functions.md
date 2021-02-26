---
keywords: Experience Platform;Home;beliebte Themen;Map CSV;Map CSV-Datei;CSV-Datei zu xdm zuordnen;CSV zu xdm zuordnen;ui-Handbuch;Mapper;Zuordnung;Felder;Zuordnungsfunktionen; Zuordnungsfunktionen
solution: Experience Platform
title: Funktionen für die Datenvorlagenzuordnung
topic: Übersicht
description: In diesem Dokument werden die Zuordnungsfunktionen vorgestellt, die mit Data Prep verwendet werden.
translation-type: tm+mt
source-git-commit: fd2dffd5b8957833b670e9cb434517bcb0f886a3
workflow-type: tm+mt
source-wordcount: '3625'
ht-degree: 7%

---


# Zuordnungsfunktionen für die Datenvorbereitung

Mithilfe der Funktion &quot;Datenvorgabe&quot;können Werte basierend auf den in die Quellfelder eingegebenen Werten berechnet und berechnet werden.

## Felder

Ein Feldname kann ein beliebiger offizieller Bezeichner sein - eine unbegrenzte Sequenz von Unicode-Buchstaben und -Ziffern, beginnend mit einem Buchstaben, dem Dollarzeichen (`$`) oder dem Unterstrich (`_`). Bei Variablennamen wird auch die Groß-/Kleinschreibung beachtet.

Wenn ein Feldname dieser Regel nicht entspricht, muss der Feldname mit `${}` umgebrochen werden. Wenn der Feldname beispielsweise &quot;Vorname&quot;oder &quot;Vorname&quot;lautet, muss der Name wie `${First Name}` bzw. `${First.Name}` umgebrochen werden.

Wenn ein Feldname **beliebige** der folgenden reservierten Suchbegriffe ist, muss er mit `${}` umschlossen werden:

```console
new, mod, or, break, var, lt, for, false, while, eq, gt, div, not, null, continue, else, and, ne, true, le, if, ge, return
```

Daten innerhalb von Unterfeldern können mit der Punktnotation aufgerufen werden. Wenn beispielsweise ein `name`-Objekt vorhanden ist, verwenden Sie `firstName`, um auf das Feld `name.firstName` zuzugreifen.

## Funktionsliste

In den folgenden Tabellen werden alle unterstützten Zuordnungsfunktionen, einschließlich Beispiel-Ausdruck und deren Ausgabeformate, Liste.

### Zeichenfolgen-Funktionen

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Funktion | Beschreibung | Parameter | Syntax | Ausdruck | Beispielausgabe |
-------- | ----------- | ---------- | -------| ---------- | -------------
| concat | Verkettet die angegebenen Zeichenfolgen. | <ul><li>STRING: Die zu verkettenden Zeichenfolgen.</li></ul> | concat(STRING_1, STRING_2) | concat(&quot;Hi, &quot;, &quot;there&quot;, &quot;!&quot;) | `"Hi, there!"` |
| explode | Teilt die Zeichenfolge basierend auf einem Regex und gibt ein Array von Teilen zurück. Kann optional regex einschließen, um die Zeichenfolge zu teilen. Standardmäßig wird die Aufteilung in &quot;,&quot;aufgelöst. Die folgenden Trennzeichen **müssen mit `\` Escape-Zeichen versehen werden: `+, ?, ^, |, ., [, (, {, ), *, $, \`** | <ul><li>STRING: **Erforderlich** Die zu teilende Zeichenfolge.</li><li>REGEX: *Optional* Der reguläre Ausdruck, der zum Teilen der Zeichenfolge verwendet werden kann.</li></ul> | explode(STRING, REGEX) | explode(&quot;Hi, there!&quot;, &quot;&quot;) | `["Hi,", "there"]` |
| instr | Gibt die Position/den Index einer Unterzeichenfolge zurück. | <ul><li>INPUT: **Erforderlich** Die Zeichenfolge, die gesucht wird.</li><li>UNTERZEICHNUNG: **Erforderlich** Die Unterzeichenfolge, nach der in der Zeichenfolge gesucht wird.</li><li>Beginn_POSITION: *Optional* Die Position, an der der Beginn in der Zeichenfolge suchen soll.</li><li>AUFTRAG: *Optional* Das n-te Vorkommen, das von der Position des Beginns gesucht werden soll. Der Standardwert ist 1. </li></ul> | instr(INPUT, SUBSTRING, BEGINN_POSITION, OCCURRENCE) | instr(&quot;adobe.com&quot;, &quot;com&quot;) | 6 |
| Ersatz | Ersetzt die Suchzeichenfolge, wenn sie in der ursprünglichen Zeichenfolge vorhanden ist. | <ul><li>INPUT: **Erforderlich** Die Eingabezeichenfolge.</li><li>TO_FIND: **Erforderlich** Die Zeichenfolge, die in der Eingabe nachgeschlagen werden soll.</li><li>TO_REPLACE: **Erforderlich** Die Zeichenfolge, die den Wert in &quot;TO_FIND&quot;ersetzt.</li></ul> | replace(INPUT, TO_FIND, TO_REPLACE) | replace(&quot;This is a string re test&quot;, &quot;re&quot;, &quot;replace&quot;) | &quot;Dies ist ein String-Ersatz-Test&quot; |
| substr | Gibt eine Teilzeichenfolge einer angegebenen Länge zurück. | <ul><li>INPUT: **Erforderlich** Die Eingabezeichenfolge.</li><li>Beginn_INDEX: **Erforderlich** Der Index der Eingabezeichenfolge, bei der die Unterzeichenfolge Beginn hat.</li><li>LÄNGE: **Erforderlich** Die Länge der Unterzeichenfolge.</li></ul> | substr(INPUT, BEGINN_INDEX, LENGTH) | substr(&quot;This is a substring test&quot;, 7, 8) | &quot; a subst&quot; |
| lower /<br>lcase | Konvertiert eine Zeichenfolge in Kleinbuchstaben. | <ul><li>INPUT: **Erforderlich** Die Zeichenfolge, die in Kleinbuchstaben umgewandelt wird.</li></ul> | lower(INPUT) | lower(&quot;HeLLo&quot;)<br>lcase(&quot;HeLLo&quot;) | &quot;hello&quot; |
| top /<br>ucase | Konvertiert eine Zeichenfolge in Großbuchstaben. | <ul><li>INPUT: **Erforderlich** Die Zeichenfolge, die in Großbuchstaben konvertiert wird.</li></ul> | upper(INPUT) | upper(&quot;HeLLo&quot;)<br>ucase(&quot;HeLLo&quot;) | &quot;HELLO&quot; |
| split | Teilt eine Eingabezeichenfolge auf einem Trennzeichen. Das folgende Trennzeichen **muss** mit `\` Escape-Zeichen versehen werden: `\`. | <ul><li>INPUT: **Erforderlich** Die Eingabezeichenfolge, die geteilt werden soll.</li><li>SEPARATOR: **Erforderlich** Die Zeichenfolge, die zum Teilen der Eingabe verwendet wird.</li></ul> | split(INPUT, SEPARATOR) | split(&quot;Hello world&quot;, &quot;&quot;) | `["Hello", "world"]` |
| join | Verbindet eine Liste von Objekten mit der Trennlinie. | <ul><li>SEPARATOR: **Erforderlich** Die Zeichenfolge, die zum Verbinden der Objekte verwendet wird.</li><li>OBJEKTE: **Erforderlich** Ein Array von Zeichenfolgen, die verbunden werden.</li></ul> | `join(SEPARATOR, [OBJECTS])` | `join(" ", to_array(true, "Hello", "world"))` | &quot;Hello world&quot; |
| lpad | Fügt die linke Seite einer Zeichenfolge mit der anderen angegebenen Zeichenfolge ein. | <ul><li>INPUT: **Erforderlich** Die Zeichenfolge, die hinzugefügt werden soll. Diese Zeichenfolge kann null sein.</li><li>COUNT: **Erforderlich** Die Größe der Zeichenfolge, die hinzugefügt werden soll.</li><li>HINZUFÜGEN: **Erforderlich** Die Zeichenfolge, mit der die Eingabe aufgefüllt werden soll. Wenn null oder leer, wird es als ein Leerzeichen behandelt.</li></ul> | lpad(INPUT, COUNT, PADDING) | lpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;yzyzybat&quot; |
| rpad | Fügt die rechte Seite einer Zeichenfolge mit der anderen angegebenen Zeichenfolge ein. | <ul><li>INPUT: **Erforderlich** Die Zeichenfolge, die hinzugefügt werden soll. Diese Zeichenfolge kann null sein.</li><li>COUNT: **Erforderlich** Die Größe der Zeichenfolge, die hinzugefügt werden soll.</li><li>HINZUFÜGEN: **Erforderlich** Die Zeichenfolge, mit der die Eingabe aufgefüllt werden soll. Wenn null oder leer, wird es als ein Leerzeichen behandelt.</li></ul> | rpad(INPUT, COUNT, PADDING) | rpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;batyzyzy&quot; |
| left | Ruft die ersten &quot;n&quot;-Zeichen der angegebenen Zeichenfolge ab. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, für die Sie die ersten &quot;n&quot;-Zeichen erhalten.</li><li>COUNT: **Erforderlich** Die &quot;n&quot;-Zeichen, die Sie aus der Zeichenfolge abrufen möchten.</li></ul> | left(STRING, COUNT) | left(&quot;abcde&quot;, 2) | &quot;ab&quot; |
| right | Ruft die letzten &quot;n&quot;-Zeichen der angegebenen Zeichenfolge ab. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, für die Sie die letzten &quot;n&quot;-Zeichen erhalten.</li><li>COUNT: **Erforderlich** Die &quot;n&quot;-Zeichen, die Sie aus der Zeichenfolge abrufen möchten.</li></ul> | right(STRING, COUNT) | right(&quot;abcde&quot;, 2) | &quot;de&quot; |
| ltrim | Entfernt den Leerraum vom Anfang der Zeichenfolge. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, aus der Sie den Leerraum entfernen möchten.</li></ul> | ltrim(STRING) | ltrim(&quot; hello&quot;) | &quot;hello&quot; |
| rtrim | Entfernt den Leerraum vom Ende der Zeichenfolge. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, aus der Sie den Leerraum entfernen möchten.</li></ul> | rtrim(STRING) | rtrim(&quot;hello &quot;) | &quot;hello&quot; |
| trim | Entfernt den Leerraum vom Anfang und vom Ende der Zeichenfolge. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, aus der Sie den Leerraum entfernen möchten.</li></ul> | trim(STRING) | trim(&quot; hello &quot;) | &quot;hello&quot; |
| gleich | Vergleicht zwei Zeichenfolgen, um sicherzustellen, dass sie gleich sind. Bei dieser Funktion wird zwischen Groß- und Kleinschreibung unterschieden. | <ul><li>STRING1: **Erforderlich** Die erste Zeichenfolge, die Sie vergleichen möchten.</li><li>STRING2: **Erforderlich** Die zweite Zeichenfolge, die Sie vergleichen möchten.</li></ul> | STRING1. &#x200B;equals( &#x200B; STRING2) | &quot;string1&quot;. &#x200B;gleich &#x200B;(&quot;STRING1&quot;) | false |
| equalsIgnoreCase | Vergleicht zwei Zeichenfolgen, um sicherzustellen, dass sie gleich sind. Bei dieser Funktion wird zwischen Groß- und Kleinschreibung unterschieden.**** | <ul><li>STRING1: **Erforderlich** Die erste Zeichenfolge, die Sie vergleichen möchten.</li><li>STRING2: **Erforderlich** Die zweite Zeichenfolge, die Sie vergleichen möchten.</li></ul> | STRING1. &#x200B;equalsIgnoreCase &#x200B;(STRING2) | &quot;string1&quot;. &#x200B;equalsIgnoreCase &#x200B;(&quot;STRING1) | wahr |

&#x200B;

### Regelmäßige Ausdruck-Funktionen

| Funktion | Beschreibung | Parameter | Syntax | Ausdruck | Beispielausgabe |
-------- | ----------- | ---------- | -------| ---------- | -------------
| extract_regex | Extrahiert auf Basis eines regulären Ausdrucks Gruppen aus der Eingabezeichenfolge. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, aus der Sie die Gruppen extrahieren.</li><li>REGEX: **Erforderlich** Der reguläre Ausdruck, mit dem die Gruppe übereinstimmen soll.</li></ul> | extract_regex(STRING, REGEX) | extract_regex &#x200B;(&quot;E259,E259B_009,1_1&quot; &#x200B;, &quot;([^,]+),[^,]*,([^,]+)&quot;) | [&quot;E259,E259B_009,1_1&quot;, &quot;E259&quot;, &quot;1_1&quot;] |
| match_regex | Überprüft, ob die Zeichenfolge mit dem eingegebenen regulären Ausdruck übereinstimmt. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, die Sie überprüfen, stimmt mit dem regulären Ausdruck überein.</li><li>REGEX: **Erforderlich** Der reguläre Ausdruck, mit dem Sie vergleichen.</li></ul> | match_regex(STRING, REGEX) | match_regex(&quot;E259,E259B_009,1_1&quot;, &quot;([^,]+),[^,]*,([^,]+)&quot;) | wahr |

### Hashfunktionen

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Funktion | Beschreibung | Parameter | Syntax | Ausdruck | Beispielausgabe |
-------- | ----------- | ---------- | -------| ---------- | -------------
| sha1 | Führt eine Eingabe durch und erzeugt einen Hashwert mit Secure Hash Algorithm 1 (SHA-1). | <ul><li>INPUT: **Erforderlich** Der einfache Text, der mit Hashing versehen werden soll.</li><li>CHARSET: *Optional* Der Name des Zeichensatzes. Mögliche Werte sind UTF-8, UTF-16, ISO-8859-1 und US-ASCII.</li></ul> | sha1(INPUT, CHARSET) | sha1(&quot;my text&quot;, &quot;UTF-8&quot;) | c3599c11e47719df18a24 &#x200B; 48690840c5dfcce3c80 |
| sha256 | Erstellt einen Hashwert mit Secure Hash Algorithm 256 (SHA-256). | <ul><li>INPUT: **Erforderlich** Der einfache Text, der mit Hashing versehen werden soll.</li><li>CHARSET: *Optional* Der Name des Zeichensatzes. Mögliche Werte sind UTF-8, UTF-16, ISO-8859-1 und US-ASCII.</li></ul> | sha256(INPUT, CHARSET) | sha256(&quot;my text&quot;, &quot;UTF-8&quot;) | 7330d2b39ca35eaf4cb95fc846c21 &#x200B; ee6a39af698154a83a586ee270a0d372104 |
| sha512 | Erstellt einen Hashwert mit Secure Hash Algorithm 512 (SHA-512). | <ul><li>INPUT: **Erforderlich** Der einfache Text, der mit Hashing versehen werden soll.</li><li>CHARSET: *Optional* Der Name des Zeichensatzes. Mögliche Werte sind UTF-8, UTF-16, ISO-8859-1 und US-ASCII.</li></ul> | sha512(INPUT, CHARSET) | sha512(&quot;my text&quot;, &quot;UTF-8&quot;) | a3d7e45a0d9be5fd4e4b9a3b8c9c2163c21ef &#x200B; 708bf11b4232bb21d2a8704ada2cdcd7b367dd07 a88a89 &#x200B; a5c908cfe377aceb1072a7b386b7d4fd2ff68a8fd24d16 |
| md5 | Erstellt mithilfe von MD5 eine Eingabe und einen Hashwert. | <ul><li>INPUT: **Erforderlich** Der einfache Text, der mit Hashing versehen werden soll.</li><li>CHARSET: *Optional* Der Name des Zeichensatzes. Mögliche Werte sind UTF-8, UTF-16, ISO-8859-1 und US-ASCII. </li></ul> | md5(INPUT, CHARSET) | md5(&quot;my text&quot;, &quot;UTF-8&quot;) | d3b96ce8c9fb4 &#x200B; e9bd0198d03ba6852c7 |
| crc32 | Eine Eingabe verwendet einen CRC-Algorithmus (zyklische Redundanzprüfung), um einen 32-Bit-zyklischen Code zu erzeugen. | <ul><li>INPUT: **Erforderlich** Der einfache Text, der mit Hashing versehen werden soll.</li><li>CHARSET: *Optional* Der Name des Zeichensatzes. Mögliche Werte sind UTF-8, UTF-16, ISO-8859-1 und US-ASCII.</li></ul> | crc32(INPUT, CHARSET) | crc32(&quot;my text&quot;, &quot;UTF-8&quot;) | 8df92e80 |

### URL-Funktionen

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Funktion | Beschreibung | Parameter | Syntax | Ausdruck | Beispielausgabe |
-------- | ----------- | ---------- | -------| ---------- | -------------
| get_url_protocol | Gibt das Protokoll der angegebenen URL zurück. Wenn die Eingabe ungültig ist, gibt sie null zurück. | <ul><li>URL: **Erforderlich** Die URL, aus der das Protokoll extrahiert werden muss.</li></ul> | get_url_protocol &#x200B;(URL) | get_url_protocol(&quot;https://platform &#x200B; .adobe.com/home&quot;) | https |
| get_url_host | Gibt den Host der angegebenen URL zurück. Wenn die Eingabe ungültig ist, gibt sie null zurück. | <ul><li>URL: **Erforderlich** Die URL, von der der Host extrahiert werden muss.</li></ul> | get_url_host &#x200B;(URL) | get_url_host &#x200B;(&quot;https://platform &#x200B; .adobe.com/home&quot;) | platform.adobe.com |
| get_url_port | Gibt den Anschluss der angegebenen URL zurück. Wenn die Eingabe ungültig ist, gibt sie null zurück. | <ul><li>URL: **Erforderlich** Die URL, aus der der Anschluss extrahiert werden muss.</li></ul> | get_url_port(URL) | get_url_port &#x200B;(&quot;sftp://example.com//home/ &#x200B; joe/employee.csv&quot;) | 22 |
| get_url_path | Gibt den Pfad der angegebenen URL zurück. Standardmäßig wird der vollständige Pfad zurückgegeben. | <ul><li>URL: **Erforderlich** Die URL, aus der der Pfad extrahiert werden muss.</li><li>FULL_PATH: *Optional* Ein boolescher Wert, der bestimmt, ob der vollständige Pfad zurückgegeben wird. Bei der Einstellung false wird nur das Ende des Pfads zurückgegeben.</li></ul> | get_url_path &#x200B;(URL, FULL_PATH) | get_url_path &#x200B;(&quot;sftp://example.com// &#x200B; home/joe/employee.csv&quot;) | &quot;//home/joe/ &#x200B; employee.csv&quot; |
| get_url_Abfrage_str | Gibt die Abfrage-Zeichenfolge einer angegebenen URL zurück. | <ul><li>URL: **Erforderlich** Die URL, von der Sie die Abfrage-Zeichenfolge abrufen möchten.</li><li>ANCHOR: **Erforderlich** Legt fest, was mit dem Anker in der Abfrage-Zeichenfolge geschehen soll. Kann einer von drei Werten sein: &quot;behalten&quot;, &quot;entfernen&quot;oder &quot;anhängen&quot;.<br><br>Wenn der Wert &quot;keep&quot;ist, wird der Anker an den zurückgegebenen Wert angehängt.<br>Wenn der Wert &quot;remove&quot;ist, wird der Anker aus dem zurückgegebenen Wert entfernt.<br>Wenn der Wert &quot;append&quot;ist, wird der Anker als separater Wert zurückgegeben.</li></ul> | get_url_Abfrage_str &#x200B;(URL, ANCHOR) | get_url_Abfrage_str &#x200B;(&quot;foo://example.com:8042 &#x200B;/over/there?name= &#x200B; ferret#nose&quot;, &quot;preserve&quot;)<br>get_url_Abfrage_str &#x200B;(&quot;foo://example.com:8042 &#x200B;/over/there?name= &#x200B; ferret#nose&quot;, &quot;remove&quot;)<br>get_url_Abfrage_str &#x200B;(&quot;foo://example.com:8042/2 over/thereB?name=ferret#nose&quot;, &quot;append&quot;) | `{"name": "ferret#nose"}`<br>`{"name": "ferret"}`<br>`{"name": "ferret", "_anchor_": "nose"}` |

### Datums- und Uhrzeitfunktionen

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen. Weitere Informationen zur Funktion `date` finden Sie im Funktionsleitfaden [date](./dates.md).

| Funktion | Beschreibung | Parameter | Syntax | Ausdruck | Beispielausgabe |
-------- | ----------- | ---------- | -------| ---------- | -------------
| now | Ruft die aktuelle Zeit ab. |  | now() | now() | `2020-09-23T10:10:24.556-07:00[America/Los_Angeles]` |
| timestamp | Ruft die aktuelle Unix-Zeit ab. |  | timestamp() | timestamp() | 1571850624571 |
| format | Formatiert das Eingabedatum nach einem angegebenen Format. | <ul><li>DATUM: **Erforderlich** Das Eingabedatum als ZonedDateTime-Objekt, das Sie formatieren möchten.</li><li>FORMAT: **Erforderlich** Das Format, in das das Datum geändert werden soll.</li></ul> | format(DATE, FORMAT) | format(2019-10-23T11:24:00+00:00, &quot;yyyy-MM-dd HH:mm:ss&quot;) | &quot;2019-10-23 11:24:35&quot; |
| dformat | Konvertiert einen Zeitstempel in eine Datums-Zeichenfolge in einem angegebenen Format. | <ul><li>ZEITSTEMPEL: **Erforderlich** Der Zeitstempel, den Sie formatieren möchten. Dies wird in Millisekunden geschrieben.</li><li>FORMAT: **Erforderlich** Das Format, in das Sie den Zeitstempel ändern möchten.</li></ul> | dformat &#x200B;(TIMESTAMP, FORMAT) | dformat(1571829875, &quot;dd-MMM-yyyy hh:mm&quot;) | &quot;23. Oktober 2019 11:24&quot; |
| date | Konvertiert eine Datums-Zeichenfolge in ein ZonedDateTime-Objekt (ISO 8601-Format). | <ul><li>DATUM: **Erforderlich** Die Zeichenfolge, die das Datum darstellt.</li><li>FORMAT: **Erforderlich** Die Zeichenfolge, die das Format des Datums darstellt.</li><li>DEFAULT_DATE: **Erforderlich** Das zurückgegebene Standarddatum, wenn das angegebene Datum null ist.</li></ul> | date(DATE, FORMAT, DEFAULT_DATE) | date(&quot;2019-10-23 11:24&quot;, &quot;yyyy-MM-dd HH:mm&quot;, now()) | &quot;2019-10-23T11:24Z&quot; |
| date | Konvertiert eine Datums-Zeichenfolge in ein ZonedDateTime-Objekt (ISO 8601-Format). | <ul><li>DATUM: **Erforderlich** Die Zeichenfolge, die das Datum darstellt.</li><li>FORMAT: **Erforderlich** Die Zeichenfolge, die das Format des Datums darstellt.</li></ul> | date(DATE, FORMAT) | date(&quot;2019-10-23 11:24&quot;, &quot;yyyy-MM-dd HH:mm&quot;) | &quot;2019-10-23T11:24Z&quot; |
| date | Konvertiert eine Datums-Zeichenfolge in ein ZonedDateTime-Objekt (ISO 8601-Format). | <ul><li>DATUM: **Erforderlich** Die Zeichenfolge, die das Datum darstellt.</li></ul> | date(DATE) | date(&quot;2019-10-23 11:24&quot;) | &quot;2019-10-23T11:24Z&quot; |
| date_part | Ruft die Teile des Datums ab. Die folgenden Komponentenwerte werden unterstützt: <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;quartal&quot;<br>&quot;qq&quot;<br>&quot;q&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;dayofyear&quot;<br>&quot;dy&quot; a11/>&quot;y&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;week&quot;<br>&quot;ww&quot;<br>&quot;w&quot;<br><br>&quot;week&quot;<br>&quot;dw&quot;<br>&quot;w&quot;<br><br>&quot;hour&quot;<br>&quot;hh&quot;<br>&quot;hh24&quot;<br>&quot;hh12&quot;<br><br>&quot;minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;second&quot;<br>&quot;ss&quot;<br>&quot;s&quot;<br><br>&quot;millisecond&quot;<br>&quot;ms&quot;<br> | <ul><li>KOMPONENTE: **Erforderlich** Eine Zeichenfolge, die den Teil des Datums darstellt. </li><li>DATUM: **Erforderlich** Das Datum in einem Standardformat.</li></ul> | date_part &#x200B;(COMPONENT, DATE) | date_part(&quot;MM&quot;, date(&quot;2019-10-17 11:55:12&quot;)) | 10 |
| set_date_part | Ersetzt eine Komponente in einem bestimmten Datum. Die folgenden Komponenten werden akzeptiert: <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;hour&quot;<br>&quot;hh&quot;&lt;a1 1/>&quot;minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;second&quot;<br>&quot;ss&quot;<br>&quot;s&quot;<br><br> | <ul><li>KOMPONENTE: **Erforderlich** Eine Zeichenfolge, die den Teil des Datums darstellt. </li><li>WERT: **Erforderlich** Der Wert, der für die Komponente für ein bestimmtes Datum festgelegt wird.</li><li>DATUM: **Erforderlich** Das Datum in einem Standardformat.</li></ul> | set_date_part &#x200B;(COMPONENT, VALUE, DATE) | set_date_part(&quot;m&quot;, 4, date(&quot;2016-11-09T11:44:44.797&quot;) | &quot;2016-04-09T11:44:44.797&quot; |
| make_date_time | Erstellt ein Datum aus Teilen. Diese Funktion kann auch mithilfe von make_timestamp ausgelöst werden. | <ul><li>JAHR: **Erforderlich** Das Jahr, vierstellig geschrieben.</li><li>MONAT: **Erforderlich** Der Monat. Die zulässigen Werte sind 1 bis 12.</li><li>TAG: **Erforderlich** Der Tag. Die zulässigen Werte sind 1 bis 31.</li><li>STUNDE: **Erforderlich** Die Stunde. Die zulässigen Werte liegen zwischen 0 und 23.</li><li>MINUTE: **Erforderlich** Die Minute. Die zulässigen Werte liegen zwischen 0 und 59.</li><li>NANOSECOND: **Erforderlich** Die nanosekunden Werte. Die zulässigen Werte sind 0 bis 9999999999.</li><li>TIMEZONE: **Erforderlich** Die Zeitzone für die Datumszeit.</li></ul> | make_date_time &#x200B;(JAHR, MONAT, TAG, STUNDE, MINUTE, ZWEITE, NANOSECOND, TIMEZONE) | make_date_time &#x200B;(2019, 10, 17, 11, 55, 12, 999, &quot;America/Los_Angeles&quot;) | `2019-10-17T11:55:12.0&#x200B;00000999-07:00[America/Los_Angeles]` |
| zone_date_to_utc | Konvertiert ein Datum in einer beliebigen Zeitzone in ein Datum in UTC. | <ul><li>DATUM: **Erforderlich** Das Datum, das konvertiert werden soll.</li></ul> | zone_date_to_utc &#x200B;(DATE) | `zone_date_to_utc&#x200B;(2019-10-17T11:55:&#x200B;12.000000999-&#x200B;07:00[America/Los_Angeles])` | `2019-10-17T18:55:12.000000999Z[UTC]` |
| zone_date_to_zone | Konvertiert ein Datum aus einer Zeitzone in eine andere Zeitzone. | <ul><li>DATUM: **Erforderlich** Das Datum, das konvertiert werden soll.</li><li>ZONE: **Erforderlich** Die Zeitzone, in die Sie das Datum konvertieren möchten.</li></ul> | zone_date_to_zone &#x200B;(DATE, ZONE) | `zone_date_to_utc&#x200B;(2019-10-17T11:55:12&#x200B;.000000999-07:00&#x200B;[America/Los_Angeles], "Europe/Paris")` | `2019-10-17T20:55:12.000000999+02:00[Europe/Paris]` |

&#x200B;

### Hierarchien - Objekte

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Funktion | Beschreibung | Parameter | Syntax | Ausdruck | Beispielausgabe |
-------- | ----------- | ---------- | -------| ---------- | -------------
| size_of | Gibt die Größe der Eingabe zurück. | <ul><li>INPUT: **Erforderlich** Das Objekt, für das Sie die Größe suchen möchten.</li></ul> | size_of(INPUT) | `size_of([1, 2, 3, 4])` | 4 |
| is_empty | Überprüft, ob ein Objekt leer ist. | <ul><li>INPUT: **Erforderlich** Das Objekt, das Sie überprüfen möchten, ist leer.</li></ul> | is_empty(INPUT) | `is_empty([1, 2, 3])` | false |
| arrays_to_object | Erstellt eine Liste von Objekten. | <ul><li>INPUT: **Erforderlich** Eine Gruppierung von Schlüssel- und Array-Paaren.</li></ul> | arrays_to_object(INPUT) | Bedarfsprobe | Bedarfsprobe |
| to_object | Erstellt ein Objekt basierend auf den gegebenen einfachen Schlüssel/Wert-Paaren. | <ul><li>INPUT: **Erforderlich** Eine einfache Liste von Schlüssel/Wert-Paaren.</li></ul> | to_object(INPUT) | to_object &#x200B;(&quot;firstName&quot;, &quot;John&quot;, &quot;lastName&quot;, &quot;Doe&quot;) | `{"firstName": "John", "lastName": "Doe"}` |
| str_to_object | Erstellt ein Objekt aus der Eingabezeichenfolge. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, die zum Erstellen eines Objekts analysiert wird.</li><li>VALUE_DELIMITER: *Optional* Das Trennzeichen, das ein Feld vom Wert trennt. Das Standardtrennzeichen ist `:`.</li><li>FIELD_DELIMITER: *Optional* Das Trennzeichen, das Feldwertpaare trennt. Das Standardtrennzeichen ist `,`.</li></ul> | str_to_object &#x200B;(STRING, VALUE_DELIMITER, FIELD_DELIMITER) | str_to_object(&quot;firstName - John | lastName - | phone - 123 456 7890&quot;, &quot;-&quot;, &quot; | &quot;) | `{"firstName": "John", "lastName": "Doe", "phone": "123 456 7890"}` |
| is_set | Überprüft, ob das Objekt in den Quelldaten vorhanden ist. | <ul><li>INPUT: **Erforderlich** Der zu prüfende Pfad, falls er in den Quelldaten vorhanden ist.</li></ul> | is_set(INPUT) | is_set &#x200B;(&quot;evars.evar.field1&quot;) | wahr |
| nullify | Legt den Wert des Attributs auf `null` fest. Dies sollte verwendet werden, wenn Sie das Feld nicht in das Schema Zielgruppe kopieren möchten. |  | nullify() | nullify() | `null` |

### Hierarchien - Arrays

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Funktion | Beschreibung | Parameter | Syntax | Ausdruck | Beispielausgabe |
-------- | ----------- | ---------- | -------| ---------- | -------------
| coalesce | Gibt das erste nicht-Null-Objekt in einem gegebenen Array zurück. | <ul><li>INPUT: **Erforderlich** Das Array, von dem Sie das erste Nicht-Null-Objekt suchen möchten.</li></ul> | coalesce(INPUT) | coalesce(null, null, null, &quot;first&quot;, null, &quot;second&quot;) | &quot;first&quot; |
| first | Ruft das erste Element des angegebenen Arrays ab. | <ul><li>INPUT: **Erforderlich** Das Array, von dem Sie das erste Element suchen möchten.</li></ul> | first(INPUT) | first(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;1&quot; |
| last | Ruft das letzte Element des angegebenen Arrays ab. | <ul><li>INPUT: **Erforderlich** Das Array, von dem Sie das letzte Element suchen möchten.</li></ul> | last(INPUT) | last(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;3&quot; |
| to_array | Führt eine Liste von Eingaben durch und konvertiert sie in ein Array. | <ul><li>INCLUDE_NULLS: **Erforderlich** Ein boolescher Wert, der angibt, ob Nullen in das Antwortarray einbezogen werden sollen.</li><li>WERTE: **Erforderlich** Die Elemente, die in ein Array konvertiert werden sollen.</li></ul> | to_array &#x200B;(INCLUDE_NULLS, VALUES) | to_array(false, 1, null, 2, 3) | `[1, 2, 3]` |

### Logische Operatoren

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Funktion | Beschreibung | Parameter | Syntax | Ausdruck | Beispielausgabe |
-------- | ----------- | ---------- | -------| ---------- | -------------
| decode | Bei einem Schlüssel und einer Liste von Schlüsselwertpaaren, die als Array reduziert sind, gibt die Funktion den Wert zurück, wenn der Schlüssel gefunden wird, oder gibt einen Standardwert zurück, wenn er im Array vorhanden ist. | <ul><li>SCHLÜSSEL: **Erforderlich** Der zuzuordnende Schlüssel.</li><li>OPTIONS: **Erforderlich** Ein reduziertes Array von Schlüssel/Wert-Paaren. Optional kann ein Standardwert am Ende gesetzt werden.</li></ul> | decode(KEY, OPTIONS) | decode(stateCode, &quot;ca&quot;, &quot;California&quot;, &quot;pa&quot;, &quot;Pennsylvania&quot;, &quot;N/A&quot;) | Lautet der angegebene stateCode &quot;ca&quot;, &quot;California&quot;.<br>Lautet der angegebene stateCode &quot;pa&quot;, &quot;Pennsylvania&quot;.<br>Wenn der stateCode nicht mit dem Folgenden übereinstimmt, &quot;K/A&quot;. |
| iif | Wertet einen bestimmten booleschen Ausdruck aus und gibt den angegebenen Wert basierend auf dem Ergebnis zurück. | <ul><li>Ausdruck: **Erforderlich** Der boolesche Ausdruck, der ausgewertet wird.</li><li>TRUE_VALUE: **Erforderlich** Der Wert, der zurückgegeben wird, wenn der Ausdruck &quot;true&quot;ergibt.</li><li>FALSE_VALUE: **Erforderlich** Der Wert, der zurückgegeben wird, wenn der Ausdruck &quot;false&quot;ergibt.</li></ul> | iif(AUSDRUCK, TRUE_VALUE, FALSE_VALUE) | iif(&quot;s&quot;.equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;True&quot; |

### Aggregation

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Funktion | Beschreibung | Parameter | Syntax | Ausdruck | Beispielausgabe |
-------- | ----------- | ---------- | -------| ---------- | -------------
| min | Gibt das Minimum der angegebenen Argumente zurück. Verwendet die natürliche Reihenfolge. | <ul><li>OPTIONS: **Erforderlich** Ein oder mehrere Objekte, die miteinander verglichen werden können.</li></ul> | min(OPTIONS) | min(3, 1, 4) | 1 |
| max | Gibt das Maximum der angegebenen Argumente zurück. Verwendet die natürliche Reihenfolge. | <ul><li>OPTIONS: **Erforderlich** Ein oder mehrere Objekte, die miteinander verglichen werden können.</li></ul> | max(OPTIONS) | max(3, 1, 4) | 4 |

### Typkonvertierungen

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Funktion | Beschreibung | Parameter | Syntax | Ausdruck | Beispielausgabe |
-------- | ----------- | ---------- | -------| ---------- | -------------
| to_bigint | Konvertiert eine Zeichenfolge in eine BigInteger-Zeichenfolge. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, die in einen BigInteger konvertiert werden soll.</li></ul> | to_bigint(STRING) | to_bigint &#x200B;(&quot;1000000.34&quot;) | 100000,34 |
| to_decimal | Konvertiert eine Zeichenfolge in eine Dublette. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, die in eine Dublette konvertiert werden soll.</li></ul> | to_decimal(STRING) | to_decimal(&quot;20.5&quot;) | Artikel 20 Absatz 5 |
| to_float | Konvertiert eine Zeichenfolge in eine Gleitkommazahl. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, die in eine Gleitkommazahl konvertiert werden soll.</li></ul> | to_float(STRING) | to_float(&quot;12.3456&quot;) | 12 34 566 |
| to_integer | Konvertiert eine Zeichenfolge in eine Ganzzahl. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, die in eine Ganzzahl umgewandelt werden soll.</li></ul> | to_integer(STRING) | to_integer(&quot;12&quot;) | 12 |

### JSON-Funktionen

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Funktion | Beschreibung | Parameter | Syntax | Ausdruck | Beispielausgabe |
-------- | ----------- | ---------- | -------| ---------- | -------------
| json_to_object | Deserialisieren Sie den JSON-Inhalt aus der angegebenen Zeichenfolge. | <ul><li>STRING: **Erforderlich** Die zu deserialisierende JSON-Zeichenfolge.</li></ul> | json_to_object &#x200B;(STRING) | json_to_object &#x200B;({&quot;info&quot;:{&quot;firstName&quot;:&quot;John&quot;,&quot;lastName&quot; : &quot;Doe&quot;}) | Ein Objekt, das die JSON darstellt. |

### Besondere Maßnahmen

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Funktion | Beschreibung | Parameter | Syntax | Ausdruck | Beispielausgabe |
-------- | ----------- | ---------- | -------| ---------- | -------------
| uuid /<br>guid | Erstellt eine pseudo-zufällige ID. |  | uuid()<br>guid() | uuid()<br>guid() | 7c0267d2-bb74-4e1a-9275-3bf4fccda5f4<br>c7016dc7-3163-43f7-afc7-2e1c9c206333 |

### Benutzeragenten-Funktionen

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Funktion | Beschreibung | Parameter | Syntax | Ausdruck | Beispielausgabe |
-------- | ----------- | ---------- | -------| ---------- | -------------
| ua_os_name | Extrahiert den Betriebssystemnamen aus der Benutzeragenten-Zeichenfolge. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragenten-Zeichenfolge.</li></ul> | ua_os_name &#x200B;(USER_AGENT) | ua_os_name &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 (wie Mac OS X) AppleWebKit/534.46 (KHTML, wie Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS |
| ua_os_version_major | Extrahiert die Hauptversion des Betriebssystems aus der Benutzeragenten-Zeichenfolge. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragenten-Zeichenfolge.</li></ul> | ua_os_version_major &#x200B;(USER_AGENT) | ua_os_version_major &#x200B; s(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 (wie Mac OS X) AppleWebKit/534.46 (KHTML, wie Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5 |
| ua_os_version | Extrahiert die Version des Betriebssystems aus der Benutzeragenten-Zeichenfolge. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragenten-Zeichenfolge.</li></ul> | ua_os_version &#x200B;(USER_AGENT) | ua_os_version &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 (wie Mac OS X) AppleWebKit/534.46 (KHTML, wie Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1.1 |
| ua_os_name_version | Extrahiert den Namen und die Version des Betriebssystems aus der Benutzeragenten-Zeichenfolge. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragenten-Zeichenfolge.</li></ul> | ua_os_name_version &#x200B;(USER_AGENT) | ua_os_name_version &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 (wie Mac OS X) AppleWebKit/534.46 (KHTML, wie Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5.1.1 |
| ua_agent_version | Extrahiert die Agentversion aus der Benutzeragenten-Zeichenfolge. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragenten-Zeichenfolge.</li></ul> | ua_agent_version &#x200B;(USER_AGENT) | ua_agent_version &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 (wie Mac OS X) AppleWebKit/534.46 (KHTML, wie Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1 |
| ua_agent_version_major | Extrahiert den Agentnamen und die Hauptversion aus der Benutzeragenten-Zeichenfolge. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragenten-Zeichenfolge.</li></ul> | ua_agent_version_major &#x200B;(USER_AGENT) | ua_agent_version_major &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 (wie Mac OS X) AppleWebKit/534.46 (KHTML, wie Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari 5 |
| ua_agent_name | Extrahiert den Agenten-Namen aus der Benutzeragenten-Zeichenfolge. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragenten-Zeichenfolge.</li></ul> | ua_agent_name &#x200B;(USER_AGENT) | ua_agent_name &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 (wie Mac OS X) AppleWebKit/534.46 (KHTML, wie Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari |
| ua_device_class | Extrahiert die Geräteklasse aus der Benutzeragenten-Zeichenfolge. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragenten-Zeichenfolge.</li></ul> | ua_device_class &#x200B;(USER_AGENT) | ua_device_class &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 (wie Mac OS X) AppleWebKit/534.46 (KHTML, wie Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Telefon |