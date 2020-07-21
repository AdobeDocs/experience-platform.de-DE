---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Datenspeicherung Gen2-Stecker für den Azurblau-Data-See
topic: overview
translation-type: tm+mt
source-git-commit: 4d3899e8a91d15da7e40523a03285f3ccec27191
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 1%

---


# Datenspeicherung Gen2-Stecker für den Azurblau-Data-See

Adobe Experience Platform bietet native Konnektivität für Cloud-Anbieter wie AWS [!DNL Google Cloud Platform]und [!DNL Azure]ermöglicht es Ihnen, Ihre Daten von diesen Systemen zu übertragen.

Cloud storage sources can bring your own data into [!DNL Platform] without the need to download, format, or upload. Ingetierte Daten können als XDM-JSON-, XDM-Parkett oder als Trennzeichen formatiert werden. Jeder Schritt des Prozesses ist in den Sources-Workflow integriert. [!DNL Platform] ermöglicht Ihnen, Daten von [!DNL Azure Data Lake Storage Gen2] (ADLS-Gen2) durch Stapel einzubringen.

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

## Verbinden [!DNL Azure Data Lake Storage Gen2] mit [!DNL Platform]

Die nachstehende Dokumentation enthält Informationen zum Herstellen einer Verbindung [!DNL Azure Data Lake Storage Gen2] mit [!DNL Platform] APIs oder der Benutzeroberfläche:

### APIs verwenden

- [Erstellen eines ADLS-Gen2-Connectors mithilfe der Flow Service API](../../tutorials/api/create/cloud-storage/adls-gen2.md)
- [Kennenlernen eines Cloud-Datenspeicherung-Systems mithilfe der Flow Service API](../../tutorials/api/explore/cloud-storage.md)
- [Erfassen von Cloud-Datenspeicherung-Daten mithilfe der Flow Service API](../../tutorials/api/collect/cloud-storage.md)

## Verwenden der UI

- [ADLS-Gen2-Quellanschluss in der Benutzeroberfläche erstellen](../../tutorials/ui/create/cloud-storage/adls-gen2.md)
- [Konfigurieren eines Datenflusses für einen Cloud-Datenspeicherung-Connector in der Benutzeroberfläche](../../tutorials/ui/dataflow/batch/cloud-storage.md)