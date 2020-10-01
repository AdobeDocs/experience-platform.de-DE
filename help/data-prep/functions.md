---
keywords: Experience Platform;home;popular topics;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;mapper;mapping;mapping fields;mapping functions;
solution: Experience Platform
title: Zuordnungsfunktionen
topic: overview
description: In diesem Dokument werden die Zuordnungsfunktionen vorgestellt, die mit Data Prep verwendet werden.
translation-type: tm+mt
source-git-commit: db38f0666f5c945461043ad08939ebda52c21855
workflow-type: tm+mt
source-wordcount: '3288'
ht-degree: 6%

---


# Zuordnungsfunktionen

Zuordnungsfunktionen können verwendet werden, um Werte basierend auf dem, was in die Quellfelder eingegeben wird, zu berechnen und zu berechnen.

## Felder

Ein Feldname kann ein beliebiger offizieller Bezeichner sein - eine unbegrenzte Sequenz von Unicode-Buchstaben und -Ziffern, beginnend mit einem Buchstaben, dem Dollarzeichen (`$`) oder dem Unterstrich (`_`). Bei Variablennamen wird auch die Groß-/Kleinschreibung beachtet.

Wenn ein Feldname dieser Regel nicht entspricht, muss der Feldname mit `${}`eingeschlossen werden. Wenn der Feldname beispielsweise &quot;Vorname&quot;oder &quot;Vorname&quot;lautet, muss der Name wie `${First Name}` bzw. `${First.Name}` entsprechend umgebrochen werden.

Darüber hinaus sind Feldnamen **eines** der folgenden reservierten Schlüsselwörter und müssen mit `${}`:

```console
new, mod, or, break, var, lt, for, false, while, eq, gt, div, not, null, continue, else, and, ne, true, le, if, ge, return
```

Daten innerhalb von Unterfeldern können mit der Punktnotation aufgerufen werden. Wenn beispielsweise ein `name` Objekt vorhanden war, verwenden Sie zum Zugriff auf das `firstName` Feld `name.firstName`.

## Funktionsliste

In den folgenden Tabellen werden alle unterstützten Zuordnungsfunktionen, einschließlich Beispiel-Ausdruck und deren Ausgabeformate, Liste.

### Zeichenfolgen-Funktionen

