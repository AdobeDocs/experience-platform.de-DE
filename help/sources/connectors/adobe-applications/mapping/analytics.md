---
keywords: Experience Platform; Startseite; beliebte Themen; Analytics-Zuordnungsfelder; Analytics-Zuordnung
solution: Experience Platform
title: Zuordnen von Feldern für den Adobe Analytics Source Connector
description: Mit Adobe Experience Platform können Sie Adobe Analytics-Daten über die Analytics-Quelle erfassen. Manche der über ADC erfassten Daten können direkt aus Analytics-Feldern Experience-Datenmodell (XDM)-Feldern zugeordnet werden, während andere Daten Transformationen und spezifische Funktionen erfordern, um sich richtig zuordnen zu lassen.
exl-id: 15dc1368-5cf1-42e1-9683-d5158f8aa2db
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '3419'
ht-degree: 97%

---

# Analytics-Feldzuordnungen

Mit Adobe Experience Platform können Sie Adobe Analytics-Daten über die Analytics-Quelle erfassen. Manche der über ADC erfassten Daten können direkt aus Analytics-Feldern Experience-Datenmodell (XDM)-Feldern zugeordnet werden, während andere Daten Transformationen und spezifische Funktionen erfordern, um sich richtig zuordnen zu lassen.

![](../images/analytics-data-experience-platform.png)

## Direkte Zuordnungsfelder

Bestimmte Felder werden von Adobe Analytics direkt zum Experience-Datenmodell (XDM) zugeordnet.

