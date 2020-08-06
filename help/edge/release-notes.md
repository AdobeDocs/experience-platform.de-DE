---
title: Versionshinweise zum Adobe Experience Platform Web SDK
seo-title: Versionshinweise zum Adobe Experience Platform Web SDK
description: Adobe Experience Platform Web SDK - Versionshinweise.
seo-description: Adobe Experience Platform Web SDK - Versionshinweise.
translation-type: tm+mt
source-git-commit: c1cb64dc297d9133a8e3ef18c97cbd5fac5b0cd6
workflow-type: tm+mt
source-wordcount: '77'
ht-degree: 3%

---


# Versionshinweise

## Version 2.1.0

* Unterstützung von IAB 2.0 Consent Standard.
* Unterstützt die Weitergabe zusätzlicher IDs im `setConsent` Befehl.
* Unterstützung, die den Befehl `datasetId` im `sendEvent` Befehl außer Kraft setzt.
* Entfernen Sie den `syncIdentity` Befehl und unterstützen Sie die Übergabe dieser IDs im `sendEvent` Befehl.
* Unterstützung für zulässige Monitore ([Weitere Informationen)](https://github.com/adobe/alloy/wiki/Monitoring-Hooks)
* Übergeben Sie `environment: browser` die Implementierungsdetails in die Kontextdaten.
