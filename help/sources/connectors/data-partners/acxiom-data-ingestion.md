---
title: Acxiom-Datenerfassung
description: Erfahren Sie, wie Sie [!DNL Acxiom] Daten an Real-time Customer Data Platform übermitteln, Erstanbieterprofile anreichern, Zielgruppen verbessern und über Marketingkanäle hinweg aktivieren.
badge: Beta
source-git-commit: 9419da451616ca7f087ecea7aa66a6c10a474fb3
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 42%

---

# [!DNL Acxiom Data Ingestion]

>[!NOTE]
>
>Die [!DNL Acxiom Prospecting Data Import]-Quelle befindet sich in der Beta-Phase. Bitte lesen Sie die [Quellen - Übersicht](../../home.md#terms-and-conditions) für weitere Informationen zur Verwendung von Beta-beschrifteten Quellen.

Verwenden Sie die [!DNL Acxiom Data Ingestion] zu erfassende Quelle [!DNL Acxiom] Daten in Real-time Customer Data Platform einlesen und Erstanbieterprofile anreichern. Anschließend können Sie Ihre [!DNL Acxiom]-erweiterte Erstanbieterprofile zur Verbesserung von Zielgruppen und zur Aktivierung über Marketingkanäle hinweg.

![acxiom-data-ingestion-workflow](../../images/tutorials/create/acxiom-data-enhancement-import/acxiom-data-ingestion.png)

Weitere Informationen zur Einrichtung der [!DNL Acxiom Data Ingestion] Quellkonto.

## Voraussetzungen {#prerequisites}

Um Ihre [!DNL Acxiom Data Ingestion] -Konto auf Experience Platform angegeben haben, müssen Sie Werte für die folgenden Authentifizierungsberechtigungen angeben:

| Anmeldedaten | Beschreibung |
| --- | --- |
| [!DNL Acxiom] Authentifizierungsschlüssel | Der Authentifizierungsschlüssel. Sie können diesen Wert aus dem [!DNL Acxiom] Team. |
| [!DNL Amazon S3] Zugriffsschlüssel | Die Zugriffsschlüssel-ID für Ihren Behälter. Sie können diesen Wert aus dem [!DNL Acxiom] Team. |
| Geheimer [!DNL Amazon S3]-Schlüssel | Die geheime Schlüssel-ID für Ihren Bucket. Sie können diesen Wert aus dem [!DNL Acxiom] Team. |
| Behältername | Dies ist Ihr Bucket, in dem Dateien freigegeben werden. Sie können diesen Wert aus dem [!DNL Acxiom] Team. |

## IP-Adressen-Zulassungsliste

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Performance-Einbußen führen. Weitere Information finden Sie unter [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md).

### Berechtigungen auf Experience Platform konfigurieren

Sie müssen beide **[!UICONTROL Quellen anzeigen]** und **[!UICONTROL Quellen verwalten]** für Ihr Konto aktivierte Berechtigungen, um Ihre [!DNL Acxiom Data Ingestion] -Konto auf Experience Platform. Wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten. Weitere Informationen finden Sie im Abschnitt [UI-Handbuch zur Zugriffskontrolle](../../../access-control/ui/overview.md).

### Namensbeschränkungen für Dateien und Verzeichnisse

Die unten aufgeführten Einschränkungen müssen bei der Benennung Ihrer Cloud-Speicherdatei oder des -Ordners berücksichtigt werden:

- Die Namen von Verzeichnis- und Dateikomponenten dürfen nicht länger als 255 Zeichen sein.
- Verzeichnis- und Dateinamen dürfen nicht mit einem Schrägstrich (`/`) enden. Wenn angegeben, wird er automatisch entfernt.
- Die folgenden Zeichen der reservierten URL müssen ordnungsgemäß maskiert sein: `! ' ( ) ; @ & = + $ , % # [ ]`
- Die folgenden Zeichen sind nicht zulässig: `" \ / : | < > * ?`.
- Unzulässige URL-Pfadzeichen sind nicht zulässig. Code-Punkte wie `\uE000` sind zwar in NTFS-Dateinamen gültig, aber keine gültigen Unicode-Zeichen. Darüber hinaus sind einige ASCII- oder Unicode-Zeichen wie Steuerzeichen (0x00 bis 0x1F, \u0081 usw.) ebenfalls nicht zulässig. Regeln für Unicode-Zeichenfolgen in HTTP/1.1 finden Sie unter [RFC 2616, Abschnitt 2.2: Grundregeln](https://www.ietf.org/rfc/rfc2616.txt) und [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Die folgenden Dateinamen sind nicht zulässig: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, Punktzeichen (.) und zwei Punktzeichen (..).

## Nächste Schritte

Durch Lesen dieses Dokuments haben Sie die erforderliche Einrichtung abgeschlossen, um Daten von Ihrem [!DNL Acxiom] -Konto auf Experience Platform. Sie können jetzt mit dem Handbuch zu [Verbindung [!DNL Acxiom Data Ingestion] zum Experience Platform über die Benutzeroberfläche](../../tutorials/ui/create/data-partners/acxiom-data-ingestion.md).
