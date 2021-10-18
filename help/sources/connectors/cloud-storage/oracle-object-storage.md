---
keywords: Experience Platform; Homepage; beliebte Themen; Oracle-Objektspeicher; oracle-Objektspeicher
solution: Experience Platform
title: Oracle Object Storage Source Connector - Übersicht
topic-legacy: overview
description: Erfahren Sie, wie Sie mit APIs oder der Benutzeroberfläche eine Verbindung zwischen Oracle-Objektspeicher und Adobe Experience Platform herstellen.
exl-id: 5e8b85c8-9f01-49a6-9556-7b9c7518fb4b
source-git-commit: 1f9948d6e419ee5d6a021a589378f7aa990b7291
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 3%

---

# Oracle Object Storage-Connector

Adobe Experience Platform bietet native Konnektivität für Cloud-Anbieter wie AWS, [!DNL Google Cloud Platform], mit der Sie Daten aus diesen Systemen in Platform importieren und für nachgelagerte Dienste und Ziele verwenden können.

Cloud-Speicher-Quellen können Ihre Daten in Platform übertragen, ohne herunterladen, formatieren oder hochladen zu müssen. Aufgenommene Daten können als XDM JSON-, XDM Parquet- oder als Trennzeichen formatiert werden. Jeder Schritt des Prozesses wird in den Ursprungs-Workflow integriert. Mit Platform können Sie Daten von [!DNL Oracle Object Storage] durch Batches einbringen.

## IP-Adressen-Zulassungsliste

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Leistungseinbußen führen. Weitere Informationen finden Sie im Dokument [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md) .

## Namensbeschränkungen für Dateien und Ordner

Im Folgenden finden Sie eine Liste von Einschränkungen, die Sie bei der Benennung Ihrer Cloud-Speicherdatei oder Ihres Verzeichnisses berücksichtigen müssen:

- Die Namen von Verzeichnis- und Dateikomponenten dürfen 255 Zeichen nicht überschreiten.
- Verzeichnis- und Dateinamen können nicht mit einem Schrägstrich (`/`) enden. Wenn angegeben, wird sie automatisch entfernt.
- Die folgenden Zeichen der reservierten URL müssen ordnungsgemäß maskiert sein: `! ' ( ) ; @ & = + $ , % # [ ]`
- Die folgenden Zeichen sind nicht zulässig: `" \ / : | < > * ?`.
- Unzulässige URL-Pfadzeichen sind nicht zulässig. Codepunkte wie `\uE000` sind zwar in NTFS-Dateinamen gültig, aber keine gültigen Unicode-Zeichen. Darüber hinaus sind einige ASCII- oder Unicode-Zeichen nicht zulässig, z. B. Steuerzeichen (0x00 bis 0x1F, \u0081 usw.). Regeln für Unicode-Zeichenfolgen in HTTP/1.1 finden Sie in [RFC 2616, Abschnitt 2.2: Grundregeln](https://www.ietf.org/rfc/rfc2616.txt) und [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Die folgenden Dateinamen sind nicht zulässig: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, PRN, AUX, NUL, CON, CLOCK$, Punkt (..) und zwei Zeichen (..).

## Verbinden von [!DNL Oracle Object Storage] mit Platform

Die folgende Dokumentation enthält Informationen dazu, wie Sie mithilfe von APIs oder der Benutzeroberfläche eine Verbindung zwischen Oracle-Objektspeicher und Adobe Experience Platform herstellen:

### Verwenden von APIs

- [Erstellen einer Basisverbindung für Oracle-Objektspeicher mithilfe der Flow Service-API](../../tutorials/api/create/cloud-storage/oracle-object-storage.md)
- [Datenstruktur und Inhalt einer Cloud-Speicherquelle mithilfe der Flow Service-API durchsuchen](../../tutorials/api/explore/cloud-storage.md)
- [Erstellen eines Datenflusses für eine Cloud-Speicherquelle mithilfe der Flow Service-API](../../tutorials/api/collect/cloud-storage.md)

### Verwenden der UI

- [Erstellen einer Quellverbindung der Oracle-Objektspeicherung in der Benutzeroberfläche](../../tutorials/ui/create/cloud-storage/oracle-object-storage.md)
- [Erstellen eines Datenflusses für eine Cloud-Speicherverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/batch/cloud-storage.md)
