---
keywords: Experience Platform;Home;beliebte Themen;Ereignis-Hubs;azure-Ereignis-Hubs;Ereignis-Hubs;Ereignis-Hubs
solution: Experience Platform
title: Übersicht über den Avocent Ereignis Hubs Source Connector
topic: Übersicht
description: Erfahren Sie, wie Sie Azurblase-Ereignis-Hubs mit APIs oder der Benutzeroberfläche mit Adobe Experience Platform verbinden.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 1%

---


# (Beta) Azurblauer Ereignis-Hubs-Anschluss

>[!NOTE]
>
>Der Azurblauer Ereignis Hubs Stecker ist in Beta. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie unter [Sources overview](../../home.md#terms-and-conditions).

Adobe Experience Platform bietet native Konnektivität für Cloud-Anbieter wie AWS, [!DNL Google Cloud Platform] und [!DNL Azure]. Sie können Ihre Daten von diesen Systemen in [!DNL Platform] übertragen.

Cloud-Datenspeicherung-Quellen können Ihre eigenen Daten in [!DNL Platform] übertragen, ohne dass Sie sie herunterladen, formatieren oder hochladen müssen. Ingetierte Daten können als XDM-JSON, XDM-Parquet oder als Trennzeichen formatiert werden. Jeder Schritt des Prozesses ist in den Sources-Workflow integriert. [!DNL Platform] ermöglicht es Ihnen, Daten  [!DNL Azure Event Hubs] in Echtzeit einzubringen.

## Zulassungsliste der IP-Adresse

Eine Liste von IP-Adressen muss einer Zulassungsliste hinzugefügt werden, bevor Sie mit Quellschnittstellen arbeiten können. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Leistungseinbußen führen. Weitere Informationen finden Sie auf der Zulassungsliste [IP-Adresse](../../ip-address-allow-list.md).

## Verbinden Sie [!DNL Azure Event Hubs] mit [!DNL Platform]

Die nachstehende Dokumentation enthält Informationen dazu, wie [!DNL Azure Event Hubs] mithilfe von APIs oder der Benutzeroberfläche mit [!DNL Platform] verbunden wird:

### APIs verwenden

- [Erstellen einer Azurblauen Ereignis-Hubs-Quellverbindung mit der Flow Service API](../../tutorials/api/create/cloud-storage/eventhub.md)
- [Erfassen von Streaming-Daten mithilfe der Flow Service API](../../tutorials/api/collect/streaming.md)

### Verwenden der UI

- [Erstellen einer Azurblauen Ereignis-Hubs-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/create/cloud-storage/eventhub.md)
- [Konfigurieren eines Datenflusses für eine Cloud-Datenspeicherung-Verbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)