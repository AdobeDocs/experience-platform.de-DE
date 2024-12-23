---
title: Referenz zu Tag-Konsistenztests
description: Erfahren Sie, wie die Auditor-Funktion in Adobe Experience Platform Debugger Tests zur Tag-Konsistenz durchführt.
exl-id: 642b0c49-a7c7-4142-8189-67f00ed50015
source-git-commit: df1a67e4b6f3d2eaeaba2b8d3c9b1588ee0b1461
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 40%

---

# Tag-Konsistenztest

Diese Referenz enthält weitere Informationen dazu, wie die Auditor-Funktion in Adobe Experience Platform Debugger-Tests zur Tag-Konsistenz verwendet wird.

>[!NOTE]
>
>Weitere Informationen zu Auditor-Tests in Platform Debugger finden Sie in der Übersicht über die Auditor-Funktion [1}.](./overview.md)

Tag-Konsistenztests suchen Inkonsistenzen auf allen geprüften Seiten. Dies sind Werte oder Konfigurationen, die auf allen Seiten der Site gleich sein sollten, um die genaue Datenerfassung sicherzustellen.

| Test | Gewichtung | Kriterien | Empfehlung |
| --- | --- | --- | --- |
| Adobe Analytics - Konsistente Codeversion | 5 | Es wurde mehr als eine Version des Analytics-Codes gefunden. | Ersetzen Sie alle Instanzen von Analytics durch die aktuelle Version.<br><br>[Weitere Informationen](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=de) |

{style="table-layout:auto"}
