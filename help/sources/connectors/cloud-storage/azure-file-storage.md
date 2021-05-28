---
keywords: Experience Platform; Startseite; beliebte Themen; Azure-Dateispeicher; Azure-Dateispeicher
solution: Experience Platform
title: Azure File Storage Source Connector - Übersicht
topic-legacy: overview
description: Erfahren Sie, wie Sie Azure File Storage über APIs oder die Benutzeroberfläche mit Adobe Experience Platform verbinden.
exl-id: 0a5e9df6-9760-4eeb-86d5-d92d77df3d2b
source-git-commit: e150f05df2107d7b3a2e95a55dc4ad072294279e
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 3%

---

# Azure File Storage-Connector

Adobe Experience Platform bietet native Konnektivität für Cloud-Anbieter wie AWS, [!DNL Google Cloud Platform] und [!DNL Azure], mit der Sie Ihre Daten aus diesen Systemen importieren können.

Cloud-Speicher-Quellen können Ihre eigenen Daten in [!DNL Platform] übertragen, ohne herunterladen, formatieren oder hochladen zu müssen. Aufgenommene Daten können als XDM JSON-, XDM Parquet- oder als Trennzeichen formatiert werden. Jeder Schritt des Prozesses wird in den Sources-Workflow integriert. [!DNL Platform] ermöglicht Ihnen das Einbringen von Daten aus  [!DNL Azure File Storage] Batches.

## IP-Adressen-Zulassungsliste

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Leistungseinbußen führen. Weitere Informationen finden Sie auf der Seite [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md) .

>[!IMPORTANT]
>
>Der Quell-Connector [!DNL Azure File Storage] unterstützt derzeit keine Verbindung zwischen denselben Regionen und Platform. Wenn Ihre Azure-Instanz also denselben Netzwerkbereich wie Platform verwendet, kann keine Verbindung zu Platform-Quellen hergestellt werden. Derzeit wird nur eine regionenübergreifende Konnektivität unterstützt. Weitere Informationen erhalten Sie von Ihrem Kundenbetreuer für Adoben.

## Namensbeschränkungen für Dateien und Ordner

Im Folgenden finden Sie eine Liste von Einschränkungen, die Sie beim Benennen Ihrer Cloud-Speicherdatei oder Ihres Verzeichnisses berücksichtigen müssen.

- Die Namen von Verzeichnis- und Dateikomponenten dürfen 255 Zeichen nicht überschreiten.
- Verzeichnis- und Dateinamen können nicht mit einem Schrägstrich (`/`) enden. Wenn angegeben, wird sie automatisch entfernt.
- Die folgenden Zeichen der reservierten URL müssen ordnungsgemäß maskiert sein: `! ' ( ) ; @ & = + $ , % # [ ]`
- Die folgenden Zeichen sind nicht zulässig: `" \ / : | < > * ?`.
- Unzulässige URL-Pfadzeichen sind nicht zulässig. Codepunkte wie `\uE000` sind zwar in NTFS-Dateinamen gültig, aber keine gültigen Unicode-Zeichen. Darüber hinaus sind einige ASCII- oder Unicode-Zeichen, wie Steuerzeichen (0x00 bis 0x1F, \u0081 usw.), ebenfalls nicht zulässig. Regeln für Unicode-Zeichenfolgen in HTTP/1.1 finden Sie in [RFC 2616, Abschnitt 2.2: Grundregeln](https://www.ietf.org/rfc/rfc2616.txt) und [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Die folgenden Dateinamen sind nicht zulässig: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, PRN, AUX, NUL, CON, CLOCK$, Punkt (..) und zwei Zeichen (..).

## Verbinden Sie [!DNL Azure File Storage] mit [!DNL Platform]

Die folgende Dokumentation enthält Informationen dazu, wie Sie mithilfe von APIs oder der Benutzeroberfläche eine Verbindung zwischen [!DNL Azure File Storage] und [!DNL Platform] herstellen:

### Verwenden von APIs

- [Erstellen einer Azure File Storage-Quellverbindung mit der Flow Service-API](../../tutorials/api/create/cloud-storage/azure-file-storage.md)
- [Erkunden eines Cloud-Speichersystems mithilfe der Flow Service-API](../../tutorials/api/explore/cloud-storage.md)
- [Erfassen von Cloud-Speicherdaten mithilfe der Flow Service-API](../../tutorials/api/collect/cloud-storage.md)

### Verwenden der UI

- [Erstellen einer Azure File Storage-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/create/cloud-storage/azure-file-storage.md)
- [Konfigurieren eines Datenflusses für eine Cloud-Speicherverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/batch/cloud-storage.md)
