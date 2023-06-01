---
keywords: E-Mail; E-Mail; E-Mail; E-Mail-Ziele; oracle responsys-Ziel
title: Oracle Responsys-Verbindung
description: Responsys ist ein Enterprise-E-Mail-Marketing-Tool für kanalübergreifende Marketing-Kampagnen, das von Oracle angeboten wird und der Personalisierung von Interaktionen über E-Mail, Mobile, Display und Social Media hinweg dient.
exl-id: 70f2f601-afee-4315-bf7a-ed2c92397ebe
source-git-commit: 47e0dfb59edca58e205cb478e9ee624659753ab9
workflow-type: tm+mt
source-wordcount: '642'
ht-degree: 61%

---

# [!DNL Oracle Responsys]-Verbindung

## Übersicht {#overview}

[Responsys](https://www.oracle.com/cx/marketing/campaign-management/)[!DNL Oracle] ist ein Enterprise-E-Mail-Marketing-Tool für kanalübergreifende Marketing-Kampagnen, das von angeboten wird und der Personalisierung von Interaktionen über E-Mail, Mobile, Display und Social Media hinweg dient.

So senden Sie Segmentdaten an [!DNL Oracle Responsys], müssen Sie zuerst [Verbindung zum Ziel herstellen](#connect-destination) in Adobe Experience Platform und dann [Datenimport einrichten](#import-data-into-responsys) von Ihrem Speicherort zu [!DNL Oracle Responsys].

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B. E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm „Auswählen der Profilattribute“ im [Zielaktivierungs-Workflow](../../ui/activate-batch-profile-destinations.md#select-attributes) festgelegt. |
| Exporthäufigkeit | **[!UICONTROL Batch]** | Batch-Ziele exportieren Dateien in Schritten von drei, sechs, acht, zwölf oder vierundzwanzig Stunden auf nachgelagerte Plattformen. Weitere Informationen finden Sie unter [Batch-Datei-basierte Ziele](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## IP-Adressen-Zulassungsliste {#allow-list}

Beim Einrichten von E-Mail-Marketing-Zielen mit SFTP-Speicher empfiehlt Adobe, bestimmte IP-Bereiche zu Ihrer Zulassungsliste hinzuzufügen.

Siehe [IP-Adressen-Zulassungsliste für SFTP-Ziele](../cloud-storage/ip-address-allow-list.md) , wenn Sie Ihrer Zulassungsliste Adobe-IPs hinzufügen müssen.

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die [Zugriffsberechtigung](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**. Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor.

Dieses Ziel unterstützt die folgenden Verbindungstypen:

* **[!UICONTROL SFTP mit Kennwort]**
* **[!UICONTROL SFTP mit SSH-Schlüssel]**

### Verbindungsparameter {#parameters}

Beim [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* Für **[!UICONTROL SFTP mit Kennwort]** -Verbindungen, müssen Sie Folgendes bereitstellen:
   * [!UICONTROL Domain]
   * [!UICONTROL Port]
   * [!UICONTROL Benutzername]
   * [!UICONTROL Passwort]
* Für **[!UICONTROL SFTP mit SSH-Schlüssel]** -Verbindungen, müssen Sie Folgendes bereitstellen:
   * [!UICONTROL Domain]
   * [!UICONTROL Port]
   * [!UICONTROL Benutzername]
   * [!UICONTROL SSH-Schlüssel]
* Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um eine Verschlüsselung mit PGP/GPG zu Ihren exportierten Dateien unter dem **[!UICONTROL Schlüssel]** Abschnitt. Ihr öffentlicher Schlüssel muss als eine mit [!DNL Base64] verschlüsselte Zeichenfolge verfasst sein.
* **[!UICONTROL Name]**: Wählen Sie einen passenden Namen für Ihr Ziel.
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung für Ihr Ziel ein.
* **[!UICONTROL Ordnerpfad]**: Geben Sie den Pfad an Ihrem Speicherort an, an dem Platform Ihre Exportdaten als CSV-Dateien hinterlegt.
* **[!UICONTROL Dateiformat]**: Auswählen **CSV** , um CSV-Dateien an Ihren Speicherort zu exportieren.

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**. Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](../../ui/activate-batch-profile-destinations.md).

### Zielattribute {#destination-attributes}

Beim Aktivieren von Segmenten für dieses Ziel empfiehlt Adobe, eine eindeutige Kennung aus Ihrem [Vereinigungsschema](../../../profile/home.md#profile-fragments-and-union-schemas). Wählen Sie die eindeutige Kennung und alle anderen XDM-Felder aus, die Sie an das Ziel exportieren möchten. Weitere Informationen finden Sie unter [Best Practices beim Aktivieren von Zielgruppen für E-Mail-Marketing-Ziele](overview.md#best-practices).

## Exportierte Daten {#exported-data}

Für [!DNL Oracle Responsys]-Ziele erstellt Platform eine `.csv`-Datei an dem von Ihnen angegebenen Speicherort. Weitere Informationen zu den Dateien finden Sie unter [Segmentaktivierung überprüfen](../../ui/activate-batch-profile-destinations.md#verify) im Tutorial zur Segmentaktivierung.

## Datenimport einrichten in [!DNL Oracle Responsys] {#import-data-into-responsys}

Nach Anschluss [!DNL Platform] auf [!DNL SFTP] speichern, müssen Sie den Datenimport von Ihrem Speicherort zu [!DNL Oracle Responsys]. Informationen dazu finden Sie unter [Kontakte oder Konten importieren](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) im [!DNL Oracle Responsys Help Center].
