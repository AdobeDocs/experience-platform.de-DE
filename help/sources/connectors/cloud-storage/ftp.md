---
keywords: Experience Platform;Startseite;beliebte Themen;FTP;FTP;
solution: Experience Platform
title: FTP Source Connector - Übersicht
description: Erfahren Sie, wie Sie mithilfe von APIs oder der Benutzeroberfläche einen FTP-Server mit Adobe Experience Platform verbinden.
exl-id: a6186fad-8a7b-4103-80c7-a522ff69fe9e
source-git-commit: 06b2108715ce368ff4ecf5c6c7dd3a327d9f61b1
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 64%

---

# (Beta) FTP-Connector

>[!NOTE]
>
>Der FTP-Connector befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta[gekennzeichneten Connectoren finden Sie &#x200B;](../../home.md#terms-and-conditions) „Quellen - Übersicht“ .

Adobe Experience Platform bietet native Konnektivität für Cloud-Anbieter wie AWS, [!DNL Google Cloud Platform] und [!DNL Azure], sodass Sie Ihre Daten aus diesen Systemen übernehmen können.

Mit Cloud-Speicherquellen können Sie Ihre eigenen Daten in [!DNL Experience Platform] übertragen, ohne sie herunterladen, formatieren oder hochladen zu müssen. Aufgenommene Daten können als XDM JSON, XDM Parquet oder mit Trennzeichen formatiert werden. Jeder Schritt des Prozesses wird in den Quell-Workflow integriert. Mithilfe von [!DNL Experience Platform] können Sie Daten von einem FTP- oder SFTP-Server über Batches importieren.

>[!IMPORTANT]
>
>Beim Erstellen eines Datenflusses mit dem FTP-Quell-Connector wird dringend empfohlen, einen einmaligen Aufnahmezeitplan festzulegen, da Probleme mit inkrementellen Aktualisierungen in FTP-Servern fortbestehen.

## Zulassungsliste von IP-Adressen

Sie müssen Ihrer Zulassungsliste regionsspezifische IP-Adressen hinzufügen, bevor Sie Ihre Quellen mit Experience Platform verbinden. Weitere Informationen finden Sie im Handbuch unter [Zulassungsauflistung von IP-Adressen für die Verbindung mit Experience Platform](../../ip-address-allow-list.md) .

## Namensbeschränkungen für Dateien und Verzeichnisse

Im Folgenden finden Sie eine Liste von Einschränkungen, die Sie beim Benennen Ihrer Cloud-Speicherdatei oder Ihres Verzeichnisses berücksichtigen müssen.

- Die Namen von Verzeichnis- und Dateikomponenten dürfen nicht länger als 255 Zeichen sein.
- Verzeichnis- und Dateinamen dürfen nicht mit einem Schrägstrich (`/`) enden. Wenn angegeben, wird er automatisch entfernt.
- Die folgenden Zeichen der reservierten URL müssen ordnungsgemäß maskiert sein: `! ' ( ) ; @ & = + $ , % # [ ]`
- Die folgenden Zeichen sind nicht zulässig: `" \ / : | < > * ?`.
- Unzulässige URL-Pfadzeichen sind nicht zulässig. Code-Punkte wie `\uE000` sind zwar in NTFS-Dateinamen gültig, aber keine gültigen Unicode-Zeichen. Darüber hinaus sind einige ASCII- oder Unicode-Zeichen wie Steuerzeichen (0x00 bis 0x1F, \u0081 usw.) ebenfalls nicht zulässig. Regeln für Unicode-Zeichenfolgen in HTTP/1.1 finden Sie unter [RFC 2616, Abschnitt 2.2: Grundregeln](https://www.ietf.org/rfc/rfc2616.txt) und [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Die folgenden Dateinamen sind nicht zulässig: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, Punktzeichen (.) und zwei Punktzeichen (..).

## FTP mit [!DNL Experience Platform] verbinden

Die folgende Dokumentation enthält Informationen zum Verbinden eines FTP-Servers mit [!DNL Experience Platform] mithilfe von APIs oder der Benutzeroberfläche:

### Verwenden der APIs

- [Erstellen einer FTP-Basisverbindung mithilfe der Flow Service-API](../../tutorials/api/create/cloud-storage/ftp.md)
- [Untersuchen der Datenstruktur und des Inhalts einer Cloud-Speicherquelle mit der Flow Service-API](../../tutorials/api/explore/cloud-storage.md)
- [Erstellen eines Datenflusses für eine Cloud-Speicherquelle mithilfe der Flow Service-API](../../tutorials/api/collect/cloud-storage.md)

### Verwenden der Benutzeroberfläche

- [Erstellen einer FTP-Quellverbindung über die Benutzeroberfläche](../../tutorials/ui/create/cloud-storage/ftp.md)
- [Erstellen eines Datenflusses für eine Cloud-Speicherverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/batch/cloud-storage.md)
