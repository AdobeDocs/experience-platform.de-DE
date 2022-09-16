---
title: Serverseitige Protokollierung für A4T-Daten im Platform Web SDK
description: Erfahren Sie, wie Sie die serverseitige Protokollierung für Adobe Analytics for Target (A4T) mithilfe des Experience Platform Web SDK aktivieren.
seo-title: Server-side logging for A4T data in Platform Web SDK
seo-description: Learn how to enable server-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: a4t; Target; Web; SDK; Plattform; Protokollierung
exl-id: 26c25f58-e43c-4147-8595-69ea85af561f
source-git-commit: 38d54b2c793c9dcb1a45ec4acbb9016d1e927d23
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 1%

---

# Serverseitige Protokollierung für A4T-Daten im Platform Web SDK

Mit dem Adobe Experience Platform Web SDK können Sie die A4T-Funktionalität (Adobe Analytics for Target) im Platform Edge Network implementieren. Wenn die serverseitige Protokollierung aktiviert ist, werden alle Analytics-Treffer, die über das Edge Network gesendet werden, mit Target-Details auf der Server-Seite erweitert, ohne dass der Trefferzuordnungsprozess durchlaufen werden muss.

Die serverseitige Protokollierung für Analytics ist aktiviert, wenn Analytics in der Datastream-Konfiguration aktiviert ist:

![Aktivierung der Analytics-Datastream-Konfiguration](../assets/enable-analytics-datastream.png)

Das folgende Diagramm zeigt, wie Daten durch das System fließen, wenn die serverseitige Analytics-Protokollierung aktiviert ist:

![Serverseitiger Protokollierungsfluss](../assets/analytics-server-side-logging.png)

## Nächste Schritte

In diesem Handbuch wurde die serverseitige Protokollierung für A4T-Daten im Web SDK behandelt. Siehe Handbuch unter [Clientseitige Protokollierung](./client-side.md) für weitere Informationen zur Verarbeitung von A4T-Daten auf Clientseite.
