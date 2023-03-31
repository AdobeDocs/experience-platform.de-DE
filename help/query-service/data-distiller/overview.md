---
title: Data Distiller - Übersicht
description: Eine Zusammenfassung der Data Distiller-Nutzungsbeschränkungen für Query Service-Daten im Zusammenhang mit Ihrer Lizenzberechtigung.
source-git-commit: c7e753e54f087ee45daabb9094edeb51e54271fc
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 1%

---

# Data Distiller - Übersicht

Data Distiller ist ein Package, das eine Untergruppe der Funktionen von Adobe Experience Platform enthält. Mit Data Distiller können Sie nach der Erfassung Datenvorbereitung (z. B. Reinigung, Formatierung und Bearbeitung) für Echtzeit-Kundenprofile oder Analytics-Anwendungsfälle durchführen, indem Sie in Query Service Batch-Abfragen ausführen. Ihre Verwendung von Data Distiller hängt von Ihrer Berechtigung für plattformbasierte Anwendungen ab.

## Lizenznutzung {#license-usage}

Die [Datennutzungs-Dashboard für Distiller-Lizenzen](./license-usage.md) ist verfügbar, sobald Sie Data Distiller Compute-Stunden erworben haben. Mit dem Dashboard zur Lizenznutzung können Sie den Verbrauch berechtigter Berechnungsstunden überwachen. Siehe [Nutzungsdokument zur Distiller-Lizenz](./license-usage.md) , um wichtige Informationen zur Nutzung der Query Service-Lizenz Ihres Unternehmens anzuzeigen.

<!-- Update these descriptions post 23.3 release
## Scoping parameters {#scoping-parameters}

Scoping parameters are usage limits that relate to the scoping of your required set up, and are defined by your license capacity. Without add-ons, Data Distiller's scoping parameters are as follows: 

* **Compute Hours**: You can use PSQL or the Query Service API to run batch queries executed in any sandbox (scheduled or otherwise) to scan and write data. This uses your allotted Compute Hours per year as determined in the scoping process of your license agreement. Total Compute Hours is accumulated across all Sandboxes.
* **Data Ingested**: The data ingested into Adobe Experience Platform which can be queried using Data Distiller is subject to the limitations described in your then-current license to Adobe Real-Time Customer Data Platform, Customer Journey Analytics, and/or Adobe Journey Optimizer.
* **Data Lake Storage**: The data lake storage provided in your then-current license to Adobe Real-Time Customer Data Platform, Customer Journey Analytics, and/or Adobe Journey Optimizer may also be used with Data Distiller. Data Lake Storage is a shared feature.
* **Query Service Users**: The number of Query Service users detailed in your then-current license to Adobe Real-Time Customer Data Platform, Customer Journey Analytics, and/or Adobe Journey Optimizer may also be used with Data Distiller. Query Service Users is a shared feature. 
-->

## Leitplanken

Siehe [Limits für Query Service](../guardrails.md) Dokument zu Standardbeschränkungen für Query Service-Daten in Bezug auf Ihre Lizenzberechtigung.

<!-- Update these descriptions post 23.3 release
## Static limits

A static limit is the usage limit that relates to the functional boundaries of Adobe Experience Platform Activation. [More information on Adobe Experience Platform Activation](https://helpx.adobe.com/ca/legal/product-descriptions/adobe-experience-platform0.html) can be found in the Adobe help documents. A summary of Data Distiller static limits are listed below, for more complete information please refer to the Query Service guardrail document.  

* **Batch Queries**: Scheduled batch queries time out after 24 hours.
* **Query Service**: You can use Query Service for the following purposes: 
    * To run SQL queries for data analysis and post ingestion data preparation (cleaning, shaping, and manipulation).
    * To run SQL queries to create roll-up metrics to surface directly into a BI tool.
    * To quickly inspect data within Adobe Experience Platform.
    * To generate meaningful insights from your data.
* **Reporting API Call**: To ensure queries run on aggregated data using the reporting API have enough resources to execute efficiently. This includes queries that enhance existing data models such as those provided by Real-Time Customer Data Platform. The reporting API tracks resource utilization by assigning concurrency slots to each query. A maximum of four reporting API calls are available concurrently. If you access the reporting API through a BI tool and require more concurrency slots, a BI server is required.
-->

