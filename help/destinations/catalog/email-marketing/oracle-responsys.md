---
keywords: Email;E-Mail;E-Mail;E-Mail-Ziele;Oracle Responsys-Ziel
title: Oracle Responsys-Verbindung
description: Responsys ist ein Enterprise-E-Mail-Marketing-Tool für kanalübergreifende Marketing-Kampagnen, das von Oracle angeboten wird und der Personalisierung von Interaktionen über E-Mail, Mobile, Display und Social Media hinweg dient.
exl-id: 70f2f601-afee-4315-bf7a-ed2c92397ebe
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 42%

---

# [!DNL Oracle Responsys]-Verbindung

## Übersicht {#overview}

[Responsys](https://www.oracle.com/cx/marketing/campaign-management/) ist ein E-Mail-Marketing-Tool für kanalübergreifende Marketing-Kampagnen, das von [!DNL Oracle] zur Personalisierung von Interaktionen in E-Mail, Mobile, Display und Social Media angeboten wird.

Um Zielgruppendaten an [!DNL Oracle Responsys] zu senden, müssen Sie zunächst [Verbindung zum Ziel herstellen](#connect-destination) in Adobe Experience Platform und dann [einen Datenimport einrichten](#import-data-into-responsys) von Ihrem Speicherort in [!DNL Oracle Responsys].

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Arten von Zielgruppen Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die über den Experience Platform-[&#x200B; (Segmentierungs-Service) generiert &#x200B;](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/audience-portal.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
|---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B. E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm „Auswählen der Profilattribute“ im [Zielaktivierungs-Workflow](../../ui/activate-batch-profile-destinations.md#select-attributes) festgelegt. |
| Exporthäufigkeit | **[!UICONTROL Batch]** | Batch-Ziele exportieren Dateien in Schritten von drei, sechs, acht, zwölf oder vierundzwanzig Stunden auf nachgelagerte Plattformen. Weitere Informationen finden Sie unter [Batch-Datei-basierte Ziele](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## IP-Adressen-Zulassungsliste {#allow-list}

Beim Einrichten von E-Mail-Marketing-Zielen mit SFTP-Speicher empfiehlt Adobe, Ihrer Zulassungsliste bestimmte IP-Bereiche hinzuzufügen.

Siehe [Zulassungsliste von IP-Adressen für SFTP](../cloud-storage/ip-address-allow-list.md)Ziele, wenn Sie Ihrer Zulassungsliste Adobe-IPs hinzufügen müssen.

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL View Destinations]** und **[!UICONTROL Manage Destinations]** Zugriffssteuerungsberechtigungen[. &#x200B;](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor.

Dieses Ziel unterstützt die folgenden Verbindungstypen:

* **[!UICONTROL SFTP with Password]**
* **[!UICONTROL SFTP with SSH Key]**

### Verbindungsparameter {#parameters}

Beim [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* Für **[!UICONTROL SFTP with Password]** müssen Sie Folgendes angeben:
   * [!UICONTROL Domain]
   * [!UICONTROL Port]
   * [!UICONTROL Username]
   * [!UICONTROL Password]
* Für **[!UICONTROL SFTP with SSH Key]** müssen Sie Folgendes angeben:
   * [!UICONTROL Domain]
   * [!UICONTROL Port]
   * [!UICONTROL Username]
   * [!UICONTROL SSH Key]
* Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um Ihren exportierten Dateien unter dem Abschnitt **[!UICONTROL Key]** eine Verschlüsselung mit PGP/GPG hinzuzufügen. Ihr öffentlicher Schlüssel muss als eine mit [!DNL Base64] verschlüsselte Zeichenfolge verfasst sein.
* **[!UICONTROL Name]**: Wählen Sie einen relevanten Namen für Ihr Ziel aus.
* **[!UICONTROL Description]**: Geben Sie eine Beschreibung für Ihr Ziel ein.
* **[!UICONTROL Folder Path]**: Geben Sie den Pfad an Ihrem Speicherort an, an dem Experience Platform Ihre Exportdaten als CSV-Dateien ablegt.
* **[!UICONTROL File Format]**: Wählen Sie **CSV**, um CSV-Dateien an Ihren Speicherort zu exportieren.

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Experience Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, wählen Sie **[!UICONTROL Next]** aus.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Zum Aktivieren von Daten benötigen Sie die **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** und **[!UICONTROL View Segments]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die **[!UICONTROL View Identity Graph]** Zugriffssteuerungsberechtigung[&#x200B; &#x200B;](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen [&#x200B; Aktivieren von Zielgruppen für dieses Ziel finden Sie &#x200B;](../../ui/activate-batch-profile-destinations.md)Aktivieren von Zielgruppendaten für Batch-Profil-).

### Zielattribute {#destination-attributes}

Beim Aktivieren von Zielgruppen für dieses Ziel empfiehlt Adobe die Auswahl einer eindeutigen Kennung aus Ihrem [Vereinigungsschema](../../../profile/home.md#profile-fragments-and-union-schemas). Wählen Sie die eindeutige Kennung und alle anderen XDM-Felder aus, die Sie an das Ziel exportieren möchten. Weitere Informationen finden Sie unter „Best [&#x200B; beim Aktivieren von Zielgruppen für E-Mail-Marketing-Ziele](overview.md#best-practices).

## Exportierte Daten {#exported-data}

Für [!DNL Oracle Responsys] Ziele erstellt Experience Platform eine `.csv`-Datei an dem von Ihnen angegebenen Speicherort. Weitere Informationen zu den Dateien finden Sie unter [Zielgruppenaktivierung überprüfen](../../ui/activate-batch-profile-destinations.md#verify) im Tutorial zur Zielgruppenaktivierung.

## Einrichten des Datenimports in [!DNL Oracle Responsys] {#import-data-into-responsys}

Nachdem Sie [!DNL Experience Platform] mit Ihrem [!DNL SFTP] Speicher verbunden haben, müssen Sie den Datenimport von Ihrem Speicherort in [!DNL Oracle Responsys] einrichten. Informationen hierzu finden Sie unter [&#x200B; von Kontakten oder Konten &#x200B;](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) der [!DNL Oracle Responsys Help Center].
