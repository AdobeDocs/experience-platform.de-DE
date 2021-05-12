---
title: 'Zugreifen auf die ECID '
description: Adobe Experience Platform Web SDK Extension unter Nutzung der ECID in Adobe Experience Platform Launch
source-git-commit: 3002036d7366e2f7310aa62e53c7c391d9ff7a07
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 5%

---


# Zugreifen auf die ECID

[!DNL Experience Cloud Identity (ECID)] ist eine beständige Kennung für einen Besucher Ihrer Website. Unter bestimmten Umständen könnten Sie lieber auf die ECID zugreifen (um sie beispielsweise an einen Dritten zu senden).

Für den Zugriff auf die ECID in Adobe Experience Platform Launch empfiehlt Adobe Folgendes:

1. Vergewissern Sie sich, dass Ihre Eigenschaft mit aktivierter [Regel-Komponentensequenzierung](https://experienceleague.adobe.com/docs/launch/using/ui/rules.html?lang=en#rule-component-sequencing) konfiguriert ist.
1. Erstellen Sie eine neue Regel.
1. hinzufügen Sie ein [!UICONTROL Bibliotheksladungs]-Ereignis in die Regel.
1. hinzufügen Sie eine Aktion [!UICONTROL Benutzerdefinierte Bedingung] mit folgendem Code an die Regel (vorausgesetzt, der für die SDK-Instanz konfigurierte Name ist `alloy`):

   ```javascript
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. Speichern Sie die Regel.

Sie sollten dann wie jedes andere Datenelement in nachfolgenden Regeln mit `%ECID%` oder `_satellite.getVar("ECID")` auf die ECID zugreifen können.
