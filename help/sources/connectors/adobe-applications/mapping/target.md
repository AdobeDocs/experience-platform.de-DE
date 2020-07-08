---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Zielgruppen-Mapping
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 0%

---


# Zielgruppen-Mapping-Felder

Mit der Adobe Experience Platform können Sie Adobe Target-Daten über den Target-Quellanschluss erfassen. Bei Verwendung des Connectors müssen alle Daten aus den Target-Feldern den XDM-Feldern ( [Experience Data Model)](../../../../xdm/home.md) zugeordnet sein, die der XDM ExperienceEvent-Klasse zugeordnet sind.

In der folgenden Tabelle sind die Felder eines Experience Ereignis-Schemas (Feld *XDM ExperienceEvent) und die entsprechenden Target-Felder, denen sie zugeordnet werden sollen (Feld* für *Target-Anforderung*), aufgeführt. Zusätzliche Hinweise für einige Zuordnungen werden ebenfalls bereitgestellt.

>[!NOTE]
>
>Bitte blättern Sie nach links/rechts, um den gesamten Tabelleninhalt Ansicht.

| XDM ExperienceEvent-Feld | Feld für Target-Anforderung | Anmerkungen |
| ------------------------- | -------------------- | ----- |
| **`id`** | Eine eindeutige Anforderungskennung |
| **`dataSource`** |  | Für alle Clients auf &quot;1&quot;konfiguriert. |
| `dataSource._id` | Ein systemgenerierter Wert, der nicht mit der Anforderung weitergegeben werden kann. | Die eindeutige ID dieser Datenquelle. Dies wird von der Person oder dem System bereitgestellt, die bzw. das die Datenquelle erstellt hat. |
| `dataSource.code` | Ein systemgenerierter Wert, der nicht mit der Anforderung weitergegeben werden kann. | Eine Verknüpfung zur vollständigen @id. Es kann mindestens ein Code oder @id verwendet werden. Manchmal wird dieser Code als Datenquellen-Integrationscode bezeichnet. |
| `dataSource.tags` | Ein systemgenerierter Wert, der nicht mit der Anforderung weitergegeben werden kann. | Tags werden verwendet, um anzugeben, wie die Aliase, die von einer Datenquelle dargestellt werden, von Anwendungen, die diese Aliase verwenden, interpretiert werden sollen.<br><br>Beispiele:<br><ul><li>`isAVID`: Datenquellen, die Analytics-Besucher-IDs darstellen.</li><li>`isCRSKey`: Datenquellen, die Aliase darstellen, die als Schlüssel in CRS verwendet werden sollten.</li></ul>Tags werden festgelegt, wenn die Datenquelle erstellt wird, aber sie werden auch in Pipelinemeldungen enthalten, wenn auf eine bestimmte Datenquelle verwiesen wird. |
| **`timestamp`** | Ereignis-Zeitstempel |
| **`channel`** | `context.channel` | Funktioniert nur mit Ansicht Versand. Die Optionen lauten &quot;web&quot;und &quot;mobile&quot;, wobei &quot;web&quot;die Standardeinstellung ist. |
| **`endUserIds`** |
| `endUserIds.experience.tntId` | `tntId/mboxPC` |
| `endUserIds.experience.mcId` | `marketingCloudVisitorId` |
| **`environment`** |
| `environment.browserDetails.userAgent` | `mboxRequest.userAgent` |
| `environment.browserDetails.viewPortHeight` | `mboxRequest.browserHeight` |
| `environment.browserDetails.viewPortWidth` | `mboxRequest.browserWidth` |
| `environment.operatingSystem` | `deviceAtlas.osName` |
| `environment.operatingSystemVersion` | `deviceAtlas.osVersion` |
| `environment.viewportHeight` | `mboxRequest.screenHeight` |
| `environment.viewportWidth` | `mboxRequest.screenWidth` |
| `environment.colorDepth` | `mboxRequest.colorDepth` |
| `environment.carrier` | Der Name des Mobilnetzbetreibers wurde basierend auf der IP-Adresse der Anforderung aufgelöst. |
| `environment.ipV4` | `mboxRequest.ipAddress` (im Format V4) |
| `environment.ipV6` | `mboxRequest.ipAddress` (im V6-Format) |
| **`experience`** |
| `experience.target.clientCode` | `mboxRequest.client` |
| `experience.target.mboxName` | `mboxRequest.mboxName` |
| `experience.target.mboxVersion` | `mboxRequest.mboxVersion` |
| `experience.target.sessionId` | `mboxRequest.sessionId` |
| `experience.target.environmentID` | Targets interne Zuordnung für benutzerdefinierte Umgebung (wie dev, qa oder prod). |
| `experience.target.supplementalDataID` | Bezeichner zum Verbinden von Target-Ereignissen mit Analytics-Ereignissen |
| `experience.target.pageDetails.pageId` | `mboxRequest.pageId` |
| `experience.target.pageDetails.pageScore` | `mboxRequest.mboxPageValue` |
| `experience.target.activities` | Liste (Array) der Aktivitäten, für die der Besucher sich qualifiziert hat |
| `experience.target.activities[i].activityID` | Die ID einer Aktivität, für die der Besucher die Qualifikation für die |
| `experience.target.activities[i].version` | Die Version einer bestimmten Aktivität, für die der Besucher qualifiziert ist |
| `experience.target.activities[i].activityEvents` | Umfasst die Details der Ereignis der Aktivität, die der Benutzer mit diesem Ereignis getroffen hat. |
| **`device`** |
| `device.typeIDService` | `XDMDevice.Device.TypeIDService.typeIDService_deviceatlas` |
| `device.type` | Eine der folgenden Eigenschaften von `deviceAtlas` (oder NULL): <ul><li>`type_mobile`</li><li>`type_tablet`</li><li>`type_desktop`</li><li>`type_ereader`</li><li>`type_television`</li><li>`type_settop`</li><li>`type_mediaplayer`</li></ul> |
| `device.typeID` | (leere Zeichenfolge) |
| `device.manufacturer` | `deviceAtlas.manufacturer` |
| `device.model` | `deviceAtlas.model` |
| `device.modelNumber` | (leere Zeichenfolge) |
| `device.screenHeight` | `deviceAtlas.displayHeight` |
| `device.screenWidth` | `deviceAtlas.displayWidth` |
| `device.colorDepth` | `deviceAtlas.displayColorDepth` |
| **`placeContext`** |
| `placeContext.geo.id` | UUID (optional) |
| `placeContext.geo.city` | Der Stadt-Name wurde basierend auf der IP-Adresse der Anforderung aufgelöst. |
| `placeContext.geo.countryCode` | Ländercode basierend auf der IP-Adresse der Anforderung aufgelöst. |
| `placeContext.geo.dmaId` | Code des angegebenen Marktbereichs, der auf der Grundlage der IP-Adresse der Anforderung aufgelöst wird. |
| `placeContext.geo.postalCode` | Postleitzahl, die basierend auf der IP-Adresse der Anforderung aufgelöst wird. |
| `placeContext.geo.stateProvince` | Bundesland oder Bundesland wurde auf der Grundlage der IP-Adresse des Antrags aufgelöst. |
| `placeContext.localTime` | `mboxRequest.offsetTime` + `mboxRequest.currentServerTime` |
| **`commerce`** |  | Wird nur eingestellt, wenn die Bestelldetails in der Anforderung vorhanden sind. |
| `commerce.order.priceTotal` | `mboxRequest.orderTotal` |
| `commerce.order.purchaseOrderNumber` | `mboxRequest.orderId` |
| `commerce.order.purchaseID` | `mboxRequest.orderId` |
| **`web`** |
| `web.withWebPageDetails.url` | `mboxURL.context.address.url` |
| `web.webReferrer.url` | `mboxReferrer.context.address.url` |
| **`identityMap`** |
| `identityMap.TNTID` | `tntId.mboxPC` |
| `identityMap.ECID` | `marketingCloudVisitorId` |
