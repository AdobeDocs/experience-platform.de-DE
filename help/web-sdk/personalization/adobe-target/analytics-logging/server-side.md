---
title: Server-seitige Protokollierung für A4T-Daten in Experience Platform Web SDK
description: Erfahren Sie, wie Sie die Server-seitige Protokollierung für Adobe Analytics for Target (A4T) mithilfe der Experience Platform Web SDK aktivieren.
seo-title: Server-side logging for A4T data in Experience Platform Web SDK
seo-description: Learn how to enable server-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: a4t;Target;Web;SDK;Plattform;Protokollierung;
exl-id: 26c25f58-e43c-4147-8595-69ea85af561f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 1%

---

# Server-seitige Protokollierung für A4T-Daten in Experience Platform Web SDK

Mit der Adobe Experience Platform Web SDK können Sie die Funktionen von Adobe Analytics for Target (A4T) in Experience Platform Edge Network implementieren. Wenn die Server-seitige Protokollierung aktiviert ist, werden alle über die Edge Network gesendeten Analytics-Treffer Server-seitig mit Target-Details erweitert, ohne dass der Trefferzusammenfügungsprozess durchlaufen werden muss.

Die Server-seitige Protokollierung für Analytics ist aktiviert, wenn Analytics in der Datenstromkonfiguration aktiviert ist:

![Analytics-Datenstromkonfiguration aktiviert](../assets/enable-analytics-datastream.png)

Das folgende Diagramm zeigt, wie Daten durch das System fließen, wenn die Server-seitige Analytics-Protokollierung aktiviert ist:

![Server-seitiger Protokollierungsfluss](../assets/analytics-server-side-logging.png)

## Nächste Schritte

In diesem Handbuch wurde die Server-seitige Protokollierung für A4T-Daten in der Web-SDK behandelt. Weitere Informationen zum [&#x200B; von A4T-Daten auf der Client](./client-side.md)Seite finden Sie im Handbuch zur Client-seitigen Protokollierung .
