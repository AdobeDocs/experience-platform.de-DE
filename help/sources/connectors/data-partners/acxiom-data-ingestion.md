---
title: Acxiom-Datenaufnahme
description: Erfahren Sie, wie  [!DNL Acxiom]  Daten in Real-Time Customer Data Platform aufnehmen, Erstanbieterprofile anreichern, Zielgruppen verbessern und über Marketing-Kanäle hinweg aktivieren können.
exl-id: 3bbbe4e1-5e34-4104-bf39-2c452865b807
source-git-commit: e402a58f51de49b26f9d279cebf551ec11e4698f
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 32%

---

# [!DNL Acxiom Data Ingestion]

Verwenden Sie die [!DNL Acxiom Data Ingestion], um [!DNL Acxiom] in Real-Time Customer Data Platform aufzunehmen und Erstanbieterprofile anzureichern. Anschließend können Sie Ihre mit [!DNL Acxiom] angereicherten First-Party-Profile verwenden, um Zielgruppen zu verbessern und über Marketing-Kanäle hinweg zu aktivieren.

![acxiom-data-gestion-workflow](../../images/tutorials/create/acxiom-data-enhancement-import/acxiom-data-ingestion.png)

Lesen Sie das folgende Dokument, um Informationen zum Einrichten Ihres [!DNL Acxiom Data Ingestion]-Quellkontos zu erhalten.

## Voraussetzungen {#prerequisites}

Um Ihr [!DNL Acxiom Data Ingestion]-Konto mit Experience Platform zu verbinden, müssen Sie Werte für die folgenden Authentifizierungsdaten angeben:

| Anmeldedaten | Beschreibung |
| --- | --- |
| [!DNL Acxiom] Authentifizierungsschlüssel | Der Authentifizierungsschlüssel. Sie können diesen Wert vom [!DNL Acxiom]-Team abrufen. |
| [!DNL Amazon S3] Zugriffsschlüssel | Die Zugriffsschlüssel-ID für Ihren Bucket. Sie können diesen Wert vom [!DNL Acxiom]-Team abrufen. |
| Geheimer [!DNL Amazon S3]-Schlüssel | Die geheime Schlüssel-ID für Ihren Bucket. Sie können diesen Wert vom [!DNL Acxiom]-Team abrufen. |
| Behältername | Dies ist der Bucket, in dem Dateien freigegeben werden. Sie können diesen Wert vom [!DNL Acxiom]-Team abrufen. |

## Zulassungsliste von IP-Adressen

Bevor Sie Quell-Connectoren verwenden können, müssen Sie die erforderlichen IP-Adressen für Ihre Region zu Ihrer Zulassungsliste hinzufügen. Wenn Sie diese IP-Adressen nicht hinzufügen, funktionieren die Quell-Connectoren möglicherweise nicht ordnungsgemäß oder es treten Fehler auf. Auf die Zulassungsliste setzen Detaillierte Anweisungen und die Liste der zuzulassenden IP-Adressen finden Sie auf der Seite [IP-Adresse](../../ip-address-allow-list.md) .

### Konfigurieren von Berechtigungen für Experience Platform

Sie müssen sowohl **[!UICONTROL Quellen anzeigen]** als auch **[!UICONTROL Quellen verwalten]** für Ihr Konto aktiviert haben, um Ihr [!DNL Acxiom Data Ingestion]-Konto mit Experience Platform zu verbinden. Wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten. Weitere Informationen finden Sie im [Handbuch zur Benutzeroberfläche der Zugriffssteuerung](../../../access-control/ui/overview.md).

### Namensbeschränkungen für Dateien und Verzeichnisse

Beachten Sie die folgenden Einschränkungen beim Benennen Ihrer Cloud-Speicherdatei oder Ihres Verzeichnisses:

- Die Namen von Verzeichnis- und Dateikomponenten dürfen nicht länger als 255 Zeichen sein.
- Verzeichnis- und Dateinamen dürfen nicht mit einem Schrägstrich (`/`) enden. Wenn angegeben, wird er automatisch entfernt.
- Die folgenden Zeichen der reservierten URL müssen ordnungsgemäß maskiert sein: `! ' ( ) ; @ & = + $ , % # [ ]`
- Die folgenden Zeichen sind nicht zulässig: `" \ / : | < > * ?`.
- Unzulässige URL-Pfadzeichen sind nicht zulässig. Code-Punkte wie `\uE000` sind zwar in NTFS-Dateinamen gültig, aber keine gültigen Unicode-Zeichen. Darüber hinaus sind einige ASCII- oder Unicode-Zeichen wie Steuerzeichen (0x00 bis 0x1F, \u0081 usw.) ebenfalls nicht zulässig. Regeln für Unicode-Zeichenfolgen in HTTP/1.1 finden Sie unter [RFC 2616, Abschnitt 2.2: Grundregeln](https://www.ietf.org/rfc/rfc2616.txt) und [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Die folgenden Dateinamen sind nicht zulässig: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, Punktzeichen (.) und zwei Punktzeichen (..).

## Nächste Schritte

Durch Lesen dieses Dokuments haben Sie die erforderliche Einrichtung abgeschlossen, um Daten von Ihrem [!DNL Acxiom]-Konto in Experience Platform zu übertragen. Sie können jetzt mit dem Handbuch unter [Verbinden [!DNL Acxiom Data Ingestion]  mit Experience Platform über die Benutzeroberfläche ](../../tutorials/ui/create/data-partners/acxiom-data-ingestion.md).