| Funktion | Beschreibung | Parameter | Syntax | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| concat | Verkettet die angegebenen Zeichenfolgen. | <ul><li>STRING: Die zu verkettenden Zeichenfolgen.</li></ul> | concat(STRING_1, STRING_2) | concat(&quot;Hi, &quot;, &quot;there&quot;, &quot;!&quot;) | `"Hi, there!"` |
| explode | Teilt die Zeichenfolge basierend auf einem Regex und gibt ein Array von Teilen zurück. Kann optional regex einschließen, um die Zeichenfolge zu teilen. Standardmäßig wird die Aufteilung in &quot;,&quot;aufgelöst. | <ul><li>STRING: **Erforderlich** Die zu teilende Zeichenfolge.</li><li>REGEX: *Optional* Der reguläre Ausdruck, mit dem die Zeichenfolge geteilt werden kann.</li></ul> | explode(STRING, REGEX) | explode(&quot;Hi, there!&quot;, &quot;&quot;) | `["Hi,", "there"]` |
| instr | Gibt die Position/den Index einer Unterzeichenfolge zurück. | <ul><li>INPUT: **Erforderlich** Die gesuchte Zeichenfolge.</li><li>UNTERZEICHNUNG: **Erforderlich** Die Unterzeichenfolge, nach der in der Zeichenfolge gesucht wird.</li><li>BEGINN_POSITION: *Optional* Die Position, an der der Beginn die Zeichenfolge suchen soll.</li><li>AUFTRAG: *Optional* Das n-te Vorkommen, das von der Position des Beginns aus gesucht werden soll. Der Standardwert ist 1. </li></ul> | instr(INPUT, SUBSTRING, BEGINN_POSITION, OCCURRENCE) | instr(&quot;adobe`<span>`.com&quot;, &quot;com&quot;) | 6 |
| Ersatz | Ersetzt die Suchzeichenfolge, wenn sie in der ursprünglichen Zeichenfolge vorhanden ist. | <ul><li>INPUT: **Die Eingabezeichenfolge war erforderlich** .</li><li>TO_FIND: **Erforderlich** Die Zeichenfolge, die in der Eingabe nachgeschlagen werden soll.</li><li>TO_REPLACE: **Erforderlich** Die Zeichenfolge, die den Wert in &quot;TO_FIND&quot;ersetzt.</li></ul> | replace(INPUT, TO_FIND, TO_REPLACE) | replace(&quot;This is a string re test&quot;, &quot;re&quot;, &quot;replace&quot;) | &quot;Dies ist ein String-Ersatz-Test&quot; |
| substr | Gibt eine Teilzeichenfolge einer angegebenen Länge zurück. | <ul><li>INPUT: **Die Eingabezeichenfolge war erforderlich** .</li><li>BEGINN_INDEX: **Erforderlich** Der Index der Eingabezeichenfolge, in der die Unterzeichenfolge Beginn.</li><li>LENGTH: **Required** The length of the substring.</li></ul> | substr(INPUT, BEGINN_INDEX, LENGTH) | substr(&quot;This is a substring test&quot;, 7, 8) | &quot; a subst&quot; |
| lower/<br>lcase | Konvertiert eine Zeichenfolge in Kleinbuchstaben. | <ul><li>INPUT: **Erforderlich** Die Zeichenfolge, die in Kleinbuchstaben umgewandelt wird.</li></ul> | lower(INPUT) | lower(&quot;HeLLo&quot;)<br>lcase(&quot;HeLLo&quot;) | &quot;hello&quot; |
| top/<br>ucase | Konvertiert eine Zeichenfolge in Großbuchstaben. | <ul><li>INPUT: **Erforderlich** Die Zeichenfolge, die in Großbuchstaben umgewandelt wird.</li></ul> | upper(INPUT) | upper(&quot;HeLLo&quot;)<br>ucase(&quot;HeLLo&quot;) | &quot;HELLO&quot; |
| split | Teilt eine Eingabezeichenfolge auf einem Trennzeichen. | <ul><li>INPUT: **Erforderlich** Die Eingabezeichenfolge, die geteilt werden soll.</li><li>SEPARATOR: **Erforderlich** Die Zeichenfolge, mit der die Eingabe geteilt wird.</li></ul> | split(INPUT, SEPARATOR) | split(&quot;Hello world&quot;, &quot;&quot;) | `["Hello", "world"]` |
| join | Verbindet eine Liste von Objekten mit der Trennlinie. | <ul><li>SEPARATOR: **Erforderlich** Die Zeichenfolge, die zum Verbinden der Objekte verwendet wird.</li><li>OBJEKTE: **Erforderlich** Ein Array von Zeichenfolgen, die verbunden werden.</li></ul> | join(SEPARATOR, [OBJEKTE]) | `join(" ", ["Hello", "world"])` | &quot;Hello world&quot; |
| lpad | Fügt die linke Seite einer Zeichenfolge mit der anderen angegebenen Zeichenfolge ein. | <ul><li>INPUT: **Erforderlich** Die Zeichenfolge, die entfernt werden soll. Diese Zeichenfolge kann null sein.</li><li>COUNT: **Erforderlich** Die Größe der Zeichenfolge, die entfernt werden soll.</li><li>HINZUFÜGEN: **Erforderlich** Die Zeichenfolge, mit der die Eingabe aufgezeichnet werden soll. Wenn null oder leer, wird es als ein Leerzeichen behandelt.</li></ul> | lpad(INPUT, COUNT, PADDING) | lpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;yzyzybat&quot; |
| rpad | Fügt die rechte Seite einer Zeichenfolge mit der anderen angegebenen Zeichenfolge ein. | <ul><li>INPUT: **Erforderlich** Die Zeichenfolge, die entfernt werden soll. Diese Zeichenfolge kann null sein.</li><li>COUNT: **Erforderlich** Die Größe der Zeichenfolge, die entfernt werden soll.</li><li>HINZUFÜGEN: **Erforderlich** Die Zeichenfolge, mit der die Eingabe aufgezeichnet werden soll. Wenn null oder leer, wird es als ein Leerzeichen behandelt.</li></ul> | rpad(INPUT, COUNT, PADDING) | rpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;batyzyzy&quot; |
| left | Ruft die ersten &quot;n&quot;-Zeichen der angegebenen Zeichenfolge ab. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, für die Sie die ersten &quot;n&quot;-Zeichen erhalten.</li><li>COUNT: **** ErforderlichDie &quot;n&quot;-Zeichen, die Sie aus der Zeichenfolge abrufen möchten.</li></ul> | left(STRING, COUNT) | left(&quot;abcde&quot;, 2) | &quot;ab&quot; |
| right | Ruft die letzten &quot;n&quot;-Zeichen der angegebenen Zeichenfolge ab. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, für die Sie die letzten &quot;n&quot;-Zeichen erhalten.</li><li>COUNT: **** ErforderlichDie &quot;n&quot;-Zeichen, die Sie aus der Zeichenfolge abrufen möchten.</li></ul> | right(STRING, COUNT) | right(&quot;abcde&quot;, 2) | &quot;de&quot; |
| ltrim | Entfernt den Leerraum vom Anfang der Zeichenfolge. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, aus der Sie den Leerraum entfernen möchten.</li></ul> | ltrim(STRING) | ltrim(&quot; hello&quot;) | &quot;hello&quot; |
| rtrim | Entfernt den Leerraum vom Ende der Zeichenfolge. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, aus der Sie den Leerraum entfernen möchten.</li></ul> | rtrim(STRING) | rtrim(&quot;hello &quot;) | &quot;hello&quot; |
| trim | Entfernt den Leerraum vom Anfang und vom Ende der Zeichenfolge. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, aus der Sie den Leerraum entfernen möchten.</li></ul> | trim(STRING) | trim(&quot; hello &quot;) | &quot;hello&quot; |
| gleich | Vergleicht zwei Zeichenfolgen, um sicherzustellen, dass sie gleich sind. Bei dieser Funktion wird zwischen Groß- und Kleinschreibung unterschieden. | <ul><li>STRING1: **Erforderlich** Die erste Zeichenfolge, die Sie vergleichen möchten.</li><li>STRING2: **Erforderlich** Die zweite Zeichenfolge, die Sie vergleichen möchten.</li></ul> | STRING1.equals(STRING2) | &quot;string1&quot;.equals(&quot;STRING1) | false |
| equalsIgnoreCase | Vergleicht zwei Zeichenfolgen, um sicherzustellen, dass sie gleich sind. Bei dieser Funktion wird **nicht** zwischen Groß- und Kleinschreibung unterschieden. | <ul><li>STRING1: **Erforderlich** Die erste Zeichenfolge, die Sie vergleichen möchten.</li><li>STRING2: **Erforderlich** Die zweite Zeichenfolge, die Sie vergleichen möchten.</li></ul> | STRING1.equalsIgnoreCase(STRING2) | &quot;string1&quot;.equalsIgnoreCase(&quot;STRING1&quot;) | wahr |

