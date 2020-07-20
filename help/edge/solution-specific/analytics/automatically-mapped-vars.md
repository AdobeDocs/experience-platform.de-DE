---
title: In Analytics automatisch zugeordnete Variablen
seo-title: Variablen, die in Analytics automatisch mit dem Adobe Experience Platform Web SDK zugeordnet werden
description: Erfahren Sie, welche Variablen in Analytics mit dem Experience Platform Web SDK automatisch zugeordnet werden
seo-description: Erfahren Sie, welche Variablen in Analytics mit dem Experience Platform Web SDK automatisch zugeordnet werden
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 55%

---


# In automatisch zugeordnete Variablen[!DNL Analytics]

Below is a list of variables that the Adobe Experience Platform [!DNL Edge Network] automatically maps into [!DNL Analytics].

| XDM-Feldpfad | [!DNL Analytics Query String] / HTTP-Header | Beschreibung |
| ---------- | ------------------------- | -------- |
| `commerce.order.purchaseID` | `pi` | AppMeasurement Abfrageparameter, PURCHASEID-Zuordnung. |
| `commerce.order.currencyCode` | `cc` | AppMeasurement-Abfrageparameter, CURRENCY-Zuordnung. |
| `commerce.purchases.value` | `events` | AppMeasurement-Abfrage-Parameter EREIGNIS_LISTE_FULL-Zuordnung mit Konversions-COMMERCE_PURCHASE unter Verwendung des Trennzeichens `,`. |
| `commerce.productViews.value` | `events` | AppMeasurement-Abfrage-Parameter EREIGNIS_LISTE_FULL-Zuordnung mit der Konvertierung COMMERCE_Referrer_ANSICHT unter Verwendung des Trennzeichens `,`. |
| `commerce.productListOpens.value` | `events` | AppMeasurement-Abfrage-Parameter EREIGNIS_LISTE_FULL-Zuordnung mit der Konvertierung COMMERCE_SC_OPEN unter Verwendung des Trennzeichens `,`. |
| `commerce.productListViews.value` | `events` | AppMeasurement-Abfrage-Parameter EREIGNIS_LISTE_FULL-Zuordnung mit der KonversionsCOMMERCE_SC_ANSICHT unter Verwendung des Trennzeichens `,`. |
| `commerce.checkouts.value` | `events` | AppMeasurement-Abfrage-Parameter EREIGNIS_LISTE_FULL-Zuordnung mit der Konvertierung COMMERCE_SC_CHECKOUT unter Verwendung des Trennzeichens `,`. |
| `commerce.productListAdds.value` | `events` | AppMeasurement-Abfrage-Parameter EREIGNIS_LISTE_FULL-Zuordnung mit der Konvertierung COMMERCE_SC_HINZUFÜGEN unter Verwendung des Trennzeichens `,`. |
| `commerce.productListRemovals.value` | `events` | AppMeasurement-Abfrage-Parameter EREIGNIS_LISTE_FULL-Zuordnung mit der Konvertierung COMMERCE_SC_REMOVE unter Verwendung des Trennzeichens `,`. |
| `commerce.productViews.id` | `events` | `prodView` Ereignis-Serialisierung. |
| `commerce.productListOpens.id` | `events` | `scOpen` Ereignis-Serialisierung. |
| `commerce.productListViews.id` | `events` | `scView` Ereignis-Serialisierung. |
| `commerce.productListAdds.id` | `events` | `scAdd` Ereignis-Serialisierung. |
| `commerce.productListRemovals.id` | `events` | `scRemove` Ereignis-Serialisierung. |
| `commerce.checkouts.id` | `events` | `scCheckout` Ereignis-Serialisierung. |
| `device.screenHeight` | `s` | AppMeasurement Abfrage-Parameterzuordnung Bildschirmauflösung. |
| `device.screenWidth` | `s` | AppMeasurement Abfrage-Parameterzuordnung Bildschirmauflösung. |
| `productlistitems.[N].lineitemid` | `products` | AppMeasurement Abfrage-Parameter Produktzuordnung für Kategorien. |
| `productlistitems.[N].name` | `products` | AppMeasurement Abfrage Parameter Produktnamenzuordnung. |
| `productlistitems.[N].quantity` | `products` | AppMeasurement Abfrage-Parameter Produktmengenzuordnung. |
| `productlistitems.[N].pricetotal` | `products` | AppMeasurement Abfrage-Parameter Produktpreiszuordnung. |
| `media.mediaTimed.primaryAssetViewDetails.@id` | `c.a.media.vsid` | AppMeasurement-Kontextdaten. |
| `media.mediaTimed.primaryAssetReference.@id` | `c.a.media.asset` | AppMeasurement-Kontextdaten. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Rating.[N].iptc4xmpExt:RatingValue` | `c.a.media.rating` | AppMeasurement-Kontextdaten. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Genre` | `c.a.media.genre` | AppMeasurement-Kontextdaten. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Creator.[N].iptc4xmpExt:Name` | `c.a.media.originator` | AppMeasurement-Kontextdaten. |
| `media.mediaTimed.starts.value` | `c.a.media.view` | AppMeasurement-Kontextdaten. |
| `media.mediaTimed.progress10.value` | `c.a.media.progress10` | AppMeasurement-Kontextdaten. |
| `media.mediaTimed.firstQuartiles.value` | `c.a.media.progress25` | AppMeasurement-Kontextdaten. |
| `media.mediaTimed.midpoints.value` | `c.a.media.progress50` | AppMeasurement-Kontextdaten. |
| `media.mediaTimed.thirdQuartiles.value` | `c.a.media.progress75` | AppMeasurement-Kontextdaten. |
| `media.mediaTimed.progress95.value` | `c.a.media.progress95` | AppMeasurement-Kontextdaten. |
| `media.mediaTimed.completes.value` | `c.a.media.complete` | AppMeasurement-Kontextdaten. |
| `media.mediaTimed.mediaSegmentView.value` | `c.a.media.segmentView` | AppMeasurement-Kontextdaten. |
| `media.mediaTimed.dropBeforeStart.value` | `c.a.media.view`, `c.a.media.timePlayed`, `c.a.media.play` | AppMeasurement-Kontextdaten. |
| `environment.browserDetails.userAgent` | `User-Agent` | Dies ist eine HTTP-Kopfzeilen-Zuordnung, HEADER_USER_AGENT. |
| `environment.browserDetails.acceptLanguage` | `Accept-Language` | Dies ist eine HTTP-Kopfzeilen-Zuordnung, HEADER_ACCEPT_LANGUAGE. |
| `environment.browserDetails.cookiesEnabled` | `k` | AppMeasurement-Abfrageparameter, COOKIES-Zuordnung mit der Konvertierung BOOLEAN_TO_YN. |
| `environment.browserDetails.javaScriptVersion` | `j` | AppMeasurement-Abfrageparameter, J_JSCRIPT-Zuordnung. |
| `environment.browserDetails.javaEnabled` | `v` | AppMeasurement-Abfrageparameter, JAVA_ENABLED-Zuordnung mit der Konvertierung BOOLEAN_TO_YN. |
| `environment.browserDetails.viewportHeight` | `bh` | AppMeasurement-Abfrageparameter, BROWSER_HEIGHT-Zuordnung. |
| `environment.browserDetails.viewportWidth` | `bw` | AppMeasurement-Abfrageparameter, BROWSER_WIDTH-Zuordnung. |
| `environment.connectionType` | `ct` | AppMeasurement-Abfrageparameter, CT_CONNECT_TYPE-Zuordnung. |
| `device.colorDepth` | `c` | AppMeasurement-Abfrageparameter, C_COLOR-Zuordnung. |
| `placeContext.geo.stateProvince` | `state` | AppMeasurement Abfrageparameter, STATE-Zuordnung. |
| `placeContext.geo.postalCode` | `zip` | AppMeasurement Abfrageparameter, ZIP-Zuordnung. |
| `placeContext.geo.latitude` | `lat` | AppMeasurement Abfrageparameter, LATITUDE-Zuordnung. |
| `placeContext.geo.longitude` | `lon` | AppMeasurement Abfrageparameter, LONGITUDE-Zuordnung. |
| `web.webPageDetails.server` | `sv` | AppMeasurement Abfrageparameter, USER_SERVER-Zuordnung. |
| `web.webPageDetails.name` | `gn` | AppMeasurement Abfrageparameter, PAGENAME-Zuordnung. |
| `web.webPageDetails.URL` | `g` | AppMeasurement Abfrageparameter, PAGE_URL-Zuordnung. |
| `web.webPageDetails.homePage` | `hp` | AppMeasurement-Abfrageparameter, HOMEPAGE-Zuordnung mit der Konvertierung BOOLEAN_TO_YN. |
| `web.webReferrer.URL` | `r` | AppMeasurement Abfrageparameter, REFERRER-Zuordnung. |
| `web.webInteraction.type` | `pe` | AppMeasurement-Abfrage-Parameter PAGE_EREIGNIS-Zuordnung mit Konversion CLICK_MAP_TYPE. |
| `web.webInteraction.URL` | `pev1` | AppMeasurement-Abfrage-Parameter PAGE_EREIGNIS_VAR1-Zuordnung. |
| `web.webInteraction.name` | `pev2` | AppMeasurement-Abfrage-Parameter PAGE_EREIGNIS_VAR2-Zuordnung. |
| `web.webPageDetails.siteSection` | `ch` | AppMeasurement Abfrage-Parameterzuordnung für KANAL. |
| `web.webPageDetails.errorPage` | `pageType` | AppMeasurement-Abfrage-Parameter PAGE_TYPE_FULL-Zuordnung mit Konversion ERROR_PAGE_TYPE. |
| `application.id` | `c.a.appid` | AppMeasurement-Kontextdatenzuordnung `c.a.appid`. |
| `application.launches.value` | `c.a.launches` | AppMeasurement-Kontextdatenzuordnung `c.a.launches`. |
| `marketing.trackingCode` | `v0` | AppMeasurement Abfrageparameter, CAMPAIGN-Zuordnung. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Identifier` | `a.media.name` | AppMeasurement-Kontextdatenzuordnung `a.media.name`. |
| `media.mediaTimed.primaryAssetReference.xmpDM:duration` | `c.a.media.length` | AppMeasurement-Kontextdatenzuordnung `c.a.media.length`. |
| `media.mediaTimed.primaryAssetViewDetails.broadcastContentType` | `c.a.contentType` | AppMeasurement-Kontextdatenzuordnung `c.a.contentType`. |
| `media.mediaTimed.primaryAssetViewDetails.playerName` | `c.a.media.playerName` | AppMeasurement-Kontextdatenzuordnung `c.a.media.playerName`. |
| `media.mediaTimed.primaryAssetViewDetails.broadcastChannel` | `c.a.media.channel` | AppMeasurement-Kontextdatenzuordnung `c.a.media.channel`. |
| `media.mediaTimed.primaryAssetViewDetails.mediaSegmentView.value` | `c.a.media.segment` | AppMeasurement-Kontextdatenzuordnung `c.a.media.segment`. |
| `media.mediaTimed.primaryAssetReference.dc:title` | `c.a.media.friendlyName` | AppMeasurement-Kontextdatenzuordnung `c.a.media.friendlyName`. |
| `media.mediaTimed.primaryAssetViewDetails.playerSDKVersion.version` | `c.a.media.sdkVersion` | AppMeasurement-Kontextdatenzuordnung `c.a.media.sdkVersion`. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Name` | `c.a.media.show` | AppMeasurement-Kontextdatenzuordnung `c.a.media.show`. |
| `media.mediaTimed.primaryAssetViewDetails.streamFormat` | `c.a.media.format` | AppMeasurement-Kontextdatenzuordnung `c.a.media.format`. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Season.iptc4xmpExt:Number` | `c.a.media.season` | AppMeasurement-Kontextdatenzuordnung `c.a.media.season`. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Episode.iptc4xmpExt:Number` | `c.a.media.episode` | AppMeasurement-Kontextdatenzuordnung `c.a.media.episode`. |
| `media.mediaTimed.primaryAssetViewDetails.broadcastNetwork` | `c.a.media.network` | AppMeasurement-Kontextdatenzuordnung `c.a.media.network`. |
| `media.mediaTimed.primaryAssetReference.showType` | `c.a.media.type` | AppMeasurement-Kontextdatenzuordnung `c.a.media.type` mit Konvertierung VEDIO_SHOW_TYPE. |
| `media.mediaTimed.primaryAssetViewDetails.sourceFeed` | `c.a.media.feed` | AppMeasurement-Kontextdatenzuordnung `c.a.media.feed`. |
| `media.mediaTimed.timePlayed.value` | `c.a.media.timePlayed` | AppMeasurement-Kontextdatenzuordnung `c.a.media.timePlayed`. |
| `media.mediaTimed.totalTimePlayed.value` | `c.a.media.totalTimePlayed` | AppMeasurement-Kontextdatenzuordnung `c.a.media.totalTimePlayed`. |
| `media.mediaTimed.federated.value` | `c.a.media.federated` | AppMeasurement-Kontextdatenzuordnung `c.a.media.federated`. |
| `media.mediaTimed.pauses.value` | `c.a.media.pauseCount` | AppMeasurement-Kontextdatenzuordnung `c.a.media.pauseCount`. |
| `media.mediaTimed.pauseTime.value` | `c.a.media.pauseTime` | AppMeasurement-Kontextdatenzuordnung `c.a.media.pauseTime`. |
| `media.mediaTimed.resumes.value` | `c.a.media.resume` | AppMeasurement-Kontextdatenzuordnung `c.a.media.resume`. |
| `media.mediaTimed.primaryAssetReference.showType` | `c.a.media.type` | AppMeasurement context data `c.a.media.type` mapping with conversion VIDEO_SHOW_TYPE. |
| `identityMap.ECID.[0].id` | `mid` | AppMeasurement-Abfrageparameter, MID-Zuordnung. |
