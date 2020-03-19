---
title: Variablen in Analytics automatisch zugeordnet
seo-title: Variablen, die in Analytics automatisch mit dem Adobe Experience Platform Web SDK zugeordnet werden
description: Erfahren Sie, welche Variablen in Analytics mit dem Experience Platform Web SDK automatisch zugeordnet werden.
seo-description: Erfahren Sie, welche Variablen in Analytics mit dem Experience Platform Web SDK automatisch zugeordnet werden.
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (Beta) Variablen, die in Analytics automatisch zugeordnet werden

>[!IMPORTANT]
>
>Das Adobe Experience Platform Web SDK befindet sich derzeit in der Betaphase und steht nicht allen Benutzern zur Verfügung. Dokumentation und Funktionalität können sich ändern.

Nachfolgend finden Sie eine Liste von Variablen, die vom Adobe Experience Platform Edge Network automatisch Analytics zugeordnet werden.

| XDM-Feldpfad | Analytics-Abfrage-Zeichenfolge/HTTP-Kopfzeile | Beschreibung |
| ---------- | ------------------------- | -------- |
| `environment.browserDetails.userAgent` | `User-Agent` | Dies ist eine HTTP-Header-Zuordnung, HEADER_USER_AGENT. |
| `environment.browserDetails.acceptLanguage` | `Accept-Language` | Dies ist eine HTTP-Header-Zuordnung, HEADER_ACCEPT_LANGUAGE. |
| `environment.browserDetails.cookiesEnabled` | `k` | AppMeasurement Abfrage Parameter COOKIES-Zuordnung mit der Konversion BOOLEAN_TO_YN. |
| `environment.browserDetails.javaScriptVersion` | `j` | AppMeasurement-Abfrage-Parameter J_JSCRIPT-Zuordnung. |
| `environment.browserDetails.javaEnabled` | `v` | AppMeasurement-Abfrage-Parameter JAVA_ENABLED-Zuordnung mit der Konversion BOOLEAN_TO_YN. |
| `environment.browserDetails.viewportHeight` | `bh` | AppMeasurement-Abfrage-Parameter BROWSER_HEIGHT-Zuordnung. |
| `environment.browserDetails.viewportWidth` | `bw` | AppMeasurement-Abfrage-Parameter BROWSER_WIDTH-Zuordnung. |
| `environment.connectionType` | `ct` | AppMeasurement-Abfrage-Parameter CT_CONNECT_TYPE-Zuordnung. |
| `device.colorDepth` | `c` | AppMeasurement-Abfrage-Parameter C_COLOR-Zuordnung. |
| `placeContext.geo.stateProvince` | `state` | AppMeasurement Abfrage-Parameterzuordnung STATE. |
| `placeContext.geo.postalCode` | `zip` | AppMeasurement Abfrage Parameter ZIP-Zuordnung. |
| `placeContext.geo.latitude` | `lat` | AppMeasurement Abfrage Parameter LATITUDE mapping. |
| `placeContext.geo.longitude` | `lon` | AppMeasurement Abfrage-Parameter LONGITUDE-Zuordnung. |
| `web.webPageDetails.server` | `sv` | AppMeasurement Abfrage-Parameter USER_SERVER-Zuordnung. |
| `web.webPageDetails.name` | `gn` | AppMeasurement Abfrage-Parameter PAGENAME-Zuordnung. |
| `web.webPageDetails.URL` | `g` | AppMeasurement Abfrage-Parameter PAGE_URL-Zuordnung. |
| `web.webPageDetails.homePage` | `hp` | AppMeasurement-Abfrage-Parameter HOMEPAGE-Zuordnung mit der Konversion BOOLEAN_TO_YN. |
| `web.webReferrer.URL` | `r` | AppMeasurement Abfrage-Parameterzuordnung für WERBER. |
| `application.id` | `c.a.appid` | AppMeasurement-Kontextdatenzuordnung `c.a.appid` . |
| `application.launches.value` | `c.a.launches` | AppMeasurement-Kontextdatenzuordnung `c.a.launches` . |
| `marketing.trackingCode` | `v0` | AppMeasurement Abfrage-Parameterzuordnung CAMPAIGN. |
| `commerce.purchaseID` | `pi` | AppMeasurement Abfrage-Parameter PURCHASEID-Zuordnung. |
| `commerce.currencyCode` | `cc` | AppMeasurement-Abfrage-Parameterzuordnung CURRENCY. |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Identifier` | `a.media.name` | AppMeasurement-Kontextdatenzuordnung `a.media.name` . |
| `media.mediaTimed.primaryAssetReference.xmpDM:duration` | `c.a.media.length` | AppMeasurement-Kontextdatenzuordnung `c.a.media.length` . |
| `media.mediaTimed.primaryAssetViewDetails.broadcastContentType` | `c.a.contentType` | AppMeasurement-Kontextdatenzuordnung `c.a.contentType` . |
| `media.mediaTimed.primaryAssetViewDetails.playerName` | `c.a.media.playerName` | AppMeasurement-Kontextdatenzuordnung `c.a.media.playerName` . |
| `media.mediaTimed.primaryAssetViewDetails.broadcastChannel` | `c.a.media.channel` | AppMeasurement-Kontextdatenzuordnung `c.a.media.channel` . |
| `media.mediaTimed.primaryAssetViewDetails.mediaSegmentView.value` | `c.a.media.segment` | AppMeasurement-Kontextdatenzuordnung `c.a.media.segment` . |
| `media.mediaTimed.primaryAssetReference.dc:title` | `c.a.media.friendlyName` | AppMeasurement-Kontextdatenzuordnung `c.a.media.friendlyName` . |
| `media.mediaTimed.primaryAssetViewDetails.playerSDKVersion.version` | `c.a.media.sdkVersion` | AppMeasurement-Kontextdatenzuordnung `c.a.media.sdkVersion` . |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Series.iptc4xmpExt:Name` | `c.a.media.show` | AppMeasurement-Kontextdatenzuordnung `c.a.media.show` . |
| `media.mediaTimed.primaryAssetViewDetails.streamFormat` | `c.a.media.format` | AppMeasurement-Kontextdatenzuordnung `c.a.media.format` . |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Season.iptc4xmpExt:Number` | `c.a.media.season` | AppMeasurement-Kontextdatenzuordnung `c.a.media.season` . |
| `media.mediaTimed.primaryAssetReference.iptc4xmpExt:Episode.iptc4xmpExt:Number` | `c.a.media.episode` | AppMeasurement-Kontextdatenzuordnung `c.a.media.episode` . |
| `media.mediaTimed.primaryAssetViewDetails.broadcastNetwork` | `c.a.media.network` | AppMeasurement-Kontextdatenzuordnung `c.a.media.network` . |
| `media.mediaTimed.primaryAssetReference.showType` | `c.a.media.type` | AppMeasurement-Kontextdatenzuordnung `c.a.media.type` mit Konversions-VEDIO_SHOW_TYPE. |
| `media.mediaTimed.primaryAssetViewDetails.sourceFeed` | `c.a.media.feed` | AppMeasurement-Kontextdatenzuordnung `c.a.media.feed` . |
| `media.mediaTimed.timePlayed.value` | `c.a.media.timePlayed` | AppMeasurement-Kontextdatenzuordnung `c.a.media.timePlayed` . |
| `media.mediaTimed.totalTimePlayed.value` | `c.a.media.totalTimePlayed` | AppMeasurement-Kontextdatenzuordnung `c.a.media.totalTimePlayed` . |
| `media.mediaTimed.federated.value` | `c.a.media.federated` | AppMeasurement-Kontextdatenzuordnung `c.a.media.federated` . |
| `media.mediaTimed.pauses.value` | `c.a.media.pauseCount` | AppMeasurement-Kontextdatenzuordnung `c.a.media.pauseCount` . |
| `media.mediaTimed.pauseTime.value` | `c.a.media.pauseTime` | AppMeasurement-Kontextdatenzuordnung `c.a.media.pauseTime` . |
| `media.mediaTimed.resumes.value` | `c.a.media.resume` | AppMeasurement-Kontextdatenzuordnung `c.a.media.resume` . |
| `identitymap.ecid.[0].id` | `mid` | AppMeasurement Abfrage Parameter MID-Zuordnung. |
