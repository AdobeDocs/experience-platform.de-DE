---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Analytics-Zuordnungsfelder
topic: overview
translation-type: tm+mt
source-git-commit: 53fb7ea201ed9361584d24c8bd2ad10edd9f3975
workflow-type: tm+mt
source-wordcount: '3328'
ht-degree: 14%

---


# Analytics-Zuordnungsfelder

Mit Adobe Experience Platform können Sie Adobe Analytics-Daten über den Analytics Data Connector (ADC) erfassen. Einige der über ADC erfassten Daten können direkt aus Analytics-Feldern Experience Data Model (XDM)-Feldern zugeordnet werden, während andere Daten Transformationen und spezifische Funktionen erfordern, um erfolgreich zugeordnet zu werden.

![](../images/analytics-data-experience-platform.png)

## Direkte Zuordnungsfelder

Auswahlfelder werden direkt von Adobe Analytics zum Experience Data Model (XDM) zugeordnet.

Die folgende Tabelle enthält Spalten, die den Namen des Analytics-Felds (*Analytics-Feld*), das entsprechende XDM-Feld (*XDM-Feld*) und dessen Typ (*XDM-Typ*) sowie eine Beschreibung des Felds (*Beschreibung*) anzeigen.

>[!NOTE] Bitte blättern Sie nach links/rechts, um den gesamten Tabelleninhalt Ansicht.

| Analysefeld | XDM-Feld | XDM-Typ | Beschreibung |
| --------------- | --------- | -------- | ---------- |
| m_evar1 - m_evar250 | _experience.analytics.customDimensions.eVars.eVar1 - _experience.analytics.customDimensions.eVars.eVar250 | Zeichenfolge | Eine benutzerdefinierte Variable, die zwischen 1 und 250 liegen kann. Jede Organisation verwendet diese benutzerspezifischen eVars unterschiedlich. |
| m_prop1 - m_prop75 | _experience.analytics.customDimensions.props.prop1 - _experience.analytics.customDimensions.props.prop75 | Zeichenfolge | Benutzerspezifische Traffic-Variablen, die zwischen 1 und 75 liegen können. |
| m_browser | _experience.analytics.Umgebung.browserID | Ganzzahl | Die Nummer-ID des Browsers. |
| m_browser_height | environment.browserDetails.viewportHeight | Ganzzahl | Die Höhe des Browsers in Pixel. |
| m_browser_width | environment.browserDetails.viewportWidth | Ganzzahl | Die Breite des Browsers in Pixel. |
| m_Kampagne | marketing.trackingCode | Zeichenfolge | Die in der Dimension &quot;Rückverfolgungscode&quot;verwendete Variable. |
| m_Kanal | web.webPageDetails.siteSection | Zeichenfolge | Die in der Dimension &quot;Sitebereiche&quot;verwendete Variable. |
| m_domain | environment.domain | Zeichenfolge | Die in der Dimension &quot;Domäne&quot;verwendete Variable. Dies erfolgt auf der Grundlage des Internet-Dienstleisters (ISP) des Benutzers. |
| m_geo_city | placeContext.geo.city | Zeichenfolge | Der Name der Stadt des Treffers. Dies basiert auf der IP-Adresse des Treffers. |
| m_geo_dma | placeContext.geo.dmaID | Ganzzahl | Die numerische ID des demografischen Bereichs für den Treffer. Dies basiert auf der IP-Adresse des Treffers. |
| m_geo_region | placeContext.geo.stateProvince | Zeichenfolge | Der Name des Bundesstaates oder der Region des Treffers. Dies basiert auf der IP-Adresse des Treffers. |
| m_geo_zip | placeContext.geo.postalCode | Zeichenfolge | Die Postleitzahl des Treffers. Dies basiert auf der IP-Adresse des Treffers. |
| m_keywords | search.keywords | Zeichenfolge | Die in der Suchbegriffdimension verwendete Variable. |
| m_os | _experience.analytics.Umgebung.operatingSystemID | Ganzzahl | Die numerische ID, die das Betriebssystem des Besuchers darstellt. Dies basiert auf der Spalte user_agent. |
| m_page_url | web.webPageDetails.URL | Zeichenfolge | Die URL des Seitentreffers. |
| m_pagename_no_url | web.webPageDetails.</span>name | Zeichenfolge | Eine Variable, mit der die Dimension &quot;Seiten&quot;gefüllt wird. |
| m_Werber | web.webReferrer.URL | Zeichenfolge | Die Seiten-URL der vorherigen Seite. |
| m_search_page_num | search.pageDepth | Ganzzahl | Wird von der Dimension „Rangansicht aller Suchseiten“ verwendet. Gibt an, auf welcher Seite der Suchergebnisse Ihre Site angezeigt wurde, ehe der Benutzer sich zu Ihrer Site durchgeklickt hat. |
| m_state | _experience.analytics.customDimensions.stateProvince | Zeichenfolge | Without context I&#39;m afraid I can&#39;t assess which version is the correct one. |
| m_user_server | web.webPageDetails.server | Zeichenfolge | Eine Variable, die in der Serverdimension verwendet wird. |
| m_zip | _experience.analytics.customDimensions.postalCode | Zeichenfolge | Eine Variable, mit der die Dimension &quot;Postleitzahl&quot;gefüllt wird. |
| accept_language | environment.browserDetails.acceptLanguage | Zeichenfolge | Liste aller zulässigen Sprachen, wie im Accept-Language HTTP-Header angegeben. |
| homepage | web.webPageDetails.isHomePage | Boolescher Wert | Wird nicht mehr verwendet. Wird angezeigt, wenn die aktuelle URL die Browser-Startseite ist. |
| ipv6 | environment.ipV6 | Zeichenfolge |
| j_jscript | environment.browserDetails.javaScriptVersion | Zeichenfolge | Die vom Browser unterstützte JavaScript-Version. |
| user_agent | environment.browserDetails.userAgent | Zeichenfolge | Die Benutzeragenten-Zeichenfolge, die im HTTP-Header gesendet wird. |
| mobileappid | application.</span>name | Zeichenfolge | Die mobile App-ID, die im folgenden Format gespeichert wird: `[AppName][BundleVersion]`. |
| mobiledevice | device.model | Zeichenfolge | Der Name des Mobilgeräts. Unter iOS als kommagetrennte 2-Ziffern-Zeichenfolge gespeichert. Die erste Zahl steht für die Gerätegenerierung und die zweite Zahl für die Gerätefamilie. |
| pointofinterest | placeContext.POIinteraction.POIDetail.</span>name | Zeichenfolge | Wird von Mobildiensten verwendet. Stellt den Interessenbereich dar. |
| pointofinterestdistance | placeContext.POIinteraction.POIDetail.geoInteractionDetails.distanceToCenter | number | Wird von Mobildiensten verwendet. Stellt den Zielpunkt-Abstand dar. |
| mobileplaceaccuracy | placeContext.POIinteraction.POIDetail.geoInteractionDetails.deviceGeoAccuracy | number | Erfasst mit der Kontextdatenvariablen a.loc.acc. Gibt die Genauigkeit des GPS in Metern zum Erfassungszeitpunkt an. |
| mobileplacecategory | placeContext.POIinteraction.POIDetail.category | Zeichenfolge | Wird mit der Kontextdatenvariablen a.loc.category erfasst. Beschreibt die Kategorie eines bestimmten Orts. |
| mobileplaceid | placeContext.POIinteraction.POIDetail.POIID | Zeichenfolge | Wird aus der Kontextdatenvariablen a.loc.id erfasst. Kennung für einen bestimmten Zielpunkt. |
| video | media.mediaTimed.primaryAssetReference._id | Zeichenfolge | Der Name des Videos. |
| videoad | advertising.adAssetReference._id | Zeichenfolge | Bezeichner des Anzeigenassets. |
| videocontenttype | media.mediaTimed.primaryAssetViewDetails.broadcastContentType | Zeichenfolge | Der Videoinhalt-Typ. Für alle Video-Ansichten ist dies automatisch auf &quot;Video&quot;eingestellt. |
| videoadpod | advertising.adAssetViewDetails.adBreak._id | Zeichenfolge | Der Pod, in dem sich die Videoanzeige befindet. |
| videoadinpod | advertising.adAssetViewDetails.index | Ganzzahl | Die Position der Videoanzeige im Pod. |
| videoplayername | media.mediaTimed.primaryAssetViewDetails.playerName | Zeichenfolge | Der Name des Videoplayers. |
| videochannel | media.mediaTimed.primaryAssetViewDetails.broadcastChannel | Zeichenfolge | Der Video-Kanal. |
| videoadplayername | advertising.adAssetViewDetails.playerName | Zeichenfolge | Der Name des Videoanzeigenplayers. |
| videochapter | media.mediaTimed.mediaChapter.chapterAssetReference._id | Zeichenfolge | Name des Kapitels &quot;Video&quot; |
| videoname | media.mediaTimed.primaryAssetReference._dc.title | Zeichenfolge | Der Videoname. |
| videoadname | advertising.adAssetReference._dc.title | Zeichenfolge | Der Name der Videoanzeige. |
| videoshow | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Series._iptc4xmpExt.Name | Zeichenfolge | Videosendung. |
| videoseason | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Season._iptc4xmpExt.Name | Zeichenfolge | Videosaison. |
| videoepisode | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Episode._iptc4xmpExt.Name | Zeichenfolge | Videoepisode. |
| videonetwork | media.mediaTimed.primaryAssetViewDetails.broadcastNetwork | Zeichenfolge | Videonetzwerk. |
| videoshowtype | media.mediaTimed.primaryAssetReference.showType | Zeichenfolge | Typ der Videosendung. |
| videoadload | media.mediaTimed.primaryAssetViewDetails.adLoadType | Zeichenfolge | Ladeaufforderungen der Videoanzeige. |
| videofeedtype | media.mediaTimed.primaryAssetViewDetails.sourceFeed | Zeichenfolge | Video-Feed-Typ. |
| mobilebeaconmajor | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.beaconMajor | number | Mobile Services – Haupt-Beacon. |
| mobilebeaconminor | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.beaconMinor | number | Mobile Services – Neben-Beacon. |
| mobilebeaconuuid | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.proximityUUID | Zeichenfolge | Mobile Services-Beacon UUID. |
| videosessionid | media.mediaTimed.primaryAssetViewDetails._id | Zeichenfolge | Videositzungs-ID. |
| videogenre | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Genre | array | Video-Genre. | {title (Objekt), description (Objekt), type (Objekt), meta:xdmType (Objekt), items (string), meta:xdmField (Objekt)} |
| mobileinstalls | application.firstLaunches | Objekt | Dies wird beim ersten Ausführen nach der Installation oder Neuinstallation ausgelöst | {id (Zeichenfolge), Wert (Zahl)} |
| mobileupgrades | application.upgrades | Objekt | Gibt die Anzahl der App-Aktualisierungen an. Wird beim ersten Ausführen nach der Aktualisierung oder bei jeder Änderung der Versionsnummer ausgelöst. | {id (Zeichenfolge), Wert (Zahl)} |
| mobilelaunches | application.launches | Objekt | Die Häufigkeit, mit der die App gestartet wurde. | {id (Zeichenfolge), Wert (Zahl)} |
| mobilecrashes | application.crashes | Objekt | <!-- MISSING --> | {id (Zeichenfolge), Wert (Zahl)} |
| mobilemessageclicks | directMarketing.clicks | Objekt | <!-- MISSING --> | {id (Zeichenfolge), Wert (Zahl)} |
| mobileplaceentry | placeContext.POIinteraction.poiEntries | Objekt | <!-- MISSING --> | {id (Zeichenfolge), Wert (Zahl)} |
| mobileplaceexit | placeContext.POIinteraction.poiExits | Objekt | <!-- MISSING --> | {id (Zeichenfolge), Wert (Zahl)} |
| videotime | media.mediaTimed.timePlayed | Objekt | <!-- MISSING --> | {id (Zeichenfolge), Wert (Zahl)} |
| videostart | media.mediaTimed.impressions | Objekt | <!-- MISSING --> | {id (Zeichenfolge), Wert (Zahl)} |
| videocomplete | media.mediaTimed.completes | Objekt | <!-- MISSING --> | {id (Zeichenfolge), Wert (Zahl)} |
| videosegmentviews | media.mediaTimed.mediaSegmentViews | Objekt | <!-- MISSING --> | {id (Zeichenfolge), Wert (Zahl)} |
| videoadstart | advertising.impressions | Objekt | <!-- MISSING --> | {id (Zeichenfolge), Wert (Zahl)} |
| videoadcomplete | advertising.completes | Objekt | <!-- MISSING --> | {id (Zeichenfolge), Wert (Zahl)} |
| videoadtime | advertising.timePlayed | Objekt | <!-- MISSING --> | {id (Zeichenfolge), Wert (Zahl)} |
| videochapterstart | media.mediaTimed.mediaChapter.impressions | Objekt | <!-- MISSING --> | {id (Zeichenfolge), Wert (Zahl)} |
| videochaptercomplete | media.mediaTimed.mediaChapter.completes | Objekt | <!-- MISSING --> | {id (Zeichenfolge), Wert (Zahl)} |
| videochaptertime | media.mediaTimed.mediaChapter.timePlayed | Objekt | <!-- MISSING --> | {id (Zeichenfolge), Wert (Zahl)} |
| videoplay | media.mediaTimed.starts | Objekt | <!-- MISSING --> | {id (Zeichenfolge), Wert (Zahl)} |
| videototaltime | media.mediaTimed.totalTimePlayed | Objekt | <!-- MISSING --> | {id (Zeichenfolge), Wert (Zahl)} |
| videoqoetimetostart | media.mediaTimed.primaryAssetViewDetails.qoe.timeToStart | Objekt | Die Zeit bis zum Beginn der Videoqualität. | {id (Zeichenfolge), Wert (Zahl)} |
| videoqoedropbeforestart | media.mediaTimed.dropBeforeStarts | Objekt | <!-- MISSING --> | {id (Zeichenfolge), Wert (Zahl)} |
| videoqoebuffercount | media.mediaTimed.primaryAssetViewDetails.qoe.buffers | Objekt | Anzahl der Videopuffer | {id (Zeichenfolge), Wert (Zahl)} |
| videoqoebuffertime | media.mediaTimed.primaryAssetViewDetails.qoe.bufferTime | Objekt | Videoqualitätspufferzeit | {id (Zeichenfolge), Wert (Zahl)} |
| videoqoebitratechangecount | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateChanges | Objekt | Anzahl der Videoqualitätsänderungen | {id (Zeichenfolge), Wert (Zahl)} |
| videoqoebitrateaverage | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateAverage | Objekt | Durchschnittliche Bitrate der Videoqualität | {id (Zeichenfolge), Wert (Zahl)} |
| videoqoeerrorcount | media.mediaTimed.primaryAssetViewDetails.qoe.errors | Objekt | Anzahl der Videoqualitätsfehler | {id (Zeichenfolge), Wert (Zahl)} |
| videoqoedroppedframecount | media.mediaTimed.primaryAssetViewDetails.qoe.droppedFrames | Objekt | <!-- MISSING --> | {id (Zeichenfolge), Wert (Zahl)} |
| videoprogress10 | media.mediaTimed.progress10 | Objekt | <!-- MISSING --> | {id (Zeichenfolge), Wert (Zahl)} |
| videoprogress25 | media.mediaTimed.progress25 | Objekt | <!-- MISSING --> | {id (Zeichenfolge), Wert (Zahl)} |
| videoprogress50 | media.mediaTimed.progress50 | Objekt | <!-- MISSING --> | {id (Zeichenfolge), Wert (Zahl)} |
| videoprogress75 | media.mediaTimed.progress75 | Objekt | <!-- MISSING --> | {id (Zeichenfolge), Wert (Zahl)} |
| videoprogress95 | media.mediaTimed.progress95 | Objekt | <!-- MISSING --> | {id (Zeichenfolge), Wert (Zahl)} |
| videoresume | media.mediaTimed.resumes | Objekt | <!-- MISSING --> | {id (Zeichenfolge), Wert (Zahl)} |
| videopausecount | media.mediaTimed.pauses | Objekt | <!-- MISSING --> | {id (Zeichenfolge), Wert (Zahl)} |
| videopausetime | media.mediaTimed.pauseTime | Objekt | <!-- MISSING --> | {id (Zeichenfolge), Wert (Zahl)} |
| videosecondssincelastcall | media.mediaTimed.primaryAssetViewDetails.sessionTimeout | Ganzzahl |

