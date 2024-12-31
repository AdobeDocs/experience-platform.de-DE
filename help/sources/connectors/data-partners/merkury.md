---
title: Übersicht über die Merkury Enterprise Identity Resolution Source
description: Erfahren Sie, wie Sie die Merkury Enterprise Identity Resolution über die Benutzeroberfläche mit Adobe Experience Platform verbinden.
last-substantial-update: 2023-12-12T00:00:00Z
badge: Beta
exl-id: c5eaa561-d620-4c82-bce1-972d0a422c3f
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 44%

---

# [!DNL Merkury Enterprise Identity Resolution]

>[!NOTE]
>
>Die [!DNL Merkury Enterprise Identity Resolution]-Quelle befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta[gekennzeichneten Quellen finden Sie ](../../home.md#terms-and-conditions) „Quellen - Übersicht“.

Adobe Experience Platform unterstützt die Aufnahme von Daten aus einer Datenpartneranwendung. Unterstützung für Datenpartner umfasst [!DNL Merkury Enterprise Identity Resolution].

Sie können [!DNL Merkury] nutzen, [!DNL Merkle] mehr digitale Besucher zu erkennen - auch ohne die Verwendung von Cookies - und die relevanten und personalisierten Erlebnisse bereitzustellen, die Ihre Kunden benötigen.

Sie können die **Personen-ID** als Teil der [!DNL Merkury] nutzen, um alles, was Ihr Unternehmen über eine Person weiß, zu einem einzigen, umfassenden Profil zu kombinieren. Zu diesen Details können gehören:

- Digitale Verhaltensweisen
- Kaufpräferenzen
- Identifizierungsinformationen wie Name, E-Mail-Adresse, physische Adresse oder Geräte-ID.

Sie können aufgenommene Daten als Experience-Datenmodell (XDM), JSON, XDM Parquet oder mit Trennzeichen formatieren. Jeder Schritt des Prozesses wird in die Arbeitsquellen integriert

![Abbildung des Datenverarbeitungs-Workflows für die Merkury-Quelle.](../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/architecture.png)

## IP-Adressen-Zulassungsliste

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Performance-Einbußen führen. Weitere Information finden Sie unter [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md).

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

Durch Lesen dieses Dokuments haben Sie die erforderliche Einrichtung abgeschlossen, um Daten aus Ihrem [!DNL Merkury]-Konto auf Experience Platform zu übertragen. Sie können jetzt mit dem Handbuch unter [Verbinden [!DNL Merkury] Experience Platform über die Benutzeroberfläche fortfahren](../../tutorials/ui/create/data-partners/merkury.md).
