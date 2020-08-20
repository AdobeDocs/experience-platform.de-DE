---
title: Versionshinweise zum Adobe Experience Platform Web SDK
seo-title: Versionshinweise zum Adobe Experience Platform Web SDK
description: Adobe Experience Platform Web SDK - Versionshinweise.
seo-description: Adobe Experience Platform Web SDK - Versionshinweise.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;release notes;
translation-type: tm+mt
source-git-commit: 8c256b010d5540ea0872fa7e660f71f2903bfb04
workflow-type: tm+mt
source-wordcount: '77'
ht-degree: 3%

---


# Versionshinweise

## Version 2.1.0

* Entfernen Sie den `syncIdentity` Befehl und unterstützen Sie die Übergabe dieser IDs im `sendEvent` Befehl.
* Unterstützung von IAB 2.0 Consent Standard.
* Unterstützt die Weitergabe zusätzlicher IDs im `setConsent` Befehl.
* Unterstützung, die den Befehl `datasetId` im `sendEvent` Befehl außer Kraft setzt.
* Unterstützung für zulässige Monitore ([Weitere](https://github.com/adobe/alloy/wiki/Monitoring-Hooks)Informationen)
* Übergeben Sie `environment: browser` die Implementierungsdetails in die Kontextdaten.
