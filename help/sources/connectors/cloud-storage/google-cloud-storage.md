---
keywords: Experience Platform; Startseite; beliebte Themen; Google Cloud-Speicher; Google Cloud-Speicher
solution: Experience Platform
title: Google Cloud Storage Source Connector - Überblick
topic-legacy: overview
description: Erfahren Sie, wie Sie Google Cloud Storage über APIs oder die Benutzeroberfläche mit Adobe Experience Platform verbinden.
exl-id: f7ebd213-f914-4c49-aebd-1df4514ffec0
source-git-commit: 1f9948d6e419ee5d6a021a589378f7aa990b7291
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 5%

---

# Google Cloud Storage-Connector

Adobe Experience Platform bietet native Konnektivität für Cloud-Anbieter wie AWS, [!DNL Google Cloud Platform] und [!DNL Azure], mit der Sie Ihre Daten aus diesen Systemen importieren können.

Cloud-Speicher bieten eine Quelle, von der Sie Ihre Daten in Platform übertragen können, ohne diese herunterladen, formatieren oder hochladen zu müssen. Aufgenommene Daten können als JSON- oder Parquet-Datei formatiert werden, die mit dem Experience-Datenmodell (XDM) konform ist, oder in einem getrennten Format. Jeder Schritt des Prozesses wird in den Ursprungs-Workflow integriert. Mit Platform können Sie Daten von [!DNL Google Cloud Storage] durch Batches einbringen.

## IP-Adressen-Zulassungsliste

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Leistungseinbußen führen. Weitere Informationen finden Sie auf der Seite [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md) .

## Voraussetzungen für die Einrichtung eines [!DNL Google Cloud Storage]-Kontos

Um eine Verbindung zu Platform herzustellen, müssen Sie zunächst die Interoperabilität für Ihr [!DNL Google Cloud Storage]-Konto aktivieren. Um auf die Interoperabilitätseinstellung zuzugreifen, öffnen Sie [!DNL Google Cloud Platform] und wählen Sie **[!UICONTROL Einstellungen]** aus der Option **[!UICONTROL Cloud-Speicher]** im Navigationsfenster aus.

![](../../images/tutorials/create/google-cloud-storage/nav.png)

Die Seite **[!UICONTROL Einstellungen]** wird angezeigt. Von hier aus können Sie Informationen zu Ihrer [!DNL Google] Projekt-ID und Details zu Ihrem [!DNL Google Cloud Storage]-Konto sehen. Um auf die Interoperabilitätseinstellungen zuzugreifen, wählen Sie **[!UICONTROL Interoperabilität]** in der oberen Kopfzeile aus.

![](../../images/tutorials/create/google-cloud-storage/project-access.png)

Die Seite **[!UICONTROL Interoperabilität]** enthält Informationen zur Authentifizierung, zu Zugriffsschlüsseln und zum Standardprojekt, das mit Ihrem Dienstkonto verknüpft ist. Um eine neue Zugriffsschlüssel-ID und einen geheimen Zugriffsschlüssel für Ihr Dienstkonto zu generieren, wählen Sie **[!UICONTROL Einen Schlüssel für ein Dienstkonto erstellen]**.

![](../../images/tutorials/create/google-cloud-storage/interoperability.png)

Sie können Ihre neu generierte Zugriffsschlüssel-ID und den geheimen Zugriffsschlüssel verwenden, um Ihr [!DNL Google Cloud Storage]-Konto mit Platform zu verbinden.

## Namensbeschränkungen für Dateien und Ordner

Im Folgenden finden Sie eine Liste von Einschränkungen, die Sie beim Benennen Ihrer Cloud-Speicherdatei oder Ihres Verzeichnisses berücksichtigen müssen.

- Die Namen von Verzeichnis- und Dateikomponenten dürfen 255 Zeichen nicht überschreiten.
- Verzeichnis- und Dateinamen können nicht mit einem Schrägstrich (`/`) enden. Wenn angegeben, wird sie automatisch entfernt.
- Die folgenden Zeichen der reservierten URL müssen ordnungsgemäß maskiert sein: `! ' ( ) ; @ & = + $ , % # [ ]`
- Die folgenden Zeichen sind nicht zulässig: `" \ / : | < > * ?`.
- Unzulässige URL-Pfadzeichen sind nicht zulässig. Codepunkte wie `\uE000` sind zwar in NTFS-Dateinamen gültig, aber keine gültigen Unicode-Zeichen. Darüber hinaus sind einige ASCII- oder Unicode-Zeichen, wie Steuerzeichen (0x00 bis 0x1F, \u0081 usw.), ebenfalls nicht zulässig. Regeln für Unicode-Zeichenfolgen in HTTP/1.1 finden Sie in [RFC 2616, Abschnitt 2.2: Grundregeln](https://www.ietf.org/rfc/rfc2616.txt) und [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Die folgenden Dateinamen sind nicht zulässig: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, PRN, AUX, NUL, CON, CLOCK$, Punkt (..) und zwei Zeichen (..).

## Verbinden von [!DNL Google Cloud Storage] mit Platform

Die folgende Dokumentation enthält Informationen dazu, wie Sie mithilfe von APIs oder der Benutzeroberfläche eine Verbindung von [!DNL Google Cloud Storage] mit Platform herstellen:

### Verwenden von APIs

- [Erstellen einer Basisverbindung für Google Cloud Storage mithilfe der Flow Service-API](../../tutorials/api/create/cloud-storage/google.md)
- [Datenstruktur und Inhalt einer Cloud-Speicherquelle mithilfe der Flow Service-API durchsuchen](../../tutorials/api/explore/cloud-storage.md)
- [Erstellen eines Datenflusses für eine Cloud-Speicherquelle mithilfe der Flow Service-API](../../tutorials/api/collect/cloud-storage.md)

### Verwenden der UI

- [Erstellen einer Quellverbindung für Google Cloud Storage über die Benutzeroberfläche](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [Erstellen eines Datenflusses für eine Cloud-Speicherverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/batch/cloud-storage.md)