## Zuordnungsfelder teilen

Diese Felder verfügen über eine einzige Quelle, sind aber **mehreren** XDM-Positionen zugeordnet.

| Analysefeld | XDM-Feld | XDM-Typ | Beschreibung |
| --------------- | --------- | -------- | ---------- |
| s_resolution | device.screenWidth, device.screenHeight | Ganzzahl | Numerische ID, die die Auflösung des Bildschirms darstellt. |
| mobileosversion | Umgebung.operatingSystem, Umgebung.operatingSystemVersion | Zeichenfolge | Version des mobilen Betriebssystems. |
| videoadlength | advertising.adAssetReference._xmpDM.duration | Ganzzahl | Länge der Videoanzeige |

## Generierte Zuordnungsfelder

Die Auswahl von Feldern, die von ADC kommen, muss transformiert werden, sodass eine Logik über eine direkte Kopie von Adobe Analytics hinaus erforderlich ist, um in XDM generiert zu werden.

Die folgende Tabelle enthält Spalten, die den Namen des Analytics-Felds (*Analytics-Feld*), das entsprechende XDM-Feld (*XDM-Feld*) und dessen Typ (*XDM-Typ*) sowie eine Beschreibung des Felds (*Beschreibung*) anzeigen.

>[!NOTE] Bitte blättern Sie nach links/rechts, um den gesamten Tabelleninhalt Ansicht.

| Analysefeld | XDM-Feld | XDM-Typ | Beschreibung |
| --------------- | --------- | -------- | ----------- |
| m_prop1 - m_prop75 | _experience.analytics.customDimensions.listprops.prop1 - _experience.analytics.customDimensions.listprops.prop75 | Objekt | Benutzerspezifische Traffic-Variablen, die zwischen 1 und 75 liegen | {} |
| m_hier1 - m_hier5 | _experience.analytics.customDimensions.hierarchies.hier1 - _experience.analytics.customDimensions.hierarchy.hier5 | Objekt | Wird von Hierarchievariablen verwendet. Es enthält eine | durch Trennzeichen getrennte Liste von Werten. | {Werte (Array), Trennzeichen (Zeichenfolge)} |
| m_mvvar1 - m_mvvar3 | _experience.analytics.customDimensions.Listen.Liste1.Liste[] - _experience.analytics.customDimensions.Listen.Liste3.Liste[] | array | Liste von Variablenwerten. Enthält eine durch Trennzeichen getrennte Liste von benutzerdefinierten Werten, je nach Implementierung | {value (Zeichenfolge), key (Zeichenfolge)} |
| m_color | device.colorDepth | Ganzzahl | Die Farbtiefe-ID, die auf dem Wert der Spalte c_color basiert. |
| m_cookies | environment.browserDetails.cookiesEnabled | Boolescher Wert | Eine Variable, die in der Dimension &quot;Cookie-Unterstützung&quot;verwendet wird. |
| m_Ereignis_Liste | commerce.purchase, commerce.productViews, commerce.productListOpen, commerce.checkouts, commerce.productListAdds, commerce.productListRemoval, commerce.productListViews | Objekt | Beim Treffer ausgelöste Standard-Commerce-Ereignis | {id (Zeichenfolge), Wert (Zahl)} |
| m_Ereignis_Liste | _experience.analytics.Ereignis1to100.Ereignis1 - _experience.analytics.Ereignis1to100.Ereignis100, _experience.analytics.Ereignis101to200.Ereignis101 - _experience.analytics.Ereignis101to20 Ereignis200, _experience.analytics.Ereignis201to300.Ereignis201 - _experience.analytics.Ereignis201to300.Ereignis300, _experience.analytics.Ereignis301to400.Ereignis3 01 - _experience.analytics.Ereignis301to400.400, _experience.analytics.401to500.401 - _experience.analytics.page401to500.source500, _experience.analytics.JB501bis600.JEDE501 - _experience.analytics.JEE501bis600.JEE600, _experience.analytics.JEE601bis700.JEE601 - _experience.analytics.J66001 601to700.700, _experience.analytics.701to800.701 - _experience.analytics.JEE701to800.JEE800, _experience.analytics.J8001to8177777000000000000000 900.801 - _experience.analytics.801to900.900, _experience.analytics.901to1000.901 - _experience.analytics.901to100 0.1000 | Objekt | Benutzerspezifische Ereignis, die beim Treffer ausgelöst werden. | {id (Objekt), Wert (Objekt)} |
| m_geo_country | placeContext.geo.countryCode | Zeichenfolge | Abkürzung des Landes, aus dem der Treffer stammt, das auf dem UZ basiert. |
| m_geo_latitude | placeContext.geo._Schema.latitude | number | <!-- MISSING --> |
| m_geo_Längengrad | placeContext.geo._Schema.Längengrad | number | <!-- MISSING --> |
| m_java_enabled | environment.browserDetails.javaEnabled | Boolescher Wert | Eine Flag, die angibt, ob Java aktiviert ist. |
| m_latitude | placeContext.geo._Schema.latitude | number | <!-- MISSING --> |
| m_Längengrad | placeContext.geo._Schema.Längengrad | number | <!-- MISSING --> |
| m_page_Ereignis_var1 | web.webInteraction.URL | Zeichenfolge | Eine Variable, die nur zur Linktracking von Bildanforderungen verwendet wird. Diese Variable enthält die URL des angeklickten Downloadlinks, Exitlinks oder benutzerspezifischen Links. |
| m_page_Ereignis_var2 | web.webInteraction.name | Zeichenfolge | Eine Variable, die nur zur Linktracking von Bildanforderungen verwendet wird. Auf diese Weise wird der benutzerdefinierte Name des Links Liste, sofern er angegeben ist. |
| m_page_type | web.webPageDetails.isErrorPage | Boolescher Wert | Eine Variable, mit der die Dimension &quot;Seiten nicht gefunden&quot;gefüllt wird. Diese Variable sollte entweder leer sein oder &quot;ErrorPage&quot;enthalten. |
| m_pagename_no_url | web.webPageDetails.pageViews.value | number | Der Name der Seite (falls festgelegt). Wenn keine Seite angegeben ist, bleibt dieser Wert leer. |
| m_paid_search | search.isPaid | Boolescher Wert | Eine Flag, die festgelegt wird, wenn der Treffer mit der gebührenpflichtigen Sucherkennung übereinstimmt. |
| m_product_Liste | productListItems[].items | array | Die Liste des Produkts, die über die Variable &quot;products&quot;weitergegeben wird. | {SKU (Zeichenfolge), Quantität (Ganzzahl), priceTotal (Zahl)} |
| m_ref_type | web.webReferrer.type | Zeichenfolge | Eine numerische ID, die den Typ des Verweises für den Treffer darstellt. 1 bedeutet innerhalb Ihrer Site, 2 bedeutet andere Websites, 3 bedeutet Suchmaschinen, 4 bedeutet Festplatte, 5 bedeutet USENET, 6 bedeutet Eingegeben/Mit Lesezeichen versehen (kein Werber), 7 bedeutet E-Mail, 8 bedeutet Kein JavaScript und 9 bedeutet Social Networks. |
| m_search_engine | search.searchEngine | Zeichenfolge | Die numerische ID, die die Suchmaschine darstellt, die den Besucher auf Ihre Site verwiesen hat. |
| post_currency | commerce.order.currencyCode | Zeichenfolge | Der während der Transaktion verwendete Währungscode. |
| post_cust_hit_time_gmt | timestamp | Zeichenfolge | Dies wird nur in für Zeitstempel aktivierten Datensätzen verwendet. Dieser Zeitstempel wird basierend auf der Unix-Zeit mit dem Zeitstempel gesendet. |
| post_cust_visid | identityMap | object | Die Kunden-Besucher-ID. |
| post_cust_visid | endUserIDs._experience.aacustomid.primary | Boolescher Wert | Die Kunden-Besucher-ID. |
| post_cust_visid | endUserIDs._experience.aacustomid.Namensraum.code | Zeichenfolge | Die Kunden-Besucher-ID. |
| post_visid_high + visid_low | identityMap | object | Eine eindeutige ID für einen Besuch. |
| post_visid_high + visid_low | endUserIDs._experience.aaid.id | Zeichenfolge | Eine eindeutige ID für einen Besuch. |
| post_visid_high | endUserIDs._experience.aaid.primary | Boolescher Wert | Wird in Verbindung mit visid_low verwendet, um einen Besuch eindeutig zu identifizieren. |
| post_visid_high | endUserIDs._experience.aaid.Namensraum.code | Zeichenfolge | Wird in Verbindung mit visid_low verwendet, um einen Besuch eindeutig zu identifizieren. |
| post_visid_low | identityMap | object | Wird in Verbindung mit visid_high verwendet, um einen Besuch eindeutig zu identifizieren. |
| hit_time_gmt | receiveTimestamp | Zeichenfolge | Der Zeitstempel des Treffers, basierend auf der Unix-Zeit. |
| hitid_high + hitid_low | _id | Zeichenfolge | Eine eindeutige Kennung zur Identifizierung eines Treffers. |
| hitid_low | _id | Zeichenfolge | Wird in Verbindung mit hitid_high verwendet, um einen Treffer eindeutig zu identifizieren. |
| ip | environment.ipV4 | Zeichenfolge | Die IP-Adresse, basierend auf dem HTTP-Header der Bildanforderung. |
| j_jscript | environment.browserDetails.javaScriptEnabled | Boolescher Wert | Die verwendete JavaScript-Version. |
| mcvisid_high + mcvisid_low | identityMap | object | Die Experience Cloud-Besucher-ID. |
| mcvisid_high + mcvisid_low | endUserIDs._experience.mcid.id | Zeichenfolge | Die Experience Cloud-Besucher-ID. |
| mcvisid_high | endUserIDs._experience.mcid.primary | Boolescher Wert | Die Experience Cloud-Besucher-ID. |
| mcvisid_high | endUserIDs._experience.mcid.Namensraum.code | Zeichenfolge | Die Experience Cloud-Besucher-ID. |
| mcvisid_low | identityMap | object | Die Experience Cloud-Besucher-ID. |
| sdid_high + sdid_low | _experience.Zielgruppe.additionalDataID | Zeichenfolge | Trefferstitching-ID. Das Analysefeld sdid_high und sdid_low ist die zusätzliche Daten-ID, mit der zwei (oder mehr) eingehende Treffer zusammengeführt werden. |
| mobilebeaconproximity | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.proximity | Zeichenfolge | Mobile Services – Beacon-Nähe. |
| videochapter | media.mediaTimed.mediaChapter.chapterAssetReference._xmpDM.duration | Ganzzahl | Der Name des Videokapitels. |
| videolength | media.mediaTimed.primaryAssetReference._xmpDM.duration | Ganzzahl | Die Länge des Videos. |

