---
keywords: Experience Platform; Startseite; beliebte Themen; Kafka; Kafka-Connector; Kafka;
solution: Experience Platform
title: Kafka Connector
topic-legacy: overview
description: Der Stream-Connector für Adobe Experience Platform basiert auf Apache Kafka Connect. Mit dieser Bibliothek können Sie JSON-Ereignisse von Kafka-Themen in Ihrem Rechenzentrum direkt an die Experience Platform in Echtzeit streamen.
exl-id: 062963e5-c727-4c2c-97db-8a9a5a7d903c
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 27%

---

# [!DNL Kafka] Connector für Adobe Experience Platform

Der Stream-Connector für Adobe Experience Platform basiert auf [!DNL Apache Kafka Connect]. Diese Bibliothek kann verwendet werden, um JSON-Ereignisse von [!DNL Kafka]-Themen in Ihrem Rechenzentrum direkt an [!DNL Experience Platform] in Echtzeit zu streamen.

Der Stream-Connector ist ein Einweg-Connector, der Daten von [!DNL Kafka]-Themen an einen registrierten Endpunkt unter [!DNL Experience Platform] sendet. Um diesen Connector zu verwenden, müssen Sie die Bibliothek herunterladen, sie zu Ihrer vorhandenen [!DNL Kafka]-Bereitstellung hinzufügen und die [!DNL Kafka] Themen zur Adobe Streaming-HTTP-URL konfigurieren. Es ist **kein** zusätzlicher Code erforderlich. Der Connector unterstützt die folgenden Funktionen:

- Authentifizierte Datenerfassung
- Nachrichten-Batches, um Netzwerkaufrufe zu reduzieren und den Durchsatz zu erhöhen

Weitere Informationen zum Connector [!DNL Kafka], einschließlich Anweisungen zum Einrichten des Connectors, finden Sie im [Erste Schritte-Handbuch](https://github.com/adobe/experience-platform-streaming-connect). Einen detaillierteren Workflow finden Sie im [Entwicklerhandbuch](https://www.adobe.com/go/kafka-connector-developer-guide).
