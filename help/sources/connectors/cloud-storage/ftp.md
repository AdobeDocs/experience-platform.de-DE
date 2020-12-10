---
keywords: Experience Platform;home;popular topics;FTP;ftp;
solution: Experience Platform
title: FTP-Anschluss
topic: overview
description: Die nachstehende Dokumentation enthält Informationen dazu, wie ein FTP-Server mit APIs oder der Benutzeroberfläche mit einer Plattform verbunden werden kann.
translation-type: tm+mt
source-git-commit: 5e5ac80e0c79b3cc0354b469edc036523e29b45d
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 2%

---


# (Beta) FTP-Anschluss

>[!NOTE]
>
>Der FTP-Anschluss befindet sich in der Betaphase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie in der Übersicht [zu den](../../home.md#terms-and-conditions) Quellen.

Adobe Experience Platform bietet native Konnektivität für Cloud-Anbieter wie AWS [!DNL Google Cloud Platform]und [!DNL Azure]ermöglicht es Ihnen, Ihre Daten von diesen Systemen zu übertragen.

Cloud storage sources can bring your own data into [!DNL Platform] without the need to download, format, or upload. Ingetierte Daten können als XDM-JSON-, XDM-Parkett oder als Trennzeichen formatiert werden. Jeder Schritt des Prozesses ist in den Sources-Workflow integriert. [!DNL Platform] ermöglicht es Ihnen, Daten von einem FTP- oder SFTP-Server über Stapel zu importieren.

>[!IMPORTANT]
>
>Beim Erstellen eines Datenflusses mit dem FTP-Quellanschluss wird dringend empfohlen, einen einmaligen Erfassungszeitplan festzulegen, da weiterhin Probleme mit inkrementellen Aktualisierungen auf FTP-Servern auftreten.

## ZULASSUNGSLISTE der IP-Adresse

Eine Liste von IP-Adressen muss einer Zulassungsliste hinzugefügt werden, bevor Sie mit Quellschnittstellen arbeiten können. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Leistungseinbußen führen. Weitere Informationen finden Sie auf der Seite zur Zulassungsliste [der](../../ip-address-allow-list.md) IP-Adresse.

## Benennungsbeschränkungen für Dateien und Ordner

Im Folgenden finden Sie eine Liste von Einschränkungen, die Sie bei der Benennung der Cloud-Datenspeicherung-Datei bzw. des Verzeichnisses berücksichtigen müssen.

- Name der Verzeichnis- und Dateikomponenten darf 255 Zeichen nicht überschreiten.
- Ordner- und Dateinamen können nicht mit einem Schrägstrich enden (`/`). Sofern vorhanden, wird sie automatisch entfernt.
- Die folgenden Zeichen für die reservierte URL müssen ordnungsgemäß mit Escape-Zeichen versehen sein: `! * ' ( ) ; : @ & = + $ , / ? % # [ ]`
- Die folgenden Zeichen sind nicht zulässig: `" \ / : | < > * ?`.
- Unzulässige URL-Pfadzeichen sind nicht zulässig. Codepunkte wie `\uE000`, die in NTFS-Dateinamen gültig sind, sind keine gültigen Unicode-Zeichen. Darüber hinaus sind einige ASCII- oder Unicode-Zeichen wie Steuerzeichen (0x00 bis 0x1F, \u0081 usw.) ebenfalls nicht zulässig. Regeln für Unicode-Zeichenfolgen in HTTP/1.1 finden Sie in [RFC 2616, Abschnitt 2.2: Grundregeln](https://www.ietf.org/rfc/rfc2616.txt) und [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Die folgenden Dateinamen sind nicht zulässig: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, Punkt (.) und zwei Punkt (..).

## FTP verbinden mit [!DNL Platform]

Die nachstehende Dokumentation enthält Informationen dazu, wie ein FTP-Server mit APIs oder der Benutzeroberfläche verbunden [!DNL Platform] werden kann:

### Verwenden der APIs

- [Erstellen eines FTP-Connectors mit der Flow Service API](../../tutorials/api/create/cloud-storage/ftp.md)
- [Kennenlernen eines Cloud-Datenspeicherung-Systems mithilfe der Flow Service API](../../tutorials/api/explore/cloud-storage.md)
- [Erfassen von Cloud-Datenspeicherung-Daten mithilfe der Flow Service API](../../tutorials/api/collect/cloud-storage.md)

### Verwenden der UI

- [Erstellen eines FTP-Quellconnectors in der Benutzeroberfläche](../../tutorials/ui/create/cloud-storage/ftp.md)
- [Konfigurieren eines Datenflusses für einen Cloud-Datenspeicherung-Connector in der Benutzeroberfläche](../../tutorials/ui/dataflow/batch/cloud-storage.md)