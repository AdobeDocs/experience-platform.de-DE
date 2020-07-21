---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: HDFS-Anschluss
topic: overview
translation-type: tm+mt
source-git-commit: 340f5d0611e9e9eb4676018ee10c8a8aa08dbb2d
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# (Beta) [!DNL Apache] HDFS-Anschluss

>[!NOTE]
>Der Apache HDFS-Anschluss befindet sich in der Beta-Version. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie in der Übersicht [zu den](../../home.md#terms-and-conditions) Quellen.

Adobe Experience Platform bietet native Konnektivität für Cloud-Anbieter wie AWS [!DNL Google Cloud Platform]und [!DNL Azure]ermöglicht es Ihnen, Ihre Daten von diesen Systemen zu übertragen. Ingetierte Daten können als JSON, Parquet oder als Trennzeichen formatiert werden. Zu den Cloud-Datenspeicherung-Anbietern zählen [!DNL Apache] HDFS.

## Zulassungsliste der IP-Adresse

Die folgenden IP-Adressen müssen einer Zulassungsliste hinzugefügt werden, bevor Sie mit Quellschnittstellen arbeiten können. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Leistungseinbußen führen.

### Ost-USA-Region

- `20.41.2.0/23`
- `20.41.4.0/26`
- `20.44.17.80/28`
- `20.49.102.16/29`
- `40.70.148.160/28`
- `52.167.107.224/28`

### Westeuropa

- `13.69.67.192/28`
- `13.69.107.112/28`
- `13.69.112.128/28`
- `40.74.24.192/26`
- `40.74.26.0/23`
- `40.113.176.232/29`
- `52.236.187.112/28`

### Australien Osten

- `13.70.74.144/28`
- `20.37.193.0/25`
- `20.37.193.128/26`
- `20.37.198.224/29`
- `40.79.163.80/28`
- `40.79.171.160/28`

In der folgenden Dokumentation finden Sie Informationen dazu, wie [!DNL Apache] HDFS mit APIs oder der [!DNL Platform] Benutzeroberfläche verbunden werden können:

## Verbinden von [!DNL Apache] HDFS mit [!DNL Platform] APIs

- [Erstellen eines HDFS-Connectors mit der Flow Service API](../../tutorials/api/create/cloud-storage/hdfs.md)
- [Kennenlernen eines Cloud-Datenspeicherung-Systems mithilfe der Flow Service API](../../tutorials/api/explore/cloud-storage.md)
- [Erfassen von Cloud-Datenspeicherung-Daten mithilfe der Flow Service API](../../tutorials/api/collect/cloud-storage.md)

## Verbinden von [!DNL Apache] HDFS mit [!DNL Platform] der Benutzeroberfläche

- [Erstellen eines Apache HDFS-Quellconnectors in der Benutzeroberfläche](../../tutorials/ui/create/cloud-storage/hdfs.md)
- [Konfigurieren eines Datenflusses für einen Cloud-Datenspeicherung-Connector in der Benutzeroberfläche](../../tutorials/ui/dataflow/batch/cloud-storage.md)