### Hashfunktionen

| Funktion | Beschreibung | Parameter | Syntax | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| sha1 | Führt eine Eingabe durch und erzeugt einen Hashwert mit Secure Hash Algorithm 1 (SHA-1). | <ul><li>INPUT: **Erforderlich** Der einfache Text, der mit Hashing versehen werden soll.</li><li>CHARSET: *Optional* Der Name des Zeichensatzes. Mögliche Werte sind UTF-8, UTF-16, ISO-8859-1 und US-ASCII.</li></ul> | sha1(INPUT, CHARSET) | sha1(&quot;my text&quot;, &quot;UTF-8&quot;) | c3599c11e47719df18a2448690840c5dfcce3c80 |
| sha256 | Erstellt einen Hashwert mit Secure Hash Algorithm 256 (SHA-256). | <ul><li>INPUT: **Erforderlich** Der einfache Text, der mit Hashing versehen werden soll.</li><li>CHARSET: *Optional* Der Name des Zeichensatzes. Mögliche Werte sind UTF-8, UTF-16, ISO-8859-1 und US-ASCII.</li></ul> | sha256(INPUT, CHARSET) | sha256(&quot;my text&quot;, &quot;UTF-8&quot;) | 7330d2b39ca35eaf4cb95fc846c21ee6a39af698154a83a586ee270a0d372104 |
| sha512 | Erstellt einen Hashwert mit Secure Hash Algorithm 512 (SHA-512). | <ul><li>INPUT: **Erforderlich** Der einfache Text, der mit Hashing versehen werden soll.</li><li>CHARSET: *Optional* Der Name des Zeichensatzes. Mögliche Werte sind UTF-8, UTF-16, ISO-8859-1 und US-ASCII.</li></ul> | sha512(INPUT, CHARSET) | sha512(&quot;my text&quot;, &quot;UTF-8&quot;) | a3d7e45a0d9be5fd4e4b9a3b8c9c2163c21ef708bf11b4232bb21d2a8704ada2cdcd7b367dd0788a89a5c908cfe377aceb1072a7b386b7d4fd2ff68a8fd24d16 |
| md5 | Erstellt mithilfe von MD5 eine Eingabe und einen Hashwert. | <ul><li>INPUT: **Erforderlich** Der einfache Text, der mit Hashing versehen werden soll.</li><li>CHARSET: *Optional* Der Name des Zeichensatzes. Mögliche Werte sind UTF-8, UTF-16, ISO-8859-1 und US-ASCII. </li></ul> | md5(INPUT, CHARSET) | md5(&quot;my text&quot;, &quot;UTF-8&quot;) | d3b96ce8c9fb4e9bd0198d03ba6852c7 |
| crc32 | Eine Eingabe verwendet einen CRC-Algorithmus (zyklische Redundanzprüfung), um einen 32-Bit-zyklischen Code zu erzeugen. | <ul><li>INPUT: **Erforderlich** Der einfache Text, der mit Hashing versehen werden soll.</li><li>CHARSET: *Optional* Der Name des Zeichensatzes. Mögliche Werte sind UTF-8, UTF-16, ISO-8859-1 und US-ASCII.</li></ul> | crc32(INPUT, CHARSET) | crc32(&quot;my text&quot;, &quot;UTF-8&quot;) | 8df92e80 |

### URL-Funktionen

| Funktion | Beschreibung | Parameter | Syntax | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| get_url_protocol | Gibt das Protokoll der angegebenen URL zurück. Wenn die Eingabe ungültig ist, gibt sie null zurück. | <ul><li>URL: **Erforderlich** Die URL, aus der das Protokoll extrahiert werden soll.</li></ul> | get_url_protocol(URL) | get_url_protocol(&quot;https://platform.adobe.com/home&quot;) | https |
| get_url_host | Gibt den Host der angegebenen URL zurück. Wenn die Eingabe ungültig ist, gibt sie null zurück. | <ul><li>URL: **Erforderlich** Die URL, von der der Host extrahiert werden soll.</li></ul> | get_url_host(URL) | get_url_host(&quot;https://platform.adobe.com/home&quot;) | platform.adobe.com |
| get_url_port | Gibt den Anschluss der angegebenen URL zurück. Wenn die Eingabe ungültig ist, gibt sie null zurück. | <ul><li>URL: **Erforderlich** Die URL, aus der der Anschluss extrahiert werden soll.</li></ul> | get_url_port(URL) | get_url_port(&quot;sftp://example.com//home/joe/employee.csv&quot;) | 22 |
| get_url_path | Gibt den Pfad der angegebenen URL zurück. Standardmäßig wird der vollständige Pfad zurückgegeben. | <ul><li>URL: **Erforderlich** Die URL, aus der der Pfad extrahiert werden soll.</li><li>FULL_PATH: *Optional* Ein boolescher Wert, der bestimmt, ob der vollständige Pfad zurückgegeben wird. Bei der Einstellung false wird nur das Ende des Pfads zurückgegeben.</li></ul> | get_url_path(URL, FULL_PATH) | get_url_path(&quot;sftp://example.com//home/joe/employee.csv&quot;) | &quot;//home/joe/employee.csv&quot; |
| get_url_Abfrage_str | Gibt die Abfrage-Zeichenfolge einer angegebenen URL zurück. | <ul><li>URL: **Erforderlich** Die URL, von der Sie die Abfrage-Zeichenfolge abrufen möchten.</li><li>ANCHOR: **Erforderlich** Legt fest, was mit dem Anker in der Abfrage-Zeichenfolge geschehen soll. Kann einer von drei Werten sein: &quot;behalten&quot;, &quot;entfernen&quot;oder &quot;anhängen&quot;.<br><br>Wenn der Wert &quot;keep&quot;ist, wird der Anker an den zurückgegebenen Wert angehängt.<br>Wenn der Wert &quot;remove&quot;ist, wird der Anker aus dem zurückgegebenen Wert entfernt.<br>Wenn der Wert &quot;append&quot;ist, wird der Anker als separater Wert zurückgegeben.</li></ul> | get_url_Abfrage_str(URL, ANCHOR) | get_url_Abfrage_str(&quot;foo://example.com:8042/over/there?name=ferret#nose&quot;, &quot;preserve&quot;)<br>get_url_Abfrage_str(&quot;foo://example.com:8042/over/there?name=ferret#nose&quot;, &quot;remove&quot;)<br>get_url_Abfrage_str(&quot;foo://example.com:8042/over/there?name=ferret#nose&quot;, &quot;append&quot;) | `{"name": "ferret#nose"}`<br>`{"name": "ferret"}`<br>`{"name": "ferret", "_anchor_": "nose"}` |

### Datums- und Uhrzeitfunktionen

| Funktion | Beschreibung | Parameter | Syntax | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| now | Ruft die aktuelle Zeit ab. |  | now() | now() | `2020-09-23T10:10:24.556-07:00[America/Los_Angeles]` |
| timestamp | Ruft die aktuelle Unix-Zeit ab. |  | timestamp() | timestamp() | 1571850624571 |
| format | Formatiert das Eingabedatum nach einem angegebenen Format. | <ul><li>DATUM: **Erforderlich** Das Eingabedatum als ZonedDateTime-Objekt, das Sie formatieren möchten.</li><li>FORMAT: **Erforderlich** Das Format, in das das Datum geändert werden soll.</li></ul> | format(DATE, FORMAT) | format(2019-10-23T11:24:00+00:00, &quot;yyyy-MM-dd HH:mm:ss&quot;) | &quot;2019-10-23 11:24:35&quot; |
| dformat | Konvertiert einen Zeitstempel in eine Datums-Zeichenfolge in einem angegebenen Format. | <ul><li>ZEITSTEMPEL: **Erforderlich** Der Zeitstempel, den Sie formatieren möchten. Dies wird in Millisekunden geschrieben.</li><li>FORMAT: **Erforderlich** Das Format, in das der Zeitstempel geändert werden soll.</li></ul> | dformat(TIMESTAMP, FORMAT) | dformat(1571829875, &quot;dd-MMM-yyyy hh:mm&quot;) | &quot;23. Oktober 2019 11:24&quot; |
| date | Konvertiert eine Datums-Zeichenfolge in ein ZonedDateTime-Objekt (ISO 8601-Format). | <ul><li>DATUM: **Erforderlich** Die Zeichenfolge, die das Datum darstellt.</li><li>FORMAT: **Erforderlich** Die Zeichenfolge, die das Format des Datums darstellt.</li><li>DEFAULT_DATE: **Erforderlich** Das Standarddatum wird zurückgegeben, wenn das angegebene Datum null ist.</li></ul> | date(DATE, FORMAT, DEFAULT_DATE) | date(&quot;23-Okt-2019 11:24&quot;, &quot;yyyy/MM/dd&quot;, now()) | &quot;2019-10-23T11:24:00+00:00&quot; |
| date | Konvertiert eine Datums-Zeichenfolge in ein ZonedDateTime-Objekt (ISO 8601-Format). | <ul><li>DATUM: **Erforderlich** Die Zeichenfolge, die das Datum darstellt.</li><li>FORMAT: **Erforderlich** Die Zeichenfolge, die das Format des Datums darstellt.</li></ul> | date(DATE, FORMAT) | date(&quot;23-Okt-2019 11:24&quot;) | &quot;2019-10-23T11:24:00+00:00&quot; |
| date | Konvertiert eine Datums-Zeichenfolge in ein ZonedDateTime-Objekt (ISO 8601-Format). | <ul><li>DATUM: **Erforderlich** Die Zeichenfolge, die das Datum darstellt.</li></ul> | date(DATE) | date(&quot;23-Okt-2019 11:24&quot;, &quot;yyyy/MM/dd&quot;) | &quot;2019-10-23T11:24:00+00:00&quot; |
| date_part | Ruft die Teile des Datums ab. Die folgenden Komponentenwerte werden unterstützt: <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;&quot;quar&quot;<br>&quot;qq&quot;<br>&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;dayofyear&quot;<br>&quot;&quot;y&quot;heute&quot;dd&quot;d&quot;&quot;week&quot;dann&quot;ww&quot;direkt&quot;an&quot;wochentag&quot;dz&quot;wochentag&quot;w&quot;wochentag&quot;dz&quot;ggi&quot;&quot;h&quot;h&quot;hd&quot;hd&quot;h&quot;h&quot;h&quot;d&quot;h&quot;d&quot;h&quot;d&quot;d&quot;d&quot;d&quot;d&quot;d&quot;d&quot;möglicherweise&quot;unden&quot;oder&quot;möglicherweise&quot;oder&quot;b&quot;pause&quot;pause&quot;b&quot;pause&quot;b&quot;b&quot;bzw&quot;g&quot;mit&quot;b&quot;bzw&quot;bzw&quot;bzw&quot;jz&quot;jh&quot;jz&quot;jz&quot;jh&quot;<br>&quot;jz&quot;jz&quot;jz&quot;jz&quot;jz&quot;jz&quot;jh&quot;jz&quot;jh&quot;jz&quot;jz&quot;<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>&quot;jz&quot;jz&quot;jz&quot;jhh&quot;&quot;hh24&quot;&quot;hh12&quot;Minute&quot;&quot;mi&quot;&quot;&quot;&quot;im&quot;&quot;zweiter&quot;&quot;s&quot;&quot;Millisekunden&quot;&quot;ms&quot;ms&quot; | <ul><li>KOMPONENTE: **Erforderlich** Eine Zeichenfolge, die den Teil des Datums darstellt. </li><li>DATUM: **Erforderlich** Das Datum in einem Standardformat.</li></ul> | date_part(COMPONENT, DATE) | date_part(&quot;MM&quot;, date(&quot;2019-10-17 11:55:12&quot;)) | 10 |
| set_date_part | Ersetzt eine Komponente in einem bestimmten Datum. Die folgenden Komponenten werden akzeptiert: <br><br>&quot;year&quot;<br>&quot;year&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;hour&quot;<br><br><br><br><br><br><br><br><br>&quot;hh&quot;&quot;mi&quot;&quot;&quot;n&quot;&quot;&quot;&quot;s&quot;&quot;s&quot;&quot;s&quot;s&quot;s&quot;s&quot;s&quot;s&quot; | <ul><li>KOMPONENTE: **Erforderlich** Eine Zeichenfolge, die den Teil des Datums darstellt. </li><li>WERT: **Erforderlich** Der für die Komponente für ein bestimmtes Datum festzulegende Wert.</li><li>DATUM: **Erforderlich** Das Datum in einem Standardformat.</li></ul> | set_date_part(COMPONENT, VALUE, DATE) | set_date_part(&quot;m&quot;, 4, date(&quot;2016-11-09T11:44:44.797&quot;) | &quot;2016-04-09T11:44:44.797&quot; |
| make_date_time | Erstellt ein Datum aus Teilen. Diese Funktion kann auch mithilfe von make_timestamp ausgelöst werden. | <ul><li>JAHR: **Erforderlich** Das vierstellige Jahr.</li><li>MONAT: **Erforderlich** der Monat. Die zulässigen Werte sind 1 bis 12.</li><li>TAG: **Erforderlich** der Tag. Die zulässigen Werte sind 1 bis 31.</li><li>STUNDE: **Die Stunde war erforderlich** . Die zulässigen Werte liegen zwischen 0 und 23.</li><li>MINUTE: **Erforderlich** Die Minute. Die zulässigen Werte liegen zwischen 0 und 59.</li><li>NANOSECOND: **Erforderlich** Die nanosekunden Werte. Die zulässigen Werte sind 0 bis 9999999999.</li><li>TIMEZONE: **Erforderlich** Die Zeitzone für die Datumszeit.</li></ul> | make_date_time(YEAR, MONTH, DAY, HOUR, MINUTE, SECOND, NANOSECOND, TIMEZONE) | make_date_time(2019, 10, 17, 11, 55, 12, 999, &quot;America/Los_Angeles&quot;) | `2019-10-17T11:55:12.0&#x200B;00000999-07:00[America/Los_Angeles]` |
| zone_date_to_utc | Konvertiert ein Datum in einer beliebigen Zeitzone in ein Datum in UTC. | <ul><li>DATUM: **Erforderlich** Das Datum, das konvertiert werden soll.</li></ul> | zone_date_to_utc(DATE) | `zone_date_to_utc(2019-10-17T11:55:12.000000999-07:00[America/Los_Angeles])` | `2019-10-17T18:55:12.000000999Z[UTC]` |
| zone_date_to_zone | Konvertiert ein Datum aus einer Zeitzone in eine andere Zeitzone. | <ul><li>DATUM: **Erforderlich** Das Datum, das konvertiert werden soll.</li><li>ZONE: **Erforderlich** Die Zeitzone, in die Sie das Datum konvertieren möchten.</li></ul> | zone_date_to_zone(DATE, ZONE) | `zone_date_to_utc(2019-10-17T11:55:12.000000999-07:00[America/Los_Angeles], "Europe/Paris")` | `2019-10-17T20:55:12.000000999+02:00[Europe/Paris]` |

### Hierarchien - Objekte

| Funktion | Beschreibung | Parameter | Syntax | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| size_of | Gibt die Größe der Eingabe zurück. | <ul><li>INPUT: **Erforderlich** Das Objekt, dessen Größe Sie ermitteln möchten.</li></ul> | size_of(INPUT) | `size_of([1, 2, 3, 4])` | 4 |
| is_empty | Überprüft, ob ein Objekt leer ist. | <ul><li>INPUT: **Erforderlich** Das Objekt, das Sie überprüfen möchten, ist leer.</li></ul> | is_empty(INPUT) | `is_empty([1, 2, 3])` | false |
| arrays_to_object | Erstellt eine Liste von Objekten. | <ul><li>INPUT: **Erforderlich** Eine Gruppierung von Schlüssel- und Array-Paaren.</li></ul> | arrays_to_object(INPUT) | Bedarfsprobe | Bedarfsprobe |
| to_object | Erstellt ein Objekt basierend auf den gegebenen einfachen Schlüssel/Wert-Paaren. | <ul><li>INPUT: **Erforderlich** Eine einfache Liste von Schlüssel/Wert-Paaren.</li></ul> | to_object(INPUT) | to_object(&quot;firstName&quot;, &quot;John&quot;, &quot;lastName&quot;, &quot;Doe&quot;) | `{"firstName": "John", "lastName": "Doe"}` |
| str_to_object | Erstellt ein Objekt aus der Eingabezeichenfolge. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, die analysiert wird, um ein Objekt zu erstellen.</li><li>VALUE_DELIMITER: *Optional* Das Trennzeichen, das ein Feld vom Wert trennt. The default delimiter is `:`.</li><li>FIELD_DELIMITER: *Optional* Das Trennzeichen, das Feldwertpaare voneinander trennt. The default delimiter is `,`.</li></ul> | str_to_object(STRING, VALUE_DELIMITER, FIELD_DELIMITER) | str_to_object(&quot;firstName - John | lastName - | phone - 123 456 7890&quot;, &quot;-&quot;, &quot; | &quot;) | `{"firstName": "John", "lastName": "Doe", "phone": "123 456 7890"}` |
| is_set | Überprüft, ob das Objekt in den Quelldaten vorhanden ist. | <ul><li>INPUT: **Erforderlich** Der Pfad, der überprüft werden soll, wenn er in den Quelldaten vorhanden ist.</li></ul> | is_set(INPUT) | is_set(&quot;evars.evar.field1&quot;) | wahr |

### Hierarchien - Arrays

| Funktion | Beschreibung | Parameter | Syntax | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| coalesce | Gibt das erste nicht-Null-Objekt in einem gegebenen Array zurück. | <ul><li>INPUT: **Erforderlich** Das Array, von dem Sie das erste Objekt ohne null suchen möchten.</li></ul> | coalesce(INPUT) | coalesce(null, null, null, &quot;first&quot;, null, &quot;second&quot;) | &quot;first&quot; |
| first | Ruft das erste Element des angegebenen Arrays ab. | <ul><li>INPUT: **Erforderlich** Das Array, in dem Sie das erste Element suchen möchten.</li></ul> | first(INPUT) | first(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;1&quot; |
| last | Ruft das letzte Element des angegebenen Arrays ab. | <ul><li>INPUT: **Erforderlich** Das Array, in dem Sie das letzte Element suchen möchten.</li></ul> | last(INPUT) | last(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;3&quot; |
| to_array | Führt eine Liste von Eingaben durch und konvertiert sie in ein Array. | <ul><li>INCLUDE_NULLS: **Erforderlich** Ein boolescher Wert, der angibt, ob Nullen in das Antwortarray aufgenommen werden sollen.</li><li>WERTE: **Erforderlich** Die Elemente, die in ein Array konvertiert werden sollen.</li></ul> | to_array(INCLUDE_NULLS, VALUES) | to_array(false, 1, null, 2, 3) | `[1, 2, 3]` |

### Logische Operatoren

| Funktion | Beschreibung | Parameter | Syntax | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| decode | Bei einem Schlüssel und einer Liste von Schlüsselwertpaaren, die als Array reduziert sind, gibt die Funktion den Wert zurück, wenn der Schlüssel gefunden wird, oder gibt einen Standardwert zurück, wenn er im Array vorhanden ist. | <ul><li>SCHLÜSSEL: **Erforderlich** Der Schlüssel, der übereinstimmen soll.</li><li>OPTIONS: **Erforderlich** Ein reduziertes Array mit Schlüssel/Wert-Paaren. Optional kann ein Standardwert am Ende gesetzt werden.</li></ul> | decode(KEY, OPTIONS) | decode(stateCode, &quot;ca&quot;, &quot;California&quot;, &quot;pa&quot;, &quot;Pennsylvania&quot;, &quot;N/A&quot;) | Lautet der angegebene stateCode &quot;ca&quot;, &quot;California&quot;.<br>Lautet der angegebene stateCode &quot;pa&quot;, &quot;Pennsylvania&quot;.<br>Wenn der stateCode nicht mit dem Folgenden übereinstimmt, &quot;K/A&quot;. |
| iif | Wertet einen bestimmten booleschen Ausdruck aus und gibt den angegebenen Wert basierend auf dem Ergebnis zurück. | <ul><li>BOOLEAN_AUSDRUCK: **Erforderlich** Der boolesche Ausdruck, der ausgewertet wird.</li><li>TRUE_VALUE: **Erforderlich** Der Wert, der zurückgegeben wird, wenn der Ausdruck &quot;true&quot;ergibt.</li><li>FALSE_VALUE: **Erforderlich** Der Wert, der zurückgegeben wird, wenn der Ausdruck den Wert &quot;false&quot;ergibt.</li></ul> | iif(BOOLEAN_AUSDRUCK, TRUE_VALUE, FALSE_VALUE) | iif(&quot;s&quot;.equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;True&quot; |

### Aggregation

| Funktion | Beschreibung | Parameter | Syntax | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| min | Gibt das Minimum der angegebenen Argumente zurück. Verwendet die natürliche Reihenfolge. | <ul><li>OPTIONS: **Erforderlich** Ein oder mehrere Objekte, die miteinander verglichen werden können.</li></ul> | min(OPTIONS) | min(3, 1, 4) | 1 |
| max | Gibt das Maximum der angegebenen Argumente zurück. Verwendet die natürliche Reihenfolge. | <ul><li>OPTIONS: **Erforderlich** Ein oder mehrere Objekte, die miteinander verglichen werden können.</li></ul> | max(OPTIONS) | max(3, 1, 4) | 4 |

### Typkonvertierungen

| Funktion | Beschreibung | Parameter | Syntax | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| to_bigint | Konvertiert eine Zeichenfolge in eine BigInteger-Zeichenfolge. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, die in einen BigInteger konvertiert werden soll.</li></ul> | to_bigint(STRING) | to_bigint(&quot;1000000.34&quot;) | 1000000.34 |
| to_decimal | Konvertiert eine Zeichenfolge in eine Dublette. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, die in eine Dublette konvertiert werden soll.</li></ul> | to_decimal(STRING) | to_decimal(&quot;20.5&quot;) | 20.5 |
| to_float | Konvertiert eine Zeichenfolge in eine Gleitkommazahl. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, die in eine Gleitkommazahl konvertiert werden soll.</li></ul> | to_float(STRING) | to_float(&quot;12.3456&quot;) | 12.34566 |
| to_integer | Konvertiert eine Zeichenfolge in eine Ganzzahl. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, die in eine Ganzzahl umgewandelt werden soll.</li></ul> | to_integer(STRING) | to_integer(&quot;12&quot;) | 12 |

### JSON-Funktionen

| Funktion | Beschreibung | Parameter | Syntax | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| json_to_object | Deserialisieren Sie den JSON-Inhalt aus der angegebenen Zeichenfolge. | <ul><li>STRING: **Die zu deserialisierende JSON-Zeichenfolge war erforderlich** .</li></ul> | json_to_object(STRING) | json_to_object({&quot;info&quot;:{&quot;firstName&quot;:&quot;John&quot;,&quot;lastName&quot; : &quot;Doe&quot;}) | Ein Objekt, das die JSON darstellt. |

### Besondere Maßnahmen

| Funktion | Beschreibung | Parameter | Syntax | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| uuid /<br>guid | Erstellt eine pseudo-zufällige ID. |  | uuid()<br>guid() | uuid()<br>guid() | 7c0267d2-bb74-4e1a-9275-3bf4fccda5f4<br>c7016dc7-3163-43f7-afc7-2e1c9c206333 |

### Benutzeragenten-Funktionen

| Funktion | Beschreibung | Parameter | Syntax | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| ua_os_name | Extrahiert den Betriebssystemnamen aus der Benutzeragenten-Zeichenfolge. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragenten-Zeichenfolge.</li></ul> | ua_os_name(USER_AGENT) | ua_os_name(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 (wie Mac OS X) AppleWebKit/534.46 (KHTML, wie Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS |
| ua_os_version_major | Extrahiert die Hauptversion des Betriebssystems aus der Benutzeragenten-Zeichenfolge. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragenten-Zeichenfolge.</li></ul> | ua_os_version_major(USER_AGENT) | ua_os_version_major(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 (wie Mac OS X) AppleWebKit/534.46 (KHTML, wie Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5 |
| ua_os_version | Extrahiert die Version des Betriebssystems aus der Benutzeragenten-Zeichenfolge. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragenten-Zeichenfolge.</li></ul> | ua_os_version(USER_AGENT) | ua_os_version(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 (wie Mac OS X) AppleWebKit/534.46 (KHTML, wie Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1.1 |
| ua_os_name_version | Extrahiert den Namen und die Version des Betriebssystems aus der Benutzeragenten-Zeichenfolge. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragenten-Zeichenfolge.</li></ul> | ua_os_name_version(USER_AGENT) | ua_os_name_version(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 (wie Mac OS X) AppleWebKit/534.46 (KHTML, wie Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5.1.1 |
| ua_agent_version | Extrahiert die Agentversion aus der Benutzeragenten-Zeichenfolge. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragenten-Zeichenfolge.</li></ul> | ua_agent_version(USER_AGENT) | ua_agent_version(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 (wie Mac OS X) AppleWebKit/534.46 (KHTML, wie Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1 |
| ua_agent_version_major | Extrahiert den Agentnamen und die Hauptversion aus der Benutzeragenten-Zeichenfolge. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragenten-Zeichenfolge.</li></ul> | ua_agent_version_major(USER_AGENT) | ua_agent_version_major(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 (wie Mac OS X) AppleWebKit/534.46 (KHTML, wie Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari 5 |
| ua_agent_name | Extrahiert den Agenten-Namen aus der Benutzeragenten-Zeichenfolge. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragenten-Zeichenfolge.</li></ul> | ua_agent_name(USER_AGENT) | ua_agent_name(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 (wie Mac OS X) AppleWebKit/534.46 (KHTML, wie Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari |
| ua_device_class | Extrahiert die Geräteklasse aus der Benutzeragenten-Zeichenfolge. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragenten-Zeichenfolge.</li></ul> | ua_device_class(USER_AGENT) | ua_device_class(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 (wie Mac OS X) AppleWebKit/534.46 (KHTML, wie Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Telefon |