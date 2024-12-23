---
keywords: Experience Platform;home;popular topics;HDFS;hdfs;Apache HDFS;Apache HDFS;Apache hdfs
solution: Experience Platform
title: Apache HDFS Source Connector - Überblick
description: Erfahren Sie, wie Sie mithilfe von APIs oder der Benutzeroberfläche Apache HDFS mit Adobe Experience Platform verbinden.
exl-id: 1f156f7b-a19d-4dcf-a51d-ab6cb396d8f7
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 66%

---

# (Beta) [!DNL Apache] HDFS-Connector

>[!NOTE]
>
>Der Apache HDFS-Connector befindet sich in der Betaphase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectoren finden Sie in der [Übersicht über Quellen](../../home.md#terms-and-conditions) .

Adobe Experience Platform bietet native Konnektivität für Cloud-Anbieter wie AWS, [!DNL Google Cloud Platform] und [!DNL Azure], sodass Sie Ihre Daten aus diesen Systemen importieren können. Aufgenommene Daten können als JSON, Parquet oder als Trennzeichen formatiert werden. Unterstützt werden unter anderem [!DNL Apache] HDFS-Dateien.

## IP-Adressen-Zulassungsliste

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Performance-Einbußen führen. Weitere Information finden Sie unter [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md).

## Namensbeschränkungen für Dateien und Verzeichnisse

Im Folgenden finden Sie eine Liste von Einschränkungen, die Sie beim Benennen Ihrer Cloud-Speicherdatei oder Ihres Verzeichnisses berücksichtigen müssen.

- Die Namen von Verzeichnis- und Dateikomponenten dürfen nicht länger als 255 Zeichen sein.
- Verzeichnis- und Dateinamen dürfen nicht mit einem Schrägstrich (`/`) enden. Wenn angegeben, wird er automatisch entfernt.
- Die folgenden Zeichen der reservierten URL müssen ordnungsgemäß maskiert sein: `! ' ( ) ; @ & = + $ , % # [ ]`
- Die folgenden Zeichen sind nicht zulässig: `" \ / : | < > * ?`.
- Unzulässige URL-Pfadzeichen sind nicht zulässig. Code-Punkte wie `\uE000` sind zwar in NTFS-Dateinamen gültig, aber keine gültigen Unicode-Zeichen. Darüber hinaus sind einige ASCII- oder Unicode-Zeichen wie Steuerzeichen (0x00 bis 0x1F, \u0081 usw.) ebenfalls nicht zulässig. Regeln für Unicode-Zeichenfolgen in HTTP/1.1 finden Sie unter [RFC 2616, Abschnitt 2.2: Grundregeln](https://www.ietf.org/rfc/rfc2616.txt) und [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Die folgenden Dateinamen sind nicht zulässig: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, Punktzeichen (.) und zwei Punktzeichen (..).

## [!DNL Apache] HDFS an [!DNL Platform] anbinden

Die folgende Dokumentation enthält Informationen dazu, wie Sie [!DNL Apache] HDFS mit [!DNL Platform] über APIs oder die Benutzeroberfläche verbinden:

### Verwenden von APIs

- [Erstellen einer HDFS-Basisverbindung mithilfe der Flow Service-API](../../tutorials/api/create/cloud-storage/hdfs.md)
- [Untersuchen der Datenstruktur und des Inhalts einer Cloud-Speicherquelle mit der Flow Service-API](../../tutorials/api/explore/cloud-storage.md)
- [Erstellen eines Datenflusses für eine Cloud-Speicherquelle mithilfe der Flow Service-API](../../tutorials/api/collect/cloud-storage.md)

### Verwenden der Benutzeroberfläche

- [Erstellen einer Apache HDFS-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/create/cloud-storage/hdfs.md)
- [Erstellen eines Datenflusses für eine Cloud-Speicherverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/batch/cloud-storage.md)
