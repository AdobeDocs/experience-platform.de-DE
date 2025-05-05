---
title: Echtzeit-Profilsynchronisierung für mbox3rdPartyId
description: Erfahren Sie, wie Sie mbox3rdPartyId mit der Adobe Experience Platform Web SDK verwenden.
keywords: Personalisierung;Target;Adobe Target;renderDecisions;sendEvent;mbox3rdPartyId;
exl-id: 677d1054-0769-4ec6-811e-e02d4b247c2a
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 1%

---

# `mbox3rdPartyId`

Die mbox3rdPartyId in Adobe Target ist die Besucher-ID Ihres Unternehmens, z. B. die Mitgliedschafts-ID des Treueprogramms Ihres Unternehmens.

Wenn sich ein Besucher auf der Website eines Unternehmens anmeldet, erstellt das Unternehmen in der Regel eine ID, die mit dem Konto, der Treuekarte, der Mitgliedschaftsnummer oder anderen Kennungen des Besuchers für dieses Unternehmen verknüpft ist. [Weitere Informationen](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html?lang=de#)


## Verwendung von `mbox3rdPartyId` mit der Web-SDK

### Schritt 1: Konfigurieren des `Target Third Party ID Namespace`

Konfigurieren Sie die `Target Third Party ID Namespace` in Ihrem [Datenstrom](../../../datastreams/overview.md) unter Verwendung des ID-Namespace, den Sie als mbox-Drittanbieter-ID verwenden möchten.
[Weitere Informationen zu ID-Namespaces](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=de)

![Experience Platform-Benutzeroberfläche mit dem Namespace-Feld für die Target-Third-Party-ID.](assets/mbox3rdpartyid.png)

### Schritt 2: `mbox3rdpartyId` an Target senden

Senden Sie die `mbox3rdpartyId` im `sendEvent`-Befehl unter Verwendung des ID-Namespace, den Sie in Schritt 1 konfiguriert haben, an Target.
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
