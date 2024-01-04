---
keywords: Analytics-Zuordnungsfelder;Analytics-Zuordnung
solution: Experience Platform
title: Zuordnen von Feldern für den Adobe Analytics Source Connector
description: Ordnen Sie Adobe Analytics-Felder mithilfe des Analytics Source Connector XDM-Feldern zu.
exl-id: 15dc1368-5cf1-42e1-9683-d5158f8aa2db
source-git-commit: bb07d45df3ca585b2ca4af07cc991ac0b1e4df12
workflow-type: tm+mt
source-wordcount: '2367'
ht-degree: 75%

---

# Analytics-Feldzuordnungen

Mit Adobe Experience Platform können Sie Adobe Analytics-Daten über die Analytics-Quelle erfassen. Einige der über ADC erfassten Daten können direkt aus Analytics-Feldern Experience-Datenmodell (XDM)-Feldern zugeordnet werden, während andere Daten Transformationen und spezifische Funktionen erfordern, damit sie erfolgreich zugeordnet werden können.

![](../images/analytics-data-experience-platform.png)

## Direkte Zuordnungsfelder

Bestimmte Felder werden von Adobe Analytics direkt zum Experience-Datenmodell (XDM) zugeordnet.

| Analytics-Feld | XDM-Feld | XDM-Typ | Beschreibung |
| --------------- | --------- | -------- | ---------- |
| `m_evar1`<br/>`[...]`<br/>`m_evar250` | `_experience.analytics.customDimensions.`<br/>`eVars.eVar1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`eVars.eVar250` | string | Benutzerdefinierte Analytics-eVars. Jede Organisation kann eVars anders verwenden. |
| `m_prop1`<br/>`[...]`<br/>`m_prop75` | `_experience.analytics.customDimensions.`<br/>`props.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`props.prop75` | Zeichenfolge | Benutzerdefinierte Analytics-Eigenschaften. Jede Organisation kann Props unterschiedlich verwenden. |
| `m_browser` | `_experience.analytics.environment.`<br/>`browserID` | Ganzzahl | Zahlenkennung des Browsers. |
| `m_browser_height` | `environment.browserDetails.viewportHeight` | Ganzzahl | Höhe des Browsers in Pixel. |
| `m_browser_width` | `environment.browserDetails.viewportWidth` | Ganzzahl | Breite des Browsers in Pixel. |
| `m_campaign` | `marketing.trackingCode` | Zeichenfolge | Variable, die in der Dimension „Trackingcode“ verwendet wird. |
| `m_channel` | `web.webPageDetails.siteSection` | Zeichenfolge | Variable, die in der Dimension „Site-Bereiche“ verwendet wird. |
| `m_domain` | `environment.domain` | Zeichenfolge | Variable, die in der Dimension „Domain“ verwendet wird. Er basiert auf dem Internetdienstanbieter (ISP) des Benutzers. |
| `m_geo_city` | `placeContext.geo.city` | Zeichenfolge | Name der Stadt des Treffers. Dies basiert auf der IP-Adresse des Treffers. |
| `m_geo_dma` | `placeContext.geo.dmaID` | Ganzzahl | Numerische Kennung des demografischen Bereichs für den Treffer. Dies basiert auf der IP-Adresse des Treffers. |
| `m_geo_region` | `placeContext.geo.stateProvince` | Zeichenfolge | Name des Bundeslands oder der Region des Treffers. Dies basiert auf der IP-Adresse des Treffers. |
| `m_geo_zip` | `placeContext.geo.postalCode` | Zeichenfolge | Postleitzahl des Treffers. Dies basiert auf der IP-Adresse des Treffers. |
| `m_keywords` | `search.keywords` | Zeichenfolge | Die in der Keyword-Dimension verwendete Variable. |
| `m_os` | `_experience.analytics.environment.`<br/>`operatingSystemID` | Ganzzahl | Numerische Kennung, die das Betriebssystem des Besuchers darstellt. Dieser Wert basiert auf der Spalte „user_agent“. |
| `m_page_url` | `web.webPageDetails.URL` | Zeichenfolge | URL des Seitenaufrufs. |
| `m_pagename_no_url` | `web.webPageDetails.name` | Zeichenfolge | Variable, die zum Ausfüllen der Dimension „Seiten“ dient. |
| `m_referrer` | `web.webReferrer.URL` | Zeichenfolge | Seiten-URL der vorherigen Seite. |
| `m_search_page_num` | `search.pageDepth` | Ganzzahl | Wird von der Dimension „Rangansicht aller Suchseiten“ verwendet. Gibt an, auf welcher Seite der Suchergebnisse Ihre Site angezeigt wurde, ehe der Benutzer sich zu Ihrer Site durchgeklickt hat. |
| `m_state` | `_experience.analytics.customDimensions.`<br/>`stateProvince` | Zeichenfolge | Statusvariable. |
| `m_user_server` | `web.webPageDetails.server` | Zeichenfolge | Variable, die in der Dimension „Server“ verwendet wird. |
| `m_zip` | `_experience.analytics.customDimensions.`<br/>`postalCode` | Zeichenfolge | Variable, die zum Ausfüllen der Dimension „Postleitzahl“ dient. |
| `accept_language` | `environment.browserDetails.acceptLanguage` | Zeichenfolge | Liste aller zulässigen Sprachen, wie in der HTTP-Kopfzeile „Accept-Language“ angegeben. |
| `homepage` | `web.webPageDetails.isHomePage` | Boolescher Wert | Wird nicht mehr verwendet. Wird angezeigt, wenn die aktuelle URL die Browser-Startseite ist. |
| `ipv6` | `environment.ipV6` | string |
| `j_jscript` | `environment.browserDetails.javaScriptVersion` | string | Die vom Browser unterstützte JavaScript-Version. |
| `user_agent` | `environment.browserDetails.userAgent` | Zeichenfolge | Die in der HTTP-Kopfzeile gesendete Benutzeragenten-Zeichenfolge. |
| `mobileappid` | `application.name` | Zeichenfolge | Die App-ID, die im folgenden Format gespeichert wird: `[AppName][BundleVersion]`. |
| `mobiledevice` | `device.model` | Zeichenfolge | Der Name des Mobilgeräts. Unter iOS als kommagetrennte 2-Ziffern-Zeichenfolge gespeichert. Die erste Ziffer steht für die Gerätegeneration; die zweite weist die Version der Gerätefamilie aus. |
| `pointofinterest` | `placeContext.POIinteraction.POIDetail.`<br/>`name` | Zeichenfolge | Wird von Mobile Services verwendet. Stellt den Zielpunkt dar. |
| `pointofinterestdistance` | `placeContext.POIinteraction.POIDetail.`<br/>`geoInteractionDetails.distanceToCenter` | number | Wird von Mobile Services verwendet. Stellt den Abstand zum Zielpunkt dar. |
| `mobileplaceaccuracy` | `placeContext.POIinteraction.POIDetail.`<br/>`geoInteractionDetails.deviceGeoAccuracy` | number | Erfasst mit der Kontextdatenvariablen a.loc.acc. Gibt die Genauigkeit des GPS in Metern zum Erfassungszeitpunkt an. |
| `mobileplacecategory` | `placeContext.POIinteraction.POIDetail.`<br/>`category` | Zeichenfolge | Wird mit der Kontextdatenvariablen a.loc.category erfasst. Beschreibt die Kategorie eines bestimmten Orts. |
| `mobileplaceid` | `placeContext.POIinteraction.POIDetail.`<br/>`POIID` | Zeichenfolge | Erfasst mit der Kontextdatenvariablen a.loc.id. Kennung für einen bestimmten Zielpunkt. |
| `video` | `media.mediaTimed.primaryAssetReference.`<br/>`_id` | Zeichenfolge | Der Name des Videos. |
| `videoad` | `advertising.adAssetReference._id` | Zeichenfolge | Kennung des Anzeigen-Assets. |
| `videocontenttype` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`broadcastContentType` | Zeichenfolge | Der Typ des Videoinhalts. Bei allen Videoansichten ist dieser Wert automatisch auf „Video“ eingestellt. |
| `videoadpod` | `advertising.adAssetViewDetails.adBreak._id` | Zeichenfolge | Der Pod, in dem sich die Videoanzeige befindet. |
| `videoadinpod` | `advertising.adAssetViewDetails.index` | Ganzzahl | Die Position der Videoanzeige im Pod. |
| `videoplayername` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`playerName` | Zeichenfolge | Der Name des Video-Players. |
| `videochannel` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`broadcastChannel` | Zeichenfolge | Der Videokanal. |
| `videoadplayername` | `advertising.adAssetViewDetails.playerName` | Zeichenfolge | Der Name des Videoanzeige-Players. |
| `videochapter` | `media.mediaTimed.mediaChapter.`<br/>`chapterAssetReference._id` | Zeichenfolge | Der Name des Videokapitels. |
| `videoname` | `media.mediaTimed.primaryAssetReference.`<br/>`_dc.title` | Zeichenfolge | Der Name des Videos. |
| `videoadname` | `advertising.adAssetReference._dc.title` | Zeichenfolge | Der Name der Videoanzeige. |
| `videoshow` | `media.mediaTimed.primaryAssetReference.`<br/>`_iptc4xmpExt.Series._iptc4xmpExt.Name` | Zeichenfolge | Videosendung. |
| `videoseason` | `media.mediaTimed.primaryAssetReference.`<br/>`_iptc4xmpExt.Season._iptc4xmpExt.Name` | Zeichenfolge | Videostaffel. |
| `videoepisode` | `media.mediaTimed.primaryAssetReference.`<br/>`_iptc4xmpExt.Episode._iptc4xmpExt.Name` | Zeichenfolge | Videoepisode. |
| `videonetwork` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`broadcastNetwork` | Zeichenfolge | Videonetzwerk. |
| `videoshowtype` | `media.mediaTimed.primaryAssetReference.`<br/>`showType` | Zeichenfolge | Typ der Videosendung. |
| `videoadload` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`adLoadType` | Zeichenfolge | Ladeaufforderungen der Videoanzeige. |
| `videofeedtype` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`sourceFeed` | Zeichenfolge | Video-Feed-Typ. |
| `mobilebeaconmajor` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.beaconMajor` | number | Mobile Services – Haupt-Beacon. |
| `mobilebeaconminor` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.beaconMinor` | number | Mobile Services – Neben-Beacon. |
| `mobilebeaconuuid` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.proximityUUID` | Zeichenfolge | Mobile Services-Beacon UUID. |
| `videosessionid` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`_id` | Zeichenfolge | Kennung der Videositzung. |
| `videogenre` | `media.mediaTimed.primaryAssetReference.`<br/>`_iptc4xmpExt.Genre` | array | Video-Genre. | {title (Object), description (Object), type (Object), meta:xdmType (Object), items (string), meta:xdmField (Object)} |
| `mobileinstalls` | `application.firstLaunches` | Objekt | Wird beim ersten Ausführen nach der Installation oder Neuinstallation ausgelöst | {id (string), value (number)} |
| `mobileupgrades` | `application.upgrades` | Objekt | Gibt die Zahl der App-Upgrades an. Wird beim ersten Ausführen nach einem Upgrade oder immer dann ausgelöst, wenn sich die Versionsnummer ändert. | {id (string), value (number)} |
| `mobilelaunches` | `application.launches` | Objekt | Häufigkeit, mit der die App gestartet wurde. | {id (string), value (number)} |
| `mobilecrashes` | `application.crashes` | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| `mobilemessageclicks` | `directMarketing.clicks` | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| `mobileplaceentry` | `placeContext.POIinteraction.poiEntries` | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| `mobileplaceexit` | `placeContext.POIinteraction.poiExits` | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| `videotime` | `media.mediaTimed.timePlayed` | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| `videostart` | `media.mediaTimed.impressions` | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| `videocomplete` | `media.mediaTimed.completes` | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| `videosegmentviews` | `media.mediaTimed.mediaSegmentViews` | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| `videoadstart` | `advertising.impressions` | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| `videoadcomplete` | `advertising.completes` | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| `videoadtime` | `advertising.timePlayed` | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| `videochapterstart` | `media.mediaTimed.mediaChapter.`<br/>`impressions` | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| `videochaptercomplete` | `media.mediaTimed.mediaChapter.`<br/>`completes` | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| `videochaptertime` | `media.mediaTimed.mediaChapter.`<br/>`timePlayed` | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| `videoplay` | `media.mediaTimed.starts` | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| `videototaltime` | `media.mediaTimed.totalTimePlayed` | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| `videoqoetimetostart` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.timeToStart` | Objekt | Videoqualität – Startzeitpunkt. | {id (string), value (number)} |
| `videoqoedropbeforestart` | `media.mediaTimed.dropBeforeStarts` | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| `videoqoebuffercount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.buffers` | Objekt | Videoqualität – Anzahl Puffer | {id (string), value (number)} |
| `videoqoebuffertime` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bufferTime` | Objekt | Videoqualitätspufferzeit | {id (string), value (number)} |
| `videoqoebitratechangecount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bitrateChanges` | Objekt | Videoqualität – Anzahl Änderungen | {id (string), value (number)} |
| `videoqoebitrateaverage` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bitrateAverage` | Objekt | Videoqualität – Durchschnittliche Bitrate | {id (string), value (number)} |
| `videoqoeerrorcount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.errors` | Objekt | Videoqualität – Anzahl Fehler | {id (string), value (number)} |
| `videoqoedroppedframecount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.droppedFrames` | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| `videoprogress10` | `media.mediaTimed.progress10` | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| `videoprogress25` | `media.mediaTimed.progress25` | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| `videoprogress50` | `media.mediaTimed.progress50` | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| `videoprogress75` | `media.mediaTimed.progress75` | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| `videoprogress95` | `media.mediaTimed.progress95` | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| `videoresume` | `media.mediaTimed.resumes` | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| `videopausecount` | `media.mediaTimed.pauses` | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| `videopausetime` | `media.mediaTimed.pauseTime` | Objekt | <!-- MISSING --> | {id (string), value (number)} |
| `videosecondssincelastcall` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`sessionTimeout` | integer |

