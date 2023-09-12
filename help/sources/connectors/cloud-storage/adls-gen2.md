---
title: Azure Data Lake Storage Gen2 Source Connector - Überblick
description: Erfahren Sie, wie Sie mit APIs oder der Benutzeroberfläche Azure Data Lake Storage Gen2 mit Adobe Experience Platform verbinden.
exl-id: 424d7278-44d9-4653-82c0-eb21cbb9b623
source-git-commit: f879f2a627e55db96a89796b9f3308744bf93f67
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 63%

---

# Azure Data Lake Storage Gen2-Connector

Adobe Experience Platform bietet native Konnektivität für Cloud-Anbieter wie AWS, [!DNL Google Cloud Platform] und [!DNL Azure], sodass Sie Ihre Daten aus diesen Systemen übernehmen können.

Cloud-Speicher-Quellen können Ihre eigenen Daten in Experience Platform übertragen, ohne herunterladen, formatieren oder hochladen zu müssen. Aufgenommene Daten können als XDM JSON, XDM Parquet oder mit Trennzeichen formatiert werden. Jeder Schritt des Prozesses wird in den Quell-Workflow integriert. Mit Experience Platform können Sie Daten aus [!DNL Azure Data Lake Storage Gen2] (ADLS Gen2) durch Batches.

## IP-Adressen-Zulassungsliste

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Leistungseinbußen führen. Weitere Information finden Sie unter [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md).

>[!IMPORTANT]
>
>Die [!DNL Azure Data Lake Storage Gen2] -Quelle unterstützt keine Konnektivität mit demselben Bereich zum Experience Platform. Wenn Ihre Azure-Instanz denselben Netzwerkbereich wie Experience Platform verwendet, kann keine Verbindung zu Experience Platform-Quellen hergestellt werden. Verwenden Sie bei der Einrichtung Ihrer [!DNL Azure Data Lake Storage Gen2] -Quelle. Derzeit wird nur eine regionenübergreifende Konnektivität unterstützt.

## Namensbeschränkungen für Dateien und Verzeichnisse

Im Folgenden finden Sie eine Liste von Einschränkungen, die Sie beim Benennen Ihrer Cloud-Speicherdatei oder Ihres Verzeichnisses berücksichtigen müssen.

- Die Namen von Verzeichnis- und Dateikomponenten dürfen nicht länger als 255 Zeichen sein.
- Verzeichnis- und Dateinamen dürfen nicht mit einem Schrägstrich (`/`) enden. Wenn angegeben, wird er automatisch entfernt.
- Die folgenden Zeichen der reservierten URL müssen ordnungsgemäß maskiert sein: `! ' ( ) ; @ & = + $ , % # [ ]`
- Die folgenden Zeichen sind nicht zulässig: `" \ / : | < > * ?`.
- Unzulässige URL-Pfadzeichen sind nicht zulässig. Code-Punkte wie `\uE000` sind zwar in NTFS-Dateinamen gültig, aber keine gültigen Unicode-Zeichen. Darüber hinaus sind einige ASCII- oder Unicode-Zeichen wie Steuerzeichen (0x00 bis 0x1F, \u0081 usw.) ebenfalls nicht zulässig. Regeln für Unicode-Zeichenfolgen in HTTP/1.1 finden Sie unter [RFC 2616, Abschnitt 2.2: Grundregeln](https://www.ietf.org/rfc/rfc2616.txt) und [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Die folgenden Dateinamen sind nicht zulässig: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, Punktzeichen (.) und zwei Punktzeichen (..).

## Verbinden [!DNL Azure Data Lake Storage Gen2] auf Experience Platform

>[!NOTE]
>
>Der beim Erstellen eines [!DNL Azure Data Lake Storage Gen2] -Konto sollte mindestens **Storage Blob Data Reader** Von der Zugriffskontrolle (IAM) zugewiesene Rolle

Die folgende Dokumentation enthält Informationen zur Verbindung [!DNL Azure Data Lake Storage Gen2] zum Experience Platform mithilfe von APIs oder der Benutzeroberfläche:

### Verwenden von APIs

- [Erstellen Sie eine [!DNL Azure Data Lake Storage Gen2] Basisverbindung mit der Flow Service-API](../../tutorials/api/create/cloud-storage/adls-gen2.md)
- [Untersuchen der Datenstruktur und des Inhalts einer Cloud-Speicherquelle mit der Flow Service-API](../../tutorials/api/explore/cloud-storage.md)
- [Erstellen eines Datenflusses für eine Cloud-Speicherquelle mithilfe der Flow Service-API](../../tutorials/api/collect/cloud-storage.md)

### Verwenden der Benutzeroberfläche

- [Erstellen Sie eine [!DNL Azure Data Lake Storage Gen2] Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/create/cloud-storage/adls-gen2.md)
- [Erstellen eines Datenflusses für eine Cloud-Speicherverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/batch/cloud-storage.md)
