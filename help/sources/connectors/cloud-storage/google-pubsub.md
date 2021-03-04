---
keywords: Experience Platform;Home;beliebte Themen;Google PubSub;Google-Publikum
solution: Experience Platform
title: Google PubSub Source Connector - Übersicht
topic: Übersicht
description: Erfahren Sie, wie Sie Google PubSub mit APIs oder der Benutzeroberfläche mit Adobe Experience Platform verbinden.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 1%

---


# (Beta) [!DNL Google PubSub] Connector

>[!NOTE]
>
>Der [!DNL Google PubSub]-Anschluss befindet sich in der Betaversion. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie unter [sources overview](../../home.md#terms-and-conditions).

Adobe Experience Platform bietet native Konnektivität für Cloud-Anbieter wie [!DNL AWS], [!DNL Google Cloud Platform] und [!DNL Azure], sodass Sie Daten aus diesen Systemen zur Verwendung in nachgelagerten Diensten und Zielen in die Plattform übertragen können.

Cloud-Datenspeicherung-Quellen können Ihre Daten in eine Plattform übertragen, ohne dass Sie sie herunterladen, formatieren oder hochladen müssen. Ingetierte Daten können als XDM-JSON, XDM-Parquet oder als Trennzeichen formatiert werden. Jeder Schritt des Prozesses ist in den Quellarbeitsablauf integriert. Mit der Plattform können Sie Daten von [!DNL Azure Event Hubs] in Echtzeit einbringen.

## Zulassungsliste der IP-Adresse

Eine Liste von IP-Adressen muss einer Zulassungsliste hinzugefügt werden, bevor Sie mit Quellschnittstellen arbeiten können. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Leistungseinbußen führen. Weitere Informationen finden Sie auf der Zulassungsliste [IP-Adresse](../../ip-address-allow-list.md).

## [!DNL Google PubSub] an Plattform anschließen

Die nachstehende Dokumentation enthält Informationen dazu, wie [!DNL Google PubSub] mithilfe von APIs oder der Benutzeroberfläche mit einer Plattform verbunden werden kann:

### APIs verwenden

- [Erstellen einer Google PubSub-Quellverbindung mit der Flow Service API](../../tutorials/api/create/cloud-storage/google-pubsub.md)
- [Erfassen von Streaming-Daten mithilfe der Flow Service API](../../tutorials/api/collect/streaming.md)

### Verwenden der UI

- [Erstellen einer Google PubSub-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/create/cloud-storage/google-pubsub.md)
- [Konfigurieren eines Datenflusses für eine Cloud-Datenspeicherung-Verbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)