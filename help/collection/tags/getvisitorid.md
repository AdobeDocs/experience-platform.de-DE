---
title: getVisitorId
description: Rufen Sie die Tag-Erweiterungsinstanz des Experience Cloud-Besucher-ID-Service ab.
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 1%

---

# `getVisitorId()`

Die `_satellite.getVisitorId()`-Methode gibt eine Instanz des [Adobe Experience Cloud ID-Service](https://experienceleague.adobe.com/de/docs/id-service/using/home) innerhalb Ihrer Tag-Eigenschaft zurück, **wenn** die ID-Service-Erweiterung installiert und veröffentlicht wurde. Diese Methode ist hilfreich, wenn Sie direkten Zugriff auf die Besucher-ID-Instanz zur Verwendung in benutzerdefinierten Code-Blöcken, zur Konfiguration erweiterter Datenelemente oder zur Fehlerbehebung bei Problemen mit der Besucheridentität wünschen.

>[!IMPORTANT]
>
>Diese Methode gilt nur für Eigenschaften, die die eigenständige Service-Tag-Erweiterung &quot;Experience Cloud ID“ enthalten. Dies gilt nicht für die Funktionen des impliziten ID-Diensts, die in der Tag-Erweiterung von Web SDK verfügbar sind. Siehe den Befehl [`getIdentity`](/help/collection/js/commands/getidentity.md) , wenn Sie eine Besucheridentität mithilfe der Funktionen des impliziten ID-Diensts von Web SDK abrufen müssen.

Wenn Sie diese Methode aufrufen, während die ID-Service-Erweiterung installiert und veröffentlicht ist, wird ein -Objekt zurückgegeben, das dem -Objekt ähnelt, das nach dem Aufruf der [`Visitor.getInstance()`](https://experienceleague.adobe.com/en/docs/id-service/using/id-service-api/methods/getinstance)-Methode abgerufen wurde. Wenn Sie diese Methode aufrufen, wenn die ID-Service-Erweiterung nicht installiert oder veröffentlicht ist, gibt die Methode `null` zurück.

```ts
_satellite.getVisitorId(): Visitor | null
```

## Verfügbare Felder und Methoden

Weitere Informationen zu den für Sie verfügbaren Feldern [&#x200B; Methoden finden &#x200B;](https://experienceleague.adobe.com/en/docs/id-service/using/id-service-api/methods/get-set) im Experience Cloud ID-Dienst Methoden) in der Dokumentation zum Experience Cloud-Besucher-ID-Dienst .

```js
// Retrieve a visitor's ECID
_satellite.getVisitorId().getMarketingCloudVisitorID();

// Retrieve a visitor's legacy Analytics ID
_satellite.getVisitorId().getAnalyticsVisitorID();

// Retrieve a visitor's Audience Manager blob for audience sharing
_satellite.getVisitorId().getAudienceManagerBlob();
```
