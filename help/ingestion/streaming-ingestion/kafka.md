---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Kafka-Anschluss
topic: overview
translation-type: tm+mt
source-git-commit: f80b2e1d787d1f8d9fe8ac306422aa7744a69cd3
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---


# Kafka Connector for Adobe Experience Platform

Der Stream-Connector für Adobe Experience Platform basiert auf Apache Kafka Connect. Diese Bibliothek kann verwendet werden, um JSON-Ereignis von Kafka-Themen in Ihrem Rechenzentrum direkt an Experience Platform in Echtzeit zu streamen.

Der Stream-Connector ist ein Einwegstecker, der Daten von Kafka-Themen an einen registrierten Endpunkt auf Experience Platform liefert. Um diesen Connector zu verwenden, müssen Sie die Bibliothek herunterladen, sie zu Ihrer vorhandenen Kafka-Bereitstellung hinzufügen und die Kafka-Themen zur Adobe Streaming-HTTP-URL konfigurieren. Zusätzlicher Code ist **nicht** erforderlich. Der Connector unterstützt die folgenden Funktionen:

- Authentifizierte Datenerfassung
- Batch-Nachrichten, um Netzwerkaufrufe zu reduzieren und den Durchsatz zu erhöhen

Weitere Informationen zum Kafka-Anschluss, einschließlich Anweisungen zum Einrichten des Connectors, finden Sie im Handbuch [Erste Schritte](https://github.com/adobe/experience-platform-streaming-connect). Für einen detaillierteren Arbeitsablauf lesen Sie bitte das [Entwicklerhandbuch](https://github.com/adobe/experience-platform-streaming-connect/blob/master/DEVELOPER_GUIDE.md).