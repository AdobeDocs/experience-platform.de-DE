---
title: Übersicht über den Source-Connector für Azure Data Lake Storage Gen2
description: Erfahren Sie, wie Sie Azure Data Lake Storage Gen2 mithilfe von APIs oder der Benutzeroberfläche mit Adobe Experience Platform verbinden.
exl-id: 424d7278-44d9-4653-82c0-eb21cbb9b623
source-git-commit: 06b2108715ce368ff4ecf5c6c7dd3a327d9f61b1
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 57%

---

# Azure Data Lake Storage Gen2-Connector

Adobe Experience Platform bietet native Konnektivität für Cloud-Anbieter wie AWS, [!DNL Google Cloud Platform] und [!DNL Azure], sodass Sie Ihre Daten aus diesen Systemen übernehmen können.

Cloud-Speicherquellen können Ihre eigenen Daten in Experience Platform übertragen, ohne sie herunterladen, formatieren oder hochladen zu müssen. Aufgenommene Daten können als XDM JSON, XDM Parquet oder mit Trennzeichen formatiert werden. Jeder Schritt des Prozesses wird in den Quell-Workflow integriert. Mit Experience Platform können Sie Daten aus [!DNL Azure Data Lake Storage Gen2] (ADLS Gen2) über Batches importieren.

## Zulassungsliste von IP-Adressen

Sie müssen Ihrer Zulassungsliste regionsspezifische IP-Adressen hinzufügen, bevor Sie Ihre Quellen mit Experience Platform verbinden. Weitere Informationen finden Sie im Handbuch unter [Zulassungsauflistung von IP-Adressen für die Verbindung mit Experience Platform](../../ip-address-allow-list.md) .

>[!IMPORTANT]
>
>Die [!DNL Azure Data Lake Storage Gen2]-Quelle unterstützt keine Konnektivität derselben Region mit Experience Platform. Wenn Ihre [!DNL Azure] dieselbe Netzwerkregion wie Experience Platform verwendet, kann keine Verbindung zu Experience Platform-Quellen hergestellt werden. Derzeit wird nur eine regionenübergreifende Konnektivität unterstützt.

## Namensbeschränkungen für Dateien und Verzeichnisse

Im Folgenden finden Sie eine Liste von Einschränkungen, die Sie beim Benennen Ihrer Cloud-Speicherdatei oder Ihres Verzeichnisses berücksichtigen müssen.

- Die Namen von Verzeichnis- und Dateikomponenten dürfen nicht länger als 255 Zeichen sein.
- Verzeichnis- und Dateinamen dürfen nicht mit einem Schrägstrich (`/`) enden. Wenn angegeben, wird er automatisch entfernt.
- Die folgenden Zeichen der reservierten URL müssen ordnungsgemäß maskiert sein: `! ' ( ) ; @ & = + $ , % # [ ]`
- Die folgenden Zeichen sind nicht zulässig: `" \ / : | < > * ?`.
- Unzulässige URL-Pfadzeichen sind nicht zulässig. Code-Punkte wie `\uE000` sind zwar in NTFS-Dateinamen gültig, aber keine gültigen Unicode-Zeichen. Darüber hinaus sind einige ASCII- oder Unicode-Zeichen wie Steuerzeichen (0x00 bis 0x1F, \u0081 usw.) ebenfalls nicht zulässig. Regeln für Unicode-Zeichenfolgen in HTTP/1.1 finden Sie unter [RFC 2616, Abschnitt 2.2: Grundregeln](https://www.ietf.org/rfc/rfc2616.txt) und [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Die folgenden Dateinamen sind nicht zulässig: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, Punktzeichen (.) und zwei Punktzeichen (..).

## Verbinden von [!DNL Azure Data Lake Storage Gen2] mit Experience Platform

>[!NOTE]
>
>Dem bei der Erstellung eines [!DNL Azure Data Lake Storage Gen2] verwendeten Service-Prinzipal sollte mindestens die Rolle **Storage Blob Data Reader** von Access Control (IAM) zugewiesen sein

Die folgende Dokumentation enthält Informationen zum Verbinden von [!DNL Azure Data Lake Storage Gen2] mit Experience Platform mithilfe von APIs oder der Benutzeroberfläche:

### Verwenden von APIs

- [Erstellen  [!DNL Azure Data Lake Storage Gen2]  Basisverbindung mithilfe der Flow Service-API](../../tutorials/api/create/cloud-storage/adls-gen2.md)
- [Untersuchen der Datenstruktur und des Inhalts einer Cloud-Speicherquelle mit der Flow Service-API](../../tutorials/api/explore/cloud-storage.md)
- [Erstellen eines Datenflusses für eine Cloud-Speicherquelle mithilfe der Flow Service-API](../../tutorials/api/collect/cloud-storage.md)

### Verwenden der Benutzeroberfläche

- [Erstellen einer  [!DNL Azure Data Lake Storage Gen2] -Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/create/cloud-storage/adls-gen2.md)
- [Erstellen eines Datenflusses für eine Cloud-Speicherverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/batch/cloud-storage.md)