## Erweiterte Zuordnungsfelder

Zur Auswahl stehende Felder (auch &quot;Postwerte&quot;genannt) sind erweiterte Transformationen erforderlich, bevor sie von Adobe Analytics-Feldern erfolgreich dem Experience Data Model (XDM) zugeordnet werden können. Die Durchführung dieser erweiterten Konvertierungen umfasst die Verwendung des Adobe Experience Platform Abfrage Service und vordefinierter Funktionen (als Adobe-definierte Funktionen bezeichnet) für die Segmentierung, Zuordnung und Deduplizierung-Duplikate.

Weitere Informationen zum Durchführen dieser Transformationen mithilfe des Abfrage Service finden Sie in der Dokumentation zu den von [Adobe definierten Funktionen](../../../../query-service/sql/adobe-defined-functions.md) .

Die folgende Tabelle enthält Spalten, die den Namen des Analytics-Felds (*Analytics-Feld*), das entsprechende XDM-Feld (*XDM-Feld*) und dessen Typ (*XDM-Typ*) sowie eine Beschreibung des Felds (*Beschreibung*) anzeigen.

>[!NOTE] Bitte blättern Sie nach links/rechts, um den gesamten Tabelleninhalt Ansicht.

| Analysefeld | XDM-Feld | XDM-Typ | Beschreibung |
| --------------- | --------- | -------- | ---------- |
| post_evar1 - post_evar250 | _experience.analytics.customDimensions.eVars.eVar1 - _experience.analytics.customDimensions.eVars.eVar250 | Zeichenfolge | Eine benutzerdefinierte Variable, die zwischen 1 und 250 liegen kann. Jede Organisation verwendet diese benutzerspezifischen eVars unterschiedlich. |
| post_prop1 - post_prop75 | _experience.analytics.customDimensions.props.prop1 - _experience.analytics.customDimensions.props.prop75 | Zeichenfolge | Benutzerspezifische Traffic-Variablen, die zwischen 1 und 75 liegen können. |
| post_browser_height | environment.browserDetails.viewportHeight | Ganzzahl | Die Höhe des Browsers in Pixel. |
| post_browser_width | environment.browserDetails.viewportWidth | Ganzzahl | Die Breite des Browsers in Pixel. |
| post_Kampagne | marketing.trackingCode | Zeichenfolge | Die in der Dimension &quot;Rückverfolgungscode&quot;verwendete Variable. |
| post_Kanal | web.webPageDetails.siteSection | Zeichenfolge | Die in der Dimension &quot;Sitebereiche&quot;verwendete Variable. |
| post_cust_visid | endUserIDs._experience.aacustomid.id | Zeichenfolge | Die benutzerdefinierte Besucher-ID, falls festgelegt. |
| post_first_hit_page_url | _experience.analytics.endUser.firstWeb.webPageDetails.URL | Zeichenfolge | Die URL der ersten Seite, die der Besucher erreicht. |
| post_first_hit_pagename | _experience.analytics.endUser.firstWeb.webPageDetails.name | Zeichenfolge | Eine Variable, die in der Dimension &quot;Ursprüngliche Entrypage&quot;verwendet wird. Der Seitenname der Entrypage des Besuchers. |
| post_keywords | search.keywords | Zeichenfolge | Die Suchbegriffe, die für den Treffer erfasst wurden. |
| post_page_url | web.webPageDetails.URL | Zeichenfolge | Die URL des Seitentreffers. |
| post_pagename_no_url | web.webPageDetails.name | Zeichenfolge | Eine Variable, mit der die Dimension &quot;Seiten&quot;gefüllt wird. |
| post_purchaseid | commerce.order.purchaseID | Zeichenfolge | Variable, die zur eindeutigen Identifizierung von Käufen verwendet wird. |
| post_Werber | web.webReferrer.URL | Zeichenfolge | Die URL der vorherigen Seite. |
| post_state | _experience.analytics.customDimensions.stateProvince | Zeichenfolge | Without context I&#39;m afraid I can&#39;t assess which version is the correct one. |
| post_user_server | web.webPageDetails.server | Zeichenfolge | Eine Variable, die in der Serverdimension verwendet wird. |
| post_zip | _experience.analytics.customDimensions.postalCode | Zeichenfolge | Eine Variable, mit der die Dimension &quot;Postleitzahl&quot;gefüllt wird. |
| browser | _experience.analytics.Umgebung.browserID | Ganzzahl | Die numerische ID des Browsers. |
| domain | environment.domain | Zeichenfolge | Die in der Dimension &quot;Domäne&quot;verwendete Variable. Dies erfolgt auf der Grundlage des Internet-Dienstleisters (ISP) des Benutzers. |
| first_hit_Werber | _experience.analytics.endUser.firstWeb.webReferrer.URL | Zeichenfolge | Die erste verweisende URL für den Besucher. |
| geo_city | placeContext.geo.city | Zeichenfolge | Der Name der Stadt des Treffers. Dies basiert auf der IP-Adresse des Treffers. |
| geo_dma | placeContext.geo.dmaID | Ganzzahl | Die numerische ID des demografischen Bereichs für den Treffer. Dies basiert auf der IP-Adresse des Treffers. |
| geo_region | placeContext.geo.stateProvince | Zeichenfolge | Der Name des Bundesstaates oder der Region des Treffers. Dies basiert auf der IP-Adresse des Treffers. |
| geo_zip | placeContext.geo.postalCode | Zeichenfolge | Die Postleitzahl des Treffers. Dies basiert auf der IP-Adresse des Treffers. |
| os | _experience.analytics.Umgebung.operatingSystemID | Ganzzahl | Die numerische ID, die das Betriebssystem des Besuchers darstellt. Dies basiert auf der Spalte user_agent. |
| search_page_num | search.pageDepth | Ganzzahl | Diese Variable wird von der Dimension &quot;Rangansicht aller Suchseiten&quot;verwendet und gibt an, welche Seite der Suchergebnisse Ihre Site enthält | angezeigt wurde, bevor der Benutzer auf Ihre Site klickte. |
| visit_keywords | _experience.analytics.session.search.keywords | Zeichenfolge | Eine Variable, die in der Dimension &quot;Suchbegriffe&quot;verwendet wird. |
| visit_num | _experience.analytics.session.num | Ganzzahl | Eine Variable, die in der Dimension &quot;Besuch-Nr.&quot;verwendet wird. Dieser Beginn wird bei 1 erhöht und bei jedem neuen Beginn (pro Benutzer) inkrementiert. |
| visit_page_num | _experience.analytics.session.depth | Ganzzahl | Eine Variable, die in der Dimension &quot;Treffertiefe&quot;verwendet wird. Dieser Wert wird für jeden vom Benutzer erstellten Treffer um 1 erhöht und nach jedem Besuch zurückgesetzt. |
| visit_Werber | _experience.analytics.session.web.webReferrer.URL | Zeichenfolge | Die erste verweisende Stelle des Besuchs. |
| visit_search_page_num | _experience.analytics.session.search.pageDepth | Ganzzahl | Der erste Seitenname des Besuchs. |
| post_prop1 - post_prop75 | _experience.analytics.customDimensions.listprops.prop1 - _experience.analytics.customDimensions.listprops.prop75 | Objekt | Benutzerspezifische Traffic-Variablen 1-75. |
| post_hier1 - post_hier5 | _experience.analytics.customDimensions.hierarchies.hier1 - _experience.analytics.customDimensions.hierarchy.hier5 | Objekt | Wird von Hierarchievariablen verwendet und enthält eine durch Trennzeichen getrennte Liste von Werten. | {Werte (Array), Trennzeichen (Zeichenfolge)} |
| post_mvvar1 - post_mvvar3 | _experience.analytics.customDimensions.Listen.Liste1.Liste[] - _experience.analytics.customDimensions.Listen.Liste3.Liste[] | array | Eine Liste von Variablenwerten. Enthält eine durch Trennzeichen getrennte Liste von benutzerdefinierten Werten, je nach Implementierung. | {value (Zeichenfolge), key (Zeichenfolge)} |
| post_cookies | environment.browserDetails.cookiesEnabled | Boolescher Wert | Die Variable, die in der Dimension „Cookie-Unterstützung“ verwendet wurde. |
| post_Ereignis_Liste | commerce.purchase, commerce.productViews, commerce.productListOpen, commerce.checkouts, commerce.productListAdds, commerce.productListRemoval, commerce.productListViews | Objekt | Beim Treffer ausgelöste Standard-Commerce-Ereignis | {id (Zeichenfolge), Wert (Zahl)} |
| post_Ereignis_Liste | _experience.analytics.Ereignis1to100.Ereignis1 - _experience.analytics.Ereignis1to100.Ereignis100, _experience.analytics.Ereignis101to200.Ereignis101 - _experience.analytics.Ereignis101to20 Ereignis200, _experience.analytics.Ereignis201to300.Ereignis201 - _experience.analytics.Ereignis201to300.Ereignis300, _experience.analytics.Ereignis301to400.Ereignis3 01 - _experience.analytics.Ereignis301to400.400, _experience.analytics.401to500.401 - _experience.analytics.page401to500.source500, _experience.analytics.JB501bis600.JEDE501 - _experience.analytics.JEE501bis600.JEE600, _experience.analytics.JEE601bis700.JEE601 - _experience.analytics.J66001 601to700.700, _experience.analytics.701to800.701 - _experience.analytics.JEE701to800.JEE800, _experience.analytics.J8001to8177777000000000000000 900.801 - _experience.analytics.801to900.900, _experience.analytics.901to1000.901 - _experience.analytics.901to100 0.1000 | Objekt | Benutzerspezifische Ereignis, die beim Treffer ausgelöst werden. | {id (Objekt), Wert (Objekt)} |
| post_java_enabled | environment.browserDetails.javaEnabled | Boolescher Wert | Eine Flag, die angibt, ob Java aktiviert ist. |
| post_latitude | placeContext.geo._Schema.latitude | number | <!-- MISSING --> |
| post_Längengrad | placeContext.geo._Schema.Längengrad | number | <!-- MISSING --> |
| post_page_Ereignis | web.webInteraction.type | Zeichenfolge | Der Typ des Treffers, der in der Bildanforderung gesendet wird (Standard-Treffer, Downloadlink, Ausstiegslink oder benutzerspezifischer Link angeklickt). |
| post_page_Ereignis | web.webInteraction.linkClicks.value | number | Der Typ des Treffers, der in der Bildanforderung gesendet wird (Standard-Treffer, Downloadlink, Ausstiegslink oder benutzerspezifischer Link angeklickt). |
| post_page_Ereignis_var1 | web.webInteraction.URL | Zeichenfolge | Diese Variable wird nur bei der Linktracking-Bildanforderungen verwendet. Dies ist die URL des angeklickten Downloadlinks, Exitlinks oder benutzerspezifischen Links. |
| post_page_Ereignis_var2 | web.webInteraction.name | Zeichenfolge | Diese Variable wird nur bei der Linktracking-Bildanforderungen verwendet. Dies ist der benutzerdefinierte Name des Links. |
| post_page_type | web.webPageDetails.isErrorPage | Boolescher Wert | Damit wird die Dimension &quot;Seiten nicht gefunden&quot;gefüllt. Diese Variable sollte entweder leer sein oder &quot;ErrorPage&quot; enthalten |
| post_pagename_no_url | web.webPageDetails.pageViews.value | number | Der Name der Seite (falls festgelegt). Wenn keine Seite angegeben ist, bleibt dieser Wert leer. |
| post_product_Liste | productListItems[].items | array | Die Liste des Produkts, die über die Variable &quot;products&quot;weitergegeben wird. | {SKU (Zeichenfolge), Quantität (Ganzzahl), priceTotal (Zahl)} |
| post_search_engine | search.searchEngine | Zeichenfolge | Die numerische ID, die die Suchmaschine darstellt, die den Besucher auf Ihre Site verwiesen hat. |
| mvar1_instances | .Liste.items[] | Objekt | Liste von Variablenwerten. Enthält eine durch Trennzeichen getrennte Liste von benutzerdefinierten Werten, je nach Implementierung. |
| mvar2_instances | .Liste.items[] | Objekt | Liste von Variablenwerten. Enthält eine durch Trennzeichen getrennte Liste von benutzerdefinierten Werten, je nach Implementierung. |
|  | mvar3_instances | .Liste.items[] | Objekt | Liste von Variablenwerten. Enthält eine durch Trennzeichen getrennte Liste von benutzerdefinierten Werten, je nach Implementierung. |
| color | device.colorDepth | Ganzzahl | Farbtiefe-ID, basierend auf dem Wert der Spalte c_color. |
| first_hit_ref_type | _experience.analytics.endUser.firstWeb.webReferrer.type | Zeichenfolge | Die numerische ID, die den Werber-Typ des ersten Werbers des Besuchers darstellt. |
| first_hit_time_gmt | _experience.analytics.endUser.firstTimestamp | Ganzzahl | Zeitstempel des allerersten Treffers des Besuchers in Unix-Zeit. |
| geo_country | placeContext.geo.countryCode | Zeichenfolge | Abkürzung für das Land, aus dem der Treffer stammt, basierend auf der IP. |
| geo_latitude | placeContext.geo._Schema.latitude | number | <!-- MISSING --> |
| geo_Längengrad | placeContext.geo._Schema.Längengrad | number | <!-- MISSING --> |
| paid_search | search.isPaid | Boolescher Wert | Eine Flag, die festgelegt wird, wenn der Treffer mit der gebührenpflichtigen Sucherkennung übereinstimmt. |
| ref_type | web.webReferrer.type | Zeichenfolge | Eine numerische ID, die den Typ des Verweises für den Treffer darstellt. |
| visit_paid_search | _experience.analytics.session.search.isPaid | Boolescher Wert | Eine Flag (1 = gebührenpflichtig, 0 = nicht bezahlt), die angibt, ob der erste Treffer des Besuchs von einem gebührenpflichtigen Suchtreffer stammt. |
| visit_ref_type | _experience.analytics.session.web.webReferrer.type | Zeichenfolge | Numerische ID des Typs der verweisenden Stelle der ersten verweisenden Stelle des Besuchs. |
| visit_search_engine | _experience.analytics.session.search.searchEngine | Zeichenfolge | Numerische ID der ersten Suchmaschine des Besuchs. |
| visit_Beginn_time_gmt | _experience.analytics.session.timestamp | Ganzzahl | Zeitstempel des ersten Treffers des Besuchs in Unix-Zeit. |
