---
keywords: Experience Platform;Home;beliebte Themen;Microsoft SQL;Microsoft sql;SQL;sql
solution: Experience Platform
title: Übersicht über SQL Server Source Connector
topic: Übersicht
description: Erfahren Sie, wie Sie Microsoft SQL Server mit APIs oder der Benutzeroberfläche mit Adobe Experience Platform verbinden.
translation-type: tm+mt
source-git-commit: 0fb97fcf5d3f8230ff86906aeef245e4a7f44f30
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 9%

---


# (Beta) [!DNL Microsoft] SQL Server-Connector

Adobe Experience Platform ermöglicht die Erfassung von Daten aus externen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von [!DNL Platform]-Diensten zu strukturieren, zu beschriften und zu verbessern. Daten können aus verschiedensten Quellen erfasst werden, darunter etwa Adobe-Anwendungen, Cloud-basierte Datenspeicher und Datenbanken.

[!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus Datenbanken von Drittanbietern. [!DNL Platform] kann eine Verbindung zu verschiedenen Arten von Datenbanken wie z. B. relationale Datenbanken, NoSQL oder Data Warehouse herstellen. Zu den Datenbankanbietern zählen [!DNL Microsoft] SQL Server.

## Zulassungsliste der IP-Adresse

Eine Liste von IP-Adressen muss einer Zulassungsliste hinzugefügt werden, bevor Sie mit Quellschnittstellen arbeiten können. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Leistungseinbußen führen. Weitere Informationen finden Sie auf der Zulassungsliste [IP-Adresse](../../ip-address-allow-list.md).

>[!IMPORTANT]
>
>Der [!DNL Microsoft] SQL Server-Quellanschluss unterstützt derzeit keine Verbindung mit der Plattform für dieselbe Region. Das bedeutet, dass eine Verbindung zu Plattformquellen nicht hergestellt werden kann, wenn Ihre Azurblase-Instanz denselben Netzwerkbereich wie Platform verwendet. Derzeit wird nur die regionenübergreifende Konnektivität unterstützt. Weitere Informationen erhalten Sie von Ihrem Kundenbetreuer für Adoben.

Die nachstehende Dokumentation enthält Informationen dazu, wie [!DNL Microsoft] SQL Server mit [!DNL Platform] mithilfe von APIs oder der Benutzeroberfläche verbunden wird:

## Verbinden Sie [!DNL Microsoft] SQL Server mit [!DNL Platform] mithilfe von APIs

- [Erstellen einer Microsoft SQL Server-Quellverbindung mit der Flow Service API](../../tutorials/api/create/databases/sql-server.md)
- [Durchsuchen eines Datenbanksystems mit der Flow Service API](../../tutorials/api/explore/database-nosql.md)
- [Erfassen von Daten aus einer Datenbank mithilfe der Flow Service API](../../tutorials/api/collect/database-nosql.md)

## Verbinden Sie [!DNL Microsoft] SQL Server mit [!DNL Platform] mithilfe der Benutzeroberfläche

- [Erstellen einer Microsoft SQL Server-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/create/databases/sql-server.md)
- [Konfigurieren eines Datenflusses für eine Datenbankverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/databases.md)