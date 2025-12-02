---
title: Common Web SDK Plugins-Erweiterung - Übersicht
description: Machen Sie sich mit der Tag-Erweiterung „Common Web SDK Plugins“ in Adobe Experience Platform vertraut.
exl-id: 6052603b-1537-4dc7-9278-969d892ca15b
source-git-commit: 2e39a7809049c199d4778a0e17eb9e0f3b1d9775
workflow-type: tm+mt
source-wordcount: '2063'
ht-degree: 0%

---

# Common Web SDK Plugins-Erweiterung - Übersicht

>[!IMPORTANT]
>
>Die Erweiterung ist für die Verwendung mit der Adobe Experience Platform Web SDK-Erweiterung vorgesehen. Informationen zur Version, die mit AppMeasurement verwendet werden soll, finden Sie in der Übersicht über die [Common Analytics Plugins-Erweiterung](../plugins/overview.md).

In diesem Dokument wird beschrieben, wie Sie die Tag-Erweiterung „Web SDK Plugins“ konfigurieren und zur Erweiterung der [Adobe Experience Platform Web SDK-Erweiterung“ ](../web-sdk/overview.md).

## Konfigurieren der Common Web SDK Plugins-Erweiterung

Dieser Abschnitt enthält eine Referenz für die Optionen, die bei der Konfiguration der Web SDK Plugins-Erweiterung verfügbar sind.

>[!IMPORTANT]
>
>Die Common Web SDK Plugins-Erweiterung soll die Adobe Experience Platform Web SDK-Erweiterung erweitern. Sie muss jedoch nicht installiert sein, damit die Erweiterung erwartungsgemäß funktioniert.

## Hinzufügen von Plug-ins zur Adobe Experience Platform Web SDK-Erweiterung

Außer mithilfe der folgenden nativen Datenelemente, die von der Common Web SDK Plugins-Erweiterung bereitgestellt werden, ist keine Konfiguration erforderlich, um ein Plug-in zu initialisieren oder zu Ihrer Bibliothek hinzuzufügen:

