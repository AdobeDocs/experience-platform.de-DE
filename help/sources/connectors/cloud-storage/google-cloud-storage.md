---
keywords: Experience Platform;Home;beliebte Themen;Google Cloud-Datenspeicherung;Google Cloud-Datenspeicherung
solution: Experience Platform
title: Google Cloud Datenspeicherung Source Connector - Übersicht
topic: Übersicht
description: Erfahren Sie, wie Sie Google Cloud-Datenspeicherung mit APIs oder der Benutzeroberfläche mit Adobe Experience Platform verbinden.
translation-type: tm+mt
source-git-commit: 7fc99214272d2ce743b3666826c66f5d65e4d2ca
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 5%

---


# Google Cloud-Datenspeicherung-Connector

Adobe Experience Platform bietet native Konnektivität für Cloud-Anbieter wie AWS, [!DNL Google Cloud Platform] und [!DNL Azure], sodass Sie Ihre Daten von diesen Systemen übertragen können.

Cloud-Speicher bieten eine Quelle, von der Sie Ihre Daten in Platform übertragen können, ohne diese herunterladen, formatieren oder hochladen zu müssen. Ingetierte Daten können als JSON oder Parquet formatiert werden, die mit dem Experience Data Model (XDM) konform sind, oder in einem getrennten Format. Jeder Schritt des Prozesses ist in den Quellarbeitsablauf integriert. Mit der Plattform können Sie Daten von [!DNL Google Cloud Storage] durch Stapel importieren.

## Zulassungsliste der IP-Adresse

Eine Liste von IP-Adressen muss einer Zulassungsliste hinzugefügt werden, bevor Sie mit Quellschnittstellen arbeiten können. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Leistungseinbußen führen. Weitere Informationen finden Sie auf der Zulassungsliste [IP-Adresse](../../ip-address-allow-list.md).

## Voraussetzungen für die Einrichtung des [!DNL Google Cloud Storage]-Kontos

Um eine Verbindung zur Plattform herzustellen, müssen Sie zunächst die Interoperabilität für Ihr [!DNL Google Cloud Storage]-Konto aktivieren. Um auf die Interoperabilitätseinstellung zuzugreifen, öffnen Sie [!DNL Google Cloud Platform] und wählen Sie **[!UICONTROL Settings]** aus der Option **[!UICONTROL Cloud-Datenspeicherung]** im Navigationsbereich.

![](../../images/tutorials/create/google-cloud-storage/nav.png)

Die Seite **[!UICONTROL Einstellungen]** wird angezeigt. Von hier aus können Sie Informationen zu Ihrer [!DNL Google] Projekt-ID und Details zu Ihrem [!DNL Google Cloud Storage]-Konto sehen. Um auf die Interoperabilitätseinstellungen zuzugreifen, wählen Sie **[!UICONTROL Interoperabilität]** in der oberen Kopfzeile aus.

![](../../images/tutorials/create/google-cloud-storage/project-access.png)

Die Seite **[!UICONTROL Interoperabilität]** enthält Informationen zur Authentifizierung, zu Zugriffsschlüsseln und zum Standardprojekt, das mit Ihrem Dienstkonto verknüpft ist. Um eine neue Zugriffsschlüssel-ID und einen geheimen Zugriffsschlüssel für Ihr Dienstkonto zu erstellen, wählen Sie **[!UICONTROL Einen Schlüssel für ein Dienstkonto]** erstellen.

![](../../images/tutorials/create/google-cloud-storage/interoperability.png)

Sie können Ihre neu generierte Zugriffsschlüssel-ID und den geheimen Zugriffsschlüssel verwenden, um Ihr [!DNL Google Cloud Storage]-Konto mit der Plattform zu verbinden.

## Benennungsbeschränkungen für Dateien und Ordner

Im Folgenden finden Sie eine Liste von Einschränkungen, die Sie bei der Benennung der Cloud-Datenspeicherung-Datei bzw. des Verzeichnisses berücksichtigen müssen.

- Name der Verzeichnis- und Dateikomponenten darf 255 Zeichen nicht überschreiten.
- Ordner- und Dateinamen können nicht mit einem Schrägstrich (`/`) enden. Sofern vorhanden, wird sie automatisch entfernt.
- Die folgenden Zeichen für die reservierte URL müssen ordnungsgemäß mit Escape-Zeichen versehen sein: `! ' ( ) ; @ & = + $ , % # [ ]`
- Die folgenden Zeichen sind nicht zulässig: `" \ / : | < > * ?`.
- Unzulässige URL-Pfadzeichen sind nicht zulässig. Codepunkte wie `\uE000` sind zwar in NTFS-Dateinamen gültig, aber keine gültigen Unicode-Zeichen. Darüber hinaus sind einige ASCII- oder Unicode-Zeichen wie Steuerzeichen (0x00 bis 0x1F, \u0081 usw.) ebenfalls nicht zulässig. Regeln für Unicode-Zeichenfolgen in HTTP/1.1 finden Sie unter [RFC 2616, Abschnitt 2.2: Grundlegende Regeln](https://www.ietf.org/rfc/rfc2616.txt) und [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Die folgenden Dateinamen sind nicht zulässig: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, Punkt (.) und zwei Punkt (..).

## [!DNL Google Cloud Storage] an Plattform anschließen

Die nachstehende Dokumentation enthält Informationen dazu, wie [!DNL Google Cloud Storage] mithilfe von APIs oder der Benutzeroberfläche mit einer Plattform verbunden werden kann:

### APIs verwenden

- [Erstellen einer Google Cloud-Datenspeicherung-Quellverbindung mit der Flow Service API](../../tutorials/api/create/cloud-storage/google.md)
- [Kennenlernen eines Cloud-Datenspeicherung-Systems mithilfe der Flow Service API](../../tutorials/api/explore/cloud-storage.md)
- [Erfassen von Cloud-Datenspeicherung-Daten mithilfe der Flow Service API](../../tutorials/api/collect/cloud-storage.md)

### Verwenden der UI

- [Erstellen einer Google Cloud-Datenspeicherung-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [Konfigurieren eines Datenflusses für eine Cloud-Datenspeicherung-Verbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/batch/cloud-storage.md)