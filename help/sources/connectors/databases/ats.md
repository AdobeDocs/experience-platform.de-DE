---
keywords: Experience Platform;Startseite;beliebte Themen;Azure Table Storage;aze table storage;ATS;ats
solution: Experience Platform
title: Azure Table Storage Source Connector - Übersicht
topic-legacy: overview
description: Erfahren Sie, wie Sie Azure Table Storage über APIs oder die Benutzeroberfläche mit Adobe Experience Platform verbinden.
exl-id: 096e01b1-7e95-4e30-87de-d0976f8b438a
source-git-commit: 5821f9304a37c1a03d17f0113d09548799662a2e
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 8%

---

# (Beta) [!DNL Azure Table Storage] Connector

>[!NOTE]
>
>Der Connector [!DNL Azure Table Storage] befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectoren finden Sie unter [Quellen - Übersicht](../../home.md#terms-and-conditions) .

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von [!DNL Platform]-Diensten zu strukturieren, zu beschriften und zu erweitern. Daten können aus verschiedensten Quellen erfasst werden, darunter etwa Adobe-Anwendungen, Cloud-basierte Datenspeicher und Datenbanken.

[!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus Datenbanken von Drittanbietern. [!DNL Platform] kann eine Verbindung zu verschiedenen Arten von Datenbanken wie z. B. relationalen, NoSQL- oder Data Warehouse-Datenbanken herstellen. Unterstützung für Datenbankanbieter: [!DNL Azure Table Storage].

## IP-Adressen-Zulassungsliste

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Leistungseinbußen führen. Weitere Informationen finden Sie auf der Seite [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md) .

>[!IMPORTANT]
>
>Der Quell-Connector [!DNL Azure Table Storage] unterstützt derzeit keine Verbindung zwischen denselben Regionen und Platform. Wenn Ihre Azure-Instanz also denselben Netzwerkbereich wie Platform verwendet, kann keine Verbindung zu Platform-Quellen hergestellt werden. Derzeit wird nur eine regionenübergreifende Konnektivität unterstützt. Weitere Informationen erhalten Sie von Ihrem Kundenbetreuer für Adoben.

Die folgende Dokumentation enthält Informationen dazu, wie Sie mithilfe von APIs oder der Benutzeroberfläche eine Verbindung zwischen [!DNL Azure Table Storage] und [!DNL Platform] herstellen:

## Verbinden Sie [!DNL Azure Table Storage] mit [!DNL Platform] mithilfe von APIs

- [Erstellen einer Azure Table Storage-Basisverbindung mit der Flow Service-API](../../tutorials/api/create/databases/ats.md)
- [Datenstruktur und Inhalt einer Datenbankquelle mithilfe der Flow Service-API durchsuchen](../../tutorials/api/explore/database-nosql.md)
- [Erstellen eines Datenflusses für eine Datenbankquelle mithilfe der Flow Service-API](../../tutorials/api/collect/database-nosql.md)

## Verbinden Sie [!DNL Azure Table Storage] mit [!DNL Platform] über die Benutzeroberfläche

- [Erstellen einer Quellverbindung aus Azure Table Storage in der Benutzeroberfläche](../../tutorials/ui/create/databases/ats.md)
- [Erstellen eines Datenflusses für eine Datenbankquellenverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/databases.md)
