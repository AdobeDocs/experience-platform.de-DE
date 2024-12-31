---
title: Tag Presence Test Reference
description: Erfahren Sie, wie die Auditor-Funktion das Vorhandensein von Tags im Adobe Experience Platform Debugger testet.
exl-id: 8f01f89e-2a3b-41bc-b971-f3c60d0ae3fa
source-git-commit: 10a5605c40143b58f6ba0108cc087956aa929866
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 17%

---

# Tag Presence Test Reference

Diese Referenz enthält weitere Informationen darüber, wie die Auditor-Funktion in Adobe Experience Platform Debugger-Tests auf das Vorhandensein von Tags prüft.

>[!NOTE]
>
>Weitere Informationen zu Auditor-Tests in Platform Debugger finden Sie unter [Auditor-Funktion - Übersicht](./overview.md).

Tag-Präsenztests werten aus, ob bestimmte Tags auf der Seite vorhanden sind und ob sie sich an der richtigen Stelle im Seiten-Code befinden.

| Test | Gewichtung | Kriterien | Empfehlung |
| --- | --- | --- | --- |
| Advertising Cloud - Code-Präsenz | 5 | Das Advertising Cloud-Tag ist im DOM nicht verfügbar. | Implementieren Sie das Advertising Cloud-Tag mit der [Advertising Cloud-Tag-Erweiterung](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud - Segmentpixel implementiert | 5 | Aktualisieren Sie Ihre Advertising Cloud-Segmentpixel auf die neuen „Nur Bild“-Tags der Advertising Cloud. Die Verwendung der nicht mehr unterstützten AMO-Segment-Tags kann zu Datenverlust führen. | Implementieren Sie das Advertising Cloud-Segmentpixel mit der [Advertising Cloud-Tag-Erweiterung](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Analytics - im DOM geladen | 5 | Das Adobe Analytics-Tag wurde nicht erkannt. | Installieren Sie die neueste Version von Analytics. <br><br>[Weitere Informationen](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=de) |
| Launch - Bibliothek geladen | 5 | Im DOM wurde kein `global _satellite`-Objekt gefunden, was bedeutet, dass die Tag-Bibliothek entweder nicht installiert ist oder nicht ausgeführt werden kann. | Stellen Sie sicher, dass die Tag-Bibliothek auf der Seite implementiert ist und nicht durch nachfolgende Skriptaktivitäten blockiert wird. |
| Launch - Nicht mehrere Einbettungsskripte vorhanden | 5 | Produktions-Sites sollten nur einen Einbettungs-Code pro Seite laden. | Vergewissern Sie sich, dass nur die Produktionsbibliothek auf der Seite geladen wird. |
| Launch - `pageBottom` Callback ist in `<body>` vorhanden | 5 | Der erforderliche `_satellite.pageBottom()`-Callback wurde im `<body>` der Seite nicht gefunden. Dieser Test schlägt fehl, wenn der `pageBottom`-Aufruf überhaupt nicht auf der Seite gefunden wird oder sich im `<head>`-Tag (oder an einer anderen unerwarteten Stelle) befindet. Er wird nur übergeben, wenn `pageBottom` irgendwo im `<body>`-Tag gefunden wird. | Fügen Sie das Inline-Skript unmittelbar vor dem schließenden `</body>`-Tag hinzu, um eine ordnungsgemäße Tag-Funktionalität sicherzustellen.<br><br>[Weitere Informationen](../../tags/ui/client-side/asynchronous-deployment.md) |
| Launch - `pageBottom` Callback sollte bei asynchroner Bereitstellung nicht vorhanden sein | 5 | Der `_satellite.pageBottom()` Callback wurde auf der Seite gefunden, was nicht der Fall sein sollte, wenn Tags asynchron bereitgestellt werden. | Entfernen Sie das `_satellite.pageBottom()`-Skript, um die ordnungsgemäße Funktion von Tags zu aktivieren. <br><br>[Weitere Informationen](../../tags/ui/client-side/asynchronous-deployment.md) |
| Experience Cloud-ID-Service - Code-Präsenz | 5 | Der Experience Cloud ID-Service-Code wurde nicht gefunden. Die Verwendung von Experience Cloud-IDs (ECIDs) wird dringend empfohlen, um sicherzustellen, dass Sie Ihre Experience Cloud-Lösungen optimal nutzen. Dies ist auch für die ID-Verwaltung in allen Experience Cloud-Lösungen von entscheidender Bedeutung. | Installieren Sie die neueste Version von ECID.<br><br>[Weitere Informationen](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=de) |
| Experience Cloud-ID-Dienst - Cookie-Präsenz | 5 | Das `AMCV_` Cookie wurde nicht gefunden. Sie müssen ein Besucherobjekt aus dem `VisitorAPI.js`-Code instanziieren. | Wenn es sich um eine Tags-Implementierung handelt, stellen Sie sicher, dass die Adobe Org ID ordnungsgemäß in das ECID-Tool eingegeben wurde. <br><br>[Weitere Informationen](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html) |
| Experience Cloud-ID-Dienst - MID-Wert vorhanden | 5 | Der MID-Wert wurde im `AMCV_`-Cookie nicht gefunden. | Führen Sie einen erneuten Test durch, um auf eine ECID-API-Latenz zu prüfen. Wenn der Zustand weiterhin besteht, wenden Sie sich an die Adobe-Kundenunterstützung. <br><br>[Weitere Informationen](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html) |
| Target - Code-Präsenz | 5 | Adobe Target sollte im DOM definiert werden. | Installieren Sie die neueste Version von Target (at.js). <br><br>[Weitere Informationen](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |
| Target - Bibliothek in `<head>` geladen | 4 | Die Target-Bibliothek sollte im `<head>`-Tag geladen werden. | Stellen Sie sicher, dass die Target-Bibliothek im `<head>`-Tag geladen wird. <br><br>[Weitere Informationen](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |

{style="table-layout:auto"}
