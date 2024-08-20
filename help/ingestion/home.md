---
keywords: Experience Platform;Startseite;beliebte Themen;Datenaufnahme;Datenspeicherort;Datenspeicherort;Daten-Management;Daten-Management;Abstammung;Abstammung;Batch;Batch;erfasste Daten
solution: Experience Platform
title: Datenerfassung – Übersicht
description: In diesem Dokument werden die drei Hauptwege für die Datenaufnahme in Platform vorgestellt, mit Links zu den jeweiligen Übersichtsdokumenten, in denen Sie weitere Informationen finden.
exl-id: c189dd4a-5c59-4189-a18c-a3e45a9ff01d
source-git-commit: 15de9351203f6b43653042ab73ede17781486160
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 66%

---

# Datenerfassung – Übersicht

Adobe Experience Platform bringt Daten aus mehreren Quellen zusammen, um Marketern ein besseres Verständnis des Verhaltens ihrer Kunden zu ermöglichen. Adobe Experience Platform Data Ingestion stellt die verschiedenen Methoden dar, mit denen Experience Platform Daten aus diesen Quellen erfasst, sowie die Art und Weise, wie diese Daten im Data Lake zur Verwendung durch nachgelagerte Experience Platform-Dienste persistiert werden.

In diesem Dokument werden die drei Hauptarten für die Aufnahme von Daten in Experience Platform vorgestellt, mit Links zu den jeweiligen Übersichtsdokumenten für detailliertere Informationen.

## Batch-Erfassung

Die Batch-Aufnahme erlaubt Ihnen das Erfassen von Daten in [!DNL Experience Platform] in Form von Batch-Dateien. Batches sind Dateneinheiten aus einer oder mehreren Dateien, die als Ganzes aufgenommen werden. Nach der Erfassung stellen Batches Metadaten bereit, die die Anzahl der erfolgreich erfassten Datensätze sowie alle fehlgeschlagenen Datensätze und zugehörigen Fehlermeldungen beschreiben.

Manuell hochgeladene Datendateien wie CSV-Flatfiles (die XDM-Schemata zugeordnet sind) und Parquet-Daten-Frames müssen mit dieser Methode erfasst werden.

Weitere Informationen finden Sie in der [Übersicht zur Batch-Aufnahme](./batch-ingestion/overview.md).

>[!TIP]
>
>Verwenden Sie einzeilige JSON anstelle mehrzeiliger JSON als Eingabe für die Batch-Erfassung. Eine einzeilige JSON-Datei ermöglicht eine bessere Leistung, da das System eine Eingabedatei in mehrere Blöcke unterteilen und sie parallel verarbeiten kann, während mehrzeilige JSON-Dateien nicht aufgeteilt werden können. Dies kann die Datenverarbeitungskosten erheblich senken und die Latenz bei der Batch-Verarbeitung verbessern.

## Streaming-Erfassung

Mit der Streaming-Aufnahme können Sie Daten von Client- und Server-seitigen Geräten in Echtzeit an [!DNL Experience Platform] senden. Experience Platform unterstützt die Verwendung von Daten-Inlets zum Streamen eingehender Erlebnisdaten, die in Streaming-fähigen Datensätzen im Data Lake persistiert werden. Daten-Inlets können so konfiguriert werden, dass die von ihnen erfassten Daten automatisch authentifiziert werden, sodass sichergestellt ist, dass die Daten von einer vertrauenswürdigen Quelle stammen.

Weiterführende Informationen dazu finden Sie in unter [Streaming-Aufnahme – Übersicht](./streaming-ingestion/overview.md).

## Quellen

[!DNL Experience Platform] ermöglicht es Ihnen, Quellverbindungen zu verschiedenen Datenanbietern einzurichten. Mit diesen Verbindungen können Sie sich bei Ihren externen Datenquellen authentifizieren, Zeiten für die Aufnahme festlegen und den Aufnahmedurchsatz verwalten.

Quellverbindungen können so konfiguriert sein, dass Daten aus anderen Adobe-Programmen (beispielsweise Adobe Analytics und Adobe Audience Manager), Cloud-Speichern von Drittanbietern (beispielsweise [!DNL Azure Blob], [!DNL Amazon] S3, FTP-Server und SFTP-Server) und Drittanbieter-CRM-Systemen (beispielsweise [!DNL Microsoft Dynamics] und [!DNL Salesforce]) erfasst werden.

Weiterführende Informationen dazu finden Sie in der [Übersicht zu Quellen](../sources/home.md).

### ML-gestützte Schemaerstellung {#ml-assisted-schema-creation}

Um neue Datenquellen schnell zu integrieren, können Sie jetzt maschinelle Lernalgorithmen verwenden, um ein Schema aus Beispieldaten zu generieren. Diese Automatisierung vereinfacht die Erstellung genauer Schemata, reduziert Fehler und beschleunigt den Prozess von der Datenerfassung über Analysen und Einblicke.

Weitere Informationen zu diesem Workflow finden Sie im Handbuch zur Erstellung von [ML-unterstützten Schemas](../xdm/ui/ml-assisted-schema-creation.md) .

## Nächste Schritte und zusätzliche Ressourcen

Dieses Dokument bietet eine kurze Einführung in die verschiedenen Aspekte von [!DNL Data Ingestion] in [!DNL Experience Platform]. Bitte lesen Sie darüber hinaus die Übersichtsdokumentation für jede Aufnahmemethode, um sich mit deren verschiedenen Funktionen, Anwendungsfällen und Best Practices vertraut zu machen. Sie können sich als Ergänzung zum Lernen auch das nachfolgende Video zur Aufnahme ansehen. Weitere Informationen dazu, wie [!DNL Experience Platform] die Metadaten nach erfassten Datensätzen verfolgt, finden Sie unter [Übersicht über den Katalog-Service](../catalog/home.md).

>[!WARNING]
>
>Der Begriff „Unified Profile“, der im folgenden Video verwendet wird, ist veraltet. Die Begriffe [!DNL "Profile"] oder [!DNL "Real-Time Customer Profile"] sind die korrekten Begriffe, die in der [!DNL Experience Platform]-Dokumentation verwendet werden. Die neuesten Funktionen finden Sie in der Dokumentation.

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)
