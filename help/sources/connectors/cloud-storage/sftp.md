---
keywords: Experience Platform; Startseite; beliebte Themen; SFTP; SFTP
solution: Experience Platform
title: Übersicht über den SFTP-Quell-Connector
topic-legacy: overview
description: Erfahren Sie, wie Sie über APIs oder die Benutzeroberfläche einen SFTP-Server mit Adobe Experience Platform verbinden.
exl-id: d5bced3d-cd33-40ea-bce0-32c76ecd2790
source-git-commit: 1f9948d6e419ee5d6a021a589378f7aa990b7291
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 2%

---

# SFTP-Connector

Adobe Experience Platform bietet native Konnektivität für Cloud-Anbieter wie AWS, [!DNL Google Cloud Platform] und [!DNL Azure], mit der Sie Ihre Daten aus diesen Systemen importieren können.

Cloud-Speicher-Quellen können Ihre eigenen Daten in [!DNL Platform] übertragen, ohne herunterladen, formatieren oder hochladen zu müssen. Aufgenommene Daten können als XDM JSON-, XDM Parquet- oder als Trennzeichen formatiert werden. Jeder Schritt des Prozesses wird in den Sources-Workflow integriert. [!DNL Platform] können Sie Daten von einem FTP- oder SFTP-Server über Batches importieren.

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

## SFTP an [!DNL Platform] anbinden

>[!IMPORTANT]
>
>Benutzer müssen die interaktive Tastaturauthentifizierung in der SFTP-Serverkonfiguration vor der Verbindung deaktivieren. Durch Deaktivieren der Einstellung können Kennwörter manuell eingegeben werden, anstatt über einen Dienst oder ein Programm einzugeben. Weitere Informationen zur interaktiven Tastaturauthentifizierung finden Sie im Dokument [Component Pro](https://doc.componentpro.com/ComponentPro-Sftp/authenticating-with-a-keyboard-interactive-authentication) .

Die folgende Dokumentation enthält Informationen dazu, wie Sie mithilfe von APIs oder der Benutzeroberfläche einen SFTP-Server mit [!DNL Platform] verbinden:

### APIs verwenden

- [Erstellen einer SFTP-Basisverbindung mit der Flow Service-API](../../tutorials/api/create/cloud-storage/sftp.md)
- [Datenstruktur und Inhalt einer Cloud-Speicherquelle mithilfe der Flow Service-API durchsuchen](../../tutorials/api/explore/cloud-storage.md)
- [Erstellen eines Datenflusses für eine Cloud-Speicherquelle mithilfe der Flow Service-API](../../tutorials/api/collect/cloud-storage.md)

### Verwenden der UI

- [Erstellen einer SFTP-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/create/cloud-storage/sftp.md)
- [Erstellen eines Datenflusses für eine Cloud-Speicherverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/batch/cloud-storage.md)