Folgende Tabelle enthält Spalten, die den Namen des Analytics-Felds (*Analytics-Feld*), das entsprechende XDM-Feld (*XDM-Feld*) und dessen Typ (*XDM-Typ*) sowie eine Beschreibung des Felds (*Beschreibung*) enthalten.

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Analytics-Feld | XDM-Feld | XDM-Typ | Beschreibung |
| --------------- | --------- | -------- | ---------- |
| m_evar1 - m_evar250 | _experience.analytics.customDimensions.eVars.eVar1 - _experience.analytics.customDimensions.eVars.eVar250 | Zeichenfolge | Benutzerdefinierte Variable, die im Bereich zwischen 1 und 250 liegen kann. Jede Organisation verwendet diese benutzerspezifischen eVars unterschiedlich. |
| m_prop1 - m_prop75 | _experience.analytics.customDimensions.props.prop1 - _experience.analytics.customDimensions.props.prop75 | Zeichenfolge | Benutzerdefinierte Traffic-Variablen, die im Bereich zwischen 1 und 75 liegen können. |
| m_browser | _experience.analytics.environment.browserID | Ganzzahl | Zahlenkennung des Browsers. |
| m_browser_height | environment.browserDetails.viewportHeight | Ganzzahl | Höhe des Browsers in Pixel. |
| m_browser_width | environment.browserDetails.viewportWidth | Ganzzahl | Breite des Browsers in Pixel. |
| m_campaign | marketing.trackingCode | Zeichenfolge | Variable, die in der Dimension „Trackingcode“ verwendet wird. |
| m_channel | web.webPageDetails.siteSection | Zeichenfolge | Variable, die in der Dimension „Site-Bereiche“ verwendet wird. |
| m_domain | environment.domain | Zeichenfolge | Variable, die in der Dimension „Domain“ verwendet wird. Sie hängt vom Internetdienstanbieter (ISP) des Benutzers ab. |
| m_geo_city | placeContext.geo.city | Zeichenfolge | Name der Stadt des Treffers. Dieser Wert basiert auf der IP-Adresse des Treffers. |
| m_geo_dma | placeContext.geo.dmaID | Ganzzahl | Numerische Kennung des demografischen Bereichs für den Treffer. Dieser Wert basiert auf der IP-Adresse des Treffers. |
| m_geo_region | placeContext.geo.stateProvince | Zeichenfolge | Name des Bundeslands oder der Region des Treffers. Dieser Wert basiert auf der IP-Adresse des Treffers. |
| m_geo_zip | placeContext.geo.postalCode | Zeichenfolge | Postleitzahl des Treffers. Dieser Wert basiert auf der IP-Adresse des Treffers. |
| m_keywords | search.keywords | Zeichenfolge | Die in der Keyword-Dimension verwendete Variable. |
| m_os | _experience.analytics.environment.operatingSystemID | Ganzzahl | Numerische Kennung, die das Betriebssystem des Besuchers darstellt. Dieser Wert basiert auf der Spalte „user_agent“. |
| m_page_url | web.webPageDetails.URL | Zeichenfolge | URL des Seitenaufrufs. |
| m_pagename_no_url | web.webPageDetails.</span>name | Zeichenfolge | Variable, die zum Ausfüllen der Dimension „Seiten“ dient. |
| m_referrer | web.webReferrer.URL | Zeichenfolge | Seiten-URL der vorherigen Seite. |
| m_search_page_num | search.pageDepth | Ganzzahl | Wird von der Dimension „Rangansicht aller Suchseiten“ verwendet. Gibt an, auf welcher Seite der Suchergebnisse Ihre Site angezeigt wurde, ehe der Benutzer sich zu Ihrer Site durchgeklickt hat. |
| m_state | _experience.analytics.customDimensions.stateProvince | Zeichenfolge | Statusvariable. |
| m_user_server | web.webPageDetails.server | Zeichenfolge | Variable, die in der Dimension „Server“ verwendet wird. |
| m_zip | _experience.analytics.customDimensions.postalCode | Zeichenfolge | Variable, die zum Ausfüllen der Dimension „Postleitzahl“ dient. |
| accept_language | environment.browserDetails.acceptLanguage | Zeichenfolge | Liste aller zulässigen Sprachen, wie in der HTTP-Kopfzeile „Accept-Language“ angegeben. |
| homepage | web.webPageDetails.isHomePage | Boolescher Wert | Wird nicht mehr verwendet. Wird angezeigt, wenn die aktuelle URL die Browser-Startseite ist. |
| ipv6 | environment.ipV6 | Zeichenfolge |
| j_jscript | environment.browserDetails.javaScriptVersion | Zeichenfolge | Vom Browser unterstützte JavaScript-Version. |
| user_agent | environment.browserDetails.userAgent | Zeichenfolge | Die in der HTTP-Kopfzeile gesendete Benutzeragenten-Zeichenfolge. |
| mobileappid | application.</span>name | Zeichenfolge | Die App-ID, die im folgenden Format gespeichert wird: `[AppName][BundleVersion]`. |
| mobiledevice | device.model | Zeichenfolge | Der Name des Mobilgeräts. Unter iOS als kommagetrennte 2-Ziffern-Zeichenfolge gespeichert. Die erste Ziffer steht für die Gerätegeneration; die zweite weist die Version der Gerätefamilie aus. |
| pointofinterest | placeContext.POIinteraction.POIDetail.</span>name | Zeichenfolge | Wird von Mobile Services verwendet. Stellt den Zielpunkt dar. |
| pointofinterestdistance | placeContext.POIinteraction.POIDetail.geoInteractionDetails.distanceToCenter | number | Wird von Mobile Services verwendet. Stellt den Abstand zum Zielpunkt dar. |
| mobileplaceaccuracy | placeContext.POIinteraction.POIDetail.geoInteractionDetails.deviceGeoAccuracy | number | Erfasst mit der Kontextdatenvariablen a.loc.acc. Gibt die Genauigkeit des GPS in Metern zum Erfassungszeitpunkt an. |
| mobileplacecategory | placeContext.POIinteraction.POIDetail.category | Zeichenfolge | Wird mit der Kontextdatenvariablen a.loc.category erfasst. Beschreibt die Kategorie eines bestimmten Orts. |
| mobileplaceid | placeContext.POIinteraction.POIDetail.POIID | Zeichenfolge | Erfasst mit der Kontextdatenvariablen a.loc.id. Kennung für einen bestimmten Zielpunkt. |
| video | media.mediaTimed.primaryAssetReference._id | Zeichenfolge | Der Name des Videos. |
| videoad | advertising.adAssetReference._id | Zeichenfolge | Kennung des Anzeigen-Assets. |
| videocontenttype | media.mediaTimed.primaryAssetViewDetails.broadcastContentType | Zeichenfolge | Der Typ des Videoinhalts. Bei allen Videoansichten ist dieser Wert automatisch auf „Video“ eingestellt. |
| videoadpod | advertising.adAssetViewDetails.adBreak._id | Zeichenfolge | Der Pod, in dem sich die Videoanzeige befindet. |
| videoadinpod | advertising.adAssetViewDetails.index | Ganzzahl | Die Position der Videoanzeige im Pod. |
| videoplayername | media.mediaTimed.primaryAssetViewDetails.playerName | Zeichenfolge | Der Name des Video-Players. |
| videochannel | media.mediaTimed.primaryAssetViewDetails.broadcastChannel | Zeichenfolge | Der Videokanal. |
| videoadplayername | advertising.adAssetViewDetails.playerName | Zeichenfolge | Der Name des Videoanzeige-Players. |
| videochapter | media.mediaTimed.mediaChapter.chapterAssetReference._id | Zeichenfolge | Der Name des Videokapitels. |
| videoname | media.mediaTimed.primaryAssetReference._dc.title | Zeichenfolge | Der Name des Videos. |
| videoadname | advertising.adAssetReference._dc.title | Zeichenfolge | Der Name der Videoanzeige. |
| videoshow | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Series._iptc4xmpExt.Name | Zeichenfolge | Videosendung. |
| videoseason | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Season._iptc4xmpExt.Name | Zeichenfolge | Videostaffel. |
| videoepisode | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Episode._iptc4xmpExt.Name | Zeichenfolge | Videoepisode. |
| videonetwork | media.mediaTimed.primaryAssetViewDetails.broadcastNetwork | Zeichenfolge | Videonetzwerk. |
| videoshowtype | media.mediaTimed.primaryAssetReference.showType | Zeichenfolge | Typ der Videosendung. |
| videoadload | media.mediaTimed.primaryAssetViewDetails.adLoadType | Zeichenfolge | Ladeaufforderungen der Videoanzeige. |
| videofeedtype | media.mediaTimed.primaryAssetViewDetails.sourceFeed | Zeichenfolge | Video-Feed-Typ. |
| mobilebeaconmajor | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.beaconMajor | number | Mobile Services – Haupt-Beacon. |
| mobilebeaconminor | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.beaconMinor | number | Mobile Services – Neben-Beacon. |
| mobilebeaconuuid | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.proximityUUID | Zeichenfolge | Mobile Services-Beacon UUID. |
| videosessionid | media.mediaTimed.primaryAssetViewDetails._id | Zeichenfolge | Kennung der Videositzung. |
| videogenre | media.mediaTimed.primaryAssetReference._iptc4xmpExt.Genre | array | Video-Genre. | {title (Object), description (Object), type (Object), meta:xdmType (Object), items (string), meta:xdmField (Object)} |
| mobileinstalls | application.firstLaunches | Objekt | Wird beim ersten Ausführen nach einer Installation oder Neuinstallation ausgelöst | {id (string), value (number)} |
| mobileupgrades | application.upgrades | Objekt | Gibt die Zahl der App-Upgrades an. Wird beim ersten Ausführen nach einem Upgrade oder immer dann ausgelöst, wenn sich die Versionsnummer ändert. | {id (string), value (number)} |
| mobilelaunches | application.launches | Objekt | Häufigkeit, mit der die App gestartet wurde. | {id (string), value (number)} |
| mobilecrashes | application.crashes | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| mobilemessageclicks | directMarketing.clicks | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| mobileplaceentry | placeContext.POIinteraction.poiEntries | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| mobileplaceexit | placeContext.POIinteraction.poiExits | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| videotime | media.mediaTimed.timePlayed | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| videostart | media.mediaTimed.impressions | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| videocomplete | media.mediaTimed.completes | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| videosegmentviews | media.mediaTimed.mediaSegmentViews | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| videoadstart | advertising.impressions | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| videoadcomplete | advertising.completes | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| videoadtime | advertising.timePlayed | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| videochapterstart | media.mediaTimed.mediaChapter.impressions | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| videochaptercomplete | media.mediaTimed.mediaChapter.completes | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| videochaptertime | media.mediaTimed.mediaChapter.timePlayed | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| videoplay | media.mediaTimed.starts | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| videototaltime | media.mediaTimed.totalTimePlayed | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| videoqoetimetostart | media.mediaTimed.primaryAssetViewDetails.qoe.timeToStart | Objekt | Videoqualität – Startzeitpunkt. | {id (string), value (number)} |
| videoqoedropbeforestart | media.mediaTimed.dropBeforeStarts | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| videoqoebuffercount | media.mediaTimed.primaryAssetViewDetails.qoe.buffers | Objekt | Videoqualität – Anzahl Puffer | {id (string), value (number)} |
| videoqoebuffertime | media.mediaTimed.primaryAssetViewDetails.qoe.bufferTime | Objekt | Videoqualitätspufferzeit | {id (string), value (number)} |
| videoqoebitratechangecount | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateChanges | Objekt | Videoqualität – Anzahl Änderungen | {id (string), value (number)} |
| videoqoebitrateaverage | media.mediaTimed.primaryAssetViewDetails.qoe.bitrateAverage | Objekt | Videoqualität – Durchschnittliche Bitrate | {id (string), value (number)} |
| videoqoeerrorcount | media.mediaTimed.primaryAssetViewDetails.qoe.errors | Objekt | Videoqualität – Anzahl Fehler | {id (string), value (number)} |
| videoqoedroppedframecount | media.mediaTimed.primaryAssetViewDetails.qoe.droppedFrames | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| videoprogress10 | media.mediaTimed.progress10 | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| videoprogress25 | media.mediaTimed.progress25 | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| videoprogress50 | media.mediaTimed.progress50 | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| videoprogress75 | media.mediaTimed.progress75 | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| videoprogress95 | media.mediaTimed.progress95 | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| videoresume | media.mediaTimed.resumes | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| videopausecount | media.mediaTimed.pauses | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| videopausetime | media.mediaTimed.pauseTime | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| videosecondssincelastcall | media.mediaTimed.primaryAssetViewDetails.sessionTimeout | Ganzzahl |

