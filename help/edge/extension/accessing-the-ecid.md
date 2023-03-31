---
title: Zugreifen auf die ECID
description: Erfahren Sie, wie Sie in Adobe Experience Platform-Tags auf die Experience Cloud-ID (ECID) zugreifen.
exl-id: 8e63a873-d7b5-4c6c-b14d-3c3fbc82b62f
source-git-commit: db7700d5c504e484f9571bbb82ff096497d0c96e
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 9%

---


# Zugreifen auf die ECID

Die [!DNL Experience Cloud ID (ECID)] ist eine persistente Experience Cloud-ID, die Ihnen bei der Identifizierung von Besuchern Ihrer Website helfen kann. Unter bestimmten Umständen, z. B. beim Senden der Kennung an eine Drittanbieterplattform, benötigen Sie möglicherweise Zugriff auf die [!DNL ECID].

So greifen Sie auf die [!DNL ECID] innerhalb von -Tags, führen Sie die folgenden Schritte aus:

1. Stellen Sie sicher, dass Ihre Eigenschaft mit [Sequenzierung von Regelkomponenten](../../tags/ui/managing-resources/rules.md#sequencing) aktiviert.
2. Erstellen Sie eine neue Regel.
3. Hinzufügen einer [!UICONTROL Bibliothek geladen] -Ereignis der Regel hinzufügen.
4. Hinzufügen einer [!UICONTROL Benutzerdefinierte Bedingung] -Aktion auf die Regel mit dem folgenden Code (vorausgesetzt, der für die SDK-Instanz konfigurierte Name lautet `alloy`):

   ```javascript
   return alloy("getIdentity")
       .then(function(result) {
           _satellite.setVar("ECID", result.identity.ECID);
       });
   ```

5. Speichern Sie die Regel.

Sie sollten jetzt auf die [!DNL ECID] in nachfolgenden Regeln verwenden, `%ECID%` oder `_satellite.getVar("ECID")`, ähnlich wie beim Zugriff auf andere Datenelemente.
