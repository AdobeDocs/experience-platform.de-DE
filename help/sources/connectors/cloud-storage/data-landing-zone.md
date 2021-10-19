---
keywords: Experience Platform;Home;beliebte Themen
solution: Experience Platform
title: Datenquelle der Einstiegszone
topic-legacy: overview
description: Erfahren Sie, wie Sie die Einstiegszone für Daten mit Adobe Experience Platform verbinden.
exl-id: bdc10095-7de4-4183-bfad-a7b5c89197e3
source-git-commit: ecc9bc603bfd7b56f5f232b0d6d91eb65a901510
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 4%

---

# [!DNL Data Landing Zone]

[!DNL Data Landing Zone] ist [!DNL Azure Blob] von Adobe Experience Platform bereitgestellte Speicherschnittstelle, über die Sie auf eine sichere, Cloud-basierte Dateispeichereinrichtung zugreifen können, um Dateien in Platform zu laden. Sie haben Zugriff auf eine [!DNL Data Landing Zone] Behälter pro Sandbox und das gesamte Datenvolumen über alle Container hinweg ist auf die Gesamtdaten beschränkt, die mit Ihrer Platform-Produkte- und -Services-Lizenz bereitgestellt werden. Alle Kunden von Platform und die zugehörigen Anwendungsdienste wie [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services]und [!DNL Real-time Customer Data Platform] mit einem [!DNL Data Landing Zone] Container pro Sandbox. Sie können Dateien in Ihren Container lesen und schreiben, indem Sie [!DNL Azure Storage Explorer] oder der Befehlszeilenschnittstelle.

[!DNL Data Landing Zone] unterstützt die SAS-basierte Authentifizierung und die Daten sind durch Standard geschützt [!DNL Azure Blob] Sicherheitsmechanismen für die Lagerung im Ruhezustand und im Transit. Mit der SAS-basierten Authentifizierung können Sie sicher auf Ihre [!DNL Data Landing Zone] Container über eine öffentliche Internetverbindung. Es sind keine Netzwerkänderungen erforderlich, damit Sie auf Ihre [!DNL Data Landing Zone] -Container verwenden, müssen Sie also keine Zulassungslisten oder regionenübergreifenden Setups für Ihr Netzwerk konfigurieren. Platform erzwingt für alle Dateien, die in eine [!DNL Data Landing Zone] Container. Alle Dateien werden nach sieben Tagen gelöscht.

## Namensbeschränkungen für Dateien und Ordner

Im Folgenden finden Sie eine Liste von Einschränkungen, die Sie bei der Benennung Ihrer Cloud-Speicherdateien oder -Verzeichnisse berücksichtigen müssen.

- Die Namen von Verzeichnis- und Dateikomponenten dürfen 255 Zeichen nicht überschreiten.
- Verzeichnis- und Dateinamen können nicht mit einem Schrägstrich (`/`). Wenn angegeben, wird sie automatisch entfernt.
- Die folgenden Zeichen der reservierten URL müssen ordnungsgemäß maskiert sein: `! ' ( ) ; @ & = + $ , % # [ ]`
- Die folgenden Zeichen sind nicht zulässig: `" \ / : | < > * ?`.
- Unzulässige URL-Pfadzeichen sind nicht zulässig. Codepunkte wie `\uE000`, obwohl in NTFS-Dateinamen gültig, sind keine gültigen Unicode-Zeichen. Darüber hinaus werden einige ASCII- oder Unicode-Zeichen, wie Steuerzeichen (wie `0x00` nach `0x1F`, `\u0081`usw.), sind ebenfalls nicht zulässig. Regeln für Unicode-Zeichenfolgen in HTTP/1.1 finden Sie unter [RFC 2616, Abschnitt 2.2: Grundlegende Regeln](https://www.ietf.org/rfc/rfc2616.txt) und [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Die folgenden Dateinamen sind nicht zulässig: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, PRN, AUX, NUL, CON, CLOCK$, Punkt (..) und zwei Zeichen (..).

## Verbinden [!DNL Data Landing Zone] nach [!DNL Platform]

Die nachstehende Dokumentation enthält Informationen zum Datenimport von [!DNL Data Landing Zone] -Container mit Adobe Experience Platform mithilfe von APIs oder der Benutzeroberfläche erstellen.

### Verwenden von APIs

- [Erstellen Sie eine [!DNL Data Landing Zone] Quellverbindung mit der Flow Service-API](../../tutorials/api/create/cloud-storage/data-landing-zone.md)
- [Erstellen eines Datenflusses für eine Cloud-Speicherquelle mithilfe der Flow Service-API](../../tutorials/api/collect/cloud-storage.md)

### Verwenden der UI

- [Verbinden [!DNL Data Landing Zone] zur Plattform mithilfe der Benutzeroberfläche](../../tutorials/ui/create/cloud-storage/data-landing-zone.md)
- [Erstellen eines Datenflusses für eine Cloud-Speicherverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/batch/cloud-storage.md)
