---
keywords: Experience Platform; Startseite; beliebte Themen; Kafka; Kafka-Connector; Kafka;
solution: Experience Platform
title: Kafka Connector
description: Der Stream-Connector für Adobe Experience Platform basiert auf Apache Kafka Connect. Mit dieser Bibliothek können Sie JSON-Ereignisse von Kafka-Themen in Ihrem Rechenzentrum direkt an die Experience Platform in Echtzeit streamen.
exl-id: 062963e5-c727-4c2c-97db-8a9a5a7d903c
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 27%

---

# [!DNL Kafka] Connector für Adobe Experience Platform

Der Stream-Connector für Adobe Experience Platform basiert auf [!DNL Apache Kafka Connect]. Diese Bibliothek kann zum Streamen von JSON-Ereignissen aus verwendet werden. [!DNL Kafka] Themen in Ihrem Rechenzentrum direkt zu [!DNL Experience Platform] in Echtzeit.

Der Stream-Connector ist ein Einweg-Connector, der Daten aus dem [!DNL Kafka] Themen zu einem registrierten Endpunkt auf [!DNL Experience Platform]. Um diesen Connector zu verwenden, müssen Sie die Bibliothek herunterladen und zu Ihrer vorhandenen hinzufügen [!DNL Kafka] Bereitstellung und Konfiguration der [!DNL Kafka] Themen zur Adobe Streaming-HTTP-URL. Es ist **kein** zusätzlicher Code erforderlich. Der Connector unterstützt die folgenden Funktionen:

- Authentifizierte Datenerfassung
- Nachrichten-Batches, um Netzwerkaufrufe zu reduzieren und den Durchsatz zu erhöhen

Weitere Informationen über [!DNL Kafka] Connector, einschließlich Anweisungen zum Einrichten des Connectors, finden Sie im Abschnitt [Erste Schritte](https://github.com/adobe/experience-platform-streaming-connect). Einen detaillierteren Workflow finden Sie im [Entwicklerhandbuch](https://www.adobe.com/go/kafka-connector-developer-guide).
