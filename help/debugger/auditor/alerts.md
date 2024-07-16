---
title: Warnungstest-Referenz
description: Erfahren Sie, wie die Auditor-Funktion in Adobe Experience Platform Debugger auf Warnhinweise testet.
exl-id: ac6f8675-6c34-48b4-b5dd-48e92af217fd
source-git-commit: 10a5605c40143b58f6ba0108cc087956aa929866
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 13%

---

# Warnungstest

Diese Referenz enthält weitere Informationen dazu, wie die Auditor-Funktion in Adobe Experience Platform Debugger Warnungstests ausführt.

>[!NOTE]
>
>Weitere Informationen zu Auditor-Tests in Platform Debugger finden Sie in der Übersicht über die Auditor-Funktion [1}.](./overview.md)

Warnhinweise zeigen Probleme an, die Sie kennen sollten, aber sich nicht auf Ihr Ergebnis auswirken. Dies sind Best Practice-Empfehlungen, die in einigen Fällen nicht auf Ihre Implementierung zutreffen.

| Test | Gewichtung | Kriterien | Empfehlung |
| --- | --- | --- | --- |
| Advertising Cloud - Korrektes Konversions-Tag ist implementiert | 0 | Überprüfen Sie, ob das richtige Konversions-Tag verwendet wird.<br><br>**Warnung**: Die Verwendung der veralteten TubeMogul-Konversions-Tags kann zu Datenverlust führen. | Aktualisieren Sie Ihre Konversionspixel auf die neuen Advertising Cloud-Konversions-Tags, die nur für Bilder verfügbar sind. Dies lässt sich am einfachsten mit der [Advertising Cloud Tag-Erweiterung](../../destinations/catalog/advertising/adobe-advertising-cloud.md) erreichen. |
| Advertising Cloud - Korrektes verwendetes JS-Tag | 0 | Advertising Cloud sollte die neuesten JavaScript-Tags verwenden. | Aktualisieren Sie Ihr Advertising Cloud-JavaScript auf die neueste Version. Die Verwendung veralteter JavaScript-Versionen kann zu Funktionsverlust führen. Dies lässt sich durch die Verwendung der [Advertising Cloud Tag-Erweiterung](../../destinations/catalog/advertising/adobe-advertising-cloud.md) einfacher erreichen. |
| Advertising Cloud - Nur-Bild-Tag | 0 | Das Bildpixelformat der Advertising Cloud sollte mit einem der folgenden empfohlenen Formate übereinstimmen: <ul><li>`http(s)://rtd.tubemogul.com/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://rtd-tm.everesttech.net/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://pixel.everesttech.net/px2/<NUMERIC_ID>?`</li></ul> | Aktualisieren Sie Ihre Advertising Cloud-Pixel auf die neuen Nur-Bild-Tags von Advertising Cloud, um sicherzustellen, dass Sie die gesamte Advertising Cloud-Funktionalität nutzen. Dies lässt sich am einfachsten mit der [Advertising Cloud Tag-Erweiterung](../../destinations/catalog/advertising/adobe-advertising-cloud.md) erreichen. |
| Advertising Cloud - DSP Synchronisierung ist für Segmentpixel aktiviert | 0 | Überprüfen Sie, ob das TubeMogul-Segmentpixel eine DSP Synchronisierungseinstellung enthält, und empfehlen Sie, die Einstellung dem Pixel hinzuzufügen. Die Einstellung DSP Synchronisierung wird durch die Verwendung eines Abfragezeichenfolgenparameters bestimmt. Zur Zusammenfassung: <ul><li>WENN das -Tag für einen der folgenden Ereignisse ausgelöst wird:<ul><li>`https://rtd.tubemogul.com/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://rtd-tm.everesttech.net/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://pixel.everesttech.net/px2/<NUMERIC_ID>?`</li></ul></li><li>UND das Tag den URL-Parameter `sid=` enthält</li><li>Überprüfen Sie DANN, ob der URL-Parameter `cs=0` oder `cs=1` vorhanden ist, und empfehlen Sie, diesen Pixeln `cs=1` hinzuzufügen, damit die Übereinstimmungsraten der Zielgruppe verbessert werden können.</li></ul> | Fügen Sie Ihren Advertising Cloud-Pixeln den URL-Parameter `cs=1` hinzu, damit eine DSP Synchronisierung stattfinden kann, wodurch die Übereinstimmungsraten der Zielgruppe erhöht werden. Dies lässt sich am einfachsten mit der [Advertising Cloud Tag-Erweiterung](../../destinations/catalog/advertising/adobe-advertising-cloud.md) erreichen. |
| Experience Cloud ID-Dienst - Nur eine AdobeOrg verwenden | 0 | In einer normalen ECID-Implementierung sollte eine einzelne AdobeOrg verwendet werden. | Überprüfen Sie, ob für diese Implementierung mehrere AdobeOrg-IDs vorhanden sind. <br><br>[Weitere Informationen](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html) |
| Launch - Callback-Platzierung `pageBottom` | 0 | Die Funktion `_satellite.pageBottom()` muss vorhanden sein, damit Tags funktionieren. Fügen Sie das Inline-Skript unmittelbar vor dem schließenden `</body>` -Tag hinzu, um eine ordnungsgemäße DTM-Funktionalität sicherzustellen. Hinweis: Es ist Best Practice, dass das Tag das letzte Tag im `<body>` ist. Wenn es im Tag `<body>` gefunden wird, kann es eventuell funktionieren, doch da es sich hierbei nicht um eine Best Practice handelt, könnte es falsch oder mit unerwarteten oder unerwünschten Ergebnissen funktionieren. | Fügen Sie das Inline-Skript unmittelbar vor dem schließenden `</body>` -Tag hinzu, um eine ordnungsgemäße DTM-Funktionalität sicherzustellen. <br><br>[Weitere Informationen](../../tags/ui/client-side/asynchronous-deployment.md) |
| Launch - Self-Hosting | 0 | Die Bibliothek wird auf der Tag--Akamai-Instanz unter `assets.adobedtm.com` gehostet. Das Self-Hosting ist der empfohlene Ansatz zum Laden von Tags, da es die Leistung von Websites durch Cache-Steuerung, Reduzierung der Skriptabhängigkeiten von Drittanbietern und bessere Steuerung des Veröffentlichungsprozesses verbessert. Tag-Bibliotheken können über Ihr eigenes Web-Hosting oder CDN gehostet und verwaltet werden. | Beim Wechsel zu einem Self-Hosting wird versucht, Tags auf einer Seite zu laden. Obwohl das Hosting über das Akamai CDN in den meisten Fällen funktioniert, verbessert das Self-Hosting die Seitenleistung. <br><br>Zusätzliche Informationen:<ul><li>[Schnellstartanleitung für Tags](../../tags/ui/client-side/asynchronous-deployment.md)</li><li>[Asynchrone Bereitstellung](../../tags/ui/client-side/asynchronous-deployment.md)</li></ul> |
| Launch - Sollte asynchron bereitgestellt werden | 0 | Tags sollten asynchron bereitgestellt werden, um eine optimale Leistung zu erzielen. | Fügen Sie den Parameter `async` in das Inline-Skript ein, um die ordnungsgemäße Funktion der Tags sicherzustellen <br><br>[Zusätzliche Informationen](../../tags/ui/client-side/asynchronous-deployment.md) |
| Target - Inhalt in `mboxDefault` | 0 | Bei Verwendung von `at.js` sollte Inhalt in `mboxDefault` vorhanden sein. | Stellen Sie sicher, dass der Inhalt verfügbar ist. <br><br>[Weitere Informationen](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |

{style="table-layout:auto"}
