---
keywords: Experience Platform;home;popular topics;kafka;kafka connector;Kafka;
solution: Experience Platform
title: Kafka-Connector
topic: overview
description: Der Stream-Connector für Adobe Experience Platform basiert auf Apache Kafka Connect. Mit dieser Bibliothek können Sie JSON-Ereignisse von Kafka-Themen in Ihrem Rechenzentrum in Echtzeit direkt an Experience Platform zu streamen.
translation-type: tm+mt
source-git-commit: 7fc7f0e525d994904dc71b1eb7136f11c05d5672
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 42%

---


# [!DNL Kafka] Anschluss für Adobe Experience Platform

The stream connector for Adobe Experience Platform is based on [!DNL Apache Kafka Connect]. This library can be used to stream JSON events from [!DNL Kafka] topics in your data center directly to [!DNL Experience Platform] in real-time.

The stream connector is a sink (one-way) connector, delivering data from [!DNL Kafka] topics to a registered endpoint on [!DNL Experience Platform]. To use this connector, you must download the library, add it to your existing [!DNL Kafka] deployment, and configure the [!DNL Kafka] topic(s) to the Adobe Streaming HTTP URL. Es ist **kein** zusätzlicher Code erforderlich. Der Connector unterstützt die folgenden Funktionen:

- Authentifizierte Datenerfassung
- Nachrichten-Batches, um Netzwerkaufrufe zu reduzieren und den Durchsatz zu erhöhen

For more information on the [!DNL Kafka] connector, including instructions on how to set up the connector, please read the [getting started guide](https://github.com/adobe/experience-platform-streaming-connect). Einen detaillierteren Workflow finden Sie im [Entwicklerhandbuch](https://www.adobe.com/go/kafka-connector-developer-guide).