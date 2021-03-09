---
keywords: Experience Platform;Home;beliebte Themen;Datenspeicherung von Azurblase-Dateien;Azoure-Datei-Datenspeicherung
solution: Experience Platform
title: Übersicht über den Source Connector für die AEM File Datenspeicherung
topic: Übersicht
description: Erfahren Sie, wie Sie die Datenspeicherung von Blauen Dateien mit Adobe Experience Platform über APIs oder die Benutzeroberfläche verbinden.
translation-type: tm+mt
source-git-commit: 0fb97fcf5d3f8230ff86906aeef245e4a7f44f30
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 2%

---


# (Beta) Blue File Datenspeicherung Connector

>[!NOTE]
>
>Der Azurblase File Datenspeicherung Stecker ist in Beta. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectors finden Sie unter [Sources overview](../../home.md#terms-and-conditions).

Adobe Experience Platform bietet native Konnektivität für Cloud-Anbieter wie AWS, [!DNL Google Cloud Platform] und [!DNL Azure], sodass Sie Ihre Daten von diesen Systemen übertragen können.

Cloud-Datenspeicherung-Quellen können Ihre eigenen Daten in [!DNL Platform] übertragen, ohne dass Sie sie herunterladen, formatieren oder hochladen müssen. Ingetierte Daten können als XDM-JSON, XDM-Parquet oder als Trennzeichen formatiert werden. Jeder Schritt des Prozesses ist in den Sources-Workflow integriert. [!DNL Platform] ermöglicht Ihnen, Daten aus  [!DNL Azure File Storage] Stapeln einzubringen.

## Zulassungsliste der IP-Adresse

Eine Liste von IP-Adressen muss einer Zulassungsliste hinzugefügt werden, bevor Sie mit Quellschnittstellen arbeiten können. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Leistungseinbußen führen. Weitere Informationen finden Sie auf der Zulassungsliste [IP-Adresse](../../ip-address-allow-list.md).

>[!IMPORTANT]
>
>Der [!DNL Azure File Storage]-Quellanschluss unterstützt derzeit keine Verbindung mit Plattform für dieselbe Region. Das bedeutet, dass eine Verbindung zu Plattformquellen nicht hergestellt werden kann, wenn Ihre Azurblase-Instanz denselben Netzwerkbereich wie Platform verwendet. Derzeit wird nur die regionenübergreifende Konnektivität unterstützt. Weitere Informationen erhalten Sie von Ihrem Kundenbetreuer für Adoben.

## Benennungsbeschränkungen für Dateien und Ordner

Im Folgenden finden Sie eine Liste von Einschränkungen, die Sie bei der Benennung der Cloud-Datenspeicherung-Datei bzw. des Verzeichnisses berücksichtigen müssen.

- Name der Verzeichnis- und Dateikomponenten darf 255 Zeichen nicht überschreiten.
- Ordner- und Dateinamen können nicht mit einem Schrägstrich (`/`) enden. Sofern vorhanden, wird sie automatisch entfernt.
- Die folgenden Zeichen für die reservierte URL müssen ordnungsgemäß mit Escape-Zeichen versehen sein: `! * ' ( ) ; : @ & = + $ , / ? % # [ ]`
- Die folgenden Zeichen sind nicht zulässig: `" \ / : | < > * ?`.
- Unzulässige URL-Pfadzeichen sind nicht zulässig. Codepunkte wie `\uE000` sind zwar in NTFS-Dateinamen gültig, aber keine gültigen Unicode-Zeichen. Darüber hinaus sind einige ASCII- oder Unicode-Zeichen wie Steuerzeichen (0x00 bis 0x1F, \u0081 usw.) ebenfalls nicht zulässig. Regeln für Unicode-Zeichenfolgen in HTTP/1.1 finden Sie unter [RFC 2616, Abschnitt 2.2: Grundlegende Regeln](https://www.ietf.org/rfc/rfc2616.txt) und [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Die folgenden Dateinamen sind nicht zulässig: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, Punkt (.) und zwei Punkt (..).

## Verbinden Sie [!DNL Azure File Storage] mit [!DNL Platform]

Die nachstehende Dokumentation enthält Informationen dazu, wie [!DNL Azure File Storage] mithilfe von APIs oder der Benutzeroberfläche mit [!DNL Platform] verbunden wird:

### APIs verwenden

- [Erstellen Sie eine Quellverbindung für eine Azurblase-Datenspeicherung mithilfe der Flow Service API](../../tutorials/api/create/cloud-storage/azure-file-storage.md)
- [Kennenlernen eines Cloud-Datenspeicherung-Systems mithilfe der Flow Service API](../../tutorials/api/explore/cloud-storage.md)
- [Erfassen von Cloud-Datenspeicherung-Daten mithilfe der Flow Service API](../../tutorials/api/collect/cloud-storage.md)

### Verwenden der UI

- [Erstellen einer Azurblase-Datenspeicherung-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/create/cloud-storage/azure-file-storage.md)
- [Konfigurieren eines Datenflusses für eine Cloud-Datenspeicherung-Verbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/batch/cloud-storage.md)