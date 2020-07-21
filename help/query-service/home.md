---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Abfrage-Service
topic: overview
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 25%

---


# [!DNL Query Service]Übersicht

Adobe Experience Platform nimmt Daten aus einer Vielzahl von Quellen auf. Eine große Herausforderung für Marketing-Experten besteht darin, diese Daten zu nutzen, um Einblicke in ihre Kunden zu gewinnen. Adobe Experience Platform [!DNL Query Service] facilitates that by allowing you to use standard SQL to query data in [!DNL Platform]. Using [!DNL Query Service], you can join any dataset in the [!DNL Data Lake] and capture the query results as a new dataset for use in reporting, machine learning, or for ingestion into [!DNL Real-time Customer Profile]. This document provides an overview of the role of [!DNL Query Service] within [!DNL Experience Platform].

[!DNL Query Service] ermöglicht es Marken, die Online- und Offline-Customer Journey miteinander zu verbinden und die Zuordnung von Kanälen zu verstehen. Das folgende Video zeigt, wie ein Erlebnisunternehmen wichtige Anwendungsfälle nutzen kann [!DNL Query Service] und wie [!DNL Query Service] dies funktioniert.

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## Verwenden [!DNL Query Service]

[!DNL Query Service] bietet eine Benutzeroberfläche und eine RESTful-API, mit der Sie SQL-Abfragen erstellen können, um Ihre Daten besser zu analysieren. Über die Benutzeroberfläche können Sie Abfragen schreiben und ausführen, zuvor ausgeführte Abfragen anzeigen und auf Abfragen zugreifen, die von Benutzern in Ihrer IMS-Organisation gespeichert wurden. Die Benutzeroberfläche soll als Sandbox zum Testen Ihrer Abfragen verwendet werden, bevor Sie sie auf Ihren größeren Datensatz anwenden. More information on using the interactive service within [!DNL Platform] can be found in the [Query Service user interface guide](ui/overview.md). Die RESTful-API bietet ein ähnliches Erlebnis, mit dem Sie programmatisch Abfragen schreiben und ausführen, Abfragen für die spätere Verwendung und Wiederholung planen und Vorlagen für Abfragen erstellen können, die Sie schreiben möchten. More information on using the [!DNL Query Service] API can be found in the [Query Service developer guide](api/getting-started.md).

## [!DNL Query Service] und [!DNL Experience Platform] Dienstleistungen

[!DNL Query Service] interagiert und kann in Verbindung mit mehreren [!DNL Experience Platform] Diensten verwendet werden. In order to make the most out of [!DNL Query Service's] capabilities, it is recommended that you become familiar with these services and how they interact with [!DNL Query Service].

### [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace] uses machine learning and artificial intelligence to gain insights from data stored within [!DNL Experience Platform]. [!DNL Data Science Workspace] ermöglicht es Datenwissenschaftlern, Rezepte zu erstellen, die auf Daten zu Kunden und deren Aktivitäten aus Aufzeichnungen und Zeitreihen basieren. Dies erleichtert Prognosen z. B. zu Kaufneigung und empfohlenen Angeboten, die von Einzelpersonen geschätzt und verwendet werden. You can use SQL within [!DNL Data Science Workspace] by integrating [!DNL Query Service] into [!DNL JupyterLab], allowing you to explore, transform, and analyze Adobe Analytics data. Weitere Informationen finden Sie in der [!DNL Data Science Workspace] Übersicht [!DNL Data Science Workspace]und im [!DNL Query Service] Integrationsleitfaden für weitere Informationen zur [!DNL Data Science Workspace] Interaktion [!DNL Query Service].

### [!DNL Segmentation Service]

Adobe Experience Platform [!DNL Segmentation Service] allows users to divide their customers into smaller groups that share similar traits. These segments can subsequently be evaluated to provide better analysis on your [!DNL Real-time Customer Profile] data. [!DNL Query Service] kann verwendet werden, um diese Analyse bereitzustellen, indem Abfragen für diese Segmentdaten in der [!DNL Data Lake]ausgeführt werden. Please read the [!DNL Segmentation Service] overview for more information about segmentation, and the [!DNL Profile Query Language] (PQL) guide for more information on how to analyze segments.

### Looker BI-Anwendungsfall

Mit Adobe Experience Platform können Sie alle gespeicherten Datensätze erfassen, speichern, strukturieren und abrufen — einschließlich Verhaltensdaten, CRM-Daten und Verkaufsdaten. Mithilfe [!DNL Experience Platform's Query Service]dieser Daten können Sie Abfragen zu diesen Datensätzen durchführen und spezifische Fragen zum Geschäft beantworten und dann Beginn zu wirkungsvollen Einblicken führen. Das folgende Video zeigt, wie wichtig es ist, mithilfe von BI-Tools (Business Intelligence) Dashboard zu erstellen [!DNL Query Service].

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## Nächste Schritte und zusätzliche Ressourcen

By reading this document, you have been introduced to [!DNL Query Service] and how it functions within the greater scope of [!DNL Experience Platform]. For more information on interacting with various endpoints within the [!DNL Query Service] API, please read the [Query Service developer guide](api/getting-started.md). For more information on using the interactive service within [!DNL Platform], please read the [Query Service user interface guide](ui/overview.md). For a comprehensive list on connecting external clients with [!DNL Query Service], please read the [Query Service clients overview](clients/overview.md).

Sehen Sie sich das folgende Video an, um sich besser darauf vorzubereiten, Abfragen auszuführen. In diesem Video werden Tipps und Best Practices für die Ausführung von Abfragen in der Benutzeroberfläche des Abfrage-Editors, PSQL-Clients, Business Intelligence-Lösungen (BI) und der HTTP-API vorgestellt.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
