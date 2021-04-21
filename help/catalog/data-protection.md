---
keywords: Experience Platform;Home;beliebte Themen;Katalog;Datenschutz;Verschlüsselungsdatensee
solution: Experience Platform
title: Datenschutz in Adobe Experience Platform
topic-legacy: data protection
description: Alle im Data Lake persistierten Daten werden in einem für Ihre Organisation eindeutigen, isolierten Microsoft Azure Data Lake Storage-Konto verschlüsselt, gespeichert und verwaltet. Das folgende Prozessflussdiagramm veranschaulicht, wie Daten von Experience Platform erfasst, verarbeitet, verschlüsselt und persistiert werden.
exl-id: 184b2b2d-8cd7-4299-83f8-f992f585c336
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 33%

---

# Datenschutz in Adobe Experience Platform

Alle von Adobe Experience Platform erfassten und verwendeten Daten werden im hochgradig granularen Datenspeicher [!DNL Data Lake] gespeichert, der alle von [!DNL Platform] verwalteten Daten enthält, unabhängig von der Herkunft oder dem Dateiformat. Alle Daten, die im [!DNL Data Lake] beibehalten werden, werden verschlüsselt, gespeichert und in einem isolierten [!DNL Microsoft Azure Data Lake]-Konto verwaltet, das für Ihr Unternehmen eindeutig ist.

Das folgende Prozessflussdiagramm veranschaulicht, wie Daten von [!DNL Experience Platform] erfasst, verarbeitet, verschlüsselt und beständig werden:

![](images/data-protection/flow.png)

Weitere Informationen dazu, wie Daten im Ruhezustand in [!DNL Data Lake Storage] verschlüsselt werden, finden Sie im Dokument zur [Datenverschlüsselung in der Datenspeicherung des Azurblauen Datensees](https://docs.microsoft.com/de-de/azure/data-lake-store/data-lake-store-encryption). Informationen dazu, wie Daten im Ruhezustand in [!DNL Cosmos DB] verschlüsselt werden, finden Sie im Dokument zur [Datenverschlüsselung in Azurblauer Kosmos DB](https://docs.microsoft.com/de-de/azure/cosmos-db/database-encryption-at-rest).
