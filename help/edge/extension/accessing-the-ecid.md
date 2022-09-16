---
title: Zugreifen auf die ECID
description: Adobe Experience Platform Web SDK-Erweiterung mit ECID in Tags
exl-id: 8e63a873-d7b5-4c6c-b14d-3c3fbc82b62f
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 10%

---

# Zugreifen auf die ECID

Die [!DNL Experience Cloud Identity (ECID)] ist eine beständige Kennung für einen Besucher Ihrer Website. Unter bestimmten Umständen bevorzugen Sie möglicherweise den Zugriff auf die ECID (z. B. um sie an einen Drittanbieter zu senden).

Für den Zugriff auf die ECID innerhalb von Tags empfiehlt Adobe Folgendes:

1. Stellen Sie sicher, dass Ihre Eigenschaft mit [Sequenzierung von Regelkomponenten](../../tags/ui/managing-resources/rules.md#sequencing) aktiviert.
1. Erstellen Sie eine neue Regel.
1. Hinzufügen einer [!UICONTROL Bibliothek geladen] -Ereignis der Regel hinzufügen.
1. Hinzufügen einer [!UICONTROL Benutzerdefinierte Bedingung] -Aktion mit dem folgenden Code auf die Regel anwenden (vorausgesetzt, der Name, den Sie für die SDK-Instanz konfiguriert haben, lautet `alloy`):

   ```javascript
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. Speichern Sie die Regel.

Anschließend sollten Sie in nachfolgenden Regeln mithilfe von `%ECID%` oder `_satellite.getVar("ECID")` wie jedes andere Datenelement.
