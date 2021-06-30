---
keywords: Experience Platform; Startseite; beliebte Themen; HDFS; Hdfs; Apache HDFS; Apache Hdfs
solution: Experience Platform
title: Überblick über den Apache HDFS Source Connector
topic-legacy: overview
description: Erfahren Sie, wie Sie mithilfe von APIs oder der Benutzeroberfläche Apache HDFS mit Adobe Experience Platform verbinden.
exl-id: 1f156f7b-a19d-4dcf-a51d-ab6cb396d8f7
source-git-commit: 1f9948d6e419ee5d6a021a589378f7aa990b7291
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 3%

---

# (Beta) [!DNL Apache] HDFS-Connector

>[!NOTE]
>
>Der Apache HDFS-Connector befindet sich in der Betaphase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectoren finden Sie unter [Quellen - Übersicht](../../home.md#terms-and-conditions) .

Adobe Experience Platform bietet native Konnektivität für Cloud-Anbieter wie AWS, [!DNL Google Cloud Platform] und [!DNL Azure], mit der Sie Ihre Daten aus diesen Systemen importieren können. Aufgenommene Daten können als JSON, Parquet oder als Trennzeichen formatiert werden. Unterstützt werden unter anderem [!DNL Apache] HDFS-Dateien.

## IP-Adressen-Zulassungsliste

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Leistungseinbußen führen. Weitere Informationen finden Sie auf der Seite [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md) .

## Namensbeschränkungen für Dateien und Ordner

Im Folgenden finden Sie eine Liste von Einschränkungen, die Sie beim Benennen Ihrer Cloud-Speicherdatei oder Ihres Verzeichnisses berücksichtigen müssen.

- Die Namen von Verzeichnis- und Dateikomponenten dürfen 255 Zeichen nicht überschreiten.
- Verzeichnis- und Dateinamen können nicht mit einem Schrägstrich (`/`) enden. Wenn angegeben, wird sie automatisch entfernt.
- Die folgenden Zeichen der reservierten URL müssen ordnungsgemäß maskiert sein: `! ' ( ) ; @ & = + $ , % # [ ]`
- Die folgenden Zeichen sind nicht zulässig: `" \ / : | < > * ?`.
- Unzulässige URL-Pfadzeichen sind nicht zulässig. Codepunkte wie `\uE000` sind zwar in NTFS-Dateinamen gültig, aber keine gültigen Unicode-Zeichen. Darüber hinaus sind einige ASCII- oder Unicode-Zeichen, wie Steuerzeichen (0x00 bis 0x1F, \u0081 usw.), ebenfalls nicht zulässig. Regeln für Unicode-Zeichenfolgen in HTTP/1.1 finden Sie in [RFC 2616, Abschnitt 2.2: Grundregeln](https://www.ietf.org/rfc/rfc2616.txt) und [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Die folgenden Dateinamen sind nicht zulässig: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, PRN, AUX, NUL, CON, CLOCK$, Punkt (..) und zwei Zeichen (..).

## Verbinden Sie [!DNL Apache] HDFS mit [!DNL Platform]

Die folgende Dokumentation enthält Informationen dazu, wie [!DNL Apache] HDFS mit [!DNL Platform] über APIs oder die Benutzeroberfläche verbunden werden:

### Verwenden von APIs

- [Erstellen einer HDFS-Basisverbindung mithilfe der Flow Service-API](../../tutorials/api/create/cloud-storage/hdfs.md)
- [Datenstruktur und Inhalt einer Cloud-Speicherquelle mithilfe der Flow Service-API durchsuchen](../../tutorials/api/explore/cloud-storage.md)
- [Erstellen eines Datenflusses für eine Cloud-Speicherquelle mithilfe der Flow Service-API](../../tutorials/api/collect/cloud-storage.md)

### Verwenden der UI

- [Erstellen einer Apache HDFS-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/create/cloud-storage/hdfs.md)
- [Erstellen eines Datenflusses für eine Cloud-Speicherverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/batch/cloud-storage.md)
