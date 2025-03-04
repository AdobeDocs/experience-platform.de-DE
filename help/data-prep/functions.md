---
keywords: Experience Platform;Startseite;beliebte Themen;CSV zuordnen;CSV-Datei zuordnen;CSV-Datei XDM zuordnen;CSV XDM zuordnen;UI-Handbuch;Mapper;Zuordnung;Zuordnungsfelder;Zuordnungsfunktionen;
solution: Experience Platform
title: Funktionen zur Datenvorbereitung
description: In diesem Dokument werden die mit der Datenvorbereitung verwendeten Zuordnungsfunktionen vorgestellt.
exl-id: e95d9329-9dac-4b54-b804-ab5744ea6289
source-git-commit: 2d640b282feb783694276c69366b1fccadddfd78
workflow-type: tm+mt
source-wordcount: '6028'
ht-degree: 3%

---

# Funktionen zur Datenvorbereitung

Funktionen zur Datenvorbereitung können verwendet werden, um Werte basierend auf dem, was in die Quellfelder eingegeben wird, zu berechnen und zu berechnen.

## Felder

Ein Feldname kann eine beliebige rechtliche Kennung sein - eine unbegrenzte Sequenz von Unicode-Buchstaben und -Ziffern, beginnend mit einem Buchstaben, dem Dollarzeichen (`$`) oder dem Unterstrich (`_`). Bei Variablennamen wird ebenfalls zwischen Groß- und Kleinschreibung unterschieden.

Wenn ein Feldname nicht dieser Konvention entspricht, muss der Feldname mit `${}` umschlossen werden. Wenn der Feldname beispielsweise „Vorname“ oder „Vorname“ ist, muss der Name wie `${First Name}` bzw. `${First\.Name}` umschlossen werden.

