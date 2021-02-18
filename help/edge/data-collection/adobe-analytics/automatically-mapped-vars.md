---
title: Automatisch zugeordnete Adobe Analytics-Variablen im Adobe Experience Platform Web SDK
description: Erfahren Sie, welche Variablen in Adobe Analytics automatisch mit dem Experience Platform Web SDK zugeordnet werden.
seo-description: Erfahren Sie, welche Variablen in Adobe Analytics mit dem Adobe Experience Platform Web SDK automatisch zugeordnet werden.
keywords: adobe analytics;variables;analytics;automate map;automatisch zugeordnet;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '681'
ht-degree: 35%

---


# Variablen werden automatisch in [!DNL Analytics] zugeordnet

Nachfolgend finden Sie eine Liste von Variablen, die Adobe Experience Platform Edge Network automatisch Adobe Analytics zuordnet.

| XDM-Feldpfad | [!DNL Analytics Query String] / HTTP-Header | Beschreibung |
| ---------- | ------------------------- | ----------------------------------------- |
| `application.id` | `c.a.appid` | AppMeasurement-Kontextdatenzuordnung `c.a.appid`. |
| `application.launches.value` | `c.a.launches` | AppMeasurement-Kontextdatenzuordnung `c.a.launches`. |
| `commerce.checkouts.id` | `events` | `scCheckout` Ereignis-Serialisierung. Wenn dieses Feld ausgeschlossen wird (d. h. bei nicht mehr verwendeten Ereignissen), generiert das System einen eigenen ID-Wert und weist ihn der Entität zu. |
| `commerce.checkouts.value` | `events` | AppMeasurement-Abfrage-Parameter EREIGNIS_LISTE_FULL-Zuordnung mit der Konvertierung COMMERCE_SC_CHECKOUT unter Verwendung des Trennzeichens `,`. |
| `commerce.order.currencyCode` | `cc` | AppMeasurement-Abfrageparameter, CURRENCY-Zuordnung. |
| `commerce.order.purchaseID` | `pi` | AppMeasurement Abfrageparameter, PURCHASEID-Zuordnung. |
| `commerce.productListAdds.id` | `events` | `scAdd` Ereignis-Serialisierung. Wenn dieses Feld ausgeschlossen wird (d. h. bei nicht mehr verwendeten Ereignissen), generiert das System einen eigenen ID-Wert und weist ihn der Entität zu. |
| `commerce.productListAdds.value` | `events` | AppMeasurement-Abfrage-Parameter EREIGNIS_LISTE_FULL-Zuordnung mit der Konvertierung COMMERCE_SC_HINZUFÜGEN unter Verwendung des Trennzeichens `,`. |
| `commerce.productListOpens.id` | `events` | `scOpen` Ereignis-Serialisierung. Wenn dieses Feld ausgeschlossen wird (d. h. bei nicht mehr verwendeten Ereignissen), generiert das System einen eigenen ID-Wert und weist ihn der Entität zu. |
| `commerce.productListOpens.value` | `events` | AppMeasurement-Abfrage-Parameter EREIGNIS_LISTE_FULL-Zuordnung mit der Konvertierung COMMERCE_SC_OPEN unter Verwendung des Trennzeichens `,`. |
| `commerce.productListRemovals.id` | `events` | `scRemove` Ereignis-Serialisierung. Wenn dieses Feld ausgeschlossen wird (d. h. bei nicht mehr verwendeten Ereignissen), generiert das System einen eigenen ID-Wert und weist ihn der Entität zu. |
| `commerce.productListRemovals.value` | `events` | AppMeasurement-Abfrage-Parameter EREIGNIS_LISTE_FULL-Zuordnung mit der Konvertierung COMMERCE_SC_REMOVE unter Verwendung des Trennzeichens `,`. |
| `commerce.productListViews.id` | `events` | `scView` Ereignis-Serialisierung. Wenn dieses Feld ausgeschlossen wird (d. h. bei nicht mehr verwendeten Ereignissen), generiert das System einen eigenen ID-Wert und weist ihn der Entität zu. |
| `commerce.productListViews.value` | `events` | AppMeasurement-Abfrage-Parameter EREIGNIS_LISTE_FULL-Zuordnung mit der KonversionsCOMMERCE_SC_ANSICHT unter Verwendung des Trennzeichens `,`. |
| `commerce.productViews.id` | `events` | `prodView` Ereignis-Serialisierung. Wenn dieses Feld ausgeschlossen wird (d. h. bei nicht mehr verwendeten Ereignissen), generiert das System einen eigenen ID-Wert und weist ihn der Entität zu. |
| `commerce.productViews.value` | `events` | AppMeasurement-Abfrage-Parameter EREIGNIS_LISTE_FULL-Zuordnung mit KonversionsCOMMERCE_Referrer_ANSICHT unter Verwendung des Trennzeichens `,`. |
| `commerce.purchases.value` | `events` | AppMeasurement-Abfrage-Parameter EREIGNIS_LISTE_FULL-Zuordnung mit KonversionsCOMMERCE_PURCHASE unter Verwendung des Trennzeichens `,`. |
| `device.colorDepth` | `c` | AppMeasurement-Abfrageparameter, C_COLOR-Zuordnung. |
| `device.screenHeight` | `s` | AppMeasurement Abfrage-Parameterzuordnung Bildschirmauflösung. |
| `device.screenWidth` | `s` | AppMeasurement Abfrage-Parameterzuordnung Bildschirmauflösung. |
| `environment.browserDetails.acceptLanguage` | `Accept-Language` | Dies ist eine HTTP-Kopfzeilen-Zuordnung, HEADER_ACCEPT_LANGUAGE. |
| `environment.browserDetails.cookiesEnabled` | `k` | AppMeasurement-Abfrageparameter, COOKIES-Zuordnung mit der Konvertierung BOOLEAN_TO_YN. |
| `environment.browserDetails.javaEnabled` | `v` | AppMeasurement-Abfrageparameter, JAVA_ENABLED-Zuordnung mit der Konvertierung BOOLEAN_TO_YN. |
| `environment.browserDetails.javaScriptVersion` | `j` | AppMeasurement-Abfrageparameter, J_JSCRIPT-Zuordnung. |
| `environment.browserDetails.userAgent` | `User-Agent` | Dies ist eine HTTP-Kopfzeilen-Zuordnung, HEADER_USER_AGENT. |
| `environment.browserDetails.viewportHeight` | `bh` | AppMeasurement-Abfrageparameter, BROWSER_HEIGHT-Zuordnung. |
| `environment.browserDetails.viewportWidth` | `bw` | AppMeasurement-Abfrageparameter, BROWSER_WIDTH-Zuordnung. |
| `environment.connectionType` | `ct` | AppMeasurement-Abfrageparameter, CT_CONNECT_TYPE-Zuordnung. |
| `environment.ipV4` | `X-Forwarded-For` | Dies ist eine HTTP-Header-Zuordnung, X-FORWARDED-FOR. |
| `identityMap.ECID.[0].id` | `mid` | AppMeasurement-Abfrageparameter, MID-Zuordnung. |
| `marketing.trackingCode` | `v0` | AppMeasurement Abfrageparameter, CAMPAIGN-Zuordnung. |
| `media.mediaTimed.completes.value` | `c.a.media.complete` | AppMeasurement-Kontextdaten. |
| `media.mediaTimed.dropBeforeStart.value` | `c.a.media.view`, `c.a.media.timePlayed`, `c.a.media.play` | AppMeasurement-Kontextdaten. |
| `media.mediaTimed.federated.value` | `c.a.media.federated` | AppMeasurement-Kontextdatenzuordnung `c.a.media.federated`. |
| `media.mediaTimed.firstQuartiles.value` | `c.a.media.progress25` | AppMeasurement-Kontextdaten. |
| `media.mediaTimed.mediaSegmentView.value` | `c.a.media.segmentView` | AppMeasurement-Kontextdaten. |
| `media.mediaTimed.midpoints.value` | `c.a.media.progress50` | AppMeasurement-Kontextdaten. |
| `media.mediaTimed.pauseTime.value` | `c.a.media.pauseTime` | AppMeasurement-Kontextdatenzuordnung `c.a.media.pauseTime`. |
| `media.mediaTimed.pauses.value` | `c.a.media.pauseCount` | AppMeasurement-Kontextdatenzuordnung `c.a.media.pauseCount`. |
| `media.mediaTimed.primaryAssetReference.@id` | `c.a.media.asset` | AppMeasurement-Kontextdaten. |
| `media.mediaTimed.primaryAssetReference.dc:title` | `c.a.media.friendlyName` | AppMeasurement-Kontextdatenzuordnung `c.a.media.friendlyName`. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Creator.[N].iptc4xmpExt:Name` | `c.a.media.originator` | AppMeasurement-Kontextdaten. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Episode.iptc4xmpExt:Number` | `c.a.media.episode` | AppMeasurement-Kontextdatenzuordnung `c.a.media.episode`. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Genre` | `c.a.media.genre` | AppMeasurement-Kontextdaten. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Rating.[N].iptc4xmpExt:RatingValue` | `c.a.media.rating` | AppMeasurement-Kontextdaten. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Season.iptc4xmpExt:Number` | `c.a.media.season` | AppMeasurement-Kontextdatenzuordnung `c.a.media.season`. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Identifier` | `a.media.name` | AppMeasurement-Kontextdatenzuordnung `a.media.name`. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Name` | `c.a.media.show` | AppMeasurement-Kontextdatenzuordnung `c.a.media.show`. |
| `media.mediaTimed.primaryAssetReference.showType` | `c.a.media.type` | AppMeasurement-Kontextdatenzuordnung `c.a.media.type` mit Konvertierung VEDIO_SHOW_TYPE. |
| `media.mediaTimed.primaryAssetReference.showType` | `c.a.media.type` | AppMeasurement-Kontextdaten `c.a.media.type`-Zuordnung mit KonversionsVIDEO_SHOW_TYPE. |
| `media.mediaTimed.primaryAssetReference.xmpDM:duration` | `c.a.media.length` | AppMeasurement-Kontextdatenzuordnung `c.a.media.length`. |
| `media.mediaTimed.primaryAssetViewDetails.@id` | `c.a.media.vsid` | AppMeasurement-Kontextdaten. |
| `media.mediaTimed.primaryAssetViewDetails.broadcastChannel` | `c.a.media.channel` | AppMeasurement-Kontextdatenzuordnung `c.a.media.channel`. |
| `media.mediaTimed.primaryAssetViewDetails.broadcastContentType` | `c.a.contentType` | AppMeasurement-Kontextdatenzuordnung `c.a.contentType`. |
| `media.mediaTimed.primaryAssetViewDetails.broadcastNetwork` | `c.a.media.network` | AppMeasurement-Kontextdatenzuordnung `c.a.media.network`. |
| `media.mediaTimed.primaryAssetViewDetails.mediaSegmentView.value` | `c.a.media.segment` | AppMeasurement-Kontextdatenzuordnung `c.a.media.segment`. |
| `media.mediaTimed.primaryAssetViewDetails.playerName` | `c.a.media.playerName` | AppMeasurement-Kontextdatenzuordnung `c.a.media.playerName`. |
| `media.mediaTimed.primaryAssetViewDetails.playerSDKVersion.version` | `c.a.media.sdkVersion` | AppMeasurement-Kontextdatenzuordnung `c.a.media.sdkVersion`. |
| `media.mediaTimed.primaryAssetViewDetails.sourceFeed` | `c.a.media.feed` | AppMeasurement-Kontextdatenzuordnung `c.a.media.feed`. |
| `media.mediaTimed.primaryAssetViewDetails.streamFormat` | `c.a.media.format` | AppMeasurement-Kontextdatenzuordnung `c.a.media.format`. |
| `media.mediaTimed.progress10.value` | `c.a.media.progress10` | AppMeasurement-Kontextdaten. |
| `media.mediaTimed.progress95.value` | `c.a.media.progress95` | AppMeasurement-Kontextdaten. |
| `media.mediaTimed.resumes.value` | `c.a.media.resume` | AppMeasurement-Kontextdatenzuordnung `c.a.media.resume`. |
| `media.mediaTimed.starts.value` | `c.a.media.view` | AppMeasurement-Kontextdaten. |
| `media.mediaTimed.thirdQuartiles.value` | `c.a.media.progress75` | AppMeasurement-Kontextdaten. |
| `media.mediaTimed.timePlayed.value` | `c.a.media.timePlayed` | AppMeasurement-Kontextdatenzuordnung `c.a.media.timePlayed`. |
| `media.mediaTimed.totalTimePlayed.value` | `c.a.media.totalTimePlayed` | AppMeasurement-Kontextdatenzuordnung `c.a.media.totalTimePlayed`. |
| `placeContext.geo.latitude` | `lat` | AppMeasurement Abfrageparameter, LATITUDE-Zuordnung. |
| `placeContext.geo.longitude` | `lon` | AppMeasurement Abfrageparameter, LONGITUDE-Zuordnung. |
| `placeContext.geo.postalCode` | `zip` | AppMeasurement Abfrageparameter, ZIP-Zuordnung. |
| `placeContext.geo.stateProvince` | `state` | AppMeasurement Abfrageparameter, STATE-Zuordnung. |
| `productlistitems.[N]._[NAME_SPACE].*` | `products` | AppMeasurement Abfrage-Parameter Produktvermarktungs-Ereignis/eVars-Zuordnung. |
| `productlistitems.[N].name` | `products` | AppMeasurement Abfrage Parameter Produktnamenzuordnung. |
| `productlistitems.[N].priceTotal` | `products` | AppMeasurement Abfrage-Parameter Produktpreiszuordnung. |
| `productlistitems.[N].quantity` | `products` | AppMeasurement Abfrage-Parameter Produktmengenzuordnung. |
| `web.webInteraction.URL` | `pev1` | AppMeasurement-Abfrage-Parameter PAGE_EREIGNIS_VAR1-Zuordnung. |
| `web.webInteraction.name` | `pev2` | AppMeasurement-Abfrage-Parameter PAGE_EREIGNIS_VAR2-Zuordnung. |
| `web.webInteraction.type` | `pe` | `web.webInteraction.type=other` nach  `pe=lnk_o`;  `web.webInteraction.type=download` nach  `pe=lnk_d`;  `web.webInteraction.type=exit` nach  `pe=lnk_e` |
| `web.webPageDetails.URL` | `g` | AppMeasurement Abfrageparameter, PAGE_URL-Zuordnung. |
| `web.webPageDetails.errorPage` | `pageType` | AppMeasurement-Abfrage-Parameter PAGE_TYPE_FULL-Zuordnung mit Konversion ERROR_PAGE_TYPE. |
| `web.webPageDetails.homePage` | `hp` | AppMeasurement-Abfrageparameter, HOMEPAGE-Zuordnung mit der Konvertierung BOOLEAN_TO_YN. |
| `web.webPageDetails.name` | `gn` | AppMeasurement Abfrageparameter, PAGENAME-Zuordnung. |
| `web.webPageDetails.server` | `sv` | AppMeasurement Abfrageparameter, USER_SERVER-Zuordnung. |
| `web.webPageDetails.siteSection` | `ch` | AppMeasurement Abfrage-Parameterzuordnung für KANAL. |
| `web.webReferrer.URL` | `r` | AppMeasurement Abfrageparameter, REFERRER-Zuordnung. |
