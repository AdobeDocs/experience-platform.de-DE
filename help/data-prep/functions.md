---
keywords: Experience Platform;home;beliebte Themen;Map-CSV;Map-CSV-Datei;CSV-Datei xdm zuordnen;CSV-Datei zu xdm zuordnen;Handbuch;Zuordnung;Mapping-Felder;Mapping-Funktionen
solution: Experience Platform
title: Funktionen für Datenvorlagenzuordnung
topic-legacy: overview
description: In diesem Dokument werden die Zuordnungsfunktionen vorgestellt, die mit Data Prep verwendet werden.
exl-id: e95d9329-9dac-4b54-b804-ab5744ea6289
source-git-commit: c4fc370929000a5d34ce2696da7efe8c75abd07c
workflow-type: tm+mt
source-wordcount: '3940'
ht-degree: 8%

---

# Zuordnungsfunktionen für Datenvorbereitung

Mit den Datenvorgabenfunktionen können Werte basierend auf dem, was in Quellfeldern eingegeben wird, berechnet und berechnet werden.

## Felder

Ein Feldname kann eine beliebige rechtliche Kennung sein - eine unbegrenzte Folge von Unicode-Buchstaben und Ziffern, beginnend mit einem Buchstaben, dem Dollarzeichen (`$`) oder der Unterstrich (`_`). Bei Variablennamen muss auch auf die Groß- und Kleinschreibung geachtet werden.

Wenn ein Feldname dieser Konvention nicht entspricht, muss der Feldname in `${}`. Wenn der Feldname z. B. &quot;Vorname&quot; oder &quot;Vorname&quot; lautet, muss der Name wie folgt umgebrochen werden: `${First Name}` oder `${First.Name}` bzw.

Wenn ein Feldname **beliebig** von den folgenden reservierten Keywords, muss es mit `${}`:

```console
new, mod, or, break, var, lt, for, false, while, eq, gt, div, not, null, continue, else, and, ne, true, le, if, ge, return
```

Auf Daten in Unterfeldern kann mithilfe der Punktschreibweise zugegriffen werden. Wenn es z. B. `name` Objekt, um auf `firstName` Feld, verwenden `name.firstName`.

## Funktionsliste

In den folgenden Tabellen werden alle unterstützten Zuordnungsfunktionen, einschließlich Beispiel-Ausdruck und deren Ausgabe, Liste.

