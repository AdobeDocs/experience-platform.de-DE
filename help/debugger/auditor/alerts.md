---
title: Referenz für Warnhinweistest
description: Erfahren Sie, wie die Auditor-Funktion im Adobe Experience Platform Debugger auf Warnhinweise testet.
exl-id: ac6f8675-6c34-48b4-b5dd-48e92af217fd
source-git-commit: 10a5605c40143b58f6ba0108cc087956aa929866
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 13%

---

# Referenz für Warnhinweistest

Diese Referenz enthält weitere Informationen darüber, wie die Auditor-Funktion in Adobe Experience Platform Debugger Warnhinweistests ausführt.

>[!NOTE]
>
>Weitere Informationen zu Auditor-Tests in Platform Debugger finden Sie unter [Auditor-Funktion - Übersicht](./overview.md).

Warnhinweise zeigen Probleme an, die Sie kennen sollten, aber sich nicht auf Ihr Ergebnis auswirken. Dies sind Best Practice-Empfehlungen, die in einigen Fällen nicht auf Ihre Implementierung zutreffen.

| Test | Gewichtung | Kriterien | Empfehlung |
| --- | --- | --- | --- |
| Advertising Cloud - richtiges Konvertierungs-Tag implementiert | 0 | Überprüfen Sie, ob das richtige Konversions-Tag verwendet wird.<br><br>**Warnung**: Die Verwendung der veralteten TubeMogul-Konvertierungs-Tags kann zu Datenverlust führen. | Aktualisieren Sie Ihre Konversionspixel auf die neuen Konvertierungs-Tags für reine Advertising Cloud-Bilder. Dies lässt sich am einfachsten mit der [Advertising Cloud-Tag-Erweiterung](../../destinations/catalog/advertising/adobe-advertising-cloud.md) erreichen. |
| Advertising Cloud - richtiges JS-Tag verwendet | 0 | Advertising Cloud sollte die neuesten JavaScript-Tags verwenden. | Aktualisieren Sie Ihr Advertising Cloud-JavaScript auf die neueste Version. Die Verwendung der veralteten JavaScript-Versionen kann zu Funktionsverlusten führen. Dies lässt sich durch die Verwendung der [Advertising Cloud-Tag-Erweiterung](../../destinations/catalog/advertising/adobe-advertising-cloud.md) einfacher erreichen. |
| Advertising Cloud - Tag „Nur Bild“ | 0 | Das Bildpixelformat der Advertising Cloud sollte mit einem der folgenden empfohlenen Formate übereinstimmen: <ul><li>`http(s)://rtd.tubemogul.com/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://rtd-tm.everesttech.net/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://pixel.everesttech.net/px2/<NUMERIC_ID>?`</li></ul> | Aktualisieren Sie Ihre Advertising Cloud-Pixel auf die neuen Advertising Cloud-Tags nur für Bilder, um sicherzustellen, dass Sie alle Funktionen von Advertising Cloud nutzen. Dies lässt sich am einfachsten mit der [Advertising Cloud-Tag-Erweiterung](../../destinations/catalog/advertising/adobe-advertising-cloud.md) erreichen. |
| Advertising Cloud - DSP-Synchronisierung der Segmentpixel aktiviert | 0 | Überprüfen Sie, ob das TubeMogul-Segmentpixel eine DSP-Synchronisierungseinstellung enthält, und empfehlen Sie, dass die Einstellung dem Pixel hinzugefügt wird. Die Einstellung für die DSP-Synchronisierung wird durch die Verwendung eines Abfragezeichenfolgenparameters bestimmt. Zur Zusammenfassung: <ul><li>WENN das Tag für eine der folgenden Aktionen ausgelöst wird:<ul><li>`https://rtd.tubemogul.com/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://rtd-tm.everesttech.net/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://pixel.everesttech.net/px2/<NUMERIC_ID>?`</li></ul></li><li>UND das Tag enthält den URL-Parameter `sid=`</li><li>Überprüfen Sie ANSCHLIESSEND, ob der URL-Parameter `cs=0` oder `cs=1` vorhanden ist, und empfehlen Sie, diesen Pixeln `cs=1` hinzuzufügen, damit die Übereinstimmungsraten der Zielgruppe verbessert werden können.</li></ul> | Fügen Sie die URL-`cs=1` zu Ihren Advertising Cloud-Pixeln hinzu, damit die DSP-Synchronisierung erfolgen kann, wodurch sich die Übereinstimmungsraten der Zielgruppen erhöhen. Dies lässt sich am einfachsten mit der [Advertising Cloud-Tag-Erweiterung](../../destinations/catalog/advertising/adobe-advertising-cloud.md) erreichen. |
| Experience Cloud-ID-Dienst - Nur eine AdobeOrg verwenden | 0 | In einer normalen ECID-Implementierung sollte eine einzelne AdobeOrg verwendet werden. | Überprüfen, ob mehrere AdobeOrg-IDs für diese Implementierung vorhanden sind. <br><br>[Weitere Informationen](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html) |
| Launch - `pageBottom` Callback-Platzierung | 0 | Die `_satellite.pageBottom()` muss vorhanden sein, damit Tags funktionieren. Fügen Sie das Inline-Skript unmittelbar vor dem schließenden `</body>`-Tag hinzu, um eine ordnungsgemäße DTM-Funktionalität sicherzustellen. Hinweis: Es empfiehlt sich, das -Tag als letztes -Tag im -`<body>` zu markieren. Wenn er im `<body>`-Tag gefunden wird, kann er möglicherweise funktionieren, aber da es sich nicht um Best Practice handelt, kann er falsch oder mit unerwarteten oder unerwünschten Ergebnissen funktionieren. | Fügen Sie das Inline-Skript unmittelbar vor dem schließenden `</body>`-Tag hinzu, um eine ordnungsgemäße DTM-Funktionalität sicherzustellen. <br><br>[Weitere Informationen](../../tags/ui/client-side/asynchronous-deployment.md) |
| Launch - selbst gehostet | 0 | Die Tag-Bibliothek wird auf der Akamai-Instanz von Adobe unter `assets.adobedtm.com` gehostet. Das Self-Hosting ist der empfohlene Ansatz für das Laden von Tags, da es durch Cache-Steuerung eine bessere Kontrolle über die Website-Leistung bietet, die Abhängigkeiten von Drittanbieterskripten reduziert und den Veröffentlichungsprozess besser steuert. Tag-Bibliotheken können über Ihr eigenes Web-Hosting oder CDN gehostet und verwaltet werden. | Wechseln Sie zu einem Self-Hosting-Ansatz, um Tags auf einer Seite zu laden. Obwohl das Hosting über das Akamai-CDN in den meisten Fällen funktioniert, verbessert Self-Hosting die Seitenleistung. <br><br>Weitere Informationen:<ul><li>[Tags-Schnellstartanleitung](../../tags/ui/client-side/asynchronous-deployment.md)</li><li>[Asynchrone Bereitstellung](../../tags/ui/client-side/asynchronous-deployment.md)</li></ul> |
| Launch - sollte asynchron bereitgestellt werden | 0 | Tags sollten asynchron bereitgestellt werden, um eine optimale Leistung zu erzielen. | Schließen Sie den `async`-Parameter in das Inline-Skript ein, um eine ordnungsgemäße Tag-Funktionalität sicherzustellen <br><br>[Zusätzliche Informationen](../../tags/ui/client-side/asynchronous-deployment.md) |
| Target - Inhalt in `mboxDefault` | 0 | Inhalte sollten in `mboxDefault` vorhanden sein, wenn Sie `at.js` verwenden. | Überprüfen, ob der Inhalt verfügbar ist. <br><br>[Weitere Informationen](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |

{style="table-layout:auto"}