>[!TIP]
>
>Wenn Sie mit Hierarchien arbeiten und ein untergeordnetes Attribut einen Punkt (`.`) enthält, müssen Sie einen Backslash (`\`) verwenden, um Sonderzeichen zu umgehen. Weitere Informationen finden Sie im Handbuch unter ([ von Sonderzeichen](home.md#escape-special-characters).

Wenn ein Feldname **eines** der folgenden reservierten Schlüsselwörter lautet, muss er mit `${}{}` umschlossen werden:

```console
new, mod, or, break, var, lt, for, false, while, eq, gt, div, not, null, continue, else, and, ne, true, le, if, ge, return, _errors, do, function, empty, size
```

Darüber hinaus enthalten reservierte Keywords auch alle auf dieser Seite aufgelisteten Mapper-Funktionen.

Auf Daten innerhalb von Unterfeldern kann mit der Punktnotation zugegriffen werden. Wenn beispielsweise ein `name` vorhanden ist, verwenden Sie `name.firstName`, um auf das `firstName`-Feld zuzugreifen.

## Funktionsliste

In den folgenden Tabellen sind alle unterstützten Zuordnungsfunktionen aufgelistet, einschließlich Beispielausdrücke und der resultierenden Ausgaben.

### Zeichenfolgen-Funktionen {#string}

>[!NOTE]
>
>Bitte nach links/rechts scrollen, um den vollständigen Inhalt der Tabelle anzuzeigen.

| Funktion | Beschreibung | Parameter | Aufbau | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| concat | Verkettet die angegebenen Zeichenfolgen. | <ul><li>STRING: Die Zeichenfolgen, die verkettet werden.</li></ul> | concat(STRING_1, STRING_2) | concat(„Hallo, &quot;, „dort“, &quot;!„) | `"Hi, there!"` |
| explode | Teilt die Zeichenfolge auf der Basis eines Regex und gibt ein Array von Teilen zurück. Kann optional einen Regex enthalten, um die Zeichenfolge zu teilen. Standardmäßig wird die Aufspaltung zu &quot;,“ aufgelöst. Die folgenden Trennzeichen **müssen** mit `\` maskiert werden: `+, ?, ^, \|, ., [, (, {, ), *, $, \` Wenn Sie mehrere Zeichen als Trennzeichen verwenden, wird das Trennzeichen als Trennzeichen mit mehreren Zeichen behandelt. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, die aufgeteilt werden muss.</li><li>REGEX: *Optional* Der reguläre Ausdruck, der zum Aufteilen der Zeichenfolge verwendet werden kann.</li></ul> | explode(STRING, REGEX) | explode(„Hallo, da!“, &quot; „) | `["Hi,", "there"]` |
| instr | Gibt den Speicherort/Index einer Teilzeichenfolge zurück. | <ul><li>INPUT: **Erforderlich** Die Zeichenfolge, nach der gesucht wird.</li><li>SUBSTRING: **Erforderlich** Die Teilzeichenfolge, nach der in der Zeichenfolge gesucht wird.</li><li>START_POSITION: *Optional* Die Stelle, an der mit der Suche in der Zeichenfolge begonnen werden soll.</li><li>VORKOMMEN: *Optional* Das n-te Vorkommen, nach dem von der Startposition aus gesucht werden soll. Standardmäßig ist es 1. </li></ul> | INSTR(EINGABE, TEILZEICHENFOLGE, START_POSITION, VORKOMMEN) | instr(„adobe.com“, „com„) | 6 |
| Ersatzstoff | Ersetzt die Suchzeichenfolge, falls in der ursprünglichen Zeichenfolge vorhanden. | <ul><li>INPUT: **Erforderlich** Die Eingabezeichenfolge.</li><li>TO_FIND: **Erforderlich** Die Zeichenfolge, die in der Eingabe nachgeschlagen werden soll.</li><li>TO_REPLACE: **Erforderlich** Die Zeichenfolge, die den Wert in „TO_FIND“ ersetzt.</li></ul> | replaceStr(INPUT, TO_FIND, TO_REPLACE) | replaceStr(„This is a string re test“, „re“, „replace„) | „Dies ist ein String-Ersetzungstest“ |
| substr | Gibt eine Teilzeichenfolge einer bestimmten Länge zurück. | <ul><li>INPUT: **Erforderlich** Die Eingabezeichenfolge.</li><li>START_INDEX: **Erforderlich** Der Index der Eingabezeichenfolge, in der die Unterzeichenfolge beginnt.</li><li>LENGTH: **Erforderlich** Die Länge der Teilzeichenfolge.</li></ul> | substr(EINGABE, START_INDEX, LÄNGE) | substr(„This is a substring test“, 7, 8) | „Eine Teilmenge“ |
| lower/<br>lcase | Konvertiert eine Zeichenfolge in Kleinbuchstaben. | <ul><li>INPUT: **Erforderlich** Die Zeichenfolge, die in Kleinbuchstaben konvertiert wird.</li></ul> | lower(INPUT) | lower(„HeLo„)<br>lcase(„HeLo„) | „Hallo“ |
| upper/<br> | Konvertiert eine Zeichenfolge in Großbuchstaben. | <ul><li>INPUT: **Erforderlich** Die Zeichenfolge, die in Großbuchstaben konvertiert wird.</li></ul> | upper(INPUT) | upper(„HeLo„)<br>ucase(„HeLo„) | „HALLO“ |
| split | Teilt eine Eingabezeichenfolge auf einem Trennzeichen. Das folgende Trennzeichen **muss** mit `\` versehen werden: `\`. Wenn Sie mehrere Trennzeichen einbeziehen, wird die Zeichenfolge auf (**)** in der Zeichenfolge vorhandenen Trennzeichen aufgeteilt. **Hinweis:** Diese Funktion gibt nur Indizes zurück, die nicht gleich null sind, unabhängig vom Vorhandensein des Trennzeichens. Wenn alle Indizes, einschließlich NULL, im resultierenden Array erforderlich sind, verwenden Sie stattdessen die Funktion „Explodieren“. | <ul><li>INPUT: **Erforderlich** Die Eingabezeichenfolge, die aufgeteilt werden soll.</li><li>SEPARATOR: **Required** Die Zeichenfolge, die zur Aufspaltung der Eingabe verwendet wird.</li></ul> | split(EINGABE, TRENNZEICHEN) | split(„Hello world“, &quot;„) | `["Hello", "world"]` |
| beitreten | Verbindet eine Liste von Objekten mithilfe des Trennzeichens. | <ul><li>SEPARATOR: **Erforderlich** Die Zeichenfolge, die zum Verbinden der Objekte verwendet wird.</li><li>OBJEKTE: **Erforderlich** Ein Array von Zeichenfolgen, die verbunden werden.</li></ul> | `join(SEPARATOR, [OBJECTS])` | `join(" ", to_array(true, "Hello", "world"))` | „Hallo Welt“ |
| lpad | Füllt die linke Seite einer Zeichenfolge mit der anderen angegebenen Zeichenfolge auf. | <ul><li>INPUT: **Erforderlich** Die Zeichenfolge, die aufgefüllt werden soll. Diese Zeichenfolge kann null sein.</li><li>COUNT: **Erforderlich** Die Größe der Zeichenfolge, die aufgefüllt werden soll.</li><li>PADDING: **Erforderlich** Die Zeichenfolge, mit der die Eingabe aufgefüllt wird. Wenn null oder leer, wird dies als ein einziges Leerzeichen behandelt.</li></ul> | load(INPUT, COUNT, PADDING) | LPAD(„bat“, 8, „yz„) | „Yzybat“ |
| rpad | Füllt die rechte Seite einer Zeichenfolge mit der anderen angegebenen Zeichenfolge auf. | <ul><li>INPUT: **Erforderlich** Die Zeichenfolge, die aufgefüllt werden soll. Diese Zeichenfolge kann null sein.</li><li>COUNT: **Erforderlich** Die Größe der Zeichenfolge, die aufgefüllt werden soll.</li><li>PADDING: **Erforderlich** Die Zeichenfolge, mit der die Eingabe aufgefüllt wird. Wenn null oder leer, wird dies als ein einziges Leerzeichen behandelt.</li></ul> | rpad(INPUT, COUNT, PADDING) | RPAD(„BAT“, 8, „YZ„) | „batyzyzy“ |
| left | Ruft die ersten n Zeichen der angegebenen Zeichenfolge ab. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, für die Sie die ersten „n“ Zeichen erhalten.</li><li>COUNT: **Required** Die „n“ Zeichen, die Sie aus der Zeichenfolge erhalten möchten.</li></ul> | LEFT(ZEICHENFOLGE, ANZAHL) | LEFT(„abcde“, 2) | „ab“ |
| rechts | Ruft die letzten n Zeichen der angegebenen Zeichenfolge ab. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, für die Sie die letzten „n“ Zeichen erhalten.</li><li>COUNT: **Required** Die „n“ Zeichen, die Sie aus der Zeichenfolge erhalten möchten.</li></ul> | right(STRING, COUNT) | RIGHT(„abcde“, 2) | „de“ |
| Kürzung | Entfernt das Leerzeichen vom Anfang der Zeichenfolge. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, aus der Sie das Leerzeichen entfernen möchten.</li></ul> | ltrim(ZEICHENFOLGE) | ltrim(„Hallo„) | „Hallo“ |
| rtrim | Entfernt das Leerzeichen vom Ende der Zeichenfolge. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, aus der Sie das Leerzeichen entfernen möchten.</li></ul> | trim(STRING) | rtrim(„Hallo „) | „Hallo“ |
| trim | Entfernt das Leerzeichen vom Anfang und Ende der Zeichenfolge. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, aus der Sie das Leerzeichen entfernen möchten.</li></ul> | trim(STRING) | TRIM(„Hallo „) | „Hallo“ |
| ist gleich | Vergleicht zwei Zeichenfolgen, um zu bestätigen, ob sie gleich sind. Bei dieser Funktion wird zwischen Groß- und Kleinschreibung unterschieden. | <ul><li>STRING1: **Erforderlich** Die erste Zeichenfolge, die Sie vergleichen möchten.</li><li>STRING2: **Erforderlich** Die zweite Zeichenfolge, die Sie vergleichen möchten.</li></ul> | STRING1..&#x200B;Equals(&#x200B;STRING2) | „string1“..&#x200B;Equals&#x200B;(„STRING1„) | false |
| equalsIgnoreCase | Vergleicht zwei Zeichenfolgen, um zu bestätigen, ob sie gleich sind. Bei dieser Funktion wird **Groß-** Kleinschreibung beachtet. | <ul><li>STRING1: **Erforderlich** Die erste Zeichenfolge, die Sie vergleichen möchten.</li><li>STRING2: **Erforderlich** Die zweite Zeichenfolge, die Sie vergleichen möchten.</li></ul> | STRING1..&#x200B;equalsIgnoreCase&#x200B;(STRING2) | „string1“..&#x200B;equalsIgnoreCase&#x200B;(„STRING1) | wahr |

{style="table-layout:auto"}

### Funktionen mit reguläreren Ausdrücken

| Funktion | Beschreibung | Parameter | Aufbau | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| extract_regex | Extrahiert Gruppen aus der Eingabezeichenfolge basierend auf einem regulären Ausdruck. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, aus der Sie die Gruppen extrahieren.</li><li>REGEX: **Erforderlich** Der reguläre Ausdruck, dem die Gruppe entsprechen soll.</li></ul> | extract_regex(STRING, REGEX) | extract_regex&#x200B;(„E259,E259B_009,1_1“&#x200B;, „([^,]+),[^,]*,([^,]+)„) | [„E259,E259B_009,1_1“, „E259“, „1_1“] |
| matches_regex | Prüft, ob die Zeichenfolge mit dem eingegebenen regulären Ausdruck übereinstimmt. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, die Sie überprüfen, entspricht dem regulären Ausdruck.</li><li>REGEX: **Erforderlich** Der reguläre Ausdruck, mit dem Sie vergleichen.</li></ul> | matches_regex(STRING, REGEX) | matches_regex(„E259,E259B_009,1_1“, „([^,]+),[^,]*,([^,]+)„) | wahr |

{style="table-layout:auto"}

### Hash-Funktionen {#hashing}

>[!NOTE]
>
>Bitte nach links/rechts scrollen, um den vollständigen Inhalt der Tabelle anzuzeigen.

| Funktion | Beschreibung | Parameter | Aufbau | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| sha1 | Verwendet eine Eingabe und erzeugt einen Hash-Wert mit dem sicheren Hash-Algorithmus 1 (SHA-1). | <ul><li>INPUT: **Erforderlich** Der Text, der gehasht werden soll.</li><li>CHARSET: *Optional* Der Name des Zeichensatzes. Mögliche Werte sind UTF-8, UTF-16, ISO-8859-1 und US-ASCII.</li></ul> | sha1(EINGANG, ZEICHEN) | sha1(„Mein Text“, „UTF-8„) | C3599C11E47719DF18A24&#x200B;48690840C5DFCCE3C80 |
| SHA256 | Verwendet eine Eingabe und erzeugt einen Hash-Wert mit dem sicheren Hash-Algorithmus 256 (SHA-256). | <ul><li>INPUT: **Erforderlich** Der Text, der gehasht werden soll.</li><li>CHARSET: *Optional* Der Name des Zeichensatzes. Mögliche Werte sind UTF-8, UTF-16, ISO-8859-1 und US-ASCII.</li></ul> | sha256(EINGANG, ZEICHEN) | sha256(„Mein Text“, „UTF-8„) | 7330d2b39ca35eaf4cb95fc846c21&#x200B;ee6a39af698154a83a586ee270a0d372104 |
| SHA512 | Verwendet eine Eingabe und erzeugt einen Hash-Wert mit dem sicheren Hash-Algorithmus 512 (SHA-512). | <ul><li>INPUT: **Erforderlich** Der Text, der gehasht werden soll.</li><li>CHARSET: *Optional* Der Name des Zeichensatzes. Mögliche Werte sind UTF-8, UTF-16, ISO-8859-1 und US-ASCII.</li></ul> | sha512(EINGANG, ZEICHEN) | sha512(„Mein Text“, „UTF-8„) | a3d7e45a0d9be5fd4e4b9a3b8c9c2163c21ef&#x200B;708bf11b4232bb21d2a8704ada2cdcd7b367dd0788a89&#x200B;a5c908cfe377aceb1072a7b38 b7d4fd2ff68a8fd24d16 |
| md5 | Nimmt eine Eingabe und erzeugt einen Hash-Wert mit MD5. | <ul><li>INPUT: **Erforderlich** Der Text, der gehasht werden soll.</li><li>CHARSET: *Optional* Der Name des Zeichensatzes. Mögliche Werte sind UTF-8, UTF-16, ISO-8859-1 und US-ASCII. </li></ul> | md5(EINGANG, ZEICHEN) | md5(„Mein Text“, „UTF-8„) | D3b96ce8c9fb4&#x200B;e9bd0198d03ba6852c7 |
| crc32 | Verwendet einen Input, der einen zyklischen Redundanzprüfungs-Algorithmus (CRC) verwendet, um einen 32-Bit-zyklischen Code zu erzeugen. | <ul><li>INPUT: **Erforderlich** Der Text, der gehasht werden soll.</li><li>CHARSET: *Optional* Der Name des Zeichensatzes. Mögliche Werte sind UTF-8, UTF-16, ISO-8859-1 und US-ASCII.</li></ul> | crc32(EINGANG, ZEICHEN) | crc32(„mein Text“, „UTF-8„) | 8DF92E80 |

{style="table-layout:auto"}

### URL-Funktionen {#url}

>[!NOTE]
>
>Bitte nach links/rechts scrollen, um den vollständigen Inhalt der Tabelle anzuzeigen.

| Funktion | Beschreibung | Parameter | Aufbau | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| get_url_protocol | Gibt das Protokoll der angegebenen URL aus. Wenn die Eingabe ungültig ist, wird null zurückgegeben. | <ul><li>URL: **Erforderlich** Die URL, aus der das Protokoll extrahiert werden muss.</li></ul> | get_url_protocol&#x200B;(URL) | get_url_protocol(“https://platform&#x200B;.adobe.com/home„) | https |
| get_url_host | Gibt den Host der angegebenen URL zurück. Wenn die Eingabe ungültig ist, wird null zurückgegeben. | <ul><li>URL: **Erforderlich** Die URL, aus der der Host extrahiert werden muss.</li></ul> | get_url_host&#x200B;(URL) | get_url_host&#x200B;(“https://platform&#x200B;.adobe.com/home„) | platform.adobe.com |
| get_url_port | Gibt den Port der angegebenen URL zurück. Wenn die Eingabe ungültig ist, wird null zurückgegeben. | <ul><li>URL: **Erforderlich** Die URL, aus der der Port extrahiert werden muss.</li></ul> | get_url_port(URL) | get_url_port&#x200B;(“sftp://example.com//home/&#x200B;joe/employee.csv„) | 22 |
| get_url_path | Gibt den Pfad der angegebenen URL zurück. Standardmäßig wird der vollständige Pfad zurückgegeben. | <ul><li>URL: **Erforderlich** Die URL, aus der der Pfad extrahiert werden muss.</li><li>FULL_PATH: *Optional* Ein boolescher Wert, der bestimmt, ob der vollständige Pfad zurückgegeben wird. Wenn auf „false“ gesetzt, wird nur das Ende des Pfads zurückgegeben.</li></ul> | get_url_path&#x200B;(URL, FULL_PATH) | get_url_path&#x200B;(“sftp://example.com//&#x200B;home/joe/employee.csv„) | &quot;//home/joe/&#x200B;employee.csv“ |
| get_url_query_str | Gibt die Abfragezeichenfolge einer angegebenen URL als Zuordnung des Namens der Abfragezeichenfolge und des Werts der Abfragezeichenfolge zurück. | <ul><li>URL: **Erforderlich** Die URL, von der Sie die Abfragezeichenfolge abrufen möchten.</li><li>ANKER: **Erforderlich** Legt fest, was mit dem Anker in der Abfragezeichenfolge geschehen soll. Kann einer von drei Werten sein: „retain“, „remove“ oder „append“.<br><br>Wenn der Wert „retain“ lautet, wird der Anker an den zurückgegebenen Wert angehängt.<br>Wenn der Wert „remove“ ist, wird der Anker aus dem zurückgegebenen Wert entfernt.<br>Wenn der Wert „append“ ist, wird der Anker als separater Wert zurückgegeben.</li></ul> | get_url_query_str&#x200B;(URL, ANCHOR) | GET_URL_QUERY_STR&#x200B;(“foo://example.com:8042&#x200B;/over/there?name=&#x200B;ferret#nose“, „retain„)<br>GET_URL_QUERY_STR&#x200B;(“foo://example.com:8042&#x200B;/over/there?name=&#x200B;ferret#nose“, „remove„)<br>GET_URL_QUERY_STR&#x200B; &#x200B; &#x200B;(“foo://example.com:8042/over/thereName?name=ferret#nose“, „append„) | `{"name": "ferret#nose"}`<br>`{"name": "ferret"}`<br>`{"name": "ferret", "_anchor_": "nose"}` |
| get_url_coded | Diese Funktion verwendet eine URL als Eingabe und ersetzt oder codiert die Sonderzeichen durch ASCII-Zeichen. Weitere Informationen zu Sonderzeichen finden Sie in der [Liste von Sonderzeichen](#special-characters) im Anhang dieses Dokuments. | <ul><li>URL: **Erforderlich** Die Eingabe-URL mit Sonderzeichen, die Sie ersetzen oder mit ASCII-Zeichen kodieren möchten.</li></ul> | get_url_coded(URL) | get_url_coded(„https</span>://example.com/partneralliance_Asia-Pacific_2022„) | https%3A%2F%2Fexample.com%2Fpartneralliance_Asia-Pacific_2022 |
| get_url_decoded | Diese Funktion nimmt eine URL als Eingabe und decodiert die ASCII-Zeichen in Sonderzeichen.  Weitere Informationen zu Sonderzeichen finden Sie in der [Liste von Sonderzeichen](#special-characters) im Anhang dieses Dokuments. | <ul><li>URL: **Erforderlich** Die Eingabe-URL mit ASCII-Zeichen, die Sie in Sonderzeichen decodieren möchten.</li></ul> | get_url_decoded(URL) | get_url_decoded(„https%3A%2F%2Fexample.com%2Fpartneralliance_Asia-Pacific_2022„) | https</span>://example.com/partneralliance_asia-Pacific_2022 |

{style="table-layout:auto"}

### Datums- und Uhrzeitfunktionen {#date-and-time}

>[!NOTE]
>
>Bitte nach links/rechts scrollen, um den vollständigen Inhalt der Tabelle anzuzeigen. Weitere Informationen zur `date` finden Sie im Abschnitt „Datumsangaben“ [ Handbuchs zur Handhabung von Datenformaten](./data-handling.md#dates).

| Funktion | Beschreibung | Parameter | Aufbau | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| now | Ruft die aktuelle Zeit ab. | | now() | now() | `2021-10-26T10:10:24Z` |
| Zeitstempel | Ruft die aktuelle Unix-Zeit ab. | | timestamp() | timestamp() | 1571850624571 |
| Format | Formatiert das Eingabedatum entsprechend einem angegebenen Format. | <ul><li>DATE: **required** Das Eingabedatum, das Sie als ZonedDateTime-Objekt formatieren möchten.</li><li>FORMAT: **Erforderlich** Das Format, in das das Datum geändert werden soll.</li></ul> | format(DATE, FORMAT) | format(2019-10-23T11:24:00+00:00, &quot;`yyyy-MM-dd HH:mm:ss`„) | `2019-10-23 11:24:35` |
| formatieren | Konvertiert einen Zeitstempel in eine Datumszeichenfolge gemäß einem angegebenen Format. | <ul><li>ZEITSTEMPEL: **Erforderlich** Der Zeitstempel, den Sie formatieren möchten. Dies wird in Millisekunden geschrieben.</li><li>FORMAT: **Erforderlich** Das Format, das der Zeitstempel werden soll.</li></ul> | dformat(TIMESTAMP, FORMAT) | DFORMAT(1571829875000, &quot;`yyyy-MM-dd'T'HH:mm:ss.SSSX`„) | `2019-10-23T11:24:35.000Z` |
| date | Konvertiert eine Datumszeichenfolge in ein ZonedDateTime-Objekt (ISO 8601-Format). | <ul><li>DATE: **Required** Die Zeichenfolge, die das Datum darstellt.</li><li>FORMAT: **Erforderlich** Die Zeichenfolge, die das Format des Quelldatums darstellt.**Hinweis:** Dies **nicht** das Format dar, in das Sie die Datums-Zeichenfolge konvertieren möchten. </li><li>DEFAULT_DATE: **Erforderlich** Das Standarddatum wird zurückgegeben, wenn das angegebene Datum null ist.</li></ul> | date(DATE, FORMAT, DEFAULT_DATE) | Datum(„2019-10-23 11:24“, „JJJJ-MM-TT HH:mm“, jetzt()) | `2019-10-23T11:24:00Z` |
| date | Konvertiert eine Datumszeichenfolge in ein ZonedDateTime-Objekt (ISO 8601-Format). | <ul><li>DATE: **Required** Die Zeichenfolge, die das Datum darstellt.</li><li>FORMAT: **Erforderlich** Die Zeichenfolge, die das Format des Quelldatums darstellt.**Hinweis:** Dies **nicht** das Format dar, in das Sie die Datums-Zeichenfolge konvertieren möchten. </li></ul> | date(DATE, FORMAT) | Datum(„2019-10-23 11:24“, „JJJJ-MM-TT HH:mm„) | `2019-10-23T11:24:00Z` |
| date | Konvertiert eine Datumszeichenfolge in ein ZonedDateTime-Objekt (ISO 8601-Format). | <ul><li>DATE: **Required** Die Zeichenfolge, die das Datum darstellt.</li></ul> | date(DATE) | Datum(„2019-10-23 11:24„) | „2019-10-23T11:24:00Z“ |
| date_part | Ruft die Teile des Datums ab. Die folgenden Komponentenwerte werden unterstützt: <br><br>„Jahr“<br>„JJJJ“<br>&quot;<br><br>„Quartal“<br>„qq“<br>„q“<br><br>&quot;<br>„mm“<br>„m“<br><br>„dayofyear“<br>„dy“<br>„Tag„dd„TT“<br>„TT„Woche“<br><br>„WW“<br>„w„w„w„w“<br><br> <br> <br> <br><br> <br> <br> <br> <br><br> <br> <br> <br><br> <br> <br> <br><br> <br>„TT„w„TT„w“<br>&quot;<br><br>„h„254“<br> | <ul><li>COMPONENT: **Erforderlich** Eine Zeichenfolge, die den Teil des Datums darstellt. </li><li>DATE: **Erforderlich** Das Datum im Standardformat.</li></ul> | date_part&#x200B;(COMPONENT, DATE) | date_part(„MM“, date(„2019-10-17 11:55:12„)) | 10 |
| set_date_part | Ersetzt eine Komponente in einem bestimmten Datum. Folgende Komponenten werden akzeptiert: <br><br>„year“<br>„yyyy“<br>„yy“<br><br>„month“<br>„mm“<br>„m“<br><br>„day“<br>„dd“<br>„d“<br><br>„hour“<br>„hh“<br><br>„minute“<br>„mi“<br>&quot;„n“<br><br>„second“<br>„ss“<br>„s“ | <ul><li>COMPONENT: **Erforderlich** Eine Zeichenfolge, die den Teil des Datums darstellt. </li><li>WERT: **Erforderlich** Der Wert, der für die Komponente für ein bestimmtes Datum festgelegt werden soll.</li><li>DATE: **Erforderlich** Das Datum im Standardformat.</li></ul> | set_date_part&#x200B;(COMPONENT, VALUE, DATE) | set_date_part(„m“, 4, date(„2016-11-09T11:44:44.797„) | „2016-04-09T11:44:44Z“ |
| make_date_time | Erstellt ein Datum aus Teilen. Diese Funktion kann auch mit make_timestamp eingeleitet werden. | <ul><li>JAHR: **Erforderlich** Das Jahr, mit vier Ziffern geschrieben.</li><li>MONTH: **Erforderlich** Der Monat. Zulässige Werte sind 1 bis 12.</li><li>TAG: **Erforderlich** Der Tag. Zulässige Werte sind 1 bis 31.</li><li>STUNDE: **Erforderlich** Die Stunde. Die zulässigen Werte sind 0 bis 23.</li><li>MINUTE: **Erforderlich** Die Minute. Die zulässigen Werte sind 0 bis 59.</li><li>NANOSECOND: **Erforderlich** Die Nanosekundenwerte. Die zulässigen Werte sind 0 bis 999999999.</li><li>ZEITZONE: **Erforderlich** Die Zeitzone für das Datum/die Uhrzeit.</li></ul> | make_date_time&#x200B;(JAHR, MONAT, TAG, STUNDE, MINUTE, SEKUNDE, NANOSEKUNDE, ZEITZONE) | make_date_time&#x200B;(2019, 10, 17, 11, 55, 12, 999, „America/Los_Angeles„) | `2019-10-17T11:55:12Z` |
| zone_date_to_utc | Konvertiert ein Datum in einer beliebigen Zeitzone in ein Datum in UTC. | <ul><li>DATE: **Required** Das Datum, das Sie konvertieren möchten.</li></ul> | zone_date_to_utc&#x200B;(DATE) | `zone_date_to_utc&#x200B;(2019-10-17T11:55:&#x200B;12 PST` | `2019-10-17T19:55:12Z` |
| zone_date_to_zone | Konvertiert ein Datum aus einer Zeitzone in eine andere Zeitzone. | <ul><li>DATE: **Required** Das Datum, das Sie konvertieren möchten.</li><li>ZONE: **Erforderlich** Die Zeitzone, in die Sie das Datum konvertieren möchten.</li></ul> | zone_date_to_zone&#x200B;(DATE, ZONE) | `zone_date_to_zone(now(), "Europe/Paris")` | `2021-10-26T15:43:59Z` |

{style="table-layout:auto"}

### Hierarchien - Objekte {#objects}

>[!NOTE]
>
>Bitte nach links/rechts scrollen, um den vollständigen Inhalt der Tabelle anzuzeigen.

| Funktion | Beschreibung | Parameter | Aufbau | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| is_empty | Prüft, ob ein Objekt leer ist. | <ul><li>INPUT: **Erforderlich** Das Objekt, das Sie überprüfen möchten, ist leer.</li></ul> | is_empty(INPUT) | `is_empty([1, null, 2, 3])` | false |
| arrays_to_object | Erstellt eine Liste von Objekten. | <ul><li>INPUT: **Erforderlich** Eine Gruppierung von Schlüssel- und Array-Paaren.</li></ul> | arrays_to_object(INPUT) | `arrays_to_objects('sku', explode("id1\|id2", '\\\|'), 'price', [22.5,14.35])` | ```[{ "sku": "id1", "price": 22.5 }, { "sku": "id2", "price": 14.35 }]``` |
| to_object | Erstellt ein -Objekt basierend auf den angegebenen einfachen Schlüssel/Wert-Paaren. | <ul><li>INPUT: **Erforderlich** Eine flache Liste von Schlüssel/Wert-Paaren.</li></ul> | to_object(INPUT) | to_object&#x200B;(„firstName“, „John“, „lastName“, „Doe„) | `{"firstName": "John", "lastName": "Doe"}` |
| str_to_object | Erstellt ein -Objekt aus der Eingabezeichenfolge. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, die geparst wird, um ein -Objekt zu erstellen.</li><li>VALUE_DELIMITER: *Optional* Das Trennzeichen, das ein Feld vom Wert trennt. Das standardmäßige Trennzeichen ist `:`.</li><li>FIELD_DELIMITER: *Optional* Das Trennzeichen, das Feldwertpaare trennt. Das standardmäßige Trennzeichen ist `,`.</li></ul> | str_to_object&#x200B;(STRING, VALUE_DELIMITER, FIELD_DELIMITER) **Hinweis**: Sie können die `get()`-Funktion zusammen mit `str_to_object()` verwenden, um Werte für die Schlüssel in der Zeichenfolge abzurufen. | <ul><li>Beispiel #1: str_to_object(„firstName - John ; lastName - ; - 123 345 7890“, &quot;-&quot;, &quot;;„)</li><li>Beispiel #2: str_to_object(„firstName - John ; lastName - ; Telefon - 123 456 7890“, &quot;-&quot;, &quot;;„).get(„firstName„)</li></ul> | <ul><li>Beispiel #1:`{"firstName": "John", "lastName": "Doe", "phone": "123 456 7890"}`</li><li>Beispiel #2: „John“</li></ul> |
| contains_key | Prüft, ob das Objekt in den Quelldaten vorhanden ist. **Hinweis:** Diese Funktion ersetzt die veraltete `is_set()`. | <ul><li>INPUT: **Erforderlich** Der Pfad, der überprüft werden soll, wenn er in den Quelldaten vorhanden ist.</li></ul> | contains_key(INPUT) | CONTAINS_KEY(„eVars.eVar.field1„) | wahr |
| für nichtig erklären | Setzt den Wert des Attributs auf `null`. Dies sollte verwendet werden, wenn Sie das Feld nicht in das Zielschema kopieren möchten. | | nullify() | nullify() | `null` |
| get_keys | Analysiert die Schlüssel/Wert-Paare und gibt alle Schlüssel zurück. | <ul><li>OBJEKT: **Erforderlich** Das Objekt, aus dem die Schlüssel extrahiert werden.</li></ul> | get_keys(OBJECT) | get_keys({„book1“: „Stolz und Vorurteil“, „book2“: „1984“}) | `["book1", "book2"]` |
| get_values | Analysiert die Schlüssel/Wert-Paare und gibt den Wert der Zeichenfolge basierend auf dem angegebenen Schlüssel zurück. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, die Sie analysieren möchten.</li><li>KEY: **Required** Der Schlüssel, für den der Wert extrahiert werden muss.</li><li>VALUE_DELIMITER: **Erforderlich** Das Trennzeichen, das das Feld und den Wert trennt. Wenn entweder eine `null` oder eine leere Zeichenfolge angegeben wird, wird dieser Wert `:`.</li><li>FIELD_DELIMITER: *Optional* Das Trennzeichen, das Feld- und Wertpaare trennt. Wenn entweder eine `null` oder eine leere Zeichenfolge angegeben wird, wird dieser Wert `,`.</li></ul> | get_values(STRING, KEY, VALUE_DELIMITER, FIELD_DELIMITER) | get_values(\„firstName - John , lastName - Cena , Telefon - 555 420 8692\&quot;, \„firstName\&quot;, \&quot;-\&quot;, \&quot;,\„) | John |
| map_get_values | Nimmt eine Zuordnung und eine Eingabe. Wenn die Eingabe ein einzelner Schlüssel ist, gibt die Funktion den mit diesem Schlüssel verknüpften Wert zurück. Wenn die Eingabe ein Zeichenfolgen-Array ist, gibt die Funktion alle Werte zurück, die den bereitgestellten Schlüsseln entsprechen. Wenn die eingehende Zuordnung doppelte Schlüssel enthält, muss der Rückgabewert die Schlüssel deduplizieren und eindeutige Werte zurückgeben. | <ul><li>ZUORDNUNG: **Erforderlich** Die Eingabe-Zuordnungsdaten.</li><li>KEY: **Erforderlich** Der Schlüssel kann eine einzelne Zeichenfolge oder ein Zeichenfolgen-Array sein. Wenn ein anderer primitiver Typ (Daten/Zahl) angegeben wird, wird er als Zeichenfolge behandelt.</li></ul> | get_values(MAP, KEY) | Ein Codebeispiel finden Sie [Anhang](#map_get_values) . | |
| map_has_keys | Wenn eine oder mehrere Eingabetasten bereitgestellt werden, gibt die Funktion „true“ zurück. Wenn ein Zeichenfolgen-Array als Eingabe bereitgestellt wird, gibt die Funktion für den ersten gefundenen Schlüssel „true“ zurück. | <ul><li>ZUORDNUNG: **Erforderlich** Die Eingabe-Zuordnungsdaten</li><li>KEY: **Erforderlich** Der Schlüssel kann eine einzelne Zeichenfolge oder ein Zeichenfolgen-Array sein. Wenn ein anderer primitiver Typ (Daten/Zahl) angegeben wird, wird er als Zeichenfolge behandelt.</li></ul> | map_has_keys(MAP, KEY) | Ein Codebeispiel finden Sie [Anhang](#map_has_keys) . | |
| add_to_map | Akzeptiert mindestens zwei Eingaben. Als Eingabe können beliebig viele Zuordnungen bereitgestellt werden. Die Datenvorbereitung gibt eine einzelne Zuordnung zurück, die alle Schlüssel-Wert-Paare aus allen Eingaben enthält. Wenn ein oder mehrere Schlüssel wiederholt werden (in derselben Zuordnung oder in allen Zuordnungen), dedupliziert die Datenvorbereitung die Schlüssel, sodass das erste Schlüssel-Wert-Paar in der Reihenfolge verbleibt, in der sie in der Eingabe übergeben wurden. | ZUORDNUNG: **Erforderlich** Die Eingabe-Zuordnungsdaten. | add_to_map(MAP 1, MAP 2, MAP 3, …) | Ein Codebeispiel finden Sie [Anhang](#add_to_map) . | |
| object_to_map (Syntax 1) | Mit dieser Funktion können Sie Datentypen zuordnen erstellen. | <ul><li>KEY: **Required** Schlüssel müssen eine Zeichenfolge sein. Wenn andere primitive Werte wie Ganzzahlen oder Datumswerte angegeben werden, werden sie automatisch in Zeichenfolgen konvertiert und als Zeichenfolgen behandelt.</li><li>ANY_TYPE: **Erforderlich** Bezieht sich auf jeden unterstützten XDM-Datentyp außer Zuordnungen.</li></ul> | object_to_map(KEY, ANY_TYPE, KEY, ANY_TYPE, … ) | Ein Codebeispiel finden Sie [Anhang](#object_to_map) . | |
| object_to_map (Syntax 2) | Mit dieser Funktion können Sie Datentypen zuordnen erstellen. | <ul><li>OBJECT: **Erforderlich** Sie können ein eingehendes Objekt oder Objekt-Array bereitstellen und auf ein Attribut innerhalb des Objekts als Schlüssel verweisen.</li></ul> | object_to_map(OBJECT) | Ein Codebeispiel finden Sie [Anhang](#object_to_map) . |
| object_to_map (Syntax 3) | Mit dieser Funktion können Sie Datentypen zuordnen erstellen. | <ul><li>OBJECT: **Erforderlich** Sie können ein eingehendes Objekt oder Objekt-Array bereitstellen und auf ein Attribut innerhalb des Objekts als Schlüssel verweisen.</li></ul> | object_to_map(OBJECT_ARRAY, ATTRIBUTE_IN_OBJECT_TO_BE_USED_AS_A_KEY) | Ein Codebeispiel finden Sie [Anhang](#object_to_map) . |

{style="table-layout:auto"}

Informationen zur Funktion zum Kopieren von Objekten finden Sie im Abschnitt [unten](#object-copy).

### Hierarchien - Arrays {#arrays}

>[!NOTE]
>
>Bitte nach links/rechts scrollen, um den vollständigen Inhalt der Tabelle anzuzeigen.

| Funktion | Beschreibung | Parameter | Aufbau | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| coalesce | Gibt das erste Objekt zurück, das nicht null ist, in einem angegebenen Array. | <ul><li>INPUT: **Erforderlich** Das Array, von dem Sie das erste Objekt finden möchten, das nicht null ist.</li></ul> | zusammenfügen (EINGABE) | COALESCE(null, null, null, „first“, null, „second„) | „Erste“ |
| first | Ruft das erste Element des angegebenen Arrays ab. | <ul><li>INPUT: **Erforderlich** Das Array, in dem Sie das erste Element finden möchten.</li></ul> | first(INPUT) | first(„1“, „2“, „3„) | „1“ |
| last | Ruft das letzte Element des angegebenen Arrays ab. | <ul><li>INPUT: **Erforderlich** Das Array, von dem Sie das letzte Element finden möchten.</li></ul> | last(INPUT) | last(„1“, „2“, „3„) | „3“ |
| add_to_array | Fügt Elemente am Ende des Arrays hinzu. | <ul><li>ARRAY: **Erforderlich** Das Array, dem Sie Elemente hinzufügen.</li><li>WERTE: Die Elemente, die Sie an das Array anhängen möchten.</li></ul> | add_to_array&#x200B;(ARRAY, VALUES) | ADD_TO_ARRAY&#x200B;([&#39;a&#39;, &#39;b&#39;], &#39;c&#39;, &#39;d&#39;) | [&#39;a&#39;, &#39;b&#39;, &#39;c&#39;, &#39;d&#39;] |
| join_arrays | Kombiniert die Arrays miteinander. | <ul><li>ARRAY: **Erforderlich** Das Array, dem Sie Elemente hinzufügen.</li><li>WERTE: Die Arrays, die Sie an das übergeordnete Array anhängen möchten.</li></ul> | join_arrays&#x200B;(ARRAY, VALUES) | JOIN_ARRAYS&#x200B;([&#39;A&#39;, &#39;B&#39;], [&#39;C&#39;], [&#39;D&#39;, &#39;E&#39;]) | [&#39;a&#39;, &#39;b&#39;, &#39;c&#39;, &#39;d&#39;, &#39;e&#39;] |
| to_array | Nimmt eine Liste von Eingaben und konvertiert sie in ein Array. | <ul><li>INCLUDE_NULLS: **Required** Ein boolescher Wert, der angibt, ob NULL im Antwort-Array enthalten sein sollen oder nicht.</li><li>WERTE: **Erforderlich** Die Elemente, die in ein Array konvertiert werden sollen.</li></ul> | to_array&#x200B;(INCLUDE_NULLS, VALUES) | to_array(false, 1, null, 2, 3) | `[1, 2, 3]` |
| size_of | Gibt die Größe der Eingabe zurück. | <ul><li>INPUT: **Erforderlich** Das Objekt, dessen Größe Sie suchen.</li></ul> | size_of(INPUT) | `size_of([1, 2, 3, 4])` | 4 |
| upsert_array_append | Mit dieser Funktion werden alle Elemente im gesamten Eingabe-Array an das Ende des Arrays im Profil angehängt. Diese Funktion ist **nur** während Aktualisierungen anwendbar. Bei Verwendung im Kontext von Einfügungen gibt diese Funktion die Eingabe wie vorliegend zurück. | <ul><li>ARRAY: **Erforderlich** Das Array zum Anhängen des Arrays im Profil.</li></ul> | upsert_array_append(ARRAY) | `upsert_array_append([123, 456])` | [123 456 ] |
| upsert_array_replace | Diese Funktion wird verwendet, um Elemente in einem Array zu ersetzen. Diese Funktion ist **nur** während Aktualisierungen anwendbar. Bei Verwendung im Kontext von Einfügungen gibt diese Funktion die Eingabe wie vorliegend zurück. | <ul><li>ARRAY: **Erforderlich** Das Array, das das Array im Profil ersetzen soll.</li></li> | upsert_array_replace(ARRAY) | `upsert_array_replace([123, 456], 1)` | [123 456 ] |
| [!BADGE Nur Ziele]{type=Informative} array_to_string | Verbindet die Zeichenfolgendarstellungen der Elemente in einem Array mit dem angegebenen Trennzeichen. Wenn das Array mehrdimensional ist, wird es reduziert, bevor es verbunden wird. **Hinweis**: Diese Funktion wird in Zielen verwendet. Weitere Informationen finden [ in der ](../destinations/ui/export-arrays-maps-objects.md). | <ul><li>SEPARATOR: **Erforderlich** Das Trennzeichen, das zum Verbinden der Elemente im Array verwendet wird.</li><li>ARRAY: **Erforderlich** Das Array, das verbunden werden soll (nach dem Reduzieren).</li></ul> | array_to_string(SEPARATOR, ARRAY) | `array_to_string(";", ["Hello", "world"])` | „Hallo;Welt“ |
| [!BADGE Nur Ziele]{type=Informative} filterArray* | Filtert das angegebene Array basierend auf einer Eigenschaft. **Hinweis**: Diese Funktion wird in Zielen verwendet. Weitere Informationen finden [ in der ](../destinations/ui/export-arrays-maps-objects.md). | <ul><li>ARRAY: **Erforderlich** Das zu filternde Array</li><li>PRÄDIKAT: **Erforderlich** Das Prädikat, das auf jedes Element des angegebenen Arrays angewendet werden soll. | filterArray(ARRAY, PREDICATE) | `filterArray([5, -6, 0, 7], x -> x > 0)` | [5, 7 ] |
| [!BADGE Nur Ziele]{type=Informative} transformArray* | Transformiert das angegebene Array basierend auf einer Eigenschaft. **Hinweis**: Diese Funktion wird in Zielen verwendet. Weitere Informationen finden [ in der ](../destinations/ui/export-arrays-maps-objects.md). | <ul><li>ARRAY: **Erforderlich** Das zu transformierende Array.</li><li>PRÄDIKAT: **Erforderlich** Das Prädikat, das auf jedes Element des angegebenen Arrays angewendet werden soll. | transformArray(ARRAY, PREDICATE) | ` transformArray([5, 6, 7], x -> x + 1)` | [6, 7, 8 ] |
| [!BADGE Nur Ziele]{type=Informative} flachenArray* | Reduziert das angegebene (mehrdimensionale) Array auf ein eindimensionales Array. **Hinweis**: Diese Funktion wird in Zielen verwendet. Weitere Informationen finden [ in der ](../destinations/ui/export-arrays-maps-objects.md). | <ul><li>ARRAY: **Erforderlich** Das Array, das reduziert werden soll.</li></ul> | flachenArray(Array) | flachenArray([[[&#39;a&#39;, &#39;b&#39;], [&#39;c&#39;, &#39;d&#39;]], [[&#39;e&#39;], [&#39;f&#39;]])) | [&#39;a&#39;, &#39;b&#39;, &#39;c&#39;, &#39;d&#39;, &#39;e&#39;, &#39;f&#39;] |

{style="table-layout:auto"}

### Hierarchien - Zuordnung {#map}

>[!NOTE]
>
>Bitte nach links/rechts scrollen, um den vollständigen Inhalt der Tabelle anzuzeigen.

| Funktion | Beschreibung | Parameter | Aufbau | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| array_to_map | Diese Funktion akzeptiert ein Objekt-Array und einen Schlüssel als Eingabe und gibt eine Zuordnung des Schlüsselfelds mit dem Wert als Schlüssel und dem Array-Element als Wert zurück. | <ul><li>INPUT: **Erforderlich** Das Objekt-Array, von dem Sie das erste Objekt finden möchten, das nicht null ist.</li><li>KEY: **Required** Der Schlüssel muss ein Feldname im Objekt-Array und das Objekt als Wert sein.</li></ul> | array_to_map(OBJECT[] INPUTS, KEY) | Ein Codebeispiel finden [ im ](#object_to_map)Anhang“. |
| object_to_map | Diese Funktion akzeptiert ein -Objekt als Argument und gibt eine Zuordnung von Schlüssel-Wert-Paaren zurück. | <ul><li>INPUT: **Erforderlich** Das Objekt-Array, von dem Sie das erste Objekt finden möchten, das nicht null ist.</li></ul> | object_to_map(OBJECT_INPUT) | „object_to_map(address) where input is &quot; + „address: {line1 : \„345 park ave\&quot;,line2: \„bldg 2\&quot;,city : \„san jose\&quot;,state : \„CA\&quot;,type: \„office\&quot;}&quot; | Gibt eine Zuordnung mit angegebenen Feldnamen- und Wertepaaren zurück oder null, wenn die Eingabe null ist. Beispiel: `"{line1 : \"345 park ave\",line2: \"bldg 2\",City : \"san jose\",State : \"CA\",type: \"office\"}"` |
| to_map | Diese Funktion nimmt eine Liste von Schlüssel-Wert-Paaren und gibt eine Zuordnung von Schlüssel-Wert-Paaren zurück. | | to_map(OBJECT_INPUT) | „to_map(\„firstName\&quot;, \„John\&quot;, \„lastName\&quot;, \„Doe\„)“ | Gibt eine Zuordnung mit angegebenen Feldnamen- und Wertepaaren zurück oder null, wenn die Eingabe null ist. Beispiel: `"{\"firstName\" : \"John\", \"lastName\": \"Doe\"}"` |

{style="table-layout:auto"}

### Logische Operatoren {#logical-operators}

>[!NOTE]
>
>Bitte nach links/rechts scrollen, um den vollständigen Inhalt der Tabelle anzuzeigen.

| Funktion | Beschreibung | Parameter | Aufbau | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| decode | Wenn ein Schlüssel und eine Liste von Schlüsselwertpaaren als Array reduziert sind, gibt die Funktion den Wert zurück, wenn der Schlüssel gefunden wird, oder gibt einen Standardwert zurück, wenn er im Array vorhanden ist. | <ul><li>KEY: **Required** Der Schlüssel, der abgeglichen werden soll.</li><li>OPTIONS: **Erforderlich** Ein reduziertes Array von Schlüssel/Wert-Paaren. Optional kann ein Standardwert am Ende eingefügt werden.</li></ul> | decode(KEY, OPTIONS) | decode(stateCode, „ca“, „California“, „pa“, „Pennsylvania“, „N/A„) | Wenn der angegebene stateCode „ca“, „California“ lautet.<br>Wenn der angegebene stateCode „pa“, „Pennsylvania“ lautet.<br>Wenn der stateCode nicht dem folgenden Wert entspricht, „K. A.“. |
| IIF | Wertet einen gegebenen booleschen Ausdruck aus und gibt den angegebenen Wert basierend auf dem Ergebnis zurück. | <ul><li>AUSDRUCK: **Erforderlich** Der boolesche Ausdruck, der ausgewertet wird.</li><li>TRUE_VALUE: **Erforderlich** Der Wert, der zurückgegeben wird, wenn der Ausdruck „true“ ergibt.</li><li>FALSE_VALUE: **Erforderlich** Der Wert, der zurückgegeben wird, wenn der Ausdruck als „false“ ausgewertet wird.</li></ul> | IF(EXPRESSION, TRUE_VALUE, FALSE_VALUE) | if(„s“.equalsIgnoreCase(„S„), „True“, „False„) | „TRUE“ |

{style="table-layout:auto"}

### Aggregation {#aggregation}

>[!NOTE]
>
>Bitte nach links/rechts scrollen, um den vollständigen Inhalt der Tabelle anzuzeigen.

| Funktion | Beschreibung | Parameter | Aufbau | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| min | Gibt das Minimum der angegebenen Argumente zurück. Verwendet eine natürliche Reihenfolge. | <ul><li>OPTIONS: **Erforderlich** Ein oder mehrere Objekte, die miteinander verglichen werden können.</li></ul> | min(OPTIONS) | MIN(3, 1, 4) | 1 |
| max | Gibt das Maximum der angegebenen Argumente zurück. Verwendet eine natürliche Reihenfolge. | <ul><li>OPTIONS: **Erforderlich** Ein oder mehrere Objekte, die miteinander verglichen werden können.</li></ul> | max(OPTIONS) | max(3, 1, 4) | 4 |

{style="table-layout:auto"}

### Typkonvertierungen {#type-conversions}

>[!NOTE]
>
>Bitte nach links/rechts scrollen, um den vollständigen Inhalt der Tabelle anzuzeigen.

| Funktion | Beschreibung | Parameter | Aufbau | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| to_bigint | Konvertiert eine Zeichenfolge in eine BigInteger. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, die in eine BigInteger-Zahl konvertiert werden soll.</li></ul> | to_bigint(ZEICHENFOLGE) | to_bigint&#x200B;(„1000000.34„) | 1000000,34 |
| to_decimal | Konvertiert eine Zeichenfolge in Double. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, die in eine Double-Zeichenfolge konvertiert werden soll.</li></ul> | to_decimal(ZEICHENFOLGE) | to_decimal(„20.5„) | 20,5 |
| to_float | Konvertiert eine Zeichenfolge in einen Gleitkommazahl. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, die in einen Float konvertiert werden soll.</li></ul> | to_float(STRING) | to_float(„12.3456„) | 12,34566 |
| to_integer | Konvertiert eine Zeichenfolge in eine Ganzzahl. | <ul><li>STRING: **Erforderlich** Die Zeichenfolge, die in eine Ganzzahl konvertiert werden soll.</li></ul> | to_integer(STRING) | to_integer(„12„) | 12 |

{style="table-layout:auto"}

### JSON-Funktionen {#json}

>[!NOTE]
>
>Bitte nach links/rechts scrollen, um den vollständigen Inhalt der Tabelle anzuzeigen.

| Funktion | Beschreibung | Parameter | Aufbau | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| json_to_object | Deserialisieren von JSON-Inhalten aus der angegebenen Zeichenfolge. | <ul><li>STRING: **Erforderlich** Die zu deserialisierende JSON-Zeichenfolge.</li></ul> | json_to_object&#x200B;(STRING) | json_to_object&#x200B;({„info“:{„firstName“:„John“,„lastName“: „Doe“}}) | Ein Objekt, das die JSON darstellt. |

{style="table-layout:auto"}

### Spezielle Operationen {#special-operations}

>[!NOTE]
>
>Bitte nach links/rechts scrollen, um den vollständigen Inhalt der Tabelle anzuzeigen.

| Funktion | Beschreibung | Parameter | Aufbau | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| uuid /<br>guid | Erzeugt eine pseudo-zufällige ID. | | uuid()<br>guid() | uuid()<br>guid() | 7c0267d2-bb74-4e1a-9275-3bf4fccda5f4<br>c7016dc7-3163-43f7-afc7-2e1c9c206333 |
| `fpid_to_ecid ` | Diese Funktion wandelt eine FPID-Zeichenfolge in eine ECID um, die in Adobe Experience Platform- und Adobe Experience Cloud-Anwendungen verwendet werden kann. | <ul><li>STRING: **Erforderlich** Die FPID-Zeichenfolge, die in eine ECID konvertiert werden soll.</li></ul> | `fpid_to_ecid(STRING)` | `fpid_to_ecid("4ed70bee-b654-420a-a3fd-b58b6b65e991")` | `"28880788470263023831040523038280731744"` |

{style="table-layout:auto"}

### User Agent-Funktionen {#user-agent}

Jede der in der folgenden Tabelle enthaltenen Benutzeragentenfunktionen kann einen der folgenden Werte zurückgeben:

* Smartphone : Ein Mobilgerät mit einem kleinen Bildschirm (häufig &lt; 7 Zoll)
* Mobile : Ein Mobilgerät, das noch identifiziert werden muss. Bei diesem Mobilgerät kann es sich um einen eReader, ein Tablet, ein Smartphone, eine Uhr usw. handeln.

Weitere Informationen zu Gerätefeldwerten finden Sie in der [Liste der Gerätefeldwerte](#device-field-values) im Anhang dieses Dokuments.

>[!NOTE]
>
>Bitte nach links/rechts scrollen, um den vollständigen Inhalt der Tabelle anzuzeigen.

| Funktion | Beschreibung | Parameter | Aufbau | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| ua_os_name | Extrahiert den Betriebssystemnamen aus der Benutzeragenten-Zeichenfolge. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragenten-Zeichenfolge.</li></ul> | ua_os_name&#x200B;(USER_AGENT) | ua_os_name&#x200B;(„Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3„) | iOS |
| ua_os_version_major | Extrahiert die Hauptversion des Betriebssystems aus der Benutzeragenten-Zeichenfolge. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragenten-Zeichenfolge.</li></ul> | ua_os_version_major&#x200B;(USER_AGENT) | ua_os_version_major&#x200B;s(„Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3„) | IOS 5 |
| ua_os_version | Extrahiert die Betriebssystemversion aus der Benutzeragenten-Zeichenfolge. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragenten-Zeichenfolge.</li></ul> | ua_os_version&#x200B;(USER_AGENT) | ua_os_version&#x200B;(„Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3„) | 5.1.1 |
| ua_os_name_version | Extrahiert Namen und Version des Betriebssystems aus der Benutzeragenten-Zeichenfolge. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragenten-Zeichenfolge.</li></ul> | ua_os_name_version&#x200B;(USER_AGENT) | ua_os_name_version&#x200B;(„Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 wie Mac OS X) AppleWebKit/534.46 (KHTML, wie Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3„) | iOS 5.1.1 |
| ua_agent_version | Extrahiert die Agentenversion aus der Benutzeragenten-Zeichenfolge. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragenten-Zeichenfolge.</li></ul> | ua_agent_version&#x200B;(USER_AGENT) | ua_agent_version&#x200B;(„Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3„) | 5,1 |
| ua_agent_version_major | Extrahiert den Agentennamen und die Hauptversion aus der Benutzeragenten-Zeichenfolge. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragenten-Zeichenfolge.</li></ul> | ua_agent_version_major&#x200B;(USER_AGENT) | ua_agent_version_major&#x200B;(„Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 wie Mac OS X) AppleWebKit/534.46 (KHTML, wie Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3„) | Safari 5 |
| ua_agent_name | Extrahiert den Namen des Agenten aus der Benutzeragenten-Zeichenfolge. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragenten-Zeichenfolge.</li></ul> | ua_agent_name&#x200B;(USER_AGENT) | ua_agent_name&#x200B;(„Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3„) | Safari |
| ua_device_class | Extrahiert die Geräteklasse aus der Benutzeragenten-Zeichenfolge. | <ul><li>USER_AGENT: **Erforderlich** Die Benutzeragenten-Zeichenfolge.</li></ul> | ua_device_class&#x200B;(USER_AGENT) | ua_device_class&#x200B;(„Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3„) | Telefon |

{style="table-layout:auto"}

### Analytics-Funktionen {#analytics}

>[!NOTE]
>
>Sie können nur die folgenden Analysefunktionen für WebSDK- und Adobe Analytics-Flüsse verwenden.

| Funktion | Beschreibung | Parameter | Aufbau | Ausdruck | Beispielausgabe |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| aa_get_event_id | Extrahiert die Ereignis-ID aus einer Analytics-Ereigniszeichenfolge. | <ul><li>EVENT_STRING: **Erforderlich** Die kommagetrennte Analytics-Ereigniszeichenfolge.</li><li>EVENT_NAME: **Erforderlich** Der Ereignisname, aus dem extrahiert werden soll und die ID.</li></ul> | aa_get_event_id(EVENT_STRING, EVENT_NAME) | aa_get_event_id(„event101=5:123456,scOpen“, „event101„) | 123456 |
| aa_get_event_value | Extrahiert den Ereigniswert aus einer Analytics-Ereigniszeichenfolge. Wenn der Ereigniswert nicht angegeben ist, wird 1 zurückgegeben. | <ul><li>EVENT_STRING: **Erforderlich** Die kommagetrennte Analytics-Ereigniszeichenfolge.</li><li>EVENT_NAME: **Erforderlich** Der Ereignisname, aus dem ein Wert extrahiert werden soll.</li></ul> | aa_get_event_value(EVENT_STRING, EVENT_NAME) | aa_get_event_value(„event101=5:123456,scOpen“, „event101„) | 5 |
| aa_get_product_categories | Extrahiert die Produktkategorie aus einer Analytics-Produktzeichenfolge. | <ul><li>PRODUCTS_STRING: **Erforderlich** Die Analytics-Produktzeichenfolge.</li></ul> | aa_get_product_categories(PRODUCTS_STRING) | aa_get_product_categories(“;Beispielprodukt 1;1;3.50,Beispielkategorie 2;Beispielprodukt 2;1;5.99„) | [null,„Beispiel für Kategorie 2“] |
| aa_get_product_names | Extrahiert den Produktnamen aus einer Analytics-Produktzeichenfolge. | <ul><li>PRODUCTS_STRING: **Erforderlich** Die Analytics-Produktzeichenfolge.</li></ul> | aa_get_product_names(PRODUCTS_STRING) | aa_get_product_names(“;Beispielprodukt 1;1;3.50,Beispielkategorie 2;Beispielprodukt 2;1;5.99„) | [„Beispielprodukt 1“,„Beispielprodukt 2“] |
| aa_get_product_quantity | Extrahiert die Mengen aus einer Analytics-Produktzeichenfolge. | <ul><li>PRODUCTS_STRING: **Erforderlich** Die Analytics-Produktzeichenfolge.</li></ul> | aa_get_product_quantity(PRODUCTS_STRING) | aa_get_product_quantity(“;Beispielprodukt 1;1;3.50,Beispielkategorie 2;Beispielprodukt 2„) | [„1“, null] |
| aa_get_product_prices | Extrahiert den Preis aus einer Analytics-Produktzeichenfolge. | <ul><li>PRODUCTS_STRING: **Erforderlich** Die Analytics-Produktzeichenfolge.</li></ul> | aa_get_product_prices(PRODUCTS_STRING) | aa_get_product_prices(“;Beispielprodukt 1;1;3.50,Beispielkategorie 2;Beispielprodukt 2„) | [„3.50“, null] |
| aa_get_product_event_values | Extrahiert Werte für das benannte Ereignis aus der Produktzeichenfolge als Zeichenfolgen-Array. | <ul><li>PRODUCTS_STRING: **Erforderlich** Die Analytics-Produktzeichenfolge.</li><li>EVENT_NAME: **Erforderlich** Der Ereignisname, aus dem Werte extrahiert werden sollen.</li></ul> | aa_get_product_event_values(PRODUCTS_STRING, EVENT_NAME) | aa_get_product_event_values(“;Beispielprodukt 1;1;4.20;event1=2.3\|event2=5:1,;Beispielprodukt 2;1;4.20;event1=3\|event2=2:2“, „event1„) | [„2.3“, „3“] |
| aa_get_product_evars | Extrahiert die eVar-Werte für das benannte Ereignis aus der Produktzeichenfolge als Zeichenfolgen-Array. | <ul><li>PRODUCTS_STRING: **Erforderlich** Die Analytics-Produktzeichenfolge.</li><li>EVAR_NAME: **Erforderlich** Der zu extrahierende eVar-Name.</li></ul> | aa_get_product_evars(PRODUCTS_STRING, EVENT_NAME) | aa_get_product_evars(“;Beispielprodukt;1;6.69;;eVar1=Merchandising-Wert“, &quot;eVar1„) | [„Merchandising-Wert“] |

{style="table-layout:auto"}

<!-- | aa_get_product_events | Extracts a named event from the products string as an array of objects. | <ul><li>PRODUCTS_STRING: **Required** The Analytics products string.</li><li>EVENT_NAME: **Required** The event name to extract values from.</li></ul> | aa_get_product_events(PRODUCTS_STRING, EVENT_NAME) | aa_get_product_events(";Example product 1;1;4.20;event1=2.3\|event2=5:1,;Example product 2;1;4.20;event1=3\|event2=2:2", "event2") | [`{"id": "1","value", "5"}`, `{"id": "2","value", "1"}`] |
| aa_get_product_event_ids | Extracts the IDs for the named event from the products string as an array of strings. | <ul><li>PRODUCTS_STRING: **Required** The Analytics products string.</li><li>EVENT_NAME: **Required** The event name to extract values from.</li></ul> | aa_get_product_event_ids(PRODUCTS_STRING, EVENT_NAME) | aa_get_product_event_ids(";Example product 1;1;4.20;event1=2.3\|event2=5:1,;Example product 2;1;4.20;event1=3\|event2=2:2", "event2") | ["1", "2"] | -->

### Objektkopie {#object-copy}

>[!TIP]
>
>Die Funktion zum Kopieren von Objekten wird automatisch angewendet, wenn ein Objekt in der Quelle einem Objekt in XDM zugeordnet wird. Keine zusätzlichen Aktionen von Benutzern erforderlich.

Mit der Funktion zum Kopieren von Objekten können Sie Attribute eines Objekts automatisch kopieren, ohne die Zuordnung zu ändern. Wenn Ihre Quelldaten beispielsweise die Struktur aufweisen:

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

Danach wird die Zuordnung zu:

```json
address -> addr
address.line1 -> addr.addrLine1
```

Im obigen Beispiel werden die Attribute `city` und `state` auch automatisch zur Laufzeit aufgenommen, da das `address`-Objekt `addr` zugeordnet ist. Wenn Sie ein `line2` in der XDM-Struktur erstellen würden und Ihre Eingabedaten auch ein -`line2` im `address` enthalten, werden sie ebenfalls automatisch aufgenommen, ohne dass die Zuordnung manuell geändert werden muss.

Um sicherzustellen, dass die automatische Zuordnung funktioniert, müssen die folgenden Voraussetzungen erfüllt sein:

* Objekte auf übergeordneter Ebene sollten zugeordnet werden;
* Im XDM-Schema müssen neue Attribute erstellt worden sein.
* Neue Attribute sollten über übereinstimmende Namen im Quellschema und im XDM-Schema verfügen.

Wenn eine der Voraussetzungen nicht erfüllt ist, müssen Sie das Quellschema mithilfe der Datenvorbereitung manuell dem XDM-Schema zuordnen.

## Anhang

Im Folgenden finden Sie zusätzliche Informationen zur Verwendung der Funktionen zur Datenvorbereitung

### Sonderzeichen {#special-characters}

In der folgenden Tabelle finden Sie eine Liste der reservierten Zeichen und der zugehörigen codierten Zeichen.

| Reserviertes Zeichen | Codiertes Zeichen |
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
| * | %2a |
| + | %2b |
| , | %2c |
| / | %2F |
| : | %3a |
|   | %3b |
| &lt; | %3c |
| = | %3d |
| > | %3E |
| ? | %3F |
| @ | %40 |
| [ | %5b |
| | | %5C |
| ] | %5d |
| ^ | %5E |
| &quot; | %60 |
| ~ | %7E |

{style="table-layout:auto"}

### Gerätefeldwerte {#device-field-values}

In der folgenden Tabelle finden Sie eine Liste der Gerätefeldwerte und die entsprechenden Beschreibungen.

| Gerät | Beschreibung |
| --- | --- |
| Desktop | Ein Desktop- oder Laptop-Gerät. |
| anonymisiert | Ein anonymes Gerät. In einigen Fällen handelt es sich dabei um `useragents`, die durch eine Anonymisierungssoftware verändert wurden. |
| Unbekannt | Ein unbekanntes Gerät. Diese sind in der Regel `useragents`, die keine Informationen über das Gerät enthalten. |
| Mobile | Ein Mobilgerät, das noch identifiziert werden muss. Bei diesem Mobilgerät kann es sich um einen eReader, ein Tablet, ein Smartphone, eine Uhr usw. handeln. |
| Tablet | Ein Mobilgerät mit einem großen Bildschirm (häufig > 7„). |
| Telefon | Ein Mobilgerät mit einem kleinen Bildschirm (häufig &lt; 7„). |
| Beobachten | Ein Mobilgerät mit einem winzigen Bildschirm (häufig &lt; 2„). Diese Geräte fungieren normalerweise als zusätzlicher Bildschirm für Geräte vom Typ Smartphones/Tablets. |
| erweiterte Realität | Ein Mobilgerät mit AR-Funktionen. |
| Virtuelle Realität | Ein Mobilgerät mit VR-Funktionen. |
| Lesegerät | Ein Gerät, das einem Tablet ähnelt, aber in der Regel mit einem [!DNL eInk] Bildschirm ausgestattet ist. |
| Set-Top-Box | Ein angeschlossenes Gerät, das die Interaktion über einen TV-Bildschirm ermöglicht. |
| TV | Ein Gerät, das der Set-Top-Box ähnelt, aber in den Fernseher integriert ist. |
| Haushaltsgerät | Ein (meist großes) Haushaltsgerät, wie ein Kühlschrank. |
| Spielkonsole | Ein festes Spielsystem wie ein [!DNL Playstation] oder ein [!DNL XBox]. |
| Handheld-Spielkonsole | Ein mobiles Spielsystem wie ein [!DNL Nintendo Switch]. |
| Stimme | Ein sprachgesteuertes Gerät wie ein [!DNL Amazon Alexa] oder ein [!DNL Google Home]. |
| Wagen | Ein fahrzeugbasierter Browser. |
| Roboter | Roboter, die eine Website besuchen. |
| Roboter mobil | Roboter, die eine Website besuchen, aber angeben, dass sie als mobiler Besucher angesehen werden möchten. |
| Roboterimitator | Roboter, die eine Website besuchen und so tun, als wären sie Roboter wie [!DNL Google], aber das sind sie nicht. **Hinweis**: In den meisten Fällen sind Roboterimitatoren tatsächlich Roboter. |
| Cloud | Eine Cloud-basierte Anwendung. Das sind weder Roboter noch Hacker, aber es sind Anwendungen, die sich verbinden müssen. Dazu gehören [!DNL Mastodon]. |
| Hacker | Dieser Gerätewert wird verwendet, falls Skripterstellung in der `useragent` erkannt wird. |

{style="table-layout:auto"}

### Code-Beispiele {#code-samples}

#### map_get_values {#map-get-values}

+++Beispiel auswählen, um es anzuzeigen

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

+++Beispiel auswählen, um es anzuzeigen

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

+++Beispiel auswählen, um es anzuzeigen

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

+++Beispiel auswählen, um es anzuzeigen

```json
example = "object_to_map(\"firstName\", \"John\", \"lastName\", \"Doe\")",
result = "{\"firstName\" : \"John\", \"lastName\": \"Doe\"}"
```

+++

**Syntax 2**

+++Beispiel auswählen, um es anzuzeigen

```json
example = "object_to_map(address) where input is " +
  "address: {line1 : \"345 park ave\",line2: \"bldg 2\",City : \"san jose\",State : \"CA\",type: \"office\"}",
result = "{line1 : \"345 park ave\",line2: \"bldg 2\",City : \"san jose\",State : \"CA\",type: \"office\"}"
```

+++

**Syntax 3**

+++Beispiel auswählen, um es anzuzeigen

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

+++Beispiel auswählen, um es anzuzeigen

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

