---
title: Echtzeit-Profilsynchronisierung für mbox3rdPartyId
description: Erfahren Sie, wie Sie mbox3rdPartyId mit dem Adobe Experience Platform Web SDK verwenden.
keywords: Personalisierung;Target;adobe target;renderDecisions;sendEvent;mbox3rdPartyId;
source-git-commit: 439f26177837e985ef95e972c3102cc2db37d539
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 9%

---


# Was ist `mbox3rdPartyId`

Die mbox3rdPartyId in Adobe Target ist die Besucher-ID Ihres Unternehmens, z. B. die Mitgliedschafts-ID für das Treueprogramm Ihres Unternehmens.

Wenn sich ein Besucher bei der Site eines Unternehmens anmeldet, erstellt das Unternehmen in der Regel eine ID, die mit dem Konto, der Treuekarte, der Mitgliedsnummer oder anderen für dieses Unternehmen geltenden Kennungen des Besuchers verknüpft ist. [Weitere Informationen](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html?lang=en#)


## Verwendung `mbox3rdPartyId` mit dem Web SDK

### Schritt 1: Konfigurieren Sie die `Target Third Party ID Namespace`

Konfigurieren Sie die `Target Third Party ID Namespace` in [Datastream](../../fundamentals/datastreams.md), unter Verwendung des ID-Namespace, den Sie als Mbox-Drittanbieter-ID verwenden möchten.
[Weitere Informationen zu ID-Namespaces](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=de)

![](assets/mbox3rdpartyid.png)

### Schritt 2: Senden Sie die `mbox3rdpartyId` in Target

Senden Sie die `mbox3rdpartyId` in Target im `sendEvent` -Befehl mithilfe des ID-Namespace, den Sie in Schritt 1 konfiguriert haben.
[Weitere Informationen zum Senden von IDs](../../identity/overview.md#syncing-identities)

```javascript
alloy("sendEvent", {
  xdm: {
    "identityMap": {
      "ID_NAMESPACE": [ // Replace `ID_NAMESPACE` with the namespace you have configured in Step 1.
        {
          "id": "1234",
          "authenticatedState": "authenticated"
        }
      ]
    }
  }
});
```


