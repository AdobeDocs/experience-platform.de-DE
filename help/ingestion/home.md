---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Übersicht über die Dateneinbindung in Adobe Experience Platformen
topic: overview
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 18%

---


# Datenaufnahme – Übersicht

Adobe Experience Platform bringt Daten aus mehreren Quellen zusammen, um Marketern ein besseres Verständnis des Verhaltens ihrer Kunden zu ermöglichen. Adobe Experience Platform Data Ingestion represents the multiple methods by which [!DNL Platform] ingests data from these sources, as well as how that data is persisted within the Data Lake for use by downstream [!DNL Platform] services.

In diesem Dokument werden die drei Hauptwege für die Dateneingabe vorgestellt [!DNL Platform], mit Links zu den jeweiligen Übersichtsdokumenten.

## Batch-Aufnahme

Batch ingestion allows you to ingest data into [!DNL Experience Platform] as batch files. Batches sind Dateneinheiten aus einer oder mehreren Dateien, die als Ganzes aufgenommen werden. Nach der Erfassung stellen Batches Metadaten bereit, die die Anzahl der erfolgreich erfassten Datensätze sowie alle fehlgeschlagenen Datensätze und zugehörigen Fehlermeldungen beschreiben.

Manuell hochgeladene Datendateien wie flache CSV-Dateien (XDM-Schemas zugeordnet) und Parquet-Datenbilder müssen mit dieser Methode erfasst werden.

See the [batch ingestion overview](./batch-ingestion/overview.md) for more information.

## Streaming-Aufnahme

Streaming ingestion allows you to send data from client- and server-side devices to [!DNL Experience Platform] in real-time. [!DNL Platform] unterstützt die Verwendung von Dateneinlässen zum Streamen eingehender Erlebnisdaten, die in Streaming-fähigen Datensätzen im Data Lake beibehalten werden. Dateneingänge können so konfiguriert werden, dass die von ihnen erfassten Daten automatisch authentifiziert werden, sodass sichergestellt ist, dass die Daten von einer vertrauenswürdigen Quelle stammen.

See the [streaming ingestion overview](./streaming-ingestion/overview.md) for more information.

## Quellen

[!DNL Experience Platform] ermöglicht es Ihnen, Quellverbindungen zu verschiedenen Datenanbietern einzurichten. Mit diesen Verbindungen können Sie sich bei Ihren externen Datenquellen authentifizieren, Zeiten für die Erfassung festlegen und den Erfassungsdurchsatz verwalten.

Source connections can be configured to gather data from other Adobe applications (such as Adobe Analytics and Adobe Audience Manager), third-party cloud storage sources (such as [!DNL Azure Blob], [!DNL Amazon] S3, FTP servers, and SFTP servers), and third-party CRM systems (such as [!DNL Microsoft Dynamics] and [!DNL Salesforce]).

See the [Sources overview](../sources/home.md) for more information.

## Nächste Schritte und zusätzliche Ressourcen

Dieses Dokument gab eine kurze Einführung zu den verschiedenen Aspekten von [!DNL Data Ingestion] in [!DNL Experience Platform]. Bitte lesen Sie weiterhin die Übersichtsdokumentation für jede Erfassungsmethode, um sich mit ihren verschiedenen Fähigkeiten, Anwendungsfällen und Best Practices vertraut zu machen. Sie können Ihre Lernerfahrung auch über das unten stehende Video zur Erfassung von Übersichten ergänzen. Weitere Informationen zum [!DNL Experience Platform] Verfolgen der Metadaten für erfasste Datensätze finden Sie in der Übersicht über den [Katalogdienst](../catalog/home.md).

>[!WARNING]
>
> Der Begriff &quot;Einheitliches Profil&quot;, der im folgenden Video verwendet wird, ist veraltet. Die Begriffe [!DNL "Profile"] oder [!DNL "Real-time Customer Profile"] sind die richtigen Begriffe, die in der [!DNL Experience Platform] Dokumentation verwendet werden. Die neuesten Funktionen finden Sie in der Dokumentation.

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)