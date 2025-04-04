---
title: Protokollierung von Adobe Analytics for Target (A4T) in der Experience Platform Web SDK
description: Erfahren Sie, wie Sie die Erfassung von Daten aus Adobe Analytics for Target (A4T) mit der Experience Platform Web SDK steuern.
seo-title: Adobe Analytics for Target (A4T) Logging in the Experience Platform Web SDK
seo-description: Learn how to control the collection of Adobe Analytics for Target (A4T) data using the Experience Platform Web SDK.
keywords: a4t;Protokollierung;Analytics;SDK;Web SDK;
exl-id: f1c90ccd-48a9-4668-b2ac-eacd5bec0b91
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 1%

---

# Protokollierung von Adobe Analytics for Target (A4T) in der Experience Platform Web SDK

Bei der Verwendung von Adobe Target für die Personalisierung können Sie auswählen, welches System Sie für die Leistungsmessung verwenden möchten. Jede [Target-Aktivität](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html?lang=de) ermöglicht die Auswahl zwischen Target-Berichten und Adobe Analytics-Berichten.

Wenn Sie Analytics-Reporting verwenden, muss Adobe Target Analytics Folgendes mitteilen:

* Die von Ihren Besuchern eingegebene Adobe Target-Aktivität
* Welche Erfahrung sie gesehen haben
* Welche Konversion erreicht wurde

Adobe Experience Platform Web SDK unterstützt zwei Arten von Anwendungsfällen der Analytics-Protokollierung für Analytics for Target (A4T):

| Protokollierungsmethode | Beschreibung |
| --- | --- |
| Server-seitige Analytics-Protokollierung | Alle über die Edge Network gesendeten Analytics-Treffer werden Server-seitig um Target-Details erweitert, ohne dass der Trefferzusammenfügungsprozess durchlaufen werden muss. |
| Client-seitige Analytics-Protokollierung | Target-Daten werden Client-seitig zurückgegeben, sodass Sie Daten manuell erweitern und über die „Data Insertion[API an Analytics senden ](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html). |

Die Protokollierungsmethode wird davon bestimmt, ob Adobe Analytics in Ihrem konfigurierten (Datenstrom[ aktiviert ](../../../../datastreams/overview.md):

![Entscheidungsfluss der Protokollierungsmethode](../assets/analytics-logging.png)

## Nächste Schritte

Dieses Dokument bietet eine kurze Einführung in die verschiedenen Protokollierungsmethoden für A4T-Daten in der Web-SDK. Weitere Informationen zu den einzelnen Methoden finden Sie in der folgenden Dokumentation:

* [Server-seitige Protokollierung für A4T-Daten in der Experience Platform Web SDK](./server-side.md)
* [Client-seitige Protokollierung für A4T-Daten in der Experience Platform Web SDK](./client-side.md)
