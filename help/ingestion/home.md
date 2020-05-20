---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Übersicht über die Dateneinbindung in der Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 2f0f155beacbc6a4ba2892ae211a9c0305e969ac
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---


# Dateneinbindung - Übersicht

Die Adobe Experience Platform bringt Daten aus mehreren Quellen zusammen, um Marketingexperten ein besseres Verständnis des Verhaltens ihrer Kunden zu ermöglichen. Adobe Experience Platform Data Ingestion stellt die verschiedenen Methoden dar, mit denen Plattform Daten aus diesen Quellen zusammenfasst, sowie die Art und Weise, wie diese Daten im Data Lake für die Verwendung durch nachgelagerte Plattformdienste beibehalten werden.

In diesem Dokument werden die drei Hauptwege für die Dateneinbindung in die Plattform vorgestellt, mit Links zu den jeweiligen Übersichtsdokumenten für weitere Informationen.

## Stapelverarbeitung

Mit der Stapelverarbeitung können Sie Daten als Stapeldateien in Experience Platform erfassen. Stapel sind Dateneinheiten, die aus einer oder mehreren Dateien bestehen, die als eine Einheit erfasst werden sollen. Nach der Erfassung stellen Stapel Metadaten bereit, die die Anzahl der erfolgreich erfassten Datensätze sowie alle fehlgeschlagenen Datensätze und zugehörigen Fehlermeldungen beschreiben.

Manuell hochgeladene Datendateien wie flache CSV-Dateien (XDM-Schemas zugeordnet) und Parquet-Datenbilder müssen mit dieser Methode erfasst werden.

See the [batch ingestion overview](./batch-ingestion/overview.md) for more information.

## Streaming-Erfassung

Mit der Streaming-Erfassung können Sie Daten von client- und serverseitigen Geräten in Echtzeit an Experience Platform senden. Plattform unterstützt die Verwendung von Dateneinlässen zum Streamen eingehender Erlebnisdaten, die in Streaming-fähigen Datensätzen im Data Lake beibehalten werden. Dateneingänge können so konfiguriert werden, dass die von ihnen erfassten Daten automatisch authentifiziert werden, sodass sichergestellt ist, dass die Daten von einer vertrauenswürdigen Quelle stammen.

See the [streaming ingestion overview](./streaming-ingestion/overview.md) for more information.

## Quellen

Mit Experience Platform können Sie Quellverbindungen zu verschiedenen Datenanbietern einrichten. Mit diesen Verbindungen können Sie sich bei Ihren externen Datenquellen authentifizieren, Zeiten für die Erfassung festlegen und den Erfassungsdurchsatz verwalten.

Quellverbindungen können so konfiguriert werden, dass Daten aus anderen Adobe-Anwendungen (z. B. Adobe Analytics und Adobe Audience Manager), Cloud-Datenspeicherung-Quellen von Drittanbietern (z. B. Azurblase, Amazon S3, FTP-Server und SFTP-Server) und CRM- von Drittanbietern (z. B. Microsoft Dynamics und Salesforce) erfasst werden.

See the [Sources overview](../sources/home.md) for more information.

## Nächste Schritte

In diesem Dokument erhalten Sie eine kurze Einführung zu den verschiedenen Aspekten der Dateneinbettung in der Experience Platform. Bitte lesen Sie weiterhin die Übersichtsdokumentation für jede Erfassungsmethode, um sich mit ihren verschiedenen Fähigkeiten, Anwendungsfällen und Best Practices vertraut zu machen. Weitere Informationen dazu, wie Experience Platform die Metadaten für erfasste Datensätze verfolgt, finden Sie in der Übersicht über den [Katalogdienst](../catalog/home.md).