---
keywords: Experience Platform;Home;beliebte Themen
solution: Experience Platform
title: Datenquelle der Einstiegszone
topic-legacy: overview
description: Erfahren Sie, wie Sie die Einstiegszone für Daten mit Adobe Experience Platform verbinden.
exl-id: bdc10095-7de4-4183-bfad-a7b5c89197e3
source-git-commit: 57089cc9aa9c586f5fae70e2a7154d48ebd62447
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 4%

---

# [!DNL Data Landing Zone]

[!DNL Data Landing Zone] ist eine von Adobe Experience Platform bereitgestellte  [!DNL Azure Blob] Speicherschnittstelle, über die Sie auf eine sichere, Cloud-basierte Dateispeicheranlage zugreifen können, über die Dateien in Platform geladen werden können. Sie haben Zugriff auf einen [!DNL Data Landing Zone]-Container pro Sandbox, und das Datenvolumen insgesamt über alle Container hinweg ist auf die Gesamtdaten beschränkt, die mit Ihrer Platform Produces and Services-Lizenz bereitgestellt werden. Alle Kunden von Platform und deren Anwendungsdiensten wie [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services] und [!DNL Real-time Customer Data Platform] werden mit einem [!DNL Data Landing Zone]-Container pro Sandbox bereitgestellt. Sie können Dateien in Ihren Container über [!DNL Azure Storage Explorer] oder Ihre Befehlszeilenschnittstelle lesen und schreiben.

[!DNL Data Landing Zone] unterstützt die SAS-basierte Authentifizierung und ihre Daten sind durch standardmäßige  [!DNL Azure Blob] Speichersicherheitsmechanismen im Ruhezustand und während der Übertragung geschützt. Mit der SAS-basierten Authentifizierung können Sie über eine öffentliche Internetverbindung sicher auf Ihren [!DNL Data Landing Zone]-Container zugreifen. Es sind keine Netzwerkänderungen erforderlich, damit Sie auf Ihren [!DNL Data Landing Zone]-Container zugreifen können. Dies bedeutet, dass Sie keine Zulassungslisten oder regionenübergreifenden Setups für Ihr Netzwerk konfigurieren müssen. Platform erzwingt für alle Dateien, die in einen [!DNL Data Landing Zone]-Container hochgeladen werden, eine strikte TTL (sieben Tage lang). Alle Dateien werden nach sieben Tagen gelöscht.

## Namensbeschränkungen für Dateien und Ordner

Im Folgenden finden Sie eine Liste von Einschränkungen, die Sie bei der Benennung Ihrer Cloud-Speicherdateien oder -Verzeichnisse berücksichtigen müssen.

- Die Namen von Verzeichnis- und Dateikomponenten dürfen 255 Zeichen nicht überschreiten.
- Verzeichnis- und Dateinamen können nicht mit einem Schrägstrich (`/`) enden. Wenn angegeben, wird sie automatisch entfernt.
- Die folgenden Zeichen der reservierten URL müssen ordnungsgemäß maskiert sein: `! ' ( ) ; @ & = + $ , % # [ ]`
- Die folgenden Zeichen sind nicht zulässig: `" \ / : | < > * ?`.
- Unzulässige URL-Pfadzeichen sind nicht zulässig. Codepunkte wie `\uE000` sind zwar in NTFS-Dateinamen gültig, aber keine gültigen Unicode-Zeichen. Darüber hinaus sind einige ASCII- oder Unicode-Zeichen, wie Steuerzeichen (wie `0x00` bis `0x1F`, `\u0081` usw.), ebenfalls nicht zulässig. Regeln für Unicode-Zeichenfolgen in HTTP/1.1 finden Sie in [RFC 2616, Abschnitt 2.2: Grundregeln](https://www.ietf.org/rfc/rfc2616.txt) und [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Die folgenden Dateinamen sind nicht zulässig: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, PRN, AUX, NUL, CON, CLOCK$, Punkt (..) und zwei Zeichen (..).

## Verbinden Sie [!DNL Data Landing Zone] mit [!DNL Platform]

Die folgende Dokumentation enthält Informationen dazu, wie Sie Daten aus Ihrem [!DNL Data Landing Zone]-Container mit APIs oder der Benutzeroberfläche in Adobe Experience Platform importieren können.

### Verwenden von APIs

- [Erstellen einer Quellverbindung [!DNL Data Landing Zone] mithilfe der Flow Service-API](../../tutorials/api/create/cloud-storage/data-landing-zone.md)
- [Erstellen eines Datenflusses für eine Cloud-Speicherquelle mithilfe der Flow Service-API](../../tutorials/api/collect/cloud-storage.md)

### Verwenden der UI

- [Verbinden [!DNL Data Landing Zone] mit Platform über die Benutzeroberfläche](../../tutorials/ui/create/cloud-storage/data-landing-zone.md)
- [Erstellen eines Datenflusses für eine Cloud-Speicherverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/batch/cloud-storage.md)
