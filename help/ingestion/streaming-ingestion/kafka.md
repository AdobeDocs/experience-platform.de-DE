---
keywords: Experience Platform;home;popular topics;kafka;kafka connector;Kafka;
solution: Experience Platform
title: Kafka Connector
description: Der Stream-Connector für Adobe Experience Platform basiert auf Apache Kafka Connect. Diese Bibliothek kann verwendet werden, um JSON-Ereignisse von Kafka-Themen in Ihrem Rechenzentrum direkt auf Experience Platform in Echtzeit zu streamen.
exl-id: 062963e5-c727-4c2c-97db-8a9a5a7d903c
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 26%

---

# [!DNL Kafka] Connector für Adobe Experience Platform

Der Stream-Connector für Adobe Experience Platform basiert auf [!DNL Apache Kafka Connect]. Mit dieser Bibliothek können Sie JSON-Ereignisse von [!DNL Kafka] -Themen in Ihrem Rechenzentrum in Echtzeit direkt auf [!DNL Experience Platform] streamen.

Der Stream-Connector ist ein Einweg-Connector, der Daten von [!DNL Kafka] -Themen an einen registrierten Endpunkt unter [!DNL Experience Platform] sendet. Um diesen Connector zu verwenden, müssen Sie die Bibliothek herunterladen, sie zu Ihrer vorhandenen [!DNL Kafka]-Bereitstellung hinzufügen und die [!DNL Kafka] Themen zur Adobe-Streaming-HTTP-URL konfigurieren. Es ist **kein** zusätzlicher Code erforderlich. Der Connector unterstützt die folgenden Funktionen:

- Authentifizierte Datenerfassung
- Nachrichten-Batches, um Netzwerkaufrufe zu reduzieren und den Durchsatz zu erhöhen

Weitere Informationen zum [!DNL Kafka]-Connector, einschließlich Anweisungen zum Einrichten des Connectors, finden Sie in der Anleitung [Erste Schritte](https://github.com/adobe/experience-platform-streaming-connect) . Einen detaillierteren Workflow finden Sie im [Entwicklerhandbuch](https://www.adobe.com/go/kafka-connector-developer-guide).
