---
keywords: Experience Platform; Startseite; beliebte Themen; Blob; Blob; Azure Blob; Azure Blob
solution: Experience Platform
title: Azure Blob Source Connector - Überblick
topic-legacy: overview
description: Erfahren Sie, wie Sie Azure Blob mit Adobe Experience Platform über APIs oder die Benutzeroberfläche verbinden.
exl-id: 62adc74f-3570-42c7-9ae6-3ddbc09eccc7
source-git-commit: 251da91844311d08766ee2407ae0b775d4ac6aba
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 64%

---

# Azure-Blob-Connector

Adobe Experience Platform bietet native Konnektivität für Cloud-Anbieter wie AWS, [!DNL Google Cloud Platform]und [!DNL Azure]. Sie können Ihre Daten aus diesen Systemen in [!DNL Platform].

Mit Cloud-Speicherquellen können Sie Ihre eigenen Daten in [!DNL Platform] übertragen, ohne sie herunterladen, formatieren oder hochladen zu müssen. Aufgenommene Daten können als XDM JSON, XDM Parquet oder mit Trennzeichen formatiert werden. Jeder Schritt des Prozesses wird in den Quell-Workflow integriert. [!DNL Platform] ermöglicht Ihnen das Einbringen von Daten aus [!DNL Azure Blob] durch Batches.

## IP-Adressen-Zulassungsliste

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Leistungseinbußen führen. Weitere Information finden Sie unter [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md).

>[!IMPORTANT]
>
>Die [!DNL Azure Blob] -Quelle unterstützt keine Konnektivität der gleichen Region mit Experience Platform. Wenn Ihre Azure-Instanz denselben Netzwerkbereich wie Experience Platform verwendet, kann keine Verbindung zu Experience Platform-Quellen hergestellt werden. Verwenden Sie bei der Einrichtung Ihrer [!DNL Azure Blob] -Quelle. Derzeit wird nur eine regionenübergreifende Konnektivität unterstützt.

## Namensbeschränkungen für Dateien und Verzeichnisse

Im Folgenden finden Sie eine Liste von Einschränkungen, die Sie beim Benennen Ihrer Cloud-Speicherdatei oder Ihres Verzeichnisses berücksichtigen müssen.

- Die Namen von Verzeichnis- und Dateikomponenten dürfen nicht länger als 255 Zeichen sein.
- Verzeichnis- und Dateinamen dürfen nicht mit einem Schrägstrich (`/`) enden. Wenn angegeben, wird er automatisch entfernt.
- Die folgenden Zeichen der reservierten URL müssen ordnungsgemäß maskiert sein: `! ' ( ) ; @ & = + $ , % # [ ]`
- Die folgenden Zeichen sind nicht zulässig: `" \ / : | < > * ?`.
- Unzulässige URL-Pfadzeichen sind nicht zulässig. Code-Punkte wie `\uE000` sind zwar in NTFS-Dateinamen gültig, aber keine gültigen Unicode-Zeichen. Darüber hinaus sind einige ASCII- oder Unicode-Zeichen wie Steuerzeichen (0x00 bis 0x1F, \u0081 usw.) ebenfalls nicht zulässig. Regeln für Unicode-Zeichenfolgen in HTTP/1.1 finden Sie unter [RFC 2616, Abschnitt 2.2: Grundregeln](https://www.ietf.org/rfc/rfc2616.txt) und [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Die folgenden Dateinamen sind nicht zulässig: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, Punktzeichen (.) und zwei Punktzeichen (..).

## Verbinden [!DNL Azure Blob] nach [!DNL Platform]

Die folgende Dokumentation enthält Informationen dazu, wie Sie Azure Blob mit Adobe Experience Platform über APIs oder die Benutzeroberfläche verbinden:

### Verwenden von APIs

- [Erstellen einer Azure Blob-Basisverbindung mit der Flow Service-API](../../tutorials/api/create/cloud-storage/blob.md)
- [Untersuchen der Datenstruktur und des Inhalts einer Cloud-Speicherquelle mit der Flow Service-API](../../tutorials/api/explore/cloud-storage.md)
- [Erstellen eines Datenflusses für eine Cloud-Speicherquelle mithilfe der Flow Service-API](../../tutorials/api/collect/cloud-storage.md)

### Verwenden der Benutzeroberfläche

- [Erstellen einer Azure Blob-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/create/cloud-storage/blob.md)
- [Erstellen eines Datenflusses für eine Cloud-Speicherverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/batch/cloud-storage.md)
