---
title: Übersicht über die Merkury Enterprise Identity Resolution Source
description: Erfahren Sie, wie Sie die Merkury Enterprise Identity Resolution über die Benutzeroberfläche mit Adobe Experience Platform verbinden.
exl-id: c5eaa561-d620-4c82-bce1-972d0a422c3f
source-git-commit: e402a58f51de49b26f9d279cebf551ec11e4698f
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 34%

---

# [!DNL Merkury Enterprise Identity Resolution]

Adobe Experience Platform unterstützt die Aufnahme von Daten aus einer Datenpartneranwendung. Unterstützung für Datenpartner umfasst [!DNL Merkury Enterprise Identity Resolution].

Sie können [!DNL Merkury] nutzen, [!DNL Merkle] mehr digitale Besucher zu erkennen - auch ohne die Verwendung von Cookies - und die relevanten und personalisierten Erlebnisse bereitzustellen, die Ihre Kunden benötigen.

Sie können die **Personen-ID** als Teil der [!DNL Merkury] nutzen, um alles, was Ihr Unternehmen über eine Person weiß, zu einem einzigen, umfassenden Profil zu kombinieren. Zu diesen Details können gehören:

- Digitale Verhaltensweisen
- Kaufpräferenzen
- Identifizierungsinformationen wie Name, E-Mail-Adresse, physische Adresse oder Geräte-ID.

Sie können aufgenommene Daten als Experience-Datenmodell (XDM), JSON, XDM Parquet oder mit Trennzeichen formatieren. Jeder Schritt des Prozesses wird in die Arbeitsquellen integriert

![Abbildung des Datenverarbeitungs-Workflows für die Merkury-Quelle.](../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/architecture.png)

## Zulassungsliste von IP-Adressen

Bevor Sie Quell-Connectoren verwenden können, müssen Sie die erforderlichen IP-Adressen für Ihre Region zu Ihrer Zulassungsliste hinzufügen. Wenn Sie diese IP-Adressen nicht hinzufügen, funktionieren die Quell-Connectoren möglicherweise nicht ordnungsgemäß oder es treten Fehler auf. Auf die Zulassungsliste setzen Detaillierte Anweisungen und die Liste der zuzulassenden IP-Adressen finden Sie auf der Seite [IP-Adresse](../../ip-address-allow-list.md) .

## Namensbeschränkungen für Dateien und Verzeichnisse

Im Folgenden finden Sie eine Liste von Einschränkungen, die Sie beim Benennen Ihrer Cloud-Speicherdatei oder Ihres Verzeichnisses berücksichtigen müssen.

- Die Namen von Verzeichnis- und Dateikomponenten dürfen nicht länger als 255 Zeichen sein.
- Verzeichnis- und Dateinamen dürfen nicht mit einem Schrägstrich (`/`) enden. Wenn angegeben, wird er automatisch entfernt.
- Die folgenden Zeichen der reservierten URL müssen ordnungsgemäß maskiert sein: `! ' ( ) ; @ & = + $ , % # [ ]`
- Die folgenden Zeichen sind nicht zulässig: `" \ / : | < > * ?`.
- Unzulässige URL-Pfadzeichen sind nicht zulässig. Code-Punkte wie `\uE000` sind zwar in NTFS-Dateinamen gültig, aber keine gültigen Unicode-Zeichen. Darüber hinaus sind einige ASCII- oder Unicode-Zeichen wie Steuerzeichen (0x00 bis 0x1F, \u0081 usw.) ebenfalls nicht zulässig. Regeln für Unicode-Zeichenfolgen in HTTP/1.1 finden Sie unter [RFC 2616, Abschnitt 2.2: Grundregeln](https://www.ietf.org/rfc/rfc2616.txt) und [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Die folgenden Dateinamen sind nicht zulässig: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, Punktzeichen (.) und zwei Punktzeichen (..).

## Voraussetzungen

Sie müssen die folgenden Voraussetzungen erfüllen, bevor Sie mit der Verwendung der [!DNL Merkury] beginnen können:

- Sie müssen die [!DNL Merkury]-Einrichtung mit Ihrem [!DNL Merkury]-Team abschließen.
- Sie müssen Ihre Anmeldeinformationen (Zugriffsschlüssel, geheimer Schlüssel und Behältername) von Ihrem [!DNL Merkury]-Team abrufen. 

>[!NOTE]
>
>Ein Dateipfad wie `myBucket/folder/subfolder/subsubfolder/abc.csv` kann dazu führen, dass Sie nur auf `subsubfolder/abc.csv` zugreifen. Wenn Sie auf den Unterordner zugreifen möchten, können Sie den Bucket-Parameter als myBucket und den folderPath als Ordner/Unterordner angeben, um sicherzustellen, dass die Dateiexploration beim Unterordner beginnt und nicht beim `subsubfolder/abc.csv`.

## Nächste Schritte

Durch Lesen dieses Dokuments haben Sie die erforderliche Einrichtung abgeschlossen, um Daten aus Ihrem [!DNL Merkury]-Konto in Experience Platform zu übertragen. Sie können jetzt mit dem Handbuch unter [Verbinden [!DNL Merkury]  mit Experience Platform über die Benutzeroberfläche ](../../tutorials/ui/create/data-partners/merkury.md).
