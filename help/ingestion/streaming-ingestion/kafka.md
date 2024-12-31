---
keywords: Experience Platform;Startseite;beliebte Themen;kafka;kafka connector;kafka;
solution: Experience Platform
title: Kafka-Connector
description: Der Stream-Connector für Adobe Experience Platform basiert auf Apache Kafka Connect. Diese Bibliothek kann verwendet werden, um JSON-Ereignisse aus Kafka-Themen in Ihrem Rechenzentrum direkt in Echtzeit auf Experience Platform zu streamen.
exl-id: 062963e5-c727-4c2c-97db-8a9a5a7d903c
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 26%

---

# [!DNL Kafka] Connector für Adobe Experience Platform

Der Stream-Connector für Adobe Experience Platform basiert auf [!DNL Apache Kafka Connect]. Diese Bibliothek kann verwendet werden, um JSON-Ereignisse aus [!DNL Kafka] Themen in Ihrem Rechenzentrum direkt in Echtzeit zu [!DNL Experience Platform].

Der Stream-Connector ist ein Sink-Connector (unidirektional), der Daten aus [!DNL Kafka] Themen an einen registrierten Endpunkt in [!DNL Experience Platform] übermittelt. Um diesen Connector zu verwenden, müssen Sie die Bibliothek herunterladen, sie zu Ihrer vorhandenen [!DNL Kafka]-Bereitstellung hinzufügen und das/die [!DNL Kafka] Thema(e) zur Adobe-Streaming-HTTP-URL konfigurieren. Es ist **kein** zusätzlicher Code erforderlich. Der Connector unterstützt die folgenden Funktionen:

- Authentifizierte Datenerfassung
- Nachrichten-Batches, um Netzwerkaufrufe zu reduzieren und den Durchsatz zu erhöhen

Weitere Informationen zum [!DNL Kafka]-Connector, einschließlich Anweisungen zum Einrichten des Connectors, finden Sie im Abschnitt [Erste Schritte](https://github.com/adobe/experience-platform-streaming-connect). Einen detaillierteren Workflow finden Sie im [Entwicklerhandbuch](https://www.adobe.com/go/kafka-connector-developer-guide).
