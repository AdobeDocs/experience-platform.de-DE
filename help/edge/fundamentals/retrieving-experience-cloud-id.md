---
title: Abrufen der Experience Cloud ID
seo-title: Adobe Experience Platform Web SDK Abrufen der Experience Cloud ID
description: Erfahren Sie, wie Sie die Adobe Experience Cloud ID abrufen.
seo-description: Erfahren Sie, wie Sie die Adobe Experience Cloud ID abrufen.
translation-type: tm+mt
source-git-commit: fc48c11cb1f8a88f9fec8a36646f59f39ac3819f
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 19%

---


# (Beta) Abrufen der Experience Cloud ID

>[!IMPORTANT]
>
>Das Adobe Experience Platform Web SDK befindet sich derzeit in der Betaphase und steht nicht allen Nutzern zur Verfügung. Dokumentation und Funktionalität können sich ändern.

Adobe Experience Cloud verwendet eine eindeutige ID für jeden Kunden. Wenn Sie diese eindeutige ID verwenden möchten, verwenden Sie den `getIdentity` Befehl. `getIdentity` gibt die vorhandene ECID für den aktuellen Besucher zurück. Für erstmalige Besucher, die noch keine ECID haben, generiert dieser Befehl eine neue ECID.

>[!NOTE]
>
>Diese Methode wird in der Regel bei benutzerdefinierten Lösungen verwendet, bei denen die Experience Cloud ID gelesen werden muss. Es wird nicht von einer Standardimplementierung verwendet.

```javascript
alloy("getIdentity")
  .then(function(ecid) {
    // This function will get called with Adobe Experience Cloud Id when the command promise is resolved
  })
  .catch(function(error) {
    // The command failed.
    // "error" will be an error object with additional information
  })
```
