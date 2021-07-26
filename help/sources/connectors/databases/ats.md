---
keywords: Experience Platform;Startseite;beliebte Themen;Azure Table Storage;aze table storage;ATS;ats
solution: Experience Platform
title: Azure Table Storage Source Connector - Übersicht
topic-legacy: overview
description: Erfahren Sie, wie Sie Azure Table Storage über APIs oder die Benutzeroberfläche mit Adobe Experience Platform verbinden.
exl-id: 096e01b1-7e95-4e30-87de-d0976f8b438a
source-git-commit: 7af79b9e0d6ed29b796ac7c98b4df1dda09f3513
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 18%

---

# [!DNL Azure Table Storage] Connector

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen erfasst werden, darunter etwa Adobe-Anwendungen, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform ermöglicht die Aufnahme von Daten aus Datenbanken von Drittanbietern. Platform kann eine Verbindung zu verschiedenen Arten von Datenbanken wie z. B. relationalen, NoSQL- oder Data Warehouse-Datenbanken herstellen. Unterstützung für Datenbankanbieter: [!DNL Azure Table Storage].

## IP-Adressen-Zulassungsliste

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Leistungseinbußen führen. Weitere Informationen finden Sie auf der Seite [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md) .

>[!IMPORTANT]
>
>Der Quell-Connector [!DNL Azure Table Storage] unterstützt derzeit keine Verbindung zwischen denselben Regionen und Platform. Wenn Ihre Azure-Instanz also denselben Netzwerkbereich wie Platform verwendet, kann keine Verbindung zu Platform-Quellen hergestellt werden. Derzeit wird nur eine regionenübergreifende Konnektivität unterstützt. Weitere Informationen erhalten Sie von Ihrem Kundenbetreuer für Adoben.

Die folgende Dokumentation enthält Informationen dazu, wie Sie mithilfe von APIs oder der Benutzeroberfläche eine Verbindung von [!DNL Azure Table Storage] mit Platform herstellen:

## Verbinden von [!DNL Azure Table Storage] mit Platform mithilfe von APIs

- [Erstellen einer Azure Table Storage-Basisverbindung mit der Flow Service-API](../../tutorials/api/create/databases/ats.md)
- [Datenstruktur und Inhalt einer Datenbankquelle mithilfe der Flow Service-API durchsuchen](../../tutorials/api/explore/database-nosql.md)
- [Erstellen eines Datenflusses für eine Datenbankquelle mithilfe der Flow Service-API](../../tutorials/api/collect/database-nosql.md)

## Verbinden von [!DNL Azure Table Storage] mit Platform über die Benutzeroberfläche

- [Erstellen einer Quellverbindung aus Azure Table Storage in der Benutzeroberfläche](../../tutorials/ui/create/databases/ats.md)
- [Erstellen eines Datenflusses für eine Datenbankquellenverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/databases.md)