* [`getAndPersistValue`](web-sdk-plugins.md#getandpersistvalue)
* [`getGeoCoordinates`](#getgeocoordinates)
* [`getNewRepeat`](#getnewrepeat)
* [`getPageName`](#getpagename)
* [`getPreviousValue`](#getpreviousvalue)
* [`getQueryParam`](#getqueryparam)
* [`getTimeParting`](#gettimeparting)
* [`getTimeSinceLastVisit`](#gettimesincelastvisit)
* [`getValOnce`](#getvalonce)
* [`getVisitDuration`](#getvisitduration)
* [`getVisitNum`](#getvisitnum)
* [`p_fo`](#p_fo-page-first-only)

[//]: # (- [ ] Add links to plugin pages within the data elements below)

### `getAndPersistValue`

>[!IMPORTANT]
>
>Dieses Datenelement setzt Cookies und ermöglicht die Speicherung benutzergenerierter Werte in Cookies. Weitere Informationen finden Sie in der Plug-in-spezifischen Dokumentation .

Ermöglicht die Einrichtung und Konfiguration des [`getAndPersistValue` Analytics-Plug-ins](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getandpersistvalue.html). Das `getAndPersistValue` Datenelement speichert einen Wert in einem Cookie, der später während eines Besuchs abgerufen werden kann.

Das `getAndPersistValue` Datenelement stellt die folgenden Argumente bereit:

* `vtp` (erforderlich): Der Wert, der von Seite zu Seite beibehalten werden soll
* `cn` (optional): Der Name des Cookies, in dem der Wert gespeichert werden soll. Wenn dieses Argument nicht festgelegt ist, heißt das Cookie `"s_gapv"`
* `ex` (optional): Die Anzahl der Tage vor Ablauf des Cookies. Wenn dieses Argument `0` oder nicht festgelegt ist, läuft das Cookie am Ende des Besuchs ab (30 Minuten ohne Aktivität).

Wenn die Variable im `vtp` festgelegt ist, legt das Datenelement das Cookie fest und gibt dann den Cookie-Wert zurück. Wenn die Variable im `vtp` nicht festgelegt ist, gibt das Datenelement nur den Cookie-Wert zurück.

### `getGeoCoordinates`

>[!IMPORTANT]
>
>Dieses Plug-in erfordert Standortzugriff auf dem Client, löst jedoch keine Ausnahme aus, wenn es dies nicht bekommt.

Ermöglicht die Einrichtung und Konfiguration des [`getGeoCoordinates` Analytics-Plug-ins](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getgeocoordinates.html). Das `getGeoCoordinates` Datenelement erfasst den Breiten- und Längengrad der Geräte von Besuchern.

Das `getGeoCoordinates` Datenelement verwendet keine Argumente. Gibt einen der folgenden Werte zurück:

* `"geo coordinates not available"`: Für Geräte, für die zum Zeitpunkt der Ausführung des Plug-ins keine Standortdaten verfügbar sind. Dieser Wert ist beim ersten Treffer des Besuchs häufig, insbesondere wenn Besucher zum ersten Mal ihre Zustimmung zum Tracking ihres Standorts geben müssen.
* `"error retrieving geo coordinates"`: Wenn das Plug-in beim Versuch, den Speicherort des Geräts abzurufen, auf Fehler stößt
* `"latitude=[LATITUDE] | longtitude=[LONGITUDE]"`: Dabei sind `[LATITUDE]/[LONGITUDE]` der Breiten- bzw. Längengrad

### `getNewRepeat`

>[!IMPORTANT]
>
>Dieses Datenelement setzt Cookies. Weitere Informationen finden Sie in der Plug-in-spezifischen Dokumentation .

Ermöglicht die Einrichtung und Konfiguration des [`getNewRepeat` Analytics-Plug-ins](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getnewrepeat.html). Das `getNewRepeat` Datenelement bestimmt, ob ein Besucher der Website ein neuer Besucher oder ein wiederholter Besucher innerhalb einer gewünschten Anzahl von Tagen ist.

Das `getNewRepeat` Datenelement verwendet die folgenden Argumente:

* `d` (Ganzzahl, optional): Die Mindestanzahl von Tagen, die zwischen Besuchen erforderlich ist, um Besucher auf `"New"` zurückzusetzen. Wenn dieses Argument nicht festgelegt ist, ist es standardmäßig auf 30 Tage eingestellt.

Dieses Datenelement gibt den Wert von `"New"` zurück, wenn das vom Datenelement eingestellte Cookie nicht vorhanden oder abgelaufen ist. Gibt den Wert von `"Repeat"` zurück, wenn das vom Datenelement eingestellte Cookie vorhanden ist und die Zeit seit dem aktuellen Treffer und die im Cookie festgelegte Zeit länger als 30 Minuten sind. Diese Methode gibt denselben Wert für einen gesamten Besuch zurück.

### `getPageName`

Ermöglicht die Einrichtung und Konfiguration des [`getPageName` Analytics-Plug-ins](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getpagename.html). Das `getPageName` Datenelement erstellt eine leicht lesbare, benutzerfreundlich formatierte Version der aktuellen URL.

Das `getPageName` Datenelement verwendet die folgenden Argumente:

* `si` (optional, Zeichenfolge): Eine ID, die am Anfang der Zeichenfolge eingefügt wird, die die ID der Site darstellt. Dieser Wert kann entweder eine numerische ID oder ein benutzerfreundlicher Name sein. Ist dies nicht festgelegt, wird standardmäßig die aktuelle Domain verwendet.
* `qv` (optional, Zeichenfolge): Eine kommagetrennte Liste von Abfragezeichenfolgenparametern, die der Zeichenfolge hinzugefügt werden, wenn sie sich in der URL befinden
* `hv` (optional, Zeichenfolge): Eine kommagetrennte Liste von Parametern, die im URL-Hash gefunden wurden und die, wenn sie sich in der URL befinden, zur Zeichenfolge hinzugefügt werden
* `de` (optional, Zeichenfolge): Das Trennzeichen, um einzelne Teile der Zeichenfolge aufzuteilen. Standardmäßig ist eine Pipe (`|`) eingestellt.

Das Datenelement gibt eine Zeichenfolge zurück, die eine benutzerfreundlich formatierte Version der URL enthält. Diese Zeichenfolge wird normalerweise der `pageName`-Variablen zugewiesen, kann aber auch in anderen Variablen verwendet werden.

### `getPreviousValue`

>[!IMPORTANT]
>
>Dieses Datenelement setzt Cookies und ermöglicht die Speicherung benutzergenerierter Werte in Cookies. Weitere Informationen finden Sie in der Plug-in-spezifischen Dokumentation .

Ermöglicht die Einrichtung und Konfiguration des [`getPreviousValue` Analytics-Plug-ins](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getpreviousvalue.html). Das `getPreviousValue` Datenelement legt eine Variable auf einen Wert fest, der bei einem vorherigen Treffer festgelegt wurde.

Das `getPreviousValue` Datenelement verwendet die folgenden Argumente:

* `v` (Zeichenfolge, erforderlich): Die Variable, deren Wert an die nächste Bildanforderung übergeben werden soll. Eine häufig verwendete Variable wird zum Abrufen des vorherigen Seitenwerts `s.pageName`.
* `c` (Zeichenfolge, optional): Der Name des Cookies, in dem der Wert gespeichert wird.  Wenn dieses Argument nicht festgelegt ist, wird standardmäßig `"s_gpv"` verwendet.

Beim Aufruf dieses Datenelements wird der im Cookie enthaltene Zeichenfolgenwert zurückgegeben. Das Plug-in setzt dann den Cookie-Ablauf zurück und weist ihm den Variablenwert aus dem `v` Argument zu. Das Cookie läuft nach 30 Minuten Inaktivität ab.

### `getQueryParam`

Ermöglicht die Einrichtung und Konfiguration des [`getQueryParam` Analytics-Plug-ins](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getqueryparam.html). Das `getQueryParam` Datenelement extrahiert den Wert jedes Abfragezeichenfolgenparameters, der in einer URL enthalten ist. Dies ist nützlich, um Kampagnen-Codes sowohl intern als auch extern aus Landingpage-URLs zu extrahieren. Dies ist auch nützlich, wenn Suchbegriffe oder andere Abfragezeichenfolgen-Parameter extrahiert werden. Dieses Datenelement bietet robuste Funktionen beim Analysieren komplexer URLs, einschließlich Hashes und URLs mit mehreren Abfragezeichenfolgen-Parametern.

Das `getQueryParam` Datenelement verwendet die folgenden Argumente:

* `qsp` (erforderlich): Eine kommagetrennte Liste von Abfragezeichenfolgen-Parametern, nach denen in der URL gesucht werden soll. Dabei wird nicht zwischen Groß- und Kleinschreibung unterschieden.
* `de` (optional): Das Trennzeichen, das verwendet werden soll, wenn mehrere Abfragezeichenfolgenparameter übereinstimmen. Standardmäßig ist eine leere Zeichenfolge.
* `url` (optional): Eine benutzerdefinierte URL, Zeichenfolge oder Variable, aus der die Parameterwerte der Abfragezeichenfolge extrahiert werden sollen. Die Standardeinstellung ist `window.location`.

Der Aufruf dieses Datenelements gibt einen Wert zurück, der von den oben genannten Argumenten und der URL abhängt:

* Wenn kein übereinstimmender Abfragezeichenfolgen-Parameter gefunden wird, gibt die Methode eine leere Zeichenfolge zurück.
* Wenn ein übereinstimmender Abfragezeichenfolgen-Parameter gefunden wird, gibt die Methode den Parameterwert der Abfragezeichenfolge zurück.
* Wenn ein übereinstimmender Abfragezeichenfolgen-Parameter gefunden wird, der Wert jedoch leer ist, gibt die Methode `true` zurück.
* Wenn mehrere übereinstimmende Abfragezeichenfolgen-Parameter gefunden werden, gibt die Methode eine Zeichenfolge zurück, bei der jeder Parameterwert durch die Zeichenfolge im `de`-Argument getrennt wird.

### `getTimeParting`

Ermöglicht die Einrichtung und Konfiguration des [`getTimeParting` Analytics-Plug-ins](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/gettimeparting.html). Das `getTimeParting` Datenelement erfasst die Details des Zeitpunkts, zu dem eine messbare Aktivität auf Ihrer Site stattfindet. Dieses Datenelement ist nützlich, wenn Sie Metriken nach einer wiederholbaren Zeitteilung über einen bestimmten Datumsbereich aufschlüsseln möchten. Sie können beispielsweise die Konversionsraten zwischen zwei verschiedenen Wochentagen vergleichen, z. B. alle Sonntage und alle Donnerstage. Sie können auch Zeiträume des Tages vergleichen, z. B. alle Vormittage und alle Abende.

Das `getTimeParting` Datenelement verwendet das folgende Argument:

`t` (optional, aber empfohlen, Zeichenfolge): Der Name der Zeitzone, in die die Ortszeit des Besuchers konvertiert werden soll.  Die Standardeinstellung ist UTC/GMT-Zeit. Siehe die [Liste der Zeitzonen der TZ-Datenbank](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) auf Wikipedia für eine vollständige Liste der gültigen Werte.

Zu den gängigen gültigen Werten gehören:

* `"America/New_York"` für Eastern Time
* `"America/Chicago"` für Central Time
* `"America/Denver"` für Mountain Time
* `"America/Los_Angeles"` für Pacific Time

Der Aufruf dieses Datenelements gibt eine Zeichenfolge zurück, die die folgenden durch einen senkrechten Strich (`|`) getrennten Zeichen enthält:

* Das aktuelle Jahr
* Der aktuelle Monat
* Der Tag des Monats
* Der Wochentag
* Die aktuelle Zeit (AM/PM)

### `getTimeSinceLastVisit`

>[!IMPORTANT]
>
>Dieses Datenelement setzt Cookies. Weitere Informationen finden Sie in der Plug-in-spezifischen Dokumentation .

Ermöglicht die Einrichtung und Konfiguration des [`getTimeSinceLastVisit` Analytics-Plug-ins](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/gettimesincelastvisit.html). Das `getTimeSinceLastVisit` Datenelement verfolgt, wie lange ein Besucher nach seinem letzten Besuch gebraucht hat, um zu Ihrer Site zurückzukehren.

Das `getTimeSinceLastVisit` Datenelement verwendet keine Argumente. Gibt die Zeit zurück, die seit der letzte Besuch der Website verstrichen ist, und wird im folgenden Format in Buckets zusammengefasst:

* Die Zeit zwischen 30 Minuten und einer Stunde seit dem letzten Besuch wird auf den nächsten halben Minuten-Benchmark eingestellt. Beispiel: `"30.5 minutes"`, `"53 minutes"`
* Die Zeit zwischen einer Stunde und einem Tag wird auf den nächsten Viertelstunden-Benchmark gerundet. Beispiel: `"2.25 hours"`, `"7.5 hours"`
* Zeit, die länger als ein Tag ist, wird auf den nächsten Tag-Benchmark gerundet. Beispiel: `"1 day"`, `"3 days"`, `"9 days"`, `"372 days"`
* Wenn ein Besucher vor noch nicht war oder die verstrichene Zeit länger als zwei Jahre ist, wird der Wert auf `"New Visitor"` gesetzt.

### `getValOnce`

>[!IMPORTANT]
>
>Dieses Datenelement setzt Cookies und ermöglicht die Speicherung benutzergenerierter Werte in Cookies. Weitere Informationen finden Sie in der Plug-in-spezifischen Dokumentation .

Ermöglicht die Einrichtung und Konfiguration des [`getValOnce` Analytics-Plug-ins](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvalonce.html). Das `getValOnce`-Datenelement verhindert, dass eine Variable mehrmals auf denselben Wert gesetzt wird.

Das `getValOnce` Datenelement verwendet die folgenden Argumente:

* `vtc` (erforderlich, Zeichenfolge): Die Variable, die überprüft werden soll, ob sie gerade zuvor auf einen identischen Wert festgelegt wurde
* `cn` (optional, Zeichenfolge): Der Name des Cookies, das den zu überprüfenden Wert enthält. Standardwert ist `"s_gvo"`
* `et` (optional, Ganzzahl): Der Ablauf des Cookies in Tagen (oder Minuten, je nach `ep`). Die Standardeinstellung ist `0` und läuft am Ende der Browser-Sitzung ab
* `ep` (optional, Zeichenfolge): Legen Sie dieses Argument nur fest, wenn auch das `et` festgelegt ist. Legen Sie dieses Argument auf `"m"` fest, wenn das `et`-Argument in Minuten anstatt in Tagen ablaufen soll. Die Standardeinstellung ist `"d"`, wodurch das `et` in Tagen festgelegt wird.

Wenn das `vtc` Argument und der Cookie-Wert übereinstimmen, gibt diese Methode eine leere Zeichenfolge zurück. Wenn das `vtc` Argument und der Cookie-Wert nicht übereinstimmen, gibt die Methode das `vtc` Argument als Zeichenfolge zurück.

### `getVisitDuration`

>[!IMPORTANT]
>
>Dieses Datenelement setzt Cookies. Weitere Informationen finden Sie in der Plug-in-spezifischen Dokumentation .

Ermöglicht die Einrichtung und Konfiguration des [`getVisitDuration` Analytics-Plug-ins](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvisitduration.html). Das `getVisitDuration` Datenelement verfolgt die Zeit in Minuten, die der Besucher bis zu diesem Zeitpunkt auf der Website war.

Das `getVisitDuration` Datenelement verwendet keine Argumente. Gibt einen der folgenden Werte zurück:

* `"first hit of visit"`
* `"less than a minute"`
* `"1 minute"`
* `"[x] minutes"` (wobei `[x]` die Anzahl der Minuten ist, die seit der Landung des Besuchers auf der Website vergangen sind)

### `getVisitNum`

>[!IMPORTANT]
>
>Dieses Datenelement setzt Cookies. Weitere Informationen finden Sie in der Plug-in-spezifischen Dokumentation .

Ermöglicht die Einrichtung und Konfiguration des [`getVisitNum` Analytics-Plug-ins](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvisitnum.html). Das `getVisitNum` Datenelement gibt die Besuchsnummer für alle Besucher zurück, die innerhalb der gewünschten Anzahl von Tagen auf die Website kommen.

Das `getVisitNum` Datenelement verwendet die folgenden Argumente:

* `rp` (optional, Ganzzahl ODER Zeichenfolge): Die Anzahl der Tage vor dem Zurücksetzen des Zählers für die Besuchsanzahl.  Die Standardeinstellung ist `365`, wenn nicht festgelegt.
   * Wenn dieses Argument `"w"` wird, wird der Zähler am Ende der Woche (diesen Samstag um 23 :59) zurückgesetzt
   * Wenn dieses Argument `"m"` wird, wird der Zähler am Ende des Monats (dem letzten Tag dieses Monats) zurückgesetzt
   * Wenn dieses Argument `"y"` wird, wird der Zähler am Ende des Jahres (31. Dezember) zurückgesetzt
* `erp` (optional, boolesch): Wenn das `rp` Argument eine Zahl ist, bestimmt dieses Argument, ob der Ablauf der Besuchsnummer verlängert werden soll. Wenn auf `true` festgelegt, wird bei nachfolgenden Treffern auf Ihrer Site der Besuchsnummernzähler zurückgesetzt. Wenn auf `false` festgelegt, werden nachfolgende Treffer auf Ihrer Site nicht verlängert, wenn der Zähler für die Besuchsnummer zurückgesetzt wird. Die Standardeinstellung ist `true`. Dieses Argument ist nicht gültig, wenn das `rp` Argument eine Zeichenfolge ist.

Die Besuchsnummer erhöht sich immer dann, wenn der Besucher nach 30 Minuten Inaktivität zu Ihrer Site zurückkehrt. Der Aufruf dieser Methode gibt eine Ganzzahl zurück, die die aktuelle Besuchsnummer des Besuchers darstellt.

### `p_fo` (nur Seite zuerst)

Ermöglicht die Einrichtung und Konfiguration des [`p_fo` Analytics-Plug-ins](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/p-fo.html). Das `p_fo` Datenelement ist ein Dienstprogramm, das überprüft, ob ein bestimmtes JavaScript-Objekt vorhanden ist. Wenn das Objekt nicht vorhanden ist, erstellt das Plug-in das Objekt und gibt `true` zurück. Wenn das JavaScript-Objekt bereits auf der Seite vorhanden ist, wird `false` zurückgegeben. Dieses Datenelement ist nützlich, um Code genau einmal auf einer Seite auszuführen.

Das `p_fo` Datenelement verwendet die folgenden Argumente:

* `on` (erforderlich, Zeichenfolge): Der Name des JavaScript-Objekts, das das Datenelement erstellt, wenn das Objekt noch nicht auf der Seite vorhanden ist.

Wenn das Objekt noch nicht vorhanden ist, gibt diese Methode `true` zurück und erstellt das -Objekt. Wenn das Objekt bereits vorhanden ist, gibt diese Methode `false` zurück.
