---
solution: Experience Platform
title: Zuordnen von Adobe Target-Ereignisdaten zu XDM
description: Erfahren Sie, wie Sie Adobe Target-Ereignisfelder einem Experience-Datenmodell (XDM)-Schema zur Verwendung in Adobe Experience Platform zuordnen.
exl-id: dab08ab6-6c1c-460a-bb52-8dcdb5709a34
source-git-commit: 81412493b096264ce7a89e3ca2348edb2dcd1798
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 3%

---

# Zielgruppen-Mapping-Feldzuordnungen

In der folgenden Tabelle sind die Felder eines Experience-Datenmodell (XDM)-Erlebnisereignisschemas und die entsprechenden Felder aus Adobe Target, denen sie zugeordnet werden sollen, aufgeführt. Zusätzliche Hinweise für einige Zuordnungen werden ebenfalls bereitgestellt.

>[!NOTE]
>
>Bitte scrollen Sie nach links/rechts, um den gesamten Tabelleninhalt anzuzeigen.

| XDM ExperienceEvent-Feld | Feld für Target-Anforderung | Anmerkungen |
| ------------------------- | -------------------- | ----- |
| **`id`** | Eine eindeutige Anforderungskennung |
| **`dataSource`** | | Für alle Clients auf &quot;1&quot;konfiguriert. |
| `dataSource._id` | Ein systemgenerierter Wert, der nicht mit der Anfrage übergeben werden kann. | Die eindeutige ID dieser Datenquelle. Dies würde von der Person oder dem System bereitgestellt, die bzw. das die Datenquelle erstellt hat. |
| `dataSource.code` | Ein systemgenerierter Wert, der nicht mit der Anfrage übergeben werden kann. | Eine Verknüpfung zur vollständigen @id. Es kann mindestens ein Code oder @id verwendet werden. Manchmal wird dieser Code als Integrationscode der Datenquelle bezeichnet. |
| `dataSource.tags` | Ein systemgenerierter Wert, der nicht mit der Anfrage übergeben werden kann. | Tags werden verwendet, um anzugeben, wie die Aliase einer bestimmten Datenquelle von Anwendungen mithilfe dieser Aliase interpretiert werden sollen.<br><br>Beispiele:<br><ul><li>`isAVID`: Datenquellen, die Analytics-Besucher-IDs darstellen.</li><li>`isCRSKey`: Datenquellen, die Aliase darstellen, die als Schlüssel in CRS verwendet werden sollen.</li></ul>Tags werden festgelegt, wenn die Datenquelle erstellt wird, aber auch in Pipeline-Nachrichten eingeschlossen, wenn auf eine bestimmte Datenquelle verwiesen wird. |
| **`timestamp`** | Ereigniszeitstempel |
| **`channel`** | `context.channel` | Funktioniert nur mit der Anzeigebereitstellung. Die Optionen sind &quot;Web&quot;und &quot;Mobil&quot;, wobei &quot;Web&quot;die Standardeinstellung ist. |
| **`endUserIds`** |
| `endUserIds.experience.tntId` | `tntId/mboxPC` |
| `endUserIds.experience.mcId` | `marketingCloudVisitorId` | Die Experience Cloud-ID (ECID) wird auch als MCID bezeichnet und wird weiterhin in Namespaces verwendet. |
| **`environment`** |
| `environment.browserDetails.userAgent` | `mboxRequest.userAgent` |
| `environment.browserDetails.viewPortHeight` | `mboxRequest.browserHeight` |
| `environment.browserDetails.viewPortWidth` | `mboxRequest.browserWidth` |
| `environment.operatingSystem` | `deviceAtlas.osName` |
| `environment.operatingSystemVersion` | `deviceAtlas.osVersion` |
| `environment.viewportHeight` | `mboxRequest.screenHeight` |
| `environment.viewportWidth` | `mboxRequest.screenWidth` |
| `environment.colorDepth` | `mboxRequest.colorDepth` |
| `environment.carrier` | Der Name des Mobilnetzbetreibers wurde basierend auf der IP-Adresse der Anfrage aufgelöst. |
| `environment.ipV4` | `mboxRequest.ipAddress` (im V4-Format) |
| `environment.ipV6` | `mboxRequest.ipAddress` (im V6-Format) |
| **`experience`** |
| `experience.target.clientCode` | `mboxRequest.client` |
| `experience.target.mboxName` | `mboxRequest.mboxName` |
| `experience.target.mboxVersion` | `mboxRequest.mboxVersion` |
| `experience.target.sessionId` | `mboxRequest.sessionId` |
| `experience.target.environmentID` | Internes Mapping von Target für kundendefinierte Umgebungen (z. B. dev, qa oder prod). |
| `experience.target.supplementalDataID` | Bezeichner, der zum Zuordnen von Target-Ereignissen zu Analytics-Ereignissen verwendet wird |
| `experience.target.pageDetails.pageId` | `mboxRequest.pageId` |
| `experience.target.pageDetails.pageScore` | `mboxRequest.mboxPageValue` |
| `experience.target.activities` | Liste (Array) der Aktivitäten, für die sich der Besucher qualifiziert hat |
| `experience.target.activities[i].activityID` | Die ID einer bestimmten Aktivität, für die sich der Besucher qualifiziert hat |
| `experience.target.activities[i].version` | Die Version einer bestimmten Aktivität, für die sich der Besucher qualifiziert hat |
| `experience.target.activities[i].activityEvents` | Enthält Details zu Aktivitätsereignissen, die der Benutzer mit diesem Ereignis getroffen hat. |
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
| `placeContext.geo.id` | Zufällige UID (erforderlich) |
| `placeContext.geo.city` | Der Stadt-Name wird basierend auf der IP-Adresse der Anfrage aufgelöst. |
| `placeContext.geo.countryCode` | Ländercode basierend auf der IP-Adresse der Anfrage aufgelöst. |
| `placeContext.geo.dmaId` | Der angegebene Marktbereich-Code wurde basierend auf der IP-Adresse der Anfrage aufgelöst. |
| `placeContext.geo.postalCode` | Postleitzahl basierend auf der IP-Adresse der Anfrage aufgelöst. |
| `placeContext.geo.stateProvince` | Bundesland oder Bundesland basierend auf der IP-Adresse der Anfrage aufgelöst. |
| `placeContext.localTime` | `mboxRequest.offsetTime` + `mboxRequest.currentServerTime` |
| **`commerce`** | | Wird nur eingestellt, wenn Bestelldetails in der Anfrage vorhanden sind. |
| `commerce.order.priceTotal` | `mboxRequest.orderTotal` |
| `commerce.order.purchaseOrderNumber` | `mboxRequest.orderId` |
| `commerce.order.purchaseID` | `mboxRequest.orderId` |
| **`web`** |
| `web.withWebPageDetails.url` | `mboxURL.context.address.url` |
| `web.webReferrer.url` | `mboxReferrer.context.address.url` |
| **`identityMap`** |
| `identityMap.TNTID` | `tntId.mboxPC` |
| `identityMap.ECID` | `marketingCloudVisitorId` |

{style="table-layout:auto"}
