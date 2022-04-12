---
title: Tag-Präsenz-Test-Referenz
description: Erfahren Sie, wie die Auditor-Funktion im Adobe Experience Platform Debugger Tests auf Tag-Präsenz durchführt.
exl-id: 8f01f89e-2a3b-41bc-b971-f3c60d0ae3fa
source-git-commit: 10a5605c40143b58f6ba0108cc087956aa929866
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 34%

---

# Testreferenz für Tag-Präsenz

Diese Referenz enthält weitere Informationen dazu, wie die Auditor-Funktion in Adobe Experience Platform Debugger-Tests auf Tag-Präsenz funktioniert.

>[!NOTE]
>
>Weitere Informationen zu Auditor-Tests in Platform Debugger finden Sie in der [Übersicht über Auditor-Funktionen](./overview.md).

Anhand von Tag-Präsenz-Tests wird geprüft, ob bestimmte Tags auf der Seite vorhanden sind und ob sie sich an der richtigen Stelle im Seiten-Code befinden.

| Test | Gewichtung | Kriterien | Empfehlung |
| --- | --- | --- | --- |
| Advertising Cloud – Codepräsenz | 5 | Das Advertising Cloud-Tag ist im DOM nicht verfügbar. | Implementieren Sie das Advertising Cloud-Tag mit dem [Advertising Cloud-Tag-Erweiterung](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud – Segmentpixel sind implementiert | 5 | Aktualisieren Sie Ihre Advertising Cloud-Segmentpixel auf die neuen „Nur Bild“-Tags der Advertising Cloud. Die Verwendung der nicht mehr unterstützten AMO-Segment-Tags kann zu Datenverlust führen. | Implementieren Sie das Advertising Cloud-Segmentpixel mit dem [Advertising Cloud-Tag-Erweiterung](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Analytics – Ist in DOM geladen | 5 | Das Adobe Analytics-Tag wurde nicht erkannt. | Installieren Sie die neueste Version von Analytics. <br><br>[Weitere Informationen](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=de) |
| Launch – Bibliothek ist geladen | 5 | A `global _satellite` -Objekt wurde im DOM nicht gefunden, was bedeutet, dass die Tag-Bibliothek entweder nicht installiert ist oder nicht ausgeführt werden kann. | Stellen Sie sicher, dass die Tag-Bibliothek auf der Seite implementiert ist und nicht von nachfolgenden Skriptaktivitäten blockiert wird. |
| Launch – Nicht mehrere Einbettungsskripte angeben | 5 | Produktions-Sites sollten nur einen Einbettungscode pro Seite laden. | Vergewissern Sie sich, dass nur die Produktionsbibliothek auf der Seite geladen wird. |
| Launch - `pageBottom` Rückruf ist in vorhanden `<body>` | 5 | Die erforderlichen `_satellite.pageBottom()` Rückruf wurde im `<body>` der Seite. Dieser Test schlägt fehl, wenn die `pageBottom` -Aufruf überhaupt nicht auf der Seite gefunden wird oder sich im `<head>` -Tag (oder eine andere unerwartete Position). Sie wird nur dann bestanden, wenn `pageBottom` befindet sich irgendwo in der `<body>` -Tag. | Fügen Sie das Inline-Skript unmittelbar vor dem schließenden `</body>` Tags verwenden, um eine ordnungsgemäße Funktion der Tags sicherzustellen.<br><br>[Weitere Informationen](../../tags/ui/client-side/asynchronous-deployment.md) |
| Launch - `pageBottom` Rückruf sollte bei asynchroner Bereitstellung nicht vorhanden sein | 5 | Die `_satellite.pageBottom()` -Rückruf wurde auf der Seite gefunden, was bei asynchroner Bereitstellung von Tags nicht der Fall sein sollte. | Entfernen Sie die `_satellite.pageBottom()` Skript, um die ordnungsgemäße Funktion der Tags zu aktivieren. <br><br>[Weitere Informationen](../../tags/ui/client-side/asynchronous-deployment.md) |
| Experience Cloud ID-Service – Codepräsenz | 5 | Der Experience Cloud ID-Service-Code wurde nicht gefunden. Die Verwendung von Experience Cloud-IDs (ECIDs) wird dringend empfohlen, um sicherzustellen, dass Sie Ihre Experience Cloud-Lösungen optimal nutzen. Sie ist außerdem für das ID-Management in allen Experience Cloud-Lösungen von entscheidender Bedeutung. | Installieren Sie die neueste Version von ECID.<br><br>[Weitere Informationen](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=de) |
| Experience Cloud ID-Service – Cookiepräsenz | 5 | Die `AMCV_` -Cookie nicht gefunden. Sie müssen ein Besucherobjekt aus dem Code `VisitorAPI.js`   instanziieren. | Wenn es sich um eine Implementierung von Tags handelt, überprüfen Sie, ob die AdobeOrg-ID richtig in das ECID-Tool eingegeben wurde. <br><br>[Weitere Informationen](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html?lang=de) |
| Experience Cloud ID-Service – MID-Wert ist vorhanden | 5 | Der MID-Wert wurde im `AMCV_` Cookie. | Testen Sie erneut, um nach einer beliebigen ECID-API-Latenz zu suchen. Wenn diese Bedingung weiterhin besteht, wenden Sie sich an die Adobe-Kundenunterstützung. <br><br>[Weitere Informationen](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html) |
| Target – Codepräsenz | 5 | Adobe Target sollte im DOM definiert werden. | Installieren Sie die neueste Version von Target (at.js). <br><br>[Weitere Informationen](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |
| Target - Bibliothek wird in geladen `<head>` | 4 | Die Target-Bibliothek sollte in die `<head>` -Tag. | Vergewissern Sie sich, dass die Target-Bibliothek in die `<head>` -Tag. <br><br>[Weitere Informationen](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |

{style=&quot;table-layout:auto&quot;}
