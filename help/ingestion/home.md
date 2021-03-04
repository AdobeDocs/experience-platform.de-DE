---
keywords: Experience Platform;Startseite;beliebte Themen;Datenerfassung;Datenposition;Datenposition;Data Management;Data Management;Lineage;Linie;Batch;Stapel;Ingetierte Daten
solution: Experience Platform
title: Übersicht über die Dateneinbindung
topic: Übersicht
description: In diesem Dokument werden die drei Hauptwege für die Dateneinbindung in die Plattform vorgestellt, mit Links zu den jeweiligen Übersichtsdokumenten für weitere Informationen.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 16%

---


# Datenerfassung – Übersicht

Adobe Experience Platform bringt Daten aus mehreren Quellen zusammen, um Marketern ein besseres Verständnis des Verhaltens ihrer Kunden zu ermöglichen. Adobe Experience Platform Data Ingestion stellt die verschiedenen Methoden dar, mit denen [!DNL Platform] Daten aus diesen Quellen erfasst und wie diese Daten im Data Lake für die Verwendung durch nachgelagerte [!DNL Platform]-Dienste beibehalten werden.

In diesem Dokument werden die drei Hauptwege für die Erfassung von Daten in [!DNL Platform] mit Links zu den jeweiligen Übersichtsdokumenten vorgestellt.

## Batch-Erfassung

Mit der Stapelverarbeitung können Sie Daten als Stapeldateien in [!DNL Experience Platform] erfassen. Batches sind Dateneinheiten aus einer oder mehreren Dateien, die als Ganzes aufgenommen werden. Nach der Erfassung stellen Batches Metadaten bereit, die die Anzahl der erfolgreich erfassten Datensätze sowie alle fehlgeschlagenen Datensätze und zugehörigen Fehlermeldungen beschreiben.

Manuell hochgeladene Datendateien wie flache CSV-Dateien (XDM-Schemas zugeordnet) und Parquet-Datenbilder müssen mit dieser Methode erfasst werden.

Weitere Informationen finden Sie unter [Überblick über die Stapelverarbeitung](./batch-ingestion/overview.md).

## Streaming-Erfassung

Mit der Streaming-Erfassung können Sie Daten von client- und serverseitigen Geräten in Echtzeit an [!DNL Experience Platform] senden. [!DNL Platform] unterstützt die Verwendung von Dateneinlässen zum Streamen eingehender Erlebnisdaten, die in Streaming-fähigen Datensätzen im Data Lake beibehalten werden. Dateneingänge können so konfiguriert werden, dass die von ihnen erfassten Daten automatisch authentifiziert werden, sodass sichergestellt ist, dass die Daten von einer vertrauenswürdigen Quelle stammen.

Weitere Informationen finden Sie unter [Streaming-Erfassungsübersicht](./streaming-ingestion/overview.md).

## Quellen

[!DNL Experience Platform] ermöglicht es Ihnen, Quellverbindungen zu verschiedenen Datenanbietern einzurichten. Mit diesen Verbindungen können Sie sich bei Ihren externen Datenquellen authentifizieren, Zeiten für die Erfassung festlegen und den Erfassungsdurchsatz verwalten.

Quellverbindungen können so konfiguriert werden, dass Daten aus anderen Anwendungen der Adobe (z. B. Adobe Analytics und Adobe Audience Manager), Cloud-Datenspeicherung von Drittanbietern (z. B. [!DNL Azure Blob], [!DNL Amazon] S3-, FTP- und SFTP-Server) und CRM-Systemen von Drittanbietern (z. B. [!DNL Microsoft Dynamics] und [!DNL Salesforce]) erfasst werden.

Weitere Informationen finden Sie unter [Übersicht über Quellen](../sources/home.md).

## Nächste Schritte und zusätzliche Ressourcen

Dieses Dokument bietet eine kurze Einführung zu den verschiedenen Aspekten von [!DNL Data Ingestion] in [!DNL Experience Platform]. Bitte lesen Sie weiterhin die Übersichtsdokumentation für jede Erfassungsmethode, um sich mit ihren verschiedenen Fähigkeiten, Anwendungsfällen und Best Practices vertraut zu machen. Sie können Ihr Lernen auch ergänzen, indem Sie sich das unten stehende Video zur Erfassung ansehen. Weitere Informationen dazu, wie [!DNL Experience Platform] die Metadaten nach erfassten Datensätzen verfolgt, finden Sie unter [Übersicht über den Katalogdienst](../catalog/home.md).

>[!WARNING]
>
>Der Begriff &quot;Einheitliches Profil&quot;, der im folgenden Video verwendet wird, ist veraltet. Die Begriffe [!DNL "Profile"] oder [!DNL "Real-time Customer Profile"] sind die korrekten Begriffe, die in der [!DNL Experience Platform]-Dokumentation verwendet werden. Die neuesten Funktionen finden Sie in der Dokumentation.

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)