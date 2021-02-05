---
keywords: Experience Platform;Home;beliebte Themen;Kafka;Kafka-Anschluss;Kafka;
solution: Experience Platform
title: Kafka Connector
topic: overview
description: Der Stream-Connector für Adobe Experience Platform basiert auf Apache Kafka Connect. Mit dieser Bibliothek können Sie JSON-Ereignisse von Kafka-Themen in Ihrem Rechenzentrum in Echtzeit direkt an Experience Platform zu streamen.
translation-type: tm+mt
source-git-commit: 089a4d517476b614521d1db4718966e3ebb13064
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 39%

---


# [!DNL Kafka] Anschluss für Adobe Experience Platform

Der Stream-Connector für Adobe Experience Platform basiert auf [!DNL Apache Kafka Connect]. Diese Bibliothek kann verwendet werden, um JSON-Ereignis von [!DNL Kafka]-Themen in Ihrem Rechenzentrum direkt zu [!DNL Experience Platform] in Echtzeit zu streamen.

Der Stream-Connector ist ein Einweg-Connector, der Daten von [!DNL Kafka]-Themen an einen registrierten Endpunkt unter [!DNL Experience Platform] liefert. Um diesen Connector verwenden zu können, müssen Sie die Bibliothek herunterladen, sie Ihrer vorhandenen [!DNL Kafka]-Bereitstellung hinzufügen und die [!DNL Kafka]-Themen zur Adobe Streaming HTTP-URL konfigurieren. Es ist **kein** zusätzlicher Code erforderlich. Der Connector unterstützt die folgenden Funktionen:

- Authentifizierte Datenerfassung
- Nachrichten-Batches, um Netzwerkaufrufe zu reduzieren und den Durchsatz zu erhöhen

Weitere Informationen zum Anschluss [!DNL Kafka], einschließlich Anweisungen zum Einrichten des Connectors, finden Sie im Handbuch [Erste Schritte](https://github.com/adobe/experience-platform-streaming-connect). Einen detaillierteren Workflow finden Sie im [Entwicklerhandbuch](https://www.adobe.com/go/kafka-connector-developer-guide).