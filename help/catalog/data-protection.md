---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Datenschutz in Adobe Experience Platform
topic: data protection
translation-type: tm+mt
source-git-commit: edf7cef0991ceef0465d5c1d750bd1885754f716
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---


# Datenschutz in Adobe Experience Platform

Alle Daten, die von Adobe Experience Platform erfasst und verwendet werden, werden im Data Lake gespeichert, einem hochgradig granularen Datenspeicher, der alle von Platform verwalteten Daten enthält, unabhängig von der Herkunft oder dem Dateiformat. Alle im Data Lake gespeicherten Daten werden verschlüsselt, gespeichert und in einem für Ihr Unternehmen einzigartigen, isolierten Microsoft Azurblase Data Lake Datenspeicherung-Konto verwaltet.

Das folgende Prozessflussdiagramm veranschaulicht, wie Daten von Experience Platform erfasst, verarbeitet, verschlüsselt und dauerhaft gespeichert werden:

![](images/data-protection/flow.png)

Einzelheiten dazu, wie Daten in der Datenspeicherung von Data Lake verschlüsselt werden, finden Sie im Dokument zur [Datenverschlüsselung in der Datenspeicherung](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption)der Azurblauen Data Lake. Informationen darüber, wie Daten im Ruhezustand in Cosmos DB verschlüsselt werden, finden Sie im Dokument zur [Datenverschlüsselung in der Azurblauen Kosmos DB](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest).