---
title: Protokollierung von Adobe Analytics for Target (A4T) im Platform Web SDK
description: Erfahren Sie, wie Sie die Erfassung von Adobe Analytics for Target-Daten (A4T) mithilfe des Experience Platform Web SDK steuern.
seo-title: Adobe Analytics for Target (A4T) Logging in the Platform Web SDK
seo-description: Learn how to control the collection of Adobe Analytics for Target (A4T) data using the Experience Platform Web SDK.
keywords: a4t; Protokollierung; Analytics; SDK; Web SDK;
exl-id: f1c90ccd-48a9-4668-b2ac-eacd5bec0b91
source-git-commit: fb0d8aedbb88aad8ed65592e0b706bd17840406b
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 4%

---

# Protokollierung von Adobe Analytics for Target (A4T) im Platform Web SDK

Bei der Verwendung von Adobe Target zur Personalisierung können Sie auswählen, welches System für die Leistungsmessung verwendet werden soll. Jeder [Target-Aktivität](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html?lang=de) ermöglicht Ihnen die Auswahl zwischen Target-Berichterstellung und Adobe Analytics-Berichterstellung.

Wenn Sie Analytics-Berichte verwenden, muss Adobe Target Analytics Folgendes mitteilen:

* Welche Adobe Target-Aktivität Ihre Besucher eingegeben haben
* Welche Erfahrung haben sie gesehen?
* Welche Konversion wurde erreicht?

Das Adobe Experience Platform Web SDK unterstützt zwei Arten von Analytics-Protokollierung für Analytics for Target (A4T)-Anwendungsfälle:

| Protokollierungsmethode | Beschreibung |
| --- | --- |
| Serverseitige Analytics-Protokollierung | Alle Analytics-Treffer, die über das Edge-Netzwerk gesendet werden, werden mit Target-Details auf der Server-Seite erweitert, ohne den Trefferzuordnungsprozess durchlaufen zu müssen. |
| Clientseitige Analytics-Protokollierung | Target-Daten werden Client-seitig zurückgegeben, sodass Sie Daten mithilfe der [Dateneinfüge-API](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html). |

Die Protokollierungsmethode hängt davon ab, ob Adobe Analytics in Ihrer Konfiguration aktiviert ist. [datastream](../../../datastreams/overview.md):

![Entscheidungsfluss der Protokollierungsmethode](../assets/analytics-logging.png)

## Nächste Schritte

In diesem Dokument erhalten Sie eine kurze Einführung in die verschiedenen Protokollierungsmethoden für A4T-Daten im Web SDK. Weitere Informationen zu den einzelnen Methoden finden Sie in der folgenden Dokumentation:

* [Serverseitige Protokollierung für A4T-Daten im Platform Web SDK](./server-side.md)
* [Clientseitige Protokollierung für A4T-Daten im Platform Web SDK](./client-side.md)
