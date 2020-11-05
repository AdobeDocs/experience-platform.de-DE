---
title: Versionshinweise zum Adobe Experience Platform Web SDK
seo-title: Versionshinweise zum Adobe Experience Platform Web SDK
description: Versionshinweise zum Adobe Experience Platform Web SDK.
seo-description: Versionshinweise zum Adobe Experience Platform Web SDK.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;release notes;
translation-type: tm+mt
source-git-commit: 77c1e693668bc50a81713d02cfe4b0fabc661404
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 14%

---


# Versionshinweise

## Version 2.3.0

* Neue nonce-Unterstützung, um strengere Sicherheitsrichtlinien für Inhalte zu ermöglichen.
* Unterstützung der Personalisierung für Einzelseitenanwendungen hinzugefügt.
* Verbesserte Kompatibilität mit anderen On-Page-JavaScript-Code, der möglicherweise `window.console` APIs überschreibt.
* Fehlerbehebung: `sendBeacon` wurde nicht verwendet, wenn `documentUnloading` auf `true` oder wenn Link-Klicks automatisch verfolgt wurden.
* Fehlerbehebung: Ein Link wird nicht automatisch verfolgt, wenn das Ankerelement HTML-Inhalt enthält.
* Fehlerbehebung: Bestimmte Browser-Fehler, die eine schreibgeschützte `message` Eigenschaft enthalten, wurden nicht ordnungsgemäß behandelt, was dazu führte, dass dem Kunden ein anderer Fehler angezeigt wurde.
* Fehlerbehebung: Wenn das SDK in einem iframe ausgeführt wird, wird ein Fehler ausgegeben, wenn die HTML-Seite des iframe aus einer anderen Subdomäne stammt als die HTML-Seite des übergeordneten Fensters.

## Version 2.2.0

* Fehlerbehebung: Das Opt-in-Objekt hinderte Alloy daran, Aufrufe durchzuführen, wenn `idMigrationEnabled` dies `true`der Fall ist.
* Fehlerbehebung: Achten Sie auf Anforderungen, die Angebot zur Personalisierung zurückgeben, um ein flackerndes Problem zu vermeiden.

## Version 2.1.0

* Entfernen Sie den `syncIdentity` Befehl und unterstützen Sie die Übergabe dieser IDs im `sendEvent` Befehl.
* Unterstützung von IAB 2.0 Consent Standard.
* Unterstützt die Weitergabe zusätzlicher IDs im `setConsent` Befehl.
* Unterstützung, die den Befehl `datasetId` im `sendEvent` Befehl außer Kraft setzt.
* Unterstützung für zulässige Monitore ([Weitere](https://github.com/adobe/alloy/wiki/Monitoring-Hooks)Informationen)
* Übergeben Sie `environment: browser` die Implementierungsdetails in die Kontextdaten.
