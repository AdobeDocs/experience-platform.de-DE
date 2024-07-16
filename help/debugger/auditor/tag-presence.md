---
title: Tag-Präsenz-Test-Referenz
description: Erfahren Sie, wie die Auditor-Funktion Tests auf Tag-Präsenz in Adobe Experience Platform Debugger durchführt.
exl-id: 8f01f89e-2a3b-41bc-b971-f3c60d0ae3fa
source-git-commit: 10a5605c40143b58f6ba0108cc087956aa929866
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 17%

---

# Testreferenz für Tag-Präsenz

Diese Referenz enthält weitere Informationen dazu, wie die Auditor-Funktion in Adobe Experience Platform Debugger-Tests auf Tag-Präsenz funktioniert.

>[!NOTE]
>
>Weitere Informationen zu Auditor-Tests in Platform Debugger finden Sie in der Übersicht über die Auditor-Funktion [1}.](./overview.md)

Anhand von Tag-Präsenz-Tests wird geprüft, ob bestimmte Tags auf der Seite vorhanden sind und ob sie sich an der richtigen Stelle im Seiten-Code befinden.

| Test | Gewichtung | Kriterien | Empfehlung |
| --- | --- | --- | --- |
| Advertising Cloud - Codepräsenz | 5 | Das Advertising Cloud-Tag ist im DOM nicht verfügbar. | Implementieren Sie das Advertising Cloud-Tag mit der [Advertising Cloud-Tag-Erweiterung](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud - Segmentpixel sind implementiert | 5 | Aktualisieren Sie Ihre Advertising Cloud-Segmentpixel auf die neuen „Nur Bild“-Tags der Advertising Cloud. Die Verwendung der nicht mehr unterstützten AMO-Segment-Tags kann zu Datenverlust führen. | Implementieren Sie das Advertising Cloud-Segmentpixel mit der [Advertising Cloud-Tag-Erweiterung](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Analytics - In DOM geladen | 5 | Das Adobe Analytics-Tag wurde nicht erkannt. | Installieren Sie die neueste Version von Analytics. <br><br>[Weitere Informationen](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=de) |
| Launch - Bibliothek wird geladen | 5 | Ein `global _satellite` -Objekt wurde im DOM nicht gefunden, was bedeutet, dass die Tag-Bibliothek entweder nicht installiert ist oder nicht ausgeführt werden kann. | Stellen Sie sicher, dass die Tag-Bibliothek auf der Seite implementiert ist und nicht von nachfolgenden Skriptaktivitäten blockiert wird. |
| Launch - Nicht mehrere Einbettungsskripte haben | 5 | Produktions-Sites sollten nur einen Einbettungscode pro Seite laden. | Vergewissern Sie sich, dass nur die Produktionsbibliothek auf der Seite geladen wird. |
| Launch - `pageBottom` Rückruf ist in `<body>` vorhanden | 5 | Der erforderliche `_satellite.pageBottom()` -Rückruf wurde im `<body>` der Seite nicht gefunden. Dieser Test schlägt fehl, wenn der `pageBottom` -Aufruf überhaupt nicht auf der Seite gefunden wird oder sich im `<head>` -Tag (oder an einer anderen unerwarteten Position) befindet. Sie wird nur übergeben, wenn `pageBottom` irgendwo im Tag `<body>` gefunden wird. | Fügen Sie das Inline-Skript unmittelbar vor dem schließenden `</body>` -Tag hinzu, um eine ordnungsgemäße Tag-Funktionalität sicherzustellen.<br><br>[Weitere Informationen](../../tags/ui/client-side/asynchronous-deployment.md) |
| Launch - `pageBottom` -Rückruf sollte bei asynchroner Bereitstellung nicht vorhanden sein | 5 | Der Rückruf `_satellite.pageBottom()` wurde auf der Seite gefunden, was bei asynchroner Bereitstellung von Tags nicht der Fall sein sollte. | Entfernen Sie das Skript `_satellite.pageBottom()` , um die ordnungsgemäße Funktion der Tags zu aktivieren. <br><br>[Weitere Informationen](../../tags/ui/client-side/asynchronous-deployment.md) |
| Experience Cloud ID-Dienst - Codepräsenz | 5 | Der Experience Cloud ID-Service-Code wurde nicht gefunden. Die Verwendung von Experience Cloud-IDs (ECIDs) wird dringend empfohlen, um sicherzustellen, dass Sie Ihre Experience Cloud-Lösungen optimal nutzen und für das ID-Management in allen Experience Cloud-Lösungen von entscheidender Bedeutung sind. | Installieren Sie die neueste Version von ECID.<br><br>[Weitere Informationen](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=de) |
| Experience Cloud ID-Dienst - Cookie-Präsenz | 5 | Das `AMCV_` -Cookie wurde nicht gefunden. Sie müssen ein Besucherobjekt aus dem Code `VisitorAPI.js` instanziieren. | Wenn es sich um eine Implementierung von Tags handelt, überprüfen Sie, ob die AdobeOrg-ID richtig in das ECID-Tool eingegeben wurde. <br><br>[Weitere Informationen](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html) |
| Experience Cloud ID-Dienst - MID-Wert vorhanden | 5 | Der MID-Wert wurde im `AMCV_` -Cookie nicht gefunden. | Testen Sie erneut, um nach einer beliebigen ECID-API-Latenz zu suchen. Wenn die Bedingung weiterhin besteht, wenden Sie sich an die Adobe-Kundenunterstützung. <br><br>[Weitere Informationen](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html) |
| Target - Codepräsenz | 5 | Adobe Target sollte im DOM definiert werden. | Installieren Sie die neueste Version von Target (at.js). <br><br>[Weitere Informationen](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |
| Target - Bibliothek wird in `<head>` geladen | 4 | Die Target-Bibliothek sollte im Tag `<head>` geladen werden. | Vergewissern Sie sich, dass die Target-Bibliothek im Tag `<head>` geladen wird. <br><br>[Weitere Informationen](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |

{style="table-layout:auto"}
