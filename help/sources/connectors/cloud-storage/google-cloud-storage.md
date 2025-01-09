---
keywords: Experience Platform;Startseite;beliebte Themen;Google Cloud Storage;Google Cloud Storage
solution: Experience Platform
title: Übersicht über den Google Cloud Storage Source Connector
description: Erfahren Sie, wie Sie den Google Cloud-Speicher mithilfe von APIs oder der Benutzeroberfläche mit Adobe Experience Platform verbinden.
exl-id: f7ebd213-f914-4c49-aebd-1df4514ffec0
source-git-commit: ee659ded9701132b12d5b93672b4c958e9720028
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 72%

---

# Google Cloud Storage-Connector

>[!IMPORTANT]
>
>Sie können jetzt die [!DNL Google Cloud Storage]-Quelle verwenden, wenn Sie Adobe Experience Platform auf Amazon Web Services (AWS) ausführen. Experience Platform, das auf AWS ausgeführt wird, steht derzeit einer begrenzten Anzahl von Kunden zur Verfügung. Weitere Informationen zur unterstützten Experience Platform-Infrastruktur finden Sie in der Übersicht zur [Experience Platform-Multi-Cloud](../../../landing/multi-cloud.md).

Adobe Experience Platform bietet native Konnektivität für Cloud-Anbieter wie AWS, [!DNL Google Cloud Platform] und [!DNL Azure], sodass Sie Ihre Daten aus diesen Systemen übernehmen können.

Cloud-Speicher bieten eine Quelle, von der Sie Ihre Daten in Platform übertragen können, ohne diese herunterladen, formatieren oder hochladen zu müssen. Aufgenommene Daten können als JSON- oder Parquet-Daten formatiert werden, die mit dem Experience-Datenmodell (XDM) konform sind, oder in einem getrennten Format. Jeder Schritt des Prozesses wird in den Quell-Workflow integriert. Mit Platform können Sie Daten aus [!DNL Google Cloud Storage] durch Batches importieren.

## IP-Adressen-Zulassungsliste

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Performance-Einbußen führen. Weitere Information finden Sie unter [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md).

## Vorausgesetzte Einrichtung für das Verbinden Ihres [!DNL Google Cloud Storage]-Kontos

Um eine Verbindung von mit Platform herzustellen, müssen Sie zunächst die Interoperabilität für Ihr [!DNL Google Cloud Storage]-Konto aktivieren. Um auf die Interoperabilitätseinstellung zuzugreifen, öffnen Sie [!DNL Google Cloud Platform] und wählen Sie **[!UICONTROL Einstellungen]** in der Option **[!UICONTROL Cloud-Speicher]** im Navigationsbereich aus.

<!-- ![](../../images/tutorials/create/google-cloud-storage/nav.png) -->

Die Seite **[!UICONTROL Einstellungen]** wird angezeigt. Von hier aus können Sie Informationen zu Ihrer [!DNL Google]-Projekt-ID und Details zu Ihrem [!DNL Google Cloud Storage]-Konto ansehen. Um auf die Interoperabilitätseinstellungen zuzugreifen, wählen Sie **[!UICONTROL Interoperabilität]** aus der oberen Kopfzeile aus.

<!-- ![](../../images/tutorials/create/google-cloud-storage/project-access.png) -->

Die Seite **[!UICONTROL Interoperabilität]** enthält Informationen zur Authentifizierung, zu Zugriffsschlüsseln und zum Standardprojekt, das mit Ihrem Service-Konto verknüpft ist. Um eine neue Zugriffsschlüssel-ID und einen geheimen Zugriffsschlüssel für Ihr Service-Konto zu generieren, wählen Sie **[!UICONTROL Schlüssel für ein Service-Konto erstellen]** aus.

<!-- ![](../../images/tutorials/create/google-cloud-storage/interoperability.png) -->

Sie können die neu generierte Zugriffsschlüssel-ID und den geheimen Zugriffsschlüssel verwenden, um Ihr [!DNL Google Cloud Storage]-Konto mit Platform zu verbinden.

Weitere Informationen finden Sie im Handbuch unter [Erstellen und Verwalten von Service-Kontoschlüsseln](https://cloud.google.com/iam/docs/creating-managing-service-account-keys) in der [!DNL Google Cloud].

## Namensbeschränkungen für Dateien und Verzeichnisse

Im Folgenden finden Sie eine Liste von Einschränkungen, die Sie beim Benennen Ihrer Cloud-Speicherdatei oder Ihres Verzeichnisses berücksichtigen müssen.

- Die Namen von Verzeichnis- und Dateikomponenten dürfen nicht länger als 255 Zeichen sein.
- Verzeichnis- und Dateinamen dürfen nicht mit einem Schrägstrich (`/`) enden. Wenn angegeben, wird er automatisch entfernt.
- Die folgenden Zeichen der reservierten URL müssen ordnungsgemäß maskiert sein: `! ' ( ) ; @ & = + $ , % # [ ]`
- Die folgenden Zeichen sind nicht zulässig: `" \ / : | < > * ?`.
- Unzulässige URL-Pfadzeichen sind nicht zulässig. Code-Punkte wie `\uE000` sind zwar in NTFS-Dateinamen gültig, aber keine gültigen Unicode-Zeichen. Darüber hinaus sind einige ASCII- oder Unicode-Zeichen wie Steuerzeichen (0x00 bis 0x1F, \u0081 usw.) ebenfalls nicht zulässig. Regeln für Unicode-Zeichenfolgen in HTTP/1.1 finden Sie unter [RFC 2616, Abschnitt 2.2: Grundregeln](https://www.ietf.org/rfc/rfc2616.txt) und [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Die folgenden Dateinamen sind nicht zulässig: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, Punktzeichen (.) und zwei Punktzeichen (..).

## Verbinden von [!DNL Google Cloud Storage] mit Platform

Die folgende Dokumentation enthält Informationen dazu, wie Sie [!DNL Google Cloud Storage] mithilfe von APIs oder der Benutzeroberfläche mit Platform verbinden können:

### Verwenden von APIs

- [Erstellen einer Google Cloud Storage-Basisverbindung mithilfe der Flow Service-API](../../tutorials/api/create/cloud-storage/google.md)
- [Untersuchen der Datenstruktur und des Inhalts einer Cloud-Speicherquelle mit der Flow Service-API](../../tutorials/api/explore/cloud-storage.md)
- [Erstellen eines Datenflusses für eine Cloud-Speicherquelle mithilfe der Flow Service-API](../../tutorials/api/collect/cloud-storage.md)

### Verwenden der Benutzeroberfläche

- [Erstellen einer Google Cloud Storage-Quellverbindung über die Benutzeroberfläche](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [Erstellen eines Datenflusses für eine Cloud-Speicherverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/batch/cloud-storage.md)
