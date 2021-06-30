---
keywords: Experience Platform; Startseite; beliebte Themen; Azure Data Explorer; Azure Data Explorer
solution: Experience Platform
title: Azure Data Explorer Source Connector - Übersicht
topic-legacy: overview
description: Erfahren Sie, wie Sie Azure Data Explorer über APIs oder die Benutzeroberfläche mit Adobe Experience Platform verbinden.
exl-id: 869bd8bb-51e6-4e0c-a3ec-ff083dda5789
source-git-commit: 5821f9304a37c1a03d17f0113d09548799662a2e
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# (Beta) [!DNL Azure Data Explorer] Connector

>[!NOTE]
>
>Der Connector [!DNL Azure Data Explorer] befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectoren finden Sie unter [Quellen - Übersicht](../../home.md#terms-and-conditions) .

Adobe Experience Platform bietet native Konnektivität für Datenbankanbieter wie [!DNL Microsoft], MySQL und [!DNL Azure]. Sie können Ihre Daten aus diesen Systemen in [!DNL Platform] übertragen.

Es werden verschiedene Arten von Datenbanken von Drittanbietern unterstützt, darunter relationale Datenbanken, NoSQL-Datenbanken oder Data Warehouse. Unterstützung für Datenbankanbieter beinhaltet [!DNL Azure Data Explorer].

## IP-Adressen-Zulassungsliste

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Leistungseinbußen führen. Weitere Informationen finden Sie auf der Seite [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md) .

>[!IMPORTANT]
>
>Der Quell-Connector [!DNL Azure Data Explorer] unterstützt derzeit keine Verbindung zwischen denselben Regionen und Platform. Wenn Ihre Azure-Instanz also denselben Netzwerkbereich wie Platform verwendet, kann keine Verbindung zu Platform-Quellen hergestellt werden. Derzeit wird nur eine regionenübergreifende Konnektivität unterstützt. Weitere Informationen erhalten Sie von Ihrem Kundenbetreuer für Adoben.

Die folgende Dokumentation enthält Informationen dazu, wie Sie mithilfe von APIs oder der Benutzeroberfläche eine Verbindung zwischen [!DNL Azure Data Explorer] und [!DNL Platform] herstellen:

## Verbinden Sie [!DNL Azure Data Explorer] mit [!DNL Platform] mithilfe von APIs

- [Erstellen einer Azure Data Explorer-Basisverbindung mit der Flow Service-API](../../tutorials/api/create/databases/data-explorer.md)
- [Datenstruktur und Inhalt einer Datenbankquelle mithilfe der Flow Service-API durchsuchen](../../tutorials/api/explore/database-nosql.md)
- [Erstellen eines Datenflusses für eine Datenbankquelle mithilfe der Flow Service-API](../../tutorials/api/collect/database-nosql.md)

## Verbinden Sie [!DNL Azure Data Explorer] mit [!DNL Platform] über die Benutzeroberfläche

- [Erstellen einer Quell-Verbindung aus Azure Data Explorer in der Benutzeroberfläche](../../tutorials/ui/create/databases/data-explorer.md)
- [Erstellen eines Datenflusses für eine Datenbankquellenverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/databases.md)
