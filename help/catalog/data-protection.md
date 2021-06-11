---
keywords: Experience Platform;Home;beliebte Themen;Katalog;Datenschutz;Verschlüsselungsdatensee
solution: Experience Platform
title: Datenschutz in Adobe Experience Platform
topic-legacy: data protection
description: Alle im Data Lake persistierten Daten werden in einem für Ihre Organisation eindeutigen, isolierten Microsoft Azure Data Lake Storage-Konto verschlüsselt, gespeichert und verwaltet. Das folgende Prozessflussdiagramm veranschaulicht, wie Daten von Experience Platform erfasst, verarbeitet, verschlüsselt und persistiert werden.
exl-id: 184b2b2d-8cd7-4299-83f8-f992f585c336
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: ht
source-wordcount: '187'
ht-degree: 100%

---

# Datenschutz in Adobe Experience Platform

Alle Daten, die von Adobe Experience Platform aufgenommen und verwendet werden, werden im [!DNL Data Lake] gespeichert, einem hochgradig granularen Datenspeicher, der unabhängig von Herkunft oder Dateiformat alle von [!DNL Platform] verwalteten Daten enthält. Alle im [!DNL Data Lake] gespeicherten Daten werden in einem für Ihre Organisation eindeutigen, isolierten Datenspeicherungskonto von [!DNL Microsoft Azure Data Lake] verschlüsselt, gespeichert und verwaltet.

Das folgende Prozessflussdiagramm veranschaulicht, wie Daten von [!DNL Experience Platform] aufgenommen, verarbeitet, verschlüsselt und gespeichert werden:

![](images/data-protection/flow.png)

Einzelheiten dazu, wie Data-at-Rest im [!DNL Data Lake Storage] verschlüsselt werden, finden Sie im Dokument zur [Datenverschlüsselung in der Azure Data Lake-Datenspeicherung](https://docs.microsoft.com/de-de/azure/data-lake-store/data-lake-store-encryption). Informationen dazu, wie Data-at-Rest in [!DNL Cosmos DB] verschlüsselt werden, finden Sie im Dokument zur [Datenverschlüsselung in Azure Cosmos DB](https://docs.microsoft.com/de-de/azure/cosmos-db/database-encryption-at-rest).
