---
title: Warnungstest-Referenz
description: Erfahren Sie, wie die Auditor-Funktion in Adobe Experience Platform Debugger auf Warnhinweise testet.
exl-id: ac6f8675-6c34-48b4-b5dd-48e92af217fd
source-git-commit: 10a5605c40143b58f6ba0108cc087956aa929866
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 32%

---

# Warnungstest-Referenz

Diese Referenz enthält weitere Informationen dazu, wie die Auditor-Funktion in Adobe Experience Platform Debugger Warnungstests durchführt.

>[!NOTE]
>
>Weitere Informationen zu Auditor-Tests in Platform Debugger finden Sie in der [Übersicht über Auditor-Funktionen](./overview.md).

Warnhinweise zeigen Probleme an, die Sie kennen sollten, aber sich nicht auf Ihr Ergebnis auswirken. Dies sind Best Practice-Empfehlungen, die in einigen Fällen nicht auf Ihre Implementierung zutreffen.

| Test | Gewichtung | Kriterien | Empfehlung |
| --- | --- | --- | --- |
| Advertising Cloud – Korrektes Konversions-Tag ist implementiert | 0 | Überprüfen Sie, ob das richtige Konversions-Tag verwendet wird.<br><br>**Warnung**: Die Verwendung der veralteten TubeMogul-Konversions-Tags kann zu Datenverlust führen. | Aktualisieren Sie Ihre Konversionspixel auf die neuen „Nur-Bild“-Konversions-Tags von Advertising Cloud. Dies lässt sich am einfachsten mit dem [Advertising Cloud-Tag-Erweiterung](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud – Korrektes JS-Tag wird verwendet | 0 | Advertising Cloud sollte die neuesten JavaScript-Tags verwenden. | Aktualisieren Sie Ihr Advertising Cloud-JavaScript auf die neueste Version. Die Verwendung veralteter JavaScript-Versionen kann zu Funktionsverlust führen. Dies lässt sich durch die Verwendung des [Advertising Cloud-Tag-Erweiterung](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud – „Nur-Bild“-Tag | 0 | Das Bildpixelformat der Advertising Cloud sollte mit einem der folgenden empfohlenen Formate übereinstimmen: <ul><li>`http(s)://rtd.tubemogul.com/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://rtd-tm.everesttech.net/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://pixel.everesttech.net/px2/<NUMERIC_ID>?`</li></ul> | Aktualisieren Sie Ihre Advertising Cloud-Pixel auf die neuen „Nur-Bild“-Tags der Advertising Cloud, um sicherzustellen, dass Sie die vollständige Funktionalität der Advertising Cloud nutzen. Dies lässt sich am einfachsten mit dem [Advertising Cloud-Tag-Erweiterung](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud – DSP-Synchronisierung für Segmentpixel ist aktiviert | 0 | Überprüfen Sie, ob das TubeMogul-Segmentpixel eine DSP-Synchronisierungseinstellung enthält, und empfehlen Sie, dem Pixel die Einstellung hinzuzufügen. Die Einstellung DSP Synchronisierung wird durch die Verwendung eines Abfragezeichenfolgenparameters bestimmt. Zur Zusammenfassung: <ul><li>WENN das -Tag für einen der folgenden Ereignisse ausgelöst wird:<ul><li>`https://rtd.tubemogul.com/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://rtd-tm.everesttech.net/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://pixel.everesttech.net/px2/<NUMERIC_ID>?`</li></ul></li><li>UND das Tag den URL-Parameter enthält `sid=`</li><li>Überprüfen Sie DANN, ob der URL-Parameter `cs=0` oder `cs=1` vorhanden ist, und wenn nicht, empfehlen Sie Folgendes: `cs=1` hinzugefügt werden, damit die Übereinstimmungsraten der Zielgruppe verbessert werden können.</li></ul> | URL-Parameter hinzufügen `cs=1` zu Ihren Advertising Cloud-Pixeln hinzu, damit eine DSP Synchronisierung stattfinden kann, wodurch die Übereinstimmungsraten der Zielgruppe erhöht werden. Dies lässt sich am einfachsten mit dem [Advertising Cloud-Tag-Erweiterung](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Experience Cloud ID-Service – Nur ein AdobeOrg wird verwendet | 0 | In einer normalen ECID-Implementierung sollte eine einzelne AdobeOrg verwendet werden. | Validieren Sie, ob für diese Implementierung mehrere AdobeOrg-IDs vorhanden sind. <br><br>[Weitere Informationen](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html) |
| Launch - `pageBottom` Callback-Platzierung | 0 | Die `_satellite.pageBottom()` muss vorhanden sein, damit Tags funktionieren. Fügen Sie das Inline-Skript unmittelbar vor dem schließenden `</body>` -Tag, um eine ordnungsgemäße DTM-Funktionalität sicherzustellen. Hinweis: Es empfiehlt sich, das Tag als das letzte Tag im `<body>`. Wenn sie im `<body>` -Tag kann es funktionieren, doch da es sich nicht um eine Best Practice handelt, kann es falsch oder mit unerwarteten oder unerwünschten Ergebnissen funktionieren. | Fügen Sie das Inline-Skript unmittelbar vor dem schließenden `</body>` -Tag, um eine ordnungsgemäße DTM-Funktionalität sicherzustellen. <br><br>[Weitere Informationen](../../tags/ui/client-side/asynchronous-deployment.md) |
| Launch – Self-Hosting | 0 | Die Tag-Bibliothek wird auf der Akamai-Instanz der Adobe unter `assets.adobedtm.com`. Das Self-Hosting ist der empfohlene Ansatz zum Laden von Tags, da es die Leistung von Websites durch Cache-Steuerung, Reduzierung der Skriptabhängigkeiten von Drittanbietern und bessere Steuerung des Veröffentlichungsprozesses verbessert. Tag-Bibliotheken können über Ihr eigenes Web-Hosting oder CDN gehostet und verwaltet werden. | Beim Wechsel zu einem Self-Hosting wird versucht, Tags auf einer Seite zu laden. Obwohl das Hosting über das Akamai CDN in den meisten Fällen funktioniert, verbessert das Self-Hosting die Seitenleistung. <br><br>Weitere Informationen:<ul><li>[Schnellstartanleitung für Tags](../../tags/ui/client-side/asynchronous-deployment.md)</li><li>[Asynchrone Implementierung](../../tags/ui/client-side/asynchronous-deployment.md)</li></ul> |
| Launch – Sollte asynchron bereitgestellt werden | 0 | Tags sollten asynchron bereitgestellt werden, um eine optimale Leistung zu erzielen. | Fügen Sie die `async` Parameter im Inline-Skript, um die ordnungsgemäße Funktion der Tags sicherzustellen <br><br>[Zusätzliche Informationen](../../tags/ui/client-side/asynchronous-deployment.md) |
| Target - Inhalt in `mboxDefault` | 0 | Inhalt sollte vorhanden sein in `mboxDefault` bei Verwendung `at.js`. | Validieren Sie, ob der Inhalt verfügbar ist. <br><br>[Weitere Informationen](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |

{style="table-layout:auto"}
