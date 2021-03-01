---
title: Versionshinweise zum Adobe Experience Platform Web-SDK
description: Die neuesten Versionshinweise für Adobe Experience Platform Web-SDK.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;Versionshinweise
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 10%

---


# Versionshinweise

## Version 2.3.0

* Neue nonce-Unterstützung, um strengere Content-Sicherheitsrichtlinien zu ermöglichen.
* Unterstützung der Personalisierung für Einzelseitenanwendungen hinzugefügt.
* Verbesserte Kompatibilität mit anderen On-Page-JavaScript-Code, der `window.console`-APIs überschreiben kann.
* Fehlerbehebung: `sendBeacon` wurde nicht verwendet, wenn `documentUnloading` auf `true` gesetzt wurde oder wenn Link-Klicks automatisch verfolgt wurden.
* Fehlerbehebung: Ein Link wird nicht automatisch verfolgt, wenn das Ankerelement HTML-Inhalt enthält.
* Fehlerbehebung: Bestimmte Browserfehler, die eine schreibgeschützte `message`-Eigenschaft enthalten, wurden nicht ordnungsgemäß verarbeitet, was dazu führte, dass dem Kunden ein anderer Fehler angezeigt wurde.
* Fehlerbehebung: Wenn das SDK in einem iframe ausgeführt wird, wird ein Fehler ausgegeben, wenn die HTML-Seite des iframe aus einer anderen Subdomäne stammt als die HTML-Seite des übergeordneten Fensters.

## Version 2.2.0

* Fehlerbehebung: Das Opt-in-Objekt hinderte Alloy daran, Aufrufe durchzuführen, wenn `idMigrationEnabled` `true` ist.
* Fehlerbehebung: Achten Sie auf Anforderungen, die Angebot zur Personalisierung zurückgeben, um ein flackerndes Problem zu vermeiden.

## Version 2.1.0

* Entfernen Sie den Befehl `syncIdentity` und unterstützen Sie die Übergabe dieser IDs im Befehl `sendEvent`.
* Unterstützung von IAB 2.0 Consent Standard.
* Unterstützung der Weitergabe zusätzlicher IDs im Befehl `setConsent`.
* Support Außerkraftsetzen von `datasetId` im Befehl `sendEvent`
* Unterstützung für zulässige Monitore ([Mehr lesen](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* Übergeben Sie `environment: browser` in die Kontextdaten der Implementierung.
