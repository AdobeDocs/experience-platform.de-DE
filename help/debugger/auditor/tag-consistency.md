---
title: Tag-Konsistenztest-Referenz
description: Erfahren Sie, wie die Auditor-Funktion die Tag-Konsistenz im Adobe Experience Platform Debugger testet.
exl-id: 642b0c49-a7c7-4142-8189-67f00ed50015
source-git-commit: df1a67e4b6f3d2eaeaba2b8d3c9b1588ee0b1461
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 40%

---

# Tag-Konsistenztestreferenz

Diese Referenz enthält weitere Informationen darüber, wie die Auditor-Funktion in Adobe Experience Platform Debugger-Tests auf Tag-Konsistenz prüft.

>[!NOTE]
>
>Weitere Informationen zu Auditor-Tests in Platform Debugger finden Sie unter [Auditor-Funktion - Übersicht](./overview.md).

Tag-Konsistenztests suchen auf allen gescannten Seiten nach Inkonsistenzen. Dies sind Werte oder Konfigurationen, die auf allen Seiten der Site gleich sein sollten, um die genaue Datenerfassung sicherzustellen.

| Test | Gewichtung | Kriterien | Empfehlung |
| --- | --- | --- | --- |
| Adobe Analytics - Konsistente Code-Version | 5 | Es wurde mehr als eine Version des Analytics-Codes gefunden. | Ersetzen Sie alle Instanzen von Analytics durch die aktuelle Version.<br><br>[Weitere Informationen](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=de) |

{style="table-layout:auto"}
