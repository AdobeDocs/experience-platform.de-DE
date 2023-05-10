---
title: Automatisch zugeordnete Adobe Analytics-Variablen im Adobe Experience Platform Web SDK
description: Erfahren Sie, welche Variablen in Adobe Analytics automatisch mit dem Experience Platform Web SDK zugeordnet werden.
seo-description: Learn which variables are automatically mapped in Adobe Analytics with the Adobe Experience Platform Web SDK
keywords: Adobe Analytics; Variablen; Analytics; automatische Zuordnung; automatisch zugeordnet;
exl-id: 856fada7-b62c-4fd2-9372-a19ae1cdec33
source-git-commit: dcbe4c1b5a085878562990ed2db8e5cb27b93e28
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 35%

---

# Automatisch zugeordnete Variablen in [!DNL Analytics]

Nachstehend finden Sie eine Liste der Variablen, die das Adobe Experience Platform Edge Network automatisch Adobe Analytics zuordnet. Detaillierte Informationen zu den Adobe Analytics-Datenerfassungs-Abfrageparametern finden Sie im Abschnitt [Implementierungshandbuch für Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/validate/query-parameters.html?lang=de).

>[!NOTE]
>Die Informationen auf dieser Seite gelten auch für das Adobe Mobile SDK.

| XDM-Feldpfad | [!DNL Analytics Query String] / HTTP-Header | Beschreibung |
| ---------- | ------------------------- | ----------------------------------------- |
| application.id | c.a.appid | AppMeasurement-Kontextdatenzuordnung `c.a.appid`. |
| application.launches.value | c.a.launches | AppMeasurement-Kontextdatenzuordnung `c.a.launches`. |
| commerce.checkouts.id | Ereignisse | `scCheckout` Ereignis-Serialisierung. Wenn dieses Feld ausgeschlossen wird (d. h. bei nicht zu ersetzenden Ereignissen), generiert das System einen eigenen ID-Wert und weist ihn der Entität zu. |
| commerce.checkouts.value | Ereignisse | AppMeasurement-Abfrageparameter, EVENT_LIST_FULL-Zuordnung mit der Konvertierung COMMERCE_SC_CHECKOUT unter Verwendung des Trennzeichens `,`. |
| commerce.order.currencyCode | cc | AppMeasurement-Abfrageparameter, CURRENCY-Zuordnung. |
| commerce.order.purchaseID | pi | AppMeasurement Abfrageparameter, PURCHASEID-Zuordnung. |
| commerce.productListAdds.id | Ereignisse | `scAdd` Ereignis-Serialisierung. Wenn dieses Feld ausgeschlossen wird (d. h. bei nicht zu ersetzenden Ereignissen), generiert das System einen eigenen ID-Wert und weist ihn der Entität zu. |
| commerce.productListAdds.value | Ereignisse | AppMeasurement-Abfrageparameter, EVENT_LIST_FULL-Zuordnung mit der Konvertierung COMMERCE_SC_ADD, mithilfe des Trennzeichens `,`. |
| commerce.productListOpens.id | Ereignisse | `scOpen` Ereignis-Serialisierung. Wenn dieses Feld ausgeschlossen wird (d. h. bei nicht zu ersetzenden Ereignissen), generiert das System einen eigenen ID-Wert und weist ihn der Entität zu. |
| commerce.productListOpens.value | Ereignisse | AppMeasurement-Abfrageparameter, EVENT_LIST_FULL-Zuordnung mit der Konvertierung COMMERCE_SC_OPEN, mithilfe des Trennzeichens `,`. |
| commerce.productListRemovals.id | Ereignisse | `scRemove` Ereignis-Serialisierung. Wenn dieses Feld ausgeschlossen wird (d. h. bei nicht zu ersetzenden Ereignissen), generiert das System einen eigenen ID-Wert und weist ihn der Entität zu. |
| commerce.productListRemovals.value | Ereignisse | AppMeasurement-Abfrageparameter, EVENT_LIST_FULL-Zuordnung mit der Konvertierung COMMERCE_SC_REMOVE, mithilfe des Trennzeichens `,`. |
| commerce.productListViews.id | Ereignisse | `scView` Ereignis-Serialisierung. Wenn dieses Feld ausgeschlossen wird (d. h. bei nicht zu ersetzenden Ereignissen), generiert das System einen eigenen ID-Wert und weist ihn der Entität zu. |
| commerce.productListViews.value | Ereignisse | AppMeasurement-Abfrageparameter, EVENT_LIST_FULL-Zuordnung mit der Konvertierung COMMERCE_SC_VIEW, mithilfe des Trennzeichens `,`. |
| commerce.productViews.id | Ereignisse | `prodView` Ereignis-Serialisierung. Wenn dieses Feld ausgeschlossen wird (d. h. bei nicht zu ersetzenden Ereignissen), generiert das System einen eigenen ID-Wert und weist ihn der Entität zu. |
| commerce.productViews.value | Ereignisse | AppMeasurement-Abfrageparameter, EVENT_LIST_FULL-Zuordnung mit der Konvertierung COMMERCE_PROD_VIEW, mithilfe des Trennzeichens `,`. |
| commerce.purchases.value | Ereignisse | AppMeasurement-Abfrageparameter, EVENT_LIST_FULL-Zuordnung mit der Konvertierung COMMERCE_PURCHASE unter Verwendung des Trennzeichens `,`. |
| device.colorDepth | c | AppMeasurement-Abfrageparameter, C_COLOR-Zuordnung. |
| device.screenHeight | s | AppMeasurement-Abfrageparameter, Bildschirmauflösungszuordnung. |
| device.screenWidth | s | AppMeasurement-Abfrageparameter, Bildschirmauflösungszuordnung. |
| environment.browserDetails.acceptLanguage | Accept-Language | Dies ist eine HTTP-Kopfzeilen-Zuordnung, HEADER_ACCEPT_LANGUAGE. |
| environment.browserDetails.cookiesEnabled | k | AppMeasurement-Abfrageparameter, COOKIES-Zuordnung mit der Konvertierung BOOLEAN_TO_YN. |
| environment.browserDetails.javaEnabled | v | AppMeasurement-Abfrageparameter, JAVA_ENABLED-Zuordnung mit der Konvertierung BOOLEAN_TO_YN. |
| environment.browserDetails.javaScriptVersion | j | AppMeasurement-Abfrageparameter, J_JSCRIPT-Zuordnung. |
| environment.browserDetails.userAgent | User-Agent | Dies ist eine HTTP-Kopfzeilen-Zuordnung, HEADER_USER_AGENT. |
| environment.browserDetails.viewportHeight | bh | AppMeasurement-Abfrageparameter, BROWSER_HEIGHT-Zuordnung. |
| environment.browserDetails.viewportWidth | bw | AppMeasurement-Abfrageparameter, BROWSER_WIDTH-Zuordnung. |
| environment.connectionType | ct | AppMeasurement-Abfrageparameter, CT_CONNECT_TYPE-Zuordnung. |
| environment.ipV4 | X-Forwarded-For | Dies ist eine HTTP-Header-Zuordnung, X-FORWARDED-FOR. |
| identityMap.ECID[0].id | mid | AppMeasurement-Abfrageparameter, MID-Zuordnung. |
| marketing.trackingCode | v0 | AppMeasurement Abfrageparameter, CAMPAIGN-Zuordnung. |
| media.mediaTimed.completes.value | c.a.media.complete | AppMeasurement-Kontextdaten. |
| media.mediaTimed.dropBeforeStart.value | c.a.media.view, c.a.media.timePlayed, c.a.media.play | AppMeasurement-Kontextdaten. |
| media.mediaTimed.federated.value | c.a.media.federated | AppMeasurement-Kontextdatenzuordnung `c.a.media.federated`. |
| media.mediaTimed.firstQuartiles.value | c.a.media.progress25 | AppMeasurement-Kontextdaten. |
| media.mediaTimed.mediaSegmentView.value | c.a.media.segmentView | AppMeasurement-Kontextdaten. |
| media.mediaTimed.midpoints.value | c.a.media.progress50 | AppMeasurement-Kontextdaten. |
| media.mediaTimed.pauseTime.value | c.a.media.pauseTime | AppMeasurement-Kontextdatenzuordnung `c.a.media.pauseTime`. |
| media.mediaTimed.pauses.value | c.a.media.pauseCount | AppMeasurement-Kontextdatenzuordnung `c.a.media.pauseCount`. |
| media.mediaTimed.primaryAssetReference.@id | c.a.media.asset | AppMeasurement-Kontextdaten. |
| media.mediaTimed.primaryAssetReference.dc:title | c.a.media.friendlyName | AppMeasurement-Kontextdatenzuordnung `c.a.media.friendlyName`. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Creator[N].iptc4xmpExt:Name | c.a.media.originator | AppMeasurement-Kontextdaten. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Episode.iptc4xmpExt:Number | c.a.media.episode | AppMeasurement-Kontextdatenzuordnung `c.a.media.episode`. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Genre | c.a.media.genre | AppMeasurement-Kontextdaten. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Rating[N].iptc4xmpExt:RatingValue | c.a.media.rating | AppMeasurement-Kontextdaten. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Season.iptc4xmpExt:Number | c.a.media.season | AppMeasurement-Kontextdatenzuordnung `c.a.media.season`. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Identifier | a.media.name | AppMeasurement-Kontextdatenzuordnung `a.media.name`. |
| media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Name | c.a.media.show | AppMeasurement-Kontextdatenzuordnung `c.a.media.show`. |
| media.mediaTimed.primaryAssetReference.showType | c.a.media.type | AppMeasurement-Kontextdatenzuordnung `c.a.media.type` mit Konvertierung VEDIO_SHOW_TYPE. |
| media.mediaTimed.primaryAssetReference.showType | c.a.media.type | AppMeasurement-Kontextdaten `c.a.media.type` Zuordnung mit Konversion VIDEO_SHOW_TYPE. |
| media.mediaTimed.primaryAssetReference.xmpDM:duration | c.a.media.length | AppMeasurement-Kontextdatenzuordnung `c.a.media.length`. |
| media.mediaTimed.primaryAssetViewDetails.@id | c.a.media.vsid | AppMeasurement-Kontextdaten. |
| media.mediaTimed.primaryAssetViewDetails.broadcastChannel | c.a.media.channel | AppMeasurement-Kontextdatenzuordnung `c.a.media.channel`. |
| media.mediaTimed.primaryAssetViewDetails.broadcastContentType | c.a.contentType | AppMeasurement-Kontextdatenzuordnung `c.a.contentType`. |
| media.mediaTimed.primaryAssetViewDetails.broadcastNetwork | c.a.media.network | AppMeasurement-Kontextdatenzuordnung `c.a.media.network`. |
| media.mediaTimed.primaryAssetViewDetails.mediaSegmentView.value | c.a.media.segment | AppMeasurement-Kontextdatenzuordnung `c.a.media.segment`. |
| media.mediaTimed.primaryAssetViewDetails.playerName | c.a.media.playerName | AppMeasurement-Kontextdatenzuordnung `c.a.media.playerName`. |
| media.mediaTimed.primaryAssetViewDetails.playerSDKVersion.version | c.a.media.sdkVersion | AppMeasurement-Kontextdatenzuordnung `c.a.media.sdkVersion`. |
| media.mediaTimed.primaryAssetViewDetails.sourceFeed | c.a.media.feed | AppMeasurement-Kontextdatenzuordnung `c.a.media.feed`. |
| media.mediaTimed.primaryAssetViewDetails.streamFormat | c.a.media.format | AppMeasurement-Kontextdatenzuordnung `c.a.media.format`. |
| media.mediaTimed.progress10.value | c.a.media.progress10 | AppMeasurement-Kontextdaten. |
| media.mediaTimed.progress95.value | c.a.media.progress95 | AppMeasurement-Kontextdaten. |
| media.mediaTimed.resumes.value | c.a.media.resume | AppMeasurement-Kontextdatenzuordnung `c.a.media.resume`. |
| media.mediaTimed.starts.value | c.a.media.view | AppMeasurement-Kontextdaten. |
| media.mediaTimed.thirdQuartiles.value | c.a.media.progress75 | AppMeasurement-Kontextdaten. |
| media.mediaTimed.timePlayed.value | c.a.media.timePlayed | AppMeasurement-Kontextdatenzuordnung `c.a.media.timePlayed`. |
| media.mediaTimed.totalTimePlayed.value | c.a.media.totalTimePlayed | AppMeasurement-Kontextdatenzuordnung `c.a.media.totalTimePlayed`. |
| placeContext.geo.latitude | lat | AppMeasurement Abfrageparameter, LATITUDE-Zuordnung. |
| placeContext.geo.longitude | lon | AppMeasurement Abfrageparameter, LONGITUDE-Zuordnung. |
| placeContext.geo.postalCode | zip | AppMeasurement Abfrageparameter, ZIP-Zuordnung. |
| placeContext.geo.stateProvince | state | AppMeasurement Abfrageparameter, STATE-Zuordnung. |
| productListItems[N].lineItemId | products | AppMeasurement-Abfrageparameter, Produktkategorie-Zuordnung. |
| productlistitems[N].name | products | AppMeasurement Abfrageparameter, Produktnamenzuordnung. |
| productlistitems[N].priceTotal | products | AppMeasurement Abfrageparameter, Produktpreiszuordnung. |
| productlistitems[N].quantity | products | AppMeasurement-Abfrageparameter, Produktquantitätszuordnung. |
| web.webInteraction.URL | pev1 | AppMeasurement-Abfrageparameter, PAGE_EVENT_VAR1-Zuordnung. |
| web.webInteraction.name | pev2 | AppMeasurement-Abfrageparameter, PAGE_EVENT_VAR2-Zuordnung. |
| web.webInteraction.type | pe | `web.webInteraction.type=other` nach `pe=lnk_o`; `web.webInteraction.type=download` nach `pe=lnk_d`; `web.webInteraction.type=exit` nach `pe=lnk_e` |
| web.webPageDetails.URL | g | AppMeasurement Abfrageparameter, PAGE_URL-Zuordnung. |
| web.webPageDetails.errorPage | pageType | AppMeasurement-Abfrageparameter, PAGE_TYPE_FULL-Zuordnung mit Konvertierung ERROR_PAGE_TYPE. |
| web.webPageDetails.homePage | hp | AppMeasurement-Abfrageparameter, HOMEPAGE-Zuordnung mit der Konvertierung BOOLEAN_TO_YN. |
| web.webPageDetails.name | gn | AppMeasurement Abfrageparameter, PAGENAME-Zuordnung. |
| web.webPageDetails.server | sv | AppMeasurement Abfrageparameter, USER_SERVER-Zuordnung. |
| web.webPageDetails.siteSection | ch | AppMeasurement Abfrageparameter, KANALzuordnung. |
| web.webReferrer.URL | r | AppMeasurement Abfrageparameter, REFERRER-Zuordnung. |

{style="table-layout:auto"}
