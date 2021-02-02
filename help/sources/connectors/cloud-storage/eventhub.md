---
keywords: Experience Platform;Home;beliebte Themen;Ereignis-Hubs;azure-Ereignis-Hubs;Ereignis-Hubs;Ereignis-Hubs
solution: Experience Platform
title: Azurblauer Ereignis-Hubs-Anschluss
topic: overview
description: Die nachstehende Dokumentation enthält Informationen dazu, wie Sie Azurblase-Ereignis-Hubs mithilfe von APIs oder der Benutzeroberfläche mit der Plattform verbinden.
translation-type: tm+mt
source-git-commit: 2940f030aa21d70cceeedc7806a148695f68739e
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 1%

---


# (Beta) Azurblauer Ereignis-Hubs-Anschluss

>[!NOTE]
>
>Der Azurblauer Ereignis Hubs Stecker ist in Beta. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie unter [Sources overview](../../home.md#terms-and-conditions).

Adobe Experience Platform bietet native Konnektivität für Cloud-Anbieter wie AWS, [!DNL Google Cloud Platform] und [!DNL Azure]. Sie können Ihre Daten von diesen Systemen in [!DNL Platform] übertragen.

Cloud-Datenspeicherung-Quellen können Ihre eigenen Daten in [!DNL Platform] übertragen, ohne dass Sie sie herunterladen, formatieren oder hochladen müssen. Ingetierte Daten können als XDM-JSON, XDM-Parquet oder als Trennzeichen formatiert werden. Jeder Schritt des Prozesses ist in den Sources-Workflow integriert. [!DNL Platform] ermöglicht es Ihnen, Daten  [!DNL Azure Event Hubs] in Echtzeit einzubringen.

## ZULASSUNGSLISTE der IP-Adresse

Eine Liste von IP-Adressen muss einer Zulassungsliste hinzugefügt werden, bevor Sie mit Quellschnittstellen arbeiten können. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Leistungseinbußen führen. Weitere Informationen finden Sie auf der Zulassungsliste [IP-Adresse](../../ip-address-allow-list.md).

## Verbinden Sie [!DNL Azure Event Hubs] mit [!DNL Platform]

Die nachstehende Dokumentation enthält Informationen dazu, wie [!DNL Azure Event Hubs] mithilfe von APIs oder der Benutzeroberfläche mit [!DNL Platform] verbunden wird:

### APIs verwenden

- [Erstellen eines Azurblauen Ereignis-Hubs-Connectors mit der Flow Service API](../../tutorials/api/create/cloud-storage/eventhub.md)
- [Erfassen von Streaming-Daten mithilfe der Flow Service API](../../tutorials/api/collect/streaming.md)

### Verwenden der UI

- [Erstellen eines Azurblauen Ereignis-Hubs-Quellconnectors in der Benutzeroberfläche](../../tutorials/ui/create/cloud-storage/eventhub.md)
- [Konfigurieren eines Datenflusses für einen Cloud-Datenspeicherung-Connector in der Benutzeroberfläche](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)