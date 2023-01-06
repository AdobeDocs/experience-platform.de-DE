---
keywords: Experience Platform; Startseite; beliebte Themen; CSV zuordnen; CSV-Datei zuordnen; CSV-Datei xdm zuordnen; CSV xdm zuordnen; UI-Handbuch; Mapper; Mapping; Zuordnungsfelder; Zuordnungsfunktionen
solution: Experience Platform
title: Zuordnungsfunktionen für Datenvorbereitung
description: In diesem Dokument werden die mit der Datenvorbereitung verwendeten Zuordnungsfunktionen vorgestellt.
exl-id: e95d9329-9dac-4b54-b804-ab5744ea6289
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '4367'
ht-degree: 8%

---

# Funktionen zur Datenvorbereitung

Mit Datenvorbereitung-Funktionen können Werte basierend auf den in Quellfeldern eingegebenen Werten berechnet und berechnet werden.

## Felder

Ein Feldname kann eine beliebige gültige Kennung sein - eine unbegrenzte Sequenz von Unicode-Buchstaben und -Ziffern, beginnend mit einem Buchstaben, dem Dollarzeichen (`$`) oder dem Unterstrich (`_`). Bei Variablennamen wird auch zwischen Groß- und Kleinschreibung unterschieden.

Wenn ein Feldname dieser Konvention nicht entspricht, muss der Feldname mit `${}`. Wenn der Feldname beispielsweise &quot;Vorname&quot;oder &quot;Vorname&quot;lautet, muss der Name wie folgt umgebrochen werden: `${First Name}` oder `${First\.Name}` bzw.

>[!TIP]
>
>Wenn bei der Interaktion mit Hierarchien ein untergeordnetes Attribut einen Punkt (`.`), müssen Sie einen umgekehrten Schrägstrich (`\`), um Sonderzeichen zu maskieren. Weitere Informationen finden Sie im Handbuch unter [Maskieren von Sonderzeichen](home.md#escape-special-characters).

Wenn ein Feldname **any** der folgenden reservierten Schlüsselwörter, muss sie mit `${}`:

```console
new, mod, or, break, var, lt, for, false, while, eq, gt, div, not, null, continue, else, and, ne, true, le, if, ge, return, _errors
```

Auf Daten in Unterfeldern kann mithilfe der Punktnotation zugegriffen werden. Wenn beispielsweise eine `name` -Objekt, um auf die `firstName` Feld, verwenden `name.firstName`.

## Funktionsliste

In den folgenden Tabellen sind alle unterstützten Zuordnungsfunktionen aufgeführt, einschließlich Beispielausdrücke und der resultierenden Ausgaben.

### Zeichenfolgen-Funktionen {#string}

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Funktion | Beschreibung | Parameter | Aufbau | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| concat | Verkettet die angegebenen Zeichenfolgen. | <ul><li>STRING: Die verketteten Zeichenfolgen.</li></ul> | concat(STRING_1, STRING_2) | concat(&quot;Hi, &quot;, &quot;There&quot;, &quot;!&quot;) | `"Hi, there!"` |
| explode | Teilt die Zeichenfolge basierend auf einem Regex und gibt ein Array von Teilen zurück. Kann optional regex enthalten, um die Zeichenfolge zu teilen. Standardmäßig wird die Aufteilung in &quot;,&quot;aufgelöst. Die folgenden Trennzeichen **need** zu maskieren mit `\`: `+, ?, ^, \|, ., [, (, {, ), *, $, \` Wenn Sie mehrere Zeichen als Trennzeichen angeben, wird das Trennzeichen als Trennzeichen mit mehreren Zeichen behandelt. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, die geteilt werden muss.</li><li>REGEX: *Optional* Der reguläre Ausdruck, der zum Aufteilen der Zeichenfolge verwendet werden kann.</li></ul> | explode(STRING, REGEX) | explode(&quot;Hallo, da!&quot;, &quot;&quot;) | `["Hi,", "there"]` |
| instr | Gibt die Position/den Index einer Unterzeichenfolge zurück. | <ul><li>EINGABE: **Erforderlich** Die Zeichenfolge, die gesucht wird.</li><li>SUBSTRING: **Erforderlich** Die Unterzeichenfolge, nach der in der Zeichenfolge gesucht wird.</li><li>START_POSITION: *Optional* Die Position, an der die Suche in der Zeichenfolge beginnen soll.</li><li>VORKOMMEN: *Optional* Das n-te Vorkommen, nach dem von der Startposition aus gesucht werden soll. Standardmäßig ist dies 1. </li></ul> | instr(INPUT, SUBSTRING, START_POSITION, OCCURRENCE) | instr(&quot;adobe.com&quot;, &quot;com&quot;) | 6 |
| replace | Ersetzt die Suchzeichenfolge, sofern sie in der ursprünglichen Zeichenfolge vorhanden ist. | <ul><li>EINGABE: **Erforderlich** Die Eingabezeichenfolge.</li><li>TO_FIND: **Erforderlich** Die Zeichenfolge, die in der Eingabe nachgeschlagen werden soll.</li><li>TO_REPLACE: **Erforderlich** Die Zeichenfolge, die den Wert in &quot;TO_FIND&quot;ersetzt.</li></ul> | replacestr(INPUT, TO_FIND, TO_REPLACE) | replacestr(&quot;This is a string re test&quot;, &quot;re&quot;, &quot;replace&quot;) | &quot;Dies ist ein string replace-Test&quot; |
| substr | Gibt eine Teilzeichenfolge einer angegebenen Länge zurück. | <ul><li>EINGABE: **Erforderlich** Die Eingabezeichenfolge.</li><li>START_INDEX: **Erforderlich** Der Index der Eingabezeichenfolge, in der die Teilzeichenfolge beginnt.</li><li>LÄNGE: **Erforderlich** Die Länge der Teilzeichenfolge.</li></ul> | substr(INPUT, START_INDEX, LENGTH) | substr(&quot;This is a substring test&quot;, 7, 8) | &quot;a subst&quot; |
| lower /<br>lcase | Konvertiert einen String in Kleinbuchstaben. | <ul><li>EINGABE: **Erforderlich** Die Zeichenfolge, die in Kleinbuchstaben umgewandelt wird.</li></ul> | lower(INPUT) | lower(&quot;HeLLo&quot;)<br>lcase(&quot;HeLLo&quot;) | &quot;hello&quot; |
| upper /<br>ucase | Konvertiert einen String in Großbuchstaben. | <ul><li>EINGABE: **Erforderlich** Die Zeichenfolge, die in Großbuchstaben umgewandelt wird.</li></ul> | upper(INPUT) | upper(&quot;HeLLo&quot;)<br>ucase(&quot;HeLLo&quot;) | &quot;HELLO&quot; |
| split | Teilt eine Eingabezeichenfolge auf einem Trennzeichen. Das folgende Trennzeichen **need** zu maskieren mit `\`: `\`. Wenn Sie mehrere Trennzeichen einschließen, wird die Zeichenfolge auf **any** der in der Zeichenfolge vorhandenen Trennzeichen. | <ul><li>EINGABE: **Erforderlich** Die Eingabezeichenfolge, die geteilt werden soll.</li><li>SEPARATOR: **Erforderlich** Die Zeichenfolge, die zum Aufteilen der Eingabe verwendet wird.</li></ul> | split(INPUT, SEPARATOR) | split(&quot;Hello World&quot;, &quot;&quot;) | `["Hello", "world"]` |
| join | Verbindet eine Liste von Objekten mithilfe des Trennzeichens. | <ul><li>SEPARATOR: **Erforderlich** Die Zeichenfolge, die zum Verbinden der Objekte verwendet wird.</li><li>OBJEKTE: **Erforderlich** Ein Array von Zeichenfolgen, die verknüpft werden.</li></ul> | `join(SEPARATOR, [OBJECTS])` | `join(" ", to_array(true, "Hello", "world"))` | &quot;Hello World&quot; |
| lpad | Fügt die linke Seite einer Zeichenfolge mit der anderen angegebenen Zeichenfolge ein. | <ul><li>EINGABE: **Erforderlich** Die Zeichenfolge, die eingefügt werden soll. Diese Zeichenfolge kann null sein.</li><li>COUNT: **Erforderlich** Die Größe der Zeichenfolge, die eingefügt werden soll.</li><li>HINZUFÜGEN: **Erforderlich** Die Zeichenfolge, mit der die Eingabe aufgefüllt werden soll. Wenn null oder leer, wird es als einzelnes Leerzeichen behandelt.</li></ul> | lpad(INPUT, COUNT, PADDING) | lpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;yzyzybat&quot; |
| rpad | Fügt die rechte Seite einer Zeichenfolge mit der anderen angegebenen Zeichenfolge ein. | <ul><li>EINGABE: **Erforderlich** Die Zeichenfolge, die eingefügt werden soll. Diese Zeichenfolge kann null sein.</li><li>COUNT: **Erforderlich** Die Größe der Zeichenfolge, die eingefügt werden soll.</li><li>HINZUFÜGEN: **Erforderlich** Die Zeichenfolge, mit der die Eingabe aufgefüllt werden soll. Wenn null oder leer, wird es als einzelnes Leerzeichen behandelt.</li></ul> | rpad(INPUT, COUNT, PADDING) | rpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;batyzyzy&quot; |
| left | Ruft die ersten n Zeichen der angegebenen Zeichenfolge ab. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, für die Sie die ersten n Zeichen erhalten.</li><li>COUNT: **Erforderlich** Die &quot;n&quot;-Zeichen, die aus der Zeichenfolge abgerufen werden sollen.</li></ul> | left(STRING, COUNT) | left(&quot;abcde&quot;, 2) | &quot;ab&quot; |
| right | Ruft die letzten n Zeichen der angegebenen Zeichenfolge ab. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, für die Sie die letzten n Zeichen erhalten.</li><li>COUNT: **Erforderlich** Die &quot;n&quot;-Zeichen, die aus der Zeichenfolge abgerufen werden sollen.</li></ul> | right(STRING, COUNT) | right(&quot;abcde&quot;, 2) | &quot;de&quot; |
| ltrim | Entfernt den Leerraum am Anfang des Strings. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, aus der Sie den Leerraum entfernen möchten.</li></ul> | ltrim(STRING) | ltrim(&quot; hello&quot;) | &quot;hello&quot; |
| rtrim | Entfernt den Leerraum am Ende der Zeichenfolge. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, aus der Sie den Leerraum entfernen möchten.</li></ul> | rtrim(STRING) | rtrim(&quot;hello &quot;) | &quot;hello&quot; |
| trim | Entfernt den Leerraum vom Anfang und vom Ende der Zeichenfolge. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, aus der Sie den Leerraum entfernen möchten.</li></ul> | trim(STRING) | trim(&quot; hello &quot;) | &quot;hello&quot; |
| gleich | Vergleicht zwei Zeichenketten, um sicherzustellen, dass sie gleich sind. Bei dieser Funktion wird zwischen Groß- und Kleinschreibung unterschieden. | <ul><li>STRING1: **Erforderlich** Die erste Zeichenfolge, die Sie vergleichen möchten.</li><li>STRING2: **Erforderlich** Die zweite Zeichenfolge, die Sie vergleichen möchten.</li></ul> | STRING1. &#x200B;equals( &#x200B; STRING2) | &quot;string1&quot;. &#x200B;equals &#x200B;(&quot;STRING1&quot;) | false |
| equalsIgnoreCase | Vergleicht zwei Zeichenketten, um sicherzustellen, dass sie gleich sind. Diese Funktion ist **not** Groß-/Kleinschreibung beachten. | <ul><li>STRING1: **Erforderlich** Die erste Zeichenfolge, die Sie vergleichen möchten.</li><li>STRING2: **Erforderlich** Die zweite Zeichenfolge, die Sie vergleichen möchten.</li></ul> | STRING1. &#x200B;equalsIgnoreCase &#x200B;(STRING2) | &quot;string1&quot;. &#x200B;equalsIgnoreCase &#x200B;(&quot;STRING1) | wahr |

{style=&quot;table-layout:auto&quot;}

### Funktionen mit reguläreren Ausdrücken

| Funktion | Beschreibung | Parameter | Aufbau | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| extract_regex | Extrahiert basierend auf einem regulären Ausdruck Gruppen aus der Eingabezeichenfolge. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, aus der Sie die Gruppen extrahieren.</li><li>REGEX: **Erforderlich** Der reguläre Ausdruck, mit dem die Gruppe übereinstimmen soll.</li></ul> | extract_regex(STRING, REGEX) | extract_regex &#x200B;(&quot;E259,E259B_009,1_1&quot; &#x200B;, &quot;([^,]+),[^,]*,([^,]+)&quot;) | [&quot;E259,E259B_009,1_1&quot;, &quot;E259&quot;, &quot;1_1&quot;] |
| matches_regex | Überprüft, ob die Zeichenfolge mit dem eingegebenen regulären Ausdruck übereinstimmt. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, die Sie überprüfen, entspricht dem regulären Ausdruck.</li><li>REGEX: **Erforderlich** Der reguläre Ausdruck, mit dem Sie vergleichen.</li></ul> | matches_regex(STRING, REGEX) | matches_regex(&quot;E259,E259B_009,1_1&quot;, &quot;([^,]+),[^,]*,([^,]+)&quot;) | wahr |

{style=&quot;table-layout:auto&quot;}

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

{style=&quot;table-layout:auto&quot;}

### URL-Funktionen {#url}

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Funktion | Beschreibung | Parameter | Aufbau | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| get_url_protocol | Gibt das Protokoll aus der angegebenen URL zurück. Wenn die Eingabe ungültig ist, wird null zurückgegeben. | <ul><li>URL: **Erforderlich** Die URL, aus der das Protokoll extrahiert werden soll.</li></ul> | get_url_protocol &#x200B;(URL) | get_url_protocol(&quot;https://platform &#x200B; .adobe.com/home&quot;) | https |
| get_url_host | Gibt den Host der angegebenen URL zurück. Wenn die Eingabe ungültig ist, wird null zurückgegeben. | <ul><li>URL: **Erforderlich** Die URL, aus der der Host extrahiert werden muss.</li></ul> | get_url_host &#x200B;(URL) | get_url_host &#x200B;(&quot;https://platform &#x200B; .adobe.com/home&quot;) | platform.adobe.com |
| get_url_port | Gibt den Port der angegebenen URL zurück. Wenn die Eingabe ungültig ist, wird null zurückgegeben. | <ul><li>URL: **Erforderlich** Die URL, aus der der Port extrahiert werden muss.</li></ul> | get_url_port(URL) | get_url_port &#x200B;(&quot;sftp://example.com//home/ &#x200B; joe/employee.csv&quot;) | 22 |
| get_url_path | Gibt den Pfad der angegebenen URL zurück. Standardmäßig wird der vollständige Pfad zurückgegeben. | <ul><li>URL: **Erforderlich** Die URL, aus der der Pfad extrahiert werden muss.</li><li>FULL_PATH: *Optional* Ein boolean -Wert, der bestimmt, ob der vollständige Pfad zurückgegeben wird. Wenn der Wert auf &quot;false&quot;gesetzt ist, wird nur das Ende des Pfads zurückgegeben.</li></ul> | get_url_path &#x200B;(URL, FULL_PATH) | get_url_path &#x200B;(&quot;sftp://example.com// &#x200B; home/joe/employee.csv&quot;) | &quot;//home/joe/&#x200B; employee.csv&quot; |
| get_url_query_str | Gibt die Abfragezeichenfolge einer angegebenen URL als Zuordnung des Abfragezeichenfolgennamens und des Abfragezeichenfolgenwerts zurück. | <ul><li>URL: **Erforderlich** Die URL, von der Sie die Abfragezeichenfolge abrufen möchten.</li><li>ANCHOR: **Erforderlich** Bestimmt, was mit dem Anker in der Abfragezeichenfolge ausgeführt wird. Kann einer von drei Werten sein: &quot;keep&quot;, &quot;remove&quot;oder &quot;append&quot;.<br><br>Wenn der Wert &quot;keep&quot;lautet, wird der Anker an den zurückgegebenen Wert angehängt.<br>Wenn der Wert &quot;remove&quot;lautet, wird der Anker aus dem zurückgegebenen Wert entfernt.<br>Wenn der Wert &quot;append&quot;lautet, wird der Anker als separater Wert zurückgegeben.</li></ul> | get_url_query_str &#x200B;(URL, ANCHOR) | get_url_query_str &#x200B;(&quot;foo://example.com:8042 &#x200B;/over/dahin?name= &#x200B; ferret#nose&quot;, &quot;keep&quot;)<br>get_url_query_str &#x200B;(&quot;foo://example.com:8042 &#x200B;/over/dahin?name= &#x200B; ferret#nose&quot;, &quot;remove&quot;)<br>get_url_query_str &#x200B;(&quot;foo://example.com &#x200B;:8042/over/gibt &#x200B;?name=ferret#nose&quot;, &quot;append&quot;) | `{"name": "ferret#nose"}`<br>`{"name": "ferret"}`<br>`{"name": "ferret", "_anchor_": "nose"}` |

{style=&quot;table-layout:auto&quot;}

### Datums- und Uhrzeitfunktionen {#date-and-time}

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen. Weitere Informationen zu `date` -Funktion finden Sie im Abschnitt Datumsangaben des [Handbuch zur Handhabung von Datenformaten](./data-handling.md#dates).

| Funktion | Beschreibung | Parameter | Aufbau | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| now | Ruft die aktuelle Zeit ab. |  | now() | now() | `2021-10-26T10:10:24Z` |
| timestamp | Ruft die aktuelle Unix-Zeit ab. |  | timestamp() | timestamp() | 1571850624571 |
| format | Formatiert das Eingabedatum in einem angegebenen Format. | <ul><li>DATUM: **Erforderlich** Das Eingabedatum als ZonedDateTime -Objekt, das Sie formatieren möchten.</li><li>FORMAT: **Erforderlich** Das Format, in das das Datum geändert werden soll.</li></ul> | format(DATE, FORMAT) | format(2019-10-23T11):24:00+00:00, &quot;yyyy-MM-dd HH:mm:ss&quot;) | `2019-10-23 11:24:35` |
| dformat | Konvertiert einen Zeitstempel in eine Datums-Zeichenfolge in einem angegebenen Format. | <ul><li>ZEITSTEMPEL: **Erforderlich** Der Zeitstempel, den Sie formatieren möchten. Dies wird in Millisekunden geschrieben.</li><li>FORMAT: **Erforderlich** Das Format, in dem der Zeitstempel verwendet werden soll.</li></ul> | dformat(TIMESTAMP, FORMAT) | dformat(1571829875000, &quot;yyyy-MM-dd&#39;T&#39;HH&quot;:mm:ss.SSSX&quot;) | `2019-10-23T11:24:35.000Z` |
| date | Konvertiert eine Datums-Zeichenfolge in ein ZonedDateTime-Objekt (ISO 8601-Format). | <ul><li>DATUM: **Erforderlich** Die Zeichenfolge, die das Datum darstellt.</li><li>FORMAT: **Erforderlich** Die Zeichenfolge, die das Format des Quelldatums darstellt.**Hinweis:** Dies geschieht **not** das Format darstellen, in das Sie die Datums-Zeichenfolge konvertieren möchten. </li><li>DEFAULT_DATE: **Erforderlich** Das Standarddatum, das zurückgegeben wird, wenn das angegebene Datum null ist.</li></ul> | date(DATE, FORMAT, DEFAULT_DATE) | date(&quot;2019-10-23 11:24&quot;, &quot;yyy-MM-dd HH:mm&quot;, now()) | `2019-10-23T11:24:00Z` |
| date | Konvertiert eine Datums-Zeichenfolge in ein ZonedDateTime-Objekt (ISO 8601-Format). | <ul><li>DATUM: **Erforderlich** Die Zeichenfolge, die das Datum darstellt.</li><li>FORMAT: **Erforderlich** Die Zeichenfolge, die das Format des Quelldatums darstellt.**Hinweis:** Dies geschieht **not** das Format darstellen, in das Sie die Datums-Zeichenfolge konvertieren möchten. </li></ul> | date(DATE, FORMAT) | date(&quot;2019-10-23 11:24&quot;, &quot;yyy-MM-dd HH:mm&quot;) | `2019-10-23T11:24:00Z` |
| date | Konvertiert eine Datums-Zeichenfolge in ein ZonedDateTime-Objekt (ISO 8601-Format). | <ul><li>DATUM: **Erforderlich** Die Zeichenfolge, die das Datum darstellt.</li></ul> | date(DATE) | date(&quot;2019-10-23 11:24&quot;) | &quot;2019-10-23T11:24:00Z&quot; |
| date_part | Ruft die Teile des Datums ab. Die folgenden Komponentenwerte werden unterstützt: <br><br>&quot;year&quot;<br>&quot;jjj&quot;<br>&quot;yy&quot;<br><br>&quot;quarter&quot;<br>&quot;qq&quot;<br>&quot;q&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;dayofyear&quot;<br>&quot;dy&quot;<br>&quot;y&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;week&quot;<br>&quot;ww&quot;<br>&quot;w&quot;<br><br>&quot;Wochentag&quot;<br>&quot;dw&quot;<br>&quot;w&quot;<br><br>&quot;hour&quot;<br>&quot;hh&quot;<br>&quot;hh24&quot;<br>&quot;hh12&quot;<br><br>&quot;minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;second&quot;<br>&quot;ss&quot;<br>&quot;s&quot;<br><br>&quot;millisecond&quot;<br>&quot;ms&quot; | <ul><li>KOMPONENTE: **Erforderlich** Eine Zeichenfolge, die den Teil des Datums darstellt. </li><li>DATUM: **Erforderlich** Das Datum in einem Standardformat.</li></ul> | date_part &#x200B;(COMPONENT, DATE) | date_part(&quot;MM&quot;, date(&quot;2019-10-17 11&quot;):55:12&quot;) | 10 |
| set_date_part | Ersetzt eine Komponente an einem bestimmten Datum. Folgende Komponenten werden akzeptiert: <br><br>&quot;year&quot;<br>&quot;jjj&quot;<br>&quot;yy&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;hour&quot;<br>&quot;hh&quot;<br><br>&quot;minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;second&quot;<br>&quot;ss&quot;<br>&quot;s&quot; | <ul><li>KOMPONENTE: **Erforderlich** Eine Zeichenfolge, die den Teil des Datums darstellt. </li><li>WERT: **Erforderlich** Der Wert, der für die Komponente für ein bestimmtes Datum festgelegt werden soll.</li><li>DATUM: **Erforderlich** Das Datum in einem Standardformat.</li></ul> | set_date_part &#x200B;(COMPONENT, VALUE, DATE) | set_date_part(&quot;m&quot;, 4, date(&quot;2016-11-09T11&quot;):44:44.797&quot;) | &quot;2016-04-09T11:44:44Z&quot; |
| make_date_time | Erstellt ein Datum aus Teilen. Diese Funktion kann auch mit make_timestamp ausgelöst werden. | <ul><li>JAHR: **Erforderlich** Das Jahr, vierstellig geschrieben.</li><li>MONAT: **Erforderlich** Der Monat. Die zulässigen Werte sind 1 bis 12.</li><li>TAG: **Erforderlich** Der Tag. Die zulässigen Werte sind 1 bis 31.</li><li>STUNDE: **Erforderlich** Die Stunde. Die zulässigen Werte sind 0 bis 23.</li><li>MINUTE: **Erforderlich** Die Minute. Die zulässigen Werte sind 0 bis 59.</li><li>NANOSECOND: **Erforderlich** Die Nanosekundenwerte. Die zulässigen Werte sind 0 bis 999999999.</li><li>ZEITZONE: **Erforderlich** Die Zeitzone für die Datum/Uhrzeit.</li></ul> | make_date_time &#x200B;(YEAR, MONTH, DAY, HOUR, MINUTE, SECOND, NANOSECOND, TIMEZONE) | make_date_time &#x200B;(2019, 10, 17, 11, 55, 12, 999, &quot;America/Los_Angeles&quot;) | `2019-10-17T11:55:12Z` |
| zone_date_to_utc | Konvertiert ein Datum in einer beliebigen Zeitzone in ein Datum in UTC. | <ul><li>DATUM: **Erforderlich** Das Datum, das Sie konvertieren möchten.</li></ul> | zone_date_to_utc &#x200B;(DATE) | `zone_date_to_utc&#x200B;(2019-10-17T11:55:&#x200B;12 PST` | `2019-10-17T19:55:12Z` |
| zone_date_to_zone | Konvertiert ein Datum aus einer Zeitzone in eine andere Zeitzone. | <ul><li>DATUM: **Erforderlich** Das Datum, das Sie konvertieren möchten.</li><li>ZONE: **Erforderlich** Die Zeitzone, in die Sie das Datum konvertieren möchten.</li></ul> | zone_date_to_zone &#x200B;(DATE, ZONE) | `zone_date_to_utc&#x200B;(now(), "Europe/Paris")` | `2021-10-26T15:43:59Z` |

{style=&quot;table-layout:auto&quot;}

### Hierarchien - Objekte {#objects}

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Funktion | Beschreibung | Parameter | Aufbau | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| is_empty | Prüft, ob ein Objekt leer ist. | <ul><li>EINGABE: **Erforderlich** Das Objekt, das Sie überprüfen möchten, ist leer.</li></ul> | is_empty(INPUT) | `is_empty([1, 2, 3])` | false |
| arrays_to_object | Erstellt eine Liste von Objekten. | <ul><li>EINGABE: **Erforderlich** Eine Gruppierung von Schlüssel- und Array-Paaren.</li></ul> | arrays_to_object(INPUT) | Bedarfsbeispiel | Bedarfsbeispiel |
| to_object | Erstellt ein Objekt basierend auf den angegebenen flachen Schlüssel/Wert-Paaren. | <ul><li>EINGABE: **Erforderlich** Eine flache Liste von Schlüssel/Wert-Paaren.</li></ul> | to_object(INPUT) | to_object &#x200B;(&quot;firstName&quot;, &quot;John&quot;, &quot;lastName&quot;, &quot;Doe&quot;) | `{"firstName": "John", "lastName": "Doe"}` |
| str_to_object | Erstellt ein Objekt aus der Eingabezeichenfolge. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, die analysiert wird, um ein Objekt zu erstellen.</li><li>VALUE_DELIMITER: *Optional* Das Trennzeichen, das ein Feld vom Wert trennt. Das Standardtrennzeichen ist `:`.</li><li>FIELD_DELIMITER: *Optional* Das Trennzeichen, das Feldwertpaare trennt. Das Standardtrennzeichen ist `,`.</li></ul> | str_to_object &#x200B;(STRING, VALUE_DELIMITER, FIELD_DELIMITER) | str_to_object(&quot;firstName=John,lastName=Doe,phone=123 456 7890&quot;, &quot;=&quot;, &quot;,&quot;) | `{"firstName": "John", "lastName": "Doe", "phone": "123 456 7890"}` |
| contains_key | Überprüft, ob das Objekt in den Quelldaten vorhanden ist. **Hinweis:** Diese Funktion ersetzt die veraltete `is_set()` -Funktion. | <ul><li>EINGABE: **Erforderlich** Der Pfad, der überprüft werden soll, wenn er in den Quelldaten vorhanden ist.</li></ul> | contains_key(INPUT) | contains_key(&quot;evars.evar.field1&quot;) | wahr |
| nullify | Legt den Wert des Attributs auf `null`. Dies sollte verwendet werden, wenn Sie das Feld nicht in das Zielschema kopieren möchten. |  | nullify() | nullify() | `null` |
| get_keys | Analysiert die Schlüssel/Wert-Paare und gibt alle Schlüssel zurück. | <ul><li>OBJEKT: **Erforderlich** Das Objekt, aus dem die Schlüssel extrahiert werden.</li></ul> | get_keys(OBJECT) | get_keys({&quot;book1&quot;: &quot;Stolz und Vorurteile&quot;, &quot;Buch2&quot;: &quot;1984&quot;}) | `["book1", "book2"]` |
| get_values | Analysiert die Schlüssel-Wert-Paare und gibt den Wert der Zeichenfolge basierend auf dem angegebenen Schlüssel zurück. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, die Sie analysieren möchten.</li><li>SCHLÜSSEL: **Erforderlich** Der Schlüssel, für den der Wert extrahiert werden muss.</li><li>VALUE_DELIMITER: **Erforderlich** Das Trennzeichen, das das Feld und den Wert trennt. Wenn eine `null` oder eine leere Zeichenfolge angegeben wird, lautet dieser Wert `:`.</li><li>FIELD_DELIMITER: *Optional* Das Trennzeichen, das Feld- und Wertpaare trennt. Wenn eine `null` oder eine leere Zeichenfolge angegeben wird, lautet dieser Wert `,`.</li></ul> | get_values(STRING, KEY, VALUE_DELIMITER, FIELD_DELIMITER) | get_values(\&quot;firstName - John , lastName - Cena , phone - 555 420 8692\&quot;, \&quot;firstName\&quot;, \&quot;-\&quot;, \&quot;,\&quot;) | John |

{style=&quot;table-layout:auto&quot;}

Informationen zur Objektkopierfunktion finden Sie im Abschnitt . [below](#object-copy).

### Hierarchien - Arrays {#arrays}

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Funktion | Beschreibung | Parameter | Aufbau | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| coalesce | Gibt das erste Objekt zurück, das nicht null ist und sich in einem angegebenen Array befindet. | <ul><li>EINGABE: **Erforderlich** Das Array, von dem Sie das erste Objekt finden möchten, dessen Wert nicht null ist.</li></ul> | coalesce(INPUT) | coalesce(null, null, null, &quot;first&quot;, null, &quot;second&quot;) | &quot;first&quot; |
| first | Ruft das erste Element des angegebenen Arrays ab. | <ul><li>EINGABE: **Erforderlich** Das Array, für das Sie das erste Element suchen möchten.</li></ul> | first(INPUT) | first(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;1&quot; |
| last | Ruft das letzte Element des angegebenen Arrays ab. | <ul><li>EINGABE: **Erforderlich** Das Array, für das Sie das letzte Element suchen möchten.</li></ul> | last(INPUT) | last(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;3&quot; |
| add_to_array | Fügt Elemente am Ende des Arrays hinzu. | <ul><li>ARRAY: **Erforderlich** Das Array, dem Sie Elemente hinzufügen.</li><li>WERTE: Die Elemente, die an das Array angehängt werden sollen.</li></ul> | add_to_array &#x200B;(ARRAY, VALUES) | add_to_array &#x200B;([&quot;a&quot;, &quot;b&quot;], &#39;c&#39;, &#39;d&#39;) | [&#39;a&#39;, &#39;b&#39;, &#39;c&#39;, &#39;d&#39;] |
| join_arrays | Kombiniert die Arrays miteinander. | <ul><li>ARRAY: **Erforderlich** Das Array, dem Sie Elemente hinzufügen.</li><li>WERTE: Die Array(e), die an das übergeordnete Array angehängt werden sollen.</li></ul> | join_arrays &#x200B;(ARRAY, VALUES) | join_arrays &#x200B;([&quot;a&quot;, &quot;b&quot;], [&#39;c&#39;], [&quot;d&quot;, &quot;e&quot;]) | [&#39;a&#39;, &#39;b&#39;, &#39;c&#39;, &#39;d&#39;, &#39;e&#39;] |
| to_array | Nimmt eine Liste von Eingaben und konvertiert sie in ein Array. | <ul><li>INCLUDE_NULLS: **Erforderlich** Ein boolean -Wert, der angibt, ob Nullen in das Antwort-Array aufgenommen werden sollen.</li><li>WERTE: **Erforderlich** Die Elemente, die in ein Array konvertiert werden sollen.</li></ul> | to_array &#x200B;(INCLUDE_NULLS, VALUES) | to_array(false, 1, null, 2, 3) | `[1, 2, 3]` |
| size_of | Gibt die Größe der Eingabe zurück. | <ul><li>EINGABE: **Erforderlich** Das Objekt, dessen Größe Sie ermitteln möchten.</li></ul> | size_of(INPUT) | `size_of([1, 2, 3, 4])` | 4 |
| upsert_array_append | Mit dieser Funktion werden alle Elemente im gesamten Eingabe-Array an das Ende des Arrays in Profil angehängt. Diese Funktion ist **only** anwendbar während Aktualisierungen. Wenn diese Funktion im Kontext von Einfügen verwendet wird, gibt sie die Eingabe unverändert zurück. | <ul><li>ARRAY: **Erforderlich** Das Array, an das das Array im Profil angehängt werden soll.</li></ul> | upsert_array_append(ARRAY) | `upsert_array_append([123, 456])` | [123, 456] |
| upsert_array_replace | Diese Funktion wird verwendet, um Elemente in einem Array zu ersetzen. Diese Funktion ist **only** anwendbar während Aktualisierungen. Wenn diese Funktion im Kontext von Einfügen verwendet wird, gibt sie die Eingabe unverändert zurück. | <ul><li>ARRAY: **Erforderlich** Das Array, das das Array im Profil ersetzen soll.</li></li> | upsert_array_replace(ARRAY) | `upsert_array_replace([123, 456], 1)` | [123, 456] |

{style=&quot;table-layout:auto&quot;}

### Logische Operatoren {#logical-operators}

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Funktion | Beschreibung | Parameter | Aufbau | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| decode | Bei einem Schlüssel und einer Liste mit Schlüsselwertpaaren, die als Array reduziert werden, gibt die Funktion den Wert zurück, wenn der Schlüssel gefunden wird, oder gibt einen Standardwert zurück, wenn er im Array vorhanden ist. | <ul><li>SCHLÜSSEL: **Erforderlich** Der Schlüssel, der abgeglichen werden soll.</li><li>OPTIONS: **Erforderlich** Ein reduziertes Array von Schlüssel/Wert-Paaren. Optional kann ein Standardwert am Ende gesetzt werden.</li></ul> | decode(KEY, OPTIONS) | decode(stateCode, &quot;ca&quot;, &quot;California&quot;, &quot;pa&quot;, &quot;Pennsylvania&quot;, &quot;N/A&quot;) | Wenn der angegebene stateCode &quot;ca&quot;ist, &quot;California&quot;.<br>Wenn der angegebene stateCode &quot;pa&quot;ist, &quot;Pennsylvania&quot;.<br>Wenn der stateCode nicht mit dem folgenden übereinstimmt, &quot;N/A&quot;. |
| iif | Wertet einen bestimmten booleschen Ausdruck aus und gibt den angegebenen Wert basierend auf dem Ergebnis zurück. | <ul><li>AUSDRUCK: **Erforderlich** Der boolesche Ausdruck, der ausgewertet wird.</li><li>TRUE_VALUE: **Erforderlich** Der Wert, der zurückgegeben wird, wenn der Ausdruck &quot;true&quot;ergibt.</li><li>FALSE_VALUE: **Erforderlich** Der Wert, der zurückgegeben wird, wenn der Ausdruck &quot;false&quot;ergibt.</li></ul> | iif(EXPRESSION, TRUE_VALUE, FALSE_VALUE) | iif(&quot;s&quot;.equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;True&quot; |

{style=&quot;table-layout:auto&quot;}

### Aggregation {#aggregation}

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Funktion | Beschreibung | Parameter | Aufbau | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| min | Gibt das Minimum der angegebenen Argumente zurück. Verwendet die natürliche Reihenfolge. | <ul><li>OPTIONS: **Erforderlich** Ein oder mehrere Objekte, die miteinander verglichen werden können.</li></ul> | min(OPTIONS) | min(3, 1, 4) | 1 |
| max | Gibt das Maximum der angegebenen Argumente zurück. Verwendet die natürliche Reihenfolge. | <ul><li>OPTIONS: **Erforderlich** Ein oder mehrere Objekte, die miteinander verglichen werden können.</li></ul> | max(OPTIONS) | max(3, 1, 4) | 4 |

{style=&quot;table-layout:auto&quot;}

### Typkonvertierungen {#type-conversions}

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Funktion | Beschreibung | Parameter | Aufbau | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| to_bigint | Konvertiert einen String in einen BigInteger-Wert. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, die in einen BigInteger konvertiert werden soll.</li></ul> | to_bigint(STRING) | to_bigint &#x200B;(&quot;100000.34&quot;) | 1000000.34 |
| to_decimal | Konvertiert einen String in einen Double-String. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, die in ein Double-Zeichen umgewandelt werden soll.</li></ul> | to_decimal(STRING) | to_decimal(&quot;20.5&quot;) | 20.5 |
| to_float | Konvertiert einen String in einen Float-Wert. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, die in eine Gleitkommazahl konvertiert werden soll.</li></ul> | to_float(STRING) | to_float(&quot;12.3456&quot;) | 12.34566 |
| to_integer | Konvertiert eine Zeichenfolge in eine Ganzzahl. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, die in eine Ganzzahl umgewandelt werden soll.</li></ul> | to_integer(STRING) | to_integer(&quot;12&quot;) | 12 |

{style=&quot;table-layout:auto&quot;}

### JSON-Funktionen {#json}

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Funktion | Beschreibung | Parameter | Aufbau | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| json_to_object | Deserialisieren Sie den JSON-Inhalt aus der angegebenen Zeichenfolge. | <ul><li>STRING: **Erforderlich** Die zu deserialisierende JSON-Zeichenfolge.</li></ul> | json_to_object &#x200B;(STRING) | json_to_object &#x200B;({&quot;info&quot;:{&quot;firstName&quot;:&quot;John&quot;,&quot;lastName&quot;: &quot;Doe&quot;}) | Ein Objekt, das die JSON darstellt. |

{style=&quot;table-layout:auto&quot;}

### Sondermaßnahmen {#special-operations}

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Funktion | Beschreibung | Parameter | Aufbau | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| uid /<br>guid | Generiert eine Pseudo-Zufallskennung. |  | uuid()<br>guid() | uuid()<br>guid() | 7c0267d2-bb74-4e1a-9275-3bf4fccda5f4<br>c7016dc7-3163-43f7-afc7-2e1c9c206333 |

{style=&quot;table-layout:auto&quot;}

### Benutzeragenten-Funktionen {#user-agent}

Jede der in der folgenden Tabelle enthaltenen Benutzeragenten-Funktionen kann einen der folgenden Werte zurückgeben:

* Telefon - Ein Mobilgerät mit kleinem Bildschirm (allgemein &lt; 7&quot;)
* Mobile : Ein Mobilgerät, das noch nicht identifiziert wurde. Bei diesem Mobilgerät kann es sich um einen eReader, ein Tablet, ein Telefon, eine Uhr usw. handeln.

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Funktion | Beschreibung | Parameter | Aufbau | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| ua_os_name | Extrahiert den Betriebssystemnamen aus der Benutzeragenten-Zeichenfolge. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragenten-Zeichenfolge.</li></ul> | ua_os_name &#x200B;(USER_AGENT) | ua_os_name &#x200B;(&quot;Mozilla/5.0 (iPhone) CPU iPhone OS 5_1_1 (wie Mac OS X) AppleWebKit/534.46 (KHTML, wie Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS |
| ua_os_version_major | Extrahiert die Hauptversion des Betriebssystems aus der Zeichenfolge des Benutzeragenten. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragenten-Zeichenfolge.</li></ul> | ua_os_version_major &#x200B;(USER_AGENT) | ua_os_version_major &#x200B; s(&quot;Mozilla/5.0 (iPhone); CPU iPhone OS 5_1_1 (wie Mac OS X) AppleWebKit/534.46 (KHTML, wie Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5 |
| ua_os_version | Extrahiert die Version des Betriebssystems aus der Zeichenfolge des Benutzeragenten. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragenten-Zeichenfolge.</li></ul> | ua_os_version &#x200B;(USER_AGENT) | ua_os_version &#x200B;(&quot;Mozilla/5.0 (iPhone) CPU iPhone OS 5_1_1 (wie Mac OS X) AppleWebKit/534.46 (KHTML, wie Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1.1 |
| ua_os_name_version | Extrahiert den Namen und die Version des Betriebssystems aus der Zeichenfolge des Benutzeragenten. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragenten-Zeichenfolge.</li></ul> | ua_os_name_version &#x200B;(USER_AGENT) | ua_os_name_version &#x200B;(&quot;Mozilla/5.0 (iPhone) CPU iPhone OS 5_1_1 (wie Mac OS X) AppleWebKit/534.46 (KHTML, wie Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5.1.1 |
| ua_agent_version | Extrahiert die Agentenversion aus der Benutzeragenten-Zeichenfolge. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragenten-Zeichenfolge.</li></ul> | ua_agent_version &#x200B;(USER_AGENT) | ua_agent_version &#x200B;(&quot;Mozilla/5.0 (iPhone) CPU iPhone OS 5_1_1 (wie Mac OS X) AppleWebKit/534.46 (KHTML, wie Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1 |
| ua_agent_version_major | Extrahiert den Namen des Agenten und die Hauptversion aus der Zeichenfolge des Benutzeragenten. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragenten-Zeichenfolge.</li></ul> | ua_agent_version_major &#x200B;(USER_AGENT) | ua_agent_version_major &#x200B;(&quot;Mozilla/5.0 (iPhone) CPU iPhone OS 5_1_1 (wie Mac OS X) AppleWebKit/534.46 (KHTML, wie Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari 5 |
| ua_agent_name | Extrahiert den Agentennamen aus der Benutzeragenten-Zeichenfolge. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragenten-Zeichenfolge.</li></ul> | ua_agent_name &#x200B;(USER_AGENT) | ua_agent_name &#x200B;(&quot;Mozilla/5.0 (iPhone) CPU iPhone OS 5_1_1 (wie Mac OS X) AppleWebKit/534.46 (KHTML, wie Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari |
| ua_device_class | Extrahiert die Geräteklasse aus der Benutzeragenten-Zeichenfolge. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragenten-Zeichenfolge.</li></ul> | ua_device_class &#x200B;(USER_AGENT) | ua_device_class &#x200B;(&quot;Mozilla/5.0 (iPhone) CPU iPhone OS 5_1_1 (wie Mac OS X) AppleWebKit/534.46 (KHTML, wie Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Telefon |

{style=&quot;table-layout:auto&quot;}

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

Im obigen Beispiel wird die Variable `city` und `state` -Attribute werden auch automatisch zur Laufzeit erfasst, da die `address` -Objekt wird zugeordnet zu `addr`. Wenn Sie eine `line2` -Attribut in der XDM-Struktur verwenden, und Ihre Eingabedaten enthalten auch eine `line2` im `address` -Objekt, wird es auch automatisch erfasst, ohne dass die Zuordnung manuell geändert werden muss.

Um sicherzustellen, dass die automatische Zuordnung funktioniert, müssen die folgenden Voraussetzungen erfüllt sein:

* Übergeordnete Objekte sollten zugeordnet werden;
* Neue Attribute müssen im XDM-Schema erstellt worden sein.
* Neue Attribute sollten über übereinstimmende Namen im Quellschema und im XDM-Schema verfügen.

Wenn eine der Voraussetzungen nicht erfüllt ist, müssen Sie das Quellschema mithilfe von data prep manuell dem XDM-Schema zuordnen.
