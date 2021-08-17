---
title: 'Zugreifen auf die ECID '
description: Adobe Experience Platform Web SDK-Erweiterung mit ECID in Tags
source-git-commit: befe1efa884706165b8d65803d06f6370a8a60f2
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 10%

---


# Zugreifen auf die ECID

[!DNL Experience Cloud Identity (ECID)] ist eine beständige Kennung für einen Besucher Ihrer Website. Unter bestimmten Umständen bevorzugen Sie möglicherweise den Zugriff auf die ECID (z. B. um sie an einen Drittanbieter zu senden).

Für den Zugriff auf die ECID innerhalb von Tags empfiehlt Adobe Folgendes:

1. Stellen Sie sicher, dass Ihre Eigenschaft mit der aktivierten [Sequenzierung von Regelkomponenten](../../tags/ui/managing-resources/rules.md#sequencing) konfiguriert ist.
1. Erstellen Sie eine neue Regel.
1. Fügen Sie der Regel das Ereignis [!UICONTROL Bibliothek geladen] hinzu.
1. Fügen Sie der Regel eine Aktion [!UICONTROL Benutzerdefinierte Bedingung] mit folgendem Code hinzu (vorausgesetzt, der für die SDK-Instanz konfigurierte Name ist `alloy`):

   ```javascript
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. Speichern Sie die Regel.

Anschließend sollten Sie wie jedes andere Datenelement auch in nachfolgenden Regeln mit `%ECID%` oder `_satellite.getVar("ECID")` auf die ECID zugreifen können.