{style="table-layout:auto"}

## Aufgeteilte Zuordnungsfelder

Diese Felder verfügen über eine einzige Quelle, sind aber **mehreren** XDM-Positionen zugeordnet.

| Analytics-Feld | XDM-Feld | XDM-Typ | Beschreibung |
| --------------- | --------- | -------- | ---------- |
| s_resolution | device.screenWidth, device.screenHeight | Ganzzahl | Numerische ID, die die Auflösung des Bildschirms darstellt. |
| mobileosversion | environment.operatingSystem, environment.operatingSystemVersion | Zeichenfolge | Version des mobilen Betriebssystems. |
| videoadlength | advertising.adAssetReference._xmpDM.duration | Ganzzahl | Länge der Videoanzeige. |

{style="table-layout:auto"}

## Generierte Zuordnungsfelder

Bestimmte Felder, die aus ADC kommen, müssen transformiert werden. So ist Logik über eine direkte Kopie von Adobe Analytics hinaus erforderlich, damit sie in XDM generiert werden können.

Folgende Tabelle enthält Spalten, die den Namen des Analytics-Felds (*Analytics-Feld*), das entsprechende XDM-Feld (*XDM-Feld*) und dessen Typ (*XDM-Typ*) sowie eine Beschreibung des Felds (*Beschreibung*) enthalten.

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Analytics-Feld | XDM-Feld | XDM-Typ | Beschreibung |
| --------------- | --------- | -------- | ----------- |
| m_prop1 - m_prop75 | _experience.analytics.customDimensions.listprops.prop1 - _experience.analytics.customDimensions.listprops.prop75 | Objekt | Benutzerdefinierte Traffic-Variablen, die im Bereich zwischen 1 und 75 liegen | {} |
| m_hier1 - m_hier5 | _experience.analytics.customDimensions.hierarchies.hier1 - _experience.analytics.customDimensions.hierarchies.hier5 | Objekt | Wird von Hierarchievariablen verwendet. Enthält eine | durch Trennzeichen getrennte Liste von Werten. | {values (array), delimiter (string)} |
| m_mvvar1 - m_mvvar3 | _experience.analytics.customDimensions.lists.list1.list[] - _experience.analytics.customDimensions.lists.list3.list[] | array | Liste mit Variablenwerten. Enthält eine durch Trennzeichen getrennte Liste benutzerdefinierter Werte (in Abhängigkeit von der Implementierung) | {value (string), key (string)} |
| m_color | device.colorDepth | Ganzzahl | Kennung der Farbtiefe, die auf dem Wert der Spalte „c_color“ basiert. |
| m_cookies | environment.browserDetails.cookiesEnabled | Boolescher Wert | Variable, die in der Dimension „Cookie-Unterstützung“ verwendet wird. |
| m_event_list | commerce.purchases, commerce.productViews, commerce.productListOpens, commerce.checkouts, commerce.productListAdds, commerce.productListRemovals, commerce.productListViews | Objekt | Beim Treffer ausgelöste Standard-Verkaufsereignisse. | {id (string), value (number)} |
| m_event_list | _experience.analytics.event1to100.event1 - _experience.analytics.event1to100.event100, _experience.analytics.event101to200.event101 - _experience.analytics.event101to200.event200, _experience.analytics.event201to300.event201 - _experience.analytics.event201to300.event300, _experience.analytics.event301to400.event301 - _experience.analytics.event301to400.event400, _experience.analytics.event401to500.event401 - _experience.analytics.event401to500.event500, _experience.analytics.event501to600.event501 - _experience.analytics.event501to600.event600, _experience.analytics.event601to700.event601 - _experience.analytics.event601to700.event700, _experience.analytics.event701to800.event701 - _experience.analytics.event701to800.event800, _experience.analytics.event801to900.event801 - _experience.analytics.event801to900.event900, _experience.analytics.event901to1000.event901 - _experience.analytics.event901to1000.event1000 | Objekt | Benutzerdefinierte Ereignisse, die beim Treffer ausgelöst werden. | {id (Object), value (Object)} |
| m_geo_country | placeContext.geo.countryCode | Zeichenfolge | Abkürzung des Landes, aus dem der Treffer kam (basierend auf der IP-Adresse). |
| m_geo_latitude | placeContext.geo._schema.latitude | number | <!-- MISSING --> |
| m_geo_longitude | placeContext.geo._schema.longitude | number | <!-- MISSING --> |
| m_java_enabled | environment.browserDetails.javaEnabled | Boolescher Wert | Eine Markierung, die angibt, ob Java aktiviert ist. |
| m_latitude | placeContext.geo._schema.latitude | number | <!-- MISSING --> |
| m_longitude | placeContext.geo._schema.longitude | number | <!-- MISSING --> |
| m_page_event_var1 | web.webInteraction.URL | Zeichenfolge | Variable, die nur in Bildanforderungen zum Linktracking verwendet wird. Die Variable enthält die URL des angeklickten Downloadlinks, Exitlinks oder benutzerspezifischen Links. |
| m_page_event_var2 | web.webInteraction.name | Zeichenfolge | Variable, die nur in Bildanforderungen zum Linktracking verwendet wird. Damit wird der benutzerdefinierte Name des Links aufgeführt, sofern angegeben. |
| m_page_type | web.webPageDetails.isErrorPage | Boolescher Wert | Variable, die zum Ausfüllen der Dimension „Seiten nicht gefunden“ dient. Diese Variable sollte entweder leer sein oder „ErrorPage“ enthalten. |
| m_pagename_no_url | web.webPageDetails.pageViews.value | number | Der Name der Seite (wenn festgelegt). Wenn keine Seite angegeben wird, bleibt dieser Wert leer. |
| m_paid_search | search.isPaid | Boolescher Wert | Markierung, die gesetzt wird, wenn der Treffer mit der Paid Search-Erkennung übereinstimmt. |
| m_product_list | productListItems[].items | array | Produktliste, so wie sie von der Variable der Produkte übergeben wurde. | {SKU (string), quantity (integer), priceTotal (number)} |
| m_ref_type | web.webReferrer.type | Zeichenfolge | Eine numerische ID, die den Typ des Verweises für den Treffer darstellt. 1 bedeutet innerhalb Ihrer Site, 2 bedeutet andere Websites, 3 bedeutet Suchmaschinen, 4 bedeutet Festplatte, 5 bedeutet USENET, 6 bedeutet „Eingegeben“/„Mit Lesezeichen versehen“ (kein Referrer), 7 bedeutet E-Mail, 8 bedeutet „Kein JavaScript“ und 9 bedeutet „Soziale Netzwerke“. |
| m_search_engine | search.searchEngine | Zeichenfolge | Numerische Kennung, die die Suchmaschine darstellt, die den Besucher auf Ihre Site verwiesen hat. |
| post_currency | commerce.order.currencyCode | Zeichenfolge | Der während der Transaktion verwendete Währungscode. |
| post_cust_hit_time_gmt | timestamp | Zeichenfolge | Dieser Wert wird nur in für Zeitstempel aktivierten Datensätzen verwendet. Das ist der Zeitstempel, der mit gesendet wird und auf Unix-Zeit basiert. |
| post_cust_visid | identityMap | Objekt | Die Besucher-ID des Kunden. |
| post_cust_visid | endUserIDs._experience.aacustomid.primary | Boolescher Wert | Die Besucher-ID des Kunden. |
| post_cust_visid | endUserIDs._experience.aacustomid.namespace.code | Zeichenfolge | Die Besucher-ID des Kunden. |
| post_visid_high + visid_low | identityMap | Objekt | Eindeutige Kennung für einen Besuch. |
| post_visid_high + visid_low | endUserIDs._experience.aaid.id | Zeichenfolge | Eindeutige Kennung für einen Besuch. |
| post_visid_high | endUserIDs._experience.aaid.primary | Boolescher Wert | Dient zusammen mit visid_low zur eindeutigen Identifizierung eines Besuchs. |
| post_visid_high | endUserIDs._experience.aaid.namespace.code | Zeichenfolge | Dient zusammen mit visid_low zur eindeutigen Identifizierung eines Besuchs. |
| post_visid_low | identityMap | Objekt | Dient zusammen mit visid_high zur eindeutigen Identifizierung eines Besuchs. |
| hit_time_gmt | receivedTimestamp | Zeichenfolge | Der Zeitstempel des Treffers basierend auf Unix-Zeit. |
| hitid_high + hitid_low | _id | Zeichenfolge | Eindeutige Kennung zur Identifizierung eines Treffers. |
| hitid_low | _id | Zeichenfolge | Dient zusammen mit hitid_high zur eindeutigen Identifizierung eines Treffers. |
| ip | environment.ipV4 | Zeichenfolge | IP-Adresse basierend auf der HTTP-Kopfzeile der Bildanforderung. |
| j_jscript | environment.browserDetails.javaScriptEnabled | Boolescher Wert | Die verwendete JavaScript-Version. |
| mcvisid_high + mcvisid_low | identityMap | Objekt | Die Experience Cloud-Besucher-ID. |
| mcvisid_high + mcvisid_low | endUserIDs._experience.mcid.id | Zeichenfolge | Die Experience Cloud-ID (ECID) wird auch als MCID bezeichnet und manchmal in Namespaces verwendet. |
| mcvisid_high | endUserIDs._experience.mcid.primary | Boolescher Wert | Die Experience Cloud-ID (ECID) wird auch als MCID bezeichnet und manchmal in Namespaces verwendet. |
| mcvisid_high | endUserIDs._experience.mcid.namespace.code | Zeichenfolge | Die Experience Cloud-ID (ECID) wird auch als MCID bezeichnet und manchmal in Namespaces verwendet. |
| mcvisid_low | identityMap | Objekt | Die Experience Cloud-Besucher-ID. |
| sdid_high + sdid_low | _experience.target.supplementalDataID | Zeichenfolge | Trefferzusammenfügungs-ID. Die Analytics-Felder sdid_high und sdid_low sind die ergänzenden Daten-IDs, mit denen zwei (oder mehr) eingehende Treffer zusammengefügt werden. |
| mobilebeaconproximity | placeContext.POIinteraction.POIDetail.beaconInteractionDetails.proximity | Zeichenfolge | Mobile Services – Beacon-Nähe. |
| videochapter | media.mediaTimed.mediaChapter.chapterAssetReference._xmpDM.duration | Ganzzahl | Der Name des Videokapitels. |
| videolength | media.mediaTimed.primaryAssetReference._xmpDM.duration | Ganzzahl | Die Länge des Videos. |

