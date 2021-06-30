---
keywords: Experience Platform; Startseite; beliebte Themen; Azure synapse Analytics; azure synapse-Analyse; Synapse; Synapse
solution: Experience Platform
title: azure synapse Analytics Source Connector - Überblick
topic-legacy: overview
description: Erfahren Sie, wie Sie Azure synapse Analytics mit Adobe Experience Platform über APIs oder die Benutzeroberfläche verbinden.
exl-id: 5b94ae74-e5a7-40e9-a952-41eddf06dcde
source-git-commit: 5821f9304a37c1a03d17f0113d09548799662a2e
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 9%

---

# [!DNL Azure Synapse Analytics] Connector

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von [!DNL Platform]-Diensten zu strukturieren, zu beschriften und zu erweitern. Daten können aus verschiedensten Quellen erfasst werden, darunter etwa Adobe-Anwendungen, Cloud-basierte Datenspeicher und Datenbanken.

[!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus Datenbanken von Drittanbietern. [!DNL Platform] kann eine Verbindung zu verschiedenen Arten von Datenbanken wie z. B. relationalen, NoSQL- oder Data Warehouse-Datenbanken herstellen. Unterstützung für Datenbankanbieter: [!DNL Azure Synapse Analytics].

## IP-Adressen-Zulassungsliste

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Leistungseinbußen führen. Weitere Informationen finden Sie auf der Seite [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md) .

>[!IMPORTANT]
>
>Der Quell-Connector [!DNL Azure Synapse Analytics] unterstützt derzeit keine Verbindung zwischen denselben Regionen und Platform. Wenn Ihre Azure-Instanz also denselben Netzwerkbereich wie Platform verwendet, kann keine Verbindung zu Platform-Quellen hergestellt werden. Derzeit wird nur eine regionenübergreifende Konnektivität unterstützt. Weitere Informationen erhalten Sie von Ihrem Kundenbetreuer für Adoben.

Die folgende Dokumentation enthält Informationen dazu, wie Sie mithilfe von APIs oder der Benutzeroberfläche eine Verbindung zwischen [!DNL Azure Synapse Analytics] und [!DNL Platform] herstellen:

## Verbinden Sie [!DNL Azure Synapse Analytics] mit [!DNL Platform] mithilfe von APIs

- [Erstellen einer Basisverbindung für Azure synapse Analytics mithilfe der Flow Service-API](../../tutorials/api/create/databases/synapse-analytics.md)
- [Datenstruktur und Inhalt einer Datenbankquelle mithilfe der Flow Service-API durchsuchen](../../tutorials/api/explore/database-nosql.md)
- [Erstellen eines Datenflusses für eine Datenbankquelle mithilfe der Flow Service-API](../../tutorials/api/collect/database-nosql.md)

## Verbinden Sie [!DNL Azure Synapse Analytics] mit [!DNL Platform] über die Benutzeroberfläche

- [Erstellen einer Azure synapse Analytics-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/create/databases/synapse-analytics.md)
- [Erstellen eines Datenflusses für eine Datenbankquellenverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/databases.md)
