---
keywords: Experience Platform;Home;beliebte Themen;Oracle-Objekt-Datenspeicherung;oracle-Objekt-Datenspeicherung
solution: Experience Platform
title: Oracle Object Datenspeicherung Source Connector - Übersicht
topic: Übersicht
description: Erfahren Sie, wie Sie mithilfe von APIs oder der Benutzeroberfläche eine Verbindung zwischen Oracle Object Datenspeicherung und Adobe Experience Platform herstellen.
translation-type: tm+mt
source-git-commit: 04c605aedd4c52b54d0f075c169ce919650cdee9
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 3%

---


# Oracle Object Datenspeicherung Connector

Adobe Experience Platform bietet native Konnektivität für Cloud-Anbieter wie AWS, [!DNL Google Cloud Platform], damit Sie Daten von diesen Systemen zur Verwendung in nachgelagerten Diensten und Zielen in Plattform importieren können.

Cloud-Datenspeicherung-Quellen können Ihre Daten in eine Plattform übertragen, ohne dass Sie sie herunterladen, formatieren oder hochladen müssen. Ingetierte Daten können als XDM-JSON, XDM-Parquet oder als Trennzeichen formatiert werden. Jeder Schritt des Prozesses ist in den Quellarbeitsablauf integriert. Mit der Plattform können Sie Daten von [!DNL Oracle Object Storage] durch Stapel importieren.

## Zulassungsliste der IP-Adresse

Eine Liste von IP-Adressen muss einer Zulassungsliste hinzugefügt werden, bevor Sie mit Quellschnittstellen arbeiten können. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Leistungseinbußen führen. Weitere Informationen finden Sie im Dokument [IP-Adresse Zulassungsliste](../../ip-address-allow-list.md).

## Benennungsbeschränkungen für Dateien und Ordner

Im Folgenden finden Sie eine Liste von Einschränkungen, die Sie bei der Benennung der Cloud-Datenspeicherung-Datei bzw. des Verzeichnisses berücksichtigen müssen:

- Name der Verzeichnis- und Dateikomponenten darf 255 Zeichen nicht überschreiten.
- Ordner- und Dateinamen können nicht mit einem Schrägstrich (`/`) enden. Sofern vorhanden, wird sie automatisch entfernt.
- Die folgenden Zeichen für die reservierte URL müssen ordnungsgemäß mit Escape-Zeichen versehen sein: `! ' ( ) ; @ & = + $ , % # [ ]`
- Die folgenden Zeichen sind nicht zulässig: `" \ / : | < > * ?`.
- Unzulässige URL-Pfadzeichen sind nicht zulässig. Codepunkte wie `\uE000` sind zwar in NTFS-Dateinamen gültig, aber keine gültigen Unicode-Zeichen. Darüber hinaus sind einige ASCII- oder Unicode-Zeichen nicht zulässig, z. B. Steuerzeichen (0x00 bis 0x1F, \u0081 usw.). Regeln für Unicode-Zeichenfolgen in HTTP/1.1 finden Sie unter [RFC 2616, Abschnitt 2.2: Grundlegende Regeln](https://www.ietf.org/rfc/rfc2616.txt) und [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Die folgenden Dateinamen sind nicht zulässig: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, Punkt (.) und zwei Punkt (..).

## [!DNL Oracle Object Storage] an Plattform anschließen

Die nachstehende Dokumentation enthält Informationen zum Verbinden der Oracle Object Datenspeicherung mit Adobe Experience Platform mithilfe von APIs oder der Benutzeroberfläche:

### APIs verwenden

- [Erstellen einer Quellenverbindung zur Oracle Object Datenspeicherung mithilfe der Flow Service API](../../tutorials/api/create/cloud-storage/oracle-object-storage.md)
- [Kennenlernen eines Cloud-Datenspeicherung-Systems mithilfe der Flow Service API](../../tutorials/api/explore/cloud-storage.md)
- [Erfassen von Cloud-Datenspeicherung-Daten mithilfe der Flow Service API](../../tutorials/api/collect/cloud-storage.md)

### Verwenden der UI

- [Oracle Object Datenspeicherung-Quellverbindung in der Benutzeroberfläche erstellen](../../tutorials/ui/create/cloud-storage/oracle-object-storage.md)
- [Konfigurieren eines Datenflusses für eine Cloud-Datenspeicherung-Verbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/batch/cloud-storage.md)