{style="table-layout:auto"}

## Erweiterte Zuordnungsfelder

Bestimmte Felder (auch „postvalues“ genannt) setzen erweiterte Umwandlungen voraus, bevor sie von Adobe Analytics-Feldern erfolgreich dem Experience-Datenmodell (XDM) zugeordnet werden können. Erweiterte Umwandlungen beinhalten die Verwendung von Adobe Experience Platform Query Service und vordefinierten Funktionen (auch Adobe-definierte Funktionen genannt) für die Sessionization, Attribution und Deduplizierung.

Weiterführende Informationen zum Ausführen dieser Umwandlungen mithilfe von Query Service finden Sie in der Dokumentation [Adobe-definierte Funktionen](../../../../query-service/sql/adobe-defined-functions.md).

Folgende Tabelle enthält Spalten, die den Namen des Analytics-Felds (*Analytics-Feld*), das entsprechende XDM-Feld (*XDM-Feld*) und dessen Typ (*XDM-Typ*) sowie eine Beschreibung des Felds (*Beschreibung*) enthalten.

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| Analytics-Feld | XDM-Feld | XDM-Typ | Beschreibung |
| --------------- | --------- | -------- | ---------- |
| post_evar1 - post_evar250 | _experience.analytics.customDimensions.eVars.eVar1 - _experience.analytics.customDimensions.eVars.eVar250 | Zeichenfolge | Benutzerdefinierte Variable, die im Bereich zwischen 1 und 250 liegen kann. Jede Organisation verwendet diese benutzerspezifischen eVars unterschiedlich. |
| post_prop1 - post_prop75 | _experience.analytics.customDimensions.props.prop1 - _experience.analytics.customDimensions.props.prop75 | Zeichenfolge | Benutzerdefinierte Traffic-Variablen, die im Bereich zwischen 1 und 75 liegen können. |
| post_browser_height | environment.browserDetails.viewportHeight | Ganzzahl | Höhe des Browsers in Pixel. |
| post_browser_width | environment.browserDetails.viewportWidth | Ganzzahl | Breite des Browsers in Pixel. |
| post_campaign | marketing.trackingCode | Zeichenfolge | Variable, die in der Dimension „Trackingcode“ verwendet wird. |
| post_channel | web.webPageDetails.siteSection | Zeichenfolge | Variable, die in der Dimension „Site-Bereiche“ verwendet wird. |
| post_cust_visid | endUserIDs._experience.aacustomid.id | Zeichenfolge | Benutzerdefinierte Besucher-ID, falls festgelegt. |
| post_first_hit_page_url | _experience.analytics.endUser.firstWeb.webPageDetails.URL | Zeichenfolge | URL der ersten Seite, zu der der Besucher gelangt. |
| post_first_hit_pagename | _experience.analytics.endUser.firstWeb.webPageDetails.name | Zeichenfolge | Variable, die in der Dimension „Ursprüngliche Entrypage“ verwendet wird. Seitenname der Entrypage des Besuchers. |
| post_keywords | search.keywords | Zeichenfolge | Die Keywords, die für den Treffer gesammelt wurden. |
| post_page_url | web.webPageDetails.URL | Zeichenfolge | URL des Seitenaufrufs. |
| post_pagename_no_url | web.webPageDetails.name | Zeichenfolge | Variable, die zum Ausfüllen der Dimension „Seiten“ dient. |
| post_purchaseid | commerce.order.purchaseID | Zeichenfolge | Variable, die zur eindeutigen Identifizierung von Käufen dient. |
| post_referrer | web.webReferrer.URL | Zeichenfolge | URL der vorherigen Seite. |
| post_state | _experience.analytics.customDimensions.stateProvince | Zeichenfolge | Statusvariable. |
| post_user_server | web.webPageDetails.server | Zeichenfolge | Variable, die in der Dimension „Server“ verwendet wird. |
| post_zip | _experience.analytics.customDimensions.postalCode | Zeichenfolge | Variable, die zum Ausfüllen der Dimension „Postleitzahl“ dient. |
| browser | _experience.analytics.environment.browserID | Ganzzahl | Numerische Kennung des Browsers. |
| domain | environment.domain | Zeichenfolge | Variable, die in der Dimension „Domain“ verwendet wird. Sie hängt vom Internetdienstanbieter (ISP) des Benutzers ab. |
| first_hit_referrer | _experience.analytics.endUser.firstWeb.webReferrer.URL | Zeichenfolge | Die erste verweisende URL für den Besucher. |
| geo_city | placeContext.geo.city | Zeichenfolge | Name der Stadt des Treffers. Dieser Wert basiert auf der IP-Adresse des Treffers. |
| geo_dma | placeContext.geo.dmaID | Ganzzahl | Numerische Kennung des demografischen Bereichs für den Treffer. Dieser Wert basiert auf der IP-Adresse des Treffers. |
| geo_region | placeContext.geo.stateProvince | Zeichenfolge | Name des Bundeslands oder der Region des Treffers. Dieser Wert basiert auf der IP-Adresse des Treffers. |
| geo_zip | placeContext.geo.postalCode | Zeichenfolge | Postleitzahl des Treffers. Dieser Wert basiert auf der IP-Adresse des Treffers. |
| os | _experience.analytics.environment.operatingSystemID | Ganzzahl | Numerische Kennung, die das Betriebssystem des Besuchers darstellt. Dieser Wert basiert auf der Spalte „user_agent“. |
| search_page_num | search.pageDepth | Ganzzahl | Diese Variable wird von der Dimension „Rangansicht aller Suchseiten“ verwendet und gibt an, auf welcher Seite mit Suchergebnissen Ihre Site angezeigt | wurde, bevor sich der Benutzer durch Ihre Site geklickt hat. |
| visit_keywords | _experience.analytics.session.search.keywords | Zeichenfolge | Variable, die in der Dimension „Keywords“ verwendet wird. |
| visit_num | _experience.analytics.session.num | Ganzzahl | Eine Variable, die in der Dimension „Besuchsnummer“ verwendet wird. Sie beginnt bei 1 und erhöht sich bei jedem neuen Besuch eines Benutzers. |
| visit_page_num | _experience.analytics.session.depth | Ganzzahl | Eine Variable, die in der Dimension „Treffertiefe“ verwendet wird. Der Wert erhöht sich bei jedem vom Benutzer generierten Treffer um 1 und wird nach jedem Besuch zurückgesetzt. |
| visit_referrer | _experience.analytics.session.web.webReferrer.URL | Zeichenfolge | Die erste verweisende Stelle des Besuchs. |
| visit_search_page_num | _experience.analytics.session.search.pageDepth | Ganzzahl | Der erste Seitenname des Besuchs. |
| post_prop1 - post_prop75 | _experience.analytics.customDimensions.listprops.prop1 - _experience.analytics.customDimensions.listprops.prop75 | Objekt | Benutzerdefinierte Traffic-Variablen 1 bis 75. |
| post_hier1 - post_hier5 | _experience.analytics.customDimensions.hierarchies.hier1 - _experience.analytics.customDimensions.hierarchies.hier5 | Objekt | Wird von Hierarchievariablen verwendet und enthält eine durch Trennzeichen getrennte Liste von Werten. | {values (array), delimiter (string)} |
| post_mvvar1 - post_mvvar3 | _experience.analytics.customDimensions.lists.list1.list[] - _experience.analytics.customDimensions.lists.list3.list[] | array | Eine Liste mit Variablenwerten. Enthält eine durch Trennzeichen getrennte Liste benutzerdefinierter Werte (je nach Implementierung). | {value (string), key (string)} |
| post_cookies | environment.browserDetails.cookiesEnabled | Boolescher Wert | Die Variable, die in der Dimension „Cookie-Unterstützung“ verwendet wird. |
| post_event_list | commerce.purchases, commerce.productViews, commerce.productListOpens, commerce.checkouts, commerce.productListAdds, commerce.productListRemovals, commerce.productListViews | Objekt | Beim Treffer ausgelöste Standard-Verkaufsereignisse. | {id (string), value (number)} |
| post_event_list | _experience.analytics.event1to100.event1 - _experience.analytics.event1to100.event100, _experience.analytics.event101to200.event101 - _experience.analytics.event101to200.event200, _experience.analytics.event201to300.event201 - _experience.analytics.event201to300.event300, _experience.analytics.event301to400.event301 - _experience.analytics.event301to400.event400, _experience.analytics.event401to500.event401 - _experience.analytics.event401to500.event500, _experience.analytics.event501to600.event501 - _experience.analytics.event501to600.event600, _experience.analytics.event601to700.event601 - _experience.analytics.event601to700.event700, _experience.analytics.event701to800.event701 - _experience.analytics.event701to800.event800, _experience.analytics.event801to900.event801 - _experience.analytics.event801to900.event900, _experience.analytics.event901to1000.event901 - _experience.analytics.event901to1000.event1000 | Objekt | Benutzerdefinierte Ereignisse, die beim Treffer ausgelöst werden. | {id (Object), value (Object)} |
| post_java_enabled | environment.browserDetails.javaEnabled | Boolescher Wert | Eine Markierung, die angibt, ob Java aktiviert ist. |
| post_latitude | placeContext.geo._schema.latitude | number | <!-- MISSING --> |
| post_longitude | placeContext.geo._schema.longitude | number | <!-- MISSING --> |
| post_page_event | web.webInteraction.type | Zeichenfolge | Die Art des in der Bildanforderung gesendeten Treffers (Standardtreffer, angeklickter Downloadlink, Exitlink oder benutzerspezifischer Link). |
| post_page_event | web.webInteraction.linkClicks.value | number | Die Art des in der Bildanforderung gesendeten Treffers (Standardtreffer, angeklickter Downloadlink, Exitlink oder benutzerspezifischer Link). |
| post_page_event_var1 | web.webInteraction.URL | Zeichenfolge | Diese Variable wird nur bei Bildanforderungen zum Linktracking verwendet. Dies ist die URL des angeklickten Downloadlinks, Exitlinks oder benutzerspezifischen Links. |
| post_page_event_var2 | web.webInteraction.name | Zeichenfolge | Diese Variable wird nur bei Bildanforderungen zum Linktracking verwendet. Dies ist der benutzerdefinierte Name des Links. |
| post_page_type | web.webPageDetails.isErrorPage | Boolescher Wert | Damit wird die Dimension „Seiten nicht gefunden“ ausgefüllt. Diese Variable sollte entweder leer sein oder „ErrorPage“ enthalten. |
| post_pagename_no_url | web.webPageDetails.pageViews.value | number | Der Name der Seite (wenn festgelegt). Wenn keine Seite angegeben wird, bleibt dieser Wert leer. |
| post_product_list | productListItems[].items | array | Produktliste, so wie sie von der Variable der Produkte übergeben wurde. | {SKU (string), quantity (integer), priceTotal (number)} |
| post_search_engine | search.searchEngine | Zeichenfolge | Numerische Kennung, die die Suchmaschine darstellt, die den Besucher auf Ihre Site verwiesen hat. |
| mvvar1_instances | .list.items[] | Objekt | Liste mit Variablenwerten. Enthält eine durch Trennzeichen getrennte Liste benutzerdefinierter Werte (je nach Implementierung). |
| mvvar2_instances | .list.items[] | Objekt | Liste mit Variablenwerten. Enthält eine durch Trennzeichen getrennte Liste benutzerdefinierter Werte (je nach Implementierung). |
|  | mvvar3_instances | .list.items[] | Objekt | Liste mit Variablenwerten. Enthält eine durch Trennzeichen getrennte Liste benutzerdefinierter Werte (je nach Implementierung). |
| color | device.colorDepth | Ganzzahl | Farbtiefen-ID, basierend auf dem Wert der Spalte „c_color“. |
| first_hit_ref_type | _experience.analytics.endUser.firstWeb.webReferrer.type | Zeichenfolge | Numerische ID des Typs der verweisenden Stelle der allerersten verweisenden Stelle des Besuchers. |
| first_hit_time_gmt | _experience.analytics.endUser.firstTimestamp | Ganzzahl | Zeitstempel des allerersten Treffers des Besuchers in Unix-Zeit. |
| geo_country | placeContext.geo.countryCode | Zeichenfolge | Abkürzung für das Land, aus dem der Treffer stammt, basierend auf der IP-Adresse. |
| geo_latitude | placeContext.geo._schema.latitude | number | <!-- MISSING --> |
| geo_longitude | placeContext.geo._schema.longitude | number | <!-- MISSING --> |
| paid_search | search.isPaid | Boolescher Wert | Markierung, die gesetzt wird, wenn der Treffer mit der Paid Search-Erkennung übereinstimmt. |
| ref_type | web.webReferrer.type | Zeichenfolge | Eine numerische ID, die den Typ des Verweises für den Treffer darstellt. |
| visit_paid_search | _experience.analytics.session.search.isPaid | Boolescher Wert | Eine Markierung (1 = paid, 0 = not paid), die angibt, ob der erste Treffer des Besuchs ein Paid Search-Treffer war oder nicht. |
| visit_ref_type | _experience.analytics.session.web.webReferrer.type | Zeichenfolge | Numerische ID des Typs der verweisenden Stelle der ersten verweisenden Stelle des Besuchs. |
| visit_search_engine | _experience.analytics.session.search.searchEngine | Zeichenfolge | Numerische ID der ersten Suchmaschine des Besuchs. |
| visit_start_time_gmt | _experience.analytics.session.timestamp | Ganzzahl | Zeitstempel des ersten Treffers des Besuchs in Unix-Zeit. |

{style="table-layout:auto"}