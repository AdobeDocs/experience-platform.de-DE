---
title: Beschleunigte Abfragen senden
description: Eine Einführung in die API für beschleunigte Abfragen.
exl-id: c6cd1182-d3a9-457f-81d5-18027e47c3f9
source-git-commit: 0970fd8fbea86115d92dc78cdba753da69cc2ee6
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 13%

---

# Beschleunigte Abfragen senden

Im Rahmen der Data Distiller SKU ermöglicht Ihnen die [Abfrage-Service-API](https://developer.adobe.com/experience-platform-apis/references/query-service/), statuslose Abfragen an den beschleunigten Speicher zu stellen. Der [Endpunkt für beschleunigte Abfragen](https://developer.adobe.com/experience-platform-apis/references/query-service/#tag/Accelerated-Queries) gibt Ergebnisse zurück, die auf aggregierten Daten basieren, um die Wartezeit auf Ergebnisse zu reduzieren und einen interaktiveren Informationsaustausch zu ermöglichen.

Anweisungen zum Abfragen des [-Speichers finden ](../../api/accelerated-queries.md) in der Dokumentation zum Endpunkt „Beschleunigte Abfragen .

Mit dem abfragebeschleunigten Speicher können Sie ein benutzerdefiniertes Datenmodell erstellen und/oder ein vorhandenes Adobe Real-time Customer Data Platform-Datenmodell erweitern. Informationen zum Interagieren mit oder Einbetten Ihrer Reporting-Insights in ein Reporting-/Visualisierungs-Framework finden Sie im [Handbuch für abfragebeschleunigte Speicher-Reporting-Insights](./reporting-insights-data-model.md). Sie können auch die Dokumentation zum Real-time Customer Data Platform Insights-Datenmodell lesen, um zu erfahren, wie Sie [Ihre SQL-Abfragevorlagen anpassen, um Real-Time CDP-Berichte für Ihre Marketing- und KPI-Anwendungsfälle zu erstellen](../../../dashboards/data-models/cdp-insights-data-model-b2c.md). Sie können die [attributbasierte Zugriffssteuerungsfunktion](../../../access-control/abac/overview.md) verwenden, um den Grad der Einschränkung für Datensätze im beschleunigten Speicher zu steuern. Siehe [Data Governance in Query Service](../../data-governance/overview.md#create-field-based-access-restrictions-on-accelerated-datasets)
Dokument für weitere Informationen.
