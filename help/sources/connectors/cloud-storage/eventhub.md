---
keywords: Experience Platform;home;popular topics;Azure Event Hubs;azure event hubs;Event Hubs;event hubs
solution: Experience Platform
title: Azurblauer Ereignis-Hubs-Anschluss
topic: overview
description: Die nachstehende Dokumentation enthält Informationen dazu, wie Sie Azurblase-Ereignis-Hubs mithilfe von APIs oder der Benutzeroberfläche mit der Plattform verbinden.
translation-type: tm+mt
source-git-commit: c0c609e3f385665cf88129def0c69e7d153ce201
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 1%

---


# (Beta) Azurblauer Ereignis-Hubs-Anschluss

>[!NOTE]
>
>Der Azurblauer Ereignis Hubs Stecker ist in Beta. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie in der Übersicht [zu den](../../home.md#terms-and-conditions) Quellen.

Adobe Experience Platform bietet native Konnektivität für Cloud-Anbieter wie AWS, [!DNL Google Cloud Platform]und [!DNL Azure]. Sie können Ihre Daten von diesen Systemen in [!DNL Platform]importieren.

Cloud storage sources can bring your own data into [!DNL Platform] without the need to download, format, or upload. Ingetierte Daten können als XDM-JSON-, XDM-Parkett oder als Trennzeichen formatiert werden. Jeder Schritt des Prozesses ist in den Sources-Workflow integriert. [!DNL Platform] ermöglicht es Ihnen, Daten aus [!DNL Azure Event Hubs] Echtzeit einzubringen.

## ZULASSUNGSLISTE der IP-Adresse

Eine Liste von IP-Adressen muss einer Zulassungsliste hinzugefügt werden, bevor Sie mit Quellschnittstellen arbeiten können. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Leistungseinbußen führen. Weitere Informationen finden Sie auf der Seite zur Zulassungsliste [der](../../ip-address-allow-list.md) IP-Adresse.

## Verbinden [!DNL Azure Event Hubs] mit [!DNL Platform]

Die nachstehende Dokumentation enthält Informationen zum Herstellen einer Verbindung [!DNL Azure Event Hubs] mit [!DNL Platform] APIs oder der Benutzeroberfläche:

### APIs verwenden

- [Erstellen eines Azurblauen Ereignis-Hubs-Connectors mit der Flow Service API](../../tutorials/api/create/cloud-storage/eventhub.md)
- [Erfassen von Streaming-Daten mithilfe der Flow Service API](../../tutorials/api/collect/streaming.md)

### Verwenden der UI

- [Erstellen eines Azurblauen Ereignis-Hubs-Quellconnectors in der Benutzeroberfläche](../../tutorials/ui/create/cloud-storage/eventhub.md)
- [Konfigurieren eines Datenflusses für einen Cloud-Datenspeicherung-Connector in der Benutzeroberfläche](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)