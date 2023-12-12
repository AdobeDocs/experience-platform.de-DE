---
title: Merkur Enterprise Identity Resolution Quelle Übersicht
description: Erfahren Sie, wie Sie mithilfe der Benutzeroberfläche die Enterprise Identity-Auflösung von Merkury mit Adobe Experience Platform verbinden.
last-substantial-update: 2023-12=12
badge: Beta
source-git-commit: d862a53c7a8880e86648c05cf94e37e1a1779c9e
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 44%

---

# [!DNL Merkury Enterprise Identity Resolution]

>[!NOTE]
>
>Die [!DNL Merkury Enterprise Identity Resolution]-Quelle befindet sich in der Beta-Phase. Bitte lesen Sie die [Quellen - Übersicht](../../home.md#terms-and-conditions) für weitere Informationen zur Verwendung von Beta-beschrifteten Quellen.

Adobe Experience Platform unterstützt die Aufnahme von Daten aus einer Datenpartner-Anwendung. Unterstützung für Datenpartner umfasst [!DNL Merkury Enterprise Identity Resolution].

Sie können [!DNL Merkury] von [!DNL Merkle] um mehr digitale Besucher zu erkennen - auch ohne Cookies - und die relevanten und personalisierten Erlebnisse bereitzustellen, die Ihre Kunden benötigen.

Sie können die **Personen-ID** als Teil der [!DNL Merkury] -Quelle, um alles, was Ihr Unternehmen über eine Person weiß, in einem einzigen umfassenden Profil zusammenzuführen. Diese Details können Folgendes umfassen:

- digitales Verhalten
- Kaufpräferenzen
- Identifizierungsinformationen wie Name, E-Mail-Adresse, physische Adresse oder Geräte-ID.

Sie können aufgenommene Daten als Experience-Datenmodell (XDM)-JSON, XDM-Parquet oder als durch Trennzeichen getrennte formatieren. Jeder Schritt des Prozesses ist in die Quellarbeit integriert

![Eine Abbildung des Datenverarbeitungs-Workflows für die Merkury-Quelle.](../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/architecture.png)

## IP-Adressen-Zulassungsliste

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Leistungseinbußen führen. Weitere Information finden Sie unter [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md).

## Namensbeschränkungen für Dateien und Verzeichnisse

Im Folgenden finden Sie eine Liste von Einschränkungen, die Sie beim Benennen Ihrer Cloud-Speicherdatei oder Ihres Verzeichnisses berücksichtigen müssen.

- Die Namen von Verzeichnis- und Dateikomponenten dürfen nicht länger als 255 Zeichen sein.
- Verzeichnis- und Dateinamen dürfen nicht mit einem Schrägstrich (`/`) enden. Wenn angegeben, wird er automatisch entfernt.
- Die folgenden Zeichen der reservierten URL müssen ordnungsgemäß maskiert sein: `! ' ( ) ; @ & = + $ , % # [ ]`
- Die folgenden Zeichen sind nicht zulässig: `" \ / : | < > * ?`.
- Unzulässige URL-Pfadzeichen sind nicht zulässig. Code-Punkte wie `\uE000` sind zwar in NTFS-Dateinamen gültig, aber keine gültigen Unicode-Zeichen. Darüber hinaus sind einige ASCII- oder Unicode-Zeichen wie Steuerzeichen (0x00 bis 0x1F, \u0081 usw.) ebenfalls nicht zulässig. Regeln für Unicode-Zeichenfolgen in HTTP/1.1 finden Sie unter [RFC 2616, Abschnitt 2.2: Grundregeln](https://www.ietf.org/rfc/rfc2616.txt) und [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Die folgenden Dateinamen sind nicht zulässig: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, Punktzeichen (.) und zwei Punktzeichen (..).

## Voraussetzungen

Sie müssen die folgenden Voraussetzungen erfüllen, bevor Sie mit der Verwendung des [!DNL Merkury] source:

- Sie müssen Ihre [!DNL Merkury] -Einstellungen [!DNL Merkury] Team.
- Sie müssen Ihre Anmeldeinformationen (Zugriffsschlüssel, geheimer Schlüssel und Bucket-Name) aus Ihrem [!DNL Merkury] Team. 

>[!NOTE]
>
>Ein Dateipfad wie `myBucket/folder/subfolder/subsubfolder/abc.csv` kann nur den Zugriff ermöglichen `subsubfolder/abc.csv`. Wenn Sie auf den Unterordner zugreifen möchten, können Sie den Behälterparameter als myBucket und den OrdnerPath als Ordner/Unterordner angeben, um sicherzustellen, dass die Dateierforschung im Unterordner beginnt, anstatt `subsubfolder/abc.csv`.

## Nächste Schritte

Durch Lesen dieses Dokuments haben Sie die erforderliche Einrichtung abgeschlossen, um Daten von Ihrer [!DNL Merkury] -Konto auf Experience Platform. Sie können jetzt mit dem Handbuch zu [Verbindung [!DNL Merkury] zum Experience Platform über die Benutzeroberfläche](../../tutorials/ui/create/data-partners/merkury.md).
