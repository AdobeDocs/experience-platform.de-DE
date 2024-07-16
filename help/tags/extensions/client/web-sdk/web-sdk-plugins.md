---
title: Übersicht über die allgemeine Web SDK-Plug-ins-Erweiterung
description: Erfahren Sie mehr über die allgemeine Web SDK-Plug-in-Tag-Erweiterung in Adobe Experience Platform.
exl-id: 6052603b-1537-4dc7-9278-969d892ca15b
source-git-commit: 12bd4c6c1993afc438b75a3e5163ebe2fe8a8dd0
workflow-type: tm+mt
source-wordcount: '2064'
ht-degree: 0%

---

# Übersicht über die allgemeine Web SDK-Plug-ins-Erweiterung

>[!IMPORTANT]
>
>Die Erweiterung soll mit der Adobe Experience Platform Web SDK-Erweiterung verwendet werden. Informationen zur Version, die mit AppMeasurement verwendet werden soll, finden Sie in der Übersicht zur [allgemeinen Analytics-Plug-in-Erweiterung](../plugins/overview.md).

In diesem Dokument wird beschrieben, wie Sie die Web SDK-Plug-in-Tag-Erweiterung konfigurieren und sie zum Erweitern der [Adobe Experience Platform Web SDK-Erweiterung](../web-sdk/overview.md) verwenden.

## Konfigurieren der allgemeinen Web SDK-Plug-in-Erweiterung

Dieser Abschnitt enthält eine Referenz zu den verfügbaren Optionen beim Konfigurieren der Web SDK Plugins-Erweiterung.

>[!IMPORTANT]
>
>Die Common Web SDK Plugins-Erweiterung soll die Adobe Experience Platform Web SDK-Erweiterung erweitern. Sie müssen sie jedoch nicht installiert haben, damit die Erweiterung erwartungsgemäß funktioniert.

## Hinzufügen von Plug-ins zur Adobe Experience Platform Web SDK-Erweiterung

Es ist keine Konfiguration erforderlich, um ein Plug-in zu Ihrer Bibliothek zu initialisieren oder hinzuzufügen, außerhalb der Verwendung der folgenden nativen Datenelemente, die von der Common Web SDK Plugins-Erweiterung bereitgestellt werden:

* [`getAndPersistValue`](#getAndPersistValue)
* [`getGeoCoordinates`](#getGeoCoordinates)
* [`getNewRepeat`](#getNewRepeat)
* [&quot;getPagename&quot;](#getPagename)
* [`getPreviousValue`](#getPreviousValue)
* [`getQueryParam`](#getQueryParam)
* [`getTimeParting`](#getTimeParting)
* [`getTimeSinceLastVisit`](#getTimeSInceLastVisit)
* [`getValOnce`](#getValOnce)
* [`getVisitDuration`](#getVisitDuration)
* [`getVisitNum`](#getVisitNum)
* [`pFo`](#pFo)

[//]: # (- [ ] Add links to plugin pages within the data elements below)

### `getAndPersistValue`

>[!IMPORTANT]
>
>Dieses Datenelement setzt Cookies und ermöglicht das Speichern benutzergenerierter Werte in Cookies. Weitere Informationen finden Sie in der Dokumentation zum Plug-in.

Ermöglicht die Einrichtung und Konfiguration des [`getAndPersistValue` Analytics-Plug-ins](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getandpersistvalue.html). Das Datenelement `getAndPersistValue` speichert einen Wert in einem Cookie, das später während eines Besuchs abgerufen werden kann.

Das Datenelement `getAndPersistValue` liefert die folgenden Argumente:

* `vtp` (erforderlich): Der Wert, der von Seite zu Seite beibehalten werden soll
* `cn` (optional): Der Name des Cookies, in dem der Wert gespeichert werden soll. Wenn dieses Argument nicht festgelegt ist, heißt das Cookie `"s_gapv"`
* `ex` (optional): Die Anzahl der Tage vor Ablauf des Cookies. Wenn dieses Argument `0` ist oder nicht gesetzt ist, läuft das Cookie am Ende des Besuchs ab (30 Minuten Inaktivität).

Wenn die Variable im `vtp` -Argument festgelegt ist, setzt das Datenelement das Cookie und gibt dann den Cookie-Wert zurück. Wenn die Variable im `vtp` -Argument nicht festgelegt ist, gibt das Datenelement nur den Cookie-Wert zurück.

### `getGeoCoordinates`

>[!IMPORTANT]
>
>Dieses Plug-in erfordert den Standortzugriff auf den Client, gibt jedoch keine Ausnahme aus, wenn es sie nicht erhält.

Ermöglicht die Einrichtung und Konfiguration des [`getGeoCoordinates` Analytics-Plug-ins](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getgeocoordinates.html). Das Datenelement `getGeoCoordinates` erfasst den Längen- und Breitengrad der Geräte der Besucher.

Das Datenelement `getGeoCoordinates` verwendet keine Argumente. Es wird einer der folgenden Werte zurückgegeben:

* `"geo coordinates not available"`: Für Geräte, bei denen zum Zeitpunkt der Ausführung des Plug-ins keine Geolocation-Daten verfügbar sind. Dieser Wert wird häufig beim ersten Treffer des Besuchs verwendet, insbesondere wenn Besucher zunächst ihre Zustimmung zum Tracking ihrer Position erteilen müssen.
* `"error retrieving geo coordinates"`: Wenn das Plug-in beim Versuch, den Standort des Geräts abzurufen, auf Fehler stößt
* `"latitude=[LATITUDE] | longtitude=[LONGITUDE]"`: Wobei [LATITUDE]/[LONGITUDE] der Längen- und Breitengrad ist.

### `getNewRepeat`

>[!IMPORTANT]
>
>Dieses Datenelement setzt Cookies. Weitere Informationen finden Sie in der Dokumentation zum Plug-in.

Ermöglicht die Einrichtung und Konfiguration des [`getNewRepeat` Analytics-Plug-ins](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getnewrepeat.html). Das Datenelement `getNewRepeat` bestimmt, ob es sich bei einem Besucher um einen neuen Besucher oder einen wiederkehrenden Besucher innerhalb einer gewünschten Anzahl von Tagen handelt.

Das Datenelement `getNewRepeat` verwendet die folgenden Argumente:

* `d` (Ganzzahl, optional): Die erforderliche Mindestanzahl von Tagen zwischen Besuchen, die Besucher auf `"New"` zurücksetzt. Wenn dieses Argument nicht festgelegt ist, wird der Standardwert 30 Tage verwendet.

Dieses Datenelement gibt den Wert `"New"` zurück, wenn das vom Datenelement eingestellte Cookie nicht vorhanden oder abgelaufen ist. Gibt den Wert `"Repeat"` zurück, wenn das vom Datenelement eingestellte Cookie vorhanden ist und die Zeit seit dem aktuellen Treffer und die im Cookie festgelegte Zeit länger als 30 Minuten sind. Diese Methode gibt denselben Wert für einen gesamten Besuch zurück.

### `getPageName`

Ermöglicht die Einrichtung und Konfiguration des [`getPageName` Analytics-Plug-ins](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getpagename.html). Das Datenelement `getPageName` erstellt eine leicht lesbare, benutzerfreundlich formatierte Version der aktuellen URL.

Das Datenelement `getPageName` verwendet die folgenden Argumente:

* `si` (optional, Zeichenfolge): Eine ID, die am Anfang der Zeichenfolge eingefügt wird, welche die ID der Site darstellt. Dieser Wert kann entweder eine numerische ID oder ein benutzerfreundlicher Name sein. Wenn sie nicht festgelegt ist, wird standardmäßig die aktuelle Domäne verwendet.
* `qv` (optional, Zeichenfolge): Eine kommagetrennte Liste von Abfragezeichenfolgenparametern, die, wenn sie in der URL gefunden werden, der Zeichenfolge hinzugefügt werden
* `hv` (optional, Zeichenfolge): Eine kommagetrennte Liste von Parametern im URL-Hash, die, wenn sie in der URL gefunden werden, der Zeichenfolge hinzugefügt werden
* `de` (optional, Zeichenfolge): Das Trennzeichen zum Aufteilen einzelner Teile der Zeichenfolge. Die Standardeinstellung ist ein senkrecherisches Strich (`|`).

Das Datenelement gibt eine Zeichenfolge zurück, die eine benutzerfreundlich formatierte Version der URL enthält. Diese Zeichenfolge wird normalerweise der Variable `pageName` zugewiesen, kann aber auch in anderen Variablen verwendet werden.

### `getPreviousValue`

>[!IMPORTANT]
>
>Dieses Datenelement setzt Cookies und ermöglicht das Speichern benutzergenerierter Werte in Cookies. Weitere Informationen finden Sie in der Dokumentation zum Plug-in.

Ermöglicht die Einrichtung und Konfiguration des [`getPreviousValue` Analytics-Plug-ins](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getpreviousvalue.html). Das Datenelement `getPreviousValue` setzt eine Variable auf einen Wert, der bei einem vorherigen Treffer festgelegt wurde.

Das Datenelement `getPreviousValue` verwendet die folgenden Argumente:

* `v` (Zeichenfolge, erforderlich): Die Variable mit dem Wert, der an die nächste Bildanforderung übergeben werden soll. Eine häufig verwendete Variable ist `s.pageName` , um den Wert der vorherigen Seite abzurufen.
* `c` (Zeichenfolge, optional): Der Name des Cookies, in dem der Wert gespeichert wird.  Wenn dieses Argument nicht festgelegt ist, wird standardmäßig `"s_gpv"` verwendet.

Wenn Sie dieses Datenelement aufrufen, wird der im Cookie enthaltene Zeichenfolgenwert zurückgegeben. Das Plug-in setzt dann die Gültigkeit des Cookies zurück und weist ihm den Variablenwert aus dem `v` -Argument zu. Das Cookie läuft nach 30 Minuten Inaktivität ab.

### `getQueryParam`

Ermöglicht die Einrichtung und Konfiguration des [`getQueryParam` Analytics-Plug-ins](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getqueryparam.html). Das Datenelement `getQueryParam` extrahiert den Wert eines beliebigen Abfragezeichenfolgenparameters, der in einer URL enthalten ist. Dies ist nützlich, um interne und externe Kampagnencodes aus Landingpage-URLs zu extrahieren. Dies ist auch beim Extrahieren von Suchbegriffen oder anderen Abfragezeichenfolgenparametern nützlich. Dieses Datenelement bietet zuverlässige Funktionen zum Analysieren komplexer URLs, einschließlich Hashes und URLs, die mehrere Abfragezeichenfolgenparameter enthalten.

Das Datenelement `getQueryParam` verwendet die folgenden Argumente:

* `qsp` (erforderlich): Eine kommagetrennte Liste von Abfragezeichenfolgenparametern, nach denen in der URL gesucht werden soll. Dabei wird nicht zwischen Groß- und Kleinschreibung unterschieden.
* `de` (optional): Das Trennzeichen, das verwendet werden soll, wenn mehrere Abfragezeichenfolgenparameter übereinstimmen. Der Standardwert ist eine leere Zeichenfolge.
* `url` (optional): Eine benutzerdefinierte URL, Zeichenfolge oder Variable, aus der die Parameterwerte der Abfragezeichenfolge extrahiert werden. Die Standardeinstellung ist `window.location`.

Der Aufruf dieses Datenelements gibt einen Wert zurück, der von den oben genannten Argumenten und der URL abhängt:

* Wenn kein übereinstimmender Abfragezeichenfolgenparameter gefunden wird, gibt die Methode eine leere Zeichenfolge zurück.
* Wenn ein übereinstimmender Abfragezeichenfolgenparameter gefunden wird, gibt die Methode den Parameterwert der Abfragezeichenfolge zurück.
* Wenn ein übereinstimmender Abfragezeichenfolgenparameter gefunden wird, der Wert jedoch leer ist, gibt die Methode `true` zurück.
* Wenn mehrere übereinstimmende Abfragezeichenfolgenparameter gefunden werden, gibt die Methode eine Zeichenfolge zurück, bei der jeder Parameterwert durch die Zeichenfolge im `de` -Argument getrennt wird.

### `getTimeParting`

Ermöglicht die Einrichtung und Konfiguration des [`getTimeParting` Analytics-Plug-ins](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/gettimeparting.html). Das Datenelement `getTimeParting` erfasst die Details zu dem Zeitpunkt, zu dem eine beliebige messbare Aktivität auf Ihrer Site stattfindet. Dieses Datenelement ist nützlich, wenn Sie Metriken nach wiederholbarer Zeitteilung über einen bestimmten Datumsbereich aufschlüsseln möchten. Sie können beispielsweise Konversionsraten zwischen zwei verschiedenen Wochentagen vergleichen, z. B. alle Sonntage im Vergleich zu allen Donnerstagen. Sie können auch Tageszeiträume vergleichen, z. B. alle Morgen im Vergleich zu allen Abenden.

Das Datenelement `getTimeParting` verwendet das folgende Argument:

`t` (Optional, aber empfohlen, Zeichenfolge): Der Name der Zeitzone, in die die Ortszeit des Besuchers umgerechnet werden soll.  Die Standardeinstellung ist UTC/GMT-Zeit. Eine vollständige Liste der gültigen Werte finden Sie in der [Liste der Zeitzonen der TZ-Datenbank](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) auf Wikipedia.

Zu den allgemeinen gültigen Werten gehören:

* `"America/New_York"` für die östliche Zeit
* `"America/Chicago"` für zentrale Zeit
* `"America/Denver"` für die Mountain Time
* `"America/Los_Angeles"` für die Pacific Time

Der Aufruf dieses Datenelements gibt eine Zeichenfolge zurück, die die folgende durch einen senkrechten Strich (`|`) getrennte Zeichenfolge enthält:

* Das aktuelle Jahr
* Der aktuelle Monat
* Der Tag des Monats
* Der Wochentag
* Die aktuelle Zeit (AM/PM)

### `getTimeSinceLastVisit`

>[!IMPORTANT]
>
>Dieses Datenelement setzt Cookies. Weitere Informationen finden Sie in der Dokumentation zum Plug-in.

Ermöglicht die Einrichtung und Konfiguration des [`getTimeSinceLastVisit` Analytics-Plug-ins](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/gettimesincelastvisit.html). Das Datenelement &quot;`getTimeSinceLastVisit`&quot;verfolgt, wie lange ein Besucher nach seinem letzten Besuch gebraucht hat, um zu Ihrer Site zurückzukehren.

Das Datenelement `getTimeSinceLastVisit` verwendet keine Argumente. Es wird die seit dem letzten Besuch des Besuchers verstrichene Zeit zurückgegeben, die im folgenden Format zusammengefasst wurde:

* Die Zeit zwischen 30 Minuten und einer Stunde seit dem letzten Besuch wird auf den nächsten halbminütigen Benchmark gesetzt. Beispiel: `"30.5 minutes"`, `"53 minutes"`
* Die Zeit zwischen einer Stunde und einem Tag wird auf den nächsten viertelstündigen Benchmark gerundet. Beispiel: `"2.25 hours"`, `"7.5 hours"`
* Eine Zeit, die länger als ein Tag ist, wird auf den nächsten Tages-Benchmark gerundet. Beispiel: `"1 day"`, `"3 days"`, `"9 days"`, `"372 days"`
* Wenn ein Besucher noch keinen Besuch gemacht hat oder die verstrichene Zeit länger als zwei Jahre ist, wird der Wert auf `"New Visitor"` gesetzt.

### `getValOnce`

>[!IMPORTANT]
>
>Dieses Datenelement setzt Cookies und ermöglicht das Speichern benutzergenerierter Werte in Cookies. Weitere Informationen finden Sie in der Dokumentation zum Plug-in.

Ermöglicht die Einrichtung und Konfiguration des [`getValOnce` Analytics-Plug-ins](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvalonce.html). Das Datenelement `getValOnce` verhindert, dass eine Variable mehrmals auf denselben Wert gesetzt wird.

Das Datenelement `getValOnce` verwendet die folgenden Argumente:

* `vtc` (erforderlich, Zeichenfolge): Die Variable, die geprüft werden soll, ob sie gerade zuvor auf einen identischen Wert gesetzt wurde
* `cn` (optional, Zeichenfolge): Der Name des Cookies, das den zu prüfenden Wert enthält. Standardwert ist `"s_gvo"`
* `et` (optional, Ganzzahl): Der Ablauf des Cookies in Tagen (oder Minuten, je nach dem `ep` -Argument). Die Standardeinstellung ist `0`, die am Ende der Browser-Sitzung abläuft
* `ep` (optional, Zeichenfolge): Legen Sie dieses Argument nur fest, wenn das `et`-Argument ebenfalls festgelegt ist. Setzen Sie dieses Argument auf `"m"` , wenn das `et` -Argument in Minuten statt in Tagen ablaufen soll. Die Standardeinstellung ist `"d"`, wodurch das `et` -Argument in Tagen festgelegt wird.

Wenn das `vtc` -Argument und der Cookie-Wert übereinstimmen, gibt diese Methode eine leere Zeichenfolge zurück. Wenn das Argument `vtc` und der Cookie-Wert nicht übereinstimmen, gibt die Methode das Argument `vtc` als Zeichenfolge zurück.

### `getVisitDuration`

>[!IMPORTANT]
>
>Dieses Datenelement setzt Cookies. Weitere Informationen finden Sie in der Dokumentation zum Plug-in.

Ermöglicht die Einrichtung und Konfiguration des [`getVisitDuration` Analytics-Plug-ins](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvisitduration.html). Das Datenelement &quot;`getVisitDuration`&quot; verfolgt die Zeit in Minuten, die der Besucher bis zu diesem Zeitpunkt auf der Site verbracht hat.

Das Datenelement `getVisitDuration` verwendet keine Argumente. Es wird einer der folgenden Werte zurückgegeben:

* `"first hit of visit"`
* `"less than a minute"`
* `"1 minute"`
* `"[x] minutes"` (wobei `[x]` die Anzahl der Minuten ist, die seit der Landung des Besuchers auf der Site vergangen sind)

### `getVisitNum`

>[!IMPORTANT]
>
>Dieses Datenelement setzt Cookies. Weitere Informationen finden Sie in der Dokumentation zum Plug-in.

Ermöglicht die Einrichtung und Konfiguration des [`getVisitNum` Analytics-Plug-ins](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvisitnum.html). Das Datenelement `getVisitNum` gibt die Besuchsnummer für alle Besucher zurück, die innerhalb der gewünschten Anzahl von Tagen auf die Site kommen.

Das Datenelement `getVisitNum` verwendet die folgenden Argumente:

* `rp` (optional, Ganzzahl ODER Zeichenfolge): Die Anzahl der Tage, bevor der Besuchsnummerzähler zurückgesetzt wird.  Der Standardwert ist `365` , wenn nicht festgelegt.
   * Wenn dieses Argument `"w"` ist, wird der Zähler am Ende der Woche (an diesem Samstag um 23:59 Uhr) zurückgesetzt
   * Wenn dieses Argument `"m"` ist, wird der Zähler am Ende des Monats (am letzten Tag dieses Monats) zurückgesetzt
   * Wenn dieses Argument `"y"` ist, wird der Zähler am Ende des Jahres (am 31. Dezember) zurückgesetzt
* `erp` (optional, boolesch): Wenn das `rp`-Argument eine Zahl ist, bestimmt dieses Argument, ob die Gültigkeit der Besuchsnummer verlängert werden soll. Wenn der Wert auf `true` gesetzt wird, wird der Besuchsnummernzähler durch nachfolgende Treffer auf Ihrer Site zurückgesetzt. Wenn der Wert auf `false` gesetzt ist, werden nachfolgende Treffer auf Ihrer Site nicht verlängert, wenn der Zähler für die Besuchsnummer zurückgesetzt wird. Die Standardeinstellung ist `true`. Dieses Argument ist nicht gültig, wenn das `rp` -Argument eine Zeichenfolge ist.

Die Besuchsnummer wird erhöht, sobald der Besucher nach 30 Minuten Inaktivität zu Ihrer Site zurückkehrt. Der Aufruf dieser Methode gibt eine Ganzzahl zurück, die die aktuelle Besuchsnummer des Besuchers darstellt.

### `p_fo` (Nur Seite zuerst)

Ermöglicht die Einrichtung und Konfiguration des [`p_fo` Analytics-Plug-ins](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/p-fo.html). Das Datenelement `p_fo` ist ein Dienstprogramm, das prüft, ob ein bestimmtes JavaScript-Objekt vorhanden ist. Wenn das Objekt nicht vorhanden ist, erstellt das Plug-in das Objekt und gibt `true` zurück. Wenn das JavaScript-Objekt bereits auf der Seite vorhanden ist, wird `false` zurückgegeben. Dieses Datenelement ist nützlich, um Code genau einmal auf einer Seite auszuführen.

Das Datenelement `p_fo` verwendet die folgenden Argumente:

* `on` (erforderlich, Zeichenfolge): Der Name des JavaScript-Objekts, das vom Datenelement erstellt wird, wenn das Objekt noch nicht auf der Seite vorhanden ist.

Wenn das Objekt noch nicht vorhanden ist, gibt diese Methode `true` zurück und erstellt das Objekt. Wenn das Objekt bereits vorhanden ist, gibt diese Methode `false` zurück.
