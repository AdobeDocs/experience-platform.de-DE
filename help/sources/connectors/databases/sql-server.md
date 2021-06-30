---
keywords: Experience Platform; Startseite; beliebte Themen; Microsoft SQL; Microsoft SQL; Microsoft SQL; SQL
solution: Experience Platform
title: SQL Server Source Connector - Übersicht
topic-legacy: overview
description: Erfahren Sie, wie Sie mithilfe von APIs oder der Benutzeroberfläche Microsoft SQL Server mit Adobe Experience Platform verbinden.
exl-id: 8a77f108-7e82-4e14-a470-a4ea97def89d
source-git-commit: 5821f9304a37c1a03d17f0113d09548799662a2e
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 9%

---

# [!DNL Microsoft] SQL Server-Connector

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von [!DNL Platform]-Diensten zu strukturieren, zu beschriften und zu erweitern. Daten können aus verschiedensten Quellen erfasst werden, darunter etwa Adobe-Anwendungen, Cloud-basierte Datenspeicher und Datenbanken.

[!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus Datenbanken von Drittanbietern. [!DNL Platform] kann eine Verbindung zu verschiedenen Arten von Datenbanken wie z. B. relationalen, NoSQL- oder Data Warehouse-Datenbanken herstellen. Unterstützung für Datenbankanbieter: [!DNL Microsoft] SQL Server.

## IP-Adressen-Zulassungsliste

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Leistungseinbußen führen. Weitere Informationen finden Sie auf der Seite [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md) .

>[!IMPORTANT]
>
>Der Quell-Connector [!DNL Microsoft] SQL Server unterstützt derzeit keine Verbindung zwischen denselben Regionen und Platform. Wenn Ihre Azure-Instanz also denselben Netzwerkbereich wie Platform verwendet, kann keine Verbindung zu Platform-Quellen hergestellt werden. Derzeit wird nur eine regionenübergreifende Konnektivität unterstützt. Weitere Informationen erhalten Sie von Ihrem Kundenbetreuer für Adoben.

Die folgende Dokumentation enthält Informationen dazu, wie Sie [!DNL Microsoft] SQL Server mithilfe von APIs oder der Benutzeroberfläche mit [!DNL Platform] verbinden:

## Verbinden Sie [!DNL Microsoft] SQL Server mit [!DNL Platform] mithilfe von APIs.

- [Erstellen einer Microsoft SQL Server-Basisverbindung mithilfe der Flow Service-API](../../tutorials/api/create/databases/sql-server.md)
- [Datenstruktur und Inhalt einer Datenbankquelle mithilfe der Flow Service-API durchsuchen](../../tutorials/api/explore/database-nosql.md)
- [Erstellen eines Datenflusses für eine Datenbankquelle mithilfe der Flow Service-API](../../tutorials/api/collect/database-nosql.md)

## Verbinden Sie [!DNL Microsoft] SQL Server über die Benutzeroberfläche mit [!DNL Platform].

- [Erstellen einer Quellverbindung für Microsoft SQL Server in der Benutzeroberfläche](../../tutorials/ui/create/databases/sql-server.md)
- [Erstellen eines Datenflusses für eine Datenbankquellenverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/databases.md)
