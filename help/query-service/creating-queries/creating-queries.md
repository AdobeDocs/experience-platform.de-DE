---
keywords: Experience Platform;home;popular topics;query service;Query service;create queries;
solution: Experience Platform
title: Erstellen von Abfragen
topic: queries
type: Tutorial
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 17%

---


# Erstellen von Abfragen

Adobe Experience Platform [!DNL Query Service] provides the power to run SQL queries against datasets in the [!DNL Data Lake] within [!DNL Experience Platform]. As you use SQL to interact with datasets in the Data Lake, it is important to understand that [!DNL Query Service] automatically manages certain aspects, such as creating SQL-safe table names for each dataset in the [!DNL Data Lake]. There are also considerations around working with hierarchical data in the [!DNL Data Lake], including discovering the schema upon which a dataset is based and ensuring that you are selecting the correct field within the hierarchical model.

The following documentation will help you to better understand core concepts within [!DNL Query Service]:

- [Datensätze vs. Tabellen und Schema](./datasets-and-tables.md)
- [Allgemeine Leitlinien für das Schreiben von Abfragen](./writing-queries.md)
- [ExperienceEvent-Abfragen](./experience-event-queries.md)
- [Zusammenfügen von Datensätzen](./joining-datasets.md)
- [Deduplizieren von Daten](./deduplication.md)