### Zeichenfolgen-Funktionen {#string}

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Funktion | Beschreibung | Parameter | Syntax | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| concat | Verkettet die angegebenen Zeichenfolgen. | <ul><li>ZEICHNUNG: Die Strings, die verkettet werden.</li></ul> | concat(STRING_1, STRING_2) | concat(&quot;Hi, &quot;, &quot;There&quot;, &quot;!&quot;) | `"Hi, there!"` |
| explode | Teilt die Zeichenfolge basierend auf einem regex und gibt ein Array von Teilen zurück. Kann optional regex einschließen, um die Zeichenfolge zu teilen. Standardmäßig wird die Aufteilung in &quot;,&quot; aufgelöst. Die folgenden Trennzeichen **erforderlich** zu entkommen mit `\`: `+, ?, ^, |, ., [, (, {, ), *, $, \` Wenn Sie mehrere Zeichen als Trennzeichen angeben, wird das Trennzeichen als Trennzeichen mit mehreren Zeichen behandelt. | <ul><li>ZEICHNUNG: **Erforderlich** Die Zeichenfolge, die geteilt werden muss.</li><li>REGEX: *Optional* Der reguläre Ausdruck, mit dem die Zeichenfolge geteilt werden kann.</li></ul> | explode(STRING, REGEX) | explode(&quot;Hallo!&quot;, &quot;&quot;) | `["Hi,", "there"]` |
| instr | Gibt den Speicherort/Index einer Unterzeichenfolge zurück. | <ul><li>EINGABE: **Erforderlich** Die Zeichenfolge, die gesucht wird.</li><li>UNTERZEICHNUNG: **Erforderlich** Die Unterzeichenfolge, nach der innerhalb der Zeichenfolge gesucht wird.</li><li>Beginn_POSITION: *Optional* Der Speicherort des Beginns, der in der Zeichenfolge sucht.</li><li>VORKOMMEN: *Optional* Das n. Vorkommen, nach dem von der Position des Beginns gesucht werden soll. Standardmäßig ist es 1. </li></ul> | instr(INPUT, SUBSTRING, BEGINN_POSITION, OCCURRENCE) | instr(&quot;adobe.com&quot;, &quot;com&quot;) | 6 |
| Ersetzen | Ersetzt die Suchzeichenfolge, wenn sie in der ursprünglichen Zeichenfolge vorhanden ist. | <ul><li>EINGABE: **Erforderlich** Die Eingabezeichenfolge.</li><li>ZU_SUCHEN: **Erforderlich** Die Zeichenfolge, nach der in der Eingabe gesucht werden soll.</li><li>ZU_ERSETZEN: **Erforderlich** Die Zeichenfolge, die den Wert in &quot;TO_FIND&quot; ersetzt.</li></ul> | replace(INPUT, TO_FIND, TO_REPLACE) | replaced(&quot;This is a string re test&quot;, &quot;re&quot;, &quot;replace&quot;) | &quot;Dies ist ein Test zum Ersetzen einer Zeichenfolge&quot; |
| substr | Gibt eine Teilzeichenfolge einer angegebenen Länge zurück. | <ul><li>EINGABE: **Erforderlich** Die Eingabezeichenfolge.</li><li>Beginn_INDEX: **Erforderlich** Der Index der Eingabezeichenfolge, in der die Unterzeichenfolge Beginn ist.</li><li>LÄNGE: **Erforderlich** Die Länge der Unterzeichenfolge.</li></ul> | substr(INPUT, BEGINN_INDEX, LENGTH) | substr(&quot;Dies ist ein Unterzeichentest&quot;, 7, 8) | &quot; a subst&quot; |
| niedriger /<br>lcase | Konvertiert eine Zeichenfolge in Kleinbuchstaben. | <ul><li>EINGABE: **Erforderlich** Die Zeichenfolge, die in Kleinbuchstaben umgewandelt wird.</li></ul> | lower(INPUT) | lower(&quot;HeLo&quot;)<br>lcase(&quot;HeLo&quot;) | &quot;hello&quot; |
| oben /<br>ucase | Konvertiert eine Zeichenfolge in Großbuchstaben. | <ul><li>EINGABE: **Erforderlich** Die Zeichenfolge, die in Großbuchstaben umgewandelt wird.</li></ul> | Oben (INPUT) | Upper(&quot;HeLo&quot;)<br>ucase(&quot;HeLo&quot;) | &quot;HELLO&quot; |
| split | Teilt einen Eingabestring auf ein Trennzeichen. Das folgende Trennzeichen **Anforderungen** zu entkommen mit `\`: `\`. Wenn Sie mehrere Trennzeichen angeben, wird die Zeichenfolge aufgeteilt auf **beliebig** der in der Zeichenfolge vorhandenen Trennzeichen. | <ul><li>EINGABE: **Erforderlich** Die zu teilende Eingabezeichenfolge.</li><li>SEPARATOR: **Erforderlich** Die Zeichenfolge, die zur Teilung der Eingabe verwendet wird.</li></ul> | split(INPUT, SEPARATOR) | split(&quot;Hello world&quot;, &quot;&quot;) | `["Hello", "world"]` |
| beitreten | Verbindet eine Liste von Objekten mithilfe des Trennzeichens. | <ul><li>SEPARATOR: **Erforderlich** Die Zeichenfolge, die zum Verbinden der Objekte verwendet wird.</li><li>OBJEKTE: **Erforderlich** Ein Array von Zeichenfolgen, die verbunden werden.</li></ul> | `join(SEPARATOR, [OBJECTS])` | `join(" ", to_array(true, "Hello", "world"))` | &quot;Hello world&quot; |
| lpad | Fügt die linke Seite einer Zeichenfolge mit der anderen angegebenen Zeichenfolge ein. | <ul><li>EINGABE: **Erforderlich** Die Zeichenfolge, die verschoben wird. Diese Zeichenfolge kann null sein.</li><li>ZAHL: **Erforderlich** Die Größe des auszufügenden Strings.</li><li>HINZUFÜGEN: **Erforderlich** Die Zeichenfolge, mit der die Eingabe aufgezeichnet werden soll. Wenn Null oder leer, wird es als ein einzelnes Leerzeichen behandelt.</li></ul> | lpad(INPUT, COUNT, PADDING) | lpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;yzyzybat&quot; |
| rpad | Fügt die rechte Seite einer Zeichenfolge mit der anderen angegebenen Zeichenfolge ein. | <ul><li>EINGABE: **Erforderlich** Die Zeichenfolge, die verschoben wird. Diese Zeichenfolge kann null sein.</li><li>ZAHL: **Erforderlich** Die Größe des auszufügenden Strings.</li><li>HINZUFÜGEN: **Erforderlich** Die Zeichenfolge, mit der die Eingabe aufgezeichnet werden soll. Wenn Null oder leer, wird es als ein einzelnes Leerzeichen behandelt.</li></ul> | rpad(INPUT, COUNT, PADDING) | rpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;batyzyzy&quot; |
| left | Ruft die ersten &quot;n&quot; Zeichen der angegebenen Zeichenfolge ab. | <ul><li>ZEICHNUNG: **Erforderlich** Die Zeichenfolge, für die Sie die ersten &quot;n&quot;-Zeichen abrufen.</li><li>ZAHL: **Erforderlich** Die &quot;n&quot;-Zeichen, die aus der Zeichenfolge abgerufen werden sollen.</li></ul> | left(STRING, COUNT) | left(&quot;abcde&quot;, 2) | &quot;ab&quot; |
| rechts | Ruft die letzten &quot;n&quot; Zeichen der angegebenen Zeichenfolge ab. | <ul><li>ZEICHNUNG: **Erforderlich** Die Zeichenfolge, für die Sie die letzten &quot;n&quot;-Zeichen abrufen.</li><li>ZAHL: **Erforderlich** Die &quot;n&quot;-Zeichen, die aus der Zeichenfolge abgerufen werden sollen.</li></ul> | right(STRING, COUNT) | right(&quot;abcde&quot;, 2) | &quot;de&quot; |
| Ltrim | Entfernt den Leerraum vom Anfang der Zeichenfolge. | <ul><li>ZEICHNUNG: **Erforderlich** Der String, aus dem Sie das Leerzeichen entfernen möchten.</li></ul> | ltrim(STRING) | ltrim(&quot; hello&quot;) | &quot;hello&quot; |
| rtrim | Entfernt den Leerraum vom Ende der Zeichenfolge. | <ul><li>ZEICHNUNG: **Erforderlich** Der String, aus dem Sie das Leerzeichen entfernen möchten.</li></ul> | rtrim(STRING) | rtrim(&quot;hello&quot;) | &quot;hello&quot; |
| trim | Entfernt den Leerraum vom Anfang und vom Ende der Zeichenfolge. | <ul><li>ZEICHNUNG: **Erforderlich** Der String, aus dem Sie das Leerzeichen entfernen möchten.</li></ul> | trim(STRING) | trim(&quot; hello &quot;) | &quot;hello&quot; |
| gleich | Vergleicht zwei Strings, um zu bestätigen, ob sie gleich sind. Bei dieser Funktion wird zwischen Groß- und Kleinschreibung unterschieden. | <ul><li>STRING1: **Erforderlich** Die erste Zeichenfolge, die Sie vergleichen möchten.</li><li>STRING2: **Erforderlich** Die zweite Zeichenfolge, die Sie vergleichen möchten.</li></ul> | STRING1. &#x200B;gleich (&#x200B; STRING2) | &quot;string1&quot;. &#x200B;gleich &#x200B;(&quot;STRING1&quot;) | false |
| equalsIgnoreCase | Vergleicht zwei Strings, um zu bestätigen, ob sie gleich sind. Diese Funktion ist **nicht** Groß- und Kleinschreibung beachten. | <ul><li>STRING1: **Erforderlich** Die erste Zeichenfolge, die Sie vergleichen möchten.</li><li>STRING2: **Erforderlich** Die zweite Zeichenfolge, die Sie vergleichen möchten.</li></ul> | STRING1. &#x200B;equalsIgnorierenCase-&#x200B;(STRING2) | &quot;string1&quot;. &#x200B;equalsIgnoreCase &#x200B;(&quot;STRING1&quot;) | wahr |

{style=&quot;table-layout:auto&quot;}

### Funktionen mit reguläreren Ausdrücken

| Funktion | Beschreibung | Parameter | Syntax | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| extrakt_regex | Extrahiert Gruppen aus der Eingabezeichenfolge, basierend auf einem regulären Ausdruck. | <ul><li>ZEICHNUNG: **Erforderlich** Die Zeichenfolge, aus der Sie die Gruppen extrahieren.</li><li>REGEX: **Erforderlich** Der reguläre Ausdruck, mit dem die Gruppe übereinstimmen soll.</li></ul> | extract_regex(STRING, REGEX) | extract_regex &#x200B;(&quot;E259,E259B_009,1_1&quot; &#x200B;, &quot;([^,]+),[^,]*,([^,]+)&quot;) | [&quot;E259,E259B_009,1_1&quot;, &quot;E259&quot;, &quot;1_1&quot;] |
| match_regex | Überprüft, ob die Zeichenfolge mit dem eingegebenen regulären Ausdruck übereinstimmt. | <ul><li>ZEICHNUNG: **Erforderlich** Die Zeichenfolge, die Sie überprüfen, entspricht dem regulären Ausdruck.</li><li>REGEX: **Erforderlich** Der reguläre Ausdruck, mit dem Sie vergleichen.</li></ul> | match_regex(STRING, REGEX) | match_regex(&quot;E259,E259B_009,1_1&quot;, &quot;([^,]+),[^,]*,([^,]+)&quot;) | wahr |

{style=&quot;table-layout:auto&quot;}

### Hashfunktionen {#hashing}

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Funktion | Beschreibung | Parameter | Syntax | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| sha1 | Erstellt einen Hash-Wert mithilfe des Secure Hash Algorithm 1 (SHA-1). | <ul><li>EINGABE: **Erforderlich** Der unsichtbare Text, der mit Hash versehen werden soll.</li><li>DIAGRAMM: *Optional* Der Name des Zeichensatzes. Mögliche Werte sind UTF-8, UTF-16, ISO-8859-1 und US-ASCII.</li></ul> | sha1(INPUT, CHARSET) | sha1(&quot;my text&quot;, &quot;UTF-8&quot;) | c3599c11e47719df18a24 &#x200B; 48690840c5dfcce3c80 |
| sha256 | Erstellt einen Hash-Wert mithilfe des Secure Hash-Algorithmus 256 (SHA-256). | <ul><li>EINGABE: **Erforderlich** Der unsichtbare Text, der mit Hash versehen werden soll.</li><li>DIAGRAMM: *Optional* Der Name des Zeichensatzes. Mögliche Werte sind UTF-8, UTF-16, ISO-8859-1 und US-ASCII.</li></ul> | sha256(INPUT, CHARSET) | sha256(&quot;mein Text&quot;, &quot;UTF-8&quot;) | 7330d2b39ca35eaf4cb95fc846c21 &#x200B; ee6a39af698154a83a586ee270a0d372104 |
| sha512 | Erstellt einen Hash-Wert mithilfe des Secure Hash-Algorithmus 512 (SHA-512). | <ul><li>EINGABE: **Erforderlich** Der unsichtbare Text, der mit Hash versehen werden soll.</li><li>DIAGRAMM: *Optional* Der Name des Zeichensatzes. Mögliche Werte sind UTF-8, UTF-16, ISO-8859-1 und US-ASCII.</li></ul> | sha512(INPUT, CHARSET) | sha512(&quot;mein Text&quot;, &quot;UTF-8&quot;) | a3d7e45a0d9be5fd4e4b9a3b8c9c2163c21ef &#x200B; 708bf11b4232bb21d2a8704ada2cdcd7b367dd07 88a89 &#x200B; a5c908cfe377aceb1072a7b386b7d4fd2ff68a8fd24d16 |
| md5 | Erstellt mithilfe von MD5 einen Hash-Wert und eine Eingabe. | <ul><li>EINGABE: **Erforderlich** Der unsichtbare Text, der mit Hash versehen werden soll.</li><li>DIAGRAMM: *Optional* Der Name des Zeichensatzes. Mögliche Werte sind UTF-8, UTF-16, ISO-8859-1 und US-ASCII. </li></ul> | md5(INPUT, CHARSET) | md5(&quot;mein Text&quot;, &quot;UTF-8&quot;) | d3b96ce8c9fb4 &#x200B; e9bd0198d03ba6852c7 |
| crc32 | Eine Eingabe verwendet einen CRC-Algorithmus, um einen 32-Bit-Zirkelcode zu erzeugen. | <ul><li>EINGABE: **Erforderlich** Der unsichtbare Text, der mit Hash versehen werden soll.</li><li>DIAGRAMM: *Optional* Der Name des Zeichensatzes. Mögliche Werte sind UTF-8, UTF-16, ISO-8859-1 und US-ASCII.</li></ul> | crc32(INPUT, CHARSET) | crc32(&quot;my text&quot;, &quot;UTF-8&quot;) | 8df92e80 |

{style=&quot;table-layout:auto&quot;}

### URL-Funktionen {#url}

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Funktion | Beschreibung | Parameter | Syntax | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| get_url_protocol | Gibt das Protokoll von der angegebenen URL zurück. Wenn die Eingabe ungültig ist, gibt sie null zurück. | <ul><li>URL: **Erforderlich** Die URL, aus der das Protokoll extrahiert werden soll.</li></ul> | get_url_protocol &#x200B;(URL) | get_url_protocol(&quot;https://platform &#x200B; .adobe.com/home&quot;) | https |
| get_url_host | Gibt den Host der angegebenen URL zurück. Wenn die Eingabe ungültig ist, gibt sie null zurück. | <ul><li>URL: **Erforderlich** Die URL, von der der Host extrahiert werden muss.</li></ul> | get_url_host &#x200B;(URL) | get_url_host &#x200B;(&quot;https://platform &#x200B; .adobe.com/home&quot;) | platform.adobe.com |
| get_url_port | Gibt den Port der angegebenen URL zurück. Wenn die Eingabe ungültig ist, gibt sie null zurück. | <ul><li>URL: **Erforderlich** Die URL, aus der der Port extrahiert werden soll.</li></ul> | get_url_port(URL) | get_url_port &#x200B;(&quot;sftp://example.com//home/ &#x200B; joe/employee.csv&quot;) | 22 |
| get_url_path | Gibt den Pfad der angegebenen URL zurück. Standardmäßig wird der vollständige Pfad zurückgegeben. | <ul><li>URL: **Erforderlich** Die URL, aus der der Pfad extrahiert werden soll.</li><li>FULL_PATH: *Optional* Ein boolescher Wert, der bestimmt, ob der vollständige Pfad zurückgegeben wird. Bei der Einstellung false wird nur das Ende des Pfads zurückgegeben.</li></ul> | get_url_path &#x200B;(URL, FULL_PATH) | get_url_path &#x200B;(&quot;sftp://example.com// &#x200B; home/joe/employee.csv&quot;) | &quot;//home/joe/&#x200B; job.csv&quot; |
| get_url_Abfrage_str | Gibt die Abfrage-Zeichenfolge einer angegebenen URL zurück. | <ul><li>URL: **Erforderlich** Die URL, von der Sie die Abfrage-Zeichenfolge abrufen möchten.</li><li>ANKER: **Erforderlich** Bestimmt, was mit dem Anker in der Abfrage-Zeichenfolge gemacht wird. Kann einer von drei Werten sein: &quot;behalten&quot;, &quot;entfernen&quot; oder &quot;anhängen&quot;.<br><br>Wenn der Wert &quot;Beibehalten&quot; lautet, wird der Anker an den zurückgegebenen Wert angehängt.<br>Wenn der Wert &quot;entfernen&quot; lautet, wird der Anker aus dem zurückgegebenen Wert entfernt.<br>Wenn der Wert &quot;append&quot; lautet, wird der Anker als separater Wert zurückgegeben.</li></ul> | get_url_Abfrage_str &#x200B;(URL, ANCHOR) | get_url_Abfrage_str &#x200B;(&quot;foo://example.com:8042 &#x200B;/over/dorthin?name= &#x200B; ferret#nose&quot;, &quot;preserve&quot;)<br>get_url_Abfrage_str &#x200B;(&quot;foo://example.com:8042 &#x200B;/over/dorthin?name= &#x200B; ferret#nose&quot;, &quot;remove&quot;)<br>get_url_Abfrage_str &#x200B;(&quot;foo://example.com &#x200B;:8042/over/then &#x200B;?name=ferret#nose&quot;, &quot;append&quot;) | `{"name": "ferret#nose"}`<br>`{"name": "ferret"}`<br>`{"name": "ferret", "_anchor_": "nose"}` |

{style=&quot;table-layout:auto&quot;}

### Datums- und Uhrzeitfunktionen {#date-and-time}

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen. Weitere Informationen über `date` -Funktion finden Sie im Abschnitt &quot;Daten&quot; des [Handbuch zur Verarbeitung von Datenformaten](./data-handling.md#dates).

| Funktion | Beschreibung | Parameter | Syntax | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| now | Ruft die aktuelle Uhrzeit ab. |  | now() | now() | `2020-09-23T10:10:24.556-07:00[America/Los_Angeles]` |
| timestamp | Ruft die aktuelle Unix-Zeit ab. |  | timestamp() | timestamp() | 1571850624571 |
| format | Formatiert das Eingabedatum in einem angegebenen Format. | <ul><li>DATUM: **Erforderlich** Das Eingabedatum, das als ZonedDateTime-Objekt formatiert werden soll.</li><li>FORMAT: **Erforderlich** Das Format, in das das Datum geändert werden soll.</li></ul> | Format(DATUM, FORMAT) | format(2019-10-23T11):24:00+00:00, &quot;JJJJ-MM-TT HH:mm:ss&quot;) | &quot;2019-10-23 11:24:35 Zoll |
| dformat | Konvertiert einen Zeitstempel in eine Datumszeichenfolge in einem angegebenen Format. | <ul><li>ZEITPLAN: **Erforderlich** Der Zeitstempel, den Sie formatieren möchten. Das wird in Millisekunden geschrieben.</li><li>FORMAT: **Erforderlich** Das Format, in das der Zeitstempel geändert werden soll.</li></ul> | dformat &#x200B;(TIMESTAMP, FORMAT) | dformat(1571829875000, &quot;yyyy-MM-dd&#39;T&#39;HH:mm:ss.SSSX&quot;) | &quot;2019-10-23T11:24:35.000 Z&quot; |
| date | Konvertiert eine Datumszeichenfolge in ein ZonedDateTime-Objekt (ISO 8601-Format). | <ul><li>DATUM: **Erforderlich** Die Zeichenfolge, die das Datum darstellt.</li><li>FORMAT: **Erforderlich** Die Zeichenfolge, die das Format des Datums darstellt.</li><li>STANDARDDATUM: **Erforderlich** Das Standarddatum, das zurückgegeben wird, wenn das angegebene Datum null ist.</li></ul> | date(DATE, FORMAT, DEFAULT_DATE) | date(&quot;2019-10-23 11:24&quot;, &quot;yyyy-MM-dd HH:mm&quot;, now()) | &quot;2019-10-23T11:24Z&quot; |
| Datum | Konvertiert eine Datumszeichenfolge in ein ZonedDateTime-Objekt (ISO 8601-Format). | <ul><li>DATUM: **Erforderlich** Die Zeichenfolge, die das Datum darstellt.</li><li>FORMAT: **Erforderlich** Die Zeichenfolge, die das Format des Datums darstellt.</li></ul> | date(DATE, FORMAT) | date(&quot;2019-10-23 11:24&quot;, &quot;yyyy-MM-dd HH:mm&quot;) | &quot;2019-10-23T11:24Z&quot; |
| Datum | Konvertiert eine Datumszeichenfolge in ein ZonedDateTime-Objekt (ISO 8601-Format). | <ul><li>DATUM: **Erforderlich** Die Zeichenfolge, die das Datum darstellt.</li></ul> | Datum(DATUM) | date(&quot;2019-10-23 11:24&quot;) | &quot;2019-10-23T11:24Z&quot; |
| date_part | Ruft die Teile des Datums ab. Folgende Komponentenwerte werden unterstützt: <br><br>&quot;Jahr&quot;<br>&quot;jjjj&quot;<br>&quot;jj&quot;<br><br>&quot;Quartal&quot;<br>&quot;qq&quot;<br>&quot;q&quot;<br><br>&quot;Monat&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;dayofyear&quot;<br>&quot;dy&quot;<br>&quot;y&quot;<br><br>&quot;Tag&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;Woche&quot;<br>&quot;ww&quot;<br>&quot;w&quot;<br><br>&quot;Wochentag&quot;<br>&quot;dw&quot;<br>&quot;w&quot;<br><br>&quot;Stunde&quot;<br>&quot;hh&quot;<br>‚hh24‘<br>&quot;hh12&quot;<br><br>&quot;Minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;second&quot;<br>&quot;ss&quot;<br>&quot;s&quot;<br><br>&quot;Millisekunde&quot;<br>&quot;ms&quot; | <ul><li>KOMPONENTE: **Erforderlich** Eine Zeichenfolge, die den Teil des Datums darstellt. </li><li>DATUM: **Erforderlich** Das Datum in einem Standardformat.</li></ul> | date_part &#x200B;(COMPONENT, DATE) | date_part(&quot;MM&quot;, date(&quot;2019-10-17 11):55:12&quot;) | 10 |
| set_date_part | Ersetzt eine Komponente in einem bestimmten Datum. Die folgenden Komponenten werden akzeptiert: <br><br>&quot;Jahr&quot;<br>&quot;jjjj&quot;<br>&quot;jj&quot;<br><br>&quot;Monat&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;Tag&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;Stunde&quot;<br>&quot;hh&quot;<br><br>&quot;Minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;second&quot;<br>&quot;ss&quot;<br>&quot;s&quot; | <ul><li>KOMPONENTE: **Erforderlich** Eine Zeichenfolge, die den Teil des Datums darstellt. </li><li>WERT: **Erforderlich** Der Wert, der für die Komponente für ein bestimmtes Datum festgelegt wird.</li><li>DATUM: **Erforderlich** Das Datum in einem Standardformat.</li></ul> | set_date_part &#x200B;(KOMPONENTE, WERT, DATUM) | set_date_part(&quot;m&quot;, 4, date(&quot;2016-11-09T11:44:44.797&quot;) | &quot;2016-04-09T11:44:44.797&quot; |
| make_date_time | Erstellt ein Datum aus Teilen. Diese Funktion kann auch mithilfe von make_timestamp ausgelöst werden. | <ul><li>JAHR: **Erforderlich** Das Jahr, vierstellig angegeben.</li><li>MONAT: **Erforderlich** Der Monat. Die zulässigen Werte liegen zwischen 1 und 12.</li><li>TAG: **Erforderlich** Der Tag. Die zulässigen Werte liegen zwischen 1 und 31.</li><li>STUNDE: **Erforderlich** Die Stunde. Die zulässigen Werte liegen zwischen 0 und 23.</li><li>MINUTE: **Erforderlich** Die Minute. Die zulässigen Werte liegen zwischen 0 und 59.</li><li>NANOSEKUNDE: **Erforderlich** Die Nanosewerte. Die zulässigen Werte liegen zwischen 0 und 999999999.</li><li>ZEITZONE: **Erforderlich** Die Zeitzone für die Datumszeit.</li></ul> | make_date_time &#x200B;(JAHR, MONAT, TAG, STUNDE, MINUTE, ZWEITE, NANOSECOND, TIMEZONE) | make_date_time &#x200B;(2019, 10, 17, 11, 55, 12, 999, &quot;America/Los_Angeles&quot;) | `2019-10-17T11:55:12.0&#x200B;00000999-07:00[America/Los_Angeles]` |
| zone_date_to_utc | Konvertiert ein Datum in einer beliebigen Zeitzone in ein Datum in UTC. | <ul><li>DATUM: **Erforderlich** Das Datum, das konvertiert werden soll.</li></ul> | zone_date_to_utc &#x200B;(DATE) | `zone_date_to_utc&#x200B;(2019-10-17T11:55:&#x200B;12.000000999-&#x200B;07:00[America/Los_Angeles])` | `2019-10-17T18:55:12.000000999Z[UTC]` |
| zone_date_to_zone | Konvertiert ein Datum aus einer Zeitzone in eine andere Zeitzone. | <ul><li>DATUM: **Erforderlich** Das Datum, das konvertiert werden soll.</li><li>ZONE: **Erforderlich** Die Zeitzone, in die das Datum konvertiert werden soll.</li></ul> | zone_date_to_zone &#x200B;(DATE, ZONE) | `zone_date_to_utc&#x200B;(2019-10-17T11:55:12&#x200B;.000000999-07:00&#x200B;[America/Los_Angeles], "Europe/Paris")` | `2019-10-17T20:55:12.000000999+02:00[Europe/Paris]` |

{style=&quot;table-layout:auto&quot;}
&#x200B;

### Hierarchien - Objekte {#objects}

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Funktion | Beschreibung | Parameter | Syntax | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| size_of | Gibt die Größe der Eingabe zurück. | <ul><li>EINGABE: **Erforderlich** Das Objekt, dessen Größe Sie suchen.</li></ul> | size_of(INPUT) | `size_of([1, 2, 3, 4])` | 4 |
| is_empty | Prüft, ob ein Objekt leer ist. | <ul><li>EINGABE: **Erforderlich** Das Objekt, das Sie überprüfen möchten, ist leer.</li></ul> | is_empty(INPUT) | `is_empty([1, 2, 3])` | false |
| arrays_to_object | Erstellt eine Liste von Objekten. | <ul><li>EINGABE: **Erforderlich** Eine Gruppe von Schlüssel- und Array-Paaren.</li></ul> | arrays_to_object(INPUT) | Stichprobe benötigen | Stichprobe benötigen |
| to_object | Erstellt ein Objekt basierend auf den angegebenen flachen Schlüssel-/Wertpaaren. | <ul><li>EINGABE: **Erforderlich** Eine flache Liste von Schlüssel-/Wertpaaren.</li></ul> | to_object(INPUT) | to_object &#x200B;(&quot;firstName&quot;, &quot;John&quot;, &quot;lastName&quot;, &quot;Doe&quot;) | `{"firstName": "John", "lastName": "Doe"}` |
| str_to_object | Erstellt ein Objekt aus dem Eingabestring. | <ul><li>ZEICHNUNG: **Erforderlich** Die Zeichenfolge, die zum Erstellen eines Objekts analysiert wird.</li><li>VALUE_DELIMITER: *Optional* Das Trennzeichen, das ein Feld vom Wert trennt. Das Standardtrennzeichen ist `:`.</li><li>FIELD_DELIMITER: *Optional* Trennzeichen, das Feldwertpaare trennt. Das Standardtrennzeichen ist `,`.</li></ul> | str_to_object &#x200B;(STRING, VALUE_DELIMITER, FIELD_DELIMITER) | str_to_object(&quot;firstName - John | lastName - | Telefon - 123 456 7890&quot;, &quot;-&quot;, &quot; | &quot;) | `{"firstName": "John", "lastName": "Doe", "phone": "123 456 7890"}` |
| includes_key | Überprüft, ob das Objekt in den Quelldaten vorhanden ist. **Hinweis:** Diese Funktion ersetzt die veraltete `is_set()` Funktion. | <ul><li>EINGABE: **Erforderlich** Der Pfad, der überprüft werden soll, wenn er in den Quelldaten vorhanden ist.</li></ul> | enthält_key(INPUT) | enthält_key(&quot;evars.evar.field1&quot;) | wahr |
| Entschärfen | Legt den Wert des Attributs fest auf `null`. Dies sollte verwendet werden, wenn Sie das Feld nicht in das Schema Zielgruppe kopieren möchten. |  | nullify() | nullify() | `null` |
| get_keys | Parst die Schlüssel-/Wertpaare und gibt alle Schlüssel zurück. | <ul><li>OBJEKT: **Erforderlich** Das Objekt, aus dem die Schlüssel extrahiert werden.</li></ul> | get_keys(OBJECT) | get_keys({&quot;book1&quot;): &quot;Stolz und Vorurteile&quot;, &quot;Buch2&quot;: &quot;1984&quot;}) | `["book1", "book2"]` |
| get_values | Parst die Schlüssel-/Wertpaare und gibt den Wert der Zeichenfolge basierend auf dem angegebenen Schlüssel zurück. | <ul><li>ZEICHNUNG: **Erforderlich** Die Zeichenfolge, die analysiert werden soll.</li><li>SCHLÜSSEL: **Erforderlich** Der Schlüssel, für den der Wert extrahiert werden muss.</li><li>VALUE_DELIMITER: **Erforderlich** Trennzeichen, das Feld und Wert voneinander trennt. Wenn `null` oder eine leere Zeichenfolge angegeben wird, ist dieser Wert `:`.</li><li>FIELD_DELIMITER: *Optional* Trennzeichen, das Feld- und Wertpaare trennt. Wenn `null` oder eine leere Zeichenfolge angegeben wird, ist dieser Wert `,`.</li></ul> | get_values(STRING, KEY, VALUE_DELIMITER, FIELD_DELIMITER) | get_values(\&quot;firstName - John , lastName - Cena , phone - 555 420 8692\&quot;, \&quot;firstName\&quot;, \&quot;-\&quot;, \&quot;,\&quot;) | John |

{style=&quot;table-layout:auto&quot;}

### Hierarchien - Arrays {#arrays}

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Funktion | Beschreibung | Parameter | Syntax | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| coalesce | Gibt das erste Nicht-Null-Objekt in einem gegebenen Array zurück. | <ul><li>EINGABE: **Erforderlich** Das Array, von dem das erste Nicht-Null-Objekt gefunden werden soll.</li></ul> | coalesce(INPUT) | coalesce(null, null, null, &quot;first&quot;, null, &quot;second&quot;) | &quot;first&quot; |
| first | Ruft das erste Element des angegebenen Arrays ab. | <ul><li>EINGABE: **Erforderlich** Das Array, dessen erstes Element gefunden werden soll.</li></ul> | first(INPUT) | first(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;1&quot; |
| last | Ruft das letzte Element des angegebenen Arrays ab. | <ul><li>EINGABE: **Erforderlich** Das Array, dessen letztes Element gefunden werden soll.</li></ul> | last(INPUT) | last(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;3&quot; |
| add_to_array | Fügt Elemente am Ende des Arrays hinzu. | <ul><li>ARRAY: **Erforderlich** Das Array, dem Sie Elemente hinzufügen.</li><li>WERTE: Die Elemente, die an das Array angehängt werden sollen.</li></ul> | add_to_array &#x200B;(ARRAY, VALUES) | add_to_array &#x200B;([&#39;a&#39;, &#39;b&#39;], &#39;c&#39;, &#39;d&#39;) | [&#39;a&#39;, &#39;b&#39;, &#39;c&#39;, &#39;d&#39;] |
| join_arrays | Kombiniert die Arrays untereinander. | <ul><li>ARRAY: **Erforderlich** Das Array, dem Sie Elemente hinzufügen.</li><li>WERTE: Die Arrays, die an das übergeordnete Array angehängt werden sollen.</li></ul> | join_arrays &#x200B;(ARRAY, VALUES) | join_arrays &#x200B;([&#39;a&#39;, &#39;b&#39;], [&#39;c&#39;], [&#39;d&#39;, &#39;e&#39;]) | [&#39;a&#39;, &#39;b&#39;, &#39;c&#39;, &#39;d&#39;, &#39;e&#39;] |
| to_array | Nimmt eine Liste von Eingaben und konvertiert sie in ein Array. | <ul><li>INCLUDE_NULLS: **Erforderlich** Ein boolescher Wert, der angibt, ob Nullen in das Antwort-Array aufgenommen werden sollen.</li><li>WERTE: **Erforderlich** Die Elemente, die in ein Array umgewandelt werden sollen.</li></ul> | to_array &#x200B;(INCLUDE_NULLS, VALUES) | to_array(false, 1, null, 2, 3) | `[1, 2, 3]` |

{style=&quot;table-layout:auto&quot;}

### Logische Operatoren {#logical-operators}

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Funktion | Beschreibung | Parameter | Syntax | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| decode | Bei einem Schlüssel und einer Liste von Schlüsselwertpaaren, die als Array reduziert sind, gibt die Funktion den Wert zurück, wenn ein Schlüssel gefunden wird, oder gibt einen Standardwert zurück, wenn im Array vorhanden. | <ul><li>SCHLÜSSEL: **Erforderlich** Der passende Schlüssel.</li><li>OPTIONS: **Erforderlich** Ein reduziertes Array von Schlüssel-/Wertpaaren. Optional kann ein Standardwert am Ende gesetzt werden.</li></ul> | decode(KEY, OPTIONS) | decode(stateCode, &quot;ca&quot;, &quot;California&quot;, &quot;pa&quot;, &quot;Pennsylvania&quot;, &quot;N/A&quot;) | Wenn der angegebene stateCode &quot;ca&quot; ist, &quot;California&quot;.<br>Wenn der angegebene stateCode &quot;pa&quot; ist, &quot;Pennsylvania&quot;.<br>Wenn der stateCode nicht mit dem folgenden übereinstimmt, &quot;K/A&quot;. |
| iif | Wertet einen bestimmten booleschen Ausdruck aus und gibt den angegebenen Wert basierend auf dem Ergebnis zurück. | <ul><li>Ausdruck: **Erforderlich** Der boolesche Ausdruck, der evaluiert wird.</li><li>TRUE_VALUE: **Erforderlich** Der Wert, der zurückgegeben wird, wenn der Ausdruck true ergibt.</li><li>FALSE_VALUE: **Erforderlich** Der Wert, der zurückgegeben wird, wenn der Ausdruck false ergibt.</li></ul> | iif(AUSDRUCK, TRUE_VALUE, FALSE_VALUE) | iif(&quot;s&quot;.equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;True&quot; |

{style=&quot;table-layout:auto&quot;}

### Aggregation {#aggregation}

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Funktion | Beschreibung | Parameter | Syntax | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| min | Gibt das Minimum der angegebenen Argumente zurück. Verwendet natürliche Sortierung. | <ul><li>OPTIONS: **Erforderlich** Ein oder mehrere Objekte, die miteinander verglichen werden können.</li></ul> | Min(OPTIONS) | min(3, 1, 4) | 1 |
| max | Gibt das Maximum der angegebenen Argumente zurück. Verwendet natürliche Sortierung. | <ul><li>OPTIONS: **Erforderlich** Ein oder mehrere Objekte, die miteinander verglichen werden können.</li></ul> | max (OPTIONS) | max. (3, 1, 4) | 4 |

{style=&quot;table-layout:auto&quot;}

### Typumwandlungen {#type-conversions}

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Funktion | Beschreibung | Parameter | Syntax | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| to_bigint | Konvertiert einen String in einen BigInteger. | <ul><li>ZEICHNUNG: **Erforderlich** Der String, der in einen BigInteger umgewandelt werden soll.</li></ul> | to_bigint(STRING) | to_bigint &#x200B;(&quot;1000000.34&quot;) | 100000,34 |
| to_decimal | Konvertiert eine Zeichenfolge in eine Dublette. | <ul><li>ZEICHNUNG: **Erforderlich** Der String, der in eine Dublette konvertiert werden soll.</li></ul> | to_decimal(STRING) | to_decimal(&quot;20.5&quot;) | Artikel 20 Absatz 5 |
| to_float | Konvertiert einen String in einen Float. | <ul><li>ZEICHNUNG: **Erforderlich** Die Zeichenfolge, die in einen Float umgewandelt werden soll.</li></ul> | to_float(STRING) | to_float(&quot;12.3456&quot;) | 12 34 566 |
| to_integer | Konvertiert eine Zeichenfolge in eine Ganzzahl. | <ul><li>ZEICHNUNG: **Erforderlich** Der String, der in eine Ganzzahl umgewandelt werden soll.</li></ul> | to_integer(STRING) | to_integer(&quot;12&quot;) | 12 |

{style=&quot;table-layout:auto&quot;}

### JSON-Funktionen {#json}

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Funktion | Beschreibung | Parameter | Syntax | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| json_to_object | Deserialisieren Sie den JSON-Inhalt aus der angegebenen Zeichenfolge. | <ul><li>ZEICHNUNG: **Erforderlich** Die zu deserialisierende JSON-Zeichenfolge.</li></ul> | json_to_object &#x200B;(STRING) | json_to_object &#x200B;({&quot;info&quot;:{&quot;firstName&quot;:&quot;John&quot;,&quot;lastName&quot; : &quot;Doe&quot;}) | Ein Objekt, das die JSON darstellt. |

{style=&quot;table-layout:auto&quot;}

### Besondere Maßnahmen {#special-operations}

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Funktion | Beschreibung | Parameter | Syntax | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| uuid /<br>guid | Erzeugt eine pseudo-zufällige ID. |  | uuid()<br>guid() | uuid()<br>guid() | 7c0267d2-bb74-4e1a-9275-3bf4fccda5f4<br>c7016dc7-3163-43f7-afc7-2e1c9c206333 |

{style=&quot;table-layout:auto&quot;}

### Funktionen des Benutzeragenten {#user-agent}

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Funktion | Beschreibung | Parameter | Syntax | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| ua_os_name | Extrahiert den Betriebssystemnamen aus der Benutzeragentenzeichenfolge. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragentenzeichenfolge.</li></ul> | ua_os_name &#x200B;(USER_AGENT) | ua_os_name &#x200B;(&quot;Mozilla/5.0 (iPhone) CPU iPhone OS 5_1_1 wie Mac OS X) AppleWebKit/534.46 (KHTML, wie Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS |
| ua_os_version_major | Extrahiert die Hauptversion des Betriebssystems aus der Benutzeragentenzeichenfolge. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragentenzeichenfolge.</li></ul> | ua_os_version_major &#x200B;(USER_AGENT) | ua_os_version_major &#x200B; s(&quot;Mozilla/5.0 (iPhone) CPU iPhone OS 5_1_1 wie Mac OS X) AppleWebKit/534.46 (KHTML, wie Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5 |
| ua_os_version | Extrahiert die Version des Betriebssystems aus der Benutzeragentenzeichenfolge. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragentenzeichenfolge.</li></ul> | ua_os_version &#x200B;(USER_AGENT) | ua_os_version &#x200B;(&quot;Mozilla/5.0 (iPhone) CPU iPhone OS 5_1_1 wie Mac OS X) AppleWebKit/534.46 (KHTML, wie Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1.1 |
| ua_os_name_version | Extrahiert den Namen und die Version des Betriebssystems aus der Benutzeragentenzeichenfolge. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragentenzeichenfolge.</li></ul> | ua_os_name_version &#x200B;(USER_AGENT) | ua_os_name_version &#x200B;(&quot;Mozilla/5.0 (iPhone) CPU iPhone OS 5_1_1 wie Mac OS X) AppleWebKit/534.46 (KHTML, wie Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5.1.1 |
| ua_agent_version | Extrahiert die Agentenversion aus der Benutzeragentenzeichenfolge. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragentenzeichenfolge.</li></ul> | ua_agent_version &#x200B;(USER_AGENT) | ua_agent_version &#x200B;(&quot;Mozilla/5.0 (iPhone) CPU iPhone OS 5_1_1 wie Mac OS X) AppleWebKit/534.46 (KHTML, wie Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5,1 |
| ua_agent_version_major | Extrahiert den Agentennamen und die Hauptversion aus der Benutzeragentenzeichenfolge. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragentenzeichenfolge.</li></ul> | ua_agent_version_major &#x200B;(USER_AGENT) | ua_agent_version_major &#x200B;(&quot;Mozilla/5.0 (iPhone) CPU iPhone OS 5_1_1 wie Mac OS X) AppleWebKit/534.46 (KHTML, wie Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari 5 |
| ua_agent_name | Extrahiert den Agentennamen aus der Benutzeragentenzeichenfolge. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragentenzeichenfolge.</li></ul> | ua_agent_name &#x200B;(USER_AGENT) | ua_agent_name &#x200B;(&quot;Mozilla/5.0 (iPhone); CPU iPhone OS 5_1_1 wie Mac OS X) AppleWebKit/534.46 (KHTML, wie Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari |
| ua_device_class | Extrahiert die Geräteklasse aus der Benutzeragentenzeichenfolge. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragentenzeichenfolge.</li></ul> | ua_device_class &#x200B;(USER_AGENT) | ua_device_class &#x200B;(&quot;Mozilla/5.0 (iPhone) CPU iPhone OS 5_1_1 wie Mac OS X) AppleWebKit/534.46 (KHTML, wie Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Telefon |

{style=&quot;table-layout:auto&quot;}
