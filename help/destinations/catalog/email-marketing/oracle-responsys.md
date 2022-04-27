---
keywords: email;Email;e-mail;email destinations;oracle responsys destination
title: Oracle Responsys-Verbindung
description: Responsys ist ein Enterprise-E-Mail-Marketing-Tool für kanalübergreifende Marketing-Kampagnen, das von Oracle angeboten wird und der Personalisierung von Interaktionen über E-Mail, Mobile, Display und Social Media hinweg dient.
exl-id: 70f2f601-afee-4315-bf7a-ed2c92397ebe
source-git-commit: 0006c498cd33d9deb66f1d052b4771ec7504457d
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 25%

---

# [!DNL Oracle Responsys]-Verbindung

## Übersicht {#overview}

[Responsys](https://www.oracle.com/cx/marketing/campaign-management/)[!DNL Oracle] ist ein Enterprise-E-Mail-Marketing-Tool für kanalübergreifende Marketing-Kampagnen, das von angeboten wird und der Personalisierung von Interaktionen über E-Mail, Mobile, Display und Social Media hinweg dient.

So senden Sie Segmentdaten an [!DNL Oracle Responsys], müssen Sie zuerst [Verbindung zum Ziel herstellen](#connect-destination) in Adobe Experience Platform und dann [Datenimport einrichten](#import-data-into-responsys) von Ihrem Speicherort zu [!DNL Oracle Responsys].

## Exportart und -frequenz {#export-type-frequency}

Informationen zum Zielexporttyp und zur Häufigkeit finden Sie in der unten stehenden Tabelle.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B.: E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm Profilattribute im [Zielaktivierungs-Workflow](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Exporthäufigkeit | **[!UICONTROL Batch]** | Batch destinations export files to downstream platforms in increments of three, six, eight, twelve, or twenty-four hours. Read more about [batch file-based destinations](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## IP-Adressen-Zulassungsliste {#allow-list}

Beim Einrichten von E-Mail-Marketing-Zielen mit SFTP-Speicher empfiehlt Adobe, bestimmte IP-Bereiche zu Ihrer Zulassungsliste hinzuzufügen.

Siehe [IP-Adressen-Zulassungsliste für Cloud-Speicher-Ziele](../cloud-storage/ip-address-allow-list.md) , wenn Sie Ihrer Zulassungsliste Adobe-IPs hinzufügen müssen.

## Herstellen einer Verbindung mit der Datenbank {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele verwalten]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor.

This destination supports the following connection types:

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
   * [!UICONTROL SSH Key]
* Optionally, you can attach your RSA-formatted public key to add encryption with PGP/GPG to your exported files under the **[!UICONTROL Key]** section. Ihr öffentlicher Schlüssel muss als [!DNL Base64] kodierter String.
* **[!UICONTROL Name]**: Wählen Sie einen passenden Namen für Ihr Ziel.
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung für Ihr Ziel ein.
* **[!UICONTROL Ordnerpfad]**: Geben Sie den Pfad an Ihrem Speicherort an, an dem Platform Ihre Exportdaten als CSV-Dateien hinterlegt.
* **[!UICONTROL Dateiformat]**: Auswählen **CSV** , um CSV-Dateien an Ihren Speicherort zu exportieren.

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

See [Activate audience data to batch profile export destinations](../../ui/activate-batch-profile-destinations.md) for instructions on activating audience segments to this destination.

### Zielattribute {#destination-attributes}

Beim Aktivieren von Segmenten für dieses Ziel empfiehlt Adobe, eine eindeutige Kennung aus Ihrem [Vereinigungsschema](../../../profile/home.md#profile-fragments-and-union-schemas). Wählen Sie die eindeutige Kennung und alle anderen XDM-Felder aus, die Sie an das Ziel exportieren möchten. Weitere Informationen finden Sie unter [Best Practices beim Aktivieren von Zielgruppen für E-Mail-Marketing-Ziele](overview.md#best-practices).

## Exportierte Daten {#exported-data}

Für [!DNL Oracle Responsys] Ziele, erstellt Platform eine `.csv` -Datei in dem von Ihnen angegebenen Speicherort gespeichert. Weitere Informationen zu den Dateien finden Sie unter [Segmentaktivierung überprüfen](../../ui/activate-batch-profile-destinations.md#verify) im Tutorial zur Segmentaktivierung.

## Set up data import into [!DNL Oracle Responsys] {#import-data-into-responsys}

Nach Anschluss [!DNL Platform] auf [!DNL SFTP] speichern, müssen Sie den Datenimport von Ihrem Speicherort zu [!DNL Oracle Responsys]. To learn how to accomplish this, see [Importing contacts or accounts](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) in the [!DNL Oracle Responsys Help Center].