{style="table-layout:auto"}

## Aufspaltungsfelder

Diese Felder verfügen über eine einzige Quelle, sind aber **mehreren** XDM-Positionen zugeordnet.

| Analytics-Feld | XDM-Feld | XDM-Typ | Beschreibung |
| --------------- | --------- | -------- | ---------- |
| `s_resolution` | `device.screenWidth`,<br/>`device.screenHeight` | Ganzzahl | Numerische ID, die die Auflösung des Bildschirms darstellt. |
| `mobileosversion` | `environment.operatingSystem`,<br/>`environment.operatingSystemVersion` | Zeichenfolge | Version des mobilen Betriebssystems. |
| `videoadlength` | `advertising.adAssetReference._xmpDM.duration` | Ganzzahl | Länge der Videoanzeige. |

{style="table-layout:auto"}

## Generierte Zuordnungsfelder

Wählen Sie Felder aus, die von ADC stammen, müssen transformiert werden, sodass Logik über eine Direktkopie von Adobe Analytics hinaus in XDM generiert werden muss.

| Analytics-Feld | XDM-Feld | XDM-Typ | Beschreibung |
| --------------- | --------- | -------- | ----------- |
| `m_prop1`<br/>`[...]`<br/>`m_prop75` | `_experience.analytics.customDimensions`<br/>`.listprops.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`listprops.prop75` | Objekt | Benutzerdefinierte Analytics-Eigenschaften, die als Listen-Props konfiguriert sind. Sie enthält eine durch Trennzeichen getrennte Liste von Werten. | {} |
| `m_hier1`<br/>`[...]`<br/>`m_hier5` | `_experience.analytics.customDimensions.`<br/>`hierarchies.hier1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`hierarchies.hier5` | Objekt | Wird von Hierarchievariablen verwendet. Sie enthält eine durch Trennzeichen getrennte Liste von Werten. | {values (array), delimiter (string)} |
| `m_mvvar1`<br/>`[...]`<br/>`m_mvvar3` | `_experience.analytics.customDimensions.`<br/>`lists.list1.list[]`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`lists.list3.list[]` | array | Benutzerdefinierte Analytics-Listenvariablen. Enthält eine durch Trennzeichen getrennte Liste von Werten. | {value (string), key (string)} |
| `m_color` | `device.colorDepth` | integer | Die Farbtiefen-ID, die auf dem Wert der Spalte c_color basiert. |
| `m_cookies` | `environment.browserDetails.cookiesEnabled` | Boolescher Wert | Variable, die in der Dimension „Cookie-Unterstützung“ verwendet wird. |
| `m_event_list` | `commerce.purchases`,<br/>`commerce.productViews`,<br/>`commerce.productListOpens`,<br/>`commerce.checkouts`,<br/>`commerce.productListAdds`,<br/>`commerce.productListRemovals`,<br/>`commerce.productListViews` | Objekt | Beim Treffer ausgelöste Standard-Verkaufsereignisse. | {id (string), value (number)} |
| `m_event_list` | `_experience.analytics.event1to100.event1`<br/>`[...]`<br/>`_experience.analytics.event901to1000.event1000` | Objekt | Benutzerdefinierte Ereignisse, die beim Treffer ausgelöst werden. | {id (Object), value (Object)} |
| `m_geo_country` | `placeContext.geo.countryCode` | Zeichenfolge | Abkürzung des Landes, aus dem der Treffer stammt, basierend auf der IP. |
| `m_geo_latitude` | `placeContext.geo._schema.latitude` | number | <!-- MISSING --> |
| `m_geo_longitude` | `placeContext.geo._schema.longitude` | number | <!-- MISSING --> |
| `m_java_enabled` | `environment.browserDetails.javaEnabled` | boolean | Eine Markierung, die angibt, ob Java™ aktiviert ist. |
| `m_latitude` | `placeContext.geo._schema.latitude` | number | <!-- MISSING --> |
| `m_longitude` | `placeContext.geo._schema.longitude` | number | <!-- MISSING --> |
| `m_page_event_var1` | `web.webInteraction.URL` | Zeichenfolge | Variable, die nur in Bildanforderungen zum Linktracking verwendet wird. Die Variable enthält die URL des angeklickten Downloadlinks, Exitlinks oder benutzerspezifischen Links. |
| `m_page_event_var2` | `web.webInteraction.name` | Zeichenfolge | Variable, die nur in Bildanforderungen zum Linktracking verwendet wird. Damit wird der benutzerdefinierte Name des Links aufgeführt, sofern angegeben. |
| `m_page_type` | `web.webPageDetails.isErrorPage` | Boolescher Wert | Variable, die zum Ausfüllen der Dimension „Seiten nicht gefunden“ dient. Diese Variable sollte entweder leer sein oder „ErrorPage“ enthalten. |
| `m_pagename_no_url` | `web.webPageDetails.pageViews.value` | number | Der Name der Seite (wenn festgelegt). Wenn keine Seite angegeben ist, bleibt dieser Wert leer. |
| `m_paid_search` | `search.isPaid` | Boolescher Wert | Markierung, die gesetzt wird, wenn der Treffer mit der Paid Search-Erkennung übereinstimmt. |
| `m_product_list` | `productListItems[].items` | array | Produktliste, so wie sie von der Variable der Produkte übergeben wurde. | {SKU (string), quantity (integer), priceTotal (number)} |
| `m_ref_type` | `web.webReferrer.type` | Zeichenfolge | Eine numerische ID, die den Typ des Verweises für den Treffer darstellt.<br/>`1`: Innerhalb Ihrer Site<br/>`2`: Andere Websites<br/>`3`: Suchmaschinen<br/>`4`: Festplatte<br/>`5`: USENET<br/>`6`: Eingegeben/mit Lesezeichen versehen (kein Referrer)<br/>`7`: email<br/>`8`: Kein JavaScript<br/>`9`: Soziale Netzwerke |
| `m_search_engine` | `search.searchEngine` | Zeichenfolge | Numerische Kennung, die die Suchmaschine darstellt, die den Besucher auf Ihre Site verwiesen hat. |
| `post_currency` | `commerce.order.currencyCode` | Zeichenfolge | Der während der Transaktion verwendete Währungscode. |
| `post_cust_hit_time_gmt` | `timestamp` | Zeichenfolge | Dieser Wert wird nur in für Zeitstempel aktivierten Datensätzen verwendet. Dies ist der Zeitstempel, der mit dem Treffer gesendet wird, basierend auf der UNIX®-Zeit. |
| `post_cust_visid` | `identityMap` | Objekt | Die Besucher-ID des Kunden. |
| `post_cust_visid` | `endUserIDs._experience.aacustomid.primary` | Boolescher Wert | Die Besucher-ID des Kunden. |
| `post_cust_visid` | `endUserIDs._experience.aacustomid.namespace.code` | Zeichenfolge | Die Besucher-ID des Kunden. |
| `post_visid_high` + `visid_low` | `identityMap` | Objekt | Eindeutige Kennung für einen Besuch. |
| `post_visid_high` + `visid_low` | `endUserIDs._experience.aaid.id` | Zeichenfolge | Eindeutige Kennung für einen Besuch. |
| `post_visid_high` | `endUserIDs._experience.aaid.primary` | boolean | Verwendet mit `visid_low` zur eindeutigen Identifizierung eines Besuchs. |
| `post_visid_high` | `endUserIDs._experience.aaid.namespace.code` | Zeichenfolge | Verwendet mit `visid_low` zur eindeutigen Identifizierung eines Besuchs. |
| `post_visid_low` | `identityMap` | Objekt | Wird mit visid_high zur eindeutigen Identifizierung eines Besuchs verwendet. |
| `hit_time_gmt` | `receivedTimestamp` | Zeichenfolge | Der Zeitstempel des Treffers basierend auf der UNIX®-Zeit. |
| `hitid_high` + `hitid_low` | `_id` | Zeichenfolge | Eindeutige Kennung zur Identifizierung eines Treffers. |
| `hitid_low` | `_id` | Zeichenfolge | Wird mit hitid_high zur eindeutigen Identifizierung eines Treffers verwendet. |
| `ip` | `environment.ipV4` | Zeichenfolge | IP-Adresse basierend auf der HTTP-Kopfzeile der Bildanforderung. |
| `j_jscript` | `environment.browserDetails.javaScriptEnabled` | Boolescher Wert | Die verwendete JavaScript-Version. |
| `mcvisid_high` + `mcvisid_low` | identityMap | Objekt | Die Experience Cloud-Besucher-ID. |
| `mcvisid_high` + `mcvisid_low` | endUserIDs._experience.mcid.id | Zeichenfolge | Die Experience Cloud ID (ECID) wird auch als MCID bezeichnet und manchmal in Namespaces verwendet. |
| `mcvisid_high` | `endUserIDs._experience.mcid.primary` | boolean | Die Experience Cloud ID (ECID) wird auch als MCID bezeichnet und manchmal in Namespaces verwendet. |
| `mcvisid_high` | `endUserIDs._experience.mcid.namespace.code` | Zeichenfolge | Die Experience Cloud ID (ECID) wird auch als MCID bezeichnet und manchmal in Namespaces verwendet. |
| `mcvisid_low` | `identityMap` | Objekt | Die Experience Cloud-Besucher-ID. |
| `sdid_high` + `sdid_low` | `_experience.target.supplementalDataID` | Zeichenfolge | Trefferzusammenfügungs-ID. Die Analytics-Felder sdid_high und sdid_low sind die ergänzenden Daten-IDs, mit denen zwei (oder mehr) eingehende Treffer zusammengefügt werden. |
| `mobilebeaconproximity` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.proximity` | Zeichenfolge | Mobile Services – Beacon-Nähe. |
| `videochapter` | `media.mediaTimed.mediaChapter.`<br/>`chapterAssetReference._xmpDM.duration` | Ganzzahl | Der Name des Videokapitels. |
| `videolength` | `media.mediaTimed.primaryAssetReference.`<br/>`_xmpDM.duration` | Ganzzahl | Die Länge des Videos. |

{style="table-layout:auto"}

## Erweiterte Zuordnungsfelder

Markierte Felder (auch &quot;Nachwerte&quot;genannt) enthalten Daten, nachdem Adobe ihre Werte mithilfe von Verarbeitungsregeln, VISTA-Regeln und Suchtabellen angepasst hat. Die meisten Post-Werte haben ein vorverarbeitetes Gegenstück. Ihr Unternehmen kann entscheiden, ob Sie das vorverarbeitete Feld, das Feld nach der Verarbeitung oder beides verwenden möchten.

Weitere Informationen zum Ausführen dieser Umwandlungen mithilfe von Query Service finden Sie unter [Adobe-definierte Funktionen](/help/query-service/sql/adobe-defined-functions.md) im Benutzerhandbuch zu Query Service.

| Analytics-Feld | XDM-Feld | XDM-Typ | Beschreibung |
| --------------- | --------- | -------- | ---------- |
| `post_evar1`<br/>`[...]`<br/>`post_evar250` | `_experience.analytics.customDimensions.`<br/>`eVars.eVar1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`eVars.eVar250` | string | Benutzerdefinierte Analytics-eVars. Jede Organisation kann eVars anders verwenden. |
| `post_prop1`<br/>`[...]`<br/>`post_prop75` | `_experience.analytics.customDimensions.`<br/>`props.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`props.prop75` | Zeichenfolge | Benutzerdefinierte Analytics-Eigenschaften. Jede Organisation kann Props unterschiedlich verwenden. |
| `post_browser_height` | `environment.browserDetails.viewportHeight` | Ganzzahl | Höhe des Browsers in Pixel. |
| `post_browser_width` | `environment.browserDetails.viewportWidth` | Ganzzahl | Breite des Browsers in Pixel. |
| `post_campaign` | `marketing.trackingCode` | Zeichenfolge | Variable, die in der Dimension „Trackingcode“ verwendet wird. |
| `post_channel` | `web.webPageDetails.siteSection` | Zeichenfolge | Variable, die in der Dimension „Site-Bereiche“ verwendet wird. |
| `post_cust_visid` | `endUserIDs._experience.aacustomid.id` | Zeichenfolge | Benutzerdefinierte Besucher-ID, falls festgelegt. |
| `post_first_hit_page_url` | `_experience.analytics.endUser.`<br/>`firstWeb.webPageDetails.URL` | Zeichenfolge | URL der ersten Seite, zu der der Besucher gelangt. |
| `post_first_hit_pagename` | `_experience.analytics.endUser.`<br/>`firstWeb.webPageDetails.name` | Zeichenfolge | Variable, die in der Dimension „Ursprüngliche Entrypage“ verwendet wird. Seitenname der Entrypage des Besuchers. |
| `post_keywords` | `search.keywords` | Zeichenfolge | Die Keywords, die für den Treffer gesammelt wurden. |
| `post_page_url` | `web.webPageDetails.URL` | Zeichenfolge | URL des Seitenaufrufs. |
| `post_pagename_no_url` | `web.webPageDetails.name` | Zeichenfolge | Variable, die zum Ausfüllen der Dimension „Seiten“ dient. |
| `post_purchaseid` | `commerce.order.purchaseID` | Zeichenfolge | Variable, die zur eindeutigen Identifizierung von Käufen dient. |
| `post_referrer` | `web.webReferrer.URL` | Zeichenfolge | URL der vorherigen Seite. |
| `post_state` | `_experience.analytics.customDimensions.`<br/>`stateProvince` | Zeichenfolge | Statusvariable. |
| `post_user_server` | `web.webPageDetails.server` | Zeichenfolge | Variable, die in der Dimension „Server“ verwendet wird. |
| `post_zip` | `_experience.analytics.customDimensions.`<br/>`postalCode` | Zeichenfolge | Variable, die zum Ausfüllen der Dimension „Postleitzahl“ dient. |
| `browser` | `_experience.analytics.environment.`<br/>`browserID` | Ganzzahl | Numerische Kennung des Browsers. |
| `domain` | `environment.domain` | Zeichenfolge | Variable, die in der Dimension „Domain“ verwendet wird. Er basiert auf dem Internetdienstanbieter (ISP) des Benutzers. |
| `first_hit_referrer` | `_experience.analytics.endUser.`<br/>`firstWeb.webReferrer.URL` | Zeichenfolge | Die erste verweisende URL für den Besucher. |
| `geo_city` | `placeContext.geo.city` | Zeichenfolge | Name der Stadt des Treffers. Dies basiert auf der IP-Adresse des Treffers. |
| `geo_dma` | `placeContext.geo.dmaID` | Ganzzahl | Numerische Kennung des demografischen Bereichs für den Treffer. Dies basiert auf der IP-Adresse des Treffers. |
| `geo_region` | `placeContext.geo.stateProvince` | Zeichenfolge | Name des Bundeslands oder der Region des Treffers. Dies basiert auf der IP-Adresse des Treffers. |
| `geo_zip` | `placeContext.geo.postalCode` | Zeichenfolge | Postleitzahl des Treffers. Dies basiert auf der IP-Adresse des Treffers. |
| `os` | `_experience.analytics.environment.`<br/>`operatingSystemID` | Ganzzahl | Numerische Kennung, die das Betriebssystem des Besuchers darstellt. Dieser Wert basiert auf der Spalte „user_agent“. |
| `search_page_num` | `search.pageDepth` | Ganzzahl | Diese Variable wird von der Dimension „Rangansicht aller Suchseiten“ verwendet und gibt an, auf welcher Seite mit Suchergebnissen Ihre Site angezeigt | wurde, bevor sich der Benutzer durch Ihre Site geklickt hat. |
| `visit_keywords` | `_experience.analytics.session.`<br/>`search.keywords` | Zeichenfolge | Variable, die in der Dimension „Keywords“ verwendet wird. |
| `visit_num` | `_experience.analytics.session.`<br/>`num` | Ganzzahl | Eine Variable, die in der Dimension „Besuchsnummer“ verwendet wird. Sie beginnt bei 1 und erhöht sich bei jedem neuen Besuch eines Benutzers. |
| `visit_page_num` | `_experience.analytics.session.`<br/>`depth` | Ganzzahl | Eine Variable, die in der Dimension „Treffertiefe“ verwendet wird. Der Wert erhöht sich bei jedem vom Benutzer generierten Treffer um 1 und wird nach jedem Besuch zurückgesetzt. |
| `visit_referrer` | `_experience.analytics.session.`<br/>`web.webReferrer.URL` | Zeichenfolge | Die erste verweisende Stelle des Besuchs. |
| `visit_search_page_num` | `_experience.analytics.session.`<br/>`search.pageDepth` | Ganzzahl | Der erste Seitenname des Besuchs. |
| `post_prop1`<br/>`[...]`<br/>`post_prop75` | `_experience.analytics.customDimensions.`<br/>`listprops.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`listprops.prop75` | Objekt | Benutzerdefinierte Analytics-Eigenschaften, die als Listen-Props konfiguriert sind. Sie enthält eine durch Trennzeichen getrennte Liste von Werten. |
| `post_hier1`<br/>`[...]`<br/>`post_hier5` | `_experience.analytics.customDimensions.`<br/>`hierarchies.hier1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`hierarchies.hier5` | Objekt | Wird von Hierarchievariablen verwendet und enthält eine durch Trennzeichen getrennte Liste von Werten. | {values (array), delimiter (string)} |
| `post_mvvar1`<br/>`[...]`<br/>`post_mvvar3` | `_experience.analytics.customDimensions.`<br/>`lists.list1.list[]`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`lists.list3.list[]` | array | Eine Liste mit Variablenwerten. Enthält eine durch Trennzeichen getrennte Liste benutzerdefinierter Werte (je nach Implementierung). | {value (string), key (string)} |
| `post_cookies` | `environment.browserDetails.cookiesEnabled` | Boolescher Wert | Die Variable, die in der Dimension „Cookie-Unterstützung“ verwendet wird. |
| `post_event_list` | `commerce.purchases`,<br/>`commerce.productViews`,<br/>`commerce.productListOpens`,<br/>`commerce.checkouts`,<br/>`commerce.productListAdds`,<br/>`commerce.productListRemovals`,<br/>`commerce.productListViews` | Objekt | Beim Treffer ausgelöste Standard-Verkaufsereignisse. | {id (string), value (number)} |
| `post_event_list` | `_experience.analytics.event1to100.event1`<br/>`[...]`<br/>`_experience.analytics.event901to1000.event1000` | Objekt | Benutzerdefinierte Ereignisse, die beim Treffer ausgelöst werden. | {id (Object), value (Object)} |
| `post_java_enabled` | `environment.browserDetails.javaEnabled` | boolean | Eine Markierung, die angibt, ob Java™ aktiviert ist. |
| `post_latitude` | `placeContext.geo._schema.latitude` | number | <!-- MISSING --> |
| `post_longitude` | `placeContext.geo._schema.longitude` | number | <!-- MISSING --> |
| `post_page_event` | `web.webInteraction.type` | Zeichenfolge | Die Art des in der Bildanforderung gesendeten Treffers (Standardtreffer, angeklickter Downloadlink, Exitlink oder benutzerspezifischer Link). |
| `post_page_event` | `web.webInteraction.linkClicks.value` | number | Die Art des in der Bildanforderung gesendeten Treffers (Standardtreffer, angeklickter Downloadlink, Exitlink oder benutzerspezifischer Link). |
| `post_page_event_var1` | `web.webInteraction.URL` | Zeichenfolge | Diese Variable wird nur bei Bildanforderungen zum Linktracking verwendet. Dies ist die URL des angeklickten Downloadlinks, Exitlinks oder benutzerspezifischen Links. |
| `post_page_event_var2` | `web.webInteraction.name` | Zeichenfolge | Diese Variable wird nur bei Bildanforderungen zum Linktracking verwendet. Dies ist der benutzerdefinierte Name des Links. |
| `post_page_type` | `web.webPageDetails.isErrorPage` | Boolescher Wert | Damit wird die Dimension „Seiten nicht gefunden“ ausgefüllt. Diese Variable sollte entweder leer sein oder „ErrorPage“ enthalten. |
| `post_pagename_no_url` | `web.webPageDetails.pageViews.value` | number | Der Name der Seite (wenn festgelegt). Wenn keine Seite angegeben ist, bleibt dieser Wert leer. |
| `post_product_list` | `productListItems[].items` | array | Produktliste, so wie sie von der Variable der Produkte übergeben wurde. | {SKU (string), quantity (integer), priceTotal (number)} |
| `post_search_engine` | `search.searchEngine` | Zeichenfolge | Numerische Kennung, die die Suchmaschine darstellt, die den Besucher auf Ihre Site verwiesen hat. |
| `mvvar1_instances` | `.list.items[]` | Objekt | Liste mit Variablenwerten. Enthält eine durch Trennzeichen getrennte Liste benutzerdefinierter Werte (je nach Implementierung). |
| `mvvar2_instances` | `.list.items[]` | Objekt | Liste mit Variablenwerten. Enthält eine durch Trennzeichen getrennte Liste benutzerdefinierter Werte (je nach Implementierung). |
| `mvvar3_instances` | `.list.items[]` | Objekt | Liste mit Variablenwerten. Enthält eine durch Trennzeichen getrennte Liste benutzerdefinierter Werte (je nach Implementierung). |
| `color` | `device.colorDepth` | Ganzzahl | Farbtiefen-ID, basierend auf dem Wert der Spalte „c_color“. |
| `first_hit_ref_type` | `_experience.analytics.endUser.`<br/>`firstWeb.webReferrer.type` | Zeichenfolge | Numerische ID, die den Typ der verweisenden Stelle der ersten verweisenden Stelle des Besuchers darstellt. |
| `first_hit_time_gmt` | `_experience.analytics.endUser.`<br/>`firstTimestamp` | integer | Zeitstempel des ersten Treffers des Besuchers in UNIX®-Zeit. |
| `geo_country` | `placeContext.geo.countryCode` | Zeichenfolge | Abkürzung für das Land, aus dem der Treffer stammt, basierend auf der IP-Adresse. |
| `geo_latitude` | `placeContext.geo._schema.latitude` | number | <!-- MISSING --> |
| `geo_longitude` | `placeContext.geo._schema.longitude` | number | <!-- MISSING --> |
| `paid_search` | `search.isPaid` | Boolescher Wert | Markierung, die gesetzt wird, wenn der Treffer mit der Paid Search-Erkennung übereinstimmt. |
| `ref_type` | `web.webReferrer.type` | Zeichenfolge | Eine numerische ID, die den Typ des Verweises für den Treffer darstellt. |
| `visit_paid_search` | `_experience.analytics.session.`<br/>`search.isPaid` | Boolescher Wert | Eine Markierung (1 = paid, 0 = not paid), die angibt, ob der erste Treffer des Besuchs ein Paid Search-Treffer war oder nicht. |
| `visit_ref_type` | `_experience.analytics.session.`<br/>`web.webReferrer.type` | Zeichenfolge | Numerische ID des Typs der verweisenden Stelle der ersten verweisenden Stelle des Besuchs. |
| `visit_search_engine` | `_experience.analytics.session.`<br/>`search.searchEngine` | Zeichenfolge | Numerische ID der ersten Suchmaschine des Besuchs. |
| `visit_start_time_gmt` | `_experience.analytics.session.`<br/>`timestamp` | integer | Zeitstempel des ersten Treffers des Besuchs in UNIX®-Zeit. |

{style="table-layout:auto